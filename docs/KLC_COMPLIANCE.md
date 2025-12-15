# KiCad Library Convention (KLC) Compliance

This document summarizes the KiCad Library Convention (KLC) requirements that this library follows. Full KLC documentation is available at: https://klc.kicad.org/

## What is KLC?

The KiCad Library Convention (KLC) is a set of standards for creating KiCad library components. Following KLC ensures:
- Consistency across the library
- Compatibility with official KiCad libraries
- Professional quality components
- Ease of use for all users
- Proper electrical and physical representations

## General Requirements

### G1: File Encoding

- **Rule:** All library files must use UTF-8 encoding
- **Line Endings:** Unix-style (LF) only - configured in .gitattributes
- **Verification:** Files should not contain BOM (Byte Order Mark)

### G2: Naming Conventions

- **Characters:** Use only A-Z, a-z, 0-9, _, -, ., ,, +
- **No Spaces:** Use underscores or hyphens
- **Case:** CamelCase for words, preserve manufacturer capitalization
- **Acronyms:** ALL CAPS (USB, DAC, ADC, I2C, SPI)
- **Language:** English with American spelling

See [NAMING_CONVENTIONS.md](NAMING_CONVENTIONS.md) for detailed naming rules.

## Symbol Requirements

### S1: Symbol Naming

- Use manufacturer part number when available
- Include package variant if necessary
- Use descriptive names for generic components
- Follow naming hierarchy: Function → Manufacturer → Part Number → Variant

### S2: Pin Properties

**All pins must have:**
- **Pin number** - Matching datasheet
- **Pin name** - Descriptive, matching datasheet terminology
- **Pin type** - Correct electrical type:
  - Input
  - Output
  - Bidirectional (I/O)
  - Power Input
  - Power Output
  - Passive
  - Open Collector
  - Open Emitter
  - Unspecified (avoid when possible)

### S3: Symbol Grid

- **Grid size:** 100 mil (2.54mm) for pins
- **Pin spacing:** Minimum 100 mil between pins
- **Symbol body:** Can use 50 mil grid for outline
- **Pin length:** Typically 100 mil or 200 mil

### S4: Symbol Geometry

- **Rectangle symbols:** Preferred for ICs
- **Pin arrangement:** Logical, grouped by function (not physical package layout)
- **Power pins:** VCC/VDD at top, GND at bottom (conventional)
- **Size:** Large enough to be readable, not unnecessarily large
- **Symmetry:** Use when appropriate for clarity

### S5: Required Fields

Every symbol must have:

| Field | Description | Example |
|---|---|---|
| Reference | Component designator | U, R, C, J, etc. |
| Value | Part number or value | ESP32-WROOM-32 |
| Footprint | Default footprint | Microcontroller:ESP32-WROOM-32 |
| Datasheet | URL or path | https://... |

### S6: Optional Fields (Recommended)

| Field | Description | Example |
|---|---|---|
| Description | Brief description | WiFi & Bluetooth module |
| Keywords | Search terms | ESP32 WiFi BT IoT |
| Manufacturer | Manufacturer name | Espressif Systems |
| MPN | Manufacturer part number | ESP32-WROOM-32 |

### S7: Hidden Pins

- Use sparingly
- Only for multi-gate symbols with common power
- Must be clearly documented
- Not recommended for single-gate symbols

### S8: Reference Designator

Standard prefixes:
- R - Resistor
- C - Capacitor
- L - Inductor
- D - Diode, LED
- Q - Transistor
- U - Integrated Circuit
- J - Connector, Jack
- SW - Switch
- Y, X - Crystal, Oscillator
- TP - Test Point

## Footprint Requirements

### F1: Footprint Naming

- Use IPC-7351 naming for generic packages
- Use manufacturer part number for specific modules
- Include package variant (SMD, THT, Vertical, Horizontal)
- Be descriptive and unambiguous

### F2: Required Layers

