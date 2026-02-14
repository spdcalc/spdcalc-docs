# Tips and Best Practices

This section provides practical guidance to help you work efficiently with SPDCalc. You'll learn when to use auto-calculation features, how to choose the right integration method for your needs, what affects calculation times, and how to troubleshoot common issues.

## When to Use Auto-Calculation

SPDCalc can automatically calculate several parameters including crystal orientation angle (theta), periodic poling period, integration wavelength limits, and beam waist positions. Understanding when to use auto-calculation versus manual control helps you work more efficiently.

### Crystal Angle Auto-Calculation

The crystal theta angle is automatically calculated to achieve optimal phasematching for your chosen wavelengths and crystal type.

{% tabs %}
{% tab title="Use Auto-Calculation When" %}
**Recommended scenarios:**

- **Exploring new configurations**: When you're starting a new design and want to find the optimal crystal angle for your pump and signal wavelengths
- **Wavelength sweeps**: When varying pump or signal wavelengths to see how the system responds
- **Quick setup**: When you want to get a working configuration quickly without manual optimization

**Example workflow:**
1. Select your crystal type (e.g., KTP)
2. Set your pump wavelength (e.g., 775 nm)
3. Set your desired signal wavelength (e.g., 1550 nm)
4. SPDCalc automatically calculates the optimal theta angle

{% hint style="success" %}
Auto-calculation is ideal for exploratory work. The calculated angle ensures phasematching conditions are satisfied for your wavelengths.
{% endhint %}
{% endtab %}

{% tab title="Override When" %}
**Manual control scenarios:**

- **Fixed experimental setup**: When you have a physical crystal already mounted at a specific angle
- **Angle sweeps**: When you want to study how JSI or Schmidt number changes with crystal angle
- **Periodic poling**: When using quasi-phasematching with a fixed poling period and need to adjust the angle
- **Reproducing published results**: When implementing a configuration from a paper with specified angles

**Example workflow:**
1. Disable "Auto Calculate" for crystal theta
2. Set theta to your fixed experimental value (e.g., 46.5°)
3. Adjust other parameters to optimize your configuration

{% hint style="warning" %}
When you manually set theta, ensure it's compatible with your wavelengths and phasematching type. Check the Info Panel to verify you achieve reasonable phasematching.
{% endhint %}
{% endtab %}
{% endtabs %}

### Periodic Poling Auto-Calculation

When quasi-phasematching is enabled, SPDCalc can automatically calculate the required poling period.

**When to use auto-calculation:**
- Starting a new quasi-phasematched design
- Exploring different wavelength combinations with periodic poling
- Finding the optimal poling period for a specific crystal angle

**When to override:**
- Your crystal has a fixed fabricated poling period
- You want to study off-optimal poling conditions
- Reproducing experimental results with a known poling period

{% hint style="info" %}
With periodic poling enabled and auto-calculation on, the crystal theta is typically set to 90° for collinear phasematching. The poling period compensates for the momentum mismatch.
{% endhint %}

### Integration Limits Auto-Calculation

Auto-calculated integration limits define the wavelength ranges over which JSI calculations are performed.

**When to use auto-calculation:**
- General exploration and initial calculations
- Ensuring you capture the full spectral content
- Working with narrow pump bandwidths where the JSI is well-localized

**When to override:**
- Zooming in on specific spectral regions for detailed analysis
- Reducing calculation time by focusing on the region of interest
- Studying edge effects or specific features in the joint spectrum

{% hint style="success" %}
The "target" icon in JSI plots lets you quickly set integration limits to match your current zoom view. This is useful for high-resolution calculations of specific regions.
{% endhint %}

**Practical example:**

<details>
<summary>Workflow: From auto-calculation to manual refinement</summary>

1. **Initial exploration**: Enable auto-calculation of integration limits
   - SPDCalc sets limits to capture the full JSI based on pump bandwidth and wavelengths
   - Perform initial calculation to see overall structure

2. **Identify region of interest**: Examine the JSI plot
   - Zoom into an interesting spectral feature
   - Note the approximate wavelength ranges

3. **Refine for detail**: Switch to manual limits
   - Disable "Auto Calculate" for integration limits
   - Set narrow signal and idler ranges around your feature of interest
   - Increase grid resolution for detailed calculation
   - Calculate high-resolution data for that specific region

4. **Export results**: Download the refined data for analysis

</details>

### Waist Position Auto-Calculation

SPDCalc can automatically calculate optimal beam waist positions for signal and idler photons.

**When to use auto-calculation:**
- Initial design work
- Finding optimal coupling positions for maximum heralding efficiency
- Understanding ideal waist placement relative to the crystal

