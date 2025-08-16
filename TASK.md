# ZMK Configuration Migration Task List

## Overview
This document provides a step-by-step migration plan from zmk-config-fire to zmk-config-v2. Each task represents a minimal, atomic change that should be committed individually for easy rollback if issues arise.

## Prerequisites
- [ ] Set up local development environment: `direnv allow`
- [ ] Initialize workspace: `just init`

---

## Phase 1: Project Setup and Initial Preparation

### Task 1.1: Repository Setup
**Goal**: Initialize git tracking for migration
**Changes**: Ensure git repository is ready for migration commits
```bash
# Ensure clean working directory
# Check git status and commit any pending changes
```
**Commit**: "Initial setup: Prepare repository for migration"

### Task 1.2: Build Environment Setup
**Goal**: Set up local development environment
**Changes**: Initialize Nix environment and workspace
```bash
direnv allow
just init
```
**Commit**: "Setup: Initialize build environment with direnv and just"

### Task 1.3: Build System Verification
**Goal**: Ensure base configuration builds successfully
**Changes**: Test baseline functionality
```bash
just build all
```
**Commit**: "Verify: Confirm baseline zmk-config-v2 builds successfully"

---

## Phase 2: Hardware Configuration Migration

### Task 2.1: Update Corne Configuration
**Goal**: Replace corneish_zen references with corne naming
**Files**: `config/corneish_zen.conf`, `config/corneish_zen.keymap`, `build.yaml`
**Changes**: Rename files and update references from corneish_zen to corne
**Commit**: "Hardware: Rename corneish_zen to corne configuration"

### Task 2.2: Remove Planck Support
**Goal**: Clean up unused hardware configuration
**Files**: `config/planck_rev6.conf`, `config/planck_rev6.keymap`, `build.yaml`
**Changes**: Delete planck files and remove from build targets
**Commit**: "Hardware: Remove planck_rev6 support (unused)"

### Task 2.3: Update Build Targets
**Goal**: Configure build.yaml for correct hardware
**Files**: `build.yaml`
**Changes**: Update to match zmk-config-fire build targets (corne + glove80)
**Commit**: "Build: Update build.yaml targets to match requirements"

### Task 2.4: Phase 2 Build Verification
**Goal**: Ensure hardware configuration changes build successfully
**Changes**: Test build after hardware config changes
```bash
just build all
```
**Commit**: "Test: Verify Phase 2 hardware changes build successfully"

---

## Phase 3: Base Layer Layout Migration

### Task 3.1: Backup Original Layout
**Goal**: Document current layout before changes
**Files**: `config/base.keymap`
**Changes**: Add comment block with original layout
**Commit**: "Layout: Document original base layer before migration"

### Task 3.2: Implement Custom Alpha Layout
**Goal**: Replace QWERTY-style with custom optimized layout
**Files**: `config/base.keymap`
**Changes**: Update base layer alpha keys:
```
B Y O U Z    Q L D W V
C I E A ,    . H T S N
G X J K :    ! R M F P
```
**Commit**: "Layout: Implement custom alpha key layout"

### Task 3.3: Update Key Positions
**Goal**: Ensure key position references match new layout
**Files**: `config/base.keymap`
**Changes**: Update any position-dependent configurations
**Commit**: "Layout: Update key position references for custom layout"

### Task 3.4: Phase 3 Build Verification
**Goal**: Ensure base layout changes build successfully
**Changes**: Test build after layout migration
```bash
just build all
```
**Commit**: "Test: Verify Phase 3 layout changes build successfully"

---

## Phase 4: Home Row Mods Simplification

### Task 4.1: Simplify HRM Timing
**Goal**: Replace complex HRM with simplified 150ms timing
**Files**: `config/base.keymap`
**Changes**: Update HRM behaviors to use consistent timing
**Commit**: "HRM: Simplify home row mods with 150ms timing"

### Task 4.2: Remove Complex Trigger Positions
**Goal**: Simplify HRM trigger logic
**Files**: `config/base.keymap`
**Changes**: Remove nested HRM configurations, use basic hold-preferred
**Commit**: "HRM: Remove complex trigger position logic"

### Task 4.3: Add Specialized HRM Variants
**Goal**: Implement colon/slash and exclamation/question mark HRMs
**Files**: `config/base.keymap`
**Changes**: Add specialized HRM behaviors for symbol keys
**Commit**: "HRM: Add specialized variants for symbol keys"

### Task 4.4: Phase 4 Build Verification
**Goal**: Ensure HRM changes build successfully
**Changes**: Test build after HRM modifications
```bash
just build all
```
**Commit**: "Test: Verify Phase 4 HRM changes build successfully"

---

## Phase 5: Layer Structure Updates

