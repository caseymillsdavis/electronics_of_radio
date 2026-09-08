# Test equipment and shopping list for Problems 1–9

## Function generator — requirements derived from the problems

These are pulled straight out of the problem statements, not from a generic "good starter
generator" list. Numbers in the table are what Problems 1–9 actually ask for.

| # | Requirement | Where it comes from |
|---|---|---|
| 1 | **Sine and square** waveforms | Sq: P3, P5, P6. Sine: P4, P8, P9 |
| 2 | **20 Hz to ≥ 15 MHz** | P3A is 20 Hz; P8E sweeps 1–15 MHz |
| 3 | **50 Ω source impedance**, well controlled | P3B and P8A both do Thevenin arithmetic that assumes exactly 50 Ω |
| 4 | **20 Vpp open-circuit** (= 10 Vpp into 50 Ω) at 1–3 MHz | P8F and P9F both say "amplitude setting of 10 Vpp" |
| 5 | **Internal AM**, 1 MHz carrier, 1 kHz modulating tone, **depth adjustable to 70% and 100%** | P4 intro and P4D |
| 6 | **Sync / trigger output** on BNC | P3 ("use a sync cable from the function generator to trigger the scope"), P4 ("connect a cable from the sync output... and use external triggering") |
| 7 | Amplitude readout referenced to a **50 Ω load** | The book's convention throughout — see below |

