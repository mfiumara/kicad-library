# Development Workflow

This document describes the workflow for developing, testing, and contributing to this KiCad library.

## Overview

This library uses a git-based workflow with standards and validation to ensure quality. Whether you're adding a single component or making major changes, following this workflow ensures consistency and reliability.

## Workflow Steps

### 1. Sync with Latest Changes

Before starting any work, ensure you have the latest version:

```bash
cd /path/to/kicad-library
git checkout main
git pull origin main
git submodule update --init --recursive
```

### 2. Create a Feature Branch (Recommended)

For any non-trivial changes, create a feature branch:

```bash
git checkout -b feature/add-esp32-s3
# or
git checkout -b fix/dac-footprint-courtyard
# or
git checkout -b docs/update-setup-guide
```

**Branch Naming Convention:**
- `feature/description` - New components or functionality
- `fix/description` - Bug fixes, corrections
- `docs/description` - Documentation updates
- `refactor/description` - Code reorganization without functional changes

### 3. Make Your Changes

Follow the guidelines in [CONTRIBUTING.md](CONTRIBUTING.md):

1. Add or modify symbols in appropriate category library
2. Add or modify footprints in corresponding `.pretty` directory
3. Add or update 3D models in corresponding `.3dshapes` directory
4. Add or link datasheets in `libraries/datasheets/`
5. Update category README files

### 4. Test Your Changes

**Critical - Always test before committing!**

#### Symbol Testing

1. Open KiCad Symbol Editor
2. Load your modified symbol library
3. Check for errors in the console/log
4. Verify symbols appear correctly
5. Check all properties are present (Reference, Value, Footprint, Datasheet)

#### Footprint Testing

1. Open KiCad Footprint Editor
2. Load your modified footprint library
3. Check for errors/warnings
4. Verify courtyard, silkscreen, fabrication layers present
5. Check 3D model loads correctly (View → 3D Viewer)
6. Verify pads are correct size and position

#### Integration Testing

**Test in a real project:**

1. Create a test project or use an existing one
2. Add your symbol to schematic
3. Verify footprint auto-assigns correctly
4. Generate netlist and update PCB
5. Check footprint placement on PCB
6. Verify 3D model appears in 3D viewer
7. Run Design Rules Check (DRC)
8. Run Electrical Rules Check (ERC)
9. Fix any errors before committing

### 5. Validate Against Standards

Check your work against KiCad Library Convention:

**Manual Checks:**
- Naming follows conventions (see [NAMING_CONVENTIONS.md](NAMING_CONVENTIONS.md))
- Symbol pins on 100 mil (2.54mm) grid
- Footprint pads match datasheet
- Courtyard present and adequate
- Silkscreen doesn't overlap pads
- Pin 1 indicator present
- All required properties filled

**Automated Validation (if available):**
```bash
# Run KLC validation script (if implemented)
python scripts/validate_klc.py
```

### 6. Update Documentation

**Required documentation updates:**

1. **Category README** - Add component to appropriate category README:
   ```markdown
   ## ESP32-S3-WROOM-1
   - **Category:** Microcontroller
   - **Description:** WiFi & Bluetooth 5 module with ESP32-S3 SoC
   - **Symbol:** Microcontroller.kicad_sym → ESP32-S3-WROOM-1
   - **Footprint:** Microcontroller.pretty/ESP32-S3-WROOM-1.kicad_mod
   - **3D Model:** Microcontroller.3dshapes/ESP32-S3-WROOM-1.step
   - **Datasheet:** [Link](https://www.espressif.com/...)
   ```

2. **Datasheet INDEX** - Add to `libraries/datasheets/CategoryName/INDEX.md`

3. **Main README** (if adding new category or major feature)

### 7. Commit Your Changes

**Commit Message Format:**

Use clear, descriptive commit messages following this format:

```
<type>: <subject>

<body>

<footer>
```

**Types:**
- `feat` - New component or feature
- `fix` - Bug fix or correction
- `docs` - Documentation changes
- `refactor` - Code reorganization
- `test` - Test additions or changes
- `chore` - Maintenance tasks

**Examples:**

```
feat: Add ESP32-S3-WROOM-1 to Microcontroller library

- Added symbol with full 44-pin configuration
- Created SMD footprint with correct pad dimensions
- Included STEP 3D model from Espressif
- Linked to manufacturer datasheet

Tested in: wifi-mesh-node project
```

```
fix: Correct courtyard on DAC80508 footprint

The courtyard was too small (0.1mm clearance). Updated to
KLC-compliant 0.25mm minimum clearance.

Fixes #42
```

```
docs: Update SETUP.md with Windows path examples

Added Windows-specific path examples for environment variables
to help Windows users configure the library.
```

