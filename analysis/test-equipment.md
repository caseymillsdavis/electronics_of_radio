# Test equipment and shopping list for Problems 1–9

## Function generator — requirements derived from the problems

These are pulled straight out of the problem statements, not from a generic "good starter
generator" list. Numbers in the table are what Problems 1–9 actually ask for.

| # | Requirement | Where it comes from |
|---|---|---|
| 1 | **Sine and square** waveforms | Sq: P3, P5, P6. Sine: P4, P8, P9 |
| 2 | **20 Hz to ≥ 15 MHz** | P3A is 20 Hz; P8E sweeps 1–15 MHz |
| 3 | **50 Ω source impedance**, well controlled | P3B and P8A both do Thevenin arithmetic that assumes exactly 50 Ω |
| 4 | **20 Vpp open-circuit** (= 10 Vpp into 50 Ω) at 1–3 MHz | P8F and P9F both say "amplitude setting of 10 Vpp" |
| 5 | **Internal AM**, 1 MHz carrier, 1 kHz modulating tone, **depth adjustable to 70% and 100%** | P4 intro and P4D |
| 6 | **Sync / trigger output** on BNC | P3 ("use a sync cable from the function generator to trigger the scope"), P4 ("connect a cable from the sync output... and use external triggering") |
| 7 | Amplitude readout referenced to a **50 Ω load** | The book's convention throughout — see below |

Nice to have, not required by Problems 1–9: a second channel, frequency sweep (makes P8E's
1 MHz-interval sweep and P8C/P9C's bandwidth hunt much less tedious), and a built-in
frequency counter.

### Requirement 5 is the one that eliminates most candidates

Problem 4 needs a **1 MHz carrier, amplitude-modulated internally by a 1 kHz sine, at 70%
depth**, then re-set to 100% for part D. A lot of budget generators either have no modulation
at all or offer AM only at fixed depth. Filter on this first; everything else on the list is
common.

### Requirement 7 is a settings trap worth knowing about now

The book states its convention explicitly on p. 41:

> *"For a function generator with a 50 Ω source resistance, this amplitude, 1 V peak-to-peak,
> is the voltage that we would see if the load were 50 Ω. For an open-circuit load, the
> amplitude is twice this, or 2 Vpp."*

Every "amplitude setting" in the book is the into-50 Ω number. Modern generators let you tell
them what load to assume, and they display accordingly — so **set the output load to 50 Ω**
and the displayed value matches the book's numbers directly. If yours is in High-Z mode
you'll be off by exactly a factor of two everywhere, which is a genuinely easy way to lose
an evening on Problem 3.

### Candidates

| Model family | Notes |
|---|---|
| **Siglent SDG1032X / SDG1032X-Plus** (30 MHz, 2 ch) | Meets everything above. AM with settable source, depth, modulating frequency and waveform; 20 Vpp into high-Z (specified to 10 MHz, which covers the 10 Vpp uses at 1 MHz and 2.8 MHz); sync output on the rear Aux In/Out. The single-channel SDG1022X is the cheaper sibling. This is the safe default. |
| **Rigol DG822 / DG812 / DG1022Z** | Same class, same feature set. Check the specific model's AM depth range and sync output on its datasheet. |
| **Owon AG1022 / AG051** | Cheaper, generally adequate; verify AM depth control before ordering. |
| **FeelTech FY6900, JUNTEK / "DDS" boxes** | Have AM on paper, but output impedance and amplitude flatness at HF are the usual complaints. Given that Problems 3, 8 and 9 lean on a *known* 50 Ω source and calibrated amplitude at 7–15 MHz, I'd spend up rather than fight the instrument. |

Verify against the current datasheet before buying — model lineups shift, and I'm going off
published specs rather than something on my bench.

### Scope check

Nothing in Problems 1–9 stresses a scope except **Problem 8E**, which asks for an amplitude
response plot out to 15 MHz. A 20 MHz scope is already about 1 dB down at 15 MHz and will
visibly bend the top of that curve; 100 MHz or better and it's a non-issue.

Two things to look up on your scope before starting Problem 3, because parts E–J need them
as inputs, not as measurements:

- **Input capacitance `Co`** — usually printed next to the input jack (typically 13–20 pF).
- **The 10:1 probe's marked capacitance** — Problem 9 needs it too, since the probe's
  capacitance is part of the resonant tank.

---

## Shopping list

### Instruments

- [ ] Function generator meeting the table above
- [ ] 12 V, 0.8 A-hr sealed lead-acid battery (Yuasa NP0.8-12 or equivalent) + float charger
      — **required for Problem 2; a bench supply will not do**

### Accessories

- [ ] 2 × BNC tee (male-female-female) — P5, P8
- [ ] 1 × BNC 50 Ω feedthrough terminator — P5, P8B
- [ ] 2 × BNC-to-minigrabber / test-hook lead — P3 explicitly builds on component leads, no
      breadboard
- [ ] 2–3 × BNC-BNC coax patch cables
- [ ] BNC-to-banana or BNC-to-alligator adapter
- [ ] Non-metallic (ceramic/plastic) trimmer tuning tool set — P8, and the 40B's alignment

### Breadboard components

Quantities are "buy a few spares", not the minimum.

| Part | Qty | For |
|---|---|---|
| 510 Ω, **1/2 W** (not 1/4 W — see the audit) | 5 | P2 |
| 300 kΩ, 1% metal film | 2 | P3 |
| 3.0 kΩ, 1% metal film | 2 | P4 |
| 2.0 kΩ, 1% metal film | 4 | P5 transistor switch, P6 |
| 10 nF (0.01 µF) film, 5% | 5 | P3, P4 |
| 1N4148 | 10 | P4, P6 |
| 1 mH molded choke | 3 | P5, P6 |
| P2N2222A or PN2222A (TO-92) | 5 | P5, P6 — sacrificial, spikes kill these |

A generic 1% metal-film resistor assortment and a film capacitor assortment cover all of the
above except the chokes and transistors, and will keep covering later chapters.

### Kit-adjacent

- [ ] #26 and #28 enamelled magnet wire, small spools — the kit ships ~20% margin on wire
      and no allowance for a practice toroid wind
- [ ] Solder wick, fine 63/37 solder, 15–25 W pencil iron or temperature-controlled station
      at ~700 °F, small PCB vise — for Problems 8 and 9 onward
- [ ] 50 Ω, 5 W dummy load with a BNC connector — not needed until the radio is finished, but
      the 40B manual's alignment procedure requires it

---

## Sources

- [Siglent SDG1032X product page](https://siglentna.com/product/sdg1032x/)
- [Siglent SDG1032X datasheet (PDF)](https://siglent.co.uk/pdf/SIGLENT-SDG1032X-FUNCTION-GENERATOR-Datasheet.pdf)
- [Siglent SDG1032X user manual](https://www.manualslib.com/manual/2675359/Siglent-Sdg1032x.html)
- NM0S Electronics, *NorCal 40B Assembly and Operating Manual*, rev. 121623