**When to override:**
- Your experimental setup has fixed collection optics positions
- Studying how heralding efficiency varies with waist position
- Matching a specific experimental configuration

{% hint style="warning" %}
Auto-calculated waist positions are optimized for the theoretical maximum collection efficiency. Real experimental setups may have constraints that require different positions.
{% endhint %}

## Choosing Integration Methods

SPDCalc offers five numerical integration methods. Each has different trade-offs between accuracy, speed, and robustness. Choosing the right method can significantly impact both calculation time and result quality.

### Available Methods

{% tabs %}
{% tab title="Simpson (Default)" %}
**Simpson's Rule**

**Best for**: General-purpose calculations, smooth functions, quick results

**Characteristics:**
- Fixed grid with specified number of steps
- Very fast computation
- Good accuracy for smooth JSI functions
- Predictable performance

**When to use:**
- Initial exploration and parameter sweeps
- Interactive work where you need fast feedback
- Well-behaved systems (e.g., narrow pump bandwidth, simple phasematching)
- Grid calculations (JSI plots, phasematching curves)

**Configuration:**
- **Steps**: Number of integration points (typical: 50-200)
- Higher steps = more accurate but slower

{% hint style="success" %}
Simpson is excellent for interactive exploration. Start here, then switch to adaptive methods if you need higher accuracy or encounter numerical issues.
{% endhint %}

**Example settings:**
- Quick preview: 50 steps
- Standard quality: 100 steps
- High quality: 200+ steps
{% endtab %}

{% tab title="Adaptive Methods" %}
**ClenshawCurtis, GaussLegendre, GaussKonrod, AdaptiveSimpson**

**Best for**: Difficult integrals, high accuracy requirements, functions with sharp features

**Characteristics:**
- Automatically adjust resolution where needed
- Slower than fixed-grid Simpson
- Better handling of sharp spectral features
- More robust for challenging systems

**When to use:**
- Broad pump bandwidths with complex spectral structure
- High precision requirements
- Systems with sharp phasematching features
- Final calculations for publication

**Configuration:**
- **Tolerance (Tol)**: Target accuracy (typical: 1e-6 to 1e-3)
  - Smaller tolerance = higher accuracy but slower
- **Max Depth**: Maximum refinement level (typical: 1000-10000)
  - Prevents runaway computation time
- **Degree** (GaussLegendre only): Quadrature degree (typical: 20-50)

{% hint style="warning" %}
Adaptive methods can be 3-10× slower than Simpson but provide better accuracy for challenging integrals. Use them when accuracy matters more than speed.
{% endhint %}
{% endtab %}
{% endtabs %}

### Method Selection Guide

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
<td><strong>Narrow Pump BW (&lt;5 nm)</strong></td>
<td>Simpson with 100 steps works well. JSI is typically smooth and well-behaved.</td>
<td></td>
</tr>
<tr>
<td><strong>Broad Pump BW (&gt;10 nm)</strong></td>
<td>GaussLegendre or GaussKonrod. Complex spectral structure benefits from adaptive resolution.</td>
<td></td>
</tr>
<tr>
<td><strong>Interactive Exploration</strong></td>
<td>Simpson with 50-100 steps. Fast feedback for parameter adjustments.</td>
<td></td>
</tr>
<tr>
<td><strong>Final Publication Results</strong></td>
<td>GaussKonrod with Tol=1e-6. High accuracy and robust error control.</td>
<td></td>
</tr>
<tr>
<td><strong>Hong-Ou-Mandel Dips</strong></td>
<td>AdaptiveSimpson or GaussKonrod. Sharp features require adaptive methods.</td>
<td></td>
</tr>
<tr>
<td><strong>Heralding Efficiency</strong></td>
<td>GaussLegendre. Multi-dimensional integrals benefit from adaptive quadrature.</td>
<td></td>
</tr>
</tbody>
</table>

### Recommended Settings by Scenario

**Quick exploration:**
```
Method: Simpson
Steps: 50
Grid Size: 100
```
Calculation time: ~0.5-2 seconds for JSI

**Standard calculation:**
```
Method: Simpson
Steps: 100
Grid Size: 200
```
Calculation time: ~2-5 seconds for JSI

**High accuracy:**
```
Method: GaussKonrod
Tolerance: 1e-6
Max Depth: 5000
Grid Size: 300
```
Calculation time: ~10-30 seconds for JSI

**Production/Publication:**
```
Method: GaussKonrod
Tolerance: 1e-8
Max Depth: 10000
Grid Size: 500
```
Calculation time: ~30-120 seconds for JSI

