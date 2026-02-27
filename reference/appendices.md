# Appendices

This section provides reference material for crystal types, phasematching configurations, and technical terminology used throughout SPDCalc.

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