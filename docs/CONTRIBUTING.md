# Contributing to the KiCad Library

Thank you for contributing to this KiCad library! This guide will help you add new components following our standards and best practices.

## Before You Start

1. Read [ORGANIZATION.md](ORGANIZATION.md) to understand the library structure
2. Review [NAMING_CONVENTIONS.md](NAMING_CONVENTIONS.md) for naming guidelines
3. Check [KLC_COMPLIANCE.md](KLC_COMPLIANCE.md) for KiCad Library Convention requirements
4. Ensure you have the latest version of the repository

## Quick Contribution Checklist

- [ ] Component categorized correctly (Microcontroller, RF_Wireless, Connectors, Analog)
- [ ] Symbol created with proper properties and naming
- [ ] Footprint created following KLC standards
- [ ] 3D model added (if available)
- [ ] Datasheet added or linked
- [ ] Names follow conventions (see NAMING_CONVENTIONS.md)
- [ ] Tested in a real project
- [ ] Category README.md updated with new component
- [ ] No KiCad errors or warnings

## Adding a New Component

### Step 1: Determine the Category

Identify which category your component belongs to:

- **Microcontroller** - MCUs, SoMs, development boards with MCUs
- **RF_Wireless** - RF modules, Bluetooth, LoRa, GPS, cellular
- **Connectors** - Headers, jacks, USB, power connectors
- **Analog** - ADCs, DACs, op-amps, analog switches, voltage references

If your component doesn't fit existing categories, propose a new category in a GitHub issue.

### Step 2: Create the Symbol

#### Using the Symbol Editor

1. Open KiCad Symbol Editor
2. Select the appropriate category library (e.g., `Microcontroller.kicad_sym`)
3. Click **File → New Symbol** or duplicate a similar existing symbol
4. Draw the symbol following these guidelines:

**Symbol Requirements:**
- Use a 100 mil (2.54mm) grid
- Pin numbers must match the datasheet
- Pin names should be clear and descriptive
- Group related pins together (power, I/O, communication)
- Use standard pin electrical types (Input, Output, Bidirectional, Power Input, etc.)
- Add invisible power pins if appropriate for the component

**Required Properties:**
- **Reference** - Default reference designator (U for ICs, J for connectors, etc.)
- **Value** - Component part number or generic name
- **Footprint** - Default footprint (format: `CategoryName:FootprintName`)
- **Datasheet** - URL or path to datasheet
- **Description** - Brief component description
- **Keywords** - Searchable keywords (manufacturer, part family, function)
- **Manufacturer** - Manufacturer name
- **Manufacturer Part Number** - Official part number

**Optional Properties:**
- **Supplier** - Distributor name (Digi-Key, Mouser, etc.)
- **Supplier Part Number** - Distributor part number

#### Naming Convention

Follow the naming convention from NAMING_CONVENTIONS.md:

```
ComponentType_ManufacturerPrefix_PartNumber_Package
```

**Examples:**
- `ESP32-WROOM-32` - ESP32 WiFi/BT module
- `NRF5340-QKAA-R7` - Nordic nRF5340 wireless SoC
- `DAC80508ZRTER` - TI 8-channel DAC

### Step 3: Create the Footprint

#### Using the Footprint Editor

1. Open KiCad Footprint Editor
2. Select the appropriate category library (e.g., `Microcontroller.pretty`)
3. Click **File → New Footprint** or duplicate a similar existing footprint
4. Create the footprint following these guidelines:

**Footprint Requirements:**
- Use correct pad sizes from datasheet
- Include silkscreen outline (component body)
- Add pin 1 indicator
- Include proper courtyard (0.25mm clearance minimum)
- Add reference designator (REF**) on F.SilkS layer
- Add value field on F.Fab layer
- Add fabrication layer (F.Fab) with exact component outline
- Use correct pad types (SMD, Through-hole, NPTH)

**Layers:**
- **F.Cu** / **B.Cu** - Copper layers (pads)
- **F.SilkS** / **B.SilkS** - Silkscreen (component outline, pin 1)
- **F.Fab** / **B.Fab** - Fabrication layer (exact component dimensions)
- **F.CrtYd** / **B.CrtYd** - Courtyard (0.25mm clearance around component)

**Naming Convention:**

Follow manufacturer/industry standards or use descriptive names:

```
ManufacturerPrefix_PartNumber_Package
```

**Examples:**
- `ESP32-WROOM-32.kicad_mod` - ESP32 WROOM module
- `QFN50P300X300X80-17N.kicad_mod` - QFN package (0.5mm pitch, 3x3mm, 17 pins)
- `Raspberrypi_pico2_w_SMD.kicad_mod` - RP2040 Pico W SMD variant

### Step 4: Add 3D Model

3D models enhance PCB visualization and help catch mechanical issues.

**Where to Get 3D Models:**
1. **Manufacturer website** - Most manufacturers provide STEP models
2. **GrabCAD** - Community 3D model library
3. **SnapEDA / UltraLibrarian** - Component library websites
4. **Create your own** - Use FreeCAD or other CAD software

**3D Model Requirements:**
- Use STEP format (.step, .stp) - preferred for accuracy
- Alternatively, VRML format (.wrl) for compatibility
- Place at origin (0, 0, 0)
- Orient correctly (pin 1 at origin or clearly marked)
- Scale in millimeters
- Name matches footprint: `FootprintName.step`

**Adding 3D Model to Footprint:**

1. In Footprint Editor, open footprint properties
2. Go to **3D Settings** tab
3. Click **Add 3D Shape**
4. Browse to: `${KICAD_PERSONAL_3DMODEL_DIR}/CategoryName.3dshapes/ModelName.step`
5. Adjust offset, scale, and rotation as needed
6. Verify in 3D viewer (View → 3D Viewer)

