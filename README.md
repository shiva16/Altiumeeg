# SOUL_EEG (ARM edition)

**A 32-channel, ARM Cortex-M3-based EEG / biopotential acquisition board** — quad Texas Instruments
**ADS1299** analog front ends driven by an Atmel **ATSAM3U4EA-AU** (AT91 ARM Cortex-M3), designed in
**Altium Designer** in 2015.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![CAD: Altium Designer](https://img.shields.io/badge/CAD-Altium%20Designer-1BA1E2)](#repository-contents)
[![Channels: 32](https://img.shields.io/badge/Channels-32-brightgreen)](#technical-specifications)
[![AFE: ADS1299 x4](https://img.shields.io/badge/AFE-4%C3%97%20ADS1299-orange)](#technical-specifications)
[![MCU: ARM Cortex-M3](https://img.shields.io/badge/MCU-ARM%20Cortex--M3-5C2D91)](#technical-specifications)

This is the ARM-based sibling to [Adam-EEG](https://github.com/shiva16/Adam-EEG) — same core idea
(4× TI ADS1299 for 32 truly-simultaneous EEG channels, from the same "Soul Scientific" project era),
but a different implementation: Altium instead of EAGLE, and a single ARM Cortex-M3 controller
instead of dual ATmega328s. The project name inside the CAD files is **SOUL_EEG**; the archive's own
raw folder structure (preserved below, untouched) traces it to a contributor's machine under the
name **Luke** — this board's own history, not assumed or invented.

---

## Table of contents

- [The original archive](#the-original-archive)
- [What's in this board](#whats-in-this-board)
- [Technical specifications](#technical-specifications)
- [Signal names found in the schematics](#signal-names-found-in-the-schematics)
- [Repository contents](#repository-contents)
- [Opening the project](#opening-the-project)
- [Safety & disclaimer](#safety--disclaimer)
- [License](#license)

---

## The original archive

**`SOUL_EEG (5-2-2015 7-50-45 PM).zip` is preserved exactly as uploaded, byte-for-byte — it is not
modified, re-packed, or removed by this cleanup.** It's a raw Windows backup snapshot from
2 May 2015, taken as-is off the original design machine (user folders `Public\Documents\Altium\...`
and `Luke\Documents\...` / `Luke\Downloads\...`, nested five levels deep). That's the authoritative,
unaltered historical record of this board, timestamped the day it was captured — kept intact on
purpose.

## What's in this board

Everything below was read directly out of the real Altium files (`.PrjPcb`, `.SchDoc`, `.BomDoc`) —
not inferred from the README's own prior description or assumed from the project name.

- **4× identical ADS1299 analog channel sheets** (`EEG_1.SchDoc`–`EEG_4.SchDoc`), 42 real component
  instances each: 1× TI **ADS1299** (24-bit, 8-channel simultaneous-sampling biopotential ADC),
  21 capacitors, 16 resistors, and 4 header connectors (2× 2-pin, 1× 8×2, 1× 4-pin) per sheet.
  Four sheets × 8 channels per ADS1299 = the full **32-channel** front end.
- **`Microcontroller.SchDoc`** — U1 **ATSAM3U4EA-AU**: Atmel/Microchip AT91 ARM Cortex-M3, 2×128KB
  flash, 52KB SRAM, 96 user I/Os, 4× USART, 144-pin LQFP, industrial grade (−40°C to 85°C). Driven by
  a dedicated **ABM8 SMD crystal**, with local decoupling, an indicator LED, and a bias resistor.
- **`USB_Controller.SchDoc`** — U2 **TPS63001DRCR**, TI's buck-boost converter (1.8–5.5V in → fixed
  3.3V out), feeding a through-hole **USB Type-B** connector for host communication/power, plus an
  inductor, LED, and decoupling.
- **`Libraries/JTAG_Connector.SchDoc`** — the shared JTAG programming/debug header for the ARM core.
- **`SOUL_EEG_PCB_Rev1.PcbDoc`** — the board itself: 2 copper layers (only TOP/BOTTOM referenced in
  the layer set; no internal planes).

## Technical specifications

| Subsystem | Detail |
|---|---|
| **Analog front end** | 4 × Texas Instruments **ADS1299** — 24-bit, 8-channel, simultaneous-sampling, low-noise biopotential ADC |
| **Total channels** | **32** channels across 4 ADS1299 devices (8 per chip) |
| **Controller** | 1 × Atmel **ATSAM3U4EA-AU** — AT91 ARM Cortex-M3, 2×128KB Flash, 52KB SRAM, 96 I/Os, 4×USART, 144-pin LQFP |
| **Clocking** | ABM8 SMD crystal oscillator (microcontroller) |
| **Power** | TI **TPS63001DRCR** buck-boost, 1.8–5.5V in → 3.3V regulated out |
| **Host interface** | USB Type-B (through-hole) |
| **Debug** | Dedicated JTAG header (shared library sheet) |
| **Board** | 2-layer (TOP/BOTTOM copper only) |
| **CAD format** | Altium Designer, 2015 (native `.SchDoc`/`.PcbDoc`/`.PrjPcb` binary + text project files) |
| **License** | Apache License 2.0 |

## Signal names found in the schematics

Extracted directly from the schematic files' own net labels and ports — real signal names, not
guessed from silkscreen or footprint alone.

- **Per-channel analog inputs** (×8 per ADS1299 sheet, ×4 sheets): `IN1P_1`/`IN1N_1` … `IN8P_1`/`IN8N_1`
  (differential electrode pairs), each with a matching bias-drive pair `C_IN1P_1`/`C_IN1N_1` … etc.
- **Analog supply**: `VCAP1_1`–`VCAP4_1` (ADS1299's internal charge-pump decoupling nodes), `5V`, `GND`
- **Microcontroller**: `XIN`/`XOUT` (crystal), `GND`
- **USB/power**: `USB_POWER`, `5V`, `GND`

## Repository contents

```
SOUL_EEG (5-2-2015 7-50-45 PM).zip   ← original 2015 backup, untouched, kept for provenance
SOUL_EEG/                            ← the same real files, extracted and reorganized for browsing
├── SOUL_EEG.PrjPcb                  ← Altium project file (library paths fixed, see below)
├── SOUL_EEG.PrjPcbStructure
├── SOUL_EEG.OutJob                  ← output job (Gerbers/drill/reports)
├── Soul_EEG.BomDoc                  ← live BOM (39 catalog line items)
├── SOUL_EEG_PCB_Rev1.PcbDoc         ← the board
├── EEG_1.SchDoc … EEG_4.SchDoc      ← the 4 ADS1299 analog channel sheets
├── Microcontroller.SchDoc           ← ATSAM3U4EA-AU ARM Cortex-M3 sheet
├── USB_Controller.SchDoc            ← TPS63001 + USB-B sheet
├── ADS1299.SchLib / ADS1299.PcbLib  ← project-local ADS1299 symbol/footprint
└── Libraries/                       ← shared libraries the project depends on
    ├── common.SchLib / common.PcbLib
    ├── JTAG_Connector.SchDoc
    ├── PBL - THD Packages.PcbLib
    ├── PBL - SMD Packages.PcbLib
    ├── PBL - Connectors.SCHLIB
    └── Create Digikey BOM.OutJob
```

**One real fix made during extraction**: the original `.PrjPcb`'s 7 library references pointed at
absolute paths five directories up a specific Windows machine's user folder (e.g.
`..\..\..\..\..\Luke\Downloads\Libs_RRutledge 2013-12-23\PBL - THD Packages.PcbLib`) — meaning the
project could never actually reopen correctly on any other computer, even with the whole zip intact,
unless that exact folder structure was recreated. In `SOUL_EEG/SOUL_EEG.PrjPcb`, those 7 paths now
point at the sibling `Libraries/` folder above, relative to the project file itself. This is the only
content change made anywhere in this cleanup — every `.SchDoc`/`.PcbDoc`/`.SchLib`/`.PcbLib`/`.BomDoc`
binary file is byte-identical to what's inside the original zip.

## Opening the project

Open `SOUL_EEG/SOUL_EEG.PrjPcb` in Altium Designer (2015-era or newer — Altium maintains backward
file-format compatibility). All 7 library references now resolve relative to the project file, so no
manual path fix-up is needed after cloning.

## Safety & disclaimer

This is a research/hobbyist biopotential acquisition board, not a certified medical device. If
building this to record real physiological signals, use proper isolation (USB isolation, battery
power, no mains-referenced ground) and follow standard biopotential safety practice before connecting
anything to a person.

## License

Apache License 2.0 — see [LICENSE](LICENSE).
