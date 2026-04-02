# Crystal Types Reference

SPDCalc includes a set of built-in crystals with validated Sellmeier equations, and also supports defining custom crystals via tabulated data.

## Built-in Crystals

| Crystal | ID(s) | Temp. Dependence | Reference |
|---|---|---|---|
| [BBO](#bbo-beta-barium-borate) | `BBO_1` | Yes | [Newlight Photonics](http://www.newlightphotonics.com/v1/bbo-properties.html) |
| [KTP](#ktp-potassium-titanyl-phosphate) | `KTP` | Yes | [Red Optronics](http://www.redoptronics.com/KTP-crystal.html) |
| [BiBO](#bibo-bismuth-borate) | `BiBO_1` | No | [Newlight Photonics](http://www.newlightphotonics.com/v1/bibo-properties.html) |
| [LiNbO₃](#linbo-lithium-niobate) | `LiNbO3_1` | Yes | [Newlight Photonics](http://www.newlightphotonics.com/v1/LN-crystal.html) |
| [LiNb:MgO](#linbmgo-magnesium-doped-lithium-niobate) | `LiNb_MgO` | Yes | — |
| [KDP](#kdp-potassium-dihydrogen-phosphate) | `KDP_1` | No | [Newlight Photonics](http://www.newlightphotonics.com/v1/KDP-crystal.html) |
| [AgGaSe₂](#aggase-silver-gallium-selenide) | `AgGaSe2_1`, `AgGaSe2_2` | Yes | [Sciencedirect](https://www.sciencedirect.com/science/article/pii/0030401873903167) |
| [LiIO₃](#liio-lithium-iodate) | `LiIO3_1`, `LiIO3_2` | Varies by ref. | — |
| [AgGaS₂](#aggas-silver-gallium-sulfide) | `AgGaS2_1` | Yes | — |

### BBO (Beta Barium Borate)

**ID:** `BBO_1` | **Axis:** Uniaxial negative | **Temp. dependence:** Yes

### KTP (Potassium Titanyl Phosphate)

**ID:** `KTP` | **Axis:** Biaxial | **Temp. dependence:** Yes

### BiBO (Bismuth Borate)

**ID:** `BiBO_1` | **Axis:** Biaxial | **Temp. dependence:** No

### LiNbO₃ (Lithium Niobate)

**ID:** `LiNbO3_1` | **Axis:** Uniaxial negative | **Temp. dependence:** Yes

### LiNb:MgO (Magnesium-Doped Lithium Niobate)

**ID:** `LiNb_MgO` | **Axis:** Uniaxial negative | **Temp. dependence:** Yes

### KDP (Potassium Dihydrogen Phosphate)

**ID:** `KDP_1` | **Axis:** Uniaxial negative | **Temp. dependence:** No

### AgGaSe₂ (Silver Gallium Selenide)

**IDs:** `AgGaSe2_1`, `AgGaSe2_2` | **Axis:** Uniaxial | **Temp. dependence:** Yes

### LiIO₃ (Lithium Iodate)

**IDs:** `LiIO3_1`, `LiIO3_2` | **Axis:** Uniaxial negative | **Temp. dependence:** Varies by reference

### AgGaS₂ (Silver Gallium Sulfide)

**ID:** `AgGaS2_1` | **Axis:** Uniaxial | **Temp. dependence:** Yes

---

## Custom Crystals

> [!WARNING]
> Custom crystal support is experimental and currently available for evaluation. Behavior may change in future versions.

> [!NOTE]
> Custom crystals are currently saved in the URL data string. If the app is visited without that string, the custom crystals disappear.

If you have measured or published refractive index data for a uniaxial crystal not in the built-in list, SPDCalc can interpolate between your data points to define a custom crystal.

### Opening the Editor

In the Crystal Settings panel, click the **Edit Custom Crystals** button. This opens the Custom Crystal Editor dialog.

### Entering Data

Give the crystal a **Crystal Label** — a name you choose to identify it in the dropdown.

Then enter three parallel comma-separated lists:

| Field | Description |
|---|---|
| **Wavelengths (nm)** or **Frequencies (THz)** | The spectral points at which your data was measured. Select the unit from the dropdown next to the field. |
| **Ordinary Indices (no)** | The ordinary refractive index at each spectral point. |
| **Extraordinary Indices (ne)** | The extraordinary refractive index at each spectral point. |

**Requirements:**
- All three lists must have the same number of values.
- At least 2 data points are required.
- Spectral values must be in strictly ascending order.
- All refractive index values must be ≥ 1.

**Example:**

```
Wavelengths (nm):    400, 532, 700, 800, 1064
Ordinary (no):       1.675, 1.661, 1.652, 1.648, 1.639
Extraordinary (ne):  1.555, 1.544, 1.537, 1.533, 1.526
```

Click **Create** to save the crystal. It will immediately be selected and will appear in the crystal type dropdown for future use.

### Managing Saved Crystals

Previously saved custom crystals appear in the **Crystal Preset** dropdown at the top of the editor. Select one to load it for editing or deletion.