**File Location:**
```
libraries/3dmodels/CategoryName.3dshapes/ModelName.step
```

### Step 5: Add Datasheet

**Option 1: Add PDF to Repository**

For components you use frequently or where online datasheets might disappear:

1. Download PDF from manufacturer
2. Place in appropriate category:
   ```
   libraries/datasheets/CategoryName/ManufacturerOrPartSeries/datasheet.pdf
   ```
3. Update `libraries/datasheets/CategoryName/INDEX.md` with entry

**Option 2: Link to Online Datasheet**

For readily available components:

1. Add link to INDEX.md:
   ```markdown
   ## DAC80508 - 8-Channel DAC
   - [Datasheet](https://www.ti.com/lit/ds/symlink/dac80508.pdf)
   - Manufacturer: Texas Instruments
   - Package: TSSOP-16
   ```

### Step 6: Link Symbol to Footprint

1. Open Symbol Editor
2. Select your symbol
3. Edit symbol properties
4. Set **Footprint** field to: `CategoryName:FootprintName`
   - Example: `Microcontroller:ESP32-WROOM-32`

### Step 7: Test Your Component

**Critical - Do not skip this step!**

1. Create a test project or use an existing project
2. Add your new symbol to a schematic
3. Assign the footprint (should auto-assign if properly linked)
4. Generate netlist and import to PCB
5. Verify footprint appears correctly
6. Check 3D viewer - model should appear in correct position
7. Run DRC (Design Rules Check) - should pass with no errors
8. Verify symbol properties are complete

### Step 8: Update Documentation

**Update Category README:**

Add entry to `libraries/symbols/README.md`, `libraries/footprints/README.md`, or `libraries/3dmodels/README.md`:

```markdown
## ESP32-WROOM-32
- **Category:** Microcontroller
- **Description:** WiFi & Bluetooth module with ESP32 SoC
- **Symbol:** Microcontroller.kicad_sym → ESP32-WROOM-32
- **Footprint:** Microcontroller.pretty/ESP32-WROOM-32.kicad_mod
- **3D Model:** Microcontroller.3dshapes/ESP32-WROOM-32.step
- **Datasheet:** [Link](https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf)
```

### Step 9: Commit Your Changes

**Good Commit Message Format:**

```
Add [ComponentName] to [Category] library

- Added symbol: [symbol details]
- Added footprint: [footprint details]
- Added 3D model: [model source/format]
- Added datasheet: [PDF or link]

Tested in: [project name or "test project"]
```

**Example:**
```
Add ESP32-S3-WROOM-1 to Microcontroller library

- Added symbol: ESP32-S3-WROOM-1 with full pinout
- Added footprint: SMD module footprint with courtyard
- Added 3D model: STEP from Espressif
- Added datasheet: Link to manufacturer PDF

Tested in: wifi-sensor-node project
```

## Best Practices

### Symbol Design

1. **Logical pin arrangement** - Group by function, not physical location
2. **Clear labeling** - Use descriptive pin names (SDA, SCL, TX, RX, not GPIO1, GPIO2)
3. **Power pins** - Place VCC at top, GND at bottom (conventional)
4. **Consistent spacing** - Use 100 mil grid, pins every 100 mils
5. **Hidden power pins** - Use sparingly, only for multi-gate ICs

### Footprint Design

1. **Follow datasheet exactly** - Pad sizes, positions, tolerances
2. **Add keepout zones** - For components that need clearance
3. **Thermal relief** - For large ground pads on SMD components
4. **Fiducials** - Add to complex footprints for automated assembly
5. **Text size** - Readable but not too large (0.8-1.0mm typical)

### 3D Models

1. **Accurate dimensions** - Model should match datasheet specifications
2. **Simplified geometry** - Don't include every tiny detail (performance)
3. **Correct origin** - Pin 1 or center of component
4. **File size** - Keep under 1MB when possible (use STEP over STL)

### Documentation

1. **Complete datasheets** - Link or include full manufacturer datasheet
2. **Application notes** - Include relevant app notes for complex ICs
3. **Known issues** - Document any quirks or special considerations
4. **Errata** - Note silicon errata for microcontrollers

## Component Variants

If a component has multiple package options:

**Create separate symbols:**
- `ComponentName-Package1`
- `ComponentName-Package2`

**Examples:**
- `ATmega328P-PU` (DIP)
- `ATmega328P-AU` (TQFP)

Or use a single symbol with multiple footprint options if pinout is identical.

## Quality Checklist

Before submitting your component:

- [ ] Symbol follows 100 mil grid
- [ ] All pins have correct electrical types
- [ ] Pin names are clear and match datasheet terminology
- [ ] Footprint pads match datasheet dimensions
- [ ] Courtyard is present and sufficient (0.25mm clearance minimum)
- [ ] Silkscreen doesn't overlap pads
- [ ] Pin 1 indicator is clear
- [ ] 3D model is correctly positioned and scaled
- [ ] All required properties are filled (Reference, Value, Footprint, Datasheet)
- [ ] Symbol links to correct footprint
- [ ] Footprint links to correct 3D model
- [ ] Component tested in a real project
- [ ] No DRC errors when used in design
- [ ] Documentation updated (README.md, INDEX.md)

## Getting Help

- **Questions?** - Open a GitHub issue with the "question" label
- **Found a bug?** - Open an issue with the "bug" label
- **Want to propose changes?** - Open an issue with the "enhancement" label

## Code of Conduct

- Be respectful and constructive
- Follow the established conventions and standards
- Test your contributions before submitting
- Document your changes clearly
- Help review others' contributions

## License

By contributing to this library, you agree that your contributions will be licensed under the same license as the project (see LICENSE file in repository root).
