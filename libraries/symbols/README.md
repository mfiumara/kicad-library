# Symbol Libraries

This directory contains KiCad symbol libraries organized by component category.

## Library Files

### Microcontroller.kicad_sym

Microcontrollers, System-on-Module (SoM) boards, and development boards with integrated MCUs.

**Components:**

#### Espressif ESP32 Family
- **ESP32-WROOM-32** - WiFi & Bluetooth Classic module
- **ESP32-WROOM-32D** - Updated WROOM variant
- **ESP32-WROOM-32E** - Extended temperature range variant
- **ESP32-PICO-D4** - Compact SiP module
- **ESP32-MINI-1** - Smaller footprint module
- **ESP32-C3-MINI-1** - RISC-V based WiFi & BLE module
- **ESP32-S2-MINI-1** - WiFi-only module
- **ESP32-S3-WROOM-1** - WiFi & Bluetooth 5 (LE) module
- **ESP8685-WROOM-05** - Compact WiFi & BLE module
- Various development boards (DevKitC, etc.)

#### Raspberry Pi
- **RP2040** - Dual ARM Cortex-M0+ microcontroller
- **Raspberrypi_Pico2_W** - Wireless development board

### RF_Wireless.kicad_sym

Wireless communication modules, RF transceivers, and related components.

**Components:**

#### Nordic Semiconductor
- **NRF5340-QKAA-R7** - Dual Arm Cortex-M33 wireless SoC, Bluetooth 5.3, Thread, Zigbee

### Connectors.kicad_sym

Connectors, headers, jacks, and interface components.

**Components:**

- **RE130F-41-175F-12P** - Relay connector, 12-pin
- Additional connectors available via AudioJacks submodule

### Analog.kicad_sym

Analog ICs including ADCs, DACs, op-amps, and signal conditioning components.

**Components:**

#### Texas Instruments
- **DAC80508ZRTER** - 8-channel, 16-bit DAC with SPI interface, TSSOP-16 package

## Using Symbol Libraries

### In KiCad

1. **Preferences → Manage Symbol Libraries**
2. Click **Global Libraries** tab
3. Click folder icon to add library
4. Browse to this directory and select desired `.kicad_sym` file
5. Assign a nickname (e.g., "Microcontroller", "RF_Wireless")

### Recommended Library Table Entries

Add to `sym-lib-table`:

```
(lib (name "Microcontroller") (type "KiCad") (uri "${KICAD_PERSONAL_SYMBOL_DIR}/Microcontroller.kicad_sym") (options "") (descr "Microcontrollers and SoM modules"))
(lib (name "RF_Wireless") (type "KiCad") (uri "${KICAD_PERSONAL_SYMBOL_DIR}/RF_Wireless.kicad_sym") (options "") (descr "Wireless communication modules"))
(lib (name "Connectors") (type "KiCad") (uri "${KICAD_PERSONAL_SYMBOL_DIR}/Connectors.kicad_sym") (options "") (descr "Connectors and headers"))
(lib (name "Analog") (type "KiCad") (uri "${KICAD_PERSONAL_SYMBOL_DIR}/Analog.kicad_sym") (options "") (descr "Analog ICs - DACs, ADCs, Op-Amps"))
```

## Symbol Standards

All symbols in this library follow:

- **Grid:** 100 mil (2.54mm) pin grid
- **Pin naming:** Matches datasheet terminology
- **Pin types:** Correctly assigned (Input, Output, Bidirectional, Power, etc.)
- **Fields:** Complete with Reference, Value, Footprint, Datasheet
- **Organization:** Logical pin arrangement (by function, not physical layout)

See [NAMING_CONVENTIONS.md](../../docs/NAMING_CONVENTIONS.md) for naming standards.

## Adding New Symbols

1. Open KiCad Symbol Editor
2. Select appropriate category library
3. Create new symbol following KLC standards
4. Add all required fields (Reference, Value, Footprint, Datasheet)
5. Link to corresponding footprint
6. Test in a project
7. Update this README with component info

See [CONTRIBUTING.md](../../docs/CONTRIBUTING.md) for detailed instructions.

## Component Cross-Reference

| Symbol | Footprint | 3D Model | Datasheet |
|---|---|---|---|
| ESP32-WROOM-32 | Microcontroller.pretty/ESP32-WROOM-32.kicad_mod | Microcontroller.3dshapes/ESP32-WROOM-32.step | [Link](https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf) |
| RP2040 / Raspberrypi_Pico2_W | Microcontroller.pretty/Raspberrypi_pico2_w_SMD.kicad_mod | Microcontroller.3dshapes/Raspberrypi_pico2_W.step | [Link](https://datasheets.raspberrypi.com/rp2040/rp2040-datasheet.pdf) |
| NRF5340-QKAA-R7 | RF_Wireless.pretty/XCVR_NRF5340-QKAA-R7.kicad_mod | RF_Wireless.3dshapes/NRF5340-QKAA-R7.step | [Link](https://infocenter.nordicsemi.com/pdf/nRF5340_PS_v1.3.pdf) |
| DAC80508ZRTER | Analog.pretty/QFN50P300X300X80-17N.kicad_mod | Analog.3dshapes/DAC80508ZRTER.step | [Link](https://www.ti.com/lit/ds/symlink/dac80508.pdf) |
| RE130F-41-175F-12P | Connectors.pretty/RE130F41175F12P.kicad_mod | Connectors.3dshapes/RE130F-41-175F-12P.stp | Included in datasheet directory |

## Library Statistics

- **Microcontroller.kicad_sym** - 30+ symbols (ESP32 family, RP2040)
- **RF_Wireless.kicad_sym** - 1 symbol (NRF5340)
- **Connectors.kicad_sym** - 1 symbol (relay connector)
- **Analog.kicad_sym** - 1 symbol (DAC80508)

**Total:** 33+ symbols

## Questions?

- See [ORGANIZATION.md](../../docs/ORGANIZATION.md) for library structure
- See [SETUP.md](../../docs/SETUP.md) for KiCad configuration
- See [CONTRIBUTING.md](../../docs/CONTRIBUTING.md) to add components
