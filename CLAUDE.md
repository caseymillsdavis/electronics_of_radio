# Working agreement for this repo

## What this is

Notes and analysis for working through **Paul Horowitz & David Rutledge, *The Electronics of
Radio*** (Cambridge University Press). The book is a lab course: **40 problems** that build a
40-metre CW transceiver while teaching the analog and RF theory behind each stage.

## Two standing facts about how work arrives here

1. **The book is 40 problems long and they arrive incrementally.** The owner photographs
   pages and uploads them a few problems at a time. As of the last update, **Problems 1–9 have
   been analysed** (see the tracker below). When new screenshots appear, extend the existing
   docs rather than starting parallel ones — the per-problem tables and the shopping list are
   meant to grow.
2. **The radio is a NorCal 40B, not the book's NorCal 40A.** The 40A kit is discontinued. The
   40B (NM0S Electronics) is a revision of the same design and so far maps well, but every
   problem that solders to the board needs checking against
   [`reference/norcal-40b-vs-40a.md`](reference/norcal-40b-vs-40a.md) before it's assumed to
   transfer.

## Who this is for

An **experienced embedded software engineer** learning analog and RF for the first time.
Practical consequences:

- **Assume fluency in:** C, MCUs, timers/PWM/ADC/DAC/DMA, digital logic, sampling and
  quantisation, instrumentation as a concept, reading datasheets, basic circuit algebra.
  Don't explain these.
- **Don't assume fluency in:** analog intuition, RF practice, why a circuit is arranged the
  way it is, what's normal on a bench. Explain these, and explain *why* a value was chosen,
  not just what it is.
- Being told "buy this part" is less useful than being told what the part has to *do*.

## The DIY principle

**We are not reproducing the book exactly.** The goal is understanding, not fidelity to a
parts list from a 1990s course kit. So, whenever a component or instrument is missing:

1. **Say what the problem is actually teaching**, and which quantities the lesson depends on.
2. **Offer the workaround first** — a substitute value, a rescaled frequency, junk-box parts
   measured with the DMM, an MCU standing in for an instrument. There are MCU dev kits on the
   bench and using them is encouraged.
3. **Then say what buying the real thing gets you**, honestly, so it's an informed choice.
4. Only call something a hard blocker when it genuinely is, and say why.

The single most useful unlock: **for almost every passive in this book, the nominal value
doesn't matter — knowing the actual value does.** There's a good multimeter on the bench.
Measure the junk-box part and use the measured number in the calculation.

Workarounds live in
[`analysis/substitutions-and-workarounds.md`](analysis/substitutions-and-workarounds.md).
Keep it current as new problems land.

## Bench inventory

| Have | Notes |
|---|---|
| Oscilloscope | "very nice"; 10:1 probes. Confirm input C and probe C — Problems 3 and 9 need them as inputs |
| Bench power supply | Regulated. Useless for Problem 2 (needs a source with real internal resistance) |
| Multimeter | Good one. The workhorse for the measure-don't-assume approach |
| Breadboards | |
| MCU dev kits | Fair game as substitute instruments |
| **Function generator** | **Not yet owned.** Requirements and options in [`analysis/test-equipment.md`](analysis/test-equipment.md) |

Update this table when gear is bought.

## Conventions

- **No spoilers in the body text.** The point is to work the problems. Where arithmetic is
  needed to justify a claim (does this trimmer have enough range? is this substitution
  valid?), put it behind a `<details>` block with a clear warning, as in the parts audit.
- **Cite page numbers**: book pages as "p. 41", 40B manual pages by their printed number.
- **Transcribe image-only source material** into markdown so it's greppable — the 40B
  manual's Appendix A was scanned images and is now
  [`reference/norcal-40b-parts-list.md`](reference/norcal-40b-parts-list.md). Do the same for
  anything else that arrives as pictures.
- **Distinguish verified from inferred.** Published spec, measured on the bench, and "this is
  what I'd expect" are three different things; say which.
- **Don't commit the manual PDF or extracted page images** — copyrighted vendor material.
  Reference it instead.
- Prose in these docs uses en/em dashes and Ω/µ freely; keep it consistent.

## Repo layout

```
CLAUDE.md                              this file
README.md                              orientation and index
reference/   norcal-40b-parts-list.md  transcribed 40B BOM + suspected errata
             norcal-40b-vs-40a.md      where the 40B differs from the book's radio
analysis/    problems-01-09-parts-audit.md   per-problem component audit
             substitutions-and-workarounds.md  how to avoid buying things
             test-equipment.md         function generator spec + shopping list
```

New per-problem analysis extends `analysis/problems-01-09-parts-audit.md` (rename its range
as it grows) rather than creating a file per problem.

## Problem tracker

| # | Chapter | Title | Board work? | Analysed |
|---|---|---|---|---|
| 1 | 2 Components | Thevenin and Norton equivalents | no (paper) | ✅ |
| 2 | 2 Components | Sources | no | ✅ |
| 3 | 2 Components | Capacitors | no | ✅ |
| 4 | 2 Components | Diode detectors | no | ✅ |
| 5 | 2 Components | Inductors | no | ✅ |
| 6 | 2 Components | Diode snubbers | no | ✅ |
| 7 | 3 Phasors | Parallel-to-series conversion | no (paper) | ✅ |
| 8 | 3 Phasors | Series resonance | **yes** — C1, L1 | ✅ |
| 9 | 3 Phasors | Parallel resonance | **yes** — C37, C38, C39, L6 | ✅ |
| 10–40 | — | not yet uploaded | — | ⬜ |

## Git

Work on the branch given at session start. Commit with descriptive messages; push when a
piece of analysis is complete.
