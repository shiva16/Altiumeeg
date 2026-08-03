# Contributing to SOUL_EEG (Altium ARM edition)

Thanks for your interest in this board. This is a small open-hardware repository — contributions of
any size are welcome.

## Ways to contribute

- **Bug reports**: found an error in the schematic or board (wrong footprint, missing connection,
  wrong part value)? Open an issue with the sheet/designator/net name and what's wrong.
- **The unresolved SPI-bus question**: as documented in the README's
  [System architecture](README.md#system-architecture) section, this board's exact ADS1299-to-MCU
  digital bus topology (daisy-chain vs. individual per-chip bus, and the real signal names on each
  8×2 header) isn't recoverable from named net labels in the schematic files. If you open this in
  Altium and trace it, that finding — confirmed either way — is genuinely the most valuable
  contribution this repo could get right now.
- **Build reports**: fabricated and assembled a board? Open an issue or PR describing what worked,
  what didn't, and any BOM substitutions you made — real build data is the most valuable contribution
  to a hardware repo.
- **KiCad / EAGLE conversions**: this board is native Altium Designer (2015-era binary format). A
  faithful conversion to KiCad or another open format is very welcome — it would also make this board
  viewable without an Altium license.
- **Routing / layout improvements**: if you improve noise performance, layer stackup, or component
  placement, open a PR with before/after reasoning.
- **Documentation**: clarifications to the README, added datasheets/reference links, or BOM sourcing
  notes.

## Before opening a PR

1. Open an issue first for anything non-trivial, so the change can be discussed before you spend time
   on it.
2. Keep schematic/board edits in the native Altium format (`.SchDoc`/`.PcbDoc`) unless the PR *is* a
   format conversion, and make them against the files in `SOUL_EEG/`, not the original archived zip
   (see the README's [The original archive](README.md#the-original-archive) section for why the zip
   itself stays untouched).
3. Describe what you changed and why in the PR description — for hardware changes, include which
   sheets/nets/parts were touched.
4. If you've physically built and tested the change, say so — verified changes are prioritized.

## Code of Conduct

This project follows the [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you agree to abide
by it.