### Task 5.1: Remove Unicode Layer
**Goal**: Clean up unused Unicode functionality
**Files**: `config/base.keymap`
**Changes**: Remove UC layer definition and references
**Commit**: "Layers: Remove Unicode layer (unused)"

### Task 5.2: Keep Mouse Layer
**Goal**: Preserve mouse functionality from v2
**Files**: `config/base.keymap`, `config/mouse.dtsi`
**Changes**: Ensure mouse layer is properly configured and accessible
**Commit**: "Layers: Verify mouse layer functionality preserved"

### Task 5.3: Update Layer Activation Logic
**Goal**: Change layer trigger from FN+NUM→SYS to NAV+NUM→SYS
**Files**: `config/base.keymap`
**Changes**: Update conditional layer triggers
**Commit**: "Layers: Update activation logic (NAV+NUM→SYS)"

### Task 5.4: Phase 5 Build Verification
**Goal**: Ensure layer structure changes build successfully
**Changes**: Test build after layer updates
```bash
just build all
```
**Commit**: "Test: Verify Phase 5 layer changes build successfully"

---

## Phase 6: Combo System Migration

### Task 6.1: Update Combo Timing
**Goal**: Implement conservative combo timing
**Files**: `config/combos.dtsi`
**Changes**: Add COMBO_TERM_HR (15ms) and COMBO_IDLE_HR (200ms)
**Commit**: "Combos: Add conservative timing categories"

### Task 6.2: Restructure Horizontal Combos
**Goal**: Implement custom horizontal combo mappings
**Files**: `config/combos.dtsi`
**Changes**: Update horizontal combos:
- LT3+LT2: ESC with @ morph
- LT2+LT1: Return with double quotes morph
- LT3+LT1: Question mark
**Commit**: "Combos: Restructure horizontal combo mappings"

### Task 6.3: Simplify Vertical Combos
**Goal**: Remove unused vertical combos
**Files**: `config/combos.dtsi`
**Changes**: Comment out or remove unused vertical combo definitions
**Commit**: "Combos: Simplify vertical combo system"

### Task 6.4: Phase 6 Build Verification
**Goal**: Ensure combo system changes build successfully
**Changes**: Test build after combo modifications
```bash
just build all
```
**Commit**: "Test: Verify Phase 6 combo changes build successfully"

---

## Phase 7: Thumb Cluster Redesign

### Task 7.1: Remove Space Morphing
**Goal**: Eliminate complex dot_spc macro
**Files**: `config/base.keymap`
**Changes**: Remove dot_spc macro and related space morphing
**Commit**: "Thumb: Remove complex space morphing behavior"

### Task 7.2: Implement Spotlight Integration
**Goal**: Add macOS Spotlight search on shift+space
**Files**: `config/base.keymap`
**Changes**: Add space + shift → ⌘+Space mapping
**Commit**: "Thumb: Add Spotlight search (⌘+Space) on shift+space"

### Task 7.3: Relocate Control Key
**Goal**: Move Control to thumb cluster
**Files**: `config/base.keymap`
**Changes**: Add Control key to thumb cluster
**Commit**: "Thumb: Move Control key to thumb cluster"

### Task 7.4: Update Return Key Behavior
**Goal**: Add hyper modifier to Return
**Files**: `config/base.keymap`
**Changes**: Combine Return with hyper modifier (⌃⌥⇧⌘+Return)
**Commit**: "Thumb: Add hyper modifier to Return key"

### Task 7.5: Phase 7 Build Verification
**Goal**: Ensure thumb cluster changes build successfully
**Changes**: Test build after thumb cluster redesign
```bash
just build all
```
**Commit**: "Test: Verify Phase 7 thumb cluster changes build successfully"

---

## Phase 8: Navigation Layer Restructuring

### Task 8.1: Add Window Management Shortcuts
**Goal**: Implement macOS window management
**Files**: `config/base.keymap`
**Changes**: Add ⌘⇧2, ⌘⇧3, ⌘⇧4 shortcuts to navigation layer left side
**Commit**: "Navigation: Add window management shortcuts"

### Task 8.2: Relocate Arrow Keys
**Goal**: Move arrows to left side of navigation layer
**Files**: `config/base.keymap`
**Changes**: Relocate Up/Down/Left/Right to left side
**Commit**: "Navigation: Move arrow keys to left side"

### Task 8.3: Add Standard Shortcuts
**Goal**: Implement common macOS shortcuts
**Files**: `config/base.keymap`
**Changes**: Add ⌘Z, ⌘X, ⌘C, ⌘V to navigation layer
**Commit**: "Navigation: Add standard macOS shortcuts"

### Task 8.4: Consolidate Modifiers
**Goal**: Group modifier keys on right side
**Files**: `config/base.keymap`
**Changes**: Consolidate ⌘, ⌃, ⌥, ⇧ on navigation layer right side
**Commit**: "Navigation: Consolidate modifier keys on right side"

