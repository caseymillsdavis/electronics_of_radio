# Problems 1–16: what each one needs, vs. what the NorCal 40B kit has

Covers *The Electronics of Radio* Chapter 2 Problems 1–6 (pp. 39–48), Chapter 3 Problems 7–9
(pp. 65–70), Chapter 4 Problems 10–12 (pp. 92–96), Chapter 5 Problems 13–14 (pp. 112–118)
and Chapter 6 Problems 15–16 (pp. 124–127). Problem 16 is only partly uploaded — see the
warning in its section.

**This document says what the book asks for.** For what you can get away with instead —
substitute values, rescaled frequencies, MCU stand-ins, junk-box parts measured rather than
assumed — see [substitutions-and-workarounds.md](substitutions-and-workarounds.md). Most of
the "buy" verdicts below have a workaround.

## The short answer

**The kit is not a source of breadboard parts, and was never meant to be.** The book keeps
two separate stocks: a bag of loose components for the bench experiments, and the NorCal kit
for the radio. (The footnote on p. 40 points at the book's own Appendix A for "a complete
list of the supplies and equipment that are used in each problem" — check it; it's the
authority on what the course expects you to have outside the kit.)

That splits the problems by where the work happens:

| Problems | Where the work happens | 40B kit sufficient? |
|---|---|---|
| **1, 7, 11** | Paper only | n/a — nothing to buy |
| **2–6** | Breadboard | **No.** Buy loose parts. Kit covers ~2 of 8 values, and only by cannibalising. |
| **8, 9** | Soldered to the NorCal board | **Yes.** Right parts, right topology, right designators. |
| **10, 12** | A length of coax on the bench | **Not applicable** — the kit has no coax. Buy 10 m of RG58/U. |
| **13** | Soldered to the NorCal board | **Parts yes, values no.** The 40B's harmonic filter is a different design point — the one real divergence in this batch. |
| **14, 15, 16** | Soldered to the NorCal board | **Yes**, and unusually cleanly — crystals, 270 pF caps, L4, C14, T1, T2, T3 all match the book. |

The only real gaps are cheap: four resistor values, a 10 nF capacitor, a couple of
transistors, a battery, and a function generator with AM modulation.

