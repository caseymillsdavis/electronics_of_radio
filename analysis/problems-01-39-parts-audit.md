# Problems 1–39: what each one needs, vs. what the NorCal 40B kit has

Covers **every problem in the book** — Chapter 2 Problems 1–6 (pp. 39–48), Chapter 3
Problems 7–9 (pp. 65–70), Chapter 4 Problems 10–12 (pp. 92–96), Chapter 5 Problems 13–14
(pp. 112–118), Chapter 6 Problems 15–16 (pp. 124–130), Chapter 7 Problems 17–18
(pp. 138–141), Chapter 8 Problems 19–20 (pp. 149–153), Chapter 9 Problems 21–23
(pp. 175–179), Chapter 10 Problems 24–25 (pp. 199–203), Chapter 11 Problems 26–27
(pp. 219–225), Chapter 12 Problems 28–30 (pp. 237–244), Chapter 13 Problems 31–33
(pp. 250–260), Chapter 14 Problems 34–36 (pp. 274–277) and Chapter 15 Problems 37–39
(pp. 305–313).

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
| **17, 18** | A speaker in a cardboard tube | **Not applicable** — no kit parts at all. Needs a sound level meter. |
| **19–33** | Soldered to the NorCal board | **Yes on parts.** Five divergences change numbers — see the table below. |
| **34, 35** | The finished radio on the bench | **Yes on parts**, but they want a second and third transceiver. Substitutable. |
| **36, 39** | The finished radio on the air | Needs an antenna; Problem 36 needs a licence. |
| **37, 38** | Paper only | n/a — nothing to buy, and the data for 38 is printed in the book. |

