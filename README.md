# Welcome to SPDCalc Documentation

SPDCalc is a comprehensive tool for calculating optical properties of spontaneous parametric down-conversion (SPDC) crystals used in quantum optics experiments. It provides interactive visualizations, automatic parameter calculations, and multi-core computation to help researchers design and optimize SPDC sources for quantum optics applications.

## Quick Links

* [Quick Start Guide](getting-started/quick-start.md) — Get started with the SPDCalc web interface
* [Configuring Parameters](guides/configuring-parameters.md) — Learn how to configure crystal, pump, and signal settings

## About This Documentation

This documentation covers the SPDCalc web interface, the most common way to use SPDCalc. The calculation engine is written in Rust with Python bindings also available.

## Technology

The SPDCalc web UI is built with Vue 2 and uses a Rust/WebAssembly backend for high-performance calculations. Multi-threaded computation via Web Workers enables fast calculations on modern multi-core CPUs.

## Getting Help

* **UI bugs**: Report at [spdcalc-ui GitHub](https://github.com/spdcalc/spdcalc-ui)
* **Functionality bugs**: Report at [spdcalc GitHub](https://github.com/spdcalc/spdcalc)

Browse the documentation using the navigation menu on the left to explore all features and capabilities.
