# 3D Model Libraries

This directory contains 3D models for PCB components, organized by category to match symbol and footprint libraries.

## Library Directories

### Microcontroller.3dshapes/

3D models for microcontroller modules and development boards.

**Models:**

#### Espressif ESP32 Family (33 models)
- ESP32-WROOM variants (.step, .wrl formats)
- ESP32-PICO variants
- ESP32-MINI variants
- ESP32-C3 modules
- ESP32-S2 modules
- ESP32-S3 modules
- ESP8685 modules
- Development board models

#### Raspberry Pi
- **Raspberrypi_pico2_W.step** - Complete Pico 2 W board model

**Total:** 34 models

### RF_Wireless.3dshapes/

3D models for wireless communication modules.

**Models:**

- **NRF5340-QKAA-R7.step** - Nordic nRF5340 IC package

**Total:** 1 model

### Connectors.3dshapes/

3D models for connectors and interface components.

**Models:**

- **RE130F-41-175F-12P.stp** - 12-pin relay connector

**Note:** Additional audio jack models available via AudioJacks submodule in `submodules/AudioJacks/AudioJacks.3dshapes/` (22 models)

**Total:** 1 model (+ 22 in AudioJacks submodule)

### Analog.3dshapes/

3D models for analog ICs.

**Models:**

- **DAC80508ZRTER.step** - TI 8-channel DAC in QFN package

**Total:** 1 model

## 3D Model Formats

### STEP (.step, .stp)

**Preferred format** - Industry standard for mechanical CAD:
- Accurate geometry
- Material/color information
- Universal compatibility
- Best for design verification and mechanical integration
- Larger file sizes but more detailed

### VRML (.wrl)

**Legacy format** - Older 3D format:
- Smaller file sizes
- Good compatibility with older KiCad versions
- Basic geometry and colors
- Sufficient for visualization

### Recommendation

Use **STEP format** (.step or .stp) whenever possible for maximum accuracy and compatibility.

## Using 3D Models

### Automatic Loading

3D models are automatically linked from footprints using environment variables:

```
${KICAD_PERSONAL_3DMODEL_DIR}/CategoryName.3dshapes/ModelName.step
```

### Manual Configuration

If a 3D model doesn't load:

1. Open Footprint Editor
2. Select the footprint
3. **Footprint Properties → 3D Settings**
4. Click **Add 3D Shape**
5. Browse to: `${KICAD_PERSONAL_3DMODEL_DIR}/CategoryName.3dshapes/ModelName.step`
6. Adjust offset, scale, rotation if needed
7. Verify in 3D Viewer

### Environment Variable Setup

In KiCad, **Preferences → Configure Paths**:

```
KICAD_PERSONAL_3DMODEL_DIR = /path/to/kicad-library/libraries/3dmodels
```

## 3D Model Standards

All 3D models in this library follow these standards:

### Dimensions
- **Units:** Millimeters
- **Scale:** 1:1 (real-world size)
- **Accuracy:** ±5% of datasheet dimensions

### Positioning
- **Origin:** Pin 1 or geometric center (matches footprint anchor)
- **Orientation:** Aligned with footprint coordinate system
- **Height:** Component sitting on PCB surface (Z=0)

### Geometry
- **Detail Level:** Enough for visualization, not every minor feature
- **Simplified:** Keep file size reasonable (< 1MB preferred)
- **Key Features:** Major body, pins, connectors visible

### Materials/Colors
- **IC Bodies:** Black or dark gray plastic
- **Pins:** Gold/brass metallic
- **PCBs:** Green soldermask, copper pads
- **Connectors:** Appropriate colors (black plastic, metal pins)

## 3D Model Sources

