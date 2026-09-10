# Test equipment and shopping list for Problems 1–16

## Function generator — requirements derived from the problems

These are pulled straight out of the problem statements, not from a generic "good starter
generator" list. Numbers in the table are what the problems actually ask for.

Requirements 1–7 come from Problems 1–9 and were written before Chapters 4–6 arrived;
**requirements 8–12 are the additions**, and one of them (pulse mode) can genuinely disqualify
a generator that would otherwise have been fine.

| # | Requirement | Where it comes from |
|---|---|---|
| 1 | **Sine and square** waveforms | Sq: P3, P5, P6. Sine: P4, P8, P9 |
| 2 | **20 Hz to ≥ 15 MHz** | P3A is 20 Hz; P8E sweeps 1–15 MHz |
| 3 | **50 Ω source impedance**, well controlled | P3B and P8A both do Thevenin arithmetic that assumes exactly 50 Ω |
| 4 | **20 Vpp open-circuit** (= 10 Vpp into 50 Ω) at 1–3 MHz | P8F and P9F both say "amplitude setting of 10 Vpp" |
| 5 | **Internal AM**, 1 MHz carrier, 1 kHz modulating tone, **depth adjustable to 70% and 100%** | P4 intro and P4D |
| 6 | **Sync / trigger output** on BNC | P3 ("use a sync cable from the function generator to trigger the scope"), P4 ("connect a cable from the sync output... and use external triggering") |
| 7 | Amplitude readout referenced to a **50 Ω load** | The book's convention throughout — see below |
| **8** | **Pulse mode**: ~5 V, **50 ns width**, 20 kHz repetition, edges fast enough that 50 ns is still a pulse | P10A — **the new one to check** |
| **9** | The 10 Vpp amplitude setting still usable at **14 MHz** (was 3 MHz) | P13A measures loss at 7 *and* 14 MHz |
| **10** | **1 Hz frequency steps at 4.9 MHz**, and short-term stability well inside ~100 Hz over a session | P14A, P14C |
| **11** | Usable and flat down to **~100 kHz** | P15C's 3-dB cut-off lands in the 250–700 kHz range |
| **12** | Amplitude settings of 0.5, 1, 2, 5 and 10 Vpp | P16A/P14A (0.5), P12B (1), P14K (2), P15 (5), P13A (10) |

Requirements 9, 11 and 12 are free — anything meeting 1–7 already meets them. Requirement 10
looks alarming and isn't (see below). **Requirement 8 is the one that can rule a generator
out.**

Nice to have, still not required: a second channel, frequency sweep (makes P8E's 1 MHz-interval
sweep and the bandwidth hunts in P8C, P9C, P12D and P16A much less tedious), and a built-in
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

### Requirement 8: pulse mode is the new thing to check

Problem 10A wants **5 V pulses, 50 ns wide, repeating at 20 kHz**, so you can watch a pulse
travel down 10 m of coax and arrive 50 ns later. Two specs to look up on any generator you're
considering, and neither is on the front of the datasheet:

- **Minimum pulse width.** This is where generators differ. Some go down to ~20 ns; others stop
  at 80 or 100 ns. A generator that cannot make a 50 ns pulse is not disqualified, but it is
  worth knowing before rather than after.
- **Rise/fall time in pulse mode.** A 50 ns pulse with 20 ns edges is a triangle. You want edges
  of a few nanoseconds, and some generators let you set them.

**Three reasons not to panic about this:**

1. **The 50 ns is not sacred.** All part A needs is a pulse short compared with the 100 ns round
   trip. An 80 ns minimum still works on 10 m of cable, and **buying 20 m instead of 10 m
   doubles the margin** for the price of a coffee.
2. **A step works better than a pulse anyway.** Real TDR uses an edge, not a pulse — and the
   sync or TTL output most generators provide is usually the fastest edge in the box. Part D's
   open-circuit interpretation is *clearer* with a step, because you see the voltage double and
   stay doubled.