{% hint style="info" %}
Start with Simpson during exploration. Switch to adaptive methods (GaussKonrod recommended) when you need to verify accuracy or calculate final results for publication.
{% endhint %}

## Understanding Calculation Time

Calculation speed depends on several factors including grid resolution, integration method, panel type, and your computer's CPU core count. Understanding these relationships helps you balance quality and performance.

### What Affects Calculation Speed

**Grid resolution** (Integration Settings → Grid Size)
- JSI calculations scale as O(N²) where N is the grid size
- Doubling grid size increases JSI calculation time by ~4×
- Typical range: 100 (fast) to 500 (slow but detailed)

**Integration method and parameters**
- Simpson: Fastest (baseline)
- Adaptive methods: 3-10× slower than Simpson
- Higher tolerance settings increase calculation time significantly

**Panel type complexity**
- Info Panel: Nearly instant (simple calculations)
- Phasematching Curves: Fast (~0.1-0.5 seconds)
- JSI Plot: Medium (~0.5-10 seconds depending on grid size)
- Schmidt Number vs Crystal Length: Slow (~5-30 seconds, many JSI calculations)
- Hong-Ou-Mandel Dip: Slow (~10-60 seconds, integrates over JSI)
- Two-Source HOM: Very slow (~30-180 seconds, most complex calculation)

**CPU core count**
- SPDCalc automatically uses all available CPU cores
- Parallelization provides near-linear speedup for batch calculations
- 2 cores: baseline
- 4 cores: ~2× faster
- 8 cores: ~4× faster
- 16+ cores: ~6-8× faster (diminishing returns due to overhead)

{% hint style="success" %}
Check your browser's task manager to see SPDCalc using multiple threads. Performance scales well with more CPU cores.
{% endhint %}

### Expected Calculation Times

The following estimates assume a modern CPU (4-8 cores) with typical settings:

**Fast calculations** (< 1 second):
- Info Panel (refractive indices, optimum idler)
- Phasematching Curves (single wavelength sweep)
- JSI with grid size 100 and Simpson method

**Medium calculations** (1-5 seconds):
- JSI with grid size 200-300 and Simpson
- Schmidt Number single point calculation
- Heralding Efficiency single point

**Slow calculations** (5-30 seconds):
- JSI with grid size 500 and Simpson
- JSI with adaptive methods and moderate grid size
- Schmidt Number vs Pump Bandwidth (20-50 points)
- Hong-Ou-Mandel Dip with 100-200 time steps

**Very slow calculations** (30+ seconds):
- Two-Source HOM with high resolution
- Parameter sweeps with many points and high grid resolution
- Heralding Efficiency histograms with fine grids
- High-precision adaptive integration with tight tolerance

{% hint style="info" %}
Calculation times are displayed in panel status bars after completion (e.g., "calculated in 2.4s"). Use these to gauge performance for your specific system configuration.
{% endhint %}

### Optimizing for Interactive Exploration vs Final Results

{% tabs %}
{% tab title="Interactive Exploration" %}
**Goal**: Fast feedback while adjusting parameters

**Recommended settings:**
- Grid Size: 100-150
- Integration Method: Simpson
- Steps: 50-100
- Auto-update: Enabled

**Workflow:**
1. Start with low resolution settings
2. Enable auto-update so calculations happen automatically when you change parameters
3. Adjust parameters and observe trends
4. Disable auto-update when running slow calculations to prevent interruption
5. Once you find an interesting configuration, increase resolution for detailed analysis

**Typical response time:** < 1 second per parameter change

{% hint style="success" %}
The auto-update feature works best with fast settings. If calculations take more than a few seconds, consider disabling auto-update and manually refreshing panels.
{% endhint %}
{% endtab %}

{% tab title="Final Results" %}
**Goal**: Publication-quality accuracy and detail

**Recommended settings:**
- Grid Size: 300-500
- Integration Method: GaussKonrod or GaussLegendre
- Tolerance: 1e-6 to 1e-8
- Max Depth: 5000-10000
- Auto-update: Disabled

**Workflow:**
1. Use interactive settings to optimize your configuration
2. Disable auto-update to prevent accidental recalculation
3. Change to high-resolution settings
4. Manually trigger calculation using the refresh button
5. Wait for completion (monitor status bar for progress)
6. Export data as CSV for further analysis or plotting in external tools

**Typical calculation time:** 10-60 seconds depending on panel type

{% hint style="warning" %}
Always disable auto-update before switching to high-resolution settings. Otherwise, any parameter adjustment will trigger a slow recalculation.
{% endhint %}
{% endtab %}
{% endtabs %}

