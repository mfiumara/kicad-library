# KiCad Personal Library

A well-organized, category-based KiCad library following official KLC (KiCad Library Convention) standards. This library contains symbols, footprints, and 3D models for microcontrollers, wireless modules, connectors, analog ICs, and more.

## Quick Start

### 1. Clone the Repository

```bash
git clone <your-repo-url> ~/kicad-library
cd ~/kicad-library
git submodule update --init --recursive
```

### 2. Configure KiCad

Open KiCad and navigate to **Preferences → Configure Paths**. Add these environment variables:

| Variable | Path |
|---|---|
| `KICAD_PERSONAL_SYMBOL_DIR` | `/path/to/kicad-library/libraries/symbols` |
| `KICAD_PERSONAL_FOOTPRINT_DIR` | `/path/to/kicad-library/libraries/footprints` |
| `KICAD_PERSONAL_3DMODEL_DIR` | `/path/to/kicad-library/libraries/3dmodels` |
| `KICAD_PERSONAL_DATASHEET_DIR` | `/path/to/kicad-library/libraries/datasheets` |

### 3. Add Libraries to KiCad

**Symbols:** Preferences → Manage Symbol Libraries → Add library → Select `.kicad_sym` files from `libraries/symbols/`

**Footprints:** Preferences → Manage Footprint Libraries → Add library → Select `.pretty` folders from `libraries/footprints/`

See [docs/SETUP.md](docs/SETUP.md) for detailed configuration instructions.

## Library Contents

### Components

- **Microcontrollers:** ESP32 family (30+ variants), RP2040/Raspberry Pi Pico
- **RF/Wireless:** Nordic nRF5340
- **Analog ICs:** DACs, ADCs, op-amps
- **Connectors:** Headers, audio jacks, USB, specialized connectors

### Statistics

- **Symbols:** 33+ components across 4 categories
- **Footprints:** 55+ footprints
- **3D Models:** 37+ models (STEP format)
- **Projects:** 3 reference designs
- **Templates:** Schematic and PCB templates

## Repository Structure

```
kicad/
├── libraries/              # Main library content
│   ├── symbols/           # Symbol libraries (.kicad_sym)
│   │   ├── Microcontroller.kicad_sym
│   │   ├── RF_Wireless.kicad_sym
│   │   ├── Connectors.kicad_sym
│   │   └── Analog.kicad_sym
│   ├── footprints/        # Footprint libraries (.pretty)
│   │   ├── Microcontroller.pretty/
│   │   ├── RF_Wireless.pretty/
│   │   ├── Connectors.pretty/
│   │   └── Analog.pretty/
│   ├── 3dmodels/          # 3D models (.3dshapes)
│   │   ├── Microcontroller.3dshapes/
│   │   ├── RF_Wireless.3dshapes/
│   │   ├── Connectors.3dshapes/
│   │   └── Analog.3dshapes/
│   └── datasheets/        # Component datasheets
│       ├── Microcontroller/
│       ├── RF_Wireless/
│       ├── Connectors/
│       ├── Analog/
│       └── INDEX.md
│
├── submodules/            # External libraries (git submodules)
│   └── AudioJacks/        # Audio jack connector library
│
├── templates/             # Project templates
│   ├── schematic_templates/
│   ├── pcb_templates/
│   └── README.md
│
├── projects/              # Reference designs
│   ├── co2-sensor/        # ESP32-based CO2 sensor
│   ├── debughub/          # Debug interface board
│   ├── eurorack-templates/  # Eurorack module templates
│   └── README.md
│
└── docs/                  # Documentation
    ├── SETUP.md           # KiCad configuration guide
    ├── ORGANIZATION.md    # Library organization explained
    ├── CONTRIBUTING.md    # How to add components
    ├── NAMING_CONVENTIONS.md  # Naming standards
    ├── WORKFLOW.md        # Development workflow
    └── KLC_COMPLIANCE.md  # KiCad Library Convention compliance
```

## Featured Components

### Microcontrollers

- **Espressif ESP32 Family**
  - ESP32-WROOM-32 (WiFi & Bluetooth Classic)
  - ESP32-C3-MINI-1 (RISC-V, WiFi & BLE)
  - ESP32-S3-WROOM-1 (WiFi & Bluetooth 5 LE)
  - 30+ module variants

- **Raspberry Pi**
  - RP2040 microcontroller
  - Raspberry Pi Pico 2 W (THT and SMD variants)

### RF & Wireless

- Nordic nRF5340 (Bluetooth 5.3, Thread, Zigbee)

### Analog

- TI DAC80508 (8-channel 16-bit DAC with SPI)

### Connectors

- Audio jacks (3.5mm, 6.35mm) via AudioJacks submodule
- Relay connectors
- Standard headers and interface connectors

## Organization Philosophy

This library uses **category-based organization** following the official KiCad Library Convention (KLC):

- Components grouped by **function** (not manufacturer)
- Easier to find similar components
- Better for component substitution
- Scales well as library grows
- Aligned with KiCad official libraries

