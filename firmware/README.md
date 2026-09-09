# Firmware

MCU code that stands in for test equipment while working through *The Electronics of Radio*.
Rationale and per-problem detail live in
[`../analysis/substitutions-and-workarounds.md`](../analysis/substitutions-and-workarounds.md#where-the-mcu-dev-kits-genuinely-help).

## Layout

One directory per **instrument**, not per problem — a square-wave source serves Problems 3, 5
and 6, and duplicating it per problem would guarantee three divergent copies. Each directory
names the problems it serves in its own README.

```
firmware/
  <instrument>/
    README.md      what it emulates, which problems use it, how to build and flash,
                   and its calibration constants
    ...            source, build files
```

Candidates identified so far, none written yet:

| Directory | Emulates | Problems |
|---|---|---|
| `siggen-square/` | Square-wave generator, 20 Hz – 100 kHz | 3, 5, 6 |
| `siggen-am/` | AM source, frequency-scaled carrier | 4 |
| `battery-logger/` | Datalogging voltmeter for the polarisation transient | 2 |
| `freq-counter/` | Frequency counter | 40B VFO alignment |
| `pulser-tdr/` | 50 ns pulse / fast-edge source for time-domain reflectometry | 10 |
| `scalar-na/` | Scalar network analyser — DDS sweep + log detector + ADC | 12, 13, 14, 16, 40B alignment |

The last two came out of Chapters 4–6. Rationale for both is in
[`../analysis/substitutions-and-workarounds.md`](../analysis/substitutions-and-workarounds.md#the-instrument-this-batch-is-really-asking-for-a-scalar-network-analyser);
the short version is that `pulser-tdr/` is the one instrument where the dev kit beats a bought
generator outright (a timer tick is 6.25 ns, so a 50 ns pulse is exactly 8 ticks), and
`scalar-na/` replaces several hundred manual scope readings across Problems 14A, 14C and 14K
with a serial dump.

`scalar-na/` needs external hardware — an AD9850/AD9851 DDS module and an AD8307 log detector,
about $15 together — and cannot be finished in a remote session, because its slope and
intercept have to be calibrated against a known signal on the bench.

## Conventions

- **Buildable from the repo root with one documented command.** Put it at the top of the
  directory's README. A future session should not have to reconstruct the invocation.
- **Pin the toolchain.** Name the SDK/HAL and version. "Works on my machine six months ago"
  is the failure mode here.
- **No magic numbers for anything physical.** This firmware is test equipment, so it inherits
  the repo's measure-don't-assume rule: ADC reference voltage, divider ratios, timer clock,
  output series resistance — write the measured value down next to the code with a note on
  how it was measured. A wrong constant here silently corrupts a lab result.
- **State the electrical interface** in the README: output voltage swing, source impedance,
  and whether the signal is unipolar. The book's instruments are bipolar with a 50 Ω source
  and MCU pins are neither, which changes how the measurement is read.
- **Remote sessions can build but not flash** — no USB. Write accordingly, and keep the
  build step runnable without hardware attached.

## Target hardware

**2 × STM32U5G9J-DK1** — Discovery kit for the STM32U5G9NJ (Cortex-M33, 160 MHz max).
Toolchain not yet pinned; do it when the first project is built.

Two boards is a genuinely useful number here: one can be the signal source while the other
does the measuring, without a firmware reflash between the two roles.

### What each planned instrument needs from the silicon

| Instrument | Peripheral | Binding constraint | Blocked on datasheet? |
|---|---|---|---|
| `siggen-square/` | Timer + GPIO | None. 160 MHz timer clock gives 1600 counts per period at 100 kHz — better frequency resolution than a bought generator. | **No — buildable today** |
| `pulser-tdr/` | Timer + GPIO | **Edge rate into 50 Ω**, not timing. 6.25 ns per tick makes a 50 ns pulse exact; driving a real cable needs an external 74LVC1G17/74AC14 buffer and a measured series resistor. | **No — buildable today** |
| `scalar-na/` | SPI + ADC + timer | **Calibration, not silicon.** The DDS sets frequency and the log detector sets amplitude; the MCU only sequences and samples. Needs the log detector's slope and intercept measured on the bench. | **No — but needs hardware to finish** |
| `freq-counter/` | Timer input capture | Accuracy is set by the board's clock source, not the counter. 40B VFO alignment needs ~±500 Hz at 2.1 MHz (±240 ppm), which any crystal beats comfortably. | **No** |
| `battery-logger/` | ADC | Absolute DC accuracy, not speed. A few samples/second is plenty; the error budget is the voltage reference and the divider, not the converter. | Partly — want ADC offset/INL and reference accuracy |
| `siggen-am/` | DAC + DMA + timer trigger | **DAC update rate.** Sets how far Problem 4 has to be scaled down in frequency. See below. | **Yes** |

### DAC capability (verified against the datasheet)

From **DS14102 Rev 5, §5.3.24, tables 115 and 116**. Read from the datasheet, not measured on
the bench.

| Parameter | Value | Why it matters here |
|---|---|---|
| Resolution | 12-bit | Plenty |
| Full-scale settling, buffer ON | 1.90 µs typ, 3 µs max (±1 LSB) | The real speed limit |
| Full-scale settling, buffer OFF | 1.7 µs typ, 3 µs max (±1 LSB, CL = 10 pF) | Barely different — settling is slew-dominated, not accuracy-dominated |
| AC performance | ENOB **11.3 bits**, THD **−79 dB**, SNR 70.6 dB | Characterised at **Fsampling = 1 MHz** (table 116 note 6) |
| Output swing, buffer **ON** | **0.2 V to VDDA − 0.2 V** | **Cannot reach zero** — see the 100%-modulation trap below |
| Output swing, buffer **OFF** | 0 to VREF+ | Full range |
| Load, buffer ON | **RL ≥ 5 kΩ** to VSSA, ≥ 25 kΩ to VDDA | Problem 4's 3 kΩ bleeder **violates this** |
| Output impedance, buffer OFF | 10–16 kΩ, CL ≤ 50 pF | Effectively unusable without an external buffer |
| Gain error | ±0.5% | Fine; calibrate against the DMM anyway |
| Monotonicity | guaranteed to 10 bits only | Irrelevant for a sine, worth knowing |

**There is no explicit maximum-update-rate row.** The defensible design point is **1 MSa/s**,
because that is where ST characterises SNR/THD/ENOB. Faster is untested territory — you can
try it, but measure before trusting it, and note that full-scale settling (1.9 µs typ) is
already longer than a 1 µs sample period, so large code steps will not settle.

**Consequence for direct AM synthesis:** at `N` samples per carrier cycle,
`f_carrier = 1 MSa/s / N`. Ten samples per cycle puts the carrier at **100 kHz** — a factor
of ten below the book's 1 MHz. That is workable (the problem is about ratios, see the
[scaled plan](../analysis/substitutions-and-workarounds.md#problem-4-is-about-ratios-not-frequencies))
but it is not the best use of this particular DAC.

**Two traps the datasheet exposes, both easy to miss:**

1. **Buffer ON cannot output 0 V** — it floors at 0.2 V. Problem 4D needs the envelope to
   reach zero for 100% modulation; with the buffer on you top out near 88% and the
   overmodulation demonstration never quite happens. Use **buffer OFF plus an external op-amp
   follower**: full 0-to-VREF+ swing, and real drive.
2. **Buffer ON needs RL ≥ 5 kΩ.** Problem 4's 3 kΩ bleeder is below that, and the detector
   diode draws hard transient current while charging. The DAC cannot drive that circuit
   directly under any configuration — the follower is not optional.

So the standing recommendation for any DAC work here is **buffer OFF → rail-to-rail op-amp
follower → circuit**. Any jellybean RRIO part does; it only ever carries the envelope, not
the carrier.

### VREFBUF, for the ADC work

Table 117: internal reference buffer, selectable 1.5 / 1.8 / 2.048 / 2.5 V. At VDDA = 3 V,
TJ = 30 °C, 10 µA load, the 2.5 V setting is 2.493–2.507 V — **about ±0.3%**. The 2.5 V
setting needs VDDA ≥ 2.8 V, which a 3.3 V board satisfies.

For `battery-logger/` that's fine, and mostly for a reason worth stating: Problem 2 measures a
*droop* of ~0.1–0.2 V, so what matters is **short-term stability over the minutes of a run**,
not absolute accuracy — and absolute error gets calibrated out against the DMM regardless.
The tempco is not in the excerpt on hand; check it before relying on a long unattended run in
a room that changes temperature.

### Still unread

The excerpt covers §5.3.24 (DAC) and §5.3.25 (VREFBUF) only. **ADC characteristics have not
been read** — resolution and maximum sampling rate per ADC, offset/gain/INL. Not blocking
anything yet, since `battery-logger/` needs DC accuracy rather than speed, but fill it in
before assuming.

### Board-level things to confirm in the board user manual

Independent of the silicon, and more likely to bite first:

- **Are the DAC outputs actually reachable?** DAC1_OUT1/OUT2 are expected on PA4/PA5 (the
  usual STM32 assignment — confirm). A Discovery board this dense spends a lot of pins on the
  display, PSRAM and USB, and those two may be committed or not brought out to a header.
- **What sets VREF+** on this board, and is there a footprint for an external reference?
  Absolute accuracy for `battery-logger/` depends entirely on this.
- **Which pins land on a usable header** — the analysis above is worthless if the signal can
  only be reached at a BGA ball.

## Electrical reality check for any MCU-as-instrument

The book's instruments are bipolar with a 50 Ω source impedance. An MCU pin or DAC output is
neither, and pretending otherwise is how a lab result quietly goes wrong:

- **Unipolar.** 0 to VDDA, not ±V. Every "time to reach 0 V" in the book becomes "time to
  reach the midpoint". The maths is unchanged; the cursor moves.
- **Not 50 Ω.** GPIO output impedance is the pin's Rds(on) — tens of ohms, nonlinear, and
  different for the high and low sides. Where the source impedance is *part of the
  measurement* (Problem 5: `τ = L/R`), don't try to trim it to 50 Ω. Add a series resistor
  large enough to dominate the pin's variability, then measure the total and use the measured
  value.
- **Weak drive.** A DAC output cannot drive Problem 4's 3 kΩ bleeder directly without error.
  An op-amp follower between DAC and circuit fixes both the drive and the isolation from the
  reconstruction filter.
