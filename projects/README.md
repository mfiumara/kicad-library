# Projects

This directory contains reference projects and design examples that use the component libraries in this repository.

## Purpose

These projects serve multiple roles:

1. **Reference Designs** - Working examples of how to use library components
2. **Test Cases** - Verify that library changes don't break existing designs
3. **Templates** - Starting points for similar projects
4. **Documentation** - Practical examples of component usage

## Projects

### co2-sensor/

CO2 sensor project with multiple design variants.

**Description:**
Environmental monitoring device measuring CO2 concentration, temperature, and humidity.

**Variants:**

#### no-ai/ - Original Design
- **Main Board:** ESP32-based CO2 sensor
- **Key Components:**
  - ESP32-WROOM-32 (WiFi/BT connectivity)
  - CO2 sensor (NDIR or equivalent)
  - Temperature/humidity sensor
  - Power supply circuitry
  - Display interface (optional)

- **Features:**
  - WiFi connectivity for data logging
  - Local data display
  - Battery or USB powered
  - ESPHome integration ready

#### ai/ - AI-Assisted Variant
- **Location:** `ai/hardware/pcb/`
- **Files:**
  - co2-sensor-adapter.kicad_pro
  - co2-sensor-adapter.kicad_sch
  - co2-sensor-adapter.kicad_pcb

- **Purpose:** Adapter board for CO2 sensor with AI-assisted design workflow
- **ESPHome:** Configuration in `ai/.esphome/` directory

**Status:** Active development

**Library Dependencies:**
- Microcontroller: ESP32-WROOM-32
- Connectors: Various headers
- Power: Voltage regulators

### debughub/

Debug interface board for embedded development.

**Description:**
Universal debug hub for microcontroller development and testing.

**Main Board:** `Untitled/`
- Untitled.kicad_pro
- Untitled.kicad_sch
- Untitled.kicad_pcb

**Features:**
- JTAG/SWD interface
- UART connections
- Logic level translation
- Power supply options
- LED indicators

**Status:** In development

**Library Dependencies:**
- Connectors: Debug headers, USB
- Interface ICs: Level shifters
- Power: Regulators

### eurorack-templates/

Eurorack synthesizer module templates (originally from separate repository).

**Description:**
Comprehensive templates for Eurorack modular synthesizer module design.

**Origin:** https://github.com/[original-repo] (git submodule history)

**Contents:**

#### Front Panels
- **1HP** - 1 unit wide panel template
- **2HP** - 2 unit wide panel template
- **4HP** - 4 unit wide panel template
- **8HP** - 8 unit wide panel template
- **10HP** - 10 unit wide panel template
- **12HP** - 12 unit wide panel template

#### Connector Panels
- **12HP** - Standard and 100mm deep variants

#### Main Boards
- **12HP** - Main board template with power connector

**Features:**
- Correct Eurorack dimensions (1HP = 5.08mm)
- Standard mounting hole positions
- Power connector templates (10-pin or 16-pin)
- Front panel component placement guides

**Status:** Template collection

**Library Dependencies:**
- Connectors: Eurorack power connectors, audio jacks (AudioJacks submodule)
- Components: Op-amps, buffers (when populated)

## Using These Projects

### As References

1. Open project in KiCad
2. Review schematic for component usage examples
3. Check PCB layout for best practices
4. Examine bill of materials (BOM)

### As Templates

1. Copy entire project directory
2. Rename all files to your project name
3. Modify schematic and PCB for your needs
4. Update library references if needed

### For Testing

Before committing library changes:

1. Open each project
2. Verify components still load correctly
3. Check for missing footprints or 3D models
4. Run DRC (Design Rules Check)
5. Run ERC (Electrical Rules Check)
6. Fix any issues before committing library changes

## Project Structure

Standard project structure:

```
project-name/
├── project-name.kicad_pro      # Project file
├── project-name.kicad_sch      # Schematic
├── project-name.kicad_pcb      # PCB layout
├── README.md                   # Project documentation
├── bom/                        # Bill of materials
├── gerbers/                    # Manufacturing files
├── datasheets/                 # Project-specific datasheets
└── docs/                       # Assembly instructions, etc.
```