Nice to have, not required by Problems 1–9: a second channel, frequency sweep (makes P8E's
1 MHz-interval sweep and P8C/P9C's bandwidth hunt much less tedious), and a built-in
frequency counter.

### Requirement 5 is the one to check first

Problem 4 needs a **1 MHz carrier, amplitude-modulated internally by a 1 kHz sine, at 70%
depth**, then re-set to 100% for part D. Plenty of generators have no modulation at all, and
some offer AM only at a fixed depth — so check for *adjustable* depth with an internal
modulating source before anything else on this list. It is not, however, a price filter:
even the budget DDS boxes tend to spec 0–100%+ depth. See
[the FY6900 section](#is-a-cheap-dds-generator-fy6900-etc-disqualified).

### Requirement 7 is a settings trap worth knowing about now

The book states its convention explicitly on p. 41:

> *"For a function generator with a 50 Ω source resistance, this amplitude, 1 V peak-to-peak,
> is the voltage that we would see if the load were 50 Ω. For an open-circuit load, the
> amplitude is twice this, or 2 Vpp."*

Every "amplitude setting" in the book is the into-50 Ω number. Modern generators let you tell
them what load to assume, and they display accordingly — so **set the output load to 50 Ω**
and the displayed value matches the book's numbers directly. If yours is in High-Z mode
you'll be off by exactly a factor of two everywhere, which is a genuinely easy way to lose
an evening on Problem 3.

### Candidates

| Model family | Notes |
|---|---|
| **Siglent SDG1032X / SDG1032X-Plus** (30 MHz, 2 ch) | Meets everything above. AM with settable source, depth, modulating frequency and waveform; 20 Vpp into high-Z (specified to 10 MHz, which covers the 10 Vpp uses at 1 MHz and 2.8 MHz); sync output on the rear Aux In/Out. The single-channel SDG1022X is the cheaper sibling. This is the safe default. |
| **Rigol DG822 / DG812 / DG1022Z** | Same class, same feature set. Check the specific model's AM depth range and sync output on its datasheet. |
| **Owon AG1022 / AG051** | Cheaper, generally adequate; verify AM depth control before ordering. |
| **FeelTech FY6900, JUNTEK and similar "DDS" boxes** | Meet the requirements on paper, including the AM one. Not disqualified — see [the section below](#is-a-cheap-dds-generator-fy6900-etc-disqualified). |

Verify against the current datasheet before buying — model lineups shift, and I'm going off
published specs rather than something on my bench.

### Is a cheap DDS generator (FY6900 etc.) disqualified?

**No, and "DDS" is not the thing to judge them on.** Direct digital synthesis is how
essentially every modern function generator works, the Siglent and Rigol included. On an
AliExpress listing "DDS" is a marketing word, not a warning label. What separates a FY6900
from an SDG1032X is the analogue output stage, the amplitude calibration, the firmware and
the power supply — not the synthesis method.

There is exactly one artefact that is genuinely DDS-specific and worth naming: a DDS square
wave can only place its edges on DAC clock boundaries, so the period jitters by up to one
clock. On the FY6900 that's the widely-discussed **~4 ns jitter**. Measured against this
book, the shortest thing you time is `t2 ≈ 7 µs` in Problem 5 — four ns is 0.06% of that,
and 2 parts per million of Problem 3's millisecond delays. **Irrelevant here.**

#### The FY6900 against the requirements table

| # | Requirement | FY6900 (published) |
|---|---|---|
| 1 | Sine + square | ✓ |
| 2 | 20 Hz–15 MHz | ✓ (20 MHz model up) |
| 3 | 50 Ω source | ✓ **50 Ω ±10%**, typical |
| 4 | 20 Vpp open circuit at 1–3 MHz | ✓ 1 mVpp–20 Vpp, **spec'd ≤ 10 MHz** |
| 5 | Internal AM, depth settable to 70% and 100% | ✓ **depth 0–120%**, modulating waveform sine/square/triangle/ramp/arb |
| 6 | Sync / trigger output | ✓ SYNC OUT, plus a TTL output (10 ns edges, >3 Vpp) |
| 7 | Amplitude referenced to a 50 Ω load | ✗ **no output-load setting** — see below |

I flagged requirement 5 as the constraint that eliminates budget generators. On the FY6900's
published spec it doesn't — 0–120% depth with a choice of internal modulating waveform is
more than Problem 4 needs. That was reputation talking on my part, and it was wrong.

#### What actually differs: characterisation, not capability

Three things, all of which show up as *uncertainty in your answers* rather than as missing
features:

1. **Source impedance is 50 Ω ±10%.** Mostly harmless — Problem 3B tells you outright to
   ignore the generator's 50 Ω next to 300 kΩ, and in Problem 5 it's ±5 Ω out of ~110 Ω. But
   **Problem 8A deduces the inductor-plus-capacitor resistance essentially as
   `R_LC ≈ Rs × V_in/V_oc`**, so a 10% error in `Rs` is a 10% error in the answer, and it
   propagates into the Q and bandwidth in 8D.
2. **Amplitude flatness over 1–15 MHz is unspecified.** Problem 8E plots filter response
   across that whole span. If the generator droops with frequency you are plotting the
   generator.
3. **No output-load setting.** The 20 Vpp figure looks like an open-circuit number, which
   would make the display *twice* the book's "amplitude setting" everywhere. Workable, but
   it's a standing invitation to a factor-of-two error.

**All three are fixable with measurements you should arguably make on any generator.** See
[Bench calibration](#bench-calibration-worth-doing-on-any-generator) below — and note that
doing so is itself squarely Problem 1 and 2 material.

#### The real argument for spending more

Not "cheap is bad". It's that **this book's whole method is measure, calculate, compare** —
the learning lives in the disagreements. Self-studying with no instructor to sanity-check
you, every disagreement on an uncharacterised instrument has two candidate explanations
(your circuit, or your generator) and no way to tell them apart. A generator with a settable
output load and a published flatness spec deletes that entire category of dead end. You're
buying confidence, not capability.

Against that: if you'd *enjoy* characterising your own gear, the FY6900 is a legitimate
choice and the calibration is an evening's work. Budget for a better power supply — the stock
wall wart is the single most-replaced part on these, and Problem 9F asks you to find a very
small 2.8 MHz signal in the noise.

#### Checks to run on arrival, whichever you buy

Any of these failing is a return, not a workaround:

- [ ] **AM at 100% depth**, 1 MHz carrier, 1 kHz sine modulation — the envelope must cleanly
      touch zero. Problem 4D's distortion depends on genuinely reaching that point.
- [ ] **20 Vpp open circuit at 2.8 MHz.** On the FY6900 the 20 Vpp spec runs to 10 MHz, so
      this should pass, but Problem 9F sits right at the amplitude ceiling.
- [ ] **Output noise** with the output set to a few hundred mV — you need to be able to see
      Problem 9F's small signal above it.

---

### Bench calibration worth doing on any generator

Two short measurements that turn instrument uncertainty into a known correction. Do them
before Problem 8.

**Source impedance** (a five-minute Thevenin exercise, and directly Problem 1/2 material):

1. Measure the open-circuit output `V_oc` on the scope at 1 MΩ.
2. Add the 50 Ω feedthrough terminator, measure `V_50`.
3. `Rs = 50 × (V_oc / V_50 − 1)`.

If that comes out at 50 Ω, use 50 Ω. If it comes out at 46 or 54, use *that* in Problem 8A
and your deduced `R_LC` gets better, not worse. This also settles requirement 7: whichever
of `V_oc` and `V_50` matches the front-panel display tells you the display convention.

**Through reference for Problem 8E** — do this regardless of which generator you own:

1. Connect the generator straight to the scope with the 50 Ω feedthrough, no filter.
2. Sweep the same 1 MHz intervals from 1 to 15 MHz and record the amplitude at each.
3. Divide your filter measurements by this reference.

This removes generator flatness *and* scope frequency response in one step — and at 15 MHz
the scope's own roll-off is likely the bigger of the two. The normalised plot is better than
what you'd get by trusting anybody's flatness spec.

### Scope check

Nothing in Problems 1–9 stresses a scope except **Problem 8E**, which asks for an amplitude
response plot out to 15 MHz. A 20 MHz scope is already about 1 dB down at 15 MHz and will
visibly bend the top of that curve; 100 MHz or better and it's a non-issue.

Two things to look up on your scope before starting Problem 3, because parts E–J need them
as inputs, not as measurements:

- **Input capacitance `Co`** — usually printed next to the input jack (typically 13–20 pF).
- **The 10:1 probe's marked capacitance** — Problem 9 needs it too, since the probe's
  capacitance is part of the resonant tank.

---

## Shopping list

### Instruments

- [ ] Function generator meeting the table above
- [ ] 12 V, 0.8 A-hr sealed lead-acid battery (Yuasa NP0.8-12 or equivalent) + float charger
      — **required for Problem 2; a bench supply will not do**

### Accessories

- [ ] 2 × BNC tee (male-female-female) — P5, P8
- [ ] 1 × BNC 50 Ω feedthrough terminator — P5, P8B
- [ ] 2 × BNC-to-minigrabber / test-hook lead — P3 explicitly builds on component leads, no
      breadboard
- [ ] 2–3 × BNC-BNC coax patch cables
- [ ] BNC-to-banana or BNC-to-alligator adapter
- [ ] Non-metallic (ceramic/plastic) trimmer tuning tool set — P8, and the 40B's alignment

### Breadboard components

Quantities are "buy a few spares", not the minimum.

| Part | Qty | For |
|---|---|---|
| 510 Ω, **1/2 W** (not 1/4 W — see the audit) | 5 | P2 |
| 300 kΩ, 1% metal film | 2 | P3 |
| 3.0 kΩ, 1% metal film | 2 | P4 |
| 2.0 kΩ, 1% metal film | 4 | P5 transistor switch, P6 |
| 10 nF (0.01 µF) film, 5% | 5 | P3, P4 |
| 1N4148 | 10 | P4, P6 |
| 1 mH molded choke | 3 | P5, P6 |
| P2N2222A or PN2222A (TO-92) | 5 | P5, P6 — sacrificial, spikes kill these |

A generic 1% metal-film resistor assortment and a film capacitor assortment cover all of the
above except the chokes and transistors, and will keep covering later chapters.

### Kit-adjacent

- [ ] #26 and #28 enamelled magnet wire, small spools — the kit ships ~20% margin on wire
      and no allowance for a practice toroid wind
- [ ] Solder wick, fine 63/37 solder, 15–25 W pencil iron or temperature-controlled station
      at ~700 °F, small PCB vise — for Problems 8 and 9 onward
- [ ] 50 Ω, 5 W dummy load with a BNC connector — not needed until the radio is finished, but
      the 40B manual's alignment procedure requires it

---

## Sources

- [Siglent SDG1032X product page](https://siglentna.com/product/sdg1032x/)
- [Siglent SDG1032X datasheet (PDF)](https://siglent.co.uk/pdf/SIGLENT-SDG1032X-FUNCTION-GENERATOR-Datasheet.pdf)
- [Siglent SDG1032X user manual](https://www.manualslib.com/manual/2675359/Siglent-Sdg1032x.html)
- [FeelElec FY6900 series user manual](https://www.scribd.com/document/510174024/FY6900-Series-Users-Manual-V1-0)
  — source for the FY6900 numbers in the table (50 Ω ±10%, 1 mVpp–20 Vpp ≤10 MHz, AM depth
  0–120%, TTL and SYNC outputs)
- [FY6900 teardown review, Radiomuseum](https://www.radiomuseum.org/forum/dds_function_generator_fy6900_teardown_review.html)
- [Power supply replacement for the FY6900, element14 community](https://community.element14.com/technologies/test-and-measurement/f/forum/39941/power-supply-alternative-for-fy6900-signal-generator/151351)
- [Modifications to the FY6900 waveform generator (PDF)](https://altrish.co.uk/wp-content/uploads/2024/10/Modifications-to-the-FY6900-Waveform-Generator.pdf)
- NM0S Electronics, *NorCal 40B Assembly and Operating Manual*, rev. 121623

FY6900 figures above are published specs, not bench measurements — hence the
[arrival checks](#checks-to-run-on-arrival-whichever-you-buy).
