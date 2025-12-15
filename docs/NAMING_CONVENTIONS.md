# Naming Conventions

This document defines the naming standards for all components in this KiCad library. Following these conventions ensures consistency, searchability, and compatibility with KiCad Library Convention (KLC) standards.

## General Rules

1. **Use only ASCII characters** - No special characters, accents, or Unicode
2. **Allowed characters** - Alphanumeric (A-Z, a-z, 0-9), underscore (_), hyphen (-), period (.), comma (,), plus (+)
3. **No spaces** - Use underscores or hyphens instead
4. **CamelCase for words** - Multi-word names use CamelCase (e.g., `AudioJack`, `PowerSupply`)
5. **ALL CAPS for acronyms** - USB, DAC, ADC, MCU, SoC, FPGA, I2C, SPI, UART
6. **English language** - Use American English spelling
7. **Descriptive names** - Names should clearly indicate what the component is

## Symbol Naming

### Format

```
[Function]_[Manufacturer]_[PartNumber]_[Variant]
```

**Hierarchy:**
1. Function (optional for well-known parts)
2. Manufacturer prefix (optional but recommended)
3. Part number (required)
4. Variant/Package (optional)

### Examples

**Microcontrollers:**
```
ESP32-WROOM-32          # Espressif WiFi/BT module
ESP32-C3-MINI-1         # Espressif ESP32-C3 mini module
NRF5340-QKAA-R7         # Nordic nRF5340 wireless SoC
RP2040                  # Raspberry Pi RP2040 MCU
STM32F103C8T6           # STM32 ARM Cortex-M3
```

**Analog ICs:**
```
DAC80508ZRTER           # TI 8-channel DAC (full part number)
ADC_ADS1115             # TI 16-bit ADC
OpAmp_OPA2134           # TI dual op-amp
```

**Connectors:**
```
USB_C_Receptacle        # Generic USB-C connector
Conn_Audio_Jack_3.5mm   # 3.5mm audio jack
Header_2x20_P2.54mm     # 2x20 pin header, 2.54mm pitch
```

**Power:**
```
Regulator_LDO_AMS1117-3.3  # 3.3V LDO regulator
DC_DC_Converter_TPS54331   # TI buck converter
```

### Symbol Naming Guidelines

1. **Use manufacturer part number when possible**
   - Exact match to datasheet: `DAC80508ZRTER`, `NRF5340-QKAA-R7`

2. **For generic components, use descriptive names**
   - `Conn_USB_C_Receptacle` instead of random connector model
   - `Regulator_LDO_3.3V` for generic LDOs

3. **Include key specifications in name when helpful**
   - `DAC_8Channel_16Bit` - Clear what it does
   - `ADC_16Bit_4Channel` - Specs in name

4. **Manufacturer prefix recommendations:**
   - Espressif: ESP32, ESP8266
   - Nordic: NRF
   - Texas Instruments: Use full part number (DAC80508, ADS1115)
   - STMicroelectronics: STM32
   - Raspberry Pi: RP2040, Pico

## Footprint Naming

### Format

Footprints follow industry standard package codes or descriptive names:

```
[Manufacturer]_[PartNumber]_[Package]
```

Or for generic packages:

```
[PackageType][Pitch][Size]-[PinCount][Variant]
```

### Examples

**Manufacturer-Specific Modules:**
```
ESP32-WROOM-32.kicad_mod           # Espressif ESP32 WROOM module
ESP32-PICO-D4.kicad_mod            # ESP32 PICO module
Raspberrypi_pico2_w_SMD.kicad_mod  # RP2040 Pico W SMD
Raspberrypi_pico2_THT.kicad_mod    # RP2040 Pico W through-hole
```

**Standard Package Codes:**
```
QFN50P300X300X80-17N.kicad_mod     # QFN, 0.5mm pitch, 3x3mm, 17 pins
SOIC127P600X175-8N.kicad_mod       # SOIC-8, 1.27mm pitch
TSSOP50P640X110-16N.kicad_mod      # TSSOP-16
DIP254P762X508-28N.kicad_mod       # DIP-28, 2.54mm pitch
```

