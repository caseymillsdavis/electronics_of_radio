# Problems 1–9: what each one needs, vs. what the NorCal 40B kit has

Covers *The Electronics of Radio* Chapter 2 Problems 1–6 (pp. 39–48) and Chapter 3
Problems 7–9 (pp. 65–70).

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

That splits Problems 1–9 cleanly in two:

| Problems | Where the work happens | 40B kit sufficient? |
|---|---|---|
| **1, 7** | Paper only | n/a — nothing to buy |
| **2–6** | Breadboard | **No.** Buy loose parts. Kit covers ~2 of 8 values, and only by cannibalising. |
| **8, 9** | Soldered to the NorCal board | **Yes.** Right parts, right topology, right designators. |

The only real gaps are cheap: four resistor values, a 10 nF capacitor, a couple of
transistors, a battery, and a function generator with AM modulation.

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
