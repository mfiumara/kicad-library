# Datasheet Index

This directory contains datasheets and technical documentation for components in this library, organized by category.

## How to Use This Index

- **Local PDFs:** Datasheets stored in this repository are linked directly
- **Online Links:** Links to manufacturer websites for readily available datasheets
- **Version:** Datasheet version/revision noted when available

## Microcontroller

### Espressif ESP32 Family

#### ESP32 Original (WROOM, WROVER variants)
- **ESP32-WROOM-32 Datasheet** - [Online](https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf)
- **ESP32-WROOM-32D & 32U Datasheet** - [Online](https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32d_esp32-wroom-32u_datasheet_en.pdf)
- **ESP32 Technical Reference Manual** - [Online](https://www.espressif.com/sites/default/files/documentation/esp32_technical_reference_manual_en.pdf)
- **ESP32 Datasheet** - [Online](https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf)

#### ESP32-C3 (RISC-V)
- **ESP32-C3-MINI-1 Datasheet** - [Online](https://www.espressif.com/sites/default/files/documentation/esp32-c3-mini-1_datasheet_en.pdf)
- **ESP32-C3 Technical Reference Manual** - [Online](https://www.espressif.com/sites/default/files/documentation/esp32-c3_technical_reference_manual_en.pdf)

#### ESP32-S2 (WiFi only)
- **ESP32-S2-MINI-1 Datasheet** - [Online](https://www.espressif.com/sites/default/files/documentation/esp32-s2-mini-1_esp32-s2-mini-1u_datasheet_en.pdf)
- **ESP32-S2 Technical Reference Manual** - [Online](https://www.espressif.com/sites/default/files/documentation/esp32-s2_technical_reference_manual_en.pdf)

#### ESP32-S3 (WiFi & BLE 5)
- **ESP32-S3-WROOM-1 Datasheet** - [Online](https://www.espressif.com/sites/default/files/documentation/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf)
- **ESP32-S3 Technical Reference Manual** - [Online](https://www.espressif.com/sites/default/files/documentation/esp32-s3_technical_reference_manual_en.pdf)

#### ESP8685 (Compact WiFi & BLE)
- **ESP8685-WROOM-05 Datasheet** - [Online](https://www.espressif.com/sites/default/files/documentation/esp8685-wroom-05_datasheet_en.pdf)

### Raspberry Pi

#### RP2040
- **RP2040 Datasheet** - [Online](https://datasheets.raspberrypi.com/rp2040/rp2040-datasheet.pdf)
- **Raspberry Pi Pico Datasheet** - [Online](https://datasheets.raspberrypi.com/pico/pico-datasheet.pdf)
- **Raspberry Pi Pico W Datasheet** - [Online](https://datasheets.raspberrypi.com/picow/pico-w-datasheet.pdf)
- **Hardware Design Guide** - [Online](https://datasheets.raspberrypi.com/rp2040/hardware-design-with-rp2040.pdf)

## RF_Wireless

### Nordic Semiconductor

#### nRF5340
- **nRF5340 Product Specification v1.3** - [Online](https://infocenter.nordicsemi.com/pdf/nRF5340_PS_v1.3.pdf)
- **nRF5340 Objective Product Specification** - [Online](https://infocenter.nordicsemi.com/pdf/nRF5340_OPS_v0.5.pdf)
- **nRF5340 DK User Guide** - [Online](https://infocenter.nordicsemi.com/pdf/nRF5340_DK_User_Guide_v1.2.pdf)

## Connectors

### RE130F Relay Connector
- **RE130F-41-175F-12P** - Datasheet location: `Connectors/RE130F/`
- Connector for relay modules

### Audio Jacks
See AudioJacks submodule documentation:
- Path: `submodules/AudioJacks/DATA.md`
- Comprehensive specs for PJ301, PJ302, PJ398, PJ3410, PJ366, FCR1281

## Analog

### Texas Instruments

#### DAC80508 - 8-Channel 16-Bit DAC
- **DAC80508 Datasheet** - Local: [`Analog/DAC80508/dac80508.pdf`](Analog/DAC80508/dac80508.pdf) | [Online](https://www.ti.com/lit/ds/symlink/dac80508.pdf)
- **Key Specs:**
  - 8 channels, 16-bit resolution
  - SPI interface (up to 50 MHz)
  - Internal reference: 1.25V, 2.5V
  - Supply: 2.7V to 5.5V
  - Package: TSSOP-16, VQFN-16
- **Application Notes:**
  - [DAC80508 Application Note](https://www.ti.com/lit/an/slaa849/slaa849.pdf)

## Adding Datasheets

When adding components to the library, update this index:

### For Local PDFs

1. Create directory: `CategoryName/ManufacturerOrSeries/`
2. Add PDF: `datasheet-name.pdf`
3. Update this index with entry:
   ```markdown
   #### Component Name
   - **Datasheet** - Local: [`CategoryName/Series/file.pdf`](path) | [Online](url)
   - **Key Specs:** Brief specification summary
   ```

### For Online-Only References

1. Add entry to appropriate category:
   ```markdown
   #### Component Name
   - **Datasheet** - [Online](manufacturer-url)
   ```

## Datasheet Organization

```
datasheets/
├── Microcontroller/
│   ├── ESP32/
│   ├── RP2040/
│   └── STM32/
├── RF_Wireless/
│   ├── NRF5340/
│   └── LoRa/
├── Connectors/
│   ├── RE130F/
│   └── USB/
├── Analog/
│   ├── DAC80508/
│   ├── ADC/
│   └── OpAmp/
└── INDEX.md (this file)
```

## Best Practices

### Naming Conventions

- Use lowercase with hyphens: `component-name-datasheet.pdf`
- Include revision: `esp32-wroom-32-v3.4-datasheet.pdf` (optional)
- Keep names concise but descriptive

### Storage Guidelines

**Store locally when:**
- Datasheet might become unavailable online
- Component is custom or obscure
- Frequently referenced during design
- File size is reasonable (< 5MB)

**Link online when:**
- Manufacturer provides stable permalink
- Datasheet is very large (> 5MB)
- Datasheet updates frequently
- Common/popular components with reliable sources

### Version Control

- Note datasheet version/date when adding
- Update links if manufacturer changes URL
- Keep old versions if significant changes occur
- Check links periodically for dead links

## Additional Resources

### Espressif
- [Espressif Documentation](https://docs.espressif.com/)
- [ESP-IDF Programming Guide](https://docs.espressif.com/projects/esp-idf/en/latest/)
- [ESP32 Forum](https://www.esp32.com/)

### Raspberry Pi
- [RP2040 Documentation](https://www.raspberrypi.com/documentation/microcontrollers/)
- [Pico SDK](https://github.com/raspberrypi/pico-sdk)

### Nordic Semiconductor
- [nRF5340 Product Page](https://www.nordicsemi.com/Products/nRF5340)
- [nRF5340 DK](https://www.nordicsemi.com/Products/Development-hardware/nRF5340-DK)
- [nRF Connect SDK](https://www.nordicsemi.com/Products/Development-software/nRF-Connect-SDK)

### Texas Instruments
- [TI Product Folder - DAC80508](https://www.ti.com/product/DAC80508)
- [TI Precision Labs - DACs](https://www.ti.com/video/series/ti-precision-labs-dacs.html)

## Questions?

- See [ORGANIZATION.md](../../docs/ORGANIZATION.md) for library structure
- See [CONTRIBUTING.md](../../docs/CONTRIBUTING.md) for adding datasheets
