# Library Organization

This document explains how this KiCad library is organized and the rationale behind the structure.

## Organization Philosophy

This library follows a **category-based** organization approach, aligned with the official KiCad Library Convention (KLC). Components are grouped by their **function** rather than by manufacturer.

### Why Category-Based?

1. **Easier Component Discovery** - Find similar components together (e.g., all microcontrollers in one place)
2. **Better for Substitutions** - Quickly compare alternative parts within the same category
3. **Follows KLC Standards** - Aligned with official KiCad library conventions
4. **Scales Better** - As your library grows, functional grouping remains logical
5. **Supports Generic Parts** - Works well for components from multiple manufacturers

### When We Use Manufacturer-Specific Organization

While we primarily use category-based organization, manufacturer-specific grouping is used when:
- Components are complex and non-substitutable (e.g., specific microcontroller families)
- The manufacturer has a unique ecosystem (e.g., Espressif ESP32 variants)
- Components within a symbol file share a manufacturer part number prefix

## Directory Structure

```
kicad/
├── libraries/           # Main library content
│   ├── symbols/        # Symbol libraries (.kicad_sym files)
│   ├── footprints/     # Footprint libraries (.pretty directories)
│   ├── 3dmodels/       # 3D model libraries (.3dshapes directories)
│   └── datasheets/     # Component datasheets (organized by category)
│
├── submodules/         # External libraries (git submodules)
│   └── AudioJacks/     # Third-party audio jack library
│
├── templates/          # Project templates
│   ├── schematic_templates/
│   └── pcb_templates/
│
├── projects/           # Reference projects using this library
│   ├── co2-sensor/
│   ├── debughub/
│   └── eurorack-templates/
│
└── docs/              # Documentation
    ├── SETUP.md
    ├── ORGANIZATION.md (this file)
    ├── CONTRIBUTING.md
    ├── NAMING_CONVENTIONS.md
    └── ...
```

## Categories

### Microcontroller

**What belongs here:**
- Microcontroller modules (ESP32 variants, RP2040, etc.)
- Microcontroller ICs in various packages
- System-on-Module (SoM) boards
- Development boards with built-in MCUs

**Examples:**
- Espressif ESP32-WROOM, ESP32-PICO, ESP32-C3
- Raspberry Pi Pico 2 W (RP2040)
- STM32 modules (when added)

**File Structure:**
```
libraries/
├── symbols/Microcontroller.kicad_sym
├── footprints/Microcontroller.pretty/
│   ├── ESP32-WROOM-32.kicad_mod
│   ├── ESP32-PICO-D4.kicad_mod
│   └── Raspberrypi_pico2_w_SMD.kicad_mod
└── 3dmodels/Microcontroller.3dshapes/
    ├── ESP32-WROOM-32.step
    └── Raspberrypi_pico2_W.step
```

### RF_Wireless

**What belongs here:**
- Wireless communication modules
- RF transceivers
- Bluetooth modules
- LoRa modules
- Cellular modules
- GPS modules

**Examples:**
- Nordic nRF5340 (Bluetooth/RF SoC)
- RF transceivers
- WiFi modules (when not integrated into MCU)

**File Structure:**
```
libraries/
├── symbols/RF_Wireless.kicad_sym
├── footprints/RF_Wireless.pretty/
│   └── XCVR_NRF5340-QKAA-R7.kicad_mod
└── 3dmodels/RF_Wireless.3dshapes/
    └── NRF5340-QKAA-R7.step
```

### Connectors

**What belongs here:**
- Headers and pin connectors
- Board-to-board connectors
- Audio jacks (via AudioJacks submodule)
- Power connectors
- USB connectors
- Specialized connectors (relay sockets, etc.)

**Examples:**
- Audio jacks (3.5mm, 6.35mm)
- Pin headers
- USB connectors
- Power jacks
- RE130F relay connector

**File Structure:**
```
libraries/
├── symbols/Connectors.kicad_sym
├── footprints/Connectors.pretty/
│   └── RE130F41175F12P.kicad_mod
└── 3dmodels/Connectors.3dshapes/
    └── RE130F-41-175F-12P.stp

submodules/
└── AudioJacks/
    ├── AudioJacks.pretty/
    └── AudioJacks.3dshapes/
```

### Analog

**What belongs here:**
- Analog-to-Digital Converters (ADCs)
- Digital-to-Analog Converters (DACs)
- Operational amplifiers
- Analog switches and multiplexers
- Voltage references
- Analog filters
- Signal conditioning ICs

**Examples:**
- TI DAC80508 8-channel DAC
- ADCs
- Op-amps
- Voltage references

**File Structure:**
```
libraries/
├── symbols/Analog.kicad_sym
├── footprints/Analog.pretty/
│   └── QFN50P300X300X80-17N.kicad_mod
└── 3dmodels/Analog.3dshapes/
    └── DAC80508ZRTER.step
```

## Cross-Referencing Components

Each component typically consists of three related files:

1. **Symbol** (.kicad_sym) - Schematic representation
2. **Footprint** (.kicad_mod) - PCB layout pattern
3. **3D Model** (.step, .wrl) - 3D visualization

These are linked together by:
- Symbol → Footprint: Via footprint field in symbol properties
- Footprint → 3D Model: Via 3D model path in footprint properties

### Example: ESP32-WROOM-32

- **Symbol:** `libraries/symbols/Microcontroller.kicad_sym` → Symbol name: "ESP32-WROOM-32"
- **Footprint:** `libraries/footprints/Microcontroller.pretty/ESP32-WROOM-32.kicad_mod`
- **3D Model:** `libraries/3dmodels/Microcontroller.3dshapes/ESP32-WROOM-32.step`

The footprint references the 3D model using:
```
(model ${KICAD_PERSONAL_3DMODEL_DIR}/Microcontroller.3dshapes/ESP32-WROOM-32.step
  (offset (xyz 0 0 0))
  (scale (xyz 1 1 1))
  (rotate (xyz 0 0 0))
)
```

## Datasheets Organization

Datasheets are organized by category to match the component organization:

```
libraries/datasheets/
├── Microcontroller/
│   ├── ESP32/
│   └── RP2040/
├── RF_Wireless/
│   └── NRF5340/
├── Connectors/
│   └── AudioJacks/
└── Analog/
    └── DAC80508/
        └── dac80508.pdf
```

Each datasheet directory should contain:
- PDF datasheets
- Application notes (when relevant)
- INDEX.md file listing all datasheets with links

For components with online datasheets, the INDEX.md file provides links to manufacturer documentation.

## Submodules

External libraries are managed as git submodules in the `submodules/` directory:

### AudioJacks
- **Source:** https://github.com/clacktronics/AudioJacks
- **Purpose:** Comprehensive audio jack connector library
- **Usage:** Reference in footprint library table as `${KIPRJMOD}/../submodules/AudioJacks/AudioJacks.pretty`

To initialize submodules:
```bash
git submodule update --init --recursive
```

## Projects Directory

The `projects/` directory contains reference designs and examples that use this library:

- **co2-sensor** - CO2 sensor project with ESP32
- **debughub** - Debug interface board
- **eurorack-templates** - Eurorack synthesizer module templates

Projects serve as:
1. Test cases for library components
2. Reference designs
3. Examples of library usage
4. Validation that library changes don't break existing designs

## Templates Directory

Project templates provide starting points for common designs:

### Schematic Templates
- **ESP32_BasicBoard.kicad_sch** - Basic ESP32 board with power, USB, programming
- **RP2040_MinimalBoard.kicad_sch** - Minimal RP2040 design

### PCB Templates
- **Standard_2Layer.kicad_pcb** - 2-layer board defaults (trace widths, clearances, etc.)
- **Standard_4Layer.kicad_pcb** - 4-layer board defaults

## Finding Components

### By Function
1. Identify the component's primary function (MCU, analog, connector, etc.)
2. Look in the corresponding category library
3. Use KiCad's search/filter in the symbol or footprint picker

### By Manufacturer
Use KiCad's search feature with the manufacturer prefix:
- ESP32* for Espressif parts
- NRF* for Nordic parts
- DAC* for DAC ICs

### By Part Number
Search directly by manufacturer part number in KiCad's component picker.

## Adding New Categories

When the library grows, new categories can be added following the same structure:

1. Create category directories:
   ```
   libraries/symbols/NewCategory.kicad_sym
   libraries/footprints/NewCategory.pretty/
   libraries/3dmodels/NewCategory.3dshapes/
   libraries/datasheets/NewCategory/
   ```

2. Add to KiCad library tables (sym-lib-table, fp-lib-table)

3. Update documentation

4. Create README.md in the category directory

### Potential Future Categories
- Power (voltage regulators, power management ICs)
- Sensors (temperature, humidity, pressure, etc.)
- Display (LCD, OLED, LED drivers)
- Interface (USB, CAN, I2C, SPI chips)
- Memory (EEPROM, Flash, SRAM)

## Best Practices

1. **Keep related files together** - Symbol, footprint, and 3D model for the same component should have matching names
2. **Use consistent naming** - Follow naming conventions in NAMING_CONVENTIONS.md
3. **Document changes** - Update category README files when adding components
4. **Test with projects** - Verify new components work in actual designs
5. **Link datasheets** - Always provide datasheet references in INDEX.md

## Questions?

- See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add components
- See [NAMING_CONVENTIONS.md](NAMING_CONVENTIONS.md) for naming guidelines
- See [SETUP.md](SETUP.md) for KiCad configuration
