# NorCal 40B vs NorCal 40A, from the book's point of view

*The Electronics of Radio* builds the **NorCal 40A**. This repo substitutes the **NorCal
40B** (NM0S Electronics). This page records what actually differs where the book's problems
touch the board.

Sources: the 40B manual's *Theory of Operation*, schematic (Appendix D) and parts list
(Appendix A). Claims about the 40A come from the problem statements themselves, so they're
limited to what the book says out loud.

## The good news: reference designators survived

The 40B kept the 40A's designators for every block Problems 8–16 touch, and mostly kept the
values too. This is not a coincidence — the 40B is a revision of the same design, not a
clean-sheet radio. The one place the values genuinely part company is the transmit harmonic
filter of Problem 13.

### RF filter — Problem 8 (series resonance)

The book: *"Install C1 and L1 on the NorCal 40A board. C1 is a variable capacitor with a
nominal range from 8 to 50 pF, and L1 is an inductor with an inductance of 15 µH."*

The 40B: `C1` is a 50 pF trimmer, `L1` is a 15 µH molded choke (brown-green-black), and the
*Theory of Operation* says the receiver's RF input *"is routed to U1 via C1 and L1 (sheet 1),
which form a low-loss series-resonant circuit."*

**Same part values, same job, same designators.** Problem 8 transfers directly.

### Transmit filter — Problem 9 (parallel resonance)

The book: *"This filter is made up of C37, C38, C39, and L6... C37 (5-pF disk) and C38
(100-pF disk)... L6 uses a T37-2 core... 28 turns of #28 wire."*

The 40B schematic (sheet 2) shows exactly Figure 3.10b: the transmit mixer U4 output feeds
`C37` in series into a node with `C38`, `C39` and `L6` all to ground, then out through R10
to the buffer.

| | 40A (per the book) | 40B |
|---|---|---|
| C37 | 5 pF disk | **4.7 pF** NP0, marked `479` |
| C38 | 100 pF disk | 100 pF NP0, `101` |
| C39 | variable | 50 pF trimmer |
| L6 | T37-2, **28 t** #28, 40 cm | T37-2, **30 t** #28, 50 cm (schematic: 43 cm) |
| Nominal L6 | 4.0 nH/t² × 28² = 3.1 µH | 4.0 nH/t² × 30² = **3.6 µH** (schematic says 3.5 µH) |

**Consequences for Problem 9:** use N = 30 in part B, and 4.7 pF for C37 in part A. Your
measured `f0` in 9A will land lower than a 40A builder's, and C39 in 9C will sit further from
its maximum. Everything the problem asks you to do still works — see the range check in the
[parts audit](../analysis/problems-01-39-parts-audit.md#appendix-arithmetic-behind-the-sufficiency-claims).

### Frequency plan

Identical, so Problem 9's "difference frequency at 2.8 MHz" still applies:

| | 40A (book, Problem 9) | 40B (manual, Specifications) |
|---|---|---|
| VFO | 2.1 MHz | 2.085 MHz nominal |
| Transmit oscillator | 4.9 MHz | 4.915 MHz |
| Sum (transmit) | 7.0 MHz | 7.000 MHz |
| Difference (rejected) | 2.8 MHz | 2.830 MHz |
| IF | — | 4.915 MHz, 4-pole Cohn crystal filter |

### Harmonic filter — Problem 13 (low-pass) — **the one real divergence**

The book: *"a low-pass ladder filter... consisting of the toroidal inductors L7 and L8 and the
disk capacitors C45, C46, and C47"*, with C45 = 330 pF, C46 = 820 pF, C47 = 330 pF, and both
inductors 18 turns of #26 on a T37-2.

The 40B keeps all six designators and changes every value:

| | 40A (per the book) | 40B (Appendix A) |
|---|---|---|
| C45 | 330 pF disk | **390 pF** NP0 200 V, `391` |
| C46 | 820 pF disk | **1000 pF** NP0 200 V, `102` |
| C47 | 330 pF disk | **1000 pF** NP0 200 V, `102` |
| L7 | T37-2, **18 t** #26, 30 cm | T37-2, **15 t** #26, 24 cm |
| L8 | T37-2, **18 t** #26, 30 cm | T37-2, **12 t** #26, 20 cm |
| Nominal L7 | 4.0 nH/t² × 18² = 1.30 µH | 4.0 nH/t² × 15² = **0.90 µH** (manual agrees) |
| Nominal L8 | 4.0 nH/t² × 18² = 1.30 µH | 4.0 nH/t² × 12² = **0.58 µH** (manual agrees) |

**Consequences for Problem 13:** the method survives intact and every numerical answer moves.
The 40B's filter is a lower-impedance design — `√(L/C)` for the middle section is ~30 Ω against
the 40A's ~40 Ω — which is what you would expect of a radio built to make more power off the
same supply.

**One thing you must look up rather than assume: which end is which.** Appendix A lists values,
not order, and the 40B's filter is asymmetric (390 / 1000 / 1000). Depending on which capacitor
faces the power amplifier, the impedance the filter presents to it differs by more than a
factor of five — and finding that impedance is Problem 13D, with 13E asking you to halve it. Get
Appendix B (placement) and Appendix D (schematic) out before soldering. Numbers in the
[parts audit](../analysis/problems-01-39-parts-audit.md#appendix-arithmetic-behind-the-sufficiency-claims).

### IF filter — Problem 14 (Cohn crystal filter) — matches

| | 40A (per the book) | 40B |
|---|---|---|
| Topology | 4-element Cohn, X1–X4 | **4-pole Cohn** (manual, *Specifications*) |
| C9–C13 | 270 pF | ✓ 270 pF NP0 5%, `271` |
| Crystals | 6 matched, 4.9135 MHz | ✓ 6 × HC-49, **4.915 MHz** |
| L4 (matching) | 18 µH | ✓ 18 µH molded, brown-grey-black |
| C14 (matching) | 47 pF | ✓ 47 pF NP0 5%, `470` |
| Detector/mixer IC | SA602AN | SA612 or NE602 — same family |

**Two things to carry into the problem.** First, **start the frequency hunt at 4,915,000 Hz**,
not the book's 4,913,500 — the 1.5 kHz offset is a long walk at 1 Hz steps. Second, **the book
assumes the crystals arrive matched to 20 Hz** because Wilderness Radio sorted them for the
40A; the 40B manual doesn't say whether NM0S does. Problem 14A is itself the sorting procedure,
so measure all six, use the closest four for X1–X4, and put the outliers in the mixer
oscillators where the spread doesn't matter.

Part I quotes an upper-sideband spur 1,240 Hz above the signal — twice the 40A's 620 Hz CW
offset. Check the 40B's offset in *Specifications* before quoting a rejection figure at that
frequency.

The kit also has **no plastic crystal spacers** and **no bare #22 wire** for grounding the
crystal cans; neither appears in Appendix A. See the
[workarounds](../analysis/substitutions-and-workarounds.md#problem-14-crystal-spacers-bare-wire-and-the-can-grounds).

### Driver transformer — Problem 15 (T1) — exact match

| | 40A (per the book) | 40B |
|---|---|---|
| Core | FT37-43, **orange dot** = #43 ferrite | ✓ FT37-43, black with orange dot |
| Primary | 14 t #26, 25 cm | ✓ 14 t #26, **23 cm** |
| Secondary | 4 t #26, 10 cm | ✓ 4 t #26, 10 cm |
| R14 | 100 Ω | ✓ 100 Ω |

The only difference is the primary wire length, and only on paper — cut the book's 25 cm.

### Tuned transformers — Problem 16 (T2, T3) — matches, two small notes

| | 40A (per the book) | 40B |
|---|---|---|
| T2 core | FT37-61, `A_l` = 66 nH/t² | ✓ FT37-61 |
| T2 primary | 1 t **bare #22**, 5 cm | 1 t **#26**, 5 cm (schematic: 8 cm) |
| T2 secondary | 20 t #26, 35 cm | ✓ 20 t #26, 31 cm |
| T3 | 3 kΩ → 200 Ω step-down (turns not printed in the text) | 23 t #28 pri, 6 t #26 sec |
| C2 | variable | ✓ 50 pF trimmer |
| C4 | 5 pF | ✓ **4.7 pF** NP0, `479` |

- **T2's turns are identical**, so Figure 6.10's model — a 66 nH shunt inductor (`1² × 66 nH`,
  the magnetising inductance referred to the one-turn primary) feeding an ideal 1:20 — is
  correct for the 40B as printed. Only the primary's wire gauge differs, which one turn cannot
  care about.
- **T3's 23:6 is exactly right** for the match the problem describes: `(23/6)² = 14.7` against a
  required `3000/200 = 15`. The book doesn't print T3's turns in the pages transcribed here, so
  the 40B's are the ones to use.
- **C4 is 4.7 pF, not the 5 pF in Figure 6.10** — the same substitution as C37 in Problem 9, and
  just as harmless.

### The T37-2 inductance constant checks out on every toroid in the kit

Problem 13B hands you `A_l = 4.0 nH/turn²` for the red T37-2 cores and asks you to compute L7
and L8. On a 40B you can check it first, because Appendix A states both the turns and the
inductance for every toroid:

| Ref | Turns | `4.0 nH × N²` | Manual says |
|---|---|---|---|
| L2 | 13 | 0.68 µH | 0.68 µH ✓ |
| L6 | 30 | 3.60 µH | 3.5 µH (rounded) |
| L7 | 15 | 0.90 µH | 0.90 µH ✓ |
| L8 | 12 | 0.58 µH | 0.58 µH ✓ |

The white T68-7 (L9, 63 t, 21 µH) implies `A_l = 5.3 nH/t²`, matching the published figure for
that core. So the book's constant is right for your cores, and Problem 13B's arithmetic is a
confirmation rather than an article of faith. **The manual's stated inductances are nominal,
not measured** — the tolerance on powdered-iron `A_l` is typically ±5–10%, and the real number
depends on how tightly you wound it.

## Differences that matter elsewhere

### Receive current drain — Problem 2C

Problem 2C: *"When the NorCal 40A is receiving, it draws 20 mA."*

The 40B manual gives **15–20 mA** receiving (Specifications), and the Initial Test step says
to expect **15–18 mA**. So the book's 20 mA figure is a fine upper bound for the 40B; if you
want to redo the battery-life arithmetic with your own radio's number, measure it during the
Initial Test.

### Q6 is a metal-can 2N2222A, not a plastic P2N2222A

Problem 5's transistor-switch section (Figure 2.31) and Problem 6 use a **P2N2222A** — the
plastic TO-92 part; the book even explains *"'P' is for plastic."* The 40B kit's Q6 is a
**2N2222A in a TO-18 metal can**. Electrically equivalent for this experiment, but:

- The pinout is different. TO-18 pins are on a small circle keyed to the case tab; TO-92 is
  a flat row. Read the right datasheet before wiring the breadboard.
- The kit has exactly one, the experiment deliberately makes inductive spikes that *"can
  destroy a transistor"*, and it is soldered to the board later with a ferrite bead on its
  base lead. **Do not use the kit's Q6 for this experiment.** Buy TO-92 P2N2222A/PN2222A.

### Board layout is different

The 40B PCB is not the 40A PCB. Component *locations* and trace routing differ, so wherever
the book tells you which pad or trace to probe, you'll have to re-find it using the 40B's
Appendix B (component placement drawing) and Appendix D (schematic). The manual warns the
board is double-sided with plated-through holes, which makes de-soldering mistakes painful —
worth extra care given the book has you soldering parts out of the manual's order.

### Assembly order conflicts with the book

The 40B manual builds in one pass, grouped by part type: all fixed resistors → diodes and
molded chokes → fixed capacitors → electrolytics → trimmers → transistors/ICs/crystals →
toroids → transformers.

The book instead has you solder a handful of parts, measure them, then continue (C1 + L1 for
Problem 8; C37, C38 and L6 for Problem 9, adding C39 partway through). These orders are
incompatible, and the book's is the one to follow if you want the measurements. Nothing in
the 40B design requires the manual's grouping — it's a convenience for keeping the board
stable and reducing flip-overs. Just be deliberate: with plated-through holes, a part in the
wrong hole is a bad afternoon.

Chapters 5 and 6 make the divergence wider, not narrower. Problem 13 adds L7, L8, C45–C47 and
the BNC jack J1; Problem 14 adds X1–X4, C9–C13, L4 and C14; Problem 15 adds T1 and R14;
Problem 16 adds T2, T3, C2 and C4. That is capacitors, inductors, crystals, transformers, a
connector and a resistor interleaved in an order the manual never contemplates — and three of
those problems also have you solder in a temporary resistor and then **wick it back out**.

Two habits worth adopting now:

- **Work from a marked-up copy of Appendix B.** Tick parts off as you fit them, in the book's
  order, rather than trying to hold two orderings in your head.
- **Take the "leave the leads proud" instructions seriously.** The book repeatedly asks for
  leads left partly exposed for test hooks (C45 in Problem 13, R14 in Problem 15). Trimming
  them flush because the manual's photos look tidy costs you the measurement.

## Not yet checked

This comparison rests on the manual's *Theory of Operation*, *Specifications* and Appendix A.
**It has not been checked against Appendix D (the schematic)** for Chapters 5 and 6, nor for
Chapters 7–15. Open questions in rough order of how much they'd cost to get wrong:

- **The harmonic filter's element order** (Problem 13) — which of C45/C47 faces the power
  amplifier. Changes Problem 13D's answer by more than 5×. Read the schematic first.
- **Whether NM0S sorts the crystals** (Problem 14) and to what tolerance. Problem 14A measures
  it either way, so this costs nothing to find out the hard way.
- **The 40B's CW offset** — Problem 14I's 1,240 Hz upper-sideband spur is 2× the 40A's 620 Hz.
- **The PA's rated output** — Problem 13 opens with the 40A's 2 W.
- Whether C6 still resonates T3's magnetising inductance the way p. 124 describes for the 40A.

### Chapters 7–15 — checked against Appendix A, **not** against the schematic

Problems 17–39 have now been audited part by part in
[`../analysis/problems-01-39-parts-audit.md`](../analysis/problems-01-39-parts-audit.md).
**Every board component they install is in the 40B kit.** The differences below are the ones
that change a number or a limit; each is written up in the audit next to the problem it hits.

| Ref | Book (40A) | 40B | Problem | Why it matters |
|---|---|---|---|---|
| **Q7** | 2N3553, TO-39 can | 2SC5964 / 2SC2078, TO-220 | 24, 25 | Mounting instructions don't transfer (can-is-collector vs tab), the V<sub>CEO</sub> ceiling differs, and the thermal resistance is in a different class |
| **R<sub>θjc</sub>** | 25 °C/W, given for the 2N3553 | whatever the TO-220 part specifies | 25 | It is an **input** to Problem 25, not a result. Carry it across and every junction temperature is wrong |
| **Q1** | 2N4124 | 2N3904 | 19 | Part H computes switch loss from C<sub>obo</sub> = 3.5 pF, a 2N4124 figure |
| **C50** | air variable, ~2–25 pF | 50 pF air trimmer | 26, 27 | Part D's "average is 14 pF" is a 40A number; the 40B tunes wider |
| **C17** | assumed 7–70 pF | 50 pF trimmer | 29 | Part B computes the reachable BFO range from the book's figure |
| **L9** | 62 turns | 63 turns | 26, 27 | Parts D and H are built on the turns count |
| **R12** | 20 Ω | 22 Ω | 21, 22 | Trivial — the book tells you to measure it anyway |
| **C42 / C43** | 10 µF / 47 nF | 100 µF / 0.1 µF | 20 | Trivial — regulator bypass, same job |
| **C31** | 5 pF | 4.7 pF | 30 | Same substitution as C4 and C37 |
| **U1, U2, U4** | SA602AN | SA612 / NE602 | 28–30 | Same family and pinout. Only Problem 28E cares — it asks you to find an error in a specific figure of the **SA602AN** data sheet |
| **S1, S2** | left unpopulated through the course | supplied slide switches | 20, 24, 27, 33 | The book uses their empty holes as a current shunt and a jumper. Leave both out until Problem 33 |

Confirmed the same, and worth knowing: **J309** for Q2/Q3/Q5/Q8 (and Figure 13.5's conductance
curves are drawn for the J309 in the first place), **MVAM108** for D8, **LM393** for U6,
**LM386** for U3, **LM78L08** for U5, and the six **4.915 MHz** crystals. The 40B's **R5**
being an 8-pin 2.2 MΩ SIP network rather than four discretes is an improvement — the circuit
needs four *matched* resistors.

### Three things to resolve from Appendix D before you need them

None of these is settled by Appendix A alone, and each has a problem riding on it.

1. **C56 — the largest open question.** Figure 9.19 (p. 176) draws C56 as a **10 µF polarised
   electrolytic**; the 40B's Appendix A lists C56 among the **0.047 µF ceramics**. That is a
   factor of ~210 on the capacitor that sets the transmitter's key-up decay, and three problems
   depend on it: 21 (install), 25I (measure the emitter-current decay against theory) and 30C
   (rise and fall times of the keying envelope). A 40B keying in microseconds would click badly
   enough to be a known complaint, so this looks more like an errata than a design change —
   but **check the schematic and the parts bag before Problem 25**.
2. **D12.** The book calls it a zener that conducts at 36 V to protect the PA's collector, and
   has you probe its cathode. The 40B lists an **SB160**, a 60 V Schottky rectifier. The probe
   point may be right; the protection story is not. Read the schematic before running
   Problem 24 up to its efficiency roll-off.
3. **RFC1.** Problem 24 has you install C44, D12 and RFC1 together. **RFC1 does not appear in
   the 40B's Appendix A at all** — the molded inductors are L1, L4, L5 and RFC2, and the toroid
   list has no RFC1 either. Check the schematic and the bags; if Appendix A really omits it,
   that is another entry for the
   [parts-list errata](norcal-40b-parts-list.md#suspected-errata-in-the-manual).