### Task 8.5: Phase 8 Build Verification
**Goal**: Ensure navigation layer changes build successfully
**Changes**: Test build after navigation restructuring
```bash
just build all
```
**Commit**: "Test: Verify Phase 8 navigation changes build successfully"

---

## Phase 9: Number Layer Repositioning

### Task 9.1: Move Numbers to Right Side
**Goal**: Relocate number pad from left to right
**Files**: `config/base.keymap`
**Changes**: Reorganize number layout:
```
    7 8 9
    4 5 6 0
    1 2 3
```
**Commit**: "Numbers: Move number pad to right side"

### Task 9.2: Phase 9 Build Verification
**Goal**: Ensure number layer changes build successfully
**Changes**: Test build after number repositioning
```bash
just build all
```
**Commit**: "Test: Verify Phase 9 number changes build successfully"

---

## Phase 10: Symbol Access Strategy

### Task 10.1: Implement Equal/Caret Morph
**Goal**: Add = + Shift → ^ behavior
**Files**: `config/base.keymap`
**Changes**: Add morphing behavior for equal/caret
**Commit**: "Symbols: Add equal/caret morphing behavior"

### Task 10.2: Implement Underscore/Dollar Morph
**Goal**: Add _ + Shift → $ behavior
**Files**: `config/base.keymap`
**Changes**: Add morphing behavior for underscore/dollar
**Commit**: "Symbols: Add underscore/dollar morphing behavior"

### Task 10.3: Implement Pipe/Percent Morph
**Goal**: Add | + Shift → % behavior
**Files**: `config/base.keymap`
**Changes**: Add morphing behavior for pipe/percent
**Commit**: "Symbols: Add pipe/percent morphing behavior"

### Task 10.4: Implement Slash/Colon Morph
**Goal**: Add / + Shift → : behavior
**Files**: `config/base.keymap`
**Changes**: Add morphing behavior for slash/colon
**Commit**: "Symbols: Add slash/colon morphing behavior"

### Task 10.5: Phase 10 Build Verification
**Goal**: Ensure symbol access changes build successfully
**Changes**: Test build after symbol morphing implementation
```bash
just build all
```
**Commit**: "Test: Verify Phase 10 symbol changes build successfully"

---

## Phase 11: Behavioral Modifications

### Task 11.1: Update Swapper Behavior
**Goal**: Change Alt+Tab to Ctrl+Tab
**Files**: `config/base.keymap`
**Changes**: Update swapper from Alt+Tab to Ctrl+Tab
**Commit**: "Swapper: Change Alt+Tab swapper to Ctrl+Tab"

### Task 11.2: Add App Swapper
**Goal**: Implement ⌘+Tab app swapper
**Files**: `config/base.keymap`
**Changes**: Add separate app swapper behavior for ⌘+Tab
**Commit**: "Swapper: Add ⌘+Tab app swapper behavior"

### Task 11.3: Phase 11 Build Verification
**Goal**: Ensure behavioral changes build successfully
**Changes**: Test build after swapper modifications
```bash
just build all
```
**Commit**: "Test: Verify Phase 11 behavioral changes build successfully"

---

## Phase 12: Testing and Validation

### Task 12.1: Build Verification
**Goal**: Ensure configuration compiles successfully
**Changes**: Test build process
```bash
just build all
```
**Commit**: "Test: Verify complete configuration builds successfully"

### Task 12.2: Layer Access Testing
**Goal**: Validate all layers are accessible
**Changes**: Test layer activation and key mappings
**Commit**: "Test: Validate layer access and key mappings"

### Task 12.3: Combo Function Testing
**Goal**: Verify combo behaviors work correctly
**Changes**: Test combo timing and symbol access
**Commit**: "Test: Verify combo behaviors and symbol access"

---

## Phase 13: Final Cleanup

### Task 13.1: Remove Commented Code
**Goal**: Clean up leftover commented sections
**Files**: `config/combos.dtsi`, `config/base.keymap`
**Changes**: Remove commented-out code blocks
**Commit**: "Cleanup: Remove commented code sections"

### Task 13.2: Update Documentation
**Goal**: Document final configuration
**Files**: `readme.md`
**Changes**: Update readme with migration notes and new features
**Commit**: "Docs: Update readme with migration summary"

### Task 13.3: Final Build Test
**Goal**: Confirm everything works end-to-end
**Changes**: Complete build and functionality verification
**Commit**: "Final: Complete migration with full functionality verified"

---

## Migration Notes

### Commit Strategy
- Each task should result in exactly ONE commit
- Commit messages should follow format: "Category: Description"
- Test build after each significant change
- Push commits regularly to avoid losing work

### Testing Protocol
- Run `just build all` after major changes
- Test key functionality before moving to next phase
- Keep notes of any behavior changes or unexpected issues
