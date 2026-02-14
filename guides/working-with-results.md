# Working with Results

Once your calculations are complete, SPDCalc provides powerful visualization and data export tools to help you analyze and share your SPDC results. This guide covers how to interpret visualizations, export your data, and optimize performance for your computational needs.

## Interpreting Visualizations

SPDCalc uses interactive plots and heatmaps to visualize quantum optical properties. Understanding how to read these visualizations is essential for extracting meaningful insights from your calculations.

### Plot Types and Their Components

The application uses two main visualization types:

**Line Plots** - Used for 1D data such as Hong-Ou-Mandel dips, phasematching curves, and Schmidt number variations. These plots display:
- X-axis: Independent variable (e.g., time delay, wavelength, crystal length)
- Y-axis: Calculated property (e.g., coincidence rate, phasematching efficiency)
- Interactive hover tooltips showing exact values

**Heatmaps** - Used for 2D data such as Joint Spectrum Intensity plots. These plots display:
- X-axis: Signal photon property (wavelength, frequency, or sum/difference coordinates)
- Y-axis: Idler photon property (wavelength, frequency, or sum/difference coordinates)
- Color intensity: Magnitude of the calculated property
- Color scale legend: Shows the mapping between colors and numerical values

<figure>
<img src="../.gitbook/assets/screenshots/panels/jsi-plot-example.png" alt="Joint Spectrum Intensity heatmap with labeled axes and color scale">
<figcaption>Example JSI plot showing signal and idler wavelength correlations with color-coded intensity</figcaption>
</figure>

### Understanding Color Scales

Color scales translate numerical data into visual information. SPDCalc uses different color schemes depending on the type of data:

#### Intensity and Amplitude Plots

For intensity and amplitude data, the application uses a **gradient from white (low) to blue (high)**. This color scheme:
- Makes low-intensity regions clearly visible against the dark interface
- Provides intuitive "brighter = stronger" mapping
- Works well for identifying spectral correlation patterns

<figure>
<img src="../.gitbook/assets/screenshots/results/colormap-intensity.png" alt="Intensity color scale showing white to blue gradient">
<figcaption>Intensity color scale: white (zero) to blue (maximum)</figcaption>
</figure>

#### Phase Plots

Phase information uses a **cyclic diverging color scale** that transitions through:
- Dark gray (−π)
- Red (−π/2)
- White (0)
- Blue (+π/2)
- Dark gray (+π)

This cyclic scheme clearly shows phase discontinuities and gradients in the joint spectral amplitude.

<figure>
<img src="../.gitbook/assets/screenshots/results/colormap-phase.png" alt="Phase color scale showing cyclic red-white-blue pattern">
<figcaption>Phase color scale: cyclic representation from −π to +π</figcaption>
</figure>

#### Zero Highlighting

When enabled via the eye icon (👁), the "highlight zero" feature makes near-zero values stand out by coloring them **red** instead of white. This is particularly useful for:
- Identifying regions where SPDC efficiency vanishes
- Checking numerical accuracy (true zeros should appear red)
- Visualizing phasematching cutoffs

{% hint style="info" %}
The zero highlighting threshold is 10⁻⁶ of the maximum value. Values below this threshold appear red.
{% endhint %}

### Reading Axes Labels and Units

Each plot clearly labels its axes with the physical quantity and units. Common units you'll encounter:

| Quantity | Units | Typical Range |
|----------|-------|---------------|
| Wavelength | nm (nanometers) | 400–2000 nm |
| Frequency | THz (terahertz) | 150–750 THz |
| Time delay | fs (femtoseconds) | −1000 to +1000 fs |
| Crystal length | mm (millimeters) | 0.1–50 mm |
| Angle | deg (degrees) or mrad (milliradians) | 0–180° or 0–100 mrad |
| Pump bandwidth | nm or THz | 0.1–100 nm |

{% hint style="warning" %}
When switching between wavelength and frequency representations in the JSI plot, remember that the axes are inverted—shorter wavelengths correspond to higher frequencies.
{% endhint %}

### Logarithmic Scale

Many panels include a log scale toggle (⚡ icon) that switches between linear and logarithmic color mapping. Use logarithmic scale when:
- Your data spans multiple orders of magnitude
- You need to visualize weak spectral features alongside strong ones
- Examining the tails of distributions

