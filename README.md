---
icon: hand-wave
---

# Welcome to SPDCalc Documentation

SPDCalc is a comprehensive tool for calculating optical properties of spontaneous parametric down-conversion (SPDC) crystals used in quantum optics experiments. It provides interactive visualizations, automatic parameter calculations, and multi-core computation to help researchers design and optimize SPDC sources for quantum information applications.

## Quick Links

<table data-view="cards">
<thead>
<tr>
<th></th>
<th></th>
<th data-hidden data-card-target data-type="content-ref"></th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Quick Start Guide</strong></td>
<td>Get started with the SPDCalc web interface</td>
<td><a href="getting-started/quick-start.md">quick-start.md</a></td>
</tr>
<tr>
<td><strong>Configuring Parameters</strong></td>
<td>Learn how to configure crystal, pump, and signal settings</td>
<td><a href="guides/configuring-parameters.md">configuring-parameters.md</a></td>
</tr>
<tr>
<td><strong>Calculation Panels</strong></td>
<td>Detailed reference for all calculation panels and visualizations</td>
<td><a href="reference/calculation-panels-reference.md">calculation-panels-reference.md</a></td>
</tr>
<tr>
<td><strong>Best Practices</strong></td>
<td>Tips for efficient workflows and troubleshooting</td>
<td><a href="tips/best-practices.md">best-practices.md</a></td>
</tr>
</tbody>
</table>

## About This Documentation

This documentation covers the SPDCalc web interface, the most common way to use SPDCalc. The calculation engine is written in Rust with Python bindings also available.

### What You'll Find Here

* **Introduction** - Overview of SPDCalc and how to report bugs
* **Getting Started** - Quick start guide for new users
* **User Guides** - Comprehensive guides for all features
* **Reference** - Detailed technical reference for panels and parameters
* **Tips & Best Practices** - Optimization strategies and troubleshooting

## Technology

The SPDCalc web UI is built with Vue 2 and uses a Rust/WebAssembly backend for high-performance calculations. Multi-threaded computation via Web Workers enables fast calculations on modern multi-core CPUs.

## Getting Help

* **UI bugs**: Report at [spdcalc-ui GitHub](https://github.com/spdcalc/spdcalc-ui)
* **Functionality bugs**: Report at [spdcalc GitHub](https://github.com/spdcalc/spdcalc)

Browse the documentation using the navigation menu on the left to explore all features and capabilities.