**Connectors:**
```
USB_C_Receptacle_GCT_USB4105.kicad_mod  # Specific USB-C connector
Header_2x20_P2.54mm_Vertical.kicad_mod  # 2x20 header, vertical
AudioJack_3.5mm_PJ301M.kicad_mod        # 3.5mm audio jack
```

### Package Code Format (IPC-7351)

For generic IC packages:

```
[PackageType][Pitch]P[BodyLength]X[BodyWidth]X[Height]-[PinCount][Variant]
```

**Package Types:**
- QFN - Quad Flat No-lead
- QFP - Quad Flat Package
- SOIC - Small Outline IC
- TSSOP - Thin Shrink Small Outline Package
- DIP - Dual Inline Package
- BGA - Ball Grid Array

**Pitch codes:**
- 50 = 0.50mm
- 65 = 0.65mm
- 80 = 0.80mm
- 127 = 1.27mm
- 254 = 2.54mm

**Dimensions in tenth of mm:**
- 600 = 6.0mm
- 300 = 3.0mm
- 175 = 1.75mm

**Examples:**
```
QFN50P300X300X80-17N    # QFN, 0.5mm pitch, 3x3mm body, 0.8mm height, 17 pins
SOIC127P600X175-8N      # SOIC, 1.27mm pitch, 6x1.75mm, 8 pins
DIP254P762X508-28N      # DIP, 2.54mm pitch, 7.62x5.08mm, 28 pins
```

### Footprint Suffix Conventions

- **Vertical** - Component mounted perpendicular to PCB
- **Horizontal** - Component mounted parallel to PCB
- **SMD** - Surface mount
- **THT** - Through-hole technology
- **_HandSolder** - Larger pads for hand soldering

## 3D Model Naming

3D models should match their corresponding footprint name:

```
FootprintName.step
FootprintName.wrl
```

### Examples

```
ESP32-WROOM-32.step
QFN50P300X300X80-17N.step
USB_C_Receptacle_GCT_USB4105.step
AudioJack_3.5mm_PJ301M.wrl
```

### 3D Model File Formats

- **Preferred:** STEP (.step, .stp) - Universal, accurate
- **Alternative:** VRML (.wrl) - Older but widely compatible
- **Avoid:** STL (.stl) - No color/material info

## Library File Naming

### Symbol Libraries

```
CategoryName.kicad_sym
```

**Examples:**
```
Microcontroller.kicad_sym
RF_Wireless.kicad_sym
Connectors.kicad_sym
Analog.kicad_sym
Power.kicad_sym
Sensors.kicad_sym
```

### Footprint Libraries

```
CategoryName.pretty/
```

**Examples:**
```
Microcontroller.pretty/
RF_Wireless.pretty/
Connectors.pretty/
Analog.pretty/
```

### 3D Model Libraries

```
CategoryName.3dshapes/
```

**Examples:**
```
Microcontroller.3dshapes/
RF_Wireless.3dshapes/
Connectors.3dshapes/
Analog.3dshapes/
```

## Datasheet Naming

### Directory Structure

```
CategoryName/ManufacturerOrSeries/
```

**Examples:**
```
Microcontroller/ESP32/
Microcontroller/RP2040/
Analog/DAC80508/
RF_Wireless/NRF5340/
```

### PDF Naming

Use lowercase with hyphens, matching manufacturer naming when possible:

```
manufacturer-partnumber-datasheet.pdf
manufacturer-partnumber-appnote.pdf
```

**Examples:**
```
esp32-wroom-32-datasheet.pdf
dac80508.pdf
nrf5340-datasheet.pdf
rp2040-datasheet.pdf
```

## Property Naming (Symbol Fields)

Standard KiCad properties use specific capitalization:

### Required Properties

- **Reference** - Component designator (R, C, U, J, etc.)
- **Value** - Part number or value
- **Footprint** - CategoryName:FootprintName
- **Datasheet** - URL or file path

### Optional Properties

- **Description** - Brief component description
- **Keywords** - Space-separated search terms
- **Manufacturer** - Full manufacturer name
- **MPN** (or Manufacturer Part Number) - Official part number
- **Supplier** - Distributor (Digi-Key, Mouser, etc.)
- **SPN** (or Supplier Part Number) - Distributor part number
- **Package** - Package type (QFN, SOIC, etc.)
- **Datasheet_URL** - Direct link to online datasheet

