# Firmware

MCU code that stands in for test equipment while working through *The Electronics of Radio*.
Rationale and per-problem detail live in
[`../analysis/substitutions-and-workarounds.md`](../analysis/substitutions-and-workarounds.md#where-the-mcu-dev-kits-genuinely-help).

## Layout

One directory per **instrument**, not per problem — a square-wave source serves Problems 3, 5
and 6, and duplicating it per problem would guarantee three divergent copies. Each directory
names the problems it serves in its own README.

```
firmware/
  <instrument>/
    README.md      what it emulates, which problems use it, how to build and flash,
                   and its calibration constants
    ...            source, build files
```

Candidates identified so far, none written yet:

| Directory | Emulates | Problems |
|---|---|---|
| `siggen-square/` | Square-wave generator, 20 Hz – 100 kHz | 3, 5, 6 |
| `siggen-am/` | AM source, frequency-scaled carrier | 4 |
| `battery-logger/` | Datalogging voltmeter for the polarisation transient | 2 |
| `freq-counter/` | Frequency counter | 40B VFO alignment |

## Conventions

- **Buildable from the repo root with one documented command.** Put it at the top of the
  directory's README. A future session should not have to reconstruct the invocation.
- **Pin the toolchain.** Name the SDK/HAL and version. "Works on my machine six months ago"
  is the failure mode here.
- **No magic numbers for anything physical.** This firmware is test equipment, so it inherits
  the repo's measure-don't-assume rule: ADC reference voltage, divider ratios, timer clock,
  output series resistance — write the measured value down next to the code with a note on
  how it was measured. A wrong constant here silently corrupts a lab result.
- **State the electrical interface** in the README: output voltage swing, source impedance,
  and whether the signal is unipolar. The book's instruments are bipolar with a 50 Ω source
  and MCU pins are neither, which changes how the measurement is read.
- **Remote sessions can build but not flash** — no USB. Write accordingly, and keep the
  build step runnable without hardware attached.

## Hardware

Boards not yet recorded. When one is used, add it to the bench inventory in
[`../CLAUDE.md`](../CLAUDE.md#bench-inventory) and note the specific part here.