**Commit Best Practices:**
- Make atomic commits (one logical change per commit)
- Write clear, descriptive messages
- Reference issue numbers when applicable (#42, #123)
- Use present tense ("Add" not "Added")
- Keep subject line under 50 characters
- Wrap body at 72 characters

### 8. Push Changes

**For feature branches:**

```bash
git push origin feature/add-esp32-s3
```

**For direct commits to main** (only for minor changes):

```bash
git push origin main
```

### 9. Create Pull Request (Optional)

If working in a team or contributing to a shared repository:

1. Push your feature branch to the remote
2. Create a Pull Request on GitHub/GitLab
3. Fill out the PR template with:
   - Description of changes
   - Testing performed
   - Related issues
   - Screenshots (if applicable)
4. Request review from maintainers
5. Address feedback and make revisions
6. Wait for approval and merge

### 10. Merge and Cleanup

After your changes are merged:

```bash
# Switch back to main
git checkout main

# Pull latest changes
git pull origin main

# Delete local feature branch
git branch -d feature/add-esp32-s3

# Delete remote feature branch (if applicable)
git push origin --delete feature/add-esp32-s3
```

## Project Testing Workflow

When testing library changes with projects:

### Using Projects in This Repository

The `projects/` directory contains reference designs that use this library:

1. **Before making library changes:**
   - Open a project in `projects/`
   - Verify it loads without errors
   - Note which components it uses

2. **After making library changes:**
   - Re-open the same project
   - Verify symbols/footprints still load correctly
   - Check for any missing components or errors
   - Run DRC/ERC to ensure no new issues

### Using External Projects

For your own projects:

1. Configure library paths to point to your development library
2. Make library changes
3. Test in your project
4. Once validated, commit changes

## Submodule Workflow

For external libraries managed as submodules (e.g., AudioJacks):

### Updating a Submodule

```bash
# Navigate to submodule directory
cd submodules/AudioJacks

# Pull latest changes from upstream
git fetch origin
git checkout main
git pull origin main

# Return to main repository
cd ../..

# Commit the submodule update
git add submodules/AudioJacks
git commit -m "chore: Update AudioJacks submodule to latest version"
git push
```

### Contributing to Submodule Upstream

1. Make changes in the submodule directory
2. Commit within the submodule
3. Push to your fork of the submodule repository
4. Create a Pull Request to the upstream submodule repository
5. After merge, update the submodule reference in this repository

## Release Workflow

For creating versioned releases:

### 1. Prepare Release

1. Ensure all tests pass
2. Update version numbers (if applicable)
3. Update CHANGELOG.md
4. Tag the release:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

### 2. Create Release Notes

On GitHub/GitLab, create a release from the tag with:
- Summary of changes
- New components added
- Bug fixes
- Breaking changes (if any)
- Upgrade instructions

### 3. Notify Users

If others use this library, notify them of the new release.

## Troubleshooting Workflow Issues

### Merge Conflicts

If you encounter merge conflicts:

```bash
# Update your branch with latest main
git checkout feature/your-branch
git fetch origin
git merge origin/main

# Resolve conflicts in your editor
# For .kicad_sym files, be careful with merging - may need manual review

# After resolving
git add .
git commit -m "Merge main into feature branch"
```

### Accidental Changes

To discard uncommitted changes:

```bash
# Discard all changes
git reset --hard HEAD

# Discard changes to specific file
git checkout -- path/to/file
```

### Undo Last Commit (Not Pushed)

```bash
# Keep changes but undo commit
git reset --soft HEAD~1

# Discard changes and undo commit
git reset --hard HEAD~1
```

## Best Practices

### Do's ✓

- Always test in a real project before committing
- Write clear, descriptive commit messages
- Update documentation with your changes
- Follow naming conventions consistently
- Run validation checks before committing
- Keep commits focused and atomic
- Use feature branches for non-trivial changes

### Don'ts ✗

- Don't commit untested changes
- Don't skip documentation updates
- Don't make sweeping changes without discussion
- Don't commit generated or temporary files
- Don't force push to main branch
- Don't commit broken symbols/footprints
- Don't ignore KLC standards

## Quick Reference

### Common Commands

```bash
# Check status
git status

# View changes
git diff

# Stage changes
git add path/to/file

# Commit
git commit -m "message"

# Push
git push origin branch-name

# Create branch
git checkout -b branch-name

# Switch branches
git checkout branch-name

# Update submodules
git submodule update --init --recursive

# View commit history
git log --oneline --graph

# Undo uncommitted changes
git checkout -- path/to/file
```

### File Locations Quick Reference

- **Symbols:** `libraries/symbols/CategoryName.kicad_sym`
- **Footprints:** `libraries/footprints/CategoryName.pretty/FootprintName.kicad_mod`
- **3D Models:** `libraries/3dmodels/CategoryName.3dshapes/ModelName.step`
- **Datasheets:** `libraries/datasheets/CategoryName/PartSeries/`
- **Documentation:** `docs/`
- **Projects:** `projects/`
- **Templates:** `templates/`

## Questions?

- See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines
- See [SETUP.md](SETUP.md) for library configuration
- See [ORGANIZATION.md](ORGANIZATION.md) for structure details
