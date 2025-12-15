# Footprint Libraries

This directory contains KiCad footprint libraries organized by component category.

## Library Directories

### Microcontroller.pretty/

Footprints for microcontrollers, SoM modules, and development boards.

**Components:**

#### Espressif ESP32 Modules (47 footprints)
- ESP32-WROOM series (multiple variants)
- ESP32-PICO series
- ESP32-MINI series
- ESP32-C3 modules
- ESP32-S2 modules
- ESP32-S3 modules
- ESP8685 modules
- Development boards (DevKitC variants)

#### Raspberry Pi
- **Raspberrypi_pico2_THT.kicad_mod** - Through-hole mounting
- **Raspberrypi_pico2_w_SMD.kicad_mod** - Surface mount variant

**Total:** 49 footprints

### RF_Wireless.pretty/

Footprints for wireless communication modules and RF components.

**Components:**

- **XCVR_NRF5340-QKAA-R7.kicad_mod** - Nordic nRF5340 wireless SoC package

**Total:** 1 footprint

### Connectors.pretty/

Footprints for connectors, headers, jacks, and interface components.

**Components:**

- **RE130F41175F12P.kicad_mod** - 12-pin relay connector

**Note:** Additional audio jack connectors available via AudioJacks submodule in `submodules/AudioJacks/AudioJacks.pretty/`

**Total:** 1 footprint (+ 8 in AudioJacks submodule)

### Analog.pretty/

Footprints for analog ICs including ADCs, DACs, op-amps, and related components.

**Components:**

- **QFN50P300X300X80-17N.kicad_mod** - QFN-17 package (0.5mm pitch, 3x3mm body) for DAC80508
- Additional QFN variants from personal library

**Total:** 4 footprints

## Using Footprint Libraries

### In KiCad

1. **Preferences → Manage Footprint Libraries**
2. Click **Global Libraries** tab
3. Click folder icon to add library
4. Browse to this directory and select desired `.pretty` folder
5. Assign a nickname (e.g., "Microcontroller", "RF_Wireless")

### Recommended Library Table Entries

Add to `fp-lib-table`:

```
(lib (name "Microcontroller") (type "KiCad") (uri "${KICAD_PERSONAL_FOOTPRINT_DIR}/Microcontroller.pretty") (options "") (descr "Microcontroller modules and packages"))
(lib (name "RF_Wireless") (type "KiCad") (uri "${KICAD_PERSONAL_FOOTPRINT_DIR}/RF_Wireless.pretty") (options "") (descr "Wireless module footprints"))
(lib (name "Connectors") (type "KiCad") (uri "${KICAD_PERSONAL_FOOTPRINT_DIR}/Connectors.pretty") (options "") (descr "Connector footprints"))
(lib (name "Analog") (type "KiCad") (uri "${KICAD_PERSONAL_FOOTPRINT_DIR}/Analog.pretty") (options "") (descr "Analog IC footprints"))
```

## Footprint Standards

All footprints follow KLC (KiCad Library Convention):

- **Layers:**
  - F.Cu / B.Cu - Copper (pads only)
  - F.SilkS / B.SilkS - Silkscreen (outline, pin 1 indicator)
  - F.Fab / B.Fab - Fabrication layer (exact dimensions)
  - F.CrtYd / B.CrtYd - Courtyard (0.25mm minimum clearance)

- **Requirements:**
  - Pin 1 clearly marked
  - Silkscreen doesn't overlap pads
  - Courtyard present and adequate
  - REF** on F.SilkS
  - Value on F.Fab

- **3D Models:**
  - Linked using environment variables
  - STEP format preferred
  - Correctly positioned and oriented

See [KLC_COMPLIANCE.md](../../docs/KLC_COMPLIANCE.md) for complete standards.

## Footprint Details

### ESP32-WROOM-32

- **Dimensions:** 18mm × 25.5mm × 3.1mm
- **Pads:** 38 castellated pads (1.27mm pitch)
- **Mounting:** SMD (castellated edges for hand soldering)
- **3D Model:** Available (STEP format)
- **Datasheet:** [ESP32-WROOM-32](https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf)

### Raspberrypi Pico 2 W

**THT Variant:**
- **Dimensions:** 21mm × 51mm
- **Pads:** 40 through-hole pins (2.54mm pitch)
- **Mounting:** Through-hole
- **3D Model:** Available (STEP format)

**SMD Variant:**
- **Dimensions:** 21mm × 51mm
- **Pads:** 40 castellated SMD pads
- **Mounting:** Surface mount
- **3D Model:** Same as THT

### NRF5340-QKAA-R7

- **Package:** QFN (custom Nordic package)
- **Pins:** Multiple pads for wireless SoC
- **Mounting:** SMD (reflow soldering)
- **3D Model:** Available (STEP format)
- **Datasheet:** [nRF5340](https://infocenter.nordicsemi.com/pdf/nRF5340_PS_v1.3.pdf)

### DAC80508 - QFN50P300X300X80-17N

- **Package:** QFN-17
- **Dimensions:** 3.0mm × 3.0mm × 0.8mm
- **Pitch:** 0.5mm
- **Thermal Pad:** Central exposed pad
- **Mounting:** SMD (reflow soldering, stencil required)
- **3D Model:** Available (STEP format)

## Adding New Footprints

1. Open KiCad Footprint Editor
2. Select appropriate category library
3. Create new footprint following KLC standards
4. Add all required layers (Cu, SilkS, Fab, CrtYd)
5. Link 3D model using environment variables
6. Test in 3D viewer
7. Test in a real project
8. Update this README with footprint info

See [CONTRIBUTING.md](../../docs/CONTRIBUTING.md) for detailed instructions.

## Footprint Naming Conventions

| Type | Format | Example |
|---|---|---|
| Manufacturer Modules | ManufacturerPrefix_PartNumber | ESP32-WROOM-32 |
| Generic Packages | PackageType-Variant | QFN50P300X300X80-17N |
| With Mounting Variant | Name_Variant | Raspberrypi_pico2_THT |

See [NAMING_CONVENTIONS.md](../../docs/NAMING_CONVENTIONS.md) for complete naming guidelines.

## Component Cross-Reference

| Footprint | Symbol | 3D Model | Typical Use |
|---|---|---|---|
| ESP32-WROOM-32.kicad_mod | Microcontroller:ESP32-WROOM-32 | Microcontroller.3dshapes/ESP32-WROOM-32.step | WiFi/BT IoT projects |
| Raspberrypi_pico2_w_SMD.kicad_mod | Microcontroller:Raspberrypi_Pico2_W | Microcontroller.3dshapes/Raspberrypi_pico2_W.step | RP2040 projects, SMD |
| XCVR_NRF5340-QKAA-R7.kicad_mod | RF_Wireless:NRF5340-QKAA-R7 | RF_Wireless.3dshapes/NRF5340-QKAA-R7.step | Bluetooth/Thread devices |
| QFN50P300X300X80-17N.kicad_mod | Analog:DAC80508ZRTER | Analog.3dshapes/DAC80508ZRTER.step | Multi-channel DAC |

## Verification Checklist

Before using a footprint in production:

- [ ] Dimensions verified against datasheet
- [ ] Pin 1 indicator present and clear
- [ ] Courtyard adequate (0.25mm minimum)
- [ ] Silkscreen doesn't overlap pads
- [ ] Fabrication layer complete
- [ ] 3D model loads and aligns correctly
- [ ] Tested in actual PCB layout
- [ ] Reviewed for manufacturability

## Library Statistics

- **Microcontroller.pretty** - 49 footprints
- **RF_Wireless.pretty** - 1 footprint
- **Connectors.pretty** - 1 footprint
- **Analog.pretty** - 4 footprints

**Total:** 55 footprints (+ 8 in AudioJacks submodule)

## Questions?

- See [ORGANIZATION.md](../../docs/ORGANIZATION.md) for library structure
- See [SETUP.md](../../docs/SETUP.md) for KiCad configuration
- See [KLC_COMPLIANCE.md](../../docs/KLC_COMPLIANCE.md) for footprint standards