The only real gaps in Chapters 2–6 are cheap: four resistor values, a 10 nF capacitor, a couple
of transistors, a battery, and a function generator with AM modulation. Chapters 4–6 add
**10 m of RG58/U** with BNC ends, a handful of **temporary resistors** that get soldered in and
then discarded, a little **bare #22 wire**, and one thing that isn't a part at all — Problems
13, 14 and 16 need a **circuit simulator**. The book uses *Puff*; see
[test-equipment.md](test-equipment.md#puff-and-what-to-use-instead) for what to use instead.

### What Chapters 7–15 add

**Almost nothing from the kit is missing — every board component Problems 19–33 install is in
the 40B bag.** The cost is in three other places:

1. **Instruments.** A **frequency counter** from Problem 26 on, a **50 Ω load rated ≥ 2.5 W**
   from Problem 24 on, and a well-shielded **step attenuator of at least 80 dB** from Problem 33
   on. The attenuator is the significant one, and it is also the most buildable.
2. **Fixtures and consumables.** A keying relay or its solid-state replacement, a shorting plug
   for the Key jack, a thermometer and heat-sink compound, a hair drier and a vented box, a
   sound level meter, a 40 m antenna, a power combiner, and a growing pile of temporary
   resistors (750 Ω, 2.2 kΩ, 3 kΩ, 5.6 Ω, 8.2 Ω, 300 kΩ, several 1.5 kΩ).
3. **Other people.** Problem 34B wants a second transceiver, Problem 35 wants three radios and
   two operators, and Problem 36 is a demonstration to an instructor. All three have solo
   substitutions — see Chapter 14 below — but they need planning, not improvisation at the
   bench.

### The 40B divergences that change an answer

Problems 19–33 install about ninety components and the kit has all of them. But six places
differ from the book in ways that change a number you are asked to calculate or a limit you
are asked to respect. Each is written up in its own section:

| Ref | Book (40A) | 40B | Problem | Consequence |
|---|---|---|---|---|
| **Q7** | 2N3553, TO-39 can | 2SC5964/2SC2078, TO-220 | 24, 25 | Different mounting, different V<sub>CEO</sub> ceiling, **different thermal resistance** |
| **R<sub>θjc</sub>** | 25 °C/W (given) | a TO-220 figure | 25 | It is an *input* to the problem — substitute it or every junction temperature is wrong |
| **Q1** | 2N4124 | 2N3904 | 19 | Part H computes with the 2N4124's C<sub>obo</sub>; use the 2N3904's |
| **C50** | ~2–25 pF air variable | 50 pF air trimmer | 26, 27 | Part D's "average is 14 pF" is a 40A number |
| **C17** | 7–70 pF assumed | 50 pF trimmer | 29 | Part B computes the BFO range from the book's figure |
| **L9** | 62 turns | 63 turns | 26, 27 | Small, but it is the number parts D and H are built on |

Two more want checking against the 40B schematic before you rely on the book's description:
**D12** (the book calls it a 36 V zener; the 40B lists an SB160 Schottky) and **RFC1** (the
book has you install it; it is absent from the 40B's Appendix A). And one — **C56**, drawn as
10 µF in the book and listed as 0.047 µF in the 40B BOM — looks like an errata candidate and
matters to three problems. All three are flagged in place.

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

**Worked at the bench** on 2 × depleted AAA cells and 4 × 1.76 kΩ — measurements, the fit, and
the per-point-arithmetic trap that nearly produced a wrong conclusion are in
[bench-results.md](bench-results.md#problem-2--sources-p-4041).

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

## Problem 16 — Tuned transformers (p. 126–130) — **on the board**

The longest problem in the book so far, and it runs in two halves: parts A–E build and measure
the **RF Filter** (T2 joined to Problem 8's L1/C1), parts F–G build and measure the
**IF-Filter network** (T3 feeding Problem 14's crystal filter). Both halves end by producing a
loss figure the book tells you to keep — see the note on that below.

| Needed | Kit? | Verdict |
|---|---|---|
| T2: FT37-61, 1 t primary + 20 t secondary | ✓ FT37-61, 1 t #26 (5 cm †) + 20 t #26 (31 cm) | ✓ turns match; **gauge differs** |
| T3: FT37-61, 23 t #28 primary + 6 t #26 secondary | ✓ FT37-61, 23 t #28 (25 cm †) + 6 t #26 (13 cm) | ✓ turns *and* gauges match |
| C2, variable | ✓ 50 pF trimmer | ✓ |
| C4, 5 pF | ✓ **4.7 pF** NP0 (`479`) | ✓ same substitution as C37 in Problem 9 |
| C6, 47 pF — T3 primary tuning | ✓ 47 pF NP0 (`470`) | ✓ |
| L1, C1 — series resonator joined in at part C | ✓ | installed in Problem 8 |
| L4 (18 µH), C14 (47 pF) — IF output network | ✓ | installed in Problem 14 |
| J1 Antenna jack — generator feeds through it in part C | ✓ | installed in Problem 13 |
| 1.5 kΩ resistor ×1 — temporary; U1 stand-in (A–E), then U2 load (G) | ✗ | **Buy** — E24 kit |
| 750 Ω resistor — temporary, U1 hole #4 (part G input match) | ✗ | **Buy** — E24 kit |
| 2.2 kΩ resistor — temporary, U1 hole #5 (part G input match) | ✗ | **Buy** — E24 kit |
| Bare **#22** wire — R2 input lead, R2 jumper, board-edge ground loop | ✗ | **Buy, or strip solid hookup wire** |
| 10:1 probe with **marked capacitance** | have | ✓ — needed as a model input, not a measurement |
| Scope **low-pass / bandwidth-limit filter** | have? | **Confirm before part D** — not optional, see below |
| Function generator: 0.5 Vpp @ 7 MHz (A), **10 Vpp @ 2.8 MHz** (D), 10 Vpp @ 4.9 MHz (G) | ✗ | **Buy** — the 2.8 MHz/10 Vpp case is already [requirement 4](test-equipment.md) |
| Solder wick | on the list | ✓ — three separate "clean the holes" steps |
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
  against a required 3000/200 = 15. Page 128 prints T3's winding directly — 23 turns of #28 for
  the primary, 6 turns of #26 for the secondary — and the 40B matches on both turns *and* gauge.
  Nothing to reconcile here.
- **The book's T3 wire lengths are much longer than the kit's**, though: p. 128 says cut 40 cm
  of #28 and 15 cm of #26, against Appendix A's 25 cm and 13 cm. Since the turns counts agree
  exactly, the same winding cannot need 40 cm on one sheet and 25 cm on another — which is
  independent support for the
  [suspected errata](../reference/norcal-40b-parts-list.md#suspected-errata-in-the-manual) in
  the 40B's wire lengths, and a second reason to cut long.
- The temporary 1.5 kΩ stands in for U1's input resistance. The book quotes the SA602AN as
  **1.5 kΩ shunted by 3 pF**; the 40B's U1 is an SA612 or NE602 from the same family. Check
  your own datasheet rather than assuming, because that 3 pF is an explicit element in the
  Figure 6.10 model.
- **A 50 pF trimmer still reaches resonance against T2** on the 40B — range check in the
  [appendix](#appendix-arithmetic-behind-the-sufficiency-claims). Since T2's turns are
  identical to the 40A's, the 66 nH shunt inductor in Figure 6.10 is correct for your board
  as printed.
- **Part D is the one place a scope bandwidth-limit filter is load-bearing.** You are measuring
  the RF Filter's rejection at the VFO image, 2.8 MHz — a deliberately tiny output. But a
  function generator's own second and third harmonics of 2.8 MHz land at 5.6 and 8.4 MHz, which
  is inside the filter's 7 MHz passband. The filter therefore passes the generator's
  *impurities* far better than the fundamental you're trying to measure, and they can dominate
  the trace. Switch the scope's low-pass filter in and the harmonics go away; leave it out and
  you measure your generator instead of your radio. The book says to turn it off again
  afterwards, and means it — leaving it on quietly corrupts every later measurement.
- **Part G's "10-Vpp setting" and Figure 6.13's "20 Vpp" are the same thing.** Figure 6.13 draws
  the source as its open-circuit voltage; the instruction gives the into-50 Ω setting, per the
  [book's standing convention](test-equipment.md). Dial 20 Vpp *indicated* and you are 6 dB hot
  into a filter whose loss you are about to record. Same trap as Problem 8F and 9F.
- **Two numbers from this problem are inputs to a later one.** Part C's combined
  Harmonic-Filter-plus-RF-Filter loss and part G's IF-network loss are both explicitly "save
  this for analyzing receiver performance" — that's Problem 34 (Receiver Response). Record both
  in [`bench-results.md`](bench-results.md) with the measurement conditions, not just the dB
  figure. The book's sanity limits are >7 dB for part C and >10 dB for part G; exceeding either
  means go looking for a bad joint or a coil lead in the wrong hole, not a fudge factor.
- **Part F asks you to calculate C6, then tells you to fit 47 pF regardless.** The designer's
  stated reason is that the radio "sounds best with that value". Do the calculation anyway and
  note the gap — an intentional detune of an IF transformer is a design choice worth
  understanding, and it's the kind of thing that looks like an error later if you don't write
  down that it was deliberate.

---

## Chapter 7 — Acoustics

The odd chapter out. Nothing is soldered, nothing from the kit is used, and the transceiver
is not involved — you build a resonant loudspeaker out of a mailing tube and measure it. The
point is that a tube is a transmission line, a speaker in a tube is a resonator, and everything
you learned about Q, resonance and standing waves in Chapters 3 and 4 transfers to sound
because the mathematics is the same.

That makes it the cheapest chapter to *understand* and, awkwardly, one of the more expensive
to *perform*, because it wants an instrument you almost certainly don't own — a sound level
meter. See the [workarounds](substitutions-and-workarounds.md) for the MCU route.

---

## Problem 17 — Tuned speaker (p. 138–140) — **not on the board**

Build a small speaker into a 16-cm length of cardboard mailing tube so it resonates in the
600–650 Hz range, then measure the resonance and model the tube as a shorted quarter-wave
transmission line (Figure 7.7).

| Needed | Kit? | Verdict |
|---|---|---|
| Cardboard mailing tube, 16 cm of it | ✗ | **Buy/scrounge** — length sets the resonance, so cut to fit |
| Loudspeaker, 2.25 in, ~0.25 W, 8 Ω | ✗ | **Buy** — also becomes the radio's speaker later |
| Cork liner strip | ✗ | **Buy/scrounge** — a friction sleeve so the speaker can slide |
| Glue gun | ✗ | **Buy** if you don't have one |
| Stereo 3.5 mm mini plug, solderable | ✗ | **Buy** — several; you need one for the radio too |
| Foam blocks | ✗ | scrounge |
| **Sound level meter** | ✗ | **The real cost of this chapter** — see below |
| Multimeter, AC volts at 600 Hz | have | ✓ |
| Function generator, 25 mVrms sine, 600–650 Hz | ✗ | **Buy** — trivial spec, no new requirement |

- **The tube length is the design variable, not a fixed part.** 16 cm is what gives a
  quarter-wave resonance in the 600–650 Hz window for the book's tube. If your tube's diameter
  differs, the end correction (Problem 18D) shifts and the length that resonates shifts with
  it. The problem tells you to slide the speaker to trim, which is your adjustment.
- **Why 600–650 Hz and not any convenient frequency:** that's the audio tone the transceiver
  produces, set by the 620 Hz offset between the BFO and the IF filter. Problem 29 sets the
  BFO to exactly that, and Problem 33 tunes the sidetone to it. So this speaker is not a toy —
  it is a matched output transducer for the radio you are building, and it comes back in
  Problems 33–36. Build it properly.
- **The sound level meter is the one genuinely awkward purchase in this chapter.** The book
  specifies a Tenma 72-860 and gives its settings (`Lo`, `S`, `C` — 35–100 dB range, 1.5 s
  averaging, flat weighting). What the problem actually needs is: an **absolute** SPL reading
  in dB, **flat** across 500–700 Hz so that comparisons at different frequencies are fair, a
  **microphone small enough to sit in the mouth of the tube**, and — for Problem 18 — a
  microphone that can be pushed *down* the tube on a rod.
  Only the absolute part is hard. See the
  [workarounds doc](substitutions-and-workarounds.md) for the electret-plus-MCU option and an
  honest account of what calibration costs you.
- **A quarter-watt speaker driven from a function generator will not be loud.** 25 mVrms into
  8 Ω is about 80 µW. That is deliberate — you are measuring a resonance, not filling a room —
  but it means ambient noise sets your noise floor, and the C-weighted 35 dB bottom of the
  meter's range is a real limit. Measure somewhere quiet.

---

## Problem 18 — Acoustic standing-wave ratio (p. 141) — **not on the board**

Extend the tube past a half wavelength, run the microphone down inside it on a marked rod,
and plot pressure against distance. You get a standing-wave pattern, an SWR, and an end
correction — the acoustic twins of Problem 11.

| Needed | Kit? | Verdict |
|---|---|---|
| Tube extension, to past λ/2 (~30 cm total) | ✗ | **Buy/scrounge** — same stock as Problem 17 |
| Phenolic rod with ruler markings, fits the meter's mic | ✗ | **Make one** — any non-resonant rod plus a printed scale |
| Sound level meter reaching 114 dB | ✗ | same instrument as Problem 17 |
| Function generator, 620 Hz sine | ✗ | **Buy** — no new requirement |

- **The rod does not need to be phenolic.** It needs to be rigid, non-metallic, thin enough not
  to block the tube, and marked in centimetres. A wooden dowel with a paper scale glued on is
  fine. What matters is that it holds the microphone on the tube's axis at a repeatable depth.
- **114 dB is the top of this problem, and it is above the Tenma's `Lo` range.** The book has
  you set the amplitude so the *maximum* pressure inside the tube is 114 dB (10 Pa). That is
  the `Hi` range on a meter that has one. If your substitute instrument clips at 100 dB you
  can simply work at a lower drive level — the standing-wave *ratio* is what the problem
  wants, and a ratio doesn't care about the absolute level, as long as you stay above the
  noise floor at the minima. **This is the escape hatch that makes a cheap SPL substitute
  viable for Problem 18 even if it isn't calibrated well enough for Problem 17.**
- **The minima are the hard part, not the maxima.** SWR is max/min, so your accuracy is set
  entirely by how well you can measure the *quietest* point. Take your time there, and expect
  the answer to be sensitive to how well the rod is centred.

---

## Chapter 8 — Transistor switches

Back to the board, and the first two problems that put transistors on it. Between them they
install the Receiver Switch, the Transmitter Switch, the 8 V regulator, the supply jack and
the key jack — after this the radio has power, keying, and a receiver front end that survives
transmit.

**One divergence runs through the chapter: the 40B's Q1 is a 2N3904, not the book's 2N4124.**

---

## Problem 19 — Receiver switch (p. 149–151) — **on the board, and Q1 differs**

Q1 shorts the RF filter to ground during transmit so 2 W of your own transmitter doesn't reach
the Receive Mixer. You measure the RC turn-on and turn-off at the base, then the on–off
rejection ratio at 7 MHz, then model the whole thing.

| Needed | Kit? | Verdict |
|---|---|---|
| Q1 — book says 2N4124 | ✓ **2N3904** | ⚠️ **different part** — see below |
| R1, 1.8 kΩ | ✓ 1.8 kΩ | ✓ |
| C3, 47 nF | ✓ 0.047 µF | ✓ same value, different notation |
| C1 (trimmer), L1 (15 µH) | ✓ | installed in Problem 8; L1 matches at 15 µH |
| J1 Antenna jack | ✓ | installed in Problem 13 |
| **12 V bench supply** for part D | have | ✓ — this is what turns the switch on |
| 50 Ω scope termination | ✗ | **Buy** — low power here, but see Problem 24 |
| Function generator: 1 kHz square, 8 V open-circuit with offset; then 1 Vpp / 10 Vpp 7 MHz sine | ✗ | **Buy** — needs **DC offset** and square+sine |
| Simulator (parts G, H) | ✗ | [see the options](test-equipment.md#puff-and-what-to-use-instead) |

- **Q1 is a 2N3904 on the 40B, and Problem 19H is specifically about the transistor's off
  capacitance.** The book asks you to find the loss caused by the switch transistor's
  capacitance when it is *off*, using C<sub>obo</sub> = 3.5 pF from the 2N4124 data sheet, and
  then to repeat it for the 2N2222A at C<sub>cb</sub> = 10 pF to show why the designer chose
  the low-capacitance part. **Use the 2N3904's own number instead** — it is in the same
  low-capacitance class as the 2N4124, so the *lesson* survives intact and the comparison
  against the 2N2222A still lands. Read C<sub>obo</sub> off the 2N3904 data sheet at the right
  bias; don't carry 3.5 pF across.
  This is the repo's standing rule in miniature: the nominal part changed, the quantity the
  lesson depends on is still measurable, so go and get the real number.
- **The function generator needs a DC offset for part A, and it is not optional.** The book
  wants a 1 kHz square wave swinging 0 V to 8 V open-circuit, which on a 50 Ω generator is a
  4 Vpp setting with a 2 V offset. A generator without offset cannot produce this at all.
  Already covered by [requirement 12](test-equipment.md), but this is the problem that makes
  offset load-bearing rather than convenient.
- **Part D turns the switch on with a 12 V supply, not the generator.** Your bench supply does
  this fine — this is one of the few places the regulated bench supply is exactly right.
- **Parts A and B are scope-technique problems as much as circuit problems.** Measuring an
  initial slope and a factor-of-two decay time on an RC edge needs trigger slope control and
  enough timebase resolution to zoom into the transition. Both are on the
  [scope checklist](../CLAUDE.md#bench-inventory).

---

## Problem 20 — Transmitter switch (p. 151–153) — **on the board**

Q4 is a pnp switch that generates the 8 V TX rail from the key line. Its RC delay is what
makes the transmitter shut down gradually instead of clicking. You install the regulator and
the supply jack in the same pass, so this is the problem after which the radio can be powered
normally.

| Needed | Kit? | Verdict |
|---|---|---|
| Q4, 2N3906 | ✓ | ✓ |
| R24 150 kΩ, R9 47 kΩ | ✓ | ✓ |
| C57 47 nF | ✓ 0.047 µF | ✓ |
| D11 1N4148 | ✓ | ✓ — leave lead length for a probe |
| J3 Key jack (3.5 mm) | ✓ | ✓ |
| U5 78L08 regulator | ✓ LM78L08 | ✓ |
| C42 — book says 10 µF | ✓ **100 µF** | ✓ works; bigger bypass is harmless |
| C43 — book says 47 nF | ✓ **0.1 µF** | ✓ works; same job |
| J2 Supply jack, D7 1N5817 | ✓ | ✓ reverse-polarity protection |
| **1 Ω resistor** in the S1 holes | ✗ | **Buy** — also wanted by Problem 10C |
| **Keying relay** — Magnecraft W171DIP-7 or equivalent | ✗ | **Buy, or substitute** — see below |
| Function generator, 20 Hz 5 Vpp square | ✗ | **Buy** — low-frequency square, no new spec |
| 10:1 probe | have | ✓ |

- **The relay is a test fixture, not a radio part, and it comes back twice more** — Problem 25I
  and Problem 30C both key the transmitter with it. The 40B has no relay: the key jack takes an
  external key, and the book only uses a relay because it needs a *repetitive* key-down/key-up
  cycle that a scope can trigger on.
  The spec it must meet is modest: close a contact to ground at 10–20 Hz, driven from
  something, with switching fast compared to the millisecond-scale envelope you're measuring.
  **An MCU GPIO does this better than a relay** — no contact bounce, exact timing, and a free
  sync output for the scope. See the [workarounds doc](substitutions-and-workarounds.md).
  Buying the relay is still defensible for one reason: it is an inductive load with a snubber
  diode, which is Problem 6 made real. If you liked Problem 6, buy the relay.
- **The 1 Ω resistor in the S1 holes is a current shunt, and the 40B populates S1.** On the 40A
  the power switch is external and S1's holes are free all the way through the course; the book
  puts a 1 Ω resistor there to measure supply current, then replaces it with a wire in
  Problem 33. The 40B ships an S1 slide switch. **Leave S1 unpopulated until Problem 33** and
  follow the book — you will want that current-sense point for Problems 24 and 25, where it is
  the only way to get supply current without breaking into the supply lead.
  Measure the 1 Ω accurately with lead-resistance subtraction; Problem 24 tells you to, and the
  power measurements depend on it.
- **C42 and C43 differ from the book and it doesn't matter.** Both are regulator bypass
  capacitors — one bulk, one high-frequency. The 40B's 100 µF and 0.1 µF do the same job as the
  book's 10 µF and 47 nF. Noted only so you don't think you have the wrong bag.

---

## Chapter 9 — Transistor amplifiers

Three problems that build the transmitter's small-signal chain backwards: the Driver Amplifier
(Problem 21), the same amplifier's input impedance and Miller capacitance (Problem 22), and
the JFET Buffer that isolates it from the Transmit Filter (Problem 23). Everything here is in
the kit; the only divergence is trivial.

**Running theme: 7 MHz sine with a DC offset, and a shorting plug in the Key jack.** You will
want a proper shorting plug rather than a twisted wire — it goes in and out constantly from
here to the end of the book.

---

## Problem 21 — Driver amplifier (p. 175–177) — **on the board**

| Needed | Kit? | Verdict |
|---|---|---|
| Q6, 2N2222A metal can | ✓ TO-18 | ✓ — [40B keeps the metal can](../reference/norcal-40b-vs-40a.md) |
| R12 — book says 20 Ω | ✓ **22 Ω** | ✓ — and the book tells you to *measure* it |
| R13, 500 Ω Drive pot | ✓ 500 Ω trim pot | ✓ |
| R11, 510 Ω | ✓ | ✓ |
| C56 — book says 10 µF electrolytic | ⚠️ **0.047 µF ceramic** | ⚠️ **see the C56 note below** |
| D10, 1N5817 | ✓ | ✓ |
| T1, R14 | ✓ | installed in Problem 15 |
| **Shorting plug for J3** | ✗ | **Buy/make** — 3.5 mm plug with tip shorted to sleeve |
| 50 Ω scope termination | ✗ | **Buy** |
| Function generator, 7 MHz, ~2 V with 0.5 V offset | ✗ | **Buy** |

- **The book prints R12 as 20 Ω; your kit has 22 Ω. This costs you nothing**, because the very
  first instruction is *"Measure the resistance of R12, and make a note of it for later."*
  The book is doing the repo's measure-don't-assume rule for you. Problem 22C then asks for the
  total emitter resistance by measurement too.
- **Watch the emitter current, not the waveform.** The book's ceiling is 50 mA — above that you
  cook Q6. Since you're setting amplitude and offset by eye for "a large sine wave with high
  efficiency", it is easy to walk the offset up past the limit. Put the multimeter on R12 and
  watch it while you adjust. The 22 Ω gives you 22 mV per mA, which is comfortable.
- **Neither this problem nor Problem 22 uses C56 for anything you measure** — it's installed
  here and only becomes load-bearing in Problem 25I. See below.

<details>
<summary>⚠️ <b>The C56 discrepancy — worth resolving before Problem 25</b> (contains no answers, but it is arithmetic)</summary>

Figure 9.19 on p. 176 draws **C56 as a 10 µF polarised electrolytic**. The 40B's Appendix A
lists C56 among the **0.047 µF ceramic monolithics** (with C3, C8, C16, C25, C33, C36, C54,
C57). That is a factor of about 210.

C56 sits across the emitter network and discharges through it when the key opens. The time
constant is roughly C56 × (R12 + R13), so with the book's 10 µF you get hundreds of
microseconds to a few milliseconds depending on the Drive setting, and with 0.047 µF you get
single-digit microseconds. The book's stated design intent is a shutdown "gradual over a time
period of 1 to 2 ms" — an envelope in the microsecond range is exactly the key-clicking
behaviour Problem 20 and Problem 30 warn about.

Three problems depend on this: **21** (installation only), **25I** (measure the factor-of-two
decay of the emitter current and compare with theory), and **30C** (rise and fall times of the
keying envelope, where the book says explicitly "the fall time is controlled by the Driver
capacitor C56").

I have not confirmed this against the 40B schematic, and it is more likely a transcription or
Appendix A error than a real design change — a 40B that clicks would be a well-known
complaint. **Check Appendix D of the 40B manual before Problem 25**, and check what is actually
in the C56 bag. If the kit really does supply 0.047 µF there, ask NM0S before soldering it;
if it supplies a 10 µF electrolytic, the
[parts-list errata](../reference/norcal-40b-parts-list.md#suspected-errata-in-the-manual)
needs another entry.
</details>

---

## Problem 22 — Emitter degeneration (p. 177–178) — **on the board**

A continuation of Problem 21 with no new components — you add a 10:1 probe at the free end of
R11 and extract the voltage gain at both ends of the Drive pot's range, then back out the
Miller capacitance.

| Needed | Kit? | Verdict |
|---|---|---|
| Everything from Problem 21, still connected | — | ✓ |
| Second **10:1 probe with known capacitance** | have? | ⚠️ **you now need two probes at once** |
| Multimeter for resistance | have | ✓ |
| Function generator, 7 MHz 1 Vpp with the Problem 21 offset | ✗ | **Buy** |

- **This is the first problem that needs two 10:1 probes simultaneously** — one at R11 for the
  input, one at R14 for the output. Check you have two, and that you know both their
  capacitances, because the Miller extraction in part D is a capacitive-divider calculation and
  the probe is part of the divider.
- **Turn the generator and supply off before every resistance measurement.** The book says so
  in part C and it is not a formality: an ohmmeter reading into a live biased circuit is
  meaningless.
- **The equivalent circuit in Figure 9.21 uses a 560 Ω source resistance and V₀ = 2 V** — that
  is the generator's 50 Ω plus R11's 510 Ω, and the open-circuit voltage being twice the
  amplitude setting. It is the same into-50 Ω convention as everywhere else in the book.

---

## Problem 23 — Buffer amplifier (p. 178–179) — **on the board**

A JFET source follower that keeps the Driver Amplifier's wildly varying Miller capacitance
(10 pF to 105 pF across the Drive range) from detuning the Transmit Filter.

| Needed | Kit? | Verdict |
|---|---|---|
| Q5, JFET | ✓ **J309** | ✓ — 40B uses J309 for Q2, Q3, Q5, Q8 |
| C36 bypass | ✓ 0.047 µF | ✓ |
| R10, 510 Ω | ✓ | ✓ — leave it a few mm proud for a probe |
| C37, C39 | ✓ | installed in Problem 9 |
| 1.5 kΩ resistor into U4 hole #4 — stands in for the Transmit Mixer | ✗ | **Buy** — E24 kit |
| Shorting plug for J3 | ✗ | **Buy/make** — the Buffer needs 8 V TX |
| Non-metallic tuning tool for C39 | on the list | ✓ |
| 10:1 probe | have | ✓ |

- **Retune C39 every time the probe moves.** The book flags this twice, and it is the whole
  difficulty of the problem: the probe's capacitance is a significant part of the filter's
  tuning capacitance, so the measurement disturbs the thing being measured. Part D exists
  precisely to make you quantify that.
- **The J309 substitution is already established** and carries no consequences here — the
  problem measures g<sub>m</sub> and compares against the book's Figure 9.16 curves, which are
  drawn for the J309 in the first place (see Figure 13.5's caption in Chapter 13).
- **This is the third distinct use of a temporary 1.5 kΩ** (Problem 16, Problem 27's RIT
  reference, and here). Buy several, or accept that you will be unsoldering the same one.

---

## Chapter 10 — Power amplifiers

Two problems, and the largest 40B divergence in the whole book sits in the middle of them.
Problem 24 runs the PA up to 2 W and plots efficiency; Problem 25 measures the thermal
behaviour of the transistor and its heat sink. **The 40B's PA transistor is a different device
in a different package with a different thermal resistance**, which is fine for Problem 24 and
changes the arithmetic of Problem 25.

---

## Problem 24 — Power amplifier (p. 199–200) — **on the board, and the PA transistor differs**

| Needed | Kit? | Verdict |
|---|---|---|
| Q7 — book says **2N3553** (TO-39 can) | ✓ **2SC5964 / 2SC2078** (TO-220) | ⚠️ **different device and package** |
| Plastic spacer to keep the can off the board | ✓ 1/4" round spacer ×4 | ⚠️ **different mounting** — TO-220, not a can |
| Heat sink | ✓ Heatsink ×1 | ✓ supplied |
| C44 — book's value unclear in the figure | ✓ **470 pF** | ⚠️ **verify against the schematic** |
| D12 — book says a **36 V zener** | ✓ **SB160** (60 V Schottky) | ⚠️ **not a zener** — see below |
| RFC1 — book has you install it | ✗ **not in Appendix A** | ⚠️ **gap** — see below |
| 1 Ω current-sense resistor in S1 | ✗ | **Buy** — from Problem 20; measure it properly |
| **50 Ω termination rated ≥ 2.5 W** | ✗ | **Buy** — ⚠️ **not a standard feedthrough** |
| J1 Antenna jack | ✓ | installed in Problem 13 |
| Function generator, 1 Vpp 7 MHz no offset | ✗ | **Buy** |
| 10:1 probe, multimeter | have | ✓ |

- **The 50 Ω termination is a genuine hazard, not a formality.** Problem 24B walks the output
  up to 30 Vpp, which into 50 Ω is 2.25 W, and Problem 25 then holds it there for twenty
  minutes. A garden-variety BNC feedthrough terminator is rated **0.5 W to 1 W** and will
  drift, then fail, then take your measurements with it. You need a termination or dummy load
  rated for at least 2.5 W continuous at 7 MHz — this is the single most important purchase
  in this chapter. Problems 30 and 33 hold 30 Vpp again, so it isn't a one-off.
- **The PA transistor is different, and for Problem 24 that is mostly fine.** The 2N3553 is a
  TO-39 metal can whose case *is* the collector, which is why the book has you slip a plastic
  spacer over the leads and a slip-on heat sink over the can. The 40B's 2SC5964/2SC2078 is a
  TO-220 with a tab, mounted to the kit's own heat sink — **follow the 40B manual's mounting
  instructions, not the book's.** The measurements in parts A–D (output power, supply current,
  efficiency, dissipation) don't care what the package is.
- **Check the 40B's maximum collector voltage before you run part D.** The book opens by
  quoting the 2N3553's 40 V limit and relies on it while you push the output up until the
  efficiency rolls over. The 2SC2078's V<sub>CEO</sub> is *lower* than 40 V. Read the data
  sheet for whichever device is in your kit and know your own ceiling before you go looking for
  the roll-off — this is the one place in the book where "push it until something changes" can
  actually destroy a part that the kit has no spare of.
- **D12 is a Schottky rectifier on the 40B, not a 36 V zener.** The book describes D12 as an
  output clamp that conducts at 36 V to protect the collector, and has you hang a 10:1 probe on
  its cathode to watch the collector voltage. An SB160 is a 60 V, 1 A Schottky — a rectifier,
  not a clamp. The probe point may still be the right place to watch, but **the protection
  story does not transfer**, which compounds the voltage-ceiling point above.
  I have not read the 40B schematic here. **Read Appendix D before Problem 24** and find out
  what actually limits the collector swing on your board.
- **RFC1 is not in the 40B's Appendix A.** The book has you install C44, D12 and RFC1 together.
  Appendix A's molded inductors are L1, L4, L5 and RFC2 only, and the toroid list has no RFC1
  either. Either the transcription missed it, Appendix A missed it, or the 40B's PA collector
  feed is arranged differently. **Check the schematic and your kit bags**; if Appendix A is
  genuinely missing it, that is a sixth
  [errata entry](../reference/norcal-40b-parts-list.md#suspected-errata-in-the-manual).
- **Subtract the lead resistance when you measure the 1 Ω.** The book spells out the technique
  (short the probes, read the leads, subtract). At 1 Ω your test leads are a double-digit
  percentage error, and every supply-power number in Problems 24 and 25 is scaled by it.

---

## Problem 25 — Thermal modeling (p. 200–203) — **the 40B changes a given constant**

A twenty-minute thermal step response: drive the PA at 2.25 W, watch the heat sink warm up,
and extract the thermal resistance and thermal capacitance of a first-order RC model. Then
parts F–I return to the amplifier chain and the keying decay.

| Needed | Kit? | Verdict |
|---|---|---|
| Everything from Problem 24, still connected | — | ✓ |
| **Thermometer** that can sit on a heat sink | ✗ | **Buy, or build** — see below |
| **Heat-sink compound** | ✗ | **Buy** — a small tube lasts forever |
| C48 (10 nF), installed in part F | ✓ 0.01 µF | ✓ |
| Keying relay + cable (part I) | ✗ | from Problem 20 |
| 50 Ω termination ≥ 2.5 W, held for 20 min | ✗ | **Buy** — see Problem 24 |
| Multimeter | have | ✓ |

- **R<sub>θjc</sub> = 25 °C/W is a 2N3553 number, and it is an *input* to this problem, not an
  answer.** The book hands it to you because you cannot measure inside the package, and then
  everything downstream — junction temperature, the split between junction-to-case and
  case-to-ambient — is computed from it. A TO-220 device is in a completely different thermal
  class; typical junction-to-case figures are single-digit °C/W. **Get the figure from the data
  sheet for the transistor actually in your kit and substitute it.** If you carry 25 °C/W
  across, every junction temperature you calculate will be badly wrong, and wrong in the
  dangerous direction.
  The measured quantities — heat-sink temperature rise, the time constant, the dissipated
  power — are all yours and are unaffected. Only the given constant changes.
- **This is the best MCU-instrument opportunity in the book.** The measurement is: log
  temperature once a minute for ten minutes, then once more at twenty. Done with a glass
  thermometer and heat-sink compound, it is twenty minutes of not being able to leave the
  bench, and you get 12 data points read by eye. A thermistor or a DS18B20 on the heat sink
  with an MCU logging every few seconds gives you a properly sampled step response, from which
  the time constant falls out by fitting instead of by the book's two-point estimate — and you
  can leave it running. See the [workarounds doc](substitutions-and-workarounds.md).
  Whatever you use, the repo's rule applies: **write the calibration down next to the code.**
- **Thermal measurements punish impatience.** The book warns you: if something goes wrong you
  have to wait for the board to cool before restarting. Plan the run — supply on, output set to
  30 Vpp, multimeter leads already placed, logging already started — before you begin.
- **Part I needs the keying relay again**, at 20 Hz, and measures the emitter-current decay
  that C56 sets. Read the [C56 note](#problem-21--driver-amplifier-p-175177--on-the-board)
  under Problem 21 before you try to reconcile measurement with theory here.

---

## Chapter 11 — Oscillators

The VFO, and the chapter where a frequency counter stops being optional. Two problems that are
really one long build: Problem 26 constructs and tunes the oscillator, Problem 27 measures its
amplitude limiting and temperature stability and then adds the RIT circuit.

**Two 40B divergences here change numbers you are asked to calculate**: L9 has an extra turn,
and C50 is a bigger air variable. Neither breaks anything; both need noticing before you
compare measurement with theory.

---

## Problem 26 — VFO (p. 219–221) — **on the board**

| Needed | Kit? | Verdict |
|---|---|---|
| L9 — book says 62 t #28 on a 68-7 core | ✓ **63 t** #28, T68-7, 133 cm | ⚠️ **one more turn** — see below |
| C51 390 pF, C52/C53 1200 pF polystyrene | ✓ | ✓ exact match to Figure 11.17 |
| C50 — book says air variable, ~2–25 pF | ✓ **50 pF air trimmer** | ⚠️ **roughly double** — see below |
| D8 varactor, MVAM108 | ✓ | ✓ exact match |
| D9 detector diode | ✓ 1N4148 | ✓ |
| R17 VFO Tune, large pot | ✓ 10 kΩ 10-turn | ✓ |
| R19 47 kΩ, R20 4.7 kΩ, R21 47 kΩ, R23 1.8 kΩ | ✓ | ✓ |
| C49 47 pF, C54 47 nF, C32 150 pF, C7 10 nF | ✓ | ✓ |
| RFC2 1 mH | ✓ | ✓ |
| Q8 JFET | ✓ J309 | ✓ |
| 510 Ω into the R15 hole (temporary ground return) | ✓ | one of the kit's three 510 Ω |
| Nylon bolt, washer and nut for L9 | ✓ | ✓ supplied |
| Bare wire for two probe loops | ✗ | **Buy** — same #22 as Problem 16 |
| **Frequency counter** | ✗ | **Buy, or build** — see below |
| 10:1 probe | have | ✓ |

- **Wind L9 carefully; it is the biggest toroid in the kit and the least forgiving.** 63 turns
  of #28 on a T68-7, spread evenly, no overlaps. The book explicitly warns that if the count is
  wrong or the turns bunch you may have to add or remove one later — and Problem 27H makes you
  calculate the frequency shift from exactly one turn, so you will find out.
  The 40B allots 133 cm for it out of a 274 cm total #28 budget, with no spare. Buy a spool
  before you start; see the
  [wire budget](../reference/norcal-40b-parts-list.md#wire-budget).
- **Your L9 has 63 turns, the book computes with 62.** Problem 26D hands you A<sub>L</sub> =
  5.0 nH/turn² and asks for the inductance and the resonant frequency. The 40B's own figure
  (21 µH at 63 turns) implies A<sub>L</sub> ≈ 5.3 nH/turn², which is consistent — the cores
  vary, which is why the book says "our experience has been that the inductance constant for
  the 68-7 core varies considerably". **Use 63 turns and, if you can, your own measured
  inductance.** The point of the exercise is the *comparison*, and it is more interesting when
  the numbers are genuinely yours.
- **C50 is a 50 pF air trimmer on the 40B, not the book's ~25 pF.** Problem 26D tells you to
  "take C50 to be the average of its fully meshed and unmeshed values, 14 pF". That average is
  a 40A number. **Measure your own C50 at both extremes** and use your own average — it is an
  air trimmer, so a capacitance meter or a resonance measurement against a known inductor will
  get it. The practical effect is that the 40B's VFO has a *wider* setting range than the book
  assumes, which makes Problem 27H's "adjust C50 until the oscillation frequency is 2,085 kHz"
  easier, not harder.
- **Don't cook the polystyrene.** C51, C52 and C53 are polystyrene film and they short out
  internally if the dielectric melts. Low iron temperature, quick joints, and don't reflow them
  a second time to tidy up. These three set the resonator's frequency and its temperature
  coefficient, so a damaged one wrecks Problem 27E–G as well as the radio.
- **This is where you need a frequency counter, and the requirement gets harder in Chapter 12.**
  Here you need to read ~2.1 MHz and see a shift. Problem 29C wants the BFO "measured to the
  nearest hertz" near 4.9 MHz — that is 0.2 ppm, which a plain crystal-referenced counter (MCU
  or bench) will not deliver as an *absolute* reading. The saving grace: Problems 27E and 29C
  measure temperature *coefficients*, which are differences, so short-term stability is what
  matters and absolute accuracy is not. See the
  [workarounds doc](substitutions-and-workarounds.md) for the MCU counter and where its
  reference gives out.

---

## Problem 27 — Gain limiting (p. 221–225) — **on the board**

Parts A–D measure the oscillator's limiting amplitude against theory; E–H measure and predict
its temperature coefficient; then you build the RIT circuit.

| Needed | Kit? | Verdict |
|---|---|---|
| Everything from Problem 26 | — | ✓ |
| U6, LM393N dual comparator | ✓ LM393 | ✓ — the first DIP you solder |
| R16 RIT pot, 1 kΩ | ✓ 1 kΩ panel control | ✓ |
| R15 510 Ω, moved into its proper hole | ✓ | ✓ |
| Jumper wires for the S2 outline | ✗ | **Buy** — bare #22 again |
| 1.5 kΩ into U2 hole 2 (1.4 V reference) | ✗ | **Buy** — E24 kit; fourth use of a temporary 1.5 kΩ |
| **Thermometer** | ✗ | **Buy, or build** — same as Problem 25 |
| **Hair drier** | ✗ | scrounge |
| Vented plastic box to direct hot air | ✗ | **Make** |
| Frequency counter | ✗ | **Buy, or build** |
| 10:1 probe | have | ✓ |

- **Parts E–G are a repeatable thermal measurement, and the box matters more than the drier.**
  You heat the board to 50 °C, switch off, and record frequency against falling temperature.
  What makes this work is that the thermometer and the frequency-determining components reach
  the same temperature — hence the book's plastic box with holes to direct the airflow. Without
  it you measure the thermometer's temperature, not the resonator's.
  **Problem 29C repeats this measurement for the BFO** and warns you again to make sure the
  components and the thermometer both get the hot air. Build the box once, keep it.
- **This is the second and third use of a thermometer, which tips the balance towards building
  one.** Problem 25 (heat sink, 20 minutes, one channel), Problem 27E (board, falling ramp,
  needs simultaneous frequency), Problem 29C (same again, finer). An MCU that logs temperature
  *and* counts frequency on the same timebase turns Problem 27E from a two-handed
  scribble-it-down exercise into a data file. Given that you also need a counter here anyway,
  building one instrument that does both is the obvious move.
- **Solder the IC in the right way round the first time.** The book's warning is well earned —
  the 40B is through-plated, U6 has eight legs, and getting a DIP out of a through-plated board
  without damage is genuinely unpleasant. Check the notch against the silkscreen twice.
- **The 40B has a real S2 switch; the book jumpers it.** The book bypasses S2 with a jumper so
  the RIT is always on during measurements, and adds a second jumper across the S2 ground holes
  as a probe point. **Leave S2 unpopulated and follow the book** — you can fit the switch at
  the end with S1.
- **Part H sets the bottom of the tuning range to 2,085 kHz**, which is also the 40B's nominal
  VFO frequency in its own specifications. That is reassuring rather than coincidental: the
  frequency plans match. If you cannot reach it, the book's remedy is to change the turns count
  on L9 — and your wider C50 gives you more room to avoid that.

---

## Chapter 12 — Mixers

Three SA602-family mixers: the RF Mixer (Problem 28), the Product Detector and its BFO
(Problem 29), and the Transmit Mixer (Problem 30). After Problem 29 the receiver makes audio
for the first time; after Problem 30 the transmitter is complete.

**The 40B ships SA612 or NE602 rather than the book's SA602AN.** Same family, same pinout,
same architecture — the SA612 is the second-source/improved sibling. It matters in exactly one
place, noted under Problem 28.

---

## Problem 28 — RF mixer (p. 237–239) — **on the board**

| Needed | Kit? | Verdict |
|---|---|---|
| U1 RF Mixer | ✓ **SA612 / NE602** | ✓ same family as the book's SA602AN |
| U2 Product Detector | ✓ same | ✓ installed here, used in Problem 29 |
| C5, C8 bypass; C15 (2.2 µF) | ✓ | ✓ |
| R2 RF Gain pot | ✓ 1 kΩ panel control | ✓ — may need T2 nudged aside |
| C1, C2 RF-filter trimmers | ✓ | installed in Problems 8 and 16 |
| Frequency counter, **left connected all lab** | ✗ | **Buy, or build** |
| Function generator, 50 mVpp to max, 7 MHz region | ✗ | **Buy** |
| Scope with **AC coupling** and a **bandwidth-limit filter** | have? | ⚠️ **confirm both** |
| 10:1 probe | have | ✓ |

- **Leave the counter connected for the whole exercise — this is a real instruction, not
  housekeeping.** The counter's ~30 pF plus cable loads the VFO. Unplug it mid-measurement and
  the VFO frequency shifts enough to walk the signal out of the IF filter's passband, and you
  will think the radio is broken. Whatever counter you use or build, **know its input
  capacitance** and treat it as part of the circuit.
- **Part D is the tightest frequency discipline in the book.** You are mixing against the
  *fifth harmonic* of the LO, so a 100 Hz error in the VFO becomes a 500 Hz error at the input
  frequency — enough to miss the response entirely. The book notes that a hand near C50 or L9
  will do it. This is a good argument for the nylon-bolted L9 being properly tightened and for
  not leaning on the bench.
- **The scope's bandwidth-limit filter earns its keep again** (part B), for the same reason as
  [Problem 16D](#problem-16--tuned-transformers-p-126130--on-the-board): you are looking at a
  small IF signal and want the noise off the screen. Remember the book's warning that it costs
  you signal level too, so account for it.
- **AC coupling is mandatory here, not stylistic.** The SA602's outputs sit at a large DC
  offset (about 1.2 V below the supply), and on DC coupling at the gain you need the trace
  leaves the screen.
- **Part E asks you to find the error in Figure 4 of the SA602AN data sheet.** If you are
  working from an SA612/NE602 data sheet the figure numbering may not line up. Get the
  **SA602AN** data sheet specifically for this part — it is in the book's Appendix D and widely
  available — and read the 40B's own part for everything else.

---

## Problem 29 — Product detector (p. 239–242) — **on the board**

Build the BFO as a Clapp oscillator inside U2's own transistor, set it 620 Hz above the IF
filter's centre, and then measure the receiver's gain and its worst spurious responses right
through to audio.

| Needed | Kit? | Verdict |
|---|---|---|
| X5 crystal | ✓ 4.915 MHz HC-49 | ✓ one of the six |
| C17 — book assumes a **7–70 pF** variable | ✓ **50 pF trimmer** | ⚠️ **narrower** — see below |
| C18 270 pF | ✓ | ✓ |
| **3 kΩ resistor** into the C19 holes (detector load) | ✗ | **Buy** — E24 kit |
| Frequency counter with fine resolution | ✗ | **Buy, or build** |
| Thermometer + hair drier + box (part C) | ✗ | from Problem 27 |
| **True-RMS multimeter, floating inputs** | have | ✓ — see below |
| 10:1 probe, short test leads | have | ✓ |

- **C17's range differs and part B computes with the book's.** Problem 29B asks you to
  calculate the minimum BFO frequency you should be able to reach "assuming that the range of
  the variable capacitor C17 is 7 pF to 70 pF". Your 40B trimmer is a 50 pF part. **Measure
  yours and use your own range**; the book itself allows for coming up short ("If you cannot
  reach this frequency, get as close as you can"), so a narrower trimmer is a nuisance rather
  than a blocker — but it changes the number you are comparing against.
- **The book deliberately exploits your multimeter's bandwidth limit, and this is worth
  understanding rather than working around.** From part D onwards it switches from the scope
  to the multimeter for AC voltage, for two stated reasons: the meter's inputs are *floating*,
  so you don't short the output the way a grounded scope lead would; and the meter *rolls off
  above about 100 kHz*, so the 10 MHz sum product and the higher-order junk are ignored for
  free. Your meter is being used as a low-pass filter with a display. Check that yours is
  true-RMS and know roughly where its AC bandwidth ends, because that limit is doing real work
  in the measurement.
- **Keep the meter leads away from L9 and C50.** Same VFO-pulling problem as the counter. The
  book says so explicitly.
- **620 Hz is the number that ties the radio together.** It is the BFO-to-IF offset here, the
  resonance of the tuned speaker from Problem 17, the sidetone frequency in Problem 33, and the
  audio tone you listen for in Problems 34–36. If you changed the speaker's tube length in
  Problem 17 and landed somewhere other than 620 Hz, this is where it comes back to you.

---

## Problem 30 — Transmit mixer (p. 242–244) — **on the board, and it finishes the transmitter**

| Needed | Kit? | Verdict |
|---|---|---|
| U4 Transmit Mixer | ✓ SA612 / NE602 | ✓ |
| X6 crystal, C34 trimmer, C35, C33 | ✓ | ✓ |
| L5 18 µH | ✓ | ✓ — the extra inductor that offsets the TX oscillator |
| C31 — book says 5 pF | ✓ **4.7 pF** | ✓ same substitution as C4/C37 |
| **50 Ω load rated ≥ 2.5 W** | ✗ | **Buy** — 30 Vpp again |
| Keying relay + cable, 10 Hz 5 Vpp | ✗ | from Problem 20 |
| **Sync/trigger cable** from generator to scope | ✗ | **Buy** — BNC-BNC |
| Frequency counter, with 50 Ω in parallel | ✗ | **Buy, or build** |
| Scope with trigger slope, trigger level and **holdoff** | have? | ⚠️ **confirm holdoff** |

- **Install everything except C31 first.** The book is explicit: leaving C31 out keeps the VFO
  disconnected so you can measure the Transmit Oscillator on its own. Fitting it early makes
  part A much harder.
- **Part C needs scope trigger technique more than it needs circuit knowledge.** You are
  measuring 10 %–90 % rise and fall times on a keying envelope with a substantial and variable
  delay. The book walks through the controls to use: trigger slope to pick the leading or
  trailing edge, trigger level to choose where the sweep starts, and **holdoff** to kill the
  extra traces. Check your scope has a holdoff control and remember the book's parting
  instruction to put it back to minimum — left high, it dims every subsequent trace.
- **Part D needs a spectrum analyser and you do not have to own one.** Figure 12.15 *is* the
  spectrum-analyser plot, measured on a NorCal 40A, printed in the book with the frequency
  marked at each line. The exercise is to identify the mixing orders *n* and *m* behind each
  one. It is a paper exercise using supplied data — genuinely no instrument needed. Good news
  worth stating plainly, because "find the spurious products of your transmitter" sounds like
  the most expensive problem in the book and isn't.
  (If you later want to see *your* radio's spectrum, that is what an RTL-SDR plus a big
  attenuator is for — but it is not this problem.)
- **The fall time you measure here is set by C56.** See the
  [C56 note](#problem-21--driver-amplifier-p-175177--on-the-board) under Problem 21 before you
  compare it with anything.

---

## Chapter 13 — Audio circuits

The last chapter of construction. Problem 31 builds the LM386 audio amplifier in three stages
so you can watch each capacitor shape the response; Problem 32 adds the JFET AGC attenuator;
Problem 33 installs everything that is left, puts the board in its box, and aligns the radio.
**At the end of Problem 33 you have a working transceiver.**

Everything in this chapter is in the kit. The costs are temporary resistors and, at the very
end, an attenuator.

---

## Problem 31 — Audio amplifier (p. 250–254) — **on the board**

| Needed | Kit? | Verdict |
|---|---|---|
| U3 audio amplifier | ✓ **LM386** | ✓ book says LM386N-1 |
| C27 100 µF, C41 100 µF, C20/C21 100 nF | ✓ | ✓ |
| C23 2.2 µF (part C), C55 10 nF + R22 1.8 kΩ (part D) | ✓ | ✓ |
| C22 10 nF + R7 47 kΩ (part F) | ✓ | ✓ |
| **8 Ω load resistor**, across the LS outline | ✗ | **Buy** — ⚠️ check power rating |
| **5.6 Ω resistor** + two **1.5 kΩ** (input divider) | ✗ | **Buy** — E24 kit |
| True-RMS multimeter | have | ✓ |
| Function generator with **Vrms amplitude units**, 100 Hz–10 kHz | ✗ | **Buy** — see below |

- **Buy the 8 Ω load with its dissipation in mind.** The book substitutes a resistor for the
  speaker so that a frequency-varying impedance doesn't confuse the measurements, and then has
  you sweep gain across the band with the amplifier at full tilt. An LM386-class amplifier into
  8 Ω can deliver a few hundred milliwatts. A 1/4 W E24 part is marginal and will drift as it
  warms. **Use a 1 W or 2 W 8.2 Ω** (8.2 is the E24 value; measure it and use the measured
  number). It stays in circuit through Problem 32 and most of Problem 33, so it earns its keep.
- **Set the generator to display Vrms, not Vpp, for this whole chapter.** The book says so and
  the reason is practical: the multimeter reads rms, and matching units removes a √2 from every
  gain calculation you do for the next three problems. Any modern generator has the setting.
  Worth confirming before you buy — it is on the [requirements list](test-equipment.md).
- **The input divider exists to stop you saturating the amplifier, and it is easy to get
  wrong.** 5.6 Ω against a pair of 1.5 kΩ is a big attenuation, deliberately. Part A asks you
  to work out the exact relationship between the generator's amplitude setting and V<sub>i</sub>,
  and you carry that ratio through every later gain figure, so get it right once and write it
  down.
- **Mind where the scope ground goes.** The book warns that hooking the scope leads up
  backwards around this amplifier causes oscillations, and in part F it tells you outright not
  to put the scope ground on the differential input side of C20/C21 — use the multimeter there,
  because its inputs float. Same lesson as Problem 29.

---

## Problem 32 — Automatic gain control (p. 254–256) — **on the board**

| Needed | Kit? | Verdict |
|---|---|---|
| Q2, Q3 JFETs | ✓ J309 ×4 | ✓ — Figure 13.5's curves are drawn for the J309 |
| R5 — four matched 2.2 MΩ | ✓ **8-pin SIP network** | ✓ better than discretes; see below |
| D5, D6 Schottky | ✓ 1N5817 | ✓ — the problem asks *why* Schottky |
| R6 AGC Threshold pot | ✓ 10 kΩ trim pot | ✓ (Appendix A mislabels this as R17 — [errata](../reference/norcal-40b-parts-list.md#suspected-errata-in-the-manual)) |
| C29 10 µF, C30 2.2 µF | ✓ | ✓ |
| **300 kΩ resistor** into a C19 hole | ✗ | **Buy** — E24 kit; already needed for Problem 3 |
| 8 Ω load, still fitted | ✗ | from Problem 31 |
| True-RMS multimeter, AC **and** DC | have | ✓ |

- **The 40B's R5 being a resistor network is an upgrade, not a compromise.** The circuit needs
  four *identical* 2.2 MΩ resistors forming matched 2:1 dividers at the two JFET gates; a SIP
  network is matched far better than four 5 % discretes would be. Worth knowing when the
  measurements in part A come out symmetric.
- **The measurement rhythm is the difficulty, not the circuit.** You move one multimeter lead
  back and forth between the 8 Ω load (AC volts, audio output) and D5's anode (DC volts,
  control voltage), switching function each time, and plot one against the other on a log
  axis. The book warns that the sensitivity is wildly non-uniform — long flat stretches, then
  a cliff. Plan to take points adaptively rather than on a fixed grid, and leave enough lead
  length at D5's anode to clip onto, as the book says.
- **Part F sets the AGC threshold pot to a 1 dB reduction, and that setting persists.** Every
  later measurement — Problem 33's gain, Problem 34's MDS — is taken with R6 where you leave it
  here. Write down what you set and why.
- **Leave the 300 kΩ in place at the end.** Problem 33 uses it. (The book's own text in
  Problem 33 refers to removing "the 100-kΩ resistor that we used for the function-generator
  input", where Problem 32 installed a 300 kΩ. Treat that as a slip in the book and remove
  whatever you actually fitted.)

---

## Problem 33 — Alignment (p. 256–260) — **on the board, and it finishes the radio**

Measure the AGC recovery time, install the last dozen parts, box the radio, and align it.

| Needed | Kit? | Verdict |
|---|---|---|
| C19, C26, C28 100 nF, R8 AF Gain 500 Ω, J4 Speaker jack | ✓ | ✓ |
| D1, D2, D3 muting diodes; R3 150 kΩ + D4 | ✓ 1N4148 | ✓ |
| R4 8.2 MΩ — sidetone level | ✓ | ✓ — kit also notes a 15 MΩ option |
| S1, S2 slide switches, at last | ✓ | ✓ — fit them now |
| Enclosure, knobs, feet | ✓ | ✓ 40B supplies break-away enclosure boards |
| Speaker + 3.5 mm plug | ✗ | from Problem 17 |
| **Step attenuator, ≥ 80 dB, 50 Ω** | ✗ | ⚠️ **the big new instrument** — see below |
| Coaxial cable, BNC | ✗ | **Buy** — also Problems 10 and 12 |
| **50 Ω load ≥ 2.5 W** | ✗ | **Buy** |
| Frequency counter, with attenuator/filter for 30 Vpp | ✗ | **Buy, or build** |
| Scope reaching **0.5 s/div** | have | ✓ — trivial on a DSO; use roll mode |
| Switch for the Key jack | ✗ | **Buy/make** |
| Indelible pen | ✗ | genuinely on the parts list |

- **The step attenuator is the last significant purchase in the book, and it is not optional
  from here on.** Problem 33 starts you at **80 dB** of attenuation to find a 20 mVrms signal;
  Problem 34 wants input levels down to **−150 dBm**; Problem 35 sweeps input power over a wide
  range. What you need is 50 Ω, flat at 7 MHz, switchable in steps, with **enough shielding
  that the signal goes through it rather than around it** — the book warns twice about keeping
  cables apart so signals don't couple past the attenuator, and Problem 34B is explicitly about
  chasing down leakage. Leakage, not attenuation, is what limits a cheap attenuator.
  Options — buy a switched step attenuator, chain fixed SMA pads, or build a switched pi-pad
  in a die-cast box — are in the [test-equipment doc](test-equipment.md).
- **The 0.5 s/div sweep in part A is a non-issue on a digital scope but wants roll mode.** At
  half a second per division a DSO in normal trigger mode will sit waiting; roll mode draws it
  continuously, which is what the book's "vertical band sweeping slowly across the screen"
  describes on an analogue instrument.
- **Fit S1 and S2 now, and put a wire where the 1 Ω was.** This is the point where the book
  swaps the 1 Ω current-sense resistor for a bare jumper, so it is also the natural moment to
  install the 40B's two slide switches that you have been leaving out since Problems 20 and 27.
- **The alignment sequence produces numbers you keep.** Sidetone to 620 Hz via C34, BFO to
  620 Hz via C17, RF filter peaked on C1/C2, transmit output 2.25 W via R13, and the RIT centre
  marked on the knob. Problem 34 assumes all of it. Record the settings in
  [`bench-results.md`](bench-results.md) — the marks on the knobs are the book's own idea of
  where to write things down, and a repo is better.
- **Enjoy the part where it works.** The book stops mid-alignment to say there is almost no
  better feeling in electrical engineering than hearing the first signal out of a receiver you
  built. It is right, and it is the only place in 313 pages where it says anything of the kind.

---

## Chapter 14 — Noise and intermodulation

No soldering left. These three problems characterise the finished receiver — sensitivity,
dynamic range, and then a demonstration that it works on the air.

**This is the chapter written for a university lab, and it shows.** Problem 34B wants a second
NorCal 40A. Problem 35 says outright that it "is best done in groups of three, because two
transmitters are needed". Problem 36 is a demonstration to an instructor. A solo builder at
home has to make deliberate choices here, and they are worth making in advance rather than
discovering at part B.

The honest summary: **34 and 35 are both doable alone, with substitutions; 36 needs a licence
and another operator, who is a stranger on the air rather than a lab partner.**

---

## Problem 34 — Receiver response (p. 274–276) — **whole radio**

Plot the audio response, then the output against input power from −150 dBm to −50 dBm, and
extract the minimum discernible signal, the noise-equivalent power and the antenna noise
temperature.

| Needed | Kit? | Verdict |
|---|---|---|
| Finished, aligned transceiver | ✓ | from Problem 33 |
| **Step attenuator, ≥ 80 dB, well shielded** | ✗ | **Buy or build** — from Problem 33 |
| True-RMS multimeter, frequency counter | have / ✗ | ✓ / **Buy or build** |
| Speaker | ✗ | from Problem 17 |
| **A second transceiver** (part B) | ✗ | ⚠️ **substitute** — see below |
| **A 40 m antenna** (parts G–I) | ✗ | ⚠️ **needed, and cheap** — see below |
| Function generator with a **noise output** (part F) | ✗ | *optional* — see below |
| Battery to run the second transmitter | ✓ | the AAAs or a 12 V pack |

- **Part B's second transceiver is about isolation, not about the radio.** The book's stated
  reason for reaching for a second NorCal 40A is that "function generators often have a limited
  power range, and it may be difficult to isolate a function generator from the receiver at low
  power levels". At −150 dBm you are asking for a signal 10⁻¹⁸ W — any leakage path around the
  attenuator swamps it, and a mains-powered generator sitting on the same bench has plenty.
  A battery-powered source in a sealed metal box does not.
  So the substitution is: **a small battery-powered crystal or DDS oscillator in a die-cast box,
  feeding the attenuator through one short length of double-shielded coax.** An Si5351 or
  similar module and a coin cell will out-isolate a bench generator, for the price of a coffee.
  The book's own leakage test in part B is the acceptance test for whatever you build: set
  −150 dBm and confirm the multimeter reads the same as with no signal at all. If it doesn't,
  you have a leak, and the book names the usual suspects (the cable between source and
  attenuator, and the source's proximity to the receiver).
  Details in the [workarounds doc](substitutions-and-workarounds.md).
- **Parts G–I need a real antenna, and this is the cheapest instrument in the whole book.**
  You connect the receiver to an antenna, tune to a quiet spot, and measure the noise. The
  point is that at 7 MHz atmospheric noise — mostly distant lightning — is *larger* than the
  receiver's own noise, which is why the receiver doesn't need to be quieter than it is.
  A half-wave dipole for 40 m is about 20 m of wire, cut in half, fed in the middle. Wire,
  insulators, a length of coax and somewhere to hang it. It costs almost nothing and it is
  needed again for Problems 36 and 39.
  The book also gives you the ear test for whether you're hearing atmospheric noise or receiver
  noise: atmospheric noise has "a boom and crash sound", receiver noise is a steady roar.
- **Part F's noise measurement is optional and the book flags it as such** ("A function
  generator that can produce noise is useful for finding the NEP"). It uses the HP33120A's
  noise output at a known power density. If your generator has a noise mode with a specified
  bandwidth, do it; if not, skip part F or substitute a noise source of known ENR. It does not
  gate anything later.
- **Retune the transmitter to full power afterwards**, as the book says at the end — you
  detuned C39 to get −40 dBm out of it in part B, and Problem 35 needs 2 W.

---

## Problem 35 — Intermodulation (p. 276–277) — **whole radio, and it wants three**

Two transmitters on 7,030 and 7,040 kHz into a power combiner, one receiver listening for the
third-order product near 7,020 kHz. Plot the output against input power and find the dynamic
range.

| Needed | Kit? | Verdict |
|---|---|---|
| **Two independent 7 MHz sources at 2 W** | ✗ | ⚠️ **the substitution problem** — see below |
| **Power combiner**, 2-way, isolation > 20 dB at 7 MHz | ✗ | **Buy or build** — ⚠️ **not a BNC tee** |
| Step attenuator | ✗ | from Problem 33 |
| Receiver, multimeter, speaker | ✓ | ✓ |
| 50 Ω loads ≥ 2.5 W ×2 | ✗ | **Buy** |

- **The combiner is the part people get wrong, and the book explains exactly why.** With a
  plain BNC tee, power from each transmitter flows into the other one, and *each transmitter*
  then generates its own intermodulation products — which land on the same frequencies you are
  trying to measure in the receiver. A power combiner isolates the two sources (typically
  > 20 dB) so that the only intermodulation is the receiver's.
  A 2-way 0° hybrid combiner covering HF is an easy buy (Mini-Circuits ZFSC-2-1 and its clones
  cover 0.002–60 MHz), and it is also a build — a ferrite transmission-line hybrid on a
  binocular core is standard amateur construction. A **resistive** combiner is the wrong
  answer: it gives only about 6 dB of isolation, which is nowhere near enough.
- **The two sources do not have to be NorCal 40s, but they do have to be independent.** What
  the measurement needs is two clean carriers, 10 kHz apart, at roughly equal power, whose own
  intermodulation is far below the receiver's. The book warns that function generators
  "can also produce intermodulation products" at exactly the frequencies of interest — which
  is the same warning as part B of Problem 34, and rules out the lazy option of one two-channel
  generator with its two outputs combined internally.
  Ranked, for a solo builder:
  1. **Your 40B plus one other transmitter.** If you can borrow a second radio, do — it is
     what the book intends and it needs no thought.
  2. **Two separate battery-powered oscillator modules in two separate boxes**, each with its
     own supply, into a proper hybrid combiner. Independent by construction, and the same boxes
     you built for Problem 34B. You will not get 2 W out of them, which is fine: what matters
     is the power *at the receiver input*, and you have an attenuator between anyway. Run the
     numbers before you assume you have enough level.
  3. **Two separate function generators** — acceptable if you have two, but verify the IMD
     floor first by the book's own method: halve the input and check the product drops by 8×,
     not 2×.
  4. **One two-channel generator.** Last resort; the two channels share an output stage and a
     supply, and you are likely measuring the generator.
- **Part A is pure algebra** and needs nothing at all — expand the cube of a sum of two cosines
  and collect terms. Do it before you go anywhere near the bench; it tells you which frequency
  to tune to.

---

## Problem 36 — Demonstration (p. 277) — **on the air**

Bring the finished transceiver, show the construction is complete and neat, receive a weak
signal between 7,000 and 7,040 kHz, and transmit at least 2 W within 200 Hz of it, with the
sidetone matching the received tone.

| Needed | Kit? | Verdict |
|---|---|---|
| Finished transceiver, aligned | ✓ | ✓ |
| 40 m antenna and feedline | ✗ | from Problem 34 |
| **An amateur radio licence** | ✗ | ⚠️ **hard requirement to transmit** |
| A correspondent on the air | ✗ | — |

- **This is the one problem in the book with a legal prerequisite.** Receiving needs no licence
  anywhere. Transmitting on 40 m does. In the US the entry-level Technician class already
  carries CW privileges on part of the 40 m band (7.025–7.125 MHz), which covers most of the
  40B's tuning range; General opens the rest. Elsewhere the equivalent entry-level licence
  generally has HF CW access too. **Check your own country's current rules** — this note is
  orientation, not legal advice.
  If you are going to build a transmitter it is worth getting the licence: the exam is a
  multiple-choice paper that an engineer can pass on a weekend of study, and it converts the
  last three problems from theory into the thing the whole book was for.
- **The "demonstration" framing is the only genuinely un-substitutable part**, and it is also
  the least important. What the problem actually asks you to *do* — receive a real signal,
  answer it, match frequencies within 200 Hz using the RIT centre mark from Problem 33 — you do
  with any correspondent on the band. There is no instructor to satisfy.
- **The 200 Hz specification is why Problem 33's alignment mattered.** Your ability to answer
  on the other operator's frequency rests entirely on the sidetone being set to 620 Hz and the
  RIT centre being marked correctly. If Problem 36 is frustrating, the fix is upstream in
  Problem 33.

---

## Chapter 15 — Antennas and propagation

Three problems to finish the book. **Two of them are paper exercises that need no equipment at
all**, which is a pleasant surprise after Chapter 14. The third asks you to copy Morse code off
the air — the only thing in the book that needs a skill rather than a part.

---

## Problem 37 — Antennas (p. 305–306) — **paper**

| Needed | Kit? | Verdict |
|---|---|---|
| Nothing | — | ✓ **pencil and paper** |

Part A rewrites the Friis transmission formula in terms of gain and applies it to a
line-of-sight UHF link between two aircraft. Parts B and C size a tapped-inductor matching
network for a 3 m car whip on 40 m, with and without capacitive end loading, and ask what the
radiation efficiency comes out as.

- **Nothing to buy, nothing to build.** If you want to check part B against something, an
  antenna modelling program will do it — the book recommends EZNEC, and there are free
  alternatives now (nec2c, xnec2c, 4nec2) that are more than adequate for a whip over ground.
  Entirely optional.
- **The answer to part B is the point of the problem**, and it is the reason mobile HF antennas
  are the way they are. Worth doing carefully rather than skimming.

---

## Problem 38 — Propagation (p. 306–308) — **paper**

| Needed | Kit? | Verdict |
|---|---|---|
| Nothing | — | ✓ **the data is printed in the book** |
| A general-coverage receiver | ✗ | *optional enrichment only* |

Figure 15.24 gives 24 hours of hourly reception reports for four 14.1 MHz beacons and for WWV
and WWVH, taken from Pasadena in June 1993. The exercise is to discuss them — daylight versus
darkness on the path, sunrise and sunset, and the difference between frequencies.

- **You cannot do this one on your own radio even if you want to**, and that is fine. The
  beacons are on 20 m and WWV is on 2.5/5/10/15/20 MHz; the 40B is a single-band 40 m radio. The
  book supplies the data precisely because the measurement is a 24-hour vigil with a
  general-coverage receiver.
- **If you want the modern version anyway**, WWV still transmits, the international beacon
  network still runs on 14.100 MHz, and an RTL-SDR with an upconverter or a WebSDR in a browser
  will let you listen to both without owning anything. WSPR data is the contemporary version of
  exactly this experiment, with a global database instead of one observer's notebook.
  Enrichment, not requirement.

---

## Problem 39 — Listening (p. 308–313) — **whole radio, on the air, receive only**

Copy a two-way Morse conversation off the air and interpret it: call signs, names, locations,
signal reports, power, antennas. Tables 15.1 and 15.2 give the call-sign prefixes and the
abbreviations; Figure 15.28 gives a worked example QSO.

| Needed | Kit? | Verdict |
|---|---|---|
| Finished transceiver | ✓ | ✓ |
| 40 m antenna | ✗ | from Problem 34 |
| **A Morse decoder**, or the ability to copy by ear | ✗ | ⚠️ **build it in software** — see below |
| Speaker | ✗ | from Problem 17 |
| **No licence** | — | ✓ receiving is unlicensed |

- **The decoder is a software problem, and it is squarely in your wheelhouse.** The book
  assumes a hardware Morse decoder box tuned to 600 Hz, with the audio patched in from the
  transceiver. There is no reason to buy one. The signal is a single tone at 620 Hz keyed on
  and off; detection is a Goertzel filter at that frequency plus threshold-and-timing logic to
  turn mark/space durations into dots, dashes and gaps.
  Two routes, both fine: run **fldigi** (free, cross-platform) with the radio's audio into a PC
  sound card, or **write it on the STM32** — a Goertzel bin at 620 Hz on the ADC is a
  couple of hundred lines and it belongs in `firmware/` per the repo's convention. The second
  is more fun and gives you a self-contained instrument; the first gets you copying tonight.
- **The book's own advice is that a decoder is a crutch, and it is right.** Adjusting the RF
  gain so atmospheric noise doesn't produce spurious characters is most of the skill of using
  one — the book notes that noise shows up as strings of `E`s, because a single dot is the
  shortest character. A human ear does better at low signal-to-noise than a naive decoder,
  which is worth knowing before you conclude your decoder is broken.
- **620 Hz, one more time.** The decoder wants the tone the radio produces, which is the tone
  the speaker from Problem 17 was built to resonate at, which is the offset you set in
  Problem 29 and confirmed in Problem 33. The book closes the loop it opened 175 pages earlier.
- **This is the last problem in the book.** After it, the radio is built, aligned,
  characterised, and in use.

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
