# KiCad Project Templates

This directory contains project templates to help you quickly start new designs with pre-configured settings.

## Available Templates

### Schematic Templates

**ESP32_BasicBoard.kicad_sch** (To be created)
- Basic ESP32-WROOM-32 schematic
- Includes power supply (3.3V regulator)
- USB-to-serial interface (CH340, CP2102, or similar)
- Programming interface (boot button, EN button)
- Basic I/O headers

**RP2040_MinimalBoard.kicad_sch** (To be created)
- Minimal RP2040 schematic
- Power supply
- USB interface
- SWD programming interface
- Basic I/O

### PCB Templates

**Standard_2Layer.kicad_pcb** (To be created)
- 2-layer PCB with standard design rules
- Default trace widths: 0.25mm (signal), 0.5mm (power)
- Default clearance: 0.2mm
- Default via size: 0.8mm drill, 1.6mm pad
- Text sizes and styles pre-configured

**Standard_4Layer.kicad_pcb** (To be created)
- 4-layer PCB template
- Signal + Power/Ground + Ground/Power + Signal
- Appropriate via sizes for multilayer
- Standard design rules for 4-layer boards

## Creating Templates

Templates should be created using KiCad directly:

### Creating a Schematic Template

1. Create a new KiCad project
2. Design the schematic with common circuitry
3. Add placeholders for project-specific components
4. Save the schematic file
5. Copy to `templates/schematic_templates/`
6. Test by creating a new project from the template

### Creating a PCB Template

1. Create a new KiCad project
2. Set up design rules (File → Board Setup)
3. Configure layers
4. Set up net classes
5. Add board outline (if applicable)
6. Add mounting holes (if standard)
7. Save the PCB file
8. Copy to `templates/pcb_templates/`
9. Test by creating a new project from the template

### Creating a Complete Project Template

For a complete KiCad project template:

1. Create a directory: `templates/MyTemplate/`
2. Add these files:
   ```
   MyTemplate/
   ├── meta/
   │   ├── info.html        # Template description (HTML)
   │   └── icon.png         # Template icon (64x64 px)
   ├── MyTemplate.kicad_pro # Project file
   ├── MyTemplate.kicad_sch # Schematic
   ├── MyTemplate.kicad_pcb # PCB layout
   └── README.md            # Template usage instructions
   ```

3. Create `meta/info.html`:
   ```html
   <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">
   <HTML>
   <HEAD>
   <META HTTP-EQUIV="CONTENT-TYPE" CONTENT="text/html; charset=windows-1252">
   <TITLE>My Template</TITLE>
   </HEAD>
   <BODY LANG="en-US" BGCOLOR="#ffffff" DIR="LTR">
   <P><FONT SIZE=3><B>My Template Description</B></FONT></P>
   <P>Detailed description of what this template provides...</P>
   </BODY>
   </HTML>
   ```

4. Configure KiCad to use templates:
   - **Preferences → Configure Paths**
   - Set `KICAD_TEMPLATE_DIR` to point to this templates directory
   - Or copy templates to KiCad's default template directory

5. Test: **File → New Project from Template**

## Using Templates

### In KiCad

1. **File → New Project from Template**
2. Select template from the list
3. Choose project location and name
4. KiCad will copy template files and rename them

### Manually

1. Copy template directory to your project location
2. Rename all files to your project name
3. Open in KiCad

## Template Best Practices

### Schematic Templates

- Use clear hierarchical labels for common interfaces (power, I2C, SPI, etc.)
- Include frequently used components pre-configured
- Add title block with placeholders
- Document any required external components
- Keep it general enough to be useful across multiple projects

### PCB Templates

- Set conservative design rules (users can relax them)
- Include manufacturer capabilities in design rules
- Pre-configure layers appropriately
- Add board outline for common sizes (if applicable)
- Include mounting holes for standard enclosures
- Configure net classes (Power, Signal, High-Speed, etc.)

### Project Templates

- Include both schematic and PCB
- Add readme explaining template usage
- Include bill of materials (BOM) template
- Add standard footprints
- Document any library dependencies

## Common Template Use Cases

### Development Board Templates

- **ESP32 Development Board**
  - ESP32 module
  - USB-to-serial converter
  - Power management
  - Programming interface
  - I/O headers

- **RP2040 Development Board**
  - RP2040 with minimal support components
  - USB interface
  - SWD programming
  - Power supply
  - Boot selection

### Eurorack Module Template

- **12HP Eurorack Module**
  - Power connector (Eurorack standard)
  - CV/Gate inputs (±5V, ±10V)
  - Audio I/O (AC-coupled)
  - Standard PCB dimensions (12HP = 60.6mm)
  - Mounting holes at standard positions

### Sensor Node Template

- **Wireless Sensor Node**
  - Microcontroller (ESP32/RP2040)
  - Power management (battery + LDO)
  - Sensor interfaces (I2C, SPI, analog)
  - Wireless connectivity
  - Low-power considerations

## Contributing Templates

When adding new templates:

1. Test thoroughly in multiple scenarios
2. Document what the template provides
3. Create `meta/info.html` with description
4. Add icon if possible
5. Update this README with template description
6. Commit with clear message explaining template purpose

## Future Templates

Planned templates to add:

- [ ] ESP32 basic development board
- [ ] RP2040 minimal board
- [ ] Eurorack 12HP module
- [ ] Battery-powered sensor node
- [ ] USB device template
- [ ] Audio I/O interface
- [ ] Motor controller board

Feel free to contribute additional templates!