## Reference Designators

Standard reference prefixes:

| Type | Prefix | Example |
|---|---|---|
| Resistor | R | R1, R10 |
| Capacitor | C | C1, C22 |
| Inductor | L | L1, L3 |
| Diode | D | D1, D5 |
| LED | D or LED | D1, LED1 |
| Transistor | Q | Q1, Q7 |
| Integrated Circuit | U | U1, U15 |
| Connector | J or P | J1, P2 |
| Jack | J | J1 |
| Plug | P | P1 |
| Switch | SW | SW1 |
| Button | SW or BTN | SW1, BTN1 |
| Fuse | F | F1 |
| Crystal/Oscillator | Y or X | Y1, X1 |
| Transformer | T | T1 |
| Test Point | TP | TP1 |
| Module | MOD or U | MOD1, U5 |

## Variant Naming

When a component has multiple variants (packages, voltages, etc.):

### Package Variants

```
PartNumber-PackageCode
```

**Examples:**
```
ATmega328P-PU        # DIP package
ATmega328P-AU        # TQFP package
ATmega328P-MU        # QFN package
```

### Voltage/Specification Variants

```
PartNumber-Specification
```

**Examples:**
```
AMS1117-3.3          # 3.3V LDO
AMS1117-5.0          # 5.0V LDO
LM358-Single         # Single supply version
LM358-Dual           # Dual supply version
```

## Common Abbreviations

### Package Types
- DIP - Dual Inline Package
- SIP - Single Inline Package
- QFP - Quad Flat Package
- QFN - Quad Flat No-lead
- SOIC - Small Outline IC
- SSOP - Shrink Small Outline Package
- TSSOP - Thin Shrink Small Outline Package
- BGA - Ball Grid Array
- LGA - Land Grid Array

### Component Types
- MCU - Microcontroller Unit
- MPU - Microprocessor Unit
- SoC - System on Chip
- SoM - System on Module
- DAC - Digital-to-Analog Converter
- ADC - Analog-to-Digital Converter
- GPIO - General Purpose Input/Output
- PWM - Pulse Width Modulation
- LDO - Low Dropout Regulator
- SMPS - Switched Mode Power Supply

### Interfaces
- I2C - Inter-Integrated Circuit
- SPI - Serial Peripheral Interface
- UART - Universal Asynchronous Receiver/Transmitter
- USB - Universal Serial Bus
- CAN - Controller Area Network
- JTAG - Joint Test Action Group

### Mounting
- SMD - Surface Mount Device
- SMT - Surface Mount Technology
- THT - Through-Hole Technology
- TH - Through-Hole

## File Naming Best Practices

1. **Be specific** - `ESP32-WROOM-32` better than `ESP32-Module`
2. **Include key specs** - `Header_2x20_P2.54mm` shows pitch
3. **Match datasheets** - Use manufacturer part numbers when possible
4. **Avoid version numbers in names** - Use git for versioning
5. **Consistent capitalization** - CamelCase for words, preserve manufacturer case
6. **No redundant info** - Don't include category in symbol name if already in library

## Examples of Good vs. Bad Naming

### Good Names ✓
```
ESP32-WROOM-32                    # Specific, matches datasheet
DAC80508ZRTER                     # Full manufacturer part number
Conn_USB_C_Receptacle             # Descriptive, clear function
QFN50P300X300X80-17N              # Standard package code
Raspberrypi_pico2_w_SMD           # Clear variant (SMD vs THT)
```

### Bad Names ✗
```
esp32 module                      # Spaces, lowercase, vague
DAC                              # Too generic
usb-c                            # Missing connector type
qfn17                            # Missing dimensions
rpi_pico                         # Ambiguous variant
Module1                          # Meaningless
IC_2.kicad_mod                   # No information
connector.kicad_mod              # Too generic
```

## Questions?

- See [KLC_COMPLIANCE.md](KLC_COMPLIANCE.md) for official KiCad standards
- See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution workflow
- See [ORGANIZATION.md](ORGANIZATION.md) for library structure
