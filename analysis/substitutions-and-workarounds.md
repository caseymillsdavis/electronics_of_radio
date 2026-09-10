# Substitutions and workarounds

How to run Problems 1–16 without buying everything. Companion to the
[parts audit](problems-01-16-parts-audit.md), which says what the book asks for; this says
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

### The measurement trap: don't trust the per-point arithmetic

Part A asks you to plot current against voltage; it's tempting to skip the plot and just
divide `(Voc − V) / I` at each load point instead. **Don't** — those are not independent
estimates. They all share the single open-circuit reading, and the shared error propagates
unequally:

```
∂R_bat/∂Voc = 1/I
```

so an error in Voc distorts the lightest-load point several times harder than the
heaviest-load one. That manufactures a clean-looking monotone trend in internal resistance out
of one bad reading, and it's easy to mistake for the current-dependence Part B is hinting at.
This is not hypothetical — it happened on the first run, see
[bench results](bench-results.md#the-trap-the-r_bat-column-is-not-four-independent-estimates).

The plot doesn't have this problem: the slope of the fit never uses Voc at all, so it recovers
both the EMF and the resistance from the loaded points alone. If the fitted intercept
disagrees with the measured Voc, **that gap is a result, not an error to average away** — on
alkaline cells it's usually surface charge or relaxation, and it's the cue to re-measure Voc
right after unloading. Which is the same instruction as the two-minute settle, arriving from
the other direction.

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

## Problem 10: you do not need an antenna, and you may not need the transformer

### Part A — the 50 ns pulse is not sacred

What part A actually needs is a pulse **short compared with the round trip**, so the incident
pulse on channel 1 has finished before its reflection arrives. On 10 m of coax the round trip
is about 100 ns, so a 50 ns pulse fits with room to spare — but so does an 80 ns one, and a
longer cable widens the window further. If the generator you want has a minimum pulse width of
80 or 100 ns, **buy 20 m of coax instead of 10 m** and the constraint evaporates. (It also
halves the resonant frequency in Problem 12, which makes that measurement easier too.)

**Better still: don't use a pulse at all.** A real time-domain reflectometer sends a *step*,
not a pulse, and looks at the reflection riding on top of it. Drive the cable with a 20 kHz
square wave and you get the same delay measurement from the edge, with two advantages:

- Every generator has a square wave, so there is no pulse-width spec to satisfy. The **TTL/sync
  output** most generators provide is usually the fastest edge in the box — the FY6900's is
  spec'd at 10 ns, which is sharper than its main output.
- Part D — the open-circuited line — is *clearer* with a step. A pulse shows you a second bump;
  a step shows you the voltage doubling and staying there, which is the thing the problem wants
  you to interpret.

Amplitude is not critical either. Part A measures a **time**, and part C measures a **ratio**.
3.3 V works as well as 5 V.

### Part B — any coax stands in for the antenna cable

Part B is a length measurement on a cable whose length you supposedly don't know. If there's no
antenna up yet, use any offcut of coax with its far end left open, deduce the length from the
delay, then **check it with a tape measure**. That is strictly a better experiment than the
book's: you get to find out whether the method is right, instead of taking its word.

Two spare metres of RG58 with one BNC on it is enough. The 40B's own feedline is the eventual
subject anyway.

### Problem 10C: measuring Z0 without building the box

The book's fixture — a 1:1 transformer so a 1 Ω current-sensing resistor can sit in series
without shorting the scope ground — is the only thing in this chapter you'd have to build.
Three ways round it, cheapest first.

**1. The source-divider method (no parts, uses what you already measured).**

During the first round trip, before any reflection returns, the cable's input looks like a pure
`Z0`. So it forms a plain divider with the generator's own source resistance:

    V_in = V_oc × Z0 / (Rs + Z0)      ⟹      Z0 = Rs × V_in / (V_oc − V_in)

Measure `V_oc` (generator into the scope alone, high-Z) and `V_in` (generator into the cable,
read at the tee) and you're done. `Rs` is the reference resistor, and you were already told to
measure it in
[the bench calibration](test-equipment.md#bench-calibration-worth-doing-on-any-generator) —
which is the same Thevenin measurement, so this costs nothing new. One channel, one tee.

**2. The null method (one part, and the DMM does the work).**

Terminate the far end with a **carbon or cermet potentiometer** — 100 Ω is a good value — and
adjust it until the reflected pulse disappears into the baseline. A matched line has no
reflection, so at the null the pot *is* `Z0`. Unclip it and measure it with the multimeter.

This is the most satisfying version of the experiment and the most in the spirit of this repo:
the answer comes out as a DMM reading rather than a scope estimate, and nulls are far easier to
judge by eye than amplitudes. Use a **non-wirewound** pot and keep the leads stubby — at these
edge rates a wirewound pot is an inductor.

**3. Build the book's fixture (two parts, and you'll want it later anyway).**

A 1:1 wideband transformer is a few bifilar turns of #26 on a small #43 ferrite — an FT37-43 or
a BN-43-2402 binocular core, a dollar or two. Six to ten bifilar turns gives you flat response
from well under 1 MHz to well over 100 MHz, which covers a 50 ns pulse comfortably. The 1 Ω
resistor can be anything you can measure; two 2 Ω in parallel is fine, and the "metal box" is
any grounded enclosure — an Altoids tin with BNCs in it is the traditional answer.

**Do not use the kit's FT37-43.** That core is T1, and Problem 15 needs it.

Current-sensing transformers are genuinely useful test gear afterwards, so this is the option
to pick if you want the thing rather than just the answer.

---

## Problem 12: any cable length works

The measurement is `f₀ = v/4l` on an open-circuited line, so the resonance moves with whatever
cable you have. 20 m → 2.5 MHz, 10 m → 5 MHz, 5 m → 10 MHz. All are inside the range
Problems 8 and 9 already demanded of the generator, so **there is nothing to buy and nothing
to scale**.

Longer is mildly better: it lowers `f₀`, raises the total loss, and therefore deepens the
minimum you're hunting in part B. If you're buying coax for Problem 10 anyway, buying 20 m
rather than 10 m costs a few dollars and makes both problems easier.

The one thing you cannot substitute is the **scope's input capacitance** in part C — that's
the quantity being measured against. Look it up (it's usually printed by the input jack) rather
than guessing, and expect 13–20 pF.

---

## Problem 14: crystal spacers, bare wire, and the can grounds

Three small kit gaps, none of them a blocker.

**Plastic crystal spacers** — Appendix A doesn't list any. Their whole job is to keep the metal
can off the board and off the leads. Substitute: a punched disc of thin polyester or Kapton
tape, a slice of heatshrink slid down each lead, or a scrap of the anti-static foam the ICs
arrive in. Anything insulating and about a millimetre thick.

**Bare #22 wire** for connecting the crystal cans to ground — the kit ships #26 and #28
*enamelled* wire only, and enamel is exactly what you don't want here. Strip a length of solid
22 AWG hookup wire, or use a cut-off resistor lead (they're usually 0.6 mm ≈ #22 and they solder
beautifully). You need bare #22 again in Problem 16, so cut a few extra.

**The ground hole between the crystals may not exist on the 40B.** The book relies on a small
hole in the 40A board between X2 and X3. If the 40B doesn't have one, ground the can wire to any
convenient ground pad or to the board-edge ground the manual uses elsewhere — the point is
simply that the cans must not float, not where the wire lands.

Take the book's soldering advice seriously either way: get the can tops properly hot before
applying solder, or the bead lifts off.

---

## Problem 14K: 60 dB of dynamic range at 4.9 MHz

**This is the hardest measurement in the batch, and the only place in Chapters 4–6 where a
workaround is close to mandatory.**

Part K asks for a loss plot 60 dB deep. With a 2.0 Vpp drive and a filter whose minimum loss is
a few dB, the top of the plot is a few hundred millivolts at the 200 Ω load — so the bottom of
the plot is **sub-millivolt at 4.9 MHz**. No general-purpose scope reads that off the screen.
The book half-admits this by having you switch in a 10 MHz filter and by making the plot
relative.

Four options, in increasing order of how much they help.

**1. Scope averaging (free).** The signal is periodic and coherent; the noise isn't. Averaging
16–64 acquisitions buys you roughly 12–18 dB of noise floor. It needs a rock-steady trigger, so
**use the generator's sync output into external trigger** rather than triggering on the tiny
signal itself — which won't work at all once you're deep in the stop band. You already have the
sync cable on the accessories list for Problems 3 and 4.

**2. The scope's FFT (free).** Reading the amplitude of one bin at the drive frequency rejects
everything outside a narrow bandwidth, which is precisely the problem. On a modern scope with
FFT averaging this is often worth another 10–20 dB over a time-domain reading, and it degrades
gracefully — you can see the noise floor you're approaching.

**3. An AD8307 logarithmic detector (a few dollars, and the right answer).** The AD8307 is a
DC-to-500 MHz log amp with about **92 dB of range** and an output of roughly 25 mV/dB. Feed it
the filter output, read the DC output with the multimeter, and the entire 60 dB plot becomes a
sequence of comfortable DC voltages — about 1.5 V of span. Modules are ubiquitous in QRP
circles.

Two things to get right, because this is test equipment and inherits the
measure-don't-assume rule:

- **Calibrate the slope and intercept yourself.** Feed it known levels from the generator
  (which you can set accurately at the top of the range) and fit `V_out = m·P_dBm + c`. Write
  `m` and `c` down next to wherever you use them. The datasheet's typical values are a starting
  point, not a calibration.
- **Mind the input impedance.** The AD8307 presents about 1.1 kΩ; the filter wants to see
  200 Ω. Keep the 200 Ω load resistor in place and let the detector sit across it, so the
  filter's termination is still what the design assumes.

**4. The same detector plus an MCU and a DDS module — a scalar network analyser.** At which
point part K, part A's six-crystal hunt, and Problem 13A and 16A all stop being manual work.
See below.

---

## The instrument this batch is really asking for: a scalar network analyser

Look at what Chapters 4–6 keep demanding:

| | Sweep | Points | By hand? |
|---|---|---|---|
| P12B/D | resonance and √2 bandwidth near 5 MHz | tens | tolerable |
| P13A | loss at 7 and 14 MHz | 2 | trivial |
| **P14A** | find `f₀` to 1 Hz, **six times** | hundreds | grim |
| **P14C** | `fu`, `fl` around a ~200 Hz-wide dip | dozens | grim |
| **P14K** | 2,500 Hz span at 50 Hz steps, 60 dB deep | 50+ | grim, and at the edge of what a scope can read |
| P16A | maximum output, then 3-dB bandwidth at 7 MHz | tens | tolerable |

Three of those are hundreds of manual readings of a millivolt-level signal. That is exactly the
job an **AD9850/AD9851 DDS module + AD8307 log detector + one of the STM32 boards** does, for
something like $15 in parts:

- **DDS** — an AD9850 clocked at 125 MHz has a tuning resolution of `125e6 / 2³² = 0.029 Hz`, so
  Problem 14's 1 Hz steps are three orders of magnitude inside its capability. SPI-driven, and
  the repo
  [already planned to buy one](#a-dds-module-for-problems-8-and-9--partially) for Problems 8
  and 9 and the 40B's alignment.
- **Log detector** — turns 60 dB into 1.5 V, as above.
- **MCU** — steps the DDS, reads the ADC, dumps `frequency, dBm` over the serial port. The plot
  is then a two-line script instead of an evening with graph paper.

**What it does not give you** is absolute frequency accuracy: the AD9850 module's 125 MHz clock
is a plain crystal oscillator, ±20–50 ppm, which is ±100–250 Hz at 4.9 MHz. That sounds fatal
for Problem 14 and isn't, because **everything Problem 14 computes is a difference or a ratio**
— crystal-to-crystal matching, `Δf = fu − fl`, and an `L·C` product checked against your own
measured `f₀`. A constant offset cancels out of all of them. What matters is **stability over
the session**, so let it warm up and re-measure the first crystal last as a drift check. If you
later want absolute accuracy, calibrate the module's clock against anything you trust and store
the correction as a constant — written down, per the
[firmware conventions](../firmware/README.md#conventions).

This is the obvious next firmware project in this repo, and it serves five problems plus the
40B's alignment. It isn't written yet — it needs bench access to calibrate, and a remote session
can't flash the board.

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

### The 50 ns pulse for Problem 10 — yes, and better than a budget generator

This is the one place where the dev kit beats a bought instrument outright. At 160 MHz a timer
tick is **6.25 ns**, so a 50 ns pulse is 8 ticks and a 20 kHz repetition rate is 8,000 — both
exact, with no jitter beyond the crystal's own. A generator with an 80 ns minimum pulse width
cannot do this at all; the MCU does it to the tick.

Three things to handle:

- **Edge rate.** Set the GPIO to its highest output-speed setting. You want a rise time short
  compared with the 50 ns pulse, which the pin will manage into a light load — but 50 Ω is not
  a light load, so drive through a **74LVC1G17 or 74AC14 buffer** rather than straight off the
  pin. This is the same buffer the repo already recommends for
  [Problem 5's square waves](#square-waves-for-problems-3-5-and-6--yes).
- **Source impedance.** Add a series resistor to bring buffer plus resistor to 50 Ω, then
  measure the total — don't assume it. If you use the
  [source-divider method](#problem-10c-measuring-z0-without-building-the-box) for part C, this
  resistance *is* your reference standard, so it needs to be a measured number.
- **Amplitude.** 3.3 V instead of 5 V. Part A measures a time and part C measures a ratio, so
  this changes nothing.

Worth doing even if you buy a generator with pulse mode: it's an hour's work, it's the natural
first project for `firmware/`, and it gives you a reference edge whose timing you can trust
absolutely.

### A DDS module for Problems 8 and 9 — partially

An AD9850/AD9851 module (a few dollars, ubiquitous in QRP circles) gives clean sine output
through 7–15 MHz under SPI control. That covers the *frequency* requirements of Problems 8
and 9, and it will later serve as the "calibrated signal generator" the 40B's alignment
procedure asks for.

What it doesn't give you: calibrated amplitude, a defined 50 Ω source, or the ~20 Vpp
open-circuit that Problems 8F and 9F want. So it's a frequency source, not a substitute for a
function generator.

**It becomes much more than that in Chapter 5.** Paired with a log detector it turns into the
[scalar network analyser](#the-instrument-this-batch-is-really-asking-for-a-scalar-network-analyser)
that Problems 13A, 14A, 14C, 14K and 16A all want, and its 0.03 Hz tuning resolution is what
makes Problem 14's 1 Hz steps possible at all. If you were on the fence about buying one for
Problems 8 and 9, Chapter 5 settles it. If you go this route, the through-reference sweep in
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
  point of those problems. The same goes for L7, L8, C45–C47 and J1 (Problem 13); X1–X4,
  C9–C14 and L4 (Problem 14); T1 and R14 (Problem 15); and T2, T3, C2 and C4 (Problem 16).
- **A length of coax, for Problems 10 and 12.** There is no substitute for a transmission
  line, and the kit contains none. It is also the cheapest item in this batch.
- **The 40B schematic, for Problem 13.** Not a purchase — it's Appendix D of a manual you
  already have — but the problem cannot be done correctly without knowing which end of an
  asymmetric filter faces the power amplifier.
- **Some way of reading 60 dB of dynamic range at 4.9 MHz** for Problem 14K. Scope averaging or
  an FFT may just get you there; a log detector definitely does. What you cannot do is read
  sub-millivolt signals off a scope screen and call it a measurement.

---

## What you can skip buying

The order itself lives in **[shopping-list.md](shopping-list.md)**. This section records the
*judgment calls* behind it — the things a parts audit says to buy that a junk box and a
multimeter make unnecessary.

**Skip if you own a resistor assortment:** the 510 Ω, 300 kΩ, 3 kΩ, 2 kΩ, 150 Ω, 200 Ω, 1 kΩ and
1.5 kΩ. Every one is a standard E24 value, and a measured junk-box part beats an assumed nominal
one. Several of them (Problems 14–16) get soldered in and thrown away, so tolerance is doubly
irrelevant.

**Skip the capacitor assortment entirely.** Problems 1–16 need exactly one breadboard capacitor
value — 10 nF, in Problems 3 and 4. Everything else is on the radio board and ships in the kit.
Buy five 10 nF film caps; the tolerance only matters if your DMM has no capacitance range.

**Skip the battery.** Problem 2 is done, on depleted AAAs; high internal resistance is what makes
the droop measurable, so the dead-battery bag was the right source rather than a compromise.

**Skip *Puff*** — free alternatives are in
[test-equipment.md](test-equipment.md#puff-and-what-to-use-instead).

**Skip the book's Problem 10C fixture** (FT37-43 ferrite + 1 Ω + metal box). Two of the three
alternatives need no parts at all; buy it because current transformers are useful afterwards,
not because the problem forces you to.

**Don't skip:** the function generator (or a committed plan for the DIY routes above), the coax
for Problems 10 and 12, the BNC interconnect, and soldering gear before Problem 8. Those have no
workaround in this repo.
