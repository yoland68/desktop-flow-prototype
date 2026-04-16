# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **UX prototype** for the ComfyUI Desktop installation and onboarding experience on Windows. The prototype is built using HTML/CSS only - **no actual implementation or backend logic is required**. The purpose is to visualize and test the user flow before implementing the actual desktop application.

## Project Structure

```
desktop-2-prototype/
├── index.html                     # Navigation hub for all screens
├── styles/
│   └── common.css                # Shared styles across all screens
└── screens/
    ├── 01-welcome.html           # Initial welcome screen
    ├── 02a-migration-detect.html # Migration detection (optional)
    ├── 02b-migration-config.html # Migration configuration (optional)
    ├── 02-location-models.html   # Combined: Installation directory + model selection
    ├── 04-downloading.html       # Installation progress (3 seconds, packages only)
    └── 05-comfyui.html           # Final ComfyUI main application window
```

**Note:** The old separate files `02-location.html` and `03-models.html` have been replaced by the combined `02-location-models.html` screen.

## Running the Prototype

Simply open `index.html` in any web browser. The navigation page provides links to all screens in the installation flow.

Alternatively, navigate directly to any screen by opening the HTML files in the `screens/` directory.

## Installation Flow

The prototype supports two flow paths depending on whether the user is new or has an existing ComfyUI installation:

### Flow Path A: New Users
1. Welcome → 2a. Migration Detect (choose "Fresh Install") → 3. Location & Models → 4. Installation → 5. Main App

### Flow Path B: Existing Users (Migration)
1. Welcome → 2a. Migration Detect (choose "Migrate & Upgrade") → 2b. Migration Config → 3. Location & Models → 4. Installation → 5. Main App

### Detailed Screen Breakdown

1. **Welcome Screen** (01-welcome.html)
   - Introduces ComfyUI Desktop and its features
   - Entry point for the installation process
   - "Get Started" button leads to migration detection

2a. **Migration Detection** (02a-migration-detect.html) - Optional
   - Detects existing ComfyUI installations automatically
   - Shows detected installation path and version
   - Presents two choices:
     - "Migrate & Upgrade" → leads to migration configuration
     - "Fresh Install" → skips to location selection
   - Reassures users their old installation won't be modified

2b. **Migration Configuration** (02b-migration-config.html) - Optional
   - Only shown if user chooses to migrate
   - Checkboxes to select what to migrate:
     - Models & Checkpoints (~12.4 GB)
     - Workflows & Presets (~45 MB)
     - Generated Images (~3.2 GB)
     - Custom Nodes & Extensions (~156 MB)
     - Settings & Preferences (~2 MB)
   - Live summary showing total size and estimated time
   - JavaScript dynamically updates summary based on selections
   - Note: Files are copied, not moved (original installation remains intact)

3. **Installation Configuration** (02-location-models.html) - Combined Screen
   - **Installation Directory Section:**
     - User selects installation directory for models and data
     - Shows disk space requirements and availability
     - Includes folder browser button (simulated with alert)

   - **Model Selection Section:**
     - Checkboxes for essential and optional models
     - Shows individual model sizes
     - Stable Diffusion 1.5 (4.2 GB), VAE (324 MB), ControlNet (7.8 GB)
     - Prominent notice that models download in background

   - **Live Summary:**
     - Shows application size (~500 MB)
     - Selected model count and total model download size
     - Total required space (app + models)
     - JavaScript dynamically updates all values when checkboxes change

   - **Key UX Message:** Users are informed that model downloads won't block them from using the software

4. **Installation Progress** (04-downloading.html)
   - **Fast 3-second animation** showing package installation only
   - Progress bar animates from 0% to 100% in 3 seconds
   - Status messages cycle through installation steps:
     - Extracting packages
     - Installing dependencies
     - Configuring environment
     - Setting up ComfyUI
     - Finalizing installation
     - Ready to launch
   - **No model download shown** - only application packages
   - Blue notice box explains models will download in background
   - Auto-redirects to main window after completion
   - No detailed download stats (speed, time remaining) shown

5. **ComfyUI Main Window** (05-comfyui.html)
   - Full application interface mockup
   - Node-based workflow editor layout
   - Sidebar with node categories, canvas area, and properties panel
   - Demonstrates the final user experience after installation

## Design System

### Color Scheme
- Primary gradient: `linear-gradient(135deg, #667eea 0%, #764ba2 100%)`
- Dark background: `#1e1e1e` (for main app)
- Light background: `white` (for installer windows)
- Border/divider: `#e0e0e0` or `#1a1a1a` depending on theme

### Typography
- Font family: System default stack (`-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto...`)
- Primary text: `#333` (light theme), `#e0e0e0` (dark theme)
- Secondary text: `#666` or `#b0b0b0`

### Components
- **Installer Window**: 600px wide, centered, white background with rounded corners
- **Main App**: Full viewport, dark theme, three-column layout (sidebar, canvas, properties)
- **Buttons**: Gradient primary buttons, gray secondary buttons
- **Form Inputs**: 2px borders, rounded corners, focus state with primary color

## Key Interactive Elements

### 02b-migration-config.html
Contains JavaScript for dynamic migration summary:
- Checkboxes toggle migration items on/off
- `updateSummary()` function recalculates totals in real-time
- Updates item count, total size (GB), and estimated time
- Provides visual feedback with border highlighting for selected items

### 02-location-models.html
Contains JavaScript for dynamic installation summary:
- Checkboxes toggle model selection on/off
- `updateSummary()` function recalculates all size values in real-time
- Updates: model count, model download size, total required space
- Total space = 500 MB (app) + selected models
- Provides visual feedback with border highlighting for selected models

### 04-downloading.html
Contains JavaScript for fast installation animation:
- **3-second total duration** from 0% to 100%
- Updates every 50ms for smooth animation
- Cycles through 6 installation status messages based on progress
- Auto-enables launch button at 100%
- Auto-redirects to main window 1 second after completion
- **No model download information** - only shows package installation

### Navigation
Each screen includes:
- Forward/back navigation buttons in the flow
- "Back to Navigation" link at the bottom to return to index.html
- Conditional navigation (migration screens are optional based on user choice)

## Making Changes

When modifying the prototype:

1. **Maintain consistency**: Use existing styles from `common.css` whenever possible
2. **Update navigation**: If adding new screens, add them to `index.html` navigation
3. **Follow the flow**: New screens should maintain logical progression in numbering
4. **Keep it static**: This is a prototype - avoid adding complex functionality unless it serves the UX demonstration

## Windows-Specific Considerations

The prototype is designed for Windows users:
- Default installation path uses Windows format: `C:\Users\YourName\ComfyUI`
- File browser interactions are simulated (no actual file system access)
- Progress indicators and animations match Windows desktop app expectations