**Copper Layers:**
- **F.Cu / B.Cu** - Pads only

**Technical Layers:**
- **F.SilkS / B.SilkS** - Silkscreen (component outline, pin 1)
- **F.Fab / B.Fab** - Fabrication layer (exact component dimensions)
- **F.CrtYd / B.CrtYd** - Courtyard (clearance zone)

**Reference and Value:**
- **REF\*\*** on F.SilkS (or F.Fab if silkscreen conflicts)
- **Value** on F.Fab

### F3: Pad Requirements

**Dimensions:**
- Follow manufacturer recommendations (datasheet)
- Or follow IPC-7351 standards
- Use appropriate tolerance for manufacturing

**Pad Properties:**
- Correct pad type (SMD, Through-hole, NPTH)
- Correct pad shape (Rectangular, Circular, Oval, Rounded Rectangle)
- Pin 1 typically rectangular (others oval/circular for THT)
- Thermal relief for large ground pads (when appropriate)

### F4: Silkscreen

- **Component outline** - Simplified body outline
- **Pin 1 indicator** - Clear marking (dot, line, chamfer)
- **No overlap with pads** - Minimum 0.1mm clearance
- **Text size** - 1.0mm height typical, 0.15mm stroke width
- **Readable orientation** - REF** on F.SilkS

### F5: Fabrication Layer

- **Exact component outline** - Per datasheet dimensions
- **Pin 1 indicator** - Mark pin 1 position
- **Centerlines** - For symmetric components
- **Value field** - Component value on F.Fab
- **Package outline** - Complete component body

### F6: Courtyard

- **Purpose:** Define keep-out zone around component
- **Minimum clearance:** 0.25mm from all component features
- **Larger clearance:** 0.5mm for large components or sensitive designs
- **Grid:** Courtyard on 0.05mm grid
- **Complete:** Fully closed polygon on F.CrtYd / B.CrtYd
- **Line width:** 0.05mm

### F7: 3D Models

- **Preferred format:** STEP (.step, .stp)
- **Alternative:** VRML (.wrl)
- **Alignment:** Correctly positioned relative to footprint
- **Origin:** Pin 1 or component center (clearly defined)
- **Scale:** Millimeters
- **Orientation:** Correct rotation to match footprint
- **Path:** Use environment variables (${KICAD_PERSONAL_3DMODEL_DIR})

### F8: Anchor Point

- **For ICs:** Pin 1
- **For connectors:** Pin 1 or geometric center
- **For passives:** Geometric center
- **Consistency:** Use same anchor point convention across similar components

## 3D Model Requirements

### M1: File Format

- **Primary:** STEP (.step, .stp) - industry standard
- **Secondary:** VRML (.wrl) - legacy but compatible
- **Avoid:** STL - no material/color information

### M2: Model Quality

- **Accuracy:** Dimensions match datasheet ±5%
- **Simplification:** Enough detail for visualization, not every minor feature
- **File size:** Keep under 1MB when possible (use simplified geometry)
- **Materials:** Correct colors (black IC body, gold pins, etc.)

### M3: Model Placement

- **Origin:** Align with footprint anchor point
- **Orientation:** Match footprint orientation
- **Height:** Correct Z-offset (sitting on PCB surface)
- **Scale:** 1:1 in millimeters
- **Verification:** Check in KiCad 3D viewer

## Documentation Requirements

### D1: Datasheet Links

- Every symbol should have a datasheet link
- Use permanent URLs when possible (manufacturer sites)
- For custom/generic components, provide equivalent documentation
- Update INDEX.md files when adding datasheets

### D2: Component Description

- Provide clear, concise description
- Include key specifications (voltage, current, pins, etc.)
- Note any special requirements or limitations
- Add keywords for searchability

### D3: Version Control

- Use git for all version control
- No version numbers in filenames
- Tag releases with semantic versioning (v1.0.0, v1.1.0)
- Maintain CHANGELOG for significant changes

