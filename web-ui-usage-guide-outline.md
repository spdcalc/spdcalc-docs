# SPDCalc Usage Guide - Outline

## Introduction to the SPDCalc Web UI

### What is SPDCalc?
A brief overview explaining that SPDCalc is a tool for calculating optical properties of spontaneous parametric down-conversion (SPDC) crystals used in quantum optics experiments. The tool is most commonly used via its web interface, but the engine is written in rust, and has companion python bindings.

### How to report bugs
Explain that UI bugs can be reported here: https://github.com/spdcalc/spdcalc-ui
Functionality bugs reported here: https://github.com/spdcalc/spdcalc

## Getting Started

### Opening the Application
How to access SPDCalc in your browser and what to expect on first load.

### Understanding the Interface
Overview of the three main UI areas: the settings drawer (left), the main calculation panel area (center), and the toolbar (top).

## Configuring SPDC Parameters

### Crystal Settings
How to select crystal type, set phasematching type, configure crystal orientation (theta/phi angles), length, and temperature.

### Pump Configuration
Setting pump laser wavelength, bandwidth, beam waist size, power, and spectrum threshold parameters.

### Signal Configuration
Configuring signal photon wavelength, collection angles (theta/phi), beam waist size and position.

### Periodic Poling Settings
Enabling quasi-phasematching through periodic poling, setting the poling period, and configuring apodization profiles.

### Integration Settings
Adjusting integration wavelength ranges, grid resolution, and numerical integration methods for calculations.

### Auto-Calculation Features
Understanding which parameters are automatically calculated (crystal angle, poling period, integration limits) and when to override them.

## Working with Calculation Panels

### Adding and Removing Panels
How to add new calculation panels from the panel selector to visualize different SPDC properties.

### Available Panel Types
Brief description of each panel type: JSI Plot, Phasematching Curves, Schmidt Number plots, Hong-Ou-Mandel dips, Heralding efficiency calculations, and the Info Panel.

### Understanding Auto-Update
How panels automatically recalculate when parameters change and how to disable this behavior if needed.

## Calculation Panels Reference

### Joint Spectrum Intensity (JSI) Plot
Visualizing the two-photon joint spectral amplitude to understand spectral correlations between signal and idler photons.

### Phasematching Curves
Viewing phasematching conditions as a function of wavelength to optimize crystal configuration.

### Schmidt Number Analysis
Analyzing photon pair entanglement through Schmidt decomposition as a function of pump bandwidth and crystal length.

### Hong-Ou-Mandel Dip
Calculating the Hong-Ou-Mandel interference visibility for single-source setups to characterize photon indistinguishability.

### Two-Source HOM Dip
Simulating Hong-Ou-Mandel interference from two independent SPDC sources for quantum networking applications.

### Heralding Efficiency Analysis
Optimizing collection mode matching by analyzing heralding efficiency versus waist sizes and fiber coupling angles.

### Heralding Calculator
Quick calculation tool for determining heralding efficiency and coincidence counts for a specific configuration.

### Info Panel
Viewing calculated crystal information including refractive indices, optimum idler properties, and derived parameters.

## Managing Presets

### Saving Configurations
Creating named presets to save your current parameter configuration for later use.

### Loading Presets
Quickly switching between saved configurations using the preset selector.

### Editing and Deleting Presets
Managing your preset library by renaming or removing saved configurations.

### Understanding the Dirty State
Recognizing when your current parameters differ from the loaded preset through the warning indicator.

## Sharing and Importing

### Sharing via URL
Understanding what is saved in the URL. Generating shareable links that encode your complete configuration in the URL for collaboration.

### Importing/Exporting JSON Settings
Understanding what can be imported/exported via JSON. Loading configurations from JSON files exported from previous sessions or shared by colleagues.

## Working with Results

### Interpreting Visualizations
Understanding the color scales, axes, and units used in different calculation panels.

### Exporting Data
Downloading calculation results as CSV files for further analysis in external tools.

### Performance Considerations
Understanding calculation speed based on grid resolution, integration settings, and your computer's CPU core count.

## Advanced Workflows

(Intentionally left empty for now)

## Tips and Best Practices

### When to Use Auto-Calculation
Guidance on when automatic parameter calculation is helpful versus when manual control is needed.

### Choosing Integration Methods
Recommendations for selecting appropriate numerical integration methods based on your calculation needs.

### Understanding Calculation Time
Factors affecting computation speed and strategies for balancing accuracy with performance.

### Troubleshooting Common Issues
Solutions for common problems like slow calculations, unexpected results, or browser compatibility issues.

## Appendices

### Crystal Types Reference
List of supported crystal types with their properties and typical use cases.

### Phasematching Types Explained
Detailed explanation of Type 0, Type 1, and Type 2 phasematching configurations.

### Units and Conventions
Reference for all units used in the application (nanometers, microns, degrees, etc.).

### Glossary of Terms
Definitions of quantum optics and SPDC terminology used throughout the application.