In log scale mode, the color bar shows tick marks at powers of 10 (0.01, 0.1, 1.0) instead of linear intervals.

<figure>
<img src="../.gitbook/assets/screenshots/results/log-scale-comparison.png" alt="Side-by-side comparison of linear and logarithmic color scales">
<figcaption>Same JSI data shown in linear (left) and logarithmic (right) scales</figcaption>
</figure>

### Common Visualization Patterns

Learning to recognize common patterns helps you quickly assess your SPDC configuration:

**Joint Spectrum Intensity (JSI)**
- **Diagonal line**: Strong spectral correlation (typical for Type 0 and Type I SPDC)
- **Elliptical shape**: Spectral correlation with finite pump bandwidth
- **Circular blob**: Minimal spectral correlation (near-factorable state)
- **Multiple peaks**: May indicate apodized poling or specific phasematching conditions

**Phasematching Curves**
- **Sharp peak**: Narrow spectral acceptance (short crystal or collinear phasematching)
- **Broad peak**: Wide spectral acceptance (long crystal or specific angles)
- **Oscillations**: Interference effects from finite crystal length

**Hong-Ou-Mandel Dip**
- **Deep narrow dip**: High-quality photon indistinguishability
- **Visibility close to 1**: Near-perfect spectral matching
- **Broad dip**: Long coherence time

{% hint style="info" %}
For detailed interpretation of specific panel types, see the Calculation Panels Reference section of this guide.
{% endhint %}

## Exporting Data

SPDCalc provides multiple export options to facilitate further analysis in external tools, publication preparation, or sharing with collaborators.

### Exporting Numerical Data (JSON)

All plots include a **Download Data** button (💾 icon) in the plot toolbar. This exports the complete numerical dataset underlying the visualization.

{% stepper %}
{% step %}
#### Locate the Download Button

Find the plot toolbar at the top-right corner of any panel. The download button appears as a disk/save icon.

<figure>
<img src="../.gitbook/assets/screenshots/results/export-menu-location.png" alt="Plot toolbar with download button highlighted">
<figcaption>Download button location in the plot toolbar</figcaption>
</figure>
{% endstep %}

{% step %}
#### Click to Download

Click the download button to immediately save a JSON file named `export.json` to your default downloads folder.
{% endstep %}

{% step %}
#### Open the JSON File

The exported JSON file contains:
- `xlabel` and `ylabel`: Axis labels with units
- `url`: The shareable URL of your current configuration
- `plots`: Array of plot data (supports multi-trace plots)

Each plot in the array includes:
- `name`: Plot name (for multi-trace plots)
- `xvals`: Array of x-axis values
- `yvals`: Array of y-axis values
- `zvals`: 2D array of z-values (for heatmaps only)
{% endstep %}
{% endstepper %}

{% tabs %}
{% tab title="Line Plot JSON" %}
```json
{
  "ylabel": "Coincidence Rate",
  "xlabel": "Time Delay (fs)",
  "url": "https://spdcalc.org/?s=...",
  "plots": [
    {
      "name": "HOM Dip",
      "xvals": [-400, -396, -392, ...],
      "yvals": [1.0, 0.998, 0.995, ...]
    }
  ]
}
```

Line plots provide parallel arrays of x and y values. Import into Python, MATLAB, or other analysis tools:

```python
import json
import numpy as np

with open('export.json') as f:
    data = json.load(f)

x = np.array(data['plots'][0]['xvals'])
y = np.array(data['plots'][0]['yvals'])
```
{% endtab %}

{% tab title="Heatmap JSON" %}
```json
{
  "ylabel": "Idler wavelength (nm)",
  "xlabel": "Signal wavelength (nm)",
  "url": "https://spdcalc.org/?s=...",
  "plots": [
    {
      "name": "Joint Spectrum",
      "xvals": [780, 781, 782, ...],
      "yvals": [780, 781, 782, ...],
      "zvals": [
        [0.01, 0.02, 0.03, ...],
        [0.02, 0.05, 0.08, ...],
        ...
      ]
    }
  ]
}
```

Heatmaps include a 2D array where `zvals[i][j]` corresponds to x-coordinate `xvals[j]` and y-coordinate `yvals[i]`.

