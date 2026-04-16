# ComfyUI Desktop - Installation Flow Prototype

A UX prototype demonstrating the Windows desktop installation and onboarding experience for ComfyUI Desktop.

## Quick Start

1. Open `index.html` in your web browser
2. Navigate through the installation flow screens
3. Experience the complete onboarding journey

## Installation Flow

The prototype includes two user paths:

### New Users
1. **Welcome** - Introduction to ComfyUI Desktop
2. **Migration Detection** - Choose "Fresh Install"
3. **Installation Configuration** - Combined screen for installation directory + model selection
4. **Installation Progress** - Fast 3-second installation (packages only, models download in background)
5. **Main Application** - ComfyUI launches immediately, models continue downloading in background

### Existing Users (Migration)
1. **Welcome** - Introduction to ComfyUI Desktop
2. **Migration Detection** - Detects existing installation, choose "Migrate & Upgrade"
3. **Migration Configuration** - Select what to migrate (models, workflows, outputs, custom nodes, settings)
4. **Installation Configuration** - Choose installation directory + additional models
5. **Installation Progress** - Fast 3-second installation
6. **Main Application** - ComfyUI launches with migrated data, additional models download in background

## Key UX Features

- **Combined Configuration Screen**: Installation directory and model selection on one screen with live size calculations
- **Non-Blocking Downloads**: Models download in the background - users can start using ComfyUI immediately
- **Fast Installation**: 3-second installation animation for application packages only
- **Migration Support**: Optional wizard for users upgrading from previous ComfyUI versions

## Technology

- Pure HTML/CSS (no frameworks)
- Minimal JavaScript for progress animation
- Static prototype (no backend implementation)

## Purpose

This prototype is designed to:
- Visualize the user onboarding flow
- Test UX decisions before implementation
- Communicate design intent to stakeholders
- Serve as a reference for desktop app development

## File Structure

```
├── index.html                       # Navigation hub
├── styles/
│   └── common.css                  # Shared styles
├── screens/                        # Individual flow screens
│   ├── 01-welcome.html            # Welcome screen
│   ├── 02a-migration-detect.html  # Migration detection (optional)
│   ├── 02b-migration-config.html  # Migration configuration (optional)
│   ├── 02-location-models.html    # Combined: Installation directory + model selection
│   ├── 04-downloading.html        # Installation progress (3 seconds, packages only)
│   └── 05-comfyui.html            # Main application window
├── CLAUDE.md                       # Claude Code documentation
└── README.md                       # This file
```
