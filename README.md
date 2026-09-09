# Electronics of Radio — working notes

Notes, references and analysis collected while working through
**Paul Horowitz & David Rutledge, *The Electronics of Radio*** (Cambridge University Press).

The book is a lab course: **40 problems** that build a 40-metre CW transceiver while teaching
the analog and RF theory behind each stage. I'm an embedded software engineer learning analog
and RF, working through it at my own pace — problems get analysed here a few at a time as I
reach them.

Two substitutions run through everything: the book's **NorCal 40A** kit is discontinued, so
the radio is a **NorCal 40B** from NM0S Electronics; and where the book's exact parts aren't
worth buying, we work out a substitute instead. Fidelity to a 1990s course parts list is not
the goal.

## Contents

| Path | What it is |
|---|---|
| [`reference/norcal-40b-parts-list.md`](reference/norcal-40b-parts-list.md) | Full 40B bill of materials, transcribed from the manual's image-only Appendix A so it's searchable/greppable. Includes suspected errata. |
| [`reference/norcal-40b-vs-40a.md`](reference/norcal-40b-vs-40a.md) | How the 40B differs from the 40A where the book's problems touch the board — including the Problem 13 harmonic filter, where the values genuinely diverge. |
| [`analysis/problems-01-16-parts-audit.md`](analysis/problems-01-16-parts-audit.md) | **Main doc.** Every component each of Problems 1–16 needs, checked against the 40B kit. |
| [`analysis/substitutions-and-workarounds.md`](analysis/substitutions-and-workarounds.md) | How to run the problems without buying everything — substitute values, rescaled frequencies, MCU stand-ins, and what genuinely can't be faked. |
| [`analysis/test-equipment.md`](analysis/test-equipment.md) | Function-generator requirements derived from the problems, what to use instead of *Puff*, plus accessories and a shopping list. |
| [`firmware/`](firmware/README.md) | MCU code standing in for test equipment — built and flashed from this repo. |
| [`CLAUDE.md`](CLAUDE.md) | Standing context and working agreement — read this first if you're picking the project up. |

## Bench inventory

Have:

- Breadboards
- Bench power supply
- Multimeter
- Oscilloscope (with 10:1 probes)
- MCU dev kits — fair game as substitute instruments, see the workarounds doc

Need:

- Function generator — see [`analysis/test-equipment.md`](analysis/test-equipment.md). Chapters
  4–6 add a **pulse-mode** requirement that can rule models out; check minimum pulse width.
- A battery for Problem 2, which does not work off a regulated supply. A 9 V alkaline is
  enough; the book's 12 V / 0.8 A-hr SLA is only worth it if you want a field battery for the
  finished radio.
- 10–20 m of RG58/U coax with BNC plugs — Problems 10 and 12.
- A circuit simulator for Problems 13, 14 and 16. The book uses *Puff*;
  [free alternatives here](analysis/test-equipment.md#puff-and-what-to-use-instead).
- Very little else — see the
  [minimum shopping list](analysis/substitutions-and-workarounds.md#revised-shopping-list-if-you-want-the-minimum)

## Manual

The NorCal 40B assembly manual PDF (`Norcal_40b_manual_TH_121623.pdf`, NM0S Electronics,
rev. 2023-12-16) is not committed here. Keep a local copy alongside this repo; page numbers
cited in these notes refer to the printed page numbers in that PDF.

## Progress

Problems 1–16 analysed — Chapter 4 (transmission lines), Chapter 5 (filters) and the first two
transformer problems of Chapter 6. Problem 16 is analysed only as far as the uploaded pages go.
The tracker lives in [`CLAUDE.md`](CLAUDE.md#problem-tracker).
