

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
