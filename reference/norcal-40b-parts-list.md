# NorCal 40B — parts list (transcribed)

Transcribed from Appendix A of the NM0S Electronics *NorCal 40B Assembly and Operating
Manual* (rev. 121623), manual pages 30–33. **Appendix A in the PDF is scanned images, not
text**, so this transcription exists to make the BOM searchable. Verify against your own
kit before cutting or soldering anything.

## Capacitors

| Value | Type | Marking | Qty | Refs |
|---|---|---|---|---|
| 0.01 µF | ceramic disk | `103` | 6 | C5, C7, C19, C22, C48, C55 |
| 0.047 µF | ceramic monolithic | `473` | 9 | C3, C8, C16, C25, C33, C36, C54, C56, C57 |
| 0.1 µF | ceramic disk | `104` | 5 | C20, C21, C28, C43, C58 |
| 1000 pF | NP0, 200 V, 5% | `102` | 2 | C46, C47 |
| 100 pF | NP0, 5% | `101` | 1 | C38 |
| 150 pF | NP0, 5% | `151` | 1 | C32 |
| 220 pF | NP0, 200 V, 5% | `221` | 1 | C24 |
| 270 pF | NP0, 5% | `271` | 7 | C9, C10, C11, C12, C13, C18, C35 |
| 390 pF | NP0, 200 V, 5% | `391` | 1 | C45 |
| 470 pF | NP0, 5% | `471` | 1 | C44 |
| 47 pF | NP0, 5% | `470` | 3 | C6, C14, C49 |
| 4.7 pF | NP0 (listed as "5p") | `479` | 3 | C4, C31, C37 |
| 390 pF | polystyrene, 5% | `390` | 1 | C51 |
| 1200 pF | polystyrene, 5% | `1200` | 2 | C52, C53 |
| 50 pF | trimmer | black | 5 | C1, C2, C17, C34, C39 |
| 50 pF | air trimmer | — | 1 | C50 |
| 2.2 µF | electrolytic | `2.2u` | 3 | C15, C23, C30 |
| 10 µF | electrolytic | `10u` | 3 | C26, C29, C40 |
| 100 µF | electrolytic | `100u` | 3 | C27, C41, C42 |

## Diodes

| Value | Type | Qty | Refs |
|---|---|---|---|
| 1N4148 | glass signal diode | 6 | D1, D2, D3, D4, D9, D11 |
| 1N5817 | plastic Schottky | 4 | D5, D6, D7, D10 |
| SB160 | plastic Schottky | 1 | D12 |
| MVAM108 | varactor | 1 | D8 |

## Connectors

| Value | Type | Qty | Refs |
|---|---|---|---|
| BNC | jack, PCB mount | 1 | J1 |
| Coaxial | power jack, 2.1 × 5.5 mm | 1 | J2 |
| Audio | jack, 3.5 mm stereo | 2 | J3, J4 |

## Inductors — molded

| Value | Colour code | Qty | Refs |
|---|---|---|---|
| 15 µH | brown-green-black | 1 | **L1** |
| 18 µH | brown-grey-black | 2 | L4, L5 |
| 1 mH | brown-black-red | 1 | **RFC2** |

## Inductors and transformers — toroidal

| Spec | Core | Core colour | Qty | Ref |
|---|---|---|---|---|
| 0.68 µH, 13 t #26, 21 cm | T37-2 | red | 1 | L2 |
| 3.5 µH, 30 t #28, 50 cm † | T37-2 | red | 1 | **L6** |
| 0.90 µH, 15 t #26, 24 cm | T37-2 | red | 1 | L7 |
| 0.58 µH, 12 t #26, 20 cm | T37-2 | red | 1 | L8 |
| 21 µH, 63 t #28, 133 cm | T68-7 | white | 1 | L9 |
| XFMR, pri 14 t #26 (23 cm), sec 4 t #26 (10 cm) | FT37-43 | black + orange dot | 1 | T1 |
| XFMR, pri 1 t #26 (5 cm) †, sec 20 t #26 (31 cm) | FT37-61 | black | 1 | T2 |
| XFMR, pri 23 t #28 (25 cm) †, sec 6 t #26 (13 cm) | FT37-61 | black | 1 | T3 |

