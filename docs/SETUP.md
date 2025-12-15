# KiCad Library Setup Guide

This guide will help you configure KiCad to use this custom library repository.

## Prerequisites

- KiCad 7.0 or later installed
- Git installed on your system
- This repository cloned to your local machine

## Quick Start

### 1. Clone the Repository

```bash
git clone <your-repo-url> ~/kicad-library
cd ~/kicad-library
```

### 2. Initialize Submodules

This repository uses git submodules for external libraries (e.g., AudioJacks):

```bash
git submodule update --init --recursive
```

### 3. Configure Environment Variables in KiCad

Open KiCad and navigate to: **Preferences → Configure Paths**

Add or update the following environment variables:

| Variable Name | Path Value | Description |
|---|---|---|
| `KICAD_PERSONAL_SYMBOL_DIR` | `/path/to/kicad-library/libraries/symbols` | Symbol library directory |
| `KICAD_PERSONAL_FOOTPRINT_DIR` | `/path/to/kicad-library/libraries/footprints` | Footprint library directory |
| `KICAD_PERSONAL_3DMODEL_DIR` | `/path/to/kicad-library/libraries/3dmodels` | 3D model directory |
| `KICAD_PERSONAL_DATASHEET_DIR` | `/path/to/kicad-library/libraries/datasheets` | Datasheet directory |
| `KICAD_PROJECTS_DIR` | `/path/to/kicad-library/projects` | Projects directory |
| `KICAD_TEMPLATES_DIR` | `/path/to/kicad-library/templates` | Templates directory |

**Note:** Replace `/path/to/kicad-library` with the actual absolute path to your cloned repository.

**macOS Example:**
```
KICAD_PERSONAL_SYMBOL_DIR = /Users/username/repos/kicad/libraries/symbols
```

**Linux Example:**
```
KICAD_PERSONAL_SYMBOL_DIR = /home/username/repos/kicad/libraries/symbols
```

**Windows Example:**
```
KICAD_PERSONAL_SYMBOL_DIR = C:\Users\username\repos\kicad\libraries\symbols
```

### 4. Add Symbol Libraries

Navigate to: **Preferences → Manage Symbol Libraries**

#### Global Symbol Libraries (recommended)

Click the **Global Libraries** tab, then click the folder icon (Add existing library) and add:

| Nickname | Library Path | Description |
|---|---|---|
| `Microcontroller` | `${KICAD_PERSONAL_SYMBOL_DIR}/Microcontroller.kicad_sym` | ESP32, RP2040, etc. |
| `RF_Wireless` | `${KICAD_PERSONAL_SYMBOL_DIR}/RF_Wireless.kicad_sym` | NRF5340, wireless modules |
| `Connectors` | `${KICAD_PERSONAL_SYMBOL_DIR}/Connectors.kicad_sym` | Connectors and headers |
| `Analog` | `${KICAD_PERSONAL_SYMBOL_DIR}/Analog.kicad_sym` | DACs, ADCs, analog ICs |

#### Project-Specific Libraries (alternative)

For project-specific libraries, use the **Project Specific Libraries** tab and use relative paths:
```
${KIPRJMOD}/../libraries/symbols/Microcontroller.kicad_sym
```

### 5. Add Footprint Libraries

Navigate to: **Preferences → Manage Footprint Libraries**

#### Global Footprint Libraries (recommended)

Click the **Global Libraries** tab, then add:

| Nickname | Library Path | Library Format | Description |
|---|---|---|---|
| `Microcontroller` | `${KICAD_PERSONAL_FOOTPRINT_DIR}/Microcontroller.pretty` | KiCad | ESP32, RP2040 footprints |
| `RF_Wireless` | `${KICAD_PERSONAL_FOOTPRINT_DIR}/RF_Wireless.pretty` | KiCad | NRF5340, wireless modules |
| `Connectors` | `${KICAD_PERSONAL_FOOTPRINT_DIR}/Connectors.pretty` | KiCad | Connector footprints |
| `Analog` | `${KICAD_PERSONAL_FOOTPRINT_DIR}/Analog.pretty` | KiCad | Analog IC footprints |
| `AudioJacks` | `${KIPRJMOD}/../submodules/AudioJacks/AudioJacks.pretty` | KiCad | Audio jack connectors |

### 6. Configure 3D Model Paths

3D models should automatically resolve if you've set `KICAD_PERSONAL_3DMODEL_DIR` correctly. Footprints reference 3D models using relative paths within the library structure.

If 3D models don't appear:
1. Open the footprint editor
2. Select a footprint
3. Go to **Footprint Properties → 3D Settings**
4. Verify the path uses the correct environment variable: `${KICAD_PERSONAL_3DMODEL_DIR}/...`

### 7. Install Templates (Optional)

To use the schematic and PCB templates:

1. Copy or symlink the templates directory:
   ```bash
   ln -s /path/to/kicad-library/templates ~/KiCad/templates
   ```

2. In KiCad, navigate to: **Preferences → Configure Paths**
3. Verify `KICAD_TEMPLATE_DIR` points to your templates directory

4. When creating a new project, you can now select from available templates

## Verification

### Test Symbol Libraries

1. Open the Symbol Editor (Tools → Symbol Editor)
2. In the library tree, verify you see: Microcontroller, RF_Wireless, Connectors, Analog
3. Open each library and spot-check symbols load correctly

### Test Footprint Libraries

1. Open the Footprint Editor (Tools → Footprint Editor)
2. In the library tree, verify you see all footprint libraries
3. Open a footprint and verify the 3D model appears in the 3D viewer

### Test in a Project

1. Create a new project or open an existing one
2. Open the schematic editor
3. Press 'A' to add a symbol
4. Search for a component from your custom libraries (e.g., "ESP32")
5. Verify the symbol appears and can be placed

## Troubleshooting

### Libraries Don't Appear

- Verify environment variables are set correctly in **Preferences → Configure Paths**
- Check that paths use absolute paths or correct environment variables
- Restart KiCad after adding environment variables

### 3D Models Don't Load

- Verify `KICAD_PERSONAL_3DMODEL_DIR` is set correctly
- Open footprint properties and check the 3D model path
- Ensure 3D model files exist in the correct directory

### Submodules Not Initialized

If the AudioJacks library is empty:
```bash
cd /path/to/kicad-library
git submodule update --init --recursive
```

### Symbols Load But Footprints Missing

- Verify footprint libraries are added to the footprint library table
- Check footprint library paths use `.pretty` extension
- Ensure footprint library format is set to "KiCad"

## Updating the Library

To update your library to the latest version:

```bash
cd /path/to/kicad-library
git pull origin main
git submodule update --recursive
```

## Using Relative Paths for Portable Projects

For projects that need to be portable across different computers, use relative paths in your project-specific library tables:

**sym-lib-table:**
```
(lib (name "Microcontroller") (type "KiCad") (uri "${KIPRJMOD}/../libraries/symbols/Microcontroller.kicad_sym") (options "") (descr ""))
```

**fp-lib-table:**
```
(lib (name "Microcontroller") (type "KiCad") (uri "${KIPRJMOD}/../libraries/footprints/Microcontroller.pretty") (options "") (descr ""))
```

Where `${KIPRJMOD}` is the absolute path to your project directory (set automatically by KiCad).

## Next Steps

- Read [ORGANIZATION.md](ORGANIZATION.md) to understand the library structure
- See [CONTRIBUTING.md](CONTRIBUTING.md) to learn how to add new components
- Check [NAMING_CONVENTIONS.md](NAMING_CONVENTIONS.md) for component naming guidelines
