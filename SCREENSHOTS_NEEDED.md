# Screenshots Needed for SPDCalc Documentation

This document lists all screenshot placeholders referenced in the documentation. These images need to be captured from the live SPDCalc web application.

**Total placeholders: 49**

## Interface Screenshots (15)

Screenshots of the main interface, toolbar, and UI controls:

- [ ] `interface/auto-update-disabled.png` - Panel with auto-update disabled (lock icon)
- [ ] `interface/auto-update-enabled.png` - Panel with auto-update enabled (unlock icon)
- [ ] `interface/main-window-overview.png` - Full SPDCalc interface showing three main areas
- [ ] `interface/manual-refresh-button.png` - Refresh button on panel toolbar
- [ ] `interface/multi-core-diagram.png` - Diagram showing multi-threaded computation
- [ ] `interface/options-menu.png` - Options menu (hamburger icon in toolbar)
- [ ] `interface/panel-close-button.png` - Close button on panel
- [ ] `interface/panel-loader-card.png` - Empty panel loader card
- [ ] `interface/panel-loader.png` - Panel loader with available panel types
- [ ] `interface/panel-menu-open.png` - Panel type selection menu
- [ ] `interface/panel-toolbar-controls.png` - Panel toolbar controls close-up
- [ ] `interface/progress-spinner.png` - Calculation progress spinner
- [ ] `interface/settings-drawer-expanded.png` - Settings drawer showing all sections
- [ ] `interface/status-bar.png` - Status bar during calculation
- [ ] `interface/toolbar-overview.png` - Top toolbar with all elements

## Panel Screenshots (9)

Screenshots of each calculation panel type showing typical output:

- [ ] `panels/heralding-calculator.png` - Heralding Calculator panel
- [ ] `panels/heralding-efficiency.png` - Heralding Efficiency Analysis panel
- [ ] `panels/hom-dip.png` - Hong-Ou-Mandel Dip panel
- [ ] `panels/info-panel.png` - Info Panel showing poling domain data
- [ ] `panels/jsi-plot-example.png` - Example JSI plot with visible features
- [ ] `panels/jsi-plot.png` - Joint Spectrum Intensity plot panel
- [ ] `panels/phasematching-curves.png` - Phasematching Curves panel
- [ ] `panels/schmidt-number.png` - Schmidt Number Analysis panel
- [ ] `panels/two-source-hom.png` - Two-Source HOM Dip panel

## Preset Management Screenshots (8)

Screenshots of the preset system:

- [ ] `presets/create-preset-button.png` - Save/create preset button
- [ ] `presets/dirty-state-indicator.png` - Dirty state indicator (orange/yellow save button)
- [ ] `presets/preset-delete-icon.png` - Delete preset icon/button
- [ ] `presets/preset-dropdown.png` - Preset selection dropdown
- [ ] `presets/preset-edit-icon.png` - Edit preset icon (pencil)
- [ ] `presets/preset-name-entry.png` - Preset name entry field
- [ ] `presets/preset-rename-field.png` - Rename preset field
- [ ] `presets/save-preset-button.png` - Save preset button

## Reference Diagrams (3)

Diagrams explaining phasematching types:

- [ ] `reference/phasematching-type-0.png` - Type 0 phasematching diagram
- [ ] `reference/phasematching-type-1.png` - Type 1 phasematching diagram
- [ ] `reference/phasematching-type-2.png` - Type 2 phasematching diagram

## Results and Visualization Screenshots (5)

Screenshots showing data interpretation and export:

- [ ] `results/colormap-intensity.png` - Intensity colormap example
- [ ] `results/colormap-phase.png` - Phase colormap example
- [ ] `results/export-menu-location.png` - Export menu location in panel
- [ ] `results/log-scale-comparison.png` - Logarithmic scale comparison
- [ ] `results/plotly-camera-icon.png` - Plotly camera icon for PNG export

## Settings Screenshots (6)

Screenshots of all settings panels:

- [ ] `settings/auto-calculation-controls.png` - Auto-calculation toggle controls
- [ ] `settings/crystal-settings-panel.png` - Crystal Settings tab
- [ ] `settings/integration-settings-panel.png` - Integration Settings tab
- [ ] `settings/periodic-poling-panel.png` - Periodic Poling Settings tab
- [ ] `settings/pump-configuration-panel.png` - Pump Configuration tab
- [ ] `settings/signal-configuration-panel.png` - Signal Configuration tab

## Sharing Screenshots (3)

Screenshots of import/export and URL sharing:

- [ ] `sharing/export-dialog.png` - Export settings dialog
- [ ] `sharing/import-dialog.png` - Import settings dialog
- [ ] `sharing/url-bar-encoded-state.png` - Browser URL bar showing encoded state

## Notes for Screenshot Capture

- All screenshots should be captured at high resolution (at least 1920x1080 display)
- Use consistent browser zoom level (100%)
- Capture screenshots with meaningful data/configurations (not default empty states)
- For panel screenshots, show interesting/realistic calculations
- For settings screenshots, show typical parameter values
- Ensure UI elements are clearly visible and text is readable
- Consider using browser developer tools to ensure consistent rendering

## Directory Structure

Create the following directory structure in the repository:

```
spdcalc-docs/
└── .gitbook/
    └── assets/
        └── screenshots/
            ├── interface/
            ├── panels/
            ├── presets/
            ├── reference/
            ├── results/
            ├── settings/
            └── sharing/
```

Once screenshots are captured and placed in the appropriate directories, the documentation will be fully illustrated and ready for publication.