### Official Manufacturer Models
- **Espressif:** [ESP32 Resources](https://www.espressif.com/en/support/download/documents)
- **Nordic:** [nRF5340 Resources](https://www.nordicsemi.com/Products/nRF5340)
- **Texas Instruments:** [Product Pages](https://www.ti.com/) - Many include STEP models
- **Raspberry Pi:** [RP2040 Resources](https://www.raspberrypi.com/documentation/microcontrollers/)

### Community Resources
- **GrabCAD:** [grabcad.com](https://grabcad.com/library) - Large community library
- **3D ContentCentral:** [3dcontentcentral.com](https://www.3dcontentcentral.com/) - Manufacturer-submitted models
- **SnapEDA:** [snapeda.com](https://www.snapeda.com/) - PCB library with 3D models
- **UltraLibrarian:** [ultralibrarian.com](https://www.ultralibrarian.com/) - Component library

### Creating Your Own
Use CAD software to create models:
- **FreeCAD:** Open-source parametric CAD
- **Fusion 360:** Free for hobbyists
- **OpenSCAD:** Script-based CAD
- **Blender:** General 3D modeling (export to STEP)

## Model Details

### ESP32-WROOM-32.step

- **Dimensions:** 18mm × 25.5mm × 3.1mm
- **Format:** STEP
- **Features:** Complete module with antenna, shield, pins
- **Origin:** Pin 1 corner
- **Source:** Espressif official resources

### Raspberrypi_pico2_W.step

- **Dimensions:** 21mm × 51mm
- **Format:** STEP
- **Features:** Complete Pico 2 W board with RP2040, flash, wireless, USB, pins
- **Origin:** Bottom-left mounting hole
- **Source:** Community model

### NRF5340-QKAA-R7.step

- **Dimensions:** IC package per Nordic specifications
- **Format:** STEP
- **Features:** QFN package outline, pins
- **Origin:** Pin 1
- **Source:** Nordic official

### DAC80508ZRTER.step

- **Package:** QFN-17 (3mm × 3mm)
- **Format:** STEP
- **Features:** IC body, pins, thermal pad
- **Origin:** Pin 1
- **Source:** TI resources or created from datasheet

## Adding New 3D Models

### 1. Obtain Model

- Download from manufacturer
- Find on GrabCAD/3D ContentCentral
- Create using CAD software from datasheet dimensions

### 2. Verify Model

- Open in CAD software or KiCad 3D viewer
- Check dimensions match datasheet
- Verify origin point (pin 1 or center)
- Check orientation (top view, correct rotation)

### 3. Convert Format

If model is not in STEP format:
- Convert to STEP using CAD software (FreeCAD, Fusion 360, etc.)
- Ensure units are millimeters
- Preserve materials/colors if possible

### 4. Optimize File Size

- Simplify geometry (remove tiny features)
- Reduce polygon count if needed
- Target < 1MB per model when possible

### 5. Add to Library

1. Place file in appropriate category directory:
   ```
   libraries/3dmodels/CategoryName.3dshapes/ComponentName.step
   ```

2. Name file to match footprint: `FootprintName.step`

3. Link from footprint:
   - Open footprint in Footprint Editor
   - **Footprint Properties → 3D Settings → Add 3D Shape**
   - Path: `${KICAD_PERSONAL_3DMODEL_DIR}/CategoryName.3dshapes/ComponentName.step`

4. Adjust positioning if needed:
   - Offset: Move model in X, Y, Z
   - Scale: Usually 1, 1, 1 (if model is in mm)
   - Rotate: Align with footprint orientation

5. Test in 3D Viewer (View → 3D Viewer)

6. Update this README with model info

See [CONTRIBUTING.md](../../docs/CONTRIBUTING.md) for detailed workflow.

## Troubleshooting

### Model Doesn't Load

- Verify environment variable is set: `KICAD_PERSONAL_3DMODEL_DIR`
- Check file path in footprint properties
- Ensure file exists and has correct permissions
- Restart KiCad after setting environment variables

### Model Appears Incorrectly

- **Upside down:** Adjust rotation (180° around X or Y axis)
- **Wrong position:** Adjust offset in footprint 3D settings
- **Wrong size:** Check scale (should be 1, 1, 1 for mm models)
- **Missing features:** Model may be simplified - find more detailed version

### Model Too Large (File Size)

- Simplify geometry using CAD software
- Remove internal features not visible externally
- Consider switching from STL to STEP (better compression)
- For very complex assemblies, create simplified version

## Best Practices

### Do's ✓

- Use STEP format when available
- Verify dimensions against datasheet
- Set origin at pin 1 or geometric center
- Use millimeters as units
- Keep file sizes reasonable (< 1MB)
- Include key visual features
- Test in KiCad 3D viewer before committing

### Don'ts ✗

- Don't use excessive polygon counts
- Don't include internal circuitry (not visible)
- Don't use arbitrary origin points
- Don't mix units (always mm)
- Don't skip verification against datasheet
- Don't commit broken or misaligned models

## Library Statistics

- **Microcontroller.3dshapes** - 34 models
- **RF_Wireless.3dshapes** - 1 model
- **Connectors.3dshapes** - 1 model
- **Analog.3dshapes** - 1 model

**Total:** 37 models (+ 22 in AudioJacks submodule)

## Questions?

- See [ORGANIZATION.md](../../docs/ORGANIZATION.md) for library structure
- See [CONTRIBUTING.md](../../docs/CONTRIBUTING.md) for adding models
- See [KLC_COMPLIANCE.md](../../docs/KLC_COMPLIANCE.md) for 3D model standards