See [docs/ORGANIZATION.md](docs/ORGANIZATION.md) for detailed rationale.

## Documentation

- **[SETUP.md](docs/SETUP.md)** - Complete KiCad configuration guide
- **[ORGANIZATION.md](docs/ORGANIZATION.md)** - Library organization explained
- **[CONTRIBUTING.md](docs/CONTRIBUTING.md)** - How to add new components
- **[NAMING_CONVENTIONS.md](docs/NAMING_CONVENTIONS.md)** - Naming standards and conventions
- **[WORKFLOW.md](docs/WORKFLOW.md)** - Git workflow and development process
- **[KLC_COMPLIANCE.md](docs/KLC_COMPLIANCE.md)** - KiCad Library Convention standards

**Category Documentation:**
- [Symbol Library Index](libraries/symbols/README.md)
- [Footprint Library Index](libraries/footprints/README.md)
- [3D Model Index](libraries/3dmodels/README.md)
- [Datasheet Index](libraries/datasheets/INDEX.md)
- [Submodules Guide](submodules/README.md)
- [Projects Overview](projects/README.md)
- [Templates Guide](templates/README.md)

## Contributing

Contributions are welcome! To add new components:

1. Read [CONTRIBUTING.md](docs/CONTRIBUTING.md) for guidelines
2. Follow [NAMING_CONVENTIONS.md](docs/NAMING_CONVENTIONS.md) for naming
3. Ensure [KLC_COMPLIANCE.md](docs/KLC_COMPLIANCE.md) standards are met
4. Test in a real project before submitting
5. Update relevant documentation

See [WORKFLOW.md](docs/WORKFLOW.md) for git workflow and development process.

## Standards and Compliance

This library follows:

- **KiCad Library Convention (KLC)** - Official KiCad standards
- **IPC-7351** - Footprint naming for generic packages
- **Category-based organization** - Components grouped by function
- **Environment variables** - Portable library paths
- **Git submodules** - For external library management

All components are validated for:
- Correct symbol pin properties
- Accurate footprint dimensions
- Proper 3D model alignment
- Complete documentation

## Projects

The `projects/` directory contains reference designs:

- **co2-sensor** - ESP32-based environmental monitoring
- **debughub** - Universal debug interface board
- **eurorack-templates** - Synthesizer module templates

These projects demonstrate library usage and serve as templates for new designs.

## Submodules

External libraries are managed as git submodules:

- **AudioJacks** - Comprehensive audio jack connector library from [clacktronics](https://github.com/clacktronics/AudioJacks)

To initialize submodules after cloning:

```bash
git submodule update --init --recursive
```

See [submodules/README.md](submodules/README.md) for management details.

## Quick Reference

### Finding Components

| Component Type | Symbol Library | Footprint Library |
|---|---|---|
| ESP32, RP2040 | Microcontroller | Microcontroller.pretty |
| nRF5340, wireless | RF_Wireless | RF_Wireless.pretty |
| DAC, ADC, op-amps | Analog | Analog.pretty |
| Headers, jacks | Connectors | Connectors.pretty |

### File Naming

- **Symbols:** `ManufacturerPrefix_PartNumber` (e.g., `ESP32-WROOM-32`)
- **Footprints:** `PartNumber.kicad_mod` or `PackageCode.kicad_mod`
- **3D Models:** `FootprintName.step` (matches footprint name)

See [NAMING_CONVENTIONS.md](docs/NAMING_CONVENTIONS.md) for complete guidelines.

## Version Control

This repository uses:

- **Main branch:** Stable, tested components
- **Feature branches:** For development and testing
- **Git submodules:** For external library management
- **.gitignore:** Excludes KiCad backups, OS files, build artifacts
- **.gitattributes:** Ensures correct line endings for KiCad files

## Requirements

- **KiCad 7.0 or later** (recommended: KiCad 8.0+)
- **Git** for version control and submodule management
- **~50MB disk space** for complete library with 3D models

## Getting Help

- **Setup issues:** See [SETUP.md](docs/SETUP.md)
- **Library organization questions:** See [ORGANIZATION.md](docs/ORGANIZATION.md)
- **Adding components:** See [CONTRIBUTING.md](docs/CONTRIBUTING.md)
- **Naming questions:** See [NAMING_CONVENTIONS.md](docs/NAMING_CONVENTIONS.md)
- **Git workflow:** See [WORKFLOW.md](docs/WORKFLOW.md)

## License

This library is for personal use. Individual components may have different licenses:
- Components created by me: Free to use
- Submodules (AudioJacks): Check respective repository licenses
- Manufacturer-provided 3D models: Subject to manufacturer terms

## Acknowledgments

- **KiCad** - Open-source EDA software
- **Espressif** - ESP32 resources and documentation
- **Raspberry Pi Foundation** - RP2040 resources
- **Nordic Semiconductor** - nRF5340 resources
- **clacktronics** - AudioJacks library
- **KiCad community** - Guidelines and best practices

---

**Last Updated:** December 2024
**KiCad Version:** 7.0+
**Library Version:** 2.0.0 (reorganized structure)
