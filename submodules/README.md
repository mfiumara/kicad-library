# Submodules

This directory contains external KiCad libraries managed as git submodules. Submodules allow us to include third-party libraries while maintaining their connection to upstream repositories for updates.

## Active Submodules

### AudioJacks

- **Repository:** https://github.com/clacktronics/AudioJacks
- **Purpose:** Comprehensive audio jack connector library for synthesizer and audio hardware projects
- **Maintainer:** clacktronics
- **License:** Check submodule repository for license information

**Contents:**
- **Footprints:** 8 audio jack footprints (AudioJacks.pretty/)
  - Various QingPu models (PJ301, PJ302, PJ398, PJ3410, PJ366)
  - Cliff FCR1281 6.35mm jack
  - Both standard and knurled nut variants

- **3D Models:** 22 detailed 3D models (AudioJacks.3dshapes/)
  - STEP format models
  - Variations with different nut styles (knurled, hex)

- **Documentation:**
  - README.md - Usage guide
  - DATA.md - Detailed connector specifications
  - CONTRIBUTE.md - Contribution guidelines
  - TODO.md - Planned improvements

**Typical Use Cases:**
- Eurorack synthesizer modules
- Audio equipment
- Modular synthesizers
- Audio interfaces
- Music hardware projects

## Initializing Submodules

When cloning this repository for the first time, initialize submodules:

```bash
git clone <your-repo-url>
cd kicad-library
git submodule update --init --recursive
```

Or clone with submodules in one step:

```bash
git clone --recursive <your-repo-url>
```

## Using Submodule Libraries in KiCad

### Footprints

Add to your footprint library table (fp-lib-table):

**Global Library Table:**
```
(lib (name "AudioJacks") (type "KiCad") (uri "${KIPRJMOD}/../submodules/AudioJacks/AudioJacks.pretty") (options "") (descr "Audio jack connectors"))
```

Or use absolute path with custom environment variable:
```
(lib (name "AudioJacks") (type "KiCad") (uri "${KICAD_SUBMODULES_DIR}/AudioJacks/AudioJacks.pretty") (options "") (descr "Audio jack connectors"))
```

### 3D Models

3D models are automatically loaded if you've set up the library paths correctly. The AudioJacks footprints reference models using:
```
${KIPRJMOD}/../submodules/AudioJacks/AudioJacks.3dshapes/ModelName.step
```

## Updating Submodules

### Update to Latest Version

To update a submodule to the latest version from upstream:

```bash
cd submodules/AudioJacks
git fetch origin
git checkout main  # or master, depending on submodule
git pull origin main

cd ../..
git add submodules/AudioJacks
git commit -m "chore: Update AudioJacks submodule to latest version"
```

### Update All Submodules

```bash
git submodule update --remote --recursive
git add .
git commit -m "chore: Update all submodules to latest versions"
```

## Contributing to Submodules

To contribute improvements to a submodule:

1. **Fork the upstream repository** (e.g., fork AudioJacks on GitHub)

2. **Update submodule to point to your fork:**
   ```bash
   cd submodules/AudioJacks
   git remote add myfork https://github.com/yourusername/AudioJacks.git
   ```

3. **Make changes in the submodule:**
   ```bash
   cd submodules/AudioJacks
   git checkout -b feature/my-improvement
   # Make your changes
   git add .
   git commit -m "Add new audio jack variant"
   git push myfork feature/my-improvement
   ```

4. **Create pull request** to the upstream repository

5. **After merge, update submodule reference:**
   ```bash
   cd submodules/AudioJacks
   git checkout main
   git pull origin main
   cd ../..
   git add submodules/AudioJacks
   git commit -m "Update AudioJacks submodule after upstream merge"
   ```

## Adding New Submodules

To add a new external library as a submodule:

1. **Add the submodule:**
   ```bash
   git submodule add https://github.com/author/library.git submodules/LibraryName
   ```

2. **Initialize and update:**
   ```bash
   git submodule update --init --recursive
   ```

3. **Commit the changes:**
   ```bash
   git add .gitmodules submodules/LibraryName
   git commit -m "Add LibraryName submodule"
   ```

4. **Update this README** with submodule information

## Removing Submodules

If you need to remove a submodule:

1. **Remove from .gitmodules:**
   ```bash
   git config -f .gitmodules --remove-section submodule.submodules/SubmoduleName
   ```

2. **Remove from .git/config:**
   ```bash
   git config --remove-section submodule.submodules/SubmoduleName
   ```

3. **Remove from working tree:**
   ```bash
   git rm --cached submodules/SubmoduleName
   rm -rf submodules/SubmoduleName
   ```

4. **Remove from .git/modules:**
   ```bash
   rm -rf .git/modules/submodules/SubmoduleName
   ```

5. **Commit the changes:**
   ```bash
   git commit -m "Remove SubmoduleName submodule"
   ```

## Submodule vs. Direct Integration

### When to Use Submodules ✓

- External library with active upstream development
- Want to receive updates from original maintainer
- Library is useful across multiple projects
- Want to contribute back to upstream
- License requires attribution to original source

### When to Integrate Directly ✗

- Library is abandoned/unmaintained
- Need extensive modifications specific to your use
- Small, simple library that won't change
- Want complete control over all library content

## Troubleshooting

### Submodule Directory is Empty

```bash
git submodule update --init --recursive
```

### Detached HEAD State

Submodules checkout specific commits, not branches. This is normal. To work on a branch:

```bash
cd submodules/AudioJacks
git checkout main  # or appropriate branch
```

### Merge Conflicts in Submodules

```bash
# Update submodule to latest
cd submodules/AudioJacks
git pull origin main

# Return to main repo and commit
cd ../..
git add submodules/AudioJacks
git commit -m "Update submodule and resolve conflict"
```

### Submodule Changes Not Committing

Submodule changes must be committed **inside the submodule**, then the submodule reference updated in the parent repository:

```bash
# Commit in submodule
cd submodules/AudioJacks
git add .
git commit -m "Make changes"
git push

# Update reference in parent
cd ../..
git add submodules/AudioJacks
git commit -m "Update submodule reference"
```

## Best Practices

### Do's ✓

- Initialize submodules immediately after cloning
- Update submodules periodically to get latest fixes
- Document submodule purpose and usage
- Contribute improvements back to upstream
- Test after updating submodules
- Commit submodule updates with clear messages

### Don'ts ✗

- Don't modify submodule content without committing in submodule
- Don't ignore submodule updates indefinitely
- Don't add large submodules (>100MB) without consideration
- Don't remove attribution/license from submodule content
- Don't commit broken submodule references

## Alternative: Submodules vs. Direct Copy

### Submodules (Current Approach)

**Pros:**
- Stay up-to-date with upstream
- Maintain connection to original source
- Easy to contribute back
- Clear attribution

**Cons:**
- Extra steps to initialize
- Can be confusing for beginners
- Requires git submodule commands

### Direct Copy (Alternative)

**Pros:**
- Simpler to use (just clone and go)
- No submodule management needed
- Full control over content

**Cons:**
- No automatic updates from upstream
- Harder to contribute back
- Must manually track changes
- Can lose connection to source

## Questions?

- See [WORKFLOW.md](../docs/WORKFLOW.md) for git workflow
- See [ORGANIZATION.md](../docs/ORGANIZATION.md) for library structure
- See submodule repositories for submodule-specific questions