## Library Paths

Projects use relative paths to reference the main library:

**Symbols:**
```
${KIPRJMOD}/../../libraries/symbols/CategoryName.kicad_sym
```

**Footprints:**
```
${KIPRJMOD}/../../libraries/footprints/CategoryName.pretty
```

**3D Models:**
Referenced via `KICAD_PERSONAL_3DMODEL_DIR` environment variable or relative paths.

## Adding New Projects

When adding a new project to this directory:

1. **Create project directory:**
   ```bash
   mkdir projects/new-project
   cd projects/new-project
   ```

2. **Design your project** using libraries from this repository

3. **Configure library paths** to use relative paths when possible:
   - Use `${KIPRJMOD}/../../libraries/...` for portability

4. **Add project documentation:**
   - Create README.md with:
     - Project description
     - Key features
     - Components used
     - Build instructions (if applicable)
     - Status (prototype, tested, production, etc.)

5. **Test thoroughly:**
   - Verify all components load
   - Run DRC/ERC
   - Generate gerbers successfully
   - Test 3D view

6. **Update this README** with project entry

7. **Commit with clear message:**
   ```bash
   git add projects/new-project
   git commit -m "Add new-project: [brief description]"
   ```

## Project Guidelines

### File Organization

- Keep all project files together in one directory
- Use consistent naming (all files named after project)
- Separate manufacturing files (gerbers/) from source files
- Include README for each project

### Library Usage

- Use components from this library when possible
- Document any external library dependencies
- Test that library changes don't break project
- Report issues with library components

### Documentation

Each project should include:

- **README.md** - Overview, features, status
- **Schematic PDF** (exported from KiCad)
- **BOM** - Bill of materials (CSV or Excel)
- **Assembly notes** - Special instructions
- **Photos** - If built, include photos

### Version Control

- Commit working versions frequently
- Tag releases (v1.0, v1.1, etc.)
- Document changes in project README
- Don't commit gerbers to git (generate as needed)
- Don't commit backups or temp files (use .gitignore)

## Common Workflows

### Starting a New Project

1. Copy an existing similar project as template
2. Rename all files
3. Open in KiCad
4. Clear schematic and PCB (keep project settings)
5. Design your circuit

### Updating Library References

If library structure changes:

1. Open project in KiCad
2. **Preferences → Manage Symbol Libraries**
3. Update paths to point to new library locations
4. **Preferences → Manage Footprint Libraries**
5. Update footprint library paths
6. Verify all components still load

### Exporting for Manufacturing

1. Generate Gerbers: **File → Plot**
2. Generate Drill files: **File → Fabrication Outputs → Drill Files**
3. Generate BOM: **Tools → Generate BOM**
4. Export assembly drawings: **File → Plot** (assembly layer)
5. Export Pick & Place: **File → Fabrication Outputs → Component Placement**

## Project Status Legend

- **Prototype** - Initial design, not tested
- **Testing** - Built and under testing
- **Working** - Tested and functional
- **Production** - Proven design, ready for manufacture
- **Archived** - Old project, kept for reference

## Troubleshooting

### Components Missing

- Verify library paths are correct
- Check that library files exist
- Update library references if structure changed
- See [SETUP.md](../docs/SETUP.md) for configuration

### DRC/ERC Errors After Library Update

- Review library changes
- Update footprints if pins changed
- Check for renamed components
- Verify electrical rules still apply

### 3D Models Don't Load

- Set `KICAD_PERSONAL_3DMODEL_DIR` environment variable
- Check 3D model paths in footprints
- Verify 3D model files exist

## Questions?

- See [SETUP.md](../docs/SETUP.md) for KiCad configuration
- See [ORGANIZATION.md](../docs/ORGANIZATION.md) for library structure
- See [CONTRIBUTING.md](../docs/CONTRIBUTING.md) for adding projects
