# Introduction to the SPDCalc Web UI

SPDCalc is a web-based tool for designing and analyzing spontaneous parametric downconversion (SPDC) sources used in quantum optics experiments. This guide will help you understand what SPDCalc does and how to use its web interface.

## Background

The process of spontaneous parametric downconversion is an important source of single-photons and quantum states of light. Much recent theoretical and experimental work focuses on engineering the properties of the photons emitted from downconversion. For multi-photon experiments generating photon pairs that are spectrally pure, meaning the signal and idler photons are uncorrelated, has been an active area of investigation. For fundamental tests of quantum mechanics, such as loop-hole-free Bell tests, optimizing the coupling of photons to single-mode fiber is an important consideration.

While the principles behind the nonlinear process of downconversion are well understood, calculating the properties of the photons can be difficult and time-consuming. This library designed to simplify these calculations.

### What does SPDCalc calculate?

SPDCalc helps researchers and students design and optimize SPDC sources by calculating:

- **Phasematching properties**: Determining the conditions under which efficient photon pair generation occurs in your crystal
- **Joint spectral analysis (JSA/JSI)**: Visualizing the spectral correlations between signal and idler photons to understand entanglement and purity
- **Spectral purity**: Analyzing how well your source produces spectrally uncorrelated photon pairs through Schmidt decomposition
- **Hong-Ou-Mandel interference**: Calculating interference visibility for both single-source and two-source configurations to characterize photon indistinguishability
- **Fiber coupling efficiency**: Optimizing collection mode matching and heralding efficiency for single-mode fiber coupling

### Features

SPDCalc simplifies calculations by providing:

- **Interactive visualization**: Real-time plots and graphs that update as you adjust parameters
- **Automatic calculations**: Intelligent auto-calculation of dependent parameters like crystal angles, poling periods, and integration limits
- **Multi-core computation**: Fast calculations using your computer's CPU cores via WebAssembly and Web Workers
- **Shareable configurations**: Save and share your crystal setups via URL links or JSON files
- **No installation required**: Runs entirely in your web browser at [app.spdcalc.org](https://app.spdcalc.org)

### Who is SPDCalc for?

SPDCalc is designed for:

- **Researchers** designing quantum optics experiments with SPDC sources
- **Graduate students** learning about quantum optics and parametric downconversion
- **Experimentalists** optimizing existing SPDC setups for maximum efficiency or desired photon properties
- **Theorists** exploring the parameter space of SPDC for different crystal and beam configurations

### Technology behind the web UI

The SPDCalc web application is built using modern web technologies to deliver fast, responsive calculations directly in your browser:

- **Frontend**: Vue 2 framework with Vuetify components for a clean, intuitive interface
- **Computation engine**: Rust library compiled to WebAssembly (WASM) for near-native performance
- **Parallel processing**: Multi-threaded calculations using Web Workers that automatically scale to your CPU's core count
- **Offline capability**: Works without an internet connection after initial load (Progressive Web App)

This architecture means SPDCalc performs sophisticated quantum optics calculations entirely client-side, without sending your data to a server. All computations happen on your own computer, ensuring both privacy and performance.

### Other ways to use SPDCalc

While this guide focuses on the web interface, SPDCalc is available in other forms:

- **Rust library**: The core computation engine is available as a Rust crate on [crates.io](https://crates.io/crates/spdcalc) for integration into Rust projects
- **Python bindings**: Python users can access SPDCalc functionality through the [spdcalc-py](https://pypi.org/project/spdcalc-py/) package

This guide covers only the web UI. For information about the Rust library or Python bindings, please refer to their respective documentation.

## How to report bugs

SPDCalc is actively maintained, and we welcome bug reports and feature requests from the community. The project is split into two GitHub repositories, depending on the nature of the issue:

### UI bugs (interface, visualization, controls)

If you encounter issues with the **web interface** itself, such as:

- Display problems or layout issues
- Controls not responding correctly
- Panel rendering errors
- Browser compatibility issues
- URL sharing or preset management problems
- Settings not saving or loading properly

Please report these at the **SPDCalc UI repository**:

**GitHub**: [https://github.com/spdcalc/spdcalc-ui](https://github.com/spdcalc/spdcalc-ui)

### Functionality bugs (calculation errors, physics issues)

If you encounter issues with the **calculations or physics**, such as:

- Incorrect or unexpected calculation results
- Physical values that don't match theoretical predictions or other software
- Crashes during computation
- Problems with crystal properties or phasematching
- Errors in joint spectrum, Schmidt number, or Hong-Ou-Mandel calculations
- Issues with new crystal types or custom crystal expressions

Please report these at the **SPDCalc core library repository**:

**GitHub**: [https://github.com/spdcalc/spdcalc](https://github.com/spdcalc/spdcalc)

### Feature requests and questions

We also welcome feature requests and questions:

- **Feature requests**: Open an issue in the appropriate repository (UI features in spdcalc-ui, new calculations in spdcalc)
- **Questions about usage**: Open a discussion in [the spdcalc repository](https://github.com/spdcalc/spdcalc) or check the documentation
- **Scientific questions**: For questions about the physics of SPDC rather than the tool itself, please send an email to [info@spdcalc.org](mailto:info@spdcalc.org)

### Contributing

SPDCalc is open source, and contributions are welcome! If you'd like to contribute code, documentation, or new crystal types:

- Fork the repository and create a pull request
- For major changes, open an issue first to discuss your proposed changes

