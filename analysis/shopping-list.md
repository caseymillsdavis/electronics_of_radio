# Shopping list

**One order, everything the exercises need.** This is the consolidated list — the per-problem
reasoning lives in the [parts audit](problems-01-16-parts-audit.md), what you can avoid buying
lives in [workarounds](substitutions-and-workarounds.md), and the function-generator spec lives
in [test-equipment.md](test-equipment.md). Those explain *why*; this is what goes in the cart.

**Covers Problems 1–16.** Problems 17–39 are on hand but not yet analysed, so expect this to grow —
see [keeping it current](#keeping-this-list-current) at the bottom.

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

### Resistors — buy one E24 kit, and you're done through Problem 16

Every fixed resistor value any of Problems 1–16 asks for:

| Value | Problem | In E24? | In E12? |
|---|---|---|---|
| 150 Ω | 14 | ✅ (15) | ✅ |
| 200 Ω | 14, 15 | ✅ (20) | ❌ |
| 510 Ω | 2 | ✅ (51) | ❌ |
| 750 Ω | 16 | ✅ (75) | ❌ |
| 1 kΩ | 15 | ✅ (10) | ✅ |
| 1.5 kΩ | 16 | ✅ (15) | ✅ |
| 2.0 kΩ | 5, 6 | ✅ (20) | ❌ |
| 2.2 kΩ | 16 | ✅ (22) | ✅ |
| 3.0 kΩ | 4 | ✅ (30) | ❌ |
| 300 kΩ | 3 | ✅ (30) | ❌ |

**A standard 1% metal-film E24 assortment spanning 10 Ω–1 MΩ covers all ten.** These run
600–1500 pieces across the range for the price of a few coffees. An **E12** kit misses five of
the ten exactly — which matters less than it sounds given this repo measures everything
anyway, but E24 costs almost the same, so there's no reason to accept the gap.

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
| ☐ | 10 nF film capacitor, 5% | 5 | 1 | P3, P4 — the only breadboard cap. 5% only matters if your DMM can't measure C |
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

## Later — not for the exercises

Don't add these to this order unless you want them anyway.

- **50 Ω, 5 W dummy load with BNC** — not needed until the radio is finished, but the 40B
  manual's alignment procedure requires it.
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

---

## Keeping this list current

**When new problems are analysed, their parts land here in the same pass.** Adding a problem to
the [parts audit](problems-01-16-parts-audit.md) without updating this file leaves the audit's
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
