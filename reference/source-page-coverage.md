# Source page coverage — which book pages we actually have

The book itself is not committed here (copyrighted). This file is the index of **which pages
of *The Electronics of Radio* have been captured**, so a session can tell at a glance whether
the source for a given problem is on hand, partial, or missing.

Keep it current as pages arrive.

## How the material arrived

| Batch | Form | Pages | Notes |
|---|---|---|---|
| 1 | Phone screenshots | up to p. 127 | Problems 1–16. Problem 16 breaks off mid-sentence — see gap G1 |
| 2 | Flatbed scans (Ricoh IM C401F), 2026-09-10 | pp. 138–313, selectively | Problems 17–39. 56 scans, one book page each |

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
| 19 | 8 Transistor switches | Receiver switch ‡ | ≤149–151 | ⚠️ **start missing** — gap G2 |
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
| 40 | ? | ? | 314+ | ❌ **missing entirely** — gap G3 |

Twenty-one of the twenty-four remaining problems are complete. Every chapter's problems section
was scanned as one unbroken run, so there are no gaps *inside* the ranges above — the scans jump
only between chapters, skipping chapter body text that the problems don't strictly need.

Scanned runs, for reference: 138–141, 151–153, 175–179, 199–203, 219–225, 237–244, 250–260,
274–277, 305–313.

## Gaps — what to capture next

**G1 — rest of Problem 16 (Chapter 6), p. 128 onward.**
Pre-existing, not addressed by batch 2. Batch 1 stops at p. 127 mid-sentence, and Figure 6.9
labels a "Jumper for part C", so parts B and C at least exist beyond what we have. The analysis
in [`../analysis/problems-01-16-parts-audit.md`](../analysis/problems-01-16-parts-audit.md)
is marked provisional until this lands.

**G2 — Problem 19, roughly pp. 148–150.**
Batch 2's chapter-8 run starts at p. 151, already inside part E. The heading and parts A–D are on
the preceding page(s), which survive only as the cut-off sliver on the p. 151 scan — about 40 % of
each line, sheared at the left, so not recoverable. From that sliver the problem is clearly the
**Receiver Switch**: the text covers blocking the transmitter signal from the receiver, the AGC
circuit, and a slope-triggered scope measurement referencing Figure 8.8. **Scan pp. 148–150** —
148 as insurance, since we can't see from here whether the problems section opens on 149 or 150.

**G3 — Problem 40, p. 314 onward.**
Chapter 15's run ends at p. 313, which finishes Problem 39 and appears to end the chapter (the
text stops about three-quarters down with white space below). No Problem 40 heading appears
anywhere in batch 2, and the last scan's sliver shows p. 312, not p. 314 — so nothing hints at
where it goes. **Scan from p. 314 to the end of the problem**, wherever it lands.

## Working copy

An upright, page-ordered PDF of batch 2 (pp. 138–313, with a bookmark per book page) was built
from the two uploads and handed back to the owner. It is deliberately **not committed** — same
rule as the 40B manual. Rebuild it from the source scans if it's lost; the rotation map is
recoverable automatically, since `tesseract --psm 0` gets every page right on this material.
