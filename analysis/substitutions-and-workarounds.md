# Substitutions and workarounds

How to run Problems 1–9 without buying everything. Companion to the
[parts audit](problems-01-09-parts-audit.md), which says what the book asks for; this says
what you can get away with instead.

## Two principles that collapse most of the shopping list

**1. Nominal values don't matter. Known values do.**

Every calculation in these problems takes R, L and C as *inputs*. Nothing requires the
resistor to be 300 kΩ — it requires you to know what it actually is. With a good multimeter,
a junk-box 330 kΩ measured at 327.4 kΩ is strictly better than a 300 kΩ you assumed was
300 kΩ. The book specifies exact values because it shipped a parts kit to a class, not
because the physics cares.

Where this stops being true: the capacitor in Problems 3 and 4, if your meter has no
capacitance range. And anything where the value sets a *ratio between timescales* rather than
a number you plug in — see Problem 4 below.

**2. Understand what the problem is teaching, then scale freely.**

Several of these problems are built around a *ratio* of time constants, not around specific
frequencies. Where that's true you can slide the whole design down in frequency to fit
equipment you already have. Called out per-problem below.

---

## Problem 2: the battery — can AAA cells work?

**Yes, and a 9 V alkaline is probably the best single substitute.**

### What the problem actually needs

Problem 2 measures the battery's own source resistance from how its terminal voltage droops
under load. So the battery is the *device under test*, not a power supply. The only real
requirements are:

- **Non-trivial internal resistance** — enough droop to measure. This is why your bench
  supply fails: it's regulated, `Rs ≈ 0`, and you'd plot a flat line.
- **Load currents that are a sane fraction of its capacity** — so it doesn't visibly
  discharge while you're taking readings.
- **Primary chemistry preferred.** Alkaline has *high* internal resistance, which makes the
  effect bigger and easier to see. NiMH and Li-ion are engineered for *low* internal
  resistance, which makes them worse subjects here.

Nothing requires 12 V, and nothing requires 0.8 A-hr.

### Option A — a 9 V alkaline (recommended)

One part, a snap connector, no holder. And the numbers land well:

| Resistors (510 Ω) | Current at 9 V |
|---|---|
| 1 | 17.6 mA |
| 2 | 35.3 mA |
| 3 | 52.9 mA |
| 4 | **70.6 mA** |

Part B asks for an equivalent circuit "when the current is in the neighborhood of 75 mA" —
that's the four-resistor point, so you use the full set exactly as written.

Two bonuses:

- **Dissipation drops to 9²/510 = 0.16 W per resistor**, comfortably inside 1/4 W. The
  recommendation to buy 1/2 W parts was driven by the 12 V case; on 9 V it evaporates and
  any junk-box 1/4 W resistors will do.
- A 9 V alkaline's internal resistance is on the order of ohms and climbs steeply as it
  discharges, so Part B's punchline — that the Thevenin model "will not be accurate at
  currents much lower or higher than this" — shows up *more* clearly than with an SLA.

Cost: a 9 V battery costs less than the resistors.

### Option B — 8 × AAA (or AA) alkaline in a holder

Gets you to ~12 V so the book's numbers transfer verbatim, and AAA capacity (~1 A-hr at low
drain) is close enough to the specified 0.8 A-hr that Part C's battery-life arithmetic comes
out in the same place. Series internal resistance of eight alkaline cells is a couple of
ohms, giving a clear droop.

AA is the better choice if you want the pack to double as a field supply for the finished
radio — the 40B wants 10–16 V, and eight alkaline cells start near 12.4 V and sag below 10 V
well before they're exhausted. Note that at 12 V the 0.28 W per resistor problem comes back.

### Option C — the specified 12 V, 0.8 A-hr SLA

Worth it only if you want a proper field battery for the finished radio anyway. Be aware the
droop will be *smaller* than with alkaline (SLA internal resistance is a few hundred mΩ), and
what you're mostly measuring is electrochemical polarisation rather than ohmic resistance —
which is exactly why the book insists on waiting two minutes after each change for the
voltage to settle. Take that instruction seriously on any chemistry.

