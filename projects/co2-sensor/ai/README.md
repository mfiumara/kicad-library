# CO2 Sensor with Home Assistant Integration

A DIY CO2 sensor project based on the Waveshare ESP32-C6 Mini and SCD41 CO2 sensor, designed for easy integration with Home Assistant.

## Hardware Components

- [Waveshare ESP32-C6 Mini](https://www.waveshare.com/esp32-c6-mini.htm)
- [Sensirion SCD41 CO2 Sensor](https://sensirion.com/products/catalog/SCD41/)
- Custom PCB adapter (in development)
- **Enclosure:** [CamdenBoss CBRS02VGY Room Sensor Enclosure, Size 2, Vented, Grey, 74x74x25.5mm](https://www.camdenboss.com/camden-boss/cbrs02vgy-room-sensor-enclosure,-size-2,-vented,-grey,-74x74x25.5mm/c-23/p-24164)

## Enclosure Details

- **Model:** CamdenBoss CBRS02VGY (Room Sensor Enclosure, Size 2, Vented, Grey)
- **External Dimensions:** 74 × 74 × 25.5 mm
- **Internal Dimensions:** 66 × 66 × 17 mm
- **Vented housing** for airflow (ideal for CO2, temperature, and humidity sensors)
- **Wall-mountable** with rear knockout for cable entry
- **Internal PCB mount pillars** for easy installation
- **Material:** ABS UL94-V0 (flame retardant)
- **Color:** Grey (other colors available)
- **IP20 rated** (suitable for indoor use)

## PCB Mounting

- The PCB will be designed to fit the internal size: **66 × 66 mm**
- Mounting holes will be positioned to match the internal PCB mount pillars of the enclosure
- If required, adhesive standoffs can be used for additional support or alternative mounting
- Ensure that the SCD41 sensor is aligned with the vented area for optimal airflow

## Project Structure

```
co2-sensor/
├── firmware/           # ESPHome firmware configuration
├── hardware/          # Hardware design files
│   ├── pcb/          # PCB design files (KiCad)
│   └── enclosure/    # 3D model files for the enclosure
└── docs/             # Additional documentation
```

## Features

- CO2 concentration measurement
- Temperature and humidity monitoring
- Easy integration with Home Assistant
- Compact and modular design
- Off-the-shelf components where possible

## Development Status

🚧 This project is currently under development. 🚧

## License

[Add your chosen license here] 