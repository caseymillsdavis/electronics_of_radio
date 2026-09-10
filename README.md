# Electronics of Radio — working notes

Notes, references and analysis collected while working through
**Paul Horowitz & David Rutledge, *The Electronics of Radio*** (Cambridge University Press).

The book is a lab course: **39 problems** that build a 40-metre CW transceiver while teaching
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
| [`reference/source-page-coverage.md`](reference/source-page-coverage.md) | Which pages of the book have actually been captured, problem by problem, and the three known gaps. Check here before assuming a problem's text is on hand. |
| [`analysis/problems-01-39-parts-audit.md`](analysis/problems-01-39-parts-audit.md) | **Main doc.** Every component each of the book's 39 problems needs, checked against the 40B kit — plus the instruments, fixtures and one antenna the later chapters add. |
| [`analysis/substitutions-and-workarounds.md`](analysis/substitutions-and-workarounds.md) | How to run the problems without buying everything — substitute values, rescaled frequencies, MCU stand-ins, and what genuinely can't be faked. |
| [`analysis/shopping-list.md`](analysis/shopping-list.md) | **Buying authority.** One consolidated, order-ready list of everything the exercises need, grouped by supplier cart, with tiers and bulk-buying notes for passives. |
| [`analysis/bench-results.md`](analysis/bench-results.md) | **Results log.** Raw measurements and conclusions from problems actually worked at the bench. Contains worked answers — don't read ahead of where you are. |
| [`analysis/test-equipment.md`](analysis/test-equipment.md) | Function-generator requirements derived from the problems, what to use instead of *Puff*, plus accessories and a shopping list. |
| [`firmware/`](firmware/README.md) | MCU code standing in for test equipment — built and flashed from this repo. |
| [`CLAUDE.md`](CLAUDE.md) | Standing context and working agreement — read this first if you're picking the project up. |

## Bench inventory

Have:

- Breadboards
- Bench power supply
- Batteries — a bag of depleted AAAs, which turned out to be the *right* source for Problem 2
  rather than a compromise (high internal resistance is what makes the droop measurable). A
  12 V / 0.8 A-hr SLA is still worth buying only if you want a field battery for the finished
  radio.
- Multimeter
- Oscilloscope (with 10:1 probes)
- MCU dev kits — fair game as substitute instruments, see the workarounds doc

Need:

- Function generator — see [`analysis/test-equipment.md`](analysis/test-equipment.md). Chapters
  4–6 add a **pulse-mode** requirement that can rule models out; check minimum pulse width.
- 10–20 m of RG58/U coax with BNC plugs — Problems 10 and 12.
- A circuit simulator for Problems 13, 14 and 16. The book uses *Puff*;
  [free alternatives here](analysis/test-equipment.md#puff-and-what-to-use-instead).
- Everything else, in one order-ready list:
  [`analysis/shopping-list.md`](analysis/shopping-list.md)

## Manual

The NorCal 40B assembly manual PDF (`Norcal_40b_manual_TH_121623.pdf`, NM0S Electronics,
rev. 2023-12-16) is not committed here. Keep a local copy alongside this repo; page numbers
cited in these notes refer to the printed page numbers in that PDF.

## Progress

**All 39 problems are analysed** — the whole book, Chapters 2 through 15. Source pages for
every problem are on hand with no outstanding capture gaps; the index is in
[`reference/source-page-coverage.md`](reference/source-page-coverage.md).

The remaining work is at the bench, not in the analysis. The tracker's **Bench** column is what
is still empty.

Two things worth knowing before starting Chapters 7–15:

- **The 40B kit has every board component Problems 19–33 install.** But six places differ from
  the book in ways that change a number you're asked to calculate — most importantly the power
  amplifier transistor, whose thermal resistance is a *given* in Problem 25. They're summarised
  in [`reference/norcal-40b-vs-40a.md`](reference/norcal-40b-vs-40a.md) and flagged ⚠️ in the
  tracker.
- **The cost of the later chapters is instruments, not parts** — a 2.5 W 50 Ω load, a frequency
  counter, and an 80 dB step attenuator, plus an antenna. Several have MCU or home-built
  substitutes; see [`analysis/substitutions-and-workarounds.md`](analysis/substitutions-and-workarounds.md).

Bench work has started: **Problem 2 is worked**, results in
[`analysis/bench-results.md`](analysis/bench-results.md). The tracker lives in
[`CLAUDE.md`](CLAUDE.md#problem-tracker).
