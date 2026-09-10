# Source page coverage — which book pages we actually have

The book itself is not committed here (copyrighted). This file is the index of **which pages
of *The Electronics of Radio* have been captured**, so a session can tell at a glance whether
the source for a given problem is on hand, partial, or missing.

Keep it current as pages arrive.

## How the material arrived

| Batch | Form | Pages | Notes |
|---|---|---|---|
| 1 | Phone screenshots | up to p. 127 | Problems 1–16. Problem 16 broke off mid-sentence — closed by batch 3 |
| 2 | Flatbed scans (Ricoh IM C401F), 2026-09-10 | pp. 138–313, selectively | Problems 17–39. 56 scans, one book page each |
| 3 | Direct photographs, 2026-09-10 | pp. 126–130, 149–153 | Closed the two gaps batch 2 left: the tail of Problem 16 and the whole of Problem 19 |

**Batch 3 is the best material in the repo.** Colour photographs of the open book, full page in
frame, no shear and no spine shadow — the inner margin and its part letters are completely
legible, which is exactly where the flatbed scans are weakest. A thumb appears at the edge of
some frames without covering text. If a page ever needs recapturing, this is the method to use.

### Batch 2 mechanics

- **200 dpi, 1-bit bilevel, one book page per scan** plus a cut-off sliver of the facing page.
  The sliver is always redundant (that page is scanned in its own right) *except* at a run
  boundary, where it is the only trace of a page we don't otherwise have.
- **Alternate scans are upside down** — the book was rotated on the platen between pages.
  This is metadata-fixable, not a rescan: setting `/Rotate 180` on the affected pages
  straightens them losslessly, with no re-encoding of the image data. Orientation was
  confirmed page-by-page with `tesseract --psm 0` and re-verified after correction.
- **Legibility is good.** Body text, circuit schematics and equations all read cleanly at
  200 dpi. Halftone figures are dithered but usable.
- **The gutter shadow is the one real defect.** The inner margin falls into the spine shadow —
  a median of ~80 px (≈0.4 in), worst case ~180 px (≈0.9 in). On the worst ~10 pages it reaches
  into the text column and swallows the **lettered part labels** (A., B., C. …). The letters are
  still legible to a human eye but OCR drops them; on those pages, read the part boundaries
  from context. Worst offenders: pp. 141, 153, 151, 308, 310.

## Coverage by problem

Page ranges are the printed book page numbers. A problem's range runs from its heading to the
start of the next one. Titles marked † are OCR-confirmed from the heading; ‡ is inferred.

| # | Chapter | Title | Pages | Source status |
|---|---|---|---|---|
| 17 | 7 Acoustics | Tuned speaker † | 138–140 | ✅ complete |
| 18 | 7 Acoustics | Acoustic standing-wave ratio † | 141 | ✅ complete |
| 19 | 8 Transistor switches | Receiver switch † | 149–151 | ✅ complete (batch 3) |
| 20 | 8 Transistor switches | Transmitter switch † | 151–153 | ✅ complete |
| 21 | 9 Transistor amplifiers | Driver amplifier † | 175–177 | ✅ complete |
| 22 | 9 Transistor amplifiers | Emitter degeneration † | 177–178 | ✅ complete |
| 23 | 9 Transistor amplifiers | Buffer amplifier † | 178–179 | ✅ complete |
| 24 | 10 Power amplifiers | Power amplifier † | 199–200 | ✅ complete |
| 25 | 10 Power amplifiers | Thermal modeling † | 200–203 | ✅ complete |
| 26 | 11 Oscillators | VFO † | 219–221 | ✅ complete |
| 27 | 11 Oscillators | Gain limiting † | 221–225 | ✅ complete |
| 28 | 12 Mixers | RF mixer † | 237–239 | ✅ complete |
| 29 | 12 Mixers | Product detector † | 239–242 | ✅ complete |
| 30 | 12 Mixers | Transmit mixer † | 242–244 | ✅ complete |
| 31 | 13 Audio circuits | Audio amplifier † | 250–254 | ✅ complete |
| 32 | 13 Audio circuits | Automatic gain control † | 254–256 | ✅ complete |
| 33 | 13 Audio circuits | Alignment † | 256–260 | ✅ complete |
| 34 | 14 Noise and intermodulation | Receiver response † | 274–276 | ✅ complete |
| 35 | 14 Noise and intermodulation | Intermodulation † | 276–277 | ✅ complete |
| 36 | 14 Noise and intermodulation | Demonstration † | 277 | ✅ complete |
| 37 | 15 Antennas and propagation | Antennas † | 305–306 | ✅ complete |
| 38 | 15 Antennas and propagation | Propagation † | 306–308 | ✅ complete |
| 39 | 15 Antennas and propagation | Listening † | 308–313 | ✅ complete |

**All of Problems 17–39 are complete, and 39 is the last problem in the book** — see below.
Every chapter's problems section was scanned as one unbroken run, so there are no gaps *inside*
the ranges above; the scans jump only between chapters, skipping chapter body text that the
problems don't strictly need.

Scanned runs, for reference: 138–141, 151–153, 175–179, 199–203, 219–225, 237–244, 250–260,
274–277, 305–313.

## Gaps — none outstanding

All three gaps this file previously tracked are closed.

**G1 — tail of Problem 16 — closed by batch 3 (pp. 128–130).** Parts B–G are all present, and
p. 130 carries only part G followed by white space, so Chapter 6 ends there. The audit in
[`../analysis/problems-01-39-parts-audit.md`](../analysis/problems-01-39-parts-audit.md) is no
longer provisional.

**G2 — Problem 19 — closed by batch 3 (pp. 149–150).** p. 149 carries the chapter's
FURTHER READING, the **PROBLEM 19 – RECEIVER SWITCH** heading and Figure 8.8; p. 150 carries the
description and parts A–D. The heading is on 149, so the inferred title was right and is now
verified. Parts E–H and the run to Problem 20 were already in batch 2 on p. 151.

**G3 — Problem 40 — does not exist. The book has 39 problems, not 40.** Three independent lines
of evidence agree:

1. The problem headings run contiguously 1→39 with nothing missing and nothing after.
2. Chapter 15 is the last chapter, and its problems section ends on p. 313 with Problem 39
   finishing three-quarters down the page.
3. Across all ~176 captured pages, **the highest problem number referenced in any cross-reference
   is 39** — no passage anywhere forward-references a Problem 40.

The owner, holding the book, independently reached the same conclusion. The "40 problems" figure
that used to appear in `CLAUDE.md` and `README.md` was an early assumption and has been corrected
throughout.

## Working copy

An upright, page-ordered PDF of batch 2 (pp. 138–313, with a bookmark per book page) was built
from the two uploads and handed back to the owner. It, the batch-3 photographs and the batch-1
screenshots are all deliberately **not committed** — same rule as the 40B manual. The PDF can be
rebuilt from the source scans if lost; the rotation map is recoverable automatically, since
`tesseract --psm 0` gets every page right on this material.
