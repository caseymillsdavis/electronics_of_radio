# Electronics of Radio — working notes

Notes, references and analysis collected while working through
**Paul Horowitz & David Rutledge, *The Electronics of Radio*** (Cambridge University Press).

The book's lab problems are built around the **NorCal 40A** transceiver kit, which is no
longer available. This repo tracks the substitution I'm making: the **NorCal 40B** kit from
NM0S Electronics, plus a separate stock of breadboard parts and test gear.

## Contents

| Path | What it is |
|---|---|
| [`reference/norcal-40b-parts-list.md`](reference/norcal-40b-parts-list.md) | Full 40B bill of materials, transcribed from the manual's image-only Appendix A so it's searchable/greppable. Includes suspected errata. |
| [`reference/norcal-40b-vs-40a.md`](reference/norcal-40b-vs-40a.md) | How the 40B differs from the 40A where the book's problems touch the board. |
| [`analysis/problems-01-09-parts-audit.md`](analysis/problems-01-09-parts-audit.md) | **Main doc.** Every component each of Problems 1–9 needs, checked against the 40B kit. |
| [`analysis/test-equipment.md`](analysis/test-equipment.md) | Function-generator requirements derived from the problems, plus accessories and a shopping list. |

## Bench inventory

Have:

- Breadboards
- Bench power supply
- Multimeter
- Oscilloscope (with 10:1 probes)

Need:

- Function generator — see [`analysis/test-equipment.md`](analysis/test-equipment.md)
- 12 V / 0.8 A-hr sealed lead-acid battery (Problem 2 does not work off a regulated supply)
- A small bag of breadboard discretes — see the shopping list

## Manual

The NorCal 40B assembly manual PDF (`Norcal_40b_manual_TH_121623.pdf`, NM0S Electronics,
rev. 2023-12-16) is not committed here. Keep a local copy alongside this repo; page numbers
cited in these notes refer to the printed page numbers in that PDF.
