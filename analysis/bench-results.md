# Bench results

A running log of problems actually **worked at the bench** — the raw numbers, what came out
of them, and what to do differently next time. The [parts audit](problems-01-39-parts-audit.md)
says what a problem needs and the [workarounds doc](substitutions-and-workarounds.md) says how
to avoid buying it; this file says what happened when the thing was actually built.

> ⚠️ **This file contains worked answers by construction.** The repo's no-spoilers convention
> can't apply to a results log, so it's handled with a blanket warning instead: **don't read
> ahead of where you are.** Each problem's entry is self-contained, so skipping to the one
> you've just finished is safe.

New problems append a section here. Raw measurements go in verbatim — a transcription of what
the meter said is worth more later than a rounded conclusion.

---

## Problem 2 — Sources (p. 40–41)

**Worked 2026-09-10.** Parts A and B.

### Setup

| | |
|---|---|
| Source | 2 × AAA alkaline in series, from the depleted-battery bag |
| Load | 4 × 1.76 kΩ nominal, added one at a time in parallel |
| Instrument | DMM across the load |
| Current | **Computed** as `I = V / R_load`, not measured in series |

Two setup choices worth recording, because both turned out to matter:

**Depleted cells were the right call, not a compromise.** The measured source resistance came
out at **~42 Ω**. A fresh alkaline AAA is on the order of an ohm or less (*published typicals,
not measured here*), so a fresh pair would be somewhere near 1–2 Ω. At that level you'd need
~10 Ω loads and amps of current to produce the same fractional droop, and lead, holder and
breadboard contact resistance would be a large fraction of the answer. A dead cell puts the
source resistance up where a DMM and kΩ resistors can see it cleanly.

**Computing `I` from `V/R` beats measuring it in series.** A DMM on a mA range inserts a
current shunt whose burden voltage runs a few mV per mA — directly comparable to the 90–272 mV
of droop the whole experiment is trying to resolve. The cost of computing instead is that the
answer is only as good as `R_load`, which makes measuring the four resistors (rather than
trusting 1.76 k nominal) the thing that matters. **Not done this run — see open questions.**

### Raw data

Open-circuit: **Voc = 2.846 V**

| Resistors | R_load (Ω) | V (V) | I = V/R (mA) | R_bat = (Voc−V)/I (Ω) |
|---|---|---|---|---|
| 1 | 1760 | 2.756 | 1.5659 | 57.5 |
| 2 | 880 | 2.671 | 3.0352 | 57.7 |
| 3 | 586.7 | 2.618 | 4.4625 | 51.1 |
| 4 | 440 | 2.574 | 5.8500 | 46.5 |

`R_load` values are nominal-derived, not measured.

### Part A — the fit

Regressing both ways, since the two forms bracket the answer:

| Form | Result | R_int | EMF | I_sc |
|---|---|---|---|---|
| V on I (physical: `V = E − I·R`) | `V = 2.8114 − 42.02·I` | 42.0 Ω | 2.811 V | 66.9 mA |
| I on V | `I = −0.023306·V + 0.065599` | 42.9 Ω | 2.815 V | 65.6 mA |

`r² = 0.979`. The two forms agreeing to ~2% is the sign the fit is sound; they'd be identical
for perfectly collinear data.

**The fitted EMF is 2.811 V — 35 mV *below* the measured Voc of 2.846 V.** That gap is the
most informative number in the run, and the next section is about it.

### The trap: the R_bat column is not four independent estimates

The right-hand column above *looks* like evidence that internal resistance falls with current
(57.5 → 46.5 Ω). It isn't. All four rows share **one** measurement of Voc, so an error in that
single reading propagates into all four — and it propagates *unequally*:

```
R_bat = (Voc − V) / I        with I = V/R_load, which contains no Voc

∂R_bat/∂Voc = 1/I     →     0.64 Ω/mV at 1.57 mA
                            0.17 Ω/mV at 5.85 mA
```

A shared error in Voc therefore distorts the low-current end of the table roughly **four times
harder** than the high-current end — which is precisely the shape of a monotone downward trend.
Substituting the fitted EMF makes it vanish:

| Assumed EMF | R_bat across the four load points (Ω) |
|---|---|
| 2.846 (measured Voc) | 57.5, 57.7, 51.1, 46.5 — monotone falling |
| 2.811 (fitted) | 35.4, 46.3, 43.3, 40.6 — **no trend, just scatter** |

A conclusion that flips on a 35 mV shift in one reading is not a conclusion.

**This is the reason the book asks for a plot rather than four divisions:** the slope of the
fit never uses Voc at all. It extracts both the EMF and the resistance from the loaded points
alone, and it treats the disagreement with the open-circuit reading as an output rather than
swallowing it as an input.