### Performance Tips

**Reduce grid size when possible**
- Use auto-calculated integration limits to avoid unnecessarily large spectral ranges
- Zoom to your region of interest and use the target icon to focus calculations
- For parameter sweeps, start with coarse grids to identify interesting regions

**Use panel-specific optimizations**
- For Schmidt Number vs parameter plots: Reduce the number of sweep points initially
- For HOM dips: Reduce JSI resolution setting if the dip structure is smooth
- For heralding histograms: Start with coarse waist ranges, then refine

**Cancel slow calculations**
- Use the cancel button (X) in panel toolbars to stop in-progress calculations
- Useful when you realize settings are too high-resolution or you want to change parameters
- Panels will reset and be ready for new calculations immediately

**Batch your work**
- Set up multiple panels with different configurations
- Disable auto-update on all panels
- Configure all settings first
- Trigger calculations in sequence
- Panels calculate in parallel when possible, utilizing all CPU cores

<details>
<summary>Why does grid size have such a large impact on JSI calculations?</summary>

The Joint Spectrum Intensity is calculated on a 2D grid of signal and idler wavelengths. For a grid size N:
- Total grid points: N × N
- For N=100: 10,000 points
- For N=500: 250,000 points

Each grid point requires evaluating integrals over pump spectrum and crystal properties. This quadratic scaling means doubling the resolution quadruples the number of calculations needed.

Additionally, some calculations (like Schmidt decomposition) perform SVD on the JSI matrix, which scales as O(N³), making very high resolutions computationally expensive.

</details>

## Troubleshooting Common Issues

This section covers common problems you may encounter and how to resolve them.

### Slow or Unresponsive Calculations

**Symptom**: Calculations take a very long time or the browser becomes unresponsive.

**Common causes and solutions:**

{% hint style="warning" %}
**Grid size too high**

Check your grid size in Integration Settings. Values above 500 can cause very slow calculations, especially with adaptive integration methods.

**Solution**: Reduce grid size to 100-300 for interactive work. Use high resolution (400-500) only for final results with auto-update disabled.
{% endhint %}

{% hint style="warning" %}
**Too many calculation steps**

Parameter sweep panels (Schmidt number vs length, HOM dips) with many steps can take minutes to complete.

**Solution**: Reduce the "Steps" parameter in the panel settings. Start with 20-50 steps, increase only if needed.
{% endhint %}

**Integration method too precise**

Adaptive methods with very tight tolerance (< 1e-8) can dramatically increase computation time.

**Solution**: Use tolerance of 1e-6 for most work. Reserve tighter tolerances for final validation.

**Multiple panels auto-updating**

Having several panels with auto-update enabled can trigger many parallel calculations when you change parameters.

**Solution**: Disable auto-update on panels you're not actively using. Enable it only on the panel you're currently analyzing.

**Insufficient browser resources**

Very complex calculations may approach browser memory limits.

**Solution**:
- Close other browser tabs
- Restart your browser periodically
- Use a modern browser with good WebAssembly performance (Chrome, Edge, or Firefox recommended)

### Unexpected or Incorrect Results

**Symptom**: Calculated values seem wrong, plots are empty, or results don't match expectations.

{% hint style="danger" %}
**Phasematching conditions not satisfied**

If your crystal angle, wavelengths, and phasematching type are incompatible, calculations may produce near-zero results or strange patterns.

**Check**: Look at the Info Panel → Optimum Idler section. If the optimum idler wavelength is very different from your signal wavelength, phasematching may not be achievable.

**Solution**:
- Enable auto-calculation for crystal theta
- Verify your pump and signal wavelengths are compatible with your crystal type
- Check that phasematching type (Type 0/1/2) is appropriate for your configuration
{% endhint %}

**Integration limits too narrow**

If integration limits don't encompass the JSI, you'll see truncated or incomplete results.

**Check**: Enable auto-calculation for integration limits temporarily to see the recommended range.

**Solution**: Widen signal and idler integration ranges, or enable auto-calculation.

**Grid resolution too coarse**

Low grid resolution can miss sharp spectral features or produce blocky JSI plots.

**Solution**: Increase grid size to 200-300. For very narrow features, use 400-500.

**Numerical precision issues**

Extremely small or large parameter values can cause numerical instabilities.

**Check**:
- Pump power is typically 1 (normalized)
- Crystal length is in micrometers (typical: 100-20000 µm)
- Wavelengths are in nanometers (typical: 400-5000 nm)
- Waist sizes are reasonable (typical: 10-500 µm)

