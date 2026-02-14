# Appendices

This section provides reference material for crystal types, phasematching configurations, and technical terminology used throughout SPDCalc. Use this section as a quick lookup guide when configuring experiments or interpreting results.

## Crystal Types Reference

SPDCalc supports a variety of nonlinear optical crystals commonly used in SPDC experiments. Each crystal has different optical properties, transmission ranges, and applications.

### Available Crystals

The following crystals are built into SPDCalc with validated Sellmeier equations and temperature dependencies:

<details>
<summary><strong>BBO (Beta Barium Borate)</strong> - BBO_1</summary>

**Chemical Formula:** β-BaB₂O₄

**Optic Axis Type:** Negative Uniaxial

**Point Group:** 3m (Trigonal)

**Transmission Range:** 189 nm - 3,500 nm

**Temperature Dependence:** Known (included in calculations)

**Typical Applications:**
- UV to visible SPDC
- Broadband down-conversion
- Type I and Type II phasematching
- Common choice for 775 nm pump (telecom SPDC at 1550 nm)

**Reference:** [Newlight Photonics - BBO Properties](http://www.newlightphotonics.com/v1/bbo-properties.html)

</details>

<details>
<summary><strong>KTP (Potassium Titanyl Phosphate)</strong> - KTP</summary>

**Chemical Formula:** KTiOPO₄

**Optic Axis Type:** Positive Biaxial

**Point Group:** mm2 (Orthorhombic)

**Transmission Range:** 350 nm - 3,500 nm

**Temperature Dependence:** Known (included in calculations)

**Typical Applications:**
- Visible to near-IR SPDC
- Type 0 and Type II phasematching
- Often used with periodic poling (PPKTP)
- Excellent for telecom wavelengths with 775 nm pump
- High nonlinear coefficient

**Reference:** [Red Optronics - KTP Crystal](http://www.redoptronics.com/KTP-crystal.html)

**Note:** Periodically poled KTP (PPKTP) is widely used for quasi-phasematching at telecom wavelengths.

</details>

<details>
<summary><strong>BiBO (Bismuth Borate)</strong> - BiBO_1</summary>

**Chemical Formula:** BiB₃O₆

**Optic Axis Type:** Positive Biaxial

**Point Group:** 2 (Monoclinic)

**Transmission Range:** 286 nm - 2,500 nm

**Temperature Dependence:** Not available

**Typical Applications:**
- Visible to near-IR SPDC
- Large acceptance angles
- High effective nonlinearity
- Often used for 532 nm pumped SPDC

**Reference:** [Newlight Photonics - BiBO Properties](http://www.newlightphotonics.com/v1/bibo-properties.html)

</details>

<details>
<summary><strong>LiNbO₃ (Lithium Niobate)</strong> - LiNbO3_1</summary>

**Chemical Formula:** LiNbO₃

**Optic Axis Type:** Negative Uniaxial

**Point Group:** 3m (Trigonal)

**Transmission Range:** 0.4 nm - 3.4 nm (likely 400 nm - 3400 nm)

**Temperature Dependence:** Known (included in calculations)

**Typical Applications:**
- Widely used with periodic poling (PPLN)
- Excellent for telecom wavelengths
- High nonlinear coefficient
- Mature fabrication technology

**Reference:** [Newlight Photonics - LN Crystal](http://www.newlightphotonics.com/v1/LN-crystal.html)

</details>

<details>
<summary><strong>LiNb:MgO (Magnesium-Doped Lithium Niobate)</strong> - LiNb_MgO</summary>

**Chemical Formula:** LiNbO₃:MgO

**Optic Axis Type:** Negative Uniaxial

**Point Group:** 3m (Trigonal)

**Transmission Range:** Varies (consult reference)

**Temperature Dependence:** Known (included in calculations)

**Typical Applications:**
- Improved resistance to photorefractive damage compared to undoped LiNbO₃
- Used in high-power applications
- Periodic poling available

</details>

<details>
<summary><strong>KDP (Potassium Dihydrogen Phosphate)</strong> - KDP_1</summary>

**Chemical Formula:** KH₂PO₄

**Optic Axis Type:** Negative Uniaxial

**Point Group:** -42m (Tetragonal)

**Transmission Range:** 200 nm - 1,500 nm

**Temperature Dependence:** Not available

**Typical Applications:**
- UV to visible SPDC
- Historical importance in nonlinear optics
- Lower damage threshold than modern crystals

**Reference:** [Newlight Photonics - KDP Crystal](http://www.newlightphotonics.com/v1/KDP-crystal.html)

</details>

<details>
<summary><strong>AgGaSe₂ (Silver Gallium Selenide)</strong> - AgGaSe2_1, AgGaSe2_2</summary>

**Chemical Formula:** AgGaSe₂

**Optic Axis Type:** Negative Uniaxial

**Point Group:** 3m (Trigonal)

**Transmission Range:** 1,000 nm - 13,500 nm

**Temperature Dependence:** Known (included in calculations)

**Typical Applications:**
- Mid-infrared SPDC
- Extended transmission into mid-IR
- Useful for wavelengths beyond 2 μm

**Reference:** [Sciencedirect Article](https://www.sciencedirect.com/science/article/pii/0030401873903167)

**Note:** Two reference datasets available (AgGaSe2_1 and AgGaSe2_2).

</details>

<details>
<summary><strong>LiIO₃ (Lithium Iodate)</strong> - LiIO3_1, LiIO3_2</summary>

**Chemical Formula:** LiIO₃

**Optic Axis Type:** Negative Uniaxial

**Point Group:** 622 (Hexagonal) for ref 2

**Transmission Range:** 300 nm - 5,000 nm

**Temperature Dependence:** Varies by reference

**Typical Applications:**
- Visible to mid-IR SPDC
- Good transparency range

**Note:** Two reference datasets available with different Sellmeier coefficients.

</details>

<details>
<summary><strong>AgGaS₂ (Silver Gallium Sulfide)</strong> - AgGaS2_1</summary>

**Chemical Formula:** AgGaS₂

**Optic Axis Type:** Negative Uniaxial

**Point Group:** 3m (Trigonal)

**Transmission Range:** Consult reference

**Temperature Dependence:** Known (included in calculations)

**Typical Applications:**
- Mid-infrared applications
- Nonlinear frequency conversion in the IR

</details>

### Custom Crystal Expressions

SPDCalc also supports **custom crystal definitions** using mathematical expressions for the refractive indices. This allows you to:

- Use crystals not in the built-in library
- Test experimental Sellmeier equations
- Model custom materials

**Expression Format:**

Uniaxial crystals require `no` (ordinary) and `ne` (extraordinary) indices:

```json
{
  "no": "sqrt(2.7359+0.01878/(l^2-0.01822)-0.01354*l^2) - 9.3e-6 * T",
  "ne": "sqrt(2.3753+0.01224/(l^2-0.01667)-0.01516*l^2) - 16.6e-6 * T"
}
```

Biaxial crystals require `nx`, `ny`, and `nz` indices:

```json
{
  "nx": "expression for nx",
  "ny": "expression for ny",
  "nz": "expression for nz"
}
```

**Variables:**
- `l` = wavelength in micrometers (μm)
- `T` = temperature offset from 20°C in Kelvin (K)

**Supported Operations:** `+`, `-`, `*`, `/`, `^` (power), `sqrt()`, standard mathematical functions

## Phasematching Types Explained

Phasematching is the condition where the pump, signal, and idler photons have matched phase velocities, enabling efficient SPDC. The phasematching type refers to the polarization configuration of the three beams.

### Polarization Notation

- **o (ordinary):** Polarization perpendicular to the crystal's optical axis (optic axis)
- **e (extraordinary):** Polarization in the plane containing the optical axis

The notation format is: **pump polarization → signal polarization + idler polarization**

For example, "e → o + o" means:
- Pump: extraordinary polarization
- Signal: ordinary polarization
- Idler: ordinary polarization

### Type 0 Phasematching

**Configuration:** All three photons have the same polarization

**Variants:**
- **Type 0 (o → o + o):** All ordinary polarization
- **Type 0 (e → e + e):** All extraordinary polarization

**Characteristics:**
- No spatial walk-off between signal and idler (both same polarization)
- Highest spatial mode overlap
- Often requires periodic poling (quasi-phasematching)
- Excellent for generating high-purity single photons

**Typical Applications:**
- Generating spectrally pure photons for quantum information
- Applications requiring maximum heralding efficiency
- Experiments where spatial walk-off must be minimized

**Diagram Placeholder:**
![Type 0 Phasematching](.gitbook/assets/screenshots/reference/phasematching-type-0.png)

{% hint style="info" %}
Type 0 phasematching is most commonly achieved using periodically poled crystals (PPKTP, PPLN) because collinear Type 0 often cannot satisfy birefringent phasematching conditions.
{% endhint %}

### Type I Phasematching

**Configuration:** Signal and idler have the same polarization, different from the pump

**Standard Form:**
- **Type I (e → o + o):** Pump is extraordinary, signal and idler are ordinary

**Characteristics:**
- Signal and idler photons are indistinguishable by polarization
- No spatial walk-off between signal and idler
- Simpler collection optics than Type II
- Broader spectral bandwidth than Type II

**Phase Matching Condition:**

$$n_p(\omega_p, \theta) = n_s(\omega_s) = n_i(\omega_i)$$

where θ is the crystal angle tuned to satisfy phasematching.

**Typical Applications:**
- Generating photon pairs for HOM interference
- Photon pair sources for quantum key distribution
- Experiments requiring polarization-identical photons

**Advantages:**
- Simple collection (no need to separate by polarization)
- Both photons experience same spatial mode
- Good spectral brightness

**Disadvantages:**
- Less flexible than Type II for frequency tuning
- Cannot generate polarization-entangled states directly

**Diagram Placeholder:**
![Type I Phasematching](.gitbook/assets/screenshots/reference/phasematching-type-1.png)

### Type II Phasematching

**Configuration:** Signal and idler have orthogonal polarizations

**Variants:**
- **Type II (e → e + o):** Pump extraordinary, signal extraordinary, idler ordinary
- **Type II (e → o + e):** Pump extraordinary, signal ordinary, idler extraordinary

**Characteristics:**
- Signal and idler have opposite polarizations
- Can generate polarization-entangled photon pairs
- Spatial walk-off between signal and idler due to different polarizations
- Narrower bandwidth than Type I (better spectral purity)

**Phase Matching Condition:**

$$\vec{k}_p(\omega_p) = \vec{k}_s(\omega_s) + \vec{k}_i(\omega_i)$$

with signal and idler having different refractive indices due to polarization.

**Typical Applications:**
- Generating polarization-entangled Bell states
- High-purity heralded single photons (due to spectral filtering)
- Quantum teleportation and dense coding
- Fundamental tests of quantum mechanics (Bell tests)

**Advantages:**
- Can produce polarization entanglement
- Narrower spectral correlations (higher spectral purity)
- Signal and idler distinguishable by polarization

**Disadvantages:**
- Spatial walk-off reduces spatial mode overlap
- More complex collection optics (need to separate polarizations)
- Reduced heralding efficiency without careful spatial mode matching

**Diagram Placeholder:**
![Type II Phasematching](.gitbook/assets/screenshots/reference/phasematching-type-2.png)

{% hint style="warning" %}
Type II phasematching introduces spatial walk-off between signal and idler photons. To maintain high heralding efficiency, careful matching of collection mode waists and positions is essential.
{% endhint %}

### Choosing a Phasematching Type

| Criterion | Type 0 | Type I | Type II |
|-----------|--------|--------|---------|
| **Spectral Purity** | Excellent (with careful design) | Good | Excellent |
| **Heralding Efficiency** | Highest | High | Moderate (requires optimization) |
| **Spatial Walk-off** | None | None | Yes (signal-idler) |
| **Polarization Entanglement** | No | No | Yes |
| **Ease of Collection** | Easiest | Easy | Moderate |
| **Typical Configuration** | Quasi-phasematched | Birefringent or QPM | Birefringent |

## Glossary of Terms

### A

**Apodization**
A technique for gradually varying the nonlinear coupling strength along the crystal length (typically in periodically poled crystals) to shape the spectral or spatial properties of the down-converted light. Common apodization functions include Gaussian, Bartlett, and Hamming windows.

**Auto-Calculation**
SPDCalc's feature that automatically computes dependent parameters (crystal angle, poling period, integration limits, waist positions) based on user-specified values. Reduces manual calculation effort and ensures consistency.

### B

**Bandwidth**
The frequency or wavelength range over which a signal has significant spectral intensity. In SPDC, pump bandwidth affects spectral correlations between signal and idler photons.

**Beam Waist**
The location along a Gaussian beam where the beam radius reaches its minimum value. Critical parameter for mode-matching in SPDC experiments.

**Birefringence**
The optical property of materials having different refractive indices for different polarization orientations. Essential for phasematching in SPDC crystals.

### C

**Collinear SPDC**
Spontaneous parametric down-conversion where signal and idler photons propagate in the same direction as the pump beam (zero collection angle).

**Counter-Propagation**
A configuration where signal and idler photons propagate in opposite directions. Used in some SPDC geometries for specific applications.

**Crystal Angle (θ, φ)**
Spherical coordinates describing the orientation of the crystal's optic axis relative to the pump beam. Tuning these angles changes phasematching conditions.
- **θ (theta):** Polar angle between optic axis and pump propagation direction
- **φ (phi):** Azimuthal angle in the plane perpendicular to pump direction

### D

**Deff (Effective Nonlinear Coefficient)**
The effective second-order nonlinear coefficient (in pm/V) that quantifies the strength of the three-wave mixing process. Depends on crystal type and phasematching geometry.

**Degeneracy**
The condition where signal and idler photons have the same wavelength (typically half the pump wavelength in frequency).

**Δk (Delta-k, Wavevector Mismatch)**
The difference between the pump wavevector and the sum of signal and idler wavevectors. Phasematching occurs when Δk = 0.

$$\Delta k = k_p - k_s - k_i$$

### E

**Extraordinary Polarization (e-ray)**
Light polarized in the plane containing the crystal's optic axis. Experiences refractive index that depends on propagation angle.

### F

**Fiber Coupling**
The process of collecting down-converted photons into single-mode optical fibers. Coupling efficiency depends on spatial mode matching between SPDC mode and fiber mode.

**FWHM (Full Width at Half Maximum)**
The width of a distribution measured at half its maximum value. Used to characterize spectral widths, spatial profiles, and correlation functions.

### G

**Group Velocity**
The velocity at which the envelope of a light pulse propagates. Group velocity mismatch between pump, signal, and idler affects temporal correlations in SPDC.

**Group Velocity Dispersion (GVD)**
The frequency dependence of group velocity, causing temporal broadening of pulses.

### H

**Heralding Efficiency**
The probability that detecting one photon of a pair (the herald) indicates the presence of its partner photon in the conjugate mode. Limited by spatial mode mismatch, spectral filtering, and losses.

**Hong-Ou-Mandel (HOM) Dip**
A quantum interference effect where two indistinguishable photons entering different ports of a beam splitter both exit from the same port. Used to characterize photon indistinguishability.

**HOM Visibility**
A measure of the depth of the Hong-Ou-Mandel interference dip, quantifying the indistinguishability of two photons. Perfect visibility (V=1) indicates fully indistinguishable photons.

### I

**Idler Photon**
In SPDC, one of the two down-converted photons. Typically distinguished from the signal photon by wavelength or collection direction. Energy conservation: ω_pump = ω_signal + ω_idler.

**Integration Limits**
The wavelength or frequency ranges over which JSA/JSI calculations are performed. Can be auto-calculated based on pump spectrum or manually specified.

### J

**JSA (Joint Spectral Amplitude)**
The complex-valued two-photon wavefunction in the frequency domain, describing correlations between signal and idler photon frequencies. Contains both amplitude and phase information.

**JSI (Joint Spectral Intensity)**
The squared magnitude of the JSA, representing the probability distribution of finding signal and idler photons at particular frequencies. JSI = |JSA|².

### M

**Mode Matching**
The spatial overlap between the SPDC emission mode and the collection mode (e.g., fiber mode). Crucial for high heralding efficiency.

### N

**Noncollinear SPDC**
Spontaneous parametric down-conversion where signal and idler photons propagate at different angles relative to the pump beam.

### O

**Ordinary Polarization (o-ray)**
Light polarized perpendicular to the crystal's optic axis. Experiences the ordinary refractive index n_o, independent of propagation direction.

**Optimum Idler**
The automatically calculated idler photon properties (wavelength, angle, waist size) that satisfy energy and momentum conservation for given pump and signal parameters.

### P

**Phasematching**
The condition where momentum (or wavevector) is conserved in the three-wave mixing process:

$$\vec{k}_p = \vec{k}_s + \vec{k}_i$$

Efficient SPDC requires phasematching to be satisfied.

**Phasematching Curve**
A plot showing how phasematching conditions (or wavevector mismatch Δk) vary as a function of wavelength, crystal angle, or other parameters.

**Periodic Poling**
A technique where the sign of the nonlinear coefficient is periodically reversed along the crystal length, enabling quasi-phasematching for arbitrary wavelength combinations.

**Poling Period**
The spatial period (in microns) of the periodic domain inversion in a quasi-phasematched crystal. Determines which wavelengths achieve phasematching.

**PPKTP (Periodically Poled KTP)**
KTP crystal with periodic domain inversion. Widely used for telecom-wavelength SPDC with 775 nm pump.

**PPLN (Periodically Poled Lithium Niobate)**
LiNbO₃ crystal with periodic domain inversion. Another popular choice for telecom SPDC.

**Pump Photon**
The input photon (typically from a laser) that undergoes down-conversion to create signal and idler photon pairs. Energy: ω_pump = ω_signal + ω_idler.

### Q

**Quasi-Phasematching (QPM)**
Phasematching achieved through periodic poling rather than birefringence. Allows phasematching for polarization combinations not possible with birefringent phasematching.

### R

**Refractive Index**
The ratio of the speed of light in vacuum to the speed of light in the material. Wavelength-dependent (dispersion) and polarization-dependent (birefringence) in anisotropic crystals.

### S

**Schmidt Decomposition**
A mathematical technique for decomposing the two-photon state into a sum of products of single-photon states, revealing the degree of entanglement.

**Schmidt Number**
A quantitative measure of entanglement derived from Schmidt decomposition. K ≈ 1 indicates low entanglement (high spectral purity), while K >> 1 indicates strong spectral correlations.

**Signal Photon**
In SPDC, one of the two down-converted photons, typically the one being detected or collected. Distinguished from idler by wavelength or collection direction.

**Sellmeier Equations**
Empirical formulas describing the wavelength and temperature dependence of refractive indices in optical materials. Each crystal type has characteristic Sellmeier coefficients.

**SPDC (Spontaneous Parametric Down-Conversion)**
A nonlinear optical process where a pump photon spontaneously splits into two lower-energy photons (signal and idler) inside a nonlinear crystal, conserving energy and momentum.

**Spectral Purity**
A measure of how uncorrelated the signal and idler photons are spectrally. High purity means detecting the idler provides minimal information about the signal's wavelength. Inversely related to Schmidt number.

### T

**Temperature Tuning**
Adjusting the crystal temperature to shift refractive indices and thereby tune phasematching conditions. Some crystals have known temperature-dependent Sellmeier equations.

**Type 0, Type I, Type II**
Classification of phasematching based on the polarization combinations of pump, signal, and idler photons. See "Phasematching Types Explained" section above.

### W

**Walk-off**
Spatial separation between beams of different polarizations propagating through a birefringent crystal. Extraordinary rays walk away from the ordinary ray direction, reducing spatial overlap.

**Waist Position**
The longitudinal position (along the beam axis) where the beam waist occurs. In SPDC, optimal waist positions maximize spatial mode overlap and heralding efficiency.

**Wavelength**
The spatial period of an electromagnetic wave. In SPDC, pump wavelength determines the energy available for signal and idler photons.

---

{% hint style="info" %}
For additional technical details on crystal properties, consult the built-in Info Panel in SPDCalc, which displays calculated refractive indices and optimized parameters for your current configuration.
{% endhint %}
