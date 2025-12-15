# CO2 Sensor Adapter PCB

This PCB adapter connects the Waveshare ESP32-C6 Mini to the Sensirion SCD41 CO2 sensor.

## Pin Assignments

### ESP32-C6 Mini (Castellated Holes)
- 3.3V Power
- GND
- GPIO6 (SDA)
- GPIO7 (SCL)
- GPIO8 (Status LED)

### SCD41 Sensor
- VDD (3.3V)
- GND
- SDA
- SCL

## Design Notes

1. The PCB uses castellated holes to match the ESP32-C6 Mini's edge connectors
2. I2C pull-up resistors (4.7kΩ) are included for both SDA and SCL lines
3. Power filtering capacitors (100nF) are placed near both the ESP32 and SCD41 power pins
4. The PCB includes mounting holes for secure installation in the enclosure
5. Status LED with current-limiting resistor (220Ω) is included

## PCB Specifications
- 2-layer design
- 1.6mm thickness
- FR4 material
- ENIG finish
- Minimum trace width: 0.2mm
- Minimum via diameter: 0.4mm

## Manufacturing Notes
- Panelize with 2mm spacing between boards
- Include mouse bites for easy separation
- Add fiducial marks for automated assembly 