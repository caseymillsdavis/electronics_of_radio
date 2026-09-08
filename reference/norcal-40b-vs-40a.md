# NorCal 40B vs NorCal 40A, from the book's point of view

*The Electronics of Radio* builds the **NorCal 40A**. This repo substitutes the **NorCal
40B** (NM0S Electronics). This page records what actually differs where the book's problems
touch the board.

Sources: the 40B manual's *Theory of Operation*, schematic (Appendix D) and parts list
(Appendix A). Claims about the 40A come from the problem statements themselves, so they're
limited to what the book says out loud.

## The good news: reference designators survived

The 40B kept the 40A's designators for the two blocks Problems 8 and 9 use, and kept the
same topology. This is not a coincidence — the 40B is a revision of the same design, not a
clean-sheet radio.

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
[parts audit](../analysis/problems-01-09-parts-audit.md#appendix-arithmetic-behind-the-sufficiency-claims).

### Frequency plan

Identical, so Problem 9's "difference frequency at 2.8 MHz" still applies:

| | 40A (book, Problem 9) | 40B (manual, Specifications) |
|---|---|---|
| VFO | 2.1 MHz | 2.085 MHz nominal |
| Transmit oscillator | 4.9 MHz | 4.915 MHz |
| Sum (transmit) | 7.0 MHz | 7.000 MHz |
| Difference (rejected) | 2.8 MHz | 2.830 MHz |
| IF | — | 4.915 MHz, 4-pole Cohn crystal filter |

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

## Not yet checked

This comparison only covers Problems 1–9. Later chapters solder much more of the board
(crystal filter, VFO, mixers, PA, low-pass filter). Known differences to look into when I get
there:

- PA transistor: the 40B uses a 2SC5964/2SC2078 in TO-220 with a heatsink.
- The 40B's JFETs are J309 (Q2, Q3, Q5, Q8).
- The 40B has an LM393 (U6) for RIT switching, plus an SB160 and four 1N5817 Schottkys.
- The 40B's AGC uses an 8-pin 2.2 MΩ SIP resistor network (R5) rather than discretes.