### An embedded-engineer upgrade

The two-minute settle is a transient worth *seeing*, not just waiting out. Log the terminal
voltage with an MCU ADC — a few samples a second for the full two minutes after each resistor
goes in — and you get the polarisation curve instead of a single settled number. That's more
than the book asks for and it's the kind of thing your day job makes cheap. Watch the ADC
reference: you need an absolute voltage, so use an external reference or calibrate against
the DMM, and divide 12 V down to the ADC range with a measured divider.

---

## Problems 3–6: passives you can substitute freely

| Book calls for | Substitute | Why it's fine |
|---|---|---|
| 300 kΩ (P3) | 2 × 150 kΩ in series, 3 × 100 kΩ, or one 330 kΩ | Sets `τ` with C, and appears in a divider with the scope's 1 MΩ. Any value in the 100 kΩ–1 MΩ range works; just measure it and use the measured number. Staying well above 50 Ω and well below 1 MΩ keeps the book's two simplifications (ignore the generator's 50 Ω, don't swamp the scope) valid. |
| 3.0 kΩ (P4) | **3.3 kΩ** | E12 standard. Changes `τ` from 30 µs to 33 µs, which changes nothing — see the ratio note below. |
| 2 × 2 kΩ (P5, P6) | 1.8 kΩ or 2.2 kΩ | One limits base current, one is the collector load. Neither value is critical; the switch saturates either way. |
| 4 × 510 Ω (P2) | Any four roughly-equal resistors, 400–600 Ω | Measure each. They don't even need to match — you're computing total current, so unequal values just mean summing conductances. |
| 10 nF (P3, P4) | Any 0.01 µF you have | **The one place to be careful.** Ceramic discs run ±10–20%, and Problems 3C/3D compare measured against calculated. If your DMM has a capacitance range, measure it and the tolerance stops mattering. If it doesn't, buy a 5% film cap — it's pennies and removes a 20% unknown from the answer. |
| 1 mH choke (P5, P6) | Any 100 µH–10 mH inductor | `τ = L/R`; pick the square-wave frequency so `τ` is much shorter than a half-period and the measurement is identical. Do note the DC resistance (~10 Ω for a 1 mH molded part) and include it in R. |
| P2N2222A (P5, P6) | 2N3904, BC547, almost any TO-92 NPN rated ≥ 40 V | Vceo matters here — the inductive spike is deliberately large, and the transistor's breakdown is part of what limits it. Buy a handful of whatever you choose; these are consumable in this experiment. |
| 1N4148 (P4, P6) | Any silicon small-signal diode | Problem 4B's expected answer is a silicon forward drop. A Schottky or germanium changes that number — interesting, but know you've changed it. |
| Non-metallic tuning tool (P8) | A metal driver, used carefully | Adjust, withdraw the driver, *then* read the scope. Your hand and the driver add capacitance that shifts resonance while you're touching it. Tedious but workable. |
| 50 Ω feedthrough terminator (P5) | A 51 Ω resistor at the scope input | Fine at 1 kHz. **Not** fine for Problem 8 at 7–15 MHz, where lead inductance stops being negligible. Buy the real terminator before Problem 8. |

### Problem 4 is about ratios, not frequencies

The 1 MHz carrier is not sacred. The problem is built on three timescales:

    carrier period (1 µs)  ≪  τ = RC (30 µs)  ≪  modulation period (1 ms)

Parts A and C exist to probe each inequality — A checks that `τ` is short enough to follow
the audio, C deliberately drops the carrier to 100 kHz so `τ` *stops* being long enough and
droop appears. **Any set of values preserving those ratios teaches the same thing.**

Scaled by 10, which is what a 1 MSa/s DAC can synthesise directly at ten samples per cycle:

| | Book | ÷10 |
|---|---|---|
| Carrier | 1 MHz | **100 kHz** |
| `τ = RC` | 30 µs | **300 µs** — 30 kΩ with the 10 nF from Problem 3 |
| Modulation | 1 kHz | **100 Hz** |
| Part C carrier | 100 kHz | **10 kHz** |

Both ratios are preserved exactly: `τ / T_carrier = 30`, `T_mod / τ = 33`, and Part C still
lands at `τ / T_carrier = 3`, which is where the droop becomes visible.

This is also why 3.3 kΩ instead of 3.0 kΩ is a non-event: 33 µs sits in the same place
between the same two timescales.

---

## Where the MCU dev kits genuinely help

### Square waves for Problems 3, 5 and 6 — yes

These need 20 Hz, 1 kHz, 30 kHz and 100 kHz square waves. A hardware timer produces those
with better frequency accuracy than any function generator you'd buy, and you already know
how to write it.

Two mismatches to handle:

- **Unipolar, not bipolar.** The book's generator swings symmetrically about 0 V, so "the
  time to reach 0 V" is the half-way point. A 0–3.3 V MCU output's half-way point is 1.65 V.
  Same measurement, different cursor position — Problem 3C's `t₂ = τ ln 2` is unchanged.
- **Source impedance is not 50 Ω** — it's the pin's Rds(on), maybe 25–50 Ω, nonlinear, and
  process-dependent. For Problem 5 this matters a lot (`τ = L/R`, and R is *made of* the
  source impedance). Fix: drive through a 74AC-family buffer (Rds(on) ~5–10 Ω) into a series
  resistor chosen to bring the total to 50 Ω — then **measure the result** with the
  feedthrough-divider method in [test-equipment.md](test-equipment.md#bench-calibration-worth-doing-on-any-generator).
  Or don't bother forcing 50 Ω: measure whatever R you have and use that number.

### AM for Problem 4 — yes, and better than brute force

The obvious approach is to synthesise the whole modulated waveform sample by sample. On the
STM32U5G9 that works but caps the carrier at 100 kHz, because the DAC's characterised
sampling rate is 1 MSa/s and you need roughly ten samples per carrier cycle. See
[`../firmware/README.md`](../firmware/README.md#dac-capability-verified-against-the-datasheet)
for the numbers.

**There's a much better trick.** AM is just `carrier × envelope`, and nothing says the
multiplication has to happen in software:

- Generate the **envelope** with the DAC at a few kSa/s — a 100 Hz sine, which is so far
  inside the DAC's comfort zone that you get its full 11.3 ENOB and −79 dB THD.
- Generate the **carrier** with a timer as a square wave. At 160 MHz the U5 makes a 1 MHz
  square with 160 counts per cycle, so frequency resolution is a non-issue.
- Multiply them with a **CMOS analog switch** (74HC4066, 74LVC1G66, 74HC4053 — under a
  dollar) chopping the envelope voltage at the carrier rate.

The output is a square carrier whose amplitude tracks the envelope. **That is real AM at the
book's real 1 MHz**, with modulation depth set exactly in software, and the DAC never leaves
its sweet spot.

Does a square carrier break anything? No — an envelope detector charges to the *peak* of
whatever periodic waveform it sees, and every quantity Problem 4 asks about is a peak:

- **Part A**, τ vs the modulation period: unchanged.
- **Part B**, the input-to-output voltage difference: still one diode drop below the peak.
- **Part C**, droop at low carrier frequency: *clearer* with a square carrier, because the
  discharge happens over a well-defined off-period rather than a sinusoidal one.
- **Part D**, 100% modulation and overmodulation distortion: unchanged, provided the envelope
  can actually reach zero — see the buffer trap below.

The harmonic content differs from a sine carrier, which matters for spectrum but not for
envelope detection. If you want the textbook sine, an AD633 multiplier drops into the same
place as the analog switch.

**Two hardware constraints from the datasheet that bite whichever route you take:**

- The DAC's output buffer **cannot output below 0.2 V**, so with the buffer enabled you can
  only reach about 88% modulation and Part D's overmodulation never quite happens. Run the
  buffer **off** for the full 0-to-VREF+ swing.
- With the buffer off the DAC's output impedance is 10–16 kΩ, and with it on the minimum load
  is 5 kΩ — either way it cannot drive Problem 4's 3 kΩ bleeder, especially with a diode
  drawing transient charging current. **Put a rail-to-rail op-amp follower after the DAC.**
  It only carries the envelope, so any jellybean part works.

Chain: `DAC (buffer off) → RRIO follower → analog switch (carrier) → detector`.

### A DDS module for Problems 8 and 9 — partially

An AD9850/AD9851 module (a few dollars, ubiquitous in QRP circles) gives clean sine output
through 7–15 MHz under SPI control. That covers the *frequency* requirements of Problems 8
and 9, and it will later serve as the "calibrated signal generator" the 40B's alignment
procedure asks for.

What it doesn't give you: calibrated amplitude, a defined 50 Ω source, or the ~20 Vpp
open-circuit that Problems 8F and 9F want. So it's a frequency source, not a substitute for a
function generator. If you go this route, the through-reference sweep in
[test-equipment.md](test-equipment.md#bench-calibration-worth-doing-on-any-generator) stops
being optional — it's the only thing that makes Problem 8E's response plot mean anything.

### A frequency counter for the 40B alignment — yes, easily

The 40B's VFO alignment (manual step 2a) wants a counter on a ~2.1 MHz signal. Timer input
capture, gate for a second, done — and more accurate than you need. One caution: probing an
oscillator loads it and pulls its frequency. Buffer with a high-impedance stage or a single
JFET/FET follower rather than hanging an MCU pin off the tank.

---

## What genuinely can't be worked around

- **A regulated bench supply for Problem 2.** Zero source resistance means no experiment.
  Get a battery of some kind.
- **The 50 Ω feedthrough terminator at RF (Problems 8B, 8E).** A leaded resistor's inductance
  is a real error at 15 MHz.
- **Soldering gear for Problems 8 onward.** The 40B board is double-sided with plated-through
  holes; a mistake is genuinely hard to undo. Fine iron, fine solder, wick, and a vise.
- **Amplitude calibration for Problems 8 and 9.** Not a part you can buy your way out of
  either — but the through-reference sweep turns it into a procedure instead of a purchase.
- **The kit's own parts** for Problems 8 and 9: C1, L1, C37, C38, C39 and L6 are the NorCal
  40B's actual components, soldered to the actual board. Nothing to substitute; that's the
  point of those problems.

---

## Revised shopping list, if you want the minimum

Assuming you have a typical embedded engineer's junk box (resistor assortment, some caps,
protoboard) and are willing to measure things:

**Actually necessary:**

- Function generator, or a committed plan for the DIY routes above
- A battery — a 9 V alkaline is enough to do Problem 2 tonight
- BNC 50 Ω feedthrough terminator, 2 × BNC tee, 2 × BNC-to-minigrabber leads
- Soldering iron, fine solder, wick, PCB vise (before Problem 8)
- #26 and #28 enamelled wire (the kit has no slack for a practice toroid wind)

**Worth buying, cheap, removes uncertainty:**

- 10 nF film capacitors, 5% — unless your DMM measures capacitance
- A few TO-92 NPNs and 1 mH chokes — these are consumable in Problems 5 and 6
- Non-metallic tuning tool
- **A CMOS analog switch (74HC4066/74LVC1G66) and a rail-to-rail op-amp** — about a dollar
  between them, and they turn the STM32 DAC into a proper 1 MHz AM source for Problem 4

**Skip unless you don't have them:** the 510 Ω, 300 kΩ, 3 kΩ and 2 kΩ resistors. Any
assortment covers these, and measured junk-box parts are better than assumed nominal ones.