<details>
<summary>Full sensitivity analysis — including why DMM accuracy is <em>not</em> the culprit</summary>

Substituting `I = V/R_load` gives a form with only measured quantities:

```
R_bat = (Voc − V) · R_load / V
```

Partials:

```
∂R_bat/∂Voc    = R_load / V  = 1/I
∂R_bat/∂V      = −R_load · Voc / V²
∂R_bat/∂R_load = (Voc − V) / V
```

Note that this expression is **homogeneous of degree zero in the voltages** — scale Voc and V
by the same factor and R_bat is unchanged:

```
Voc·(∂R_bat/∂Voc) + V·(∂R_bat/∂V) = R_load·Voc/V − R_load·Voc/V = 0
```

So a **DMM gain (accuracy) error cancels exactly.** Verified numerically: injecting +1% and
−2% gain errors into all readings shifts every R_bat by 0.000 Ω. A 5 mV offset error moves
them by under 0.1 Ω.

That matters for the diagnosis. The `1/I` sensitivity is *not* sensitivity to instrument
error, which is benign here. It's sensitivity to **Voc being a physically different quantity
at the moment it was read than the EMF acting during the loaded readings** — surface charge
and relaxation, not meter accuracy. Which makes the re-measure-Voc-after-unloading check the
decisive one.

</details>

### Part B — why the equivalent circuit fails outside the range

Three separate things, worth keeping apart:

**1. The primary point is domain of validity, not nonlinearity.** A measured Thevenin
equivalent is a curve fit over the range you probed, not a discovery of components hiding
inside the battery. This run sampled 1.57–5.85 mA — **2.3% to 8.7% of the extrapolated
I_sc**. Predicting behaviour at 66 mA is an 11× extrapolation past the farthest data point.
The model isn't wrong out there; it's unwarranted. This holds even for a perfectly linear
device.

**2. A battery's source resistance genuinely isn't constant.** It depends on current
(charge-transfer and concentration overpotential), state of charge, temperature, and *how long
the load has been connected*. That last dependence is why the book insists on a two-minute
settle after each change. At 66 mA these cells would collapse and keep collapsing.

**3. This run does not demonstrate (2).** With `r² = 0.979` and residuals of ±13 mV, the cell
behaved as a **very good linear source** over the range tested. Fitting the drop as activation
overpotential instead would need a Tafel slope near 320 mV/decade, which isn't physical. Over
1.57–5.85 mA, the honest reading is: this is ohmic.

### What the short-circuit intercept means

The regression says 65.6 mA flows at V = 0, which reads like a contradiction — zero volts
driving current. It isn't. **V = 0 means R_load = 0**, and Ohm's law says a 0 Ω load needs
zero volts to carry *any* current. The current is driven by the EMF; the terminal voltage is
what's left over after the internal drop, and at short circuit nothing is left over.

The two intercepts are the **Thevenin voltage and the Norton current** of Problem 1, measured
rather than derived, with slope −1/R_th. Both endpoints deliver zero power to the load:

| | V | I | P into load |
|---|---|---|---|
| Open circuit | 2.81 V | 0 | 0 |
| 1760 Ω | 2.756 V | 1.57 mA | 4.3 mW |
| 440 Ω (heaviest tested) | 2.574 V | 5.85 mA | 15.1 mW |
| Max power (R_load = R_int = 42 Ω) | 1.41 V | 33.5 mA | 47 mW |
| Short circuit | 0 | 66.9 mA | 0 — all 188 mW dissipated internally |

All four measured points sit far up the voltage-source end of the curve.

### Open questions and what to do differently

- **Was the two-minute settle observed?** Not recorded. It matters: reading before
  polarisation finishes loses more absolute droop at higher current, which under-reports
  R_bat more at the high-current end — the same falling trend seen above, from a second
  independent cause.
- **Measure the four resistors**, and the parallel combinations directly. Since `I = V/R`, an
  error in R goes into R_bat one-for-one, and it's the one input here with no redundancy.
- **Re-measure Voc immediately after removing the load, then again after two minutes.** If it
  climbs back toward 2.846 V, the relaxation explanation for the 35 mV gap is confirmed.
- **Run the load sequence in reverse** (440 Ω first). If the R_bat trend reverses direction,
  it's drift over the session, not current-dependence.
- **Record where the voltmeter probes landed.** At the resistor, lead and contact resistance
  counts as part of "the battery"; at the battery terminals it doesn't. Immaterial at 42 Ω,
  decisive if this is ever repeated with fresh cells.
- The `battery-logger/` idea in
  [the workarounds doc](substitutions-and-workarounds.md#an-embedded-engineer-upgrade) would
  settle the first and third of these directly, by capturing the settling transient instead of
  waiting it out.