## Validation Checklist

Use this checklist when adding or modifying components:

### Symbol Validation

- [ ] Symbol name follows conventions
- [ ] All pins on 100 mil grid
- [ ] All pins have correct pin numbers
- [ ] All pins have descriptive pin names
- [ ] All pins have correct electrical type
- [ ] Power pins at top, ground at bottom (when applicable)
- [ ] Pins logically grouped by function
- [ ] Reference field set correctly (U, R, C, J, etc.)
- [ ] Value field contains part number
- [ ] Footprint field links to correct footprint
- [ ] Datasheet URL provided
- [ ] Description field filled
- [ ] Keywords added for search
- [ ] No DRC errors in symbol editor

### Footprint Validation

- [ ] Footprint name follows conventions
- [ ] All pads match datasheet dimensions
- [ ] Pin 1 clearly marked
- [ ] Silkscreen doesn't overlap pads
- [ ] Courtyard present and adequate (0.25mm min clearance)
- [ ] Fabrication layer complete
- [ ] REF** on F.SilkS (visible and readable)
- [ ] Value on F.Fab
- [ ] Anchor point set correctly
- [ ] 3D model loads correctly
- [ ] 3D model aligned with footprint
- [ ] No DRC errors in footprint editor

### 3D Model Validation

- [ ] Model file exists and loads
- [ ] File format is STEP or VRML
- [ ] Model positioned correctly (origin at pin 1 or center)
- [ ] Model scaled correctly (1:1 in mm)
- [ ] Model oriented correctly (matches footprint)
- [ ] Model height correct (Z-offset from PCB)
- [ ] Materials/colors appropriate
- [ ] File size reasonable (< 1MB preferred)

### Integration Validation

- [ ] Symbol tested in schematic editor
- [ ] Footprint tested in PCB editor
- [ ] Symbol correctly links to footprint
- [ ] Footprint correctly links to 3D model
- [ ] Tested in real project
- [ ] No ERC errors in schematic
- [ ] No DRC errors in PCB layout
- [ ] 3D viewer shows component correctly
- [ ] Documentation updated (README, INDEX)

## Common KLC Violations to Avoid

### Symbols

- Pins not on 100 mil grid
- Missing pin names or numbers
- Incorrect pin types (everything as "Passive" or "Unspecified")
- Physical pin layout instead of logical grouping
- Missing required fields
- Unclear reference designators

### Footprints

- Silkscreen overlapping pads
- Missing courtyard layer
- Courtyard too small (< 0.25mm clearance)
- Missing pin 1 indicator
- Incorrect pad sizes
- Missing fabrication layer
- 3D model path using absolute paths instead of environment variables

### 3D Models

- Incorrect scale (not in millimeters)
- Wrong origin point
- Misaligned with footprint
- Excessive file size
- Missing or incorrect materials

## Tools for Validation

### Manual Validation

- KiCad Symbol Editor - Check for errors/warnings
- KiCad Footprint Editor - Check for errors/warnings
- KiCad 3D Viewer - Verify 3D model placement
- Design Rules Check (DRC) - Run in PCB editor
- Electrical Rules Check (ERC) - Run in schematic editor

### Automated Validation (Future)

This library may implement automated KLC validation scripts:
- `scripts/validate_klc.py` - Python script to check KLC compliance
- Pre-commit hooks - Automatic validation before git commit
- CI/CD pipeline - Automatic validation on pull requests

## Reference Links

- **Official KLC Documentation:** https://klc.kicad.org/
- **KiCad Documentation:** https://docs.kicad.org/
- **IPC-7351 Standard:** Land pattern naming standard for SMT components
- **KiCad Forum:** https://forum.kicad.info/ - Community help and discussions

## Questions?

- See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution workflow
- See [NAMING_CONVENTIONS.md](NAMING_CONVENTIONS.md) for detailed naming rules
- See [WORKFLOW.md](WORKFLOW.md) for development workflow