† See [errata](#suspected-errata-in-the-manual).

## Resistors

| Value | Type | Colour code | Qty | Refs |
|---|---|---|---|---|
| 22 Ω | 1/4 W, 5% | red-red-black | 1 | R12 |
| 100 Ω | 1/4 W, 5% | brown-black-brown | 2 | R14, R25 |
| **510 Ω** | 1/4 W, 5% | green-brown-brown | **3** | R10, R11, R15 |
| 1.0 kΩ | 1/4 W, 5% | brown-black-red | 1 † | R18 |
| 1.8 kΩ | 1/4 W, 5% | brown-grey-red | 3 | R1, R22, R23 |
| 150 kΩ | 1/4 W, 5% | brown-green-yellow | 2 | R3, R24 |
| 4.7 kΩ | 1/4 W, 5% | yellow-violet-red | 1 | R20 |
| 47 kΩ | 1/4 W, 5% | yellow-violet-orange | 4 | R7, R9, R19, R21 |
| 8.2 MΩ | 1/4 W, 5% | grey-red-green | 1 | R4 |
| 2.2 MΩ | resistor network (8-pin SIP) | — | 1 | R5 |
| 500 Ω | trim pot | `501` | 2 | R8, R13 |
| 10 kΩ | trim pot | `103` | 1 | R6 † |
| 1 kΩ | panel control | — | 2 | R2 (RF gain), R16 (RIT) |
| 10 kΩ | 10-turn precision pot | — | 1 | R17 (tuning) |

## Semiconductors

| Value | Type | Qty | Refs |
|---|---|---|---|
| 2N3904 | NPN, TO-92 | 1 | Q1 |
| J309 | JFET, TO-92 | 4 | Q2, Q3, Q5, Q8 |
| 2N3906 | PNP, TO-92 | 1 | Q4 |
| **2N2222A** | **NPN, TO-18 metal can** | 1 | Q6 (driver) |
| 2SC5964 or 2SC2078 | NPN RF power, TO-220 | 1 | Q7 (PA) |
| SA612 or NE602 | mixer/oscillator IC | 3 | U1, U2, U4 |
| LM386 | AF amplifier IC | 1 | U3 |
| LM393 | dual comparator IC | 1 | U6 |
| LM78L08 | 8 V regulator | 1 | U5 |
| 4.915 MHz | HC-49 crystal | 6 | X1–X6 |
| — | ferrite bead | 1 | Z1 |

## Switches

| Value | Type | Qty | Refs |
|---|---|---|---|
| SPDT | slide switch | 2 | S1 (power), S2 (RIT) |

## Hardware and wire

| Description | Qty |
|---|---|
| 6-32 × 3/8" machine screw | 4 |
| 6-32 × 11/16" machine screw | 4 |
| 1" hex standoff | 4 |
| 1/4" round spacer | 4 |
| Heatsink | 1 |
| Knob, 0.6" | 2 |
| Knob, 0.75" | 1 |
| Nut, nylon, 6-32 | 1 |
| Screw, nylon, 0.5" 6-32 | 1 |
| Flat washer, nylon, 0.5" | 1 |
| Rubber feet | 4 |
| **Wire, #26 enamel** | **6 ft (183 cm)** |
| **Wire, #28 enamel** | **9 ft (274 cm)** |

Also in the kit but not in the Appendix A tables: 3 PCBs (main board + two break-away
enclosure boards), and a 15 MΩ resistor mentioned in the *Modifications* section as an
optional replacement for R4.

## Suspected errata in the manual

These came out of cross-checking Appendix A against the schematic (Appendix D) and the
assembly text. Check your own kit contents; I have not confirmed any of these with NM0S.

1. **R6 vs R17 trim pot.** Appendix A lists the 10 kΩ trim pot (`103`) against ref **R17**.
   But R17 is the 10-turn tuning pot (also listed, on the next page), and the assembly text
   says *"Install trimmer potentiometers R8, R13, and R6."* The schematic shows R6 as the
   10 kΩ AGC-threshold trimmer. The 10 kΩ trim pot is almost certainly **R6**.
2. **1.0 kΩ count.** Appendix A lists 1 × 1.0 kΩ for R18, but the schematic (sheet 1) also
   shows **R26 = 1.0 kΩ** in the RF-gain attenuator. Expect **two** 1.0 kΩ resistors.
3. **T3 primary wire length.** Appendix A says 23 t #28 in **25 cm**; the schematic says
   **35 cm**. 23 turns on an FT37-61 plus leads will not fit in 25 cm. Cut long.
4. **T2 primary wire length.** Appendix A says 1 t #26 in 5 cm; the schematic says 8 cm.
5. **L6 wire length.** Appendix A says 50 cm; the schematic says 43 cm. Either works for
   30 turns; the longer figure is safer.

## Wire budget

Toroid winding consumes almost all the enamel wire supplied:

- **#26**: L2 (21) + L7 (24) + L8 (20) + T1 (23 + 10) + T2 (31 + 8) + T3 sec (13) ≈ **150 cm** of 183 cm.
- **#28**: L6 (50) + L9 (133) + T3 pri (35) ≈ **218 cm** of 274 cm.

There is no spare for a practice wind or a botched toroid. Buy a small spool of each gauge.