Chapters 4–6 add three more, all small: **10 m of RG58/U** with BNC ends, a handful of
**temporary resistors** that get soldered in and then discarded (150 Ω, 200 Ω, 1 kΩ, 1.5 kΩ —
none of them in the kit), and a little **bare #22 wire**. They also add one thing that isn't a
part at all: Problems 13, 14 and 16 need a **circuit simulator**. The book uses *Puff*; see
[test-equipment.md](test-equipment.md#puff-and-what-to-use-instead) for what to use instead.

---

## Problem 1 — Thevenin and Norton equivalents (p. 39–40)

T and π networks; find `Vo`, `Is`, `Rs`. Pencil and paper. Nothing needed.

---

## Problem 2 — Sources (p. 40–41)

| Needed | Kit? | Verdict |
|---|---|---|
| 12 V, 0.8 A-hr battery (book specifies Yuasa) | ✗ | **Buy.** |
| 4 × 510 Ω, 1/4 W | Kit has **3** (R10, R11, R15) | **Buy 4+.** |
| Breadboard, multimeter | have | ✓ |

**Your bench supply cannot substitute for the battery.** The whole point of the problem is
measuring the source's internal resistance from the droop as you load it. A regulated lab
supply has a source resistance near zero by design — you'd plot a flat line and learn
nothing. You need a real battery with real internal resistance.

You do *not* need the specified 12 V SLA: the battery is the device under test, so almost any
alkaline cell or stack works, and a plain **9 V alkaline** is arguably the better subject.
See [the battery workaround](substitutions-and-workarounds.md#problem-2-the-battery--can-aaa-cells-work)
— it also removes the resistor-dissipation problem below. The SLA is worth buying only if you
want a field battery for the finished radio, in which case add a float charger.

**Watch the resistor power rating** *if you use a 12 V source.* Each 510 Ω across ~12 V
dissipates 12²/510 ≈ **0.28 W**, which is over the 1/4 W the book calls for. (On a 9 V
battery it's 0.16 W and the issue disappears.) They will get hot, and hot resistors drift, which
shows up in your plot. Buy 1/2 W or 1 W 510 Ω resistors instead — the experiment doesn't care
about the package, and it makes the two-minute settling wait the book asks for much better
behaved.

Also worth knowing: at ~94 mA with four resistors you are at the point where breadboard
contact resistance is a measurable fraction of what you're trying to measure. Seat the leads
properly and, if your numbers look odd, measure the current directly rather than trusting
the "assume 510 Ω nominal" calculation.

Part C asks about the radio's receive current. The 40B draws 15–20 mA (manual
*Specifications*), so the book's 20 mA figure works fine — see
[the comparison notes](../reference/norcal-40b-vs-40a.md#receive-current-drain--problem-2c).

---

## Problem 3 — Capacitors / RC delay (p. 41–44)

| Needed | Kit? | Verdict |
|---|---|---|
| 300 kΩ resistor | ✗ (2 × 150 kΩ in series would work, but they're R3/R24) | **Buy.** |
| 10 nF capacitor | 6 × 0.01 µF ceramic disk (C5, C7, C19, C22, C48, C55) | **Buy a 5% film cap.** |
| Function generator, 20 Hz, 1 Vpp square, 50 Ω source, sync out | ✗ | **Buy.** |
| Scope + 10:1 probe, test hooks | have (check probes) | ✓ |

The kit's `103` disc caps *are* 10 nF, and since this is a breadboard experiment you'd be
borrowing rather than consuming them. But ceramic discs in a kit are typically ±10–20% with
a temperature coefficient to match, and Problems 3C/3D ask you to compare a *measured* time
constant against a *calculated* one. A ±20% capacitor puts a ±20% error into the answer
before you start. A 10 nF polypropylene or polyester film cap at 5% costs pennies and makes
the comparison mean something. Same reasoning for the 300 kΩ: buy a 1% metal film.

Parts E–K need the scope's input capacitance `Co` (usually printed by the input jack) and a
10:1 probe with its capacitance marked. Both are things to confirm on your scope before you
start rather than mid-problem. The delays you're chasing run from milliseconds (part C, with
the 10 nF fitted) down to a few microseconds (part J, probe only) — no bandwidth challenge
for a decent scope, but you do need a probe whose marked capacitance you trust.

Note the explicit instruction *"Do not use a breadboard, because it adds capacitance that
confuses the measurements."* This one is built in free air on the component leads with test
hooks, so you need **BNC-to-minigrabber leads**, not just BNC-to-BNC coax.

---

## Problem 4 — Diode detectors (p. 44–45)

| Needed | Kit? | Verdict |
|---|---|---|
| Detector diode | 6 × 1N4148 | ✓ *(borrow, or buy — they're a cent each)* |
| 3 kΩ resistor | ✗ (nearest: 4.7 kΩ; or 1.8 k + 1.0 k = 2.8 k) | **Buy.** |
| 10 nF capacitor | see Problem 3 | **Buy.** |
| Function generator with **AM modulation** and a sync output | ✗ | **Buy — this sets the spec.** |
| Two-channel scope | have | ✓ |

The book doesn't name the diode in Figure 2.29, but part B — *"Compare the maximum voltage
of the input AM signal with the maximum voltage of the output audio... What would you expect
the difference of these voltages to be?"* — is asking for a silicon forward drop of about
0.6 V. That's a **1N4148** (the book's own Appendix A will confirm). The kit has six.

Don't casually substitute for the 3 kΩ. With 10 nF it sets τ = 30 µs, and the problem is
constructed around that value sitting between two timescales: comfortably shorter than the
1 ms modulation period (part A) and comfortably longer than the 1 µs carrier period —
until part C drops the carrier to 100 kHz (10 µs period) specifically so τ *stops* being
long enough and you can watch the droop appear. Change R and you blur the demonstration.
Buy a 3.0 kΩ.

**This problem is the one that decides which function generator to buy.** It needs a 1 MHz
carrier, internally amplitude-modulated by a 1 kHz tone, at a modulation depth you can set
to 70% and then to 100%. Plenty of cheap generators can't do AM at all. See
[test-equipment.md](test-equipment.md).

---

## Problem 5 — Inductors, and the transistor switch (p. 45–47)

| Needed | Kit? | Verdict |
|---|---|---|
| 1 mH inductor | 1 (RFC2) | **Buy spares.** |
| 50 Ω feedthrough terminator + BNC tees | ✗ | **Buy.** |
| P2N2222A transistor (TO-92) | 2N2222A in TO-18 metal can (Q6) | **Buy TO-92 parts.** |
| 2 × 2 kΩ resistors | ✗ (nearest: 1.8 kΩ) | **Buy.** |
| 12 V power supply | have | ✓ |
| 10:1 probe | have | ✓ |
| Function generator, 1 kHz / 100 kHz square, 5 Vpp | ✗ | **Buy.** |

The kit's single 1 mH choke (RFC2) would technically do the first half, but the second half
of this problem — and all of Problem 6 — deliberately drives it into producing large
inductive spikes, with the book noting the resulting voltage *"can destroy a transistor."*
Risking the kit's only 1 mH choke and its only 2N2222A to save a couple of dollars is a bad
trade. 1 mH molded chokes and PN2222A/P2N2222A transistors are both cents apiece; buy a
handful of each and keep the kit sealed.

Two more notes:

- **Pinout.** The book's P2N2222A is TO-92 (E-B-C in a flat row); the kit's Q6 is TO-18 with
  pins on a circle keyed to the case tab. If you do end up using a metal-can part, get the
  right datasheet.
- **Current-limit the bench supply** (~100 mA is plenty for the 2 kΩ collector load) before
  the first power-up. The book's warning about *"many opportunities to destroy components"*
  is real, and a current limit turns most wiring mistakes into a non-event.

The 50 Ω load is not optional — the whole measurement is `τ = L/R` with `R` being the
generator's 50 Ω plus the load's 50 Ω. Get a proper BNC feedthrough terminator, not a
resistor jammed into a breadboard.

---

## Problem 6 — Diode snubbers (p. 48)

Same circuit as the end of Problem 5, plus:

| Needed | Kit? | Verdict |
|---|---|---|
| 1N4148 snubber diode | 6 in kit | ✓ *(or buy)* |
| Everything from Problem 5 | see above | — |

No new parts beyond a diode. Part A measures the ringing frequency of the 1 mH against stray
circuit capacitance, which lands somewhere around 0.5–1 MHz for typical breadboard/probe
strays, so any modern scope handles it.

Read the safety note in part B carefully before probing the inductor: both scope grounds are
tied together through the chassis and out to the supply's negative lead, so clipping a ground
lead to the inductor puts the full supply across it. The book's workaround (reference the
trace to the supply's + lead, then move the probe tip) is the right approach.

---

## Problem 7 — Parallel-to-series conversion (p. 65–66)

Algebra, then a design calculation for a 50 Ω → 5 Ω matching network at 7 MHz. Nothing to
buy, nothing to build.

---

## Problem 8 — Series resonance (p. 66–67) — **on the board**

| Needed | Kit? |
|---|---|
| C1 — variable capacitor, book says 8–50 pF | ✓ 50 pF trimmer |
| L1 — 15 µH inductor | ✓ 15 µH molded choke (brown-green-black) |
| Soldering iron, fine solder, solder wick, electronics vise | **buy if you don't have them** |
| Non-metallic tuning tool | **buy** |
| Function generator to 15 MHz, 1 Vpp and 10 Vpp settings | **buy** |
| BNC tee, 50 Ω feedthrough terminator | **buy** |

**The 40B has exactly the right parts for this.** C1 and L1 keep the 40A's designators, the
40B's *Theory of Operation* describes them as *"a low-loss series-resonant circuit"* feeding
the receive mixer, and a 50 pF trimmer has the range to hit 7 MHz against 15 µH (arithmetic
[below](#appendix-arithmetic-behind-the-sufficiency-claims)).

Two practical points:

- The book says to adjust C1 with a **plastic screwdriver** — a metal one adds enough hand
  capacitance to move the resonance while you're tuning it. The 40B manual says the same
  thing in its alignment section. Buy a set of ceramic/plastic tuning tools.
- Leave the parts about a millimetre proud of the board as the book suggests so you can get
  test hooks onto the leads.

Part E sweeps 1–15 MHz. Check that your scope reads amplitude accurately at 15 MHz — a
20 MHz scope is already ~1 dB down there, which will visibly bend the top end of your
response plot. 100 MHz or better and it's a non-issue.

---

## Problem 9 — Parallel resonance (p. 68–70) — **on the board**

| Needed | Kit? |
|---|---|
| C37 — 5 pF disk | ✓ **4.7 pF** NP0, marked `479` |
| C38 — 100 pF disk | ✓ 100 pF NP0, `101` |
| C39 — variable | ✓ 50 pF trimmer |
| L6 — T37-2 core + #28 wire | ✓ T37-2 (red) + #28 enamel in kit |
| 10:1 probe with marked capacitance | have |
| Function generator, sine, 1 Vpp and 10 Vpp settings, ~2–9 MHz | **buy** |

**Also right in the 40B**, with the same designators and exactly the Figure 3.10b topology:
the schematic shows the transmit mixer U4 feeding C37 in series into a node with C38, C39 and
L6 to ground.

Two numbers change:

- **L6 is 30 turns on the 40B, not 28.** Use N = 30 in part B's `L = A_l N²`.
- **C37 is 4.7 pF, not 5 pF.** Use 4.7 pF in part A's total-capacitance calculation.

Everything the problem asks still works — `f0` comes out lower than a 40A builder's, and C39
ends up further from the top of its range, which is if anything more comfortable.

One thing to buy: the kit's #28 wire has about 50 cm of slack over what the toroids need, so
there's no margin for a practice wind. A spool of #26 and #28 enamel wire is cheap insurance
before you wind L6 — and L9 (63 turns) later.

---

## Chapter 4 — Transmission lines

Problems 10–12 never touch the NorCal board. They are bench work on a length of coax, so the
only *component* they add to the shopping list is the coax — though they also add a pulse-mode
requirement to the function generator you haven't bought yet, and one small fixture you can
avoid building.

---

## Problem 10 — Coaxial cable (p. 92–94)

| Needed | Kit? | Verdict |
|---|---|---|
| **10 m of RG58/U** with BNC connectors | ✗ | **Buy.** The one new consumable in this chapter. |
| A second cable of unknown length (part B's "antenna cable") | ✗ | Any offcut — [workaround](substitutions-and-workarounds.md#problem-10-you-do-not-need-an-antenna-and-you-may-not-need-the-transformer) |
| Function generator: 5 V pulses, **50 ns wide**, 20 kHz repetition | ✗ | **Buy — and this adds a new spec.** |
| Two-channel scope at **10 ns/div** | have — confirm timebase and bandwidth | ✓ probably |
| 50 Ω feedthrough terminator, BNC tee | already on the list | ✓ |
| **1:1 wideband transformer + 1 Ω resistor in a metal box** (part C) | ✗ | **Build, or dodge it** — see workarounds |

**Buy RG58/U, and know its dielectric.** Solid-polyethylene RG58 runs at v ≈ 0.66c; foam
variants run 0.78–0.85c. Either is fine — part A *measures* v, which is the whole point — but
part E's L and C come out different, and the book's tidy 250 nH/m and 100 pF/m only fall out
of a solid-PE cable. If you want your numbers to look like the book's, buy solid.

**Measure the cable with a tape before you connect it.** "10 m" on a reel label is nominal,
and `v = l/t` propagates a length error straight into part E's L and C. This is the
measure-don't-assume rule applied to a thing most people would never think to check.

Part C's fixture — a 1:1 transformer and a 1 Ω resistor in a metal box, so that a
current-sensing resistor can sit in series without shorting the scope ground — is the only
build in this chapter. Two of the three
[alternatives](substitutions-and-workarounds.md#problem-10c-measuring-z0-without-building-the-box)
need no parts at all, and one of them is a measurement you were already told to make in
[the generator calibration](test-equipment.md#bench-calibration-worth-doing-on-any-generator).

**The new instrument requirement is pulse mode**, and it is worth checking before you buy a
generator: minimum pulse width, and how fast its edges are. It is *not* a hard blocker — the
50 ns figure has slack in it and there are two ways round it entirely — but it is the kind of
spec that is easy to not notice you're missing. See
[test-equipment.md](test-equipment.md#requirement-8-pulse-mode-is-the-new-thing-to-check).

---

## Problem 11 — Waves (p. 94–95)

Paper. Phasor loci for forward and reverse waves, the SWR formula, the input impedance of an
infinite LC ladder, and a loss-and-delay calculation for 100 km of telephone cable with and
without Pupin loading coils. Nothing to buy, nothing to build, nothing from the kit.

One thing worth noticing before you start: part C's cable is specified as **L = 250 nH/m and
C = 100 pF/m**, which is exactly the 50 Ω, 0.67c coax you characterised in Problem 10E. Do
Problem 10 first and part C stops being an abstraction — it's your own cable, 10,000 times
longer.

---

## Problem 12 — Resonance (p. 95–96)

| Needed | Kit? | Verdict |
|---|---|---|
| The same 10 m cable | from Problem 10 | ✓ |
| Function generator, sine, ~5 MHz, 1 Vpp, fine frequency control | ✗ | **Buy** — no new spec beyond Problems 8/9 |
| Two-channel scope, and its **input capacitance `Co`** | have — look it up | ✓ |
| BNC tee | on the list | ✓ |

**No 50 Ω load in this one** — the book says so explicitly, and terminating would destroy the
resonance you're trying to measure. Leave the terminator in the drawer.

The resonance you're hunting is set by *your* cable: an open-circuited line is series-resonant
when it is a quarter wavelength, so `f₀ = v / 4l`. Ten metres of solid-PE RG58 puts that near
5 MHz. **Any length works** — longer moves it down, shorter moves it up — so if you bought a
different reel, nothing breaks; see the
[range check](#appendix-arithmetic-behind-the-sufficiency-claims).

Part C needs the scope's input capacitance again — the same number Problem 3 asked for. If it
never got written down, this is the third time it's been needed and it will be needed again in
Problem 16. Put it on a label on the scope.

Part D's √2-bandwidth hunt is undemanding: the Q of a 10 m coax resonator is somewhere around
15, so the half-power points are a couple of hundred kilohertz apart and any generator
resolves them easily. Enjoy it — Problem 14 wants the same measurement done on something with
a Q of tens of thousands.

---

## Chapter 5 — Filters

Problems 13 and 14 are the first sustained soldering on the board — a dozen-odd parts each
rather than Problem 8's two — and the first that need a **circuit simulator** rather than a
component. The book uses *Puff*, which ships with it. Every option here is free, including
running *Puff* itself; see
[test-equipment.md](test-equipment.md#puff-and-what-to-use-instead).

---

## Problem 13 — Harmonic filter (p. 112–114) — **on the board, and the 40B differs**

**This is the first problem whose parts are not the book's parts.** Everything is in the kit;
none of the values match.

| | Book (40A) | NorCal 40B | |
|---|---|---|---|
| C45 | 330 pF | **390 pF** NP0 200 V (`391`) | ✓ in kit |
| C46 | 820 pF | **1000 pF** NP0 200 V (`102`) | ✓ in kit |
| C47 | 330 pF | **1000 pF** NP0 200 V (`102`) | ✓ in kit |
| L7 | T37-2, **18 t** #26, 30 cm | T37-2, **15 t** #26, 24 cm → **0.90 µH** | ✓ in kit |
| L8 | T37-2, **18 t** #26, 30 cm | T37-2, **12 t** #26, 20 cm → **0.58 µH** | ✓ in kit |
| J1 | BNC antenna jack | ✓ BNC PCB-mount jack | ✓ in kit |

Also needed, none of it in the kit: a function generator that still delivers a **10 Vpp
setting at 14 MHz** (a step up from the 3 MHz ceiling Problems 8 and 9 needed), test hooks on
C45's part-exposed leads, a coax lead to J1, a **parallel** 50 Ω termination at the scope, and
a simulator for parts C–F.

### What the difference costs you

**Nothing structural. Every number, though.**

- **Parts A–E all still work.** Measure the loss at 7 and 14 MHz, compute the inductances from
  `L = A_l N²`, simulate, read off the input impedance, retune for half of it. The method is
  untouched. You simply can't compare your answers against a 40A builder's, or against the
  book's own figures.
- **Part B is actually easier to trust on a 40B.** The book hands you `A_l = 4.0 nH/turn²` and
  asks you to compute L7 and L8. The 40B manual independently states 0.90 µH and 0.58 µH — and
  `4.0 nH/t² × 15²` and `× 12²` reproduce those exactly. That's a free confirmation that the
  book's core constant is right for your cores, which a 40A builder never gets. (It checks out
  on L2, L6 and L8 too — see the
  [reference notes](../reference/norcal-40b-vs-40a.md#the-t37-2-inductance-constant-checks-out-on-every-toroid-in-the-kit).)
- **Check the schematic before you solder, and before you clip the generator on.** Appendix A
  gives values, not order — it does not tell you whether the 390 pF or a 1000 pF sits at the
  power-amplifier end. On the 40A the input is C45 and Problem 13A tells you to hook the
  generator across it. The 40B's filter is **asymmetric**, so the two ends are genuinely not
  interchangeable: depending on which way round it is, the impedance the filter presents to
  the PA differs by more than a factor of five. Get Appendix B and D out first. Numbers in the
  [arithmetic appendix](#appendix-arithmetic-behind-the-sufficiency-claims).
- **Part F is board-independent and transfers verbatim.** Designing a 5th-order 0.2 dB
  Chebyshev at `fc` = 8 MHz from the filter tables and simulating `|s21|` is paper-plus-
  simulator; the radio never enters into it.
- **The "2 watts" in the problem statement is the 40A's PA.** The 40B's is a 2SC5964 or
  2SC2078 on a heatsink; check your manual's *Specifications* before quoting a margin against
  the FCC limit. The limit itself — HF transmitters under 5 W, every spur at least 30 dB below
  the carrier — applies to both radios.

---

## Problem 14 — IF filter (p. 114–118) — **on the board, and it transfers almost perfectly**

| Needed | Kit? | Verdict |
|---|---|---|
| X1–X4, four matched crystals | ✓ **6 × 4.915 MHz HC-49** (X1–X6) | ✓ — the book also wants six: four now, two for the mixer oscillators later |
| C9–C13, 270 pF | ✓ 7 × 270 pF NP0 5% (`271`), C9–C13 among them | ✓ **exact match** |
| L4, 18 µH | ✓ 18 µH molded, brown-grey-black | ✓ **exact match** |
| C14, 47 pF | ✓ 47 pF NP0 5% (`470`) | ✓ **exact match** |
| 200 Ω resistor — temporary, discarded in part K | ✗ | **Buy.** Junk box is ideal; it gets thrown away |
| 150 Ω resistor — temporary, discarded in part K | ✗ | **Buy.** Same |
| 4 × plastic crystal spacers | ✗ not in Appendix A | **Improvise** — [workaround](substitutions-and-workarounds.md#problem-14-crystal-spacers-bare-wire-and-the-can-grounds) |
| Bare **#22** wire for the crystal-can grounds | ✗ — the kit ships #26/#28 **enamel** only | **Buy, or strip solid hookup wire** |
| Function generator with **1 Hz steps at 4.9 MHz**, 0.5–2.0 Vpp | ✗ | **Buy — the sharpest frequency spec in the book so far** |
| Scope with a bandwidth-limit filter and ~60 dB of usable range at 4.9 MHz | have — check | **The hard measurement of this batch** |
| BNC tee, sync cable, external trigger | on the list | ✓ |
| Simulator (parts E–I) | ✗ | [see below](test-equipment.md#puff-and-what-to-use-instead) |
| Solder wick — part K removes both resistors | on the list | ✓ |

**This is the best-matching problem in the batch.** C9–C13 at 270 pF, four crystals out of a
set of six, L4 at 18 µH and C14 at 47 pF are all exactly what the book asks for, and the 40B
manual describes its IF filter as a **4-pole Cohn filter** — Figure 5.18's topology, part for
part. The LC matching network of Figure 5.23 is the same too.

Four things do change:

1. **Start the hunt at 4,915,000 Hz, not 4,913,500 Hz.** The 40B's crystals are 4.915 MHz; the
   book's are 4.9135 MHz. Part A has you find `f₀` to the nearest hertz regardless, so this
   only decides where you start sweeping — but at 1 Hz steps, starting 1.5 kHz off is a long
   evening.
2. **Nobody has promised your crystals are matched.** The book leans on Wilderness Radio
   sorting the 40A's crystals to within 20 Hz. Whether NM0S sorts the 40B's is not something
   the manual says, and it is the assumption the entire filter shape rests on. The good news:
   **Problem 14A *is* the sorting procedure.** Measure all six, then pick the closest four for
   X1–X4 and leave the outliers for the mixer oscillators, where a few hundred hertz doesn't
   matter. If the spread is much worse than a few tens of hertz you have learned something
   important before soldering anything.
3. **The resistor holes the book names are 40A holes.** Part K has you solder the 200 Ω "from
   the left L4 hole... to the left C14 hole" and the 150 Ω into "the number-3 hole of T3" — all
   of which are positions on the 40A's board. The 40B's layout is different, so re-find them
   from Appendix B and the schematic. The *electrical* intent is unambiguous and is what to
   work from: 200 Ω from the filter output (C13) to ground as the load, and 150 Ω in series
   from the generator into the filter input, making the generator look like 200 Ω.
4. **The book's 10 MHz scope filter is a Tektronix-2465-ism.** Modern scopes offer a 20 MHz
   bandwidth limit instead. Use it. The book already tells you the plot is relative precisely
   because the filter attenuates at 4.9 MHz, so the extra 10 MHz of noise bandwidth costs a
   little sensitivity and nothing else.

**Part I's "1,240 Hz above the signal" is 2× the 40A's 620 Hz CW offset.** If the 40B's offset
differs, that frequency moves with it. Check the manual's *Specifications* before quoting an
upper-sideband rejection at "the" spur frequency.

**Part K is the hardest measurement so far** — a 60 dB plot at 4.9 MHz, which at realistic
drive levels means reading sub-millivolt signals on a scope. It is the one place in this batch
where a
[workaround is close to mandatory](substitutions-and-workarounds.md#problem-14k-60-db-of-dynamic-range-at-49-mhz).

---

## Chapter 6 — Transformers

---

## Problem 15 — Driver transformer (p. 124–126) — **on the board, exact match**

| Needed | Kit? | Verdict |
|---|---|---|
| T1: FT37-43 core, 14 t primary + 4 t secondary, #26 | ✓ FT37-43 (black, **orange dot**), 14 t (23 cm) + 4 t (10 cm) #26 | ✓ **exact match** |
| R14, 100 Ω | ✓ 100 Ω (R14, R25) | ✓ |
| 1 kΩ resistor — temporary | kit has one, spoken for as R18 | **Buy.** Don't borrow R18 |
| 200 Ω resistor — temporary | ✗ | **Buy** |
| Function generator, 5 Vpp 7 MHz sine, and down to ~100 kHz for part C | ✗ | **Buy** — no new spec |
| Scope with 50 Ω termination | have | ✓ |
| Solder wick — part D removes both resistors | on the list | ✓ |

Core, turns and gauge all match. The only discrepancy is trivial: the book says cut **25 cm**
for the primary, the 40B parts list says **23 cm**. Cut the longer. You can always trim, and a
toroid you have to unwind because the tail came up short is a bad twenty minutes.

Two things worth having straight before you start:

- **`A_l` for #43 ferrite is strongly frequency-dependent, and part D is built on that.** The
  book quotes 160 nH/turn² at 7 MHz from its Appendix D; part C measures `fc` somewhere between
  a few hundred kilohertz and about a megahertz, where #43's permeability is much higher. So the
  `A_l` you deduce in part D *should* come out well above 160 — the book says as much. That's
  the lesson, not an error in your measurement.
- Part C measures a −3 dB point, so it is a place where generator flatness shows up directly
  in the answer. Not a new purchase, but a good reason to have done the
  [through-reference sweep](test-equipment.md#bench-calibration-worth-doing-on-any-generator).

---

## Problem 16 — Tuned transformers (p. 126–127 onward) — **on the board; pages incomplete**

> ⚠️ **Only pages 126–127 were uploaded.** Part A and the *Puff* model of Figure 6.10 are
> covered, but Figure 6.9 labels a "Jumper for part C", so parts B and C at least exist beyond
> what's here, and the page-127 text breaks off mid-sentence. **Treat this section as
> provisional** and re-check it when the rest of the problem arrives.

| Needed | Kit? | Verdict |
|---|---|---|
| T2: FT37-61, 1 t primary + 20 t secondary | ✓ FT37-61, 1 t #26 (5 cm †) + 20 t #26 (31 cm) | ✓ turns match; **gauge differs** |
| T3: FT37-61, 23 t primary + 6 t secondary | ✓ FT37-61, 23 t #28 (25 cm †) + 6 t #26 (13 cm) | ✓ |
| C2, variable | ✓ 50 pF trimmer | ✓ |
| C4, 5 pF | ✓ **4.7 pF** NP0 (`479`) | ✓ same substitution as C37 in Problem 9 |
| 1.5 kΩ resistor — temporary, stands in for U1 | ✗ | **Buy** |
| Bare **#22** wire — R2 input lead and the board-edge ground loop | ✗ | **Buy, or strip solid hookup wire** |
| 10:1 probe with **marked capacitance** | have | ✓ — needed as a model input, not a measurement |
| Function generator, 0.5 Vpp 7 MHz sine | ✗ | **Buy** — no new spec |
| Non-metallic tuning tool for C2 | on the list | ✓ |
| Simulator | ✗ | [see below](test-equipment.md#puff-and-what-to-use-instead) |

† Appendix A's wire lengths for both transformers conflict with the schematic's — see the
[errata](../reference/norcal-40b-parts-list.md#suspected-errata-in-the-manual). Cut long.

- **The book's T2 primary is one turn of bare #22; the 40B's is #26.** One turn is one turn,
  so nothing changes electrically. But bare #22 is still needed elsewhere in this problem — the
  input lead soldered into R2's centre hole, and the ground loop at the board edge — and again
  for Problem 14's crystal cans. Buy a little regardless; it isn't in the kit.
- **C4 is 4.7 pF on a 40B, not the 5 pF printed in Figure 6.10.** Use 4.7 pF in the model. It's
  a 6% change on a series coupling element and moves nothing you'd see, but the model should
  describe the board you actually have.
- **T3's 23:6 ratio is exactly the 3 kΩ → 200 Ω match the problem describes.** (23/6)² = 14.7
  against a required 3000/200 = 15. The book doesn't print T3's turns in the visible text, so
  the 40B's numbers are the ones to use — and they're right.
- The temporary 1.5 kΩ stands in for U1's input resistance. The book quotes the SA602AN as
  **1.5 kΩ shunted by 3 pF**; the 40B's U1 is an SA612 or NE602 from the same family. Check
  your own datasheet rather than assuming, because that 3 pF is an explicit element in the
  Figure 6.10 model.
- **A 50 pF trimmer still reaches resonance against T2** on the 40B — range check in the
  [appendix](#appendix-arithmetic-behind-the-sufficiency-claims). Since T2's turns are
  identical to the 40A's, the 66 nH shunt inductor in Figure 6.10 is correct for your board
  as printed.

---

## Verdict on cannibalising the kit

For Problems 2–6 you'd be borrowing, not consuming — breadboarding doesn't damage parts. So
it's *possible* to pull the 0.01 µF caps, a 1N4148, the 1 mH choke and two 150 kΩ resistors
out of the kit bags, run the experiments and put them back. Don't:

1. **The kit has no spares.** Quantities are exact. A lost 4.7 pF cap or a stretched choke
   lead means emailing NM0S, and the through-plated board makes recovery from a wrong-hole
   solder job unpleasant.
2. **Two of the borrowings are actively risky.** The 1 mH choke and the 2N2222A both go into
   a circuit the book warns can destroy parts.
3. **The substitutes are things you probably already own.** Every value the kit could supply
   here is a generic passive; see
   [substitutions-and-workarounds.md](substitutions-and-workarounds.md). There's no reason to
   raid a $200 kit for a 0.01 µF capacitor.

Keep the kit bags sealed until Problem 8.

### The same rule, restated for Chapters 5 and 6

Problems 14, 15 and 16 each ask you to solder in a resistor, take a measurement, then
**unsolder and discard it** — 150 Ω and 200 Ω in Problem 14, 1 kΩ and 200 Ω in Problem 15,
1.5 kΩ in Problem 16. Only one of those values — **1 kΩ** — exists in the kit at all, and it
is spoken for as R18 (with a suspected second one as R26, see the
[errata](../reference/norcal-40b-parts-list.md#suspected-errata-in-the-manual)).

Don't borrow it. These resistors are *deliberately* sacrificial — the book has you remove them
and wick the holes clear — and pulling a kit resistor back out of a plated-through hole is
exactly the operation the 40B manual warns about. They cost cents; buy 150 Ω, 200 Ω, 1 kΩ and
1.5 kΩ in whatever tolerance your junk box already has. Nothing in these three problems needs
them to be precise, only to be *known*, and you have a multimeter.

---

## Appendix: arithmetic behind the sufficiency claims

*Skip this if you'd rather work the numbers yourself — these are range checks, not answers to
the problems, but they do give away the ballpark.*

<details>
<summary>Problem 8 — does a 50 pF trimmer reach resonance against 15 µH at 7 MHz?</summary>

`C = 1 / (ω²L)` with `ω = 2π × 7 MHz = 4.398 × 10⁷ rad/s` and `L = 15 µH`:

    C = 1 / (1.934e15 × 15e-6) = 34.5 pF

Comfortably inside an 8–50 pF trimmer, near the middle of its travel. ✓
</details>

<details>
<summary>Problem 9 — does a 50 pF trimmer reach 7 MHz against the 40B's larger L6?</summary>

40B L6 = 30 t on T37-2, `L = A_l N² = 4.0 nH/t² × 900 = 3.6 µH` (schematic rounds to 3.5 µH).

Total tank capacitance needed at 7 MHz:

    C = 1 / (1.934e15 × 3.6e-6) = 144 pF     (or 148 pF if L = 3.5 µH)

Already present, with the 10:1 probe attached as in Problem 9C:

    C37 (4.7) + C38 (100) + probe (~13) ≈ 118 pF

So `C39 ≈ 26–30 pF` — mid-range on a 50 pF trimmer. ✓

For comparison, a 40A with 28 turns (3.1 µH) would need ~167 pF total and push C39 close to
its maximum. The 40B's extra two turns make this easier, not harder.
</details>

<details>
<summary>Problem 2 — currents, and why the resistors run hot</summary>

At 12 V with 510 Ω nominal, adding resistors one at a time:

| Resistors | Current |
|---|---|
| 0 | 0 |
| 1 | 23.5 mA |
| 2 | 47.1 mA |
| 3 | 70.6 mA |
| 4 | 94.1 mA |

Part B's "neighbourhood of 75 mA" is the three-resistor point. Dissipation per resistor is
12²/510 = **0.28 W**, above the 1/4 W the book specifies — hence the recommendation to buy
1/2 W parts.
</details>

<details>
<summary>Problem 4 — why 3 kΩ and 10 nF specifically</summary>

`τ = RC = 3 kΩ × 10 nF = 30 µs`, against:

| Waveform | Period | vs τ |
|---|---|---|
| 1 kHz modulation (part A) | 1000 µs | τ ≪ period ✓ output follows the audio |
| 1 MHz carrier (parts A, B, D) | 1 µs | τ ≫ period ✓ no droop between cycles |
| 100 kHz carrier (part C) | 10 µs | τ only 3× period → droop becomes visible, which is the point |

</details>

<details>
<summary>Problem 5 — inductor time constant</summary>

`τ = L/R` with L = 1 mH and R = 50 Ω (generator) + 50 Ω (load) ≈ 100 Ω, plus roughly 10 Ω of
DC resistance in the molded choke (the 40B manual quotes ~10 Ω as the health check for a
1 mH part). That's τ ≈ 9–10 µs against a 500 µs half-period at 1 kHz — the square wave has
plenty of time to settle, as the problem assumes.
</details>

<details>
<summary>Problem 10 — is 10 ns/div right, and what should L and C come out at?</summary>

For a coax with a solid polyethylene dielectric, `εr = 2.25`, so

    v = c / √εr = 3.00e8 / 1.5 = 2.00e8 m/s  = 0.667 c

Over 10 m that is a **50 ns** one-way delay — five divisions at the book's 10 ns/div, which
is why it picks that scale. Round trip (part B, and the reflections in part D) is 100 ns.

Then part E:

    L = Z0 / v  = 50 / 2.00e8      = 250 nH/m
    C = 1 / (Z0 v) = 1 / (50 × 2.00e8) = 100 pF/m

which are exactly the numbers Problem 11C hands you for its 100 km telephone cable.

A **foam**-dielectric RG58 runs nearer `v = 0.8 c = 2.4e8 m/s`: 41.7 ns over 10 m (still four
divisions), `L = 208 nH/m`, `C = 83 pF/m`. Nothing breaks; the answers just aren't the book's.

**Scope note:** don't chase the 50 ns delay with a bandwidth spec. Measure the time between
the **50% points** of the two pulses, one on each channel — the probes' and scope's rise time
is common to both and cancels. A 100 MHz scope with cursors is plenty.
</details>

<details>
<summary>Problem 12 — where does the resonance land, and how fine a generator?</summary>

An open-circuited line is series-resonant at a quarter wavelength:

    f0 = v / 4l = 2.00e8 / (4 × 10) = 5.0 MHz     (solid-PE RG58, 10 m)

**Any length works.** 20 m gives 2.5 MHz, 5 m gives 10 MHz; all comfortably inside the range
Problems 8 and 9 already required. Longer cable is if anything the easier experiment — it
lowers `f0` and raises the loss, which makes the minimum in part B deeper and easier to find.

For the bandwidth hunt in part D: with RG58's attenuation somewhere around 0.04–0.06 dB/m at
5 MHz, `α ≈ 0.005–0.007 Np/m` and `β = 2πf/v ≈ 0.157 rad/m`, so `Q = β/2α` lands in the
**12–20** range and the half-power points are a couple of hundred kilohertz apart. That is
undemanding: any generator resolves it. Worth noticing now, because Problem 14 asks for the
same measurement on a resonator with a Q three to four orders of magnitude higher.
</details>

<details>
<summary>Problem 13 — how different is the 40B's filter, and why does order matter?</summary>

**Spoils Problem 13C and 13D if you read it before working them.**

Modelling the book's ladder — shunt C45, series L7, shunt C46, series L8, shunt C47 — between
50 Ω source and 50 Ω load, with `L = 4.0 nH/t² × N²`:

**40A (book):** C45 330 pF, L7 1.296 µH, C46 820 pF, L8 1.296 µH, C47 330 pF

| f | \|s21\| | Zin at the PA end |
|---|---|---|
| 7 MHz | −0.14 dB | **45.0 + 16.7j Ω** |
| 14 MHz | −22.5 dB | |
| 21 MHz | −42.1 dB | |
| 28 MHz | −55.2 dB | |

That reproduces the book's own commentary — a near-lossless passband, a load impedance close
to 50 Ω *with a small inductive component*, which is the Class-E argument on p. 113, and a
second harmonic about 22 dB down.

**40B:** the values are C45 390 pF, C46 1000 pF, C47 1000 pF, L7 0.90 µH, L8 0.576 µH — but
Appendix A doesn't say which capacitor sits at the power-amplifier end. Running all six
distinct orderings of {390, 1000, 1000} against {0.90 µH, 0.576 µH}:

| C order (PA → antenna) | L order | 7 MHz | Zin at PA | 14 MHz |
|---|---|---|---|---|
| 390 / 1000 / 1000 | 0.90 / 0.576 | −1.32 dB | 100.0 + 67.7j | −19.8 dB |
| 390 / 1000 / 1000 | 0.576 / 0.90 | −0.55 dB | 38.3 − 29.9j | −19.0 dB |
| 1000 / 1000 / 390 | 0.90 / 0.576 | −0.55 dB | 43.2 − 33.4j | −19.0 dB |
| 1000 / 1000 / 390 | 0.576 / 0.90 | −1.32 dB | **16.5 − 7.3j** | −19.8 dB |
| 1000 / 390 / 1000 | 0.90 / 0.576 | −4.66 dB | 8.9 − 41.6j | −10.0 dB |
| 1000 / 390 / 1000 | 0.576 / 0.90 | −4.66 dB | 7.8 − 34.8j | −10.0 dB |

Two conclusions:

1. **It's the same kind of filter, at a different design point.** Second-harmonic rejection
   comes out around 19–20 dB against the 40A's 22.5 dB — the same ballpark, and the same
   ballpark again when you drive it from a PA-like source impedance rather than 50 Ω. The 40B
   is a lower-impedance design: `√(L/C)` is ~40 Ω for the 40A's middle section and 24–30 Ω for
   the 40B's, which is what you'd expect of a radio making more power off the same supply.
2. **The ordering is not a detail.** Zin at the PA end ranges from 8 Ω to 100 Ω across the
   table. Problem 13D asks you to find that impedance and 13E asks you to halve it, so getting
   the ends the wrong way round doesn't give you a slightly-off answer — it gives you a
   different problem. **Read Appendix B and D before you clip the generator across a
   capacitor.**

These figures are computed from Appendix A's values, not measured, and the topology is assumed
to be the book's. Confirm against the 40B schematic.
</details>

<details>
<summary>Problem 14 — how narrow is the dip, and does generator accuracy matter?</summary>

A microprocessor crystal at 4.915 MHz has an unloaded Q of roughly 50,000–150,000 and a
motional resistance of tens of ohms. In Figure 5.20's circuit the 50 Ω generator resistance is
in series with the crystal, so what you actually see is the **loaded** Q:

    Q_loaded ≈ Q_unloaded × R / (R + 50)

Taking `Q_unloaded = 80,000` and `R = 20 Ω` gives `Q_loaded ≈ 23,000` and a half-power width of
`f0/Q ≈ 215 Hz`. With `R = 40 Ω` it's about 140 Hz. So the dip you're hunting is **on the order
of 100–250 Hz wide**, with a bottom a few tens of hertz across.

**That justifies 1 Hz steps, but not 1 Hz accuracy** — and the difference matters when you're
choosing a generator:

- Matching the six crystals against each other is a set of **differences**. A common frequency
  offset cancels exactly.
- `Q = f0 / (fu − fl)` in part C is a **ratio**, and the bandwidth is a **difference**. Same
  cancellation.
- Part D's six-significant-figure check is against **your own measured `f0`**, not against an
  absolute standard.

So a generator that is 50 ppm off (≈ 250 Hz at 4.915 MHz) gives entirely correct answers to
everything Problem 14 asks. What would ruin the measurement is **drift during the session**:
if the generator wanders by 100 Hz while you work through six crystals, the matching is
fiction. Let it warm up for half an hour first, and if you can, re-measure the first crystal
last as a drift check.
</details>

<details>
<summary>Problem 15 — where does fc land, and how low must the generator go?</summary>

**Spoils the expected range for Problem 15C/15D.**

T1's magnetising inductance sits across the primary, and `fc = R / 2π L_p` where `R` is what
the inductance works against and `L_p = N² A_l = 196 A_l`.

The load side is unambiguous:

    reflected load = (14/4)² × (100 ‖ 50) = 12.25 × 33.3 = 408 Ω

The source side is not. **I can't tell from the photographed Figure 6.7 whether the 1 kΩ is a
shunt across the primary or sits in the generator's return leg** — the schematic reads one way
and the wiring instructions on p. 125 ("the other ends of these resistors are the input leads
for the function generator") read the other. Both give the same conclusion, which is why this
is a footnote rather than a blocker:

| 1 kΩ as… | source-side R | `R` at primary | `fc` at `A_l` = 160 nH/t² | `fc` at `A_l` ≈ 350–420 nH/t² |
|---|---|---|---|---|
| shunt across the primary | (50 + 200) ‖ 1000 = 200 Ω | 134 Ω | 679 kHz | 260–310 kHz |
| in series in the return | 50 + 200 + 1000 = 1250 Ω | 308 Ω | 1.56 MHz | 600–710 kHz |

Because `A_l` *rises* as frequency falls, the self-consistent answer sits toward the low end of
whichever row applies — and noticing that is exactly what part D is for. Expect `fc` somewhere
between roughly **250 kHz and 1.5 MHz**; check the figure on the page rather than trusting this
table for the narrower answer.

The `A_l` figures for #43 at low frequency are the published core-table values (350–420
nH/turn², depending on whose table and which vintage of #43), not measurements. The book's
160 nH/turn² is its own Appendix D figure at 7 MHz.

**Equipment consequence: none, under either reading.** The generator needs to be trustworthy
from about 100 kHz to a few MHz, which every candidate already is. No new spec from this
problem.
</details>

<details>
<summary>Problem 16 — does the 50 pF trimmer still reach resonance against T2?</summary>

T2 is 1 t : 20 t on FT37-61 with `A_l = 66 nH/turn²` — identical turns on the 40B and the 40A,
so the model transfers unchanged. Note that Figure 6.10's 66 nH shunt inductor is just
`1² × 66 nH`: the magnetising inductance referred to the one-turn primary.

Referred to the 20-turn secondary it is `20² × 66 nH = 26.4 µH`, and resonating that at 7 MHz
needs

    C = 1 / (ω²L) = 1 / (1.934e15 × 26.4e-6) = 19.6 pF

against a 50 pF trimmer, so C2 sits around 40% of its travel before you subtract the probe and
stray capacitance that are already there. **Comfortable.** ✓

Swapping the book's 5 pF C4 for the 40B's 4.7 pF is a 6% change in a series coupling element —
far inside the trimmer's adjustment range, and invisible next to the probe capacitance you're
also modelling.
</details>
