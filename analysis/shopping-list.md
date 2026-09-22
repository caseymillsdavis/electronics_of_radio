# Shopping list

**One order, everything the exercises need.** This is the consolidated list — the per-problem
reasoning lives in the [parts audit](problems-01-39-parts-audit.md), what you can avoid buying
lives in [workarounds](substitutions-and-workarounds.md), and the function-generator spec lives
in [test-equipment.md](test-equipment.md). Those explain *why*; this is what goes in the cart.

**Covers Problems 1–39 — the whole book.** Chapters 7–15 add almost no *components* (the 40B kit
has every board part they install) but they add instruments, fixtures and one antenna. Those
are in [Cart 5](#cart-5--chapters-715-instruments-and-fixtures).

## How to read the tiers

| Tier | Meaning |
|---|---|
| **1 — Required** | A problem stops without it, and there's no workaround already in the repo. |
| **2 — Cheap insurance** | Single-digit cost, removes a real unknown or a genuine dead end. Buy it with the rest; deciding later costs more in shipping than the part. |
| **3 — Optional** | There's a documented workaround. Buy because you want the capability afterwards, not because a problem forces you. |

Quantities are "buy spares", not the minimum. Several parts are explicitly sacrificial —
Problems 5 and 6 make inductive spikes that kill transistors, and Problems 14/15/16 solder
resistors in and then throw them away.

---

## The one real decision: the function generator

Everything else on this page is commodity. This isn't, and it's most of the money.

**Don't order one off this page** — go to the
[requirements table](test-equipment.md#function-generator--requirements-derived-from-the-problems)
first, then the [candidates](test-equipment.md#candidates). Twelve requirements come straight
out of the problem statements. Eleven of them are met by anything in the class.

**Requirement 8 is the one that can disqualify a generator: pulse mode, ~5 V, 50 ns wide,
20 kHz repetition** (Problem 10A). Minimum pulse width is not a headline spec, it varies more
between models than anything else on the list, and none of the usual review coverage mentions
it. **Check it on the datasheet before ordering.**

The safe default is a Siglent SDG1032X or its single-channel sibling; Rigol DG8xx and Owon
AG10xx are the same class. Cheap DDS boxes (FY6900, JUNTEK) are *not* disqualified — see
[the analysis](test-equipment.md#is-a-cheap-dds-generator-fy6900-etc-disqualified). All of that
is from published specs, not from something measured on this bench.

---

## Buying passives in bulk

The useful thing to know here is that **the passive requirements for Problems 1–16 are much
smaller than they look**, and one of the two obvious kit purchases isn't worth making.

### Resistors — buy one E24 kit, and you're done through Problem 39

Every fixed resistor value any problem in the book asks for, except one (see the note below):

| Value | Problem | In E24? | In E12? |
|---|---|---|---|
| 150 Ω | 14 | ✅ (15) | ✅ |
| 200 Ω | 14, 15 | ✅ (20) | ❌ |
| 5.6 Ω | 31 | ✅ (56) | ❌ |
| 510 Ω | 2 | ✅ (51) | ❌ |
| 750 Ω | 16 | ✅ (75) | ❌ |
| 1 kΩ | 15 | ✅ (10) | ✅ |
| 1.5 kΩ | 16 | ✅ (15) | ✅ |
| 2.0 kΩ | 5, 6 | ✅ (20) | ❌ |
| 2.2 kΩ | 16 | ✅ (22) | ✅ |
| 3.0 kΩ | 4, 29 | ✅ (30) | ❌ |
| 300 kΩ | 3, 32 | ✅ (30) | ❌ |

**A standard 1% metal-film E24 assortment spanning 10 Ω–1 MΩ covers all eleven.** These run
600–1500 pieces across the range for the price of a few coffees. An **E12** kit misses six of
the eleven exactly — which matters less than it sounds given this repo measures everything
anyway, but E24 costs almost the same, so there's no reason to accept the gap.

**The one exception is Problem 31's 8 Ω speaker load**, which has to dissipate real audio power
for three problems running. A 1/4 W assortment part is marginal and drifts as it warms — buy an
8.2 Ω at 1 W or better. It's a separate line in Cart 5.

Two caveats on kits:

- **They're 1/4 W.** Fine for everything in Problems 1–16 as currently planned. (The old
  1/2 W recommendation was driven by running Problem 2 at 12 V; that's moot now — Problem 2 is
  done, on depleted AAAs at milliamp currents.)
- **They usually start at 10 Ω.** If you want the 1 Ω for Problem 10C's optional current
  transformer, buy it separately.

Tolerance is close to irrelevant here — the repo's standing rule is that you measure the part
and use the measured number, which makes a 5% part with a known value strictly better than a
1% part you assumed. Buy on range, not on tolerance.

### Capacitors — **don't** buy a kit

This is the non-obvious one. Across all of Problems 1–16 there is exactly **one** breadboard
capacitor value: **10 nF (0.01 µF)**, used in Problems 3 and 4. Every other capacitor in these
chapters is on the radio board and comes in the NorCal kit.

So a capacitor assortment buys you almost nothing for this course. Buy **five 10 nF film caps**
instead, and let one question decide the tolerance:

- **Does your DMM have a capacitance range?** If yes, any 10 nF will do — including the kit's
  own `103` discs — because you'll measure it and use the measured value. If no, **buy 5% film**:
  Problems 3C and 3D compare measured against calculated, and a ±20% ceramic disc puts a 20%
  unknown right in the middle of the comparison.

It doesn't have to be 10 nF, either. **Anything from roughly 1 nF up works, measured**, as long
as you scale with it: Problem 3 absorbs the change in the generator frequency, Problem 4 in `R`.
The rule and the arithmetic are
[in the workarounds doc](substitutions-and-workarounds.md#problem-3-if-your-capacitor-isnt-10-nf-scale-the-frequency-not-r).
Below ~2 nF, start zeroing the DMM's test leads before you trust a reading, and measure through
the 10:1 probe rather than a bare coax lead.

If you want to stock the junk box anyway, a film/polyester kit is the useful kind. **NP0/C0G**
ceramics are the ones that matter for RF tuned circuits later; general-purpose discs
(X7R, Y5V) drift with temperature and voltage and are the wrong part for anything resonant.

### What no assortment covers

Chokes, transistors, diodes, RF connectors, coax. Those are the itemised lines below.

---

## Cart 1 — general electronics supplier

Passives, semis, and the small stuff. One DigiKey/Mouser/Farnell order, or Amazon for the kits.

| ☐ | Part | Qty | Tier | What it's for |
|---|---|---|---|---|
| ☐ | 1% metal-film resistor assortment, E24, 10 Ω–1 MΩ | 1 kit | 1 | Every resistor in P1–16 (see above) |
| ☐ | 10 nF film capacitor, 5% | 5 | **3** | P3, P4 — the only breadboard cap. Demoted from Tier 1: **any measured cap from ~1 nF up now works**, by scaling P3's frequency and P4's `R` ([how](substitutions-and-workarounds.md#problem-3-if-your-capacitor-isnt-10-nf-scale-the-frequency-not-r)). Buy it to keep the book's own numbers; 5% only matters if your DMM can't measure C |
| ☐ | 1N4148 diode | 10 | 1 | P4 detector, P6 snubber |
| ☐ | P2N2222A or PN2222A, **TO-92** | 5 | 1 | P5 switch, P6. **Sacrificial** — the experiment makes spikes that kill them. Don't substitute the kit's TO-18 Q6; different pinout, and it's spoken for |
| ☐ | 1 mH moulded choke | 3 | 1 | P5, P6 — also consumable |
| ☐ | 74HC4066 or 74LVC1G66 analog switch | 2 | 2 | Turns the STM32 DAC into a real 1 MHz AM source for P4 |
| ☐ | Rail-to-rail (RRIO) op-amp, jellybean | 2 | 2 | Same, plus it's *mandatory* for any DAC work here — the U5G9's DAC can't drive P4's 3 kΩ load, and buffer-on can't reach 0 V. See [firmware notes](../firmware/README.md#dac-capability-verified-against-the-datasheet) |
| ☐ | 100 Ω cermet or carbon potentiometer | 1 | 2 | P10C null method — replaces the book's transformer-and-metal-box fixture with a DMM reading |
| ☐ | 1 Ω resistor | 2 | 3 | Only for P10C's exact fixture. Kits don't go this low |
| ☐ | FT37-43 or BN-43-2402 ferrite core | 1 | 3 | Same. **Do not wind the kit's FT37-43** — that core is T1 and P15 needs it |

## Cart 2 — RF interconnect

The cluster most likely to be forgotten, and the most annoying to be missing mid-experiment.
Often a different supplier (ham radio dealer, or Amazon) than Cart 1.

| ☐ | Part | Qty | Tier | What it's for |
|---|---|---|---|---|
| ☐ | **RG58/U with BNC plugs, 10 m minimum — 20 m better** | 1 | 1 | P10, P12. Buying the longer reel relaxes P10A's pulse-width requirement and lowers P12's resonant frequency. **Know the dielectric**: solid PE gives the book's 0.66c, foam runs faster. Measure the actual length before using it |
| ☐ | BNC tee, male-female-female | 3 | 1 | P5, P8, P10, P12 |
| ☐ | BNC 50 Ω feedthrough terminator | 1 | 1 | P5, P8B, P10A, P13 |
| ☐ | **50 Ω termination or dummy load, ≥ 2.5 W, BNC** | 1 | 1 | **P24, P25, P30, P33 hold 30 Vpp = 2.25 W.** A 0.5 W feedthrough drifts, then dies, then corrupts the measurement. This supersedes the "later" entry below |
| ☐ | BNC-BNC patch cable, short, for scope sync | 1 | 1 | P30C triggers the scope from the generator's sync output |
| ☐ | BNC-to-minigrabber / test-hook lead | 2 | 1 | P3 builds on component leads with no breadboard; P13 hooks onto C45's leads |
| ☐ | BNC-BNC patch cable | 2–3 | 1 | General |
| ☐ | BNC barrel adapter, female-female | 1 | 1 | P14 — board straight onto channel 1 with the shortest possible lead; cable capacitance distorts the filter shape |
| ☐ | BNC-to-banana or BNC-to-alligator adapter | 1 | 2 | General bench |

## Cart 3 — modules

Both are a few dollars and both convert a tedious problem into an automated one. *(Prices are
rough and from the earlier analysis, not re-checked.)*

| ☐ | Part | Qty | Tier | What it's for |
|---|---|---|---|---|
| ☐ | AD9850 or AD9851 DDS module (~$5) | 1 | 2 | 0.03 Hz resolution at 4.9 MHz. Optional for P8/P9; for P14 it's the difference between an automated sweep and several hundred manual readings |
| ☐ | AD8307 log-detector module (~$5–10) | 1 | 2 | Makes P14K's 60 dB plot a DMM reading instead of a fight with the scope's noise floor. **Calibrate its slope and intercept yourself and write them down** |

## Cart 4 — soldering and consumables

Needed **before Problem 8**, which is the first board work.

| ☐ | Part | Qty | Tier | What it's for |
|---|---|---|---|---|
| ☐ | Temperature-controlled iron (~700 °F) or 15–25 W pencil | 1 | 1 | P8 onward |
| ☐ | Fine 63/37 solder | 1 | 1 | |
| ☐ | Solder wick | 1 | 1 | P14/P15/P16 solder parts in and then remove them |
| ☐ | Small PCB vise | 1 | 1 | |
| ☐ | #26 and #28 enamelled magnet wire, small spools | 1 ea | 1 | The kit ships ~20% wire margin and no allowance for a practice toroid wind |
| ☐ | Bare #22 wire, or solid hookup wire to strip | ~1 m | 1 | P14 crystal-can grounds, P16 input lead and ground loop |
| ☐ | Non-metallic (ceramic/plastic) trimmer tuning tool set | 1 | 1 | P8, P16, and the 40B's alignment. A metal screwdriver detunes the circuit as you tune it |
| ☐ | Thin insulating sheet or heatshrink | scrap | 2 | P14 — the kit ships no crystal spacers |

## Cart 5 — Chapters 7–15 instruments and fixtures

Chapters 7–15 install ninety-odd components and the 40B kit has every one of them. What they
add is everything *around* the board. Ordered roughly by the problem that first needs it.

| ☐ | Part | Qty | Tier | What it's for |
|---|---|---|---|---|
| ☐ | Loudspeaker, ~2.25 in, 8 Ω, ≥ 0.25 W | 1 | 1 | P17 builds it into a tube; P33 onward it's the radio's speaker |
| ☐ | Stereo 3.5 mm plug, solderable | 3 | 1 | P17's speaker lead, and spares — J3/J4 are both 3.5 mm |
| ☐ | **3.5 mm shorting plug** (tip to sleeve) | 2 | 1 | P21, P23, P26, P28, P30 — in and out constantly. Make one from a spare plug |
| ☐ | Cardboard mailing tube, ≥ 35 cm | 1 | 1 | P17 (16 cm) and P18 (extended past λ/2). Cut to fit — the length *is* the tuning |
| ☐ | Cork liner sheet / gasket cork | scrap | 1 | P17 friction sleeve so the speaker slides to trim resonance |
| ☐ | Hot glue gun | 1 | 2 | P17 — any cheap one |
| ☐ | **Sound level meter**, 35–100 dB, C-weighted, small mic | 1 | 2 | P17, P18. **Has a documented MCU substitute** — see [workarounds](substitutions-and-workarounds.md) |
| ☐ | Dowel or rod, ~40 cm, non-metallic, marked in cm | 1 | 1 | P18 pushes the mic down the tube. Make it |
| ☐ | **1 Ω resistor** | 2 | **1** | Promoted from Tier 3 — P20 and P24 use it as the supply-current shunt, and every power number in P24/P25 scales with it |
| ☐ | Keying relay, 5 V DIP (Magnecraft W171DIP-7 or any 5 V/500 Ω DIP relay with a snubber) | 1 | 3 | P20, P25I, P30C. **An MCU GPIO does this better** — buy only if you want Problem 6's inductive load made real |
| ☐ | **Thermometer with a probe that can sit on a heat sink** | 1 | 2 | P25, P27E, P29C. **Prime MCU-substitute candidate** — three uses, two of which want simultaneous frequency |
| ☐ | Heat-sink compound, small tube | 1 | 1 | P25 — couples the thermometer to the sink |
| ☐ | Hair drier | 1 | 1 | P27E, P29C — scrounge. Plus a vented plastic box, which you make |
| ☐ | **Frequency counter**, ≥ 5 MHz, fine resolution | 1 | 1 | P26 onward, constantly. **Buildable on the STM32** — see [workarounds](substitutions-and-workarounds.md); note the reference-accuracy limit there |
| ☐ | 8.2 Ω resistor, **≥ 1 W** | 2 | 1 | P31–P33 audio load. Not the assortment part |
| ☐ | **Step attenuator, 50 Ω, ≥ 80 dB in steps, shielded** | 1 | **1** | P33, P34, P35. The last significant instrument in the book. Buy, chain fixed SMA pads, or build — **shielding, not attenuation, is what limits a cheap one** |
| ☐ | Antenna wire, ~22 m, plus 2 end insulators and a centre insulator | 1 | 1 | P34G, P36, P39. A 40 m dipole is ~20 m of wire and costs almost nothing |
| ☐ | Coax feedline with BNC, 10 m+ | 1 | 1 | Feeds the antenna. The P10/P12 reel can do double duty |
| ☐ | **2-way power combiner**, HF, isolation > 20 dB (e.g. ZFSC-2-1 class) | 1 | 2 | **P35 only.** A BNC tee is explicitly wrong — it lets the transmitters intermodulate each other |
| ☐ | Battery-powered oscillator module in a die-cast box (Si5351/AD9850 + cell) | 1–2 | 2 | Stands in for the second and third transceiver in P34B and P35. Out-isolates a mains generator, which is the whole point |
| ☐ | Second 10:1 probe with known capacitance | 1 | 1 | P22 needs two at once; check before you get there |

---

## Later — not for the exercises

Don't add these to this order unless you want them anyway.

- ~~**50 Ω, 5 W dummy load with BNC**~~ — **promoted into Cart 2.** Problem 24 needs it, not
  just the 40B's own alignment procedure.
- **12 V battery + float charger** — a field supply for the finished radio. The 40B wants
  10–16 V. **Not needed for Problem 2**, which is done.

---

## Deliberately not buying

Worth recording, so these don't creep back onto the list:

- **A battery for Problem 2.** Done, on depleted AAAs out of the junk drawer — which turned out
  to be the *right* source rather than a compromise. See
  [the results](bench-results.md#problem-2--sources-p-4041).
- **A capacitor assortment.** One value, five parts. Reasoned above.
- **1/2 W or 1 W resistors.** That recommendation existed only for a 12 V Problem 2.
- ***Puff*.** Problems 13, 14 and 16 call for it; free alternatives are documented in
  [test-equipment.md](test-equipment.md#puff-and-what-to-use-instead).
- **The book's Problem 10C current-transformer fixture.** Two of three alternatives need no
  parts at all.
- **A spectrum analyser.** Problem 30D looks like it demands one and doesn't — Figure 12.15 *is*
  the spectrum plot, measured and printed in the book, and the exercise is to identify the
  mixing orders behind each line. Paper, not hardware.
- **A hardware Morse decoder.** Problem 39 assumes one; it's a Goertzel filter and some timing
  logic. Run fldigi, or write it for the STM32 and put it in `firmware/`.
- **EZNEC.** Problem 37 mentions it and doesn't require it; the whole problem is closed-form.
  Free alternatives exist if you want to check yourself.
- **A second and third NorCal 40B.** Problems 34B and 35 are written for a lab with several.
  Two battery-powered oscillator modules in separate boxes substitute for both, and isolate
  *better* than a bench generator does.

---

## Keeping this list current

**When new problems are analysed, their parts land here in the same pass.** Adding a problem to
the [parts audit](problems-01-39-parts-audit.md) without updating this file leaves the audit's
"Buy" verdicts stranded in a per-problem table that nobody reads when placing an order — which
is the failure mode this file exists to prevent.

For each new problem:

1. Add anything genuinely new as a line in the right cart, with tier and one-line purpose.
2. **Check it against the existing lines first.** Most new resistor and capacitor values are
   already covered by the E24 kit — say so rather than adding a line.
3. Check it against the [workarounds](substitutions-and-workarounds.md) before marking it
   Tier 1: if there's a documented substitute, it's Tier 3.
4. Move anything now owned into [the bench inventory](../CLAUDE.md#bench-inventory) and, if it
   was a "not buying" decision, record why in the section above.