```python
import json
import numpy as np
import matplotlib.pyplot as plt

with open('export.json') as f:
    data = json.load(f)

plot = data['plots'][0]
x = np.array(plot['xvals'])
y = np.array(plot['yvals'])
z = np.array(plot['zvals'])

plt.pcolormesh(x, y, z)
plt.xlabel(data['xlabel'])
plt.ylabel(data['ylabel'])
plt.show()
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
The exported URL field allows you to trace exactly which configuration produced the data, ensuring reproducibility.
{% endhint %}

### Exporting Plot Images (PNG)

To export a high-resolution image of any plot for presentations or publications:

{% stepper %}
{% step %}
#### Open the Plot Mode Bar

Hover over the plot area to reveal the Plotly mode bar (camera icon) in the top-right corner.
{% endstep %}

{% step %}
#### Click the Camera Icon

Click the camera icon (📷) to download a PNG image. The exported image:
- Has 2000×2000 pixel resolution
- Includes axes, labels, and color scales
- Is named with timestamp: `plot-2026-02-13T12:34:56.789Z.png`
- Maintains the current zoom level and view settings
{% endstep %}
{% endstepper %}

<figure>
<img src="../.gitbook/assets/screenshots/results/plotly-camera-icon.png" alt="Plotly mode bar with camera icon highlighted">
<figcaption>Plotly's camera icon exports high-resolution PNG images</figcaption>
</figure>

{% hint style="info" %}
The image export captures the plot exactly as displayed on screen. Adjust zoom, pan, and axis ranges before exporting to frame your data perfectly.
{% endhint %}

### Exporting Full Configuration

To save or share your complete parameter configuration:

<details>
<summary>Via URL (automatic)</summary>

SPDCalc automatically encodes your entire configuration in the URL. Simply copy the browser's address bar to capture:
- All SPDC parameters (crystal, pump, signal, periodic poling)
- Integration settings
- Active panels and their settings

Share the URL with collaborators or bookmark it for later. See the **Sharing and Importing** section for details.
</details>

<details>
<summary>Via JSON Export</summary>

Use the **Import/Export Settings** dialog (accessed from the settings drawer) to export a JSON file containing your configuration. This is useful for:
- Version control of calculation parameters
- Programmatic parameter sweeps
- Archiving configurations alongside published data

See the **Sharing and Importing** section for the complete workflow.
</details>

### Use Cases for Different Export Formats

{% tabs %}
{% tab title="Publication Figures" %}
**Export Format**: PNG images

**Workflow**:
1. Adjust plot zoom and axes to highlight the relevant feature
2. Toggle log scale or zero highlighting as needed
3. Export PNG at 2000×2000 resolution
4. Import into your publication with proper attribution

**Pro tip**: Disable the mode bar before export by setting a custom zoom to avoid showing Plotly controls in the saved image.
{% endtab %}

{% tab title="Further Analysis" %}
**Export Format**: JSON data

**Workflow**:
1. Export numerical data as JSON
2. Import into Python, MATLAB, Julia, or Mathematica
3. Apply custom analysis, fitting, or visualization
4. Keep the exported URL for reproducing the calculation

**Example analyses**:
- Custom fitting of HOM dip to extract coherence time
- Schmidt decomposition analysis beyond the calculated Schmidt number
- Overlaying experimental data with theoretical predictions
{% endtab %}

{% tab title="Presentations" %}
**Export Format**: PNG images or shareable URL

**Workflow**:
1. For static slides: Export PNG images of key results
2. For interactive demos: Share the URL and open during presentation
3. Use the lock icon to prevent accidental parameter changes during demos

**Pro tip**: Create multiple browser bookmarks with different configurations to quickly switch between scenarios during presentations.
{% endtab %}

{% tab title="Collaboration" %}
**Export Format**: Shareable URL + JSON configuration

**Workflow**:
1. Share URL via email or chat for quick viewing
2. Export JSON for collaborators who want to modify parameters
3. Document which URL corresponds to which figure in shared documents

**Pro tip**: Use URL shorteners for extremely long URLs (complex configurations may produce URLs >1KB).
{% endtab %}
{% endtabs %}

## Performance Considerations

SPDCalc performs quantum optics calculations entirely in your browser using WebAssembly and multi-threaded Web Workers. Understanding the factors that affect calculation speed helps you balance accuracy with responsiveness.

### Factors Affecting Calculation Speed

Several parameters directly impact how long calculations take:

#### Integration Grid Resolution

The **size** parameter in Integration Settings controls the grid resolution for 2D calculations (JSI plots, phasematching histograms):

| Size | Grid Points | Calculation Time* | Use Case |
|------|-------------|-------------------|----------|
| 50 | 2,500 | ~50 ms | Quick preview |
| 100 | 10,000 | ~200 ms | Standard visualization |
| 200 | 40,000 | ~800 ms | High-quality plots |
| 500 | 250,000 | ~5 s | Publication figures |

\* *Approximate times on a modern 8-core CPU for JSI calculation*

{% hint style="warning" %}
Calculation time scales quadratically with grid size. Doubling the resolution quadruples the computation time.
{% endhint %}

#### Integration Range

The wavelength ranges for signal and idler integration affect the numerical integration workload:
- **Narrow ranges** (few nm): Faster calculations, but may truncate spectral features
- **Wide ranges** (100+ nm): Slower calculations, captures full spectral behavior
- **Auto-calculation**: Automatically sets ranges based on pump bandwidth and crystal properties

<details>
<summary>How auto-calculation determines integration ranges</summary>

When "Auto-calculate integration limits" is enabled, SPDCalc sets:
- **Signal wavelength range**: Pump wavelength ± 5× pump bandwidth
- **Idler wavelength range**: Calculated from energy conservation and phasematching

This ensures the integration window captures >99.9% of the spectral amplitude while minimizing unnecessary computation.
</details>

#### Number of Steps in Series Calculations

Panels that plot versus a parameter (HOM time series, Schmidt number vs. crystal length) have a **Steps** setting:
- **Fewer steps** (50–100): Faster, but may miss fine features
- **More steps** (200–500): Smoother curves, longer calculation time

The calculation time scales linearly with the number of steps.

#### Crystal Length and Periodic Poling

Longer crystals and finer poling periods require more careful numerical integration:
- **Short crystals** (< 5 mm): Broad phasematching, easier to integrate
- **Long crystals** (> 20 mm): Narrow phasematching, requires finer grids
- **Short poling periods** (< 10 μm): Rapid phase variations, may need smaller integration steps

### Multi-Threaded Computation

SPDCalc automatically detects your CPU core count and distributes calculations across multiple Web Workers.

**How it works**:
1. The application detects available cores via `navigator.hardwareConcurrency`
2. For heavy calculations, the workload is partitioned across workers
3. Each worker processes a subset of the integration grid independently
4. Results are combined when all workers complete

<figure>
<img src="../.gitbook/assets/screenshots/interface/multi-core-diagram.png" alt="Diagram showing calculation partitioned across 4 CPU cores">
<figcaption>Multi-threaded calculation distributing work across 4 CPU cores</figcaption>
</figure>

{% hint style="success" %}
On an 8-core CPU, calculations can be up to 6–7× faster than single-threaded execution. The speedup is slightly less than the core count due to coordination overhead.
{% endhint %}

**CPU Core Utilization**:
- **2 cores**: Minimal parallelization benefit
- **4 cores**: ~3× speedup on large calculations
- **8+ cores**: ~6–7× speedup on large calculations

You can observe CPU usage in your system monitor while SPDCalc calculates to verify multi-threading is active.

### Progress Indicators and Calculation Status

Each calculation panel provides real-time feedback on calculation progress:

#### Status Messages

The bottom toolbar of each panel displays:
- **"calculating..."**: Calculation in progress
- **"done in X ms"**: Calculation completed, showing duration
- **Error messages**: If calculation fails or is cancelled

<figure>
<img src="../.gitbook/assets/screenshots/interface/status-bar.png" alt="Panel status bar showing calculation time">
<figcaption>Status bar indicating completed calculation and duration</figcaption>
</figure>

#### Progress Spinner

A **yellow circular spinner** appears at the bottom of each panel during calculation:
- **Indeterminate spinner**: Rotating animation for ongoing calculations
- **Determinate progress** (when available): Shows percentage completion for long calculations

<figure>
<img src="../.gitbook/assets/screenshots/interface/progress-spinner.png" alt="Yellow progress spinner during calculation">
<figcaption>Progress spinner indicating active calculation</figcaption>
</figure>

#### Canceling Calculations

If a calculation is taking too long or you've changed your mind:

{% stepper %}
{% step %}
#### Click the Cancel Button

During calculation, the refresh button (↻) is replaced by a red **cancel button** (✖) in the panel toolbar.
{% endstep %}

{% step %}
#### Calculation Stops Immediately

Clicking cancel:
- Terminates all Web Workers for that panel
- Resets the panel to its pre-calculation state
- Frees CPU resources for other tasks
{% endstep %}

{% step %}
#### Recalculate When Ready

After canceling, click the refresh button (↻) to recalculate with updated parameters or simply wait for auto-update to trigger.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Canceling a calculation is safe and does not affect other panels or your saved configuration.
{% endhint %}

### Optimizing for Faster Calculations

To speed up calculations while maintaining acceptable accuracy:

**Start with Lower Resolution**
1. Set integration grid size to 50–100 for initial exploration
2. Adjust parameters and observe trends
3. Increase to 200–500 only for final publication-quality plots

**Narrow Integration Ranges**
1. Enable auto-calculation for initial ranges
2. Use the "compute data over current plot view" feature (🎯 target icon) to zoom into interesting regions
3. Recalculate with narrower manual ranges for faster iteration

**Disable Auto-Update When Exploring**
1. Click the lock icon to disable auto-update
2. Change multiple parameters without triggering recalculation
3. Manually refresh (↻) only when ready
4. Re-enable auto-update when done exploring

**Use Fewer Steps for Series Plots**
1. Start with 50–100 steps to identify features
2. Increase to 200+ steps only for final smooth curves

### Optimizing for Higher Accuracy

When you need the most accurate results:

**Increase Grid Resolution**
- Use size = 200–500 for JSI and 2D plots
- Verify convergence by comparing size = 200 vs. size = 500

**Widen Integration Ranges**
- Manually expand signal/idler wavelength ranges beyond auto-calculated values
- Check that spectral amplitude is truly zero at range boundaries

**Use More Steps in Series**
- 500+ steps for HOM dips to capture fine structure
- 200+ steps for Schmidt number vs. parameter sweeps

**Check Numerical Integration Settings**
- The default integration method works for most cases
- Verify results are stable when slightly varying integration parameters

{% hint style="warning" %}
**Balancing Speed and Accuracy**: For most applications, size = 100 provides excellent accuracy while maintaining sub-second calculation times. Only use size > 200 when preparing final publication figures or when fine spectral features are critical.
{% endhint %}

### Performance Troubleshooting

<details>
<summary>Calculations are very slow (>10 seconds)</summary>

**Possible causes**:
- Very high grid resolution (size > 300)
- Extremely wide integration ranges
- Many steps in series calculations (> 500)
- Browser running on low-power CPU or throttled

**Solutions**:
- Reduce grid size to 100–150
- Enable auto-calculated integration limits
- Reduce number of steps to 100–200
- Close other browser tabs to free resources
- Check CPU throttling in system settings
</details>

<details>
<summary>Browser becomes unresponsive during calculation</summary>

**Possible causes**:
- Very large calculations exhausting available memory
- Browser not supporting Web Workers or SharedArrayBuffer

**Solutions**:
- Reduce integration grid size
- Close other browser tabs and applications
- Use a modern browser (Chrome, Firefox, Edge, Safari 15+)
- Check that your browser supports WebAssembly threads
</details>

<details>
<summary>Calculations complete but results look wrong</summary>

**Possible causes**:
- Integration grid too coarse (size < 50)
- Integration ranges truncating spectral features
- Parameter values outside physical ranges

**Solutions**:
- Increase grid size to 100+
- Widen integration ranges or use auto-calculation
- Verify crystal parameters and wavelengths are reasonable
- Check the Info Panel for warnings about phasematching conditions
</details>

<details>
<summary>Multi-threading doesn't seem to work</summary>

**Possible causes**:
- Browser security headers blocking SharedArrayBuffer
- Running from `file://` instead of HTTPS
- Browser doesn't support multi-threading

**Solutions**:
- Access SPDCalc via HTTPS (recommended: use the official deployment)
- Check browser console for security errors
- Use Chrome, Firefox, or Edge (Safari may have limited support)
- Even without multi-threading, calculations will complete single-threaded
</details>

---

By understanding these visualization, export, and performance concepts, you can efficiently explore SPDC configurations, extract publication-quality data, and optimize your workflow for both speed and accuracy. For panel-specific interpretation details, see the **Calculation Panels Reference** section.