**Solution**: Verify units and typical value ranges. Extreme values may require adjusting integration tolerances.

### Browser Compatibility Issues

**Symptom**: Application doesn't load, calculations don't run, or performance is poor.

{% hint style="info" %}
**Recommended browsers**

SPDCalc requires modern browser features including WebAssembly and Web Workers. For best performance use:
- Chrome 90+ (recommended)
- Edge 90+ (recommended)
- Firefox 89+
- Safari 15.2+
{% endhint %}

**WebAssembly not supported**

Older browsers may not support WebAssembly or multi-threaded WASM.

**Solution**: Update your browser to the latest version. If you must use an older browser, SPDCalc may fall back to slower JavaScript implementations.

**Performance issues on Safari**

Safari's WebAssembly implementation may be slower than Chrome/Firefox.

**Solution**: For best performance, use Chrome or Edge. Safari is supported but may be 20-50% slower.

**Cross-origin isolation warnings**

Some browsers show warnings about cross-origin isolation required for SharedArrayBuffer.

**This is normal**: SPDCalc requires these headers to enable multi-threaded calculations. The warnings can be ignored.

**Mobile browsers**

SPDCalc works on tablets and phones but performance is limited by mobile CPU capabilities.

**Recommendation**: Use a desktop or laptop for best experience. On mobile, reduce grid size and use Simpson integration for acceptable performance.

### Error Messages and Their Meanings

**"No poling period needed for given setup"**

**Meaning**: Your configuration achieves phasematching through birefringent phasematching, so periodic poling is unnecessary.

**Action**: This is informational. You can disable periodic poling or adjust the crystal theta angle if quasi-phasematching is desired.

**"Operation not permitted" or worker initialization failures**

**Meaning**: Browser security restrictions or extension interference.

**Solutions**:
- Disable browser extensions that block workers or WebAssembly
- Check that your browser allows workers for the SPDCalc site
- Try in an incognito/private window to rule out extension conflicts
- Clear browser cache and reload

**"Calculation timeout" or similar**

**Meaning**: The calculation took longer than allowed time limits.

**Solutions**:
- Reduce grid size or integration steps
- Use a faster integration method (Simpson instead of adaptive)
- Cancel and retry with lower resolution settings

**Empty or zero results**

**Meaning**: The calculation completed but produced negligible values, often due to phasematching issues.

**Check**:
1. Info Panel → verify refractive indices are reasonable (> 1)
2. Phasematching Curves → ensure there's a visible phasematching peak
3. Parameter ranges → verify wavelengths and angles are physically reasonable

**Solution**: Enable auto-calculation features to find a valid configuration, then manually adjust as needed.

### Data Export Issues

**Downloaded CSV is empty or malformed**

**Cause**: Calculation didn't complete before export, or browser blocked the download.

**Solution**:
- Wait for calculation to complete (check status bar shows "calculated in X.Xs")
- Allow pop-ups/downloads from SPDCalc in browser settings
- Try export again after successful calculation

**CSV values seem incorrect**

**Check**: Some panels export complex data (e.g., JSI exports 2D arrays as flattened rows). Refer to column headers to understand the data structure.

### Configuration Issues

**Preset won't load or gives errors**

**Cause**: Preset may be from an older version of SPDCalc or corrupted.

**Solution**:
- Try loading the default preset
- If you have a shareable URL, use that instead of the preset file
- Re-create the configuration manually

**Shared URL doesn't load correctly**

**Cause**: Very long URLs (>60KB) may be truncated by some browsers, especially Firefox.

**Solution**:
- Use preset export/import for complex configurations instead of URLs
- Simplify panel setup before sharing (remove extra panels)
- Share configuration as JSON file instead of URL

**Parameters reset unexpectedly**

**Cause**: Auto-calculation features may be overriding your manual values.

**Solution**: Disable auto-calculation for parameters you want to control manually. Check the parameter input - it will show as "display only" if auto-calculation is enabled.

### Getting Additional Help

If you encounter issues not covered here:

1. **Check the Info Panel**: Often reveals configuration problems (impossible wavelengths, bad phasematching, etc.)
2. **Try default settings**: Load a default preset to verify the application is working correctly
3. **Report bugs**:
   - UI issues: https://github.com/spdcalc/spdcalc-ui/issues
   - Calculation issues: https://github.com/spdcalc/spdcalc/issues
4. **Share your configuration**: Export as JSON or URL to help others reproduce the issue

{% hint style="success" %}
When reporting bugs, include your browser version, operating system, and a shareable configuration URL or JSON export. This helps developers reproduce and fix issues quickly.
{% endhint %}