3. **The MCU beats every budget generator here.** At 160 MHz a timer tick is 6.25 ns, so 50 ns
   is exactly 8 ticks and 20 kHz is exactly 8,000. See
   [the workarounds](substitutions-and-workarounds.md#the-50-ns-pulse-for-problem-10--yes-and-better-than-a-budget-generator).

So: check it, prefer a generator that has it, don't let it override requirement 5.

### Requirement 10 sounds like it needs a lab standard. It doesn't.

Problem 14A asks you to set the generator "in intervals of 1 Hz" at 4.9 MHz and find a crystal's
resonance "to the nearest hertz". That is **0.2 parts per million**, which reads like a demand
for a rubidium reference. It isn't, and the distinction is worth being clear about because it
changes what you buy.

**Resolution is free.** Every DDS generator — including the cheapest — tunes in microhertz
steps, because the tuning word is a 32- or 48-bit integer. There is no generator on the
candidate list that cannot *set* 1 Hz increments at 4.9 MHz.

**Absolute accuracy doesn't matter**, because everything Problem 14 computes is a difference or
a ratio:

| Part | What it computes | Effect of a constant frequency offset |
|---|---|---|
| A | `f₀` of each crystal, six times | Cancels — you compare crystals to each other |
| C | `Q = f₀ / (fu − fl)` | Cancels — bandwidth is a difference |
| D | `L·C` from `f₀` to six digits | Self-consistent against *your* `f₀`, not an absolute one |
| E–I | *Puff* model of the filter | Built from your own L and C |

A generator that is 50 ppm off — ±250 Hz at 4.915 MHz — gives entirely correct answers to all
of it.

**Short-term stability is what actually matters.** The crystal dip is roughly 100–250 Hz wide
(arithmetic in the
[parts audit](problems-01-16-parts-audit.md#appendix-arithmetic-behind-the-sufficiency-claims)),
and you are comparing six crystals measured over perhaps an hour. If the generator drifts 100 Hz
during that hour, your matching is fiction. Two free habits fix it:

- **Warm up for 30 minutes** before Problem 14. Almost all of a crystal oscillator's drift is
  thermal and happens in the first few minutes.
- **Re-measure the first crystal last.** The difference is your drift, measured rather than
  hoped for. If it's small, the matching stands; if it isn't, you know before you solder.

An external 10 MHz reference input is nice if a generator has one, but buying one *for this* is
not justified.

### Candidates

| Model family | Notes |
|---|---|
| **Siglent SDG1032X / SDG1032X-Plus** (30 MHz, 2 ch) | Meets everything above. AM with settable source, depth, modulating frequency and waveform; 20 Vpp into high-Z (specified to 10 MHz, which covers the 10 Vpp uses at 1 MHz and 2.8 MHz); sync output on the rear Aux In/Out. The single-channel SDG1022X is the cheaper sibling. This is the safe default. |
| **Rigol DG822 / DG812 / DG1022Z** | Same class, same feature set. Check the specific model's AM depth range and sync output on its datasheet. |
| **Owon AG1022 / AG051** | Cheaper, generally adequate; verify AM depth control before ordering. |
| **FeelTech FY6900, JUNTEK and similar "DDS" boxes** | Meet the requirements on paper, including the AM one. Not disqualified — see [the section below](#is-a-cheap-dds-generator-fy6900-etc-disqualified). |

Verify against the current datasheet before buying — model lineups shift, and I'm going off
published specs rather than something on my bench. **Add "minimum pulse width" to the list of
things you check on the datasheet** (requirement 8): it is not a headline spec, it varies more
between models than anything else on this list, and none of the notes above cover it.

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
| 8 | Pulse, 50 ns wide, fast edges | **Check the current manual.** Pulse width is settable in nanosecond steps; the separate TTL output is spec'd at 10 ns edges and would do the job on its own |
| 9 | 10 Vpp setting at 14 MHz | **?** — the 20 Vpp figure is spec'd only to 10 MHz, so 14 MHz is outside the published amplitude spec |
| 10 | 1 Hz steps at 4.9 MHz | ✓ resolution is not the issue on any DDS box; **stability over a session is** |
| 11 | Flat to ~100 kHz | ✓ |
| 12 | 0.5–10 Vpp settings | ✓ 1 mVpp–20 Vpp |

Chapters 4–6 add one genuine new question mark and one non-issue. **Requirement 9 is the new
question mark**: Problem 13A compares the harmonic filter's loss at 7 MHz and 14 MHz at a
10 Vpp setting, and 14 MHz is beyond where the FY6900's amplitude is specified. That is not
fatal — Problem 13A is a *ratio* of two measured voltages, so a generator that droops at 14 MHz
biases the answer only if you assume the drive was equal at both frequencies. **Measure the
drive at both frequencies rather than trusting the front panel**, which the
[through-reference sweep](#bench-calibration-worth-doing-on-any-generator) already does for you.

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
- [ ] **A 50 ns pulse at 20 kHz**, viewed at 10 ns/div. If the shortest pulse it will make is
      much over 80 ns, plan on the [step-response route](substitutions-and-workarounds.md#part-a--the-50-ns-pulse-is-not-sacred)
      for Problem 10 — or buy 20 m of coax instead of 10 m.
- [ ] **Amplitude at 14 MHz** versus 7 MHz at the 10 Vpp setting. Whatever it is, write it down;
      Problem 13A is a ratio between exactly those two frequencies.
- [ ] **Half-hour drift at 4.915 MHz.** Set it, leave it, and come back — with a frequency
      counter if you have one, or by watching the beat against one of the kit's crystals. You
      want to know this number before Problem 14, not during it.

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

Chapters 4–6 add three demands, one of them hard:

- **A 10 ns/div timebase** (Problem 10A). Any digital scope does this. Bandwidth matters less
  than you'd think: measure between the **50% points** of the two pulses, one per channel, and
  the probes' and scope's rise time is common to both and cancels out.
- **A bandwidth-limit filter** (Problem 14K). The book asks for 10 MHz; modern scopes typically
  offer 20 MHz. Use whatever you have — the book already makes that plot relative for exactly
  this reason.
- **~60 dB of usable amplitude range at 4.9 MHz** (Problem 14K). This is the genuinely hard one:
  at realistic drive levels the bottom of that plot is a sub-millivolt signal, which no
  general-purpose scope reads off the screen. Averaging and an FFT get you part of the way; a
  log detector gets you all of it. See
  [the workaround](substitutions-and-workarounds.md#problem-14k-60-db-of-dynamic-range-at-49-mhz).

Two numbers to look up on your scope before starting Problem 3 and then **write on a label and
stick to the scope**, because four separate problems want them as *inputs* rather than
measurements — Problem 3E–J, Problem 9C, Problem 12C and Problem 16:

- **Input capacitance `Co`** — usually printed next to the input jack (typically 13–20 pF).
- **The 10:1 probe's marked capacitance `Cp`.**

---

## *Puff*, and what to use instead

Problems 13 (parts C–F), 14 (parts E–I) and 16 all say "use *Puff*". It is not a part and not a
purchase: *Puff* is the microwave-CAD program written at Caltech by Wedge, Compton and
Rutledge — the book's own co-author — and it ships with the book, with installation
instructions in **Appendix C**. It is a DOS program from the 1990s.

**You have three routes and all of them are free.**

### Route 1 — run the real thing

*Puff* runs under **DOSBox** on any modern machine. Appendix C's instructions then apply
verbatim, the book's screenshots match what you see, and the parts-window syntax the problems
quote (`x 20` for a 20:1 ideal transformer, the `s21` and `s11` plot setup, typing `=` to read
an impedance off the cursor) is exactly right. If you want to follow the book without
translation, this is the least friction.

### Route 2 — a modern S-parameter simulator

**QucsStudio** or **Qucs-S** are the closest things in spirit: GUI schematic capture with
native S-parameter analysis, so `s11` and `s21` come out directly the way *Puff* produces them.
Free. Windows-native, and they run under Wine.

### Route 3 — SPICE or Python, which is probably the right answer here

**ngspice** (free, scriptable, CLI) or **Python with an ABCD-matrix cascade** — twenty lines of
`numpy` — fit this repo's owner better than a GUI does, and give you text output you can diff,
version and plot. **LTspice** works too if you already have it.

The one thing that stops people is that SPICE gives you a voltage ratio and the book asks for
S-parameters. **The translation is a single line.** For a two-port driven from a source
resistance `Rs` into a load `RL`, with `Rs = RL = z0` real:

    |s21| = 2 × |Vout / Vsource|

where `Vsource` is the *open-circuit* source voltage, not the voltage at the input node. So
every *Puff* task in these problems becomes a `.AC` sweep of a fixture that is nothing more
than a source, a series `Rs`, your circuit, and a shunt `RL`:

| The problem says | In a SPICE fixture that means |
|---|---|
| "design frequency `fd` should be 7 MHz" | Nothing — that's a *Puff* display convention |
| "set up an `s21` plot, 0 to 28 MHz, 101 points" | `.ac lin 101 0 28meg`, plot `2*v(out)/v(src)` in dB |
| "the design impedance `zd` should be 200 Ω" (P14E) | `Rs = RL = 200` |
| "change `zd` to 50 Ω" (P14F) | `Rs = RL = 50` |
| "plot `s11`, move the cursor, type `=` to read the impedance" (P13D) | Compute the input impedance directly: `v(in)/i(vin)` |
| "`x 20` — an ideal 20:1 transformer" (P16) | Two coupled inductors with `K = 1` and an inductance ratio of 400:1, or a SPICE behavioural transformer |

Two cautions if you go this way:

- **Problem 14 will strain a careless simulation.** A crystal's equivalent circuit has `L` in
  the tens of henries and `C` in the femtofarads, and part E asks for a 2.5 kHz span centred on
  4.915 MHz — a fractional bandwidth of 5 × 10⁻⁴. Use a linear sweep with plenty of points
  (`.ac lin 1001 4.9138meg 4.9163meg`), keep double precision, and heed part D's instruction to
  carry six significant figures in whichever of `L` and `C` you derive. That instruction exists
  because the passband will slide off the plot otherwise, and it applies to any simulator.
- **Model what's on the board, not what's in the figure.** Problem 16's Figure 6.10 shows C4 as
  5 pF; the 40B's C4 is 4.7 pF. And `Cp` is your own probe's capacitance, which is why you were
  told to look it up.

### Which to pick

If you want the book's workflow and screenshots to match, use *Puff* under DOSBox. If you'd
rather have scriptable, diffable, plottable results and you're comfortable writing the fixture
yourself, use ngspice or Python — and note that having to build the S-parameter fixture is
itself a decent way to understand what `s21` actually is, which *Puff* rather hides.

The parts audit's own filter arithmetic was done the Python way, in about twenty lines.

## Shopping list

**Moved to [shopping-list.md](shopping-list.md)** — one consolidated, order-ready list covering
every problem analysed so far, grouped so each section is roughly one supplier's cart. It also
covers how to buy resistors and capacitors in bulk (short version: one E24 resistor kit does the
whole course; a capacitor kit is not worth buying).

What stays here is the *reasoning* behind the generator choice — the requirements table above,
the candidates, and the FY6900 analysis. The shopping list just says which one to click.

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
- Wedge, Compton and Rutledge, *Puff* — ships with *The Electronics of Radio*; installation and
  usage in the book's **Appendix C**
- [ngspice](https://ngspice.sourceforge.io/) · [QucsStudio](https://qucsstudio.de/) ·
  [Qucs-S](https://ra3xdh.github.io/) — the simulator alternatives
- Analog Devices **AD8307** (log detector) and **AD9850/AD9851** (DDS) datasheets — for the
  scalar-network-analyser build described in
  [substitutions-and-workarounds.md](substitutions-and-workarounds.md#the-instrument-this-batch-is-really-asking-for-a-scalar-network-analyser)

FY6900 figures above are published specs, not bench measurements — hence the
[arrival checks](#checks-to-run-on-arrival-whichever-you-buy). Minimum pulse width
(requirement 8) is **not** among the numbers I have for any of the candidates; it is the one
line on the requirements table I could not fill in from what I have, and the one worth checking
yourself before ordering.
