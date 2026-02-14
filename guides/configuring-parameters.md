# Configuring SPDC Parameters

Parameter settings are organized into logical groups in the left settings drawer, allowing you to define your crystal properties, laser configuration, collection optics, and calculation parameters.

This section covers all parameter configuration options and explains how to use auto-calculation features to optimize your setup.

## Crystal Settings

Crystal settings define the fundamental properties of your nonlinear crystal and its orientation for phasematching.

<figure>
<img src="../.gitbook/assets/screenshots/settings/crystal-settings-panel.png" alt="Crystal settings panel">
<figcaption>Crystal configuration controls including type, phasematching, orientation, and physical properties</figcaption>
</figure>

### Crystal Type

Select your nonlinear crystal from the dropdown menu. SPDCalc supports a wide range of common SPDC crystals including:

- KTP (Potassium Titanyl Phosphate)
- BBO (Beta Barium Borate)
- BiBO (Bismuth Triborate)
- LiIO3 (Lithium Iodate)
- AgGaS2 (Silver Gallium Sulfide)
- ... and more!

{% hint style="info" %}
**NEW:** You can define your own crystal by specifying data points for its effective index of refraction at a series of wavelengths.
{% endhint %}

### Phasematching Type

Choose the phasematching configuration that matches your experimental setup:

- **Type 0: o ⇒ o + o** - Ordinary pump to ordinary signal and idler
- **Type 0: e ⇒ e + e** - Extraordinary pump to extraordinary signal and idler
- **Type 1: e ⇒ o + o** - Extraordinary pump to ordinary signal and idler
- **Type 2: e ⇒ e + o** - Extraordinary pump to extraordinary signal and ordinary idler
- **Type 2: e ⇒ o + e** - Extraordinary pump to ordinary signal and extraordinary idler

### Crystal Orientation

**Theta (θ)** - The crystal azimuthal angle in degrees [0°, 180°)

This is the angle between the crystal's optical axis and the pump beam propagation direction. Crystal theta is the primary parameter for achieving phasematching without periodic poling.

{% tabs %}
{% tab title="Auto-Calculate" %}
When the auto-calculation toggle (magic wand icon) is enabled, SPDCalc automatically calculates the optimal theta angle for phasematching based on your pump and signal wavelengths. This is recommended for initial setup.

The auto-calculation sets theta to 90° when periodic poling is enabled, as quasi-phasematching does not require angle tuning.
{% endtab %}

{% tab title="Manual Entry" %}
Disable auto-calculation to manually specify the crystal angle. This is useful when:
- You have a fixed crystal mount at a specific angle
- You want to explore off-phasematched conditions
- You're studying angle-dependent properties

Enter the angle in degrees. The field will highlight if the value is outside the valid range.
{% endtab %}
{% endtabs %}

**Phi (ϕ)** - The crystal polar angle in degrees [0°, 360°)

This parameter defines the azimuthal rotation around the pump beam axis. For most collinear SPDC configurations, phi remains at 0° and affects the orientation of signal/idler emission cones in non-collinear geometries.

### Physical Properties

**Length (L)** - Crystal length in micrometers (µm)

The interaction length of the crystal determines the spectral bandwidth and spatial characteristics of the generated photon pairs. Longer crystals produce narrower spectral bandwidths but may increase spatial walk-off effects.

Typical values range from 500 µm to 50 mm (50,000 µm) depending on your application:
- Short crystals (< 1 mm): Broader bandwidth, suitable for ultrafast applications
- Medium crystals (1-10 mm): Balanced bandwidth and brightness
- Long crystals (> 10 mm): Narrow bandwidth, high brightness

**Temperature (T)** - Crystal temperature in degrees Celsius (°C)

Temperature affects the refractive indices through the Sellmeier equations and can be used for fine-tuning phasematching conditions. Most crystals are operated at room temperature (20-25°C), but temperature tuning can provide additional control.

Minimum value: -273.15°C (absolute zero)

{% hint style="warning" %}
Large temperature changes may require recalculating phasematching conditions. The auto-calculation feature will automatically adjust crystal theta when temperature changes.
{% endhint %}

**deff** - Effective nonlinear coefficient in pm/V

The effective nonlinear coefficient characterizes the strength of the second-order nonlinear interaction. This value depends on both the crystal material and the phasematching type.

Default value is 1 pm/V. For accurate calculations, consult your crystal's datasheet for the deff value corresponding to your chosen phasematching configuration and wavelengths.

## Pump Configuration

Pump settings define the properties of the laser used to generate photon pairs through the SPDC process.

<figure>
<img src="../.gitbook/assets/screenshots/settings/pump-configuration-panel.png" alt="Pump configuration panel">
<figcaption>Pump laser parameters including wavelength, bandwidth, beam profile, and power</figcaption>
</figure>

### Wavelength

The central wavelength of the pump laser in nanometers (nm). This value must be less than the signal wavelength due to energy conservation (ω_pump = ω_signal + ω_idler).

Common pump wavelengths:
- 405 nm (violet diode laser)
- 532 nm (frequency-doubled Nd:YAG)
- 775 nm (Ti:Sapphire laser)
- 1064 nm (Nd:YAG fundamental)

Changing the pump wavelength automatically triggers recalculation of:
- Crystal phasematching angle (if auto-calculation is enabled)
- Integration wavelength ranges
- Refractive indices

### Bandwidth FWHM

The full-width at half-maximum spectral bandwidth of the pump laser in nanometers (nm).

This parameter critically affects the spectral correlations of the generated photon pairs:
- **Narrow bandwidth** (< 0.1 nm): Strong spectral correlations, high entanglement
- **Medium bandwidth** (0.1-10 nm): Balanced spectral properties
- **Broad bandwidth** (> 10 nm): Weak spectral correlations, broader JSI

Minimum value: 1e-6 nm (essentially monochromatic)

{% hint style="info" %}
The pump bandwidth directly impacts the Schmidt number, which quantifies the spectral entanglement of photon pairs. Narrower pump bandwidths typically result in higher Schmidt numbers.
{% endhint %}

### Waist 1/e²

The beam waist (radius at 1/e² intensity) of the pump beam in micrometers (µm).

The pump waist determines:
- Spatial mode matching with signal/idler collection modes
- Rayleigh range and focusing conditions
- Collection efficiency in fiber-coupled systems

{% hint style="warning" %}
The paraxial approximation used in SPDCalc requires that the waist size be much larger than the wavelength divided by the refractive index. A warning appears if your waist is too small for the approximation to be valid (W << 20λ/n).
{% endhint %}

Typical values range from 20 µm to 500 µm depending on your focusing optics and crystal length.

### Spectrum Cutoff

A dimensionless threshold value (exponential notation) that sets the minimum pump spectrum amplitude to include in calculations.

When the pump's spectral amplitude falls below this threshold, the joint spectral intensity (JSI) is assumed to be zero at those wavelengths. This optimization speeds up calculations by ignoring negligible contributions.

Default value: 1e-2 (1%)
- Higher values (e.g., 1e-1): Faster calculation, may miss weak spectral features
- Lower values (e.g., 1e-4): More accurate, slower calculation

{% hint style="info" %}
If you're seeing unexpected cutoffs in your JSI plots, try decreasing the spectrum cutoff value to include more of the pump spectral wings.
{% endhint %}

### Power

The pump laser power in milliwatts (mW). This parameter is used for calculating:
- Absolute coincidence count rates in the Heralding Calculator
- Brightness estimates for the SPDC source
- Pair generation rates

Typical values range from 0.1 mW to 1000 mW (1 W), depending on your laser and experimental requirements.

### Refractive Index (np)

This read-only field displays the calculated refractive index of the pump beam in the crystal. The value is automatically computed using the crystal's Sellmeier equations at the specified wavelength, temperature, and polarization (determined by phasematching type).

The refractive index is used internally for:
- Phasematching calculations
- Walk-off angle corrections
- Beam propagation modeling

## Signal Configuration

Signal settings define the wavelength and spatial mode properties of the signal photon (one of the two photons in the down-converted pair).

<figure>
<img src="../.gitbook/assets/screenshots/settings/signal-configuration-panel.png" alt="Signal configuration panel">
<figcaption>Signal photon parameters including wavelength, collection angles, and spatial mode configuration</figcaption>
</figure>

### Counter Propagation

Enable this toggle for counter-propagating SPDC configurations where signal and idler photons are emitted in opposite directions. This is less common than co-propagating (collinear or non-collinear) configurations.

In standard collinear SPDC, leave this disabled.

### Wavelength

The signal photon wavelength in nanometers (nm). This value must be greater than the pump wavelength due to energy conservation.

The idler wavelength is automatically calculated from energy conservation:
```
1/λ_idler = 1/λ_pump - 1/λ_signal
```

Common signal wavelengths for telecommunications applications:
- 1550 nm (C-band telecom)
- 1310 nm (O-band telecom)
- 810 nm (common for quantum networking with Rb atomic transitions)

Changing the signal wavelength triggers automatic recalculation of:
- Crystal phasematching angle
- Idler wavelength and properties
- Integration limits
- Refractive indices

### Waist 1/e²

The signal beam waist (radius at 1/e² intensity) in micrometers (µm).

This parameter defines the spatial mode of signal photon collection, typically matching the mode of your single-mode fiber or spatial filter. The waist size affects:
- Spatial mode matching with the generated SPDC modes
- Heralding efficiency
- Coincidence count rates

{% hint style="warning" %}
A warning appears if the signal waist violates the paraxial approximation (W < 20λ/n). Consider increasing the waist size or verifying that your experimental conditions match the calculation assumptions.
{% endhint %}

### Collection Angles

**Theta (θ)** - Signal azimuthal angle in degrees [-180°, 180°]

The angle between the signal photon collection direction and the pump beam axis. For collinear SPDC, this is typically 0°.

{% hint style="warning" %}
The phasematching algorithms use a small-angle approximation for signal and idler angles. For accurate results, keep signal theta within ±10° of the pump direction.
{% endhint %}

**Phi (ϕ)** - Signal polar angle in degrees [0°, 360°]

The azimuthal angle around the pump beam. This field is currently disabled as most calculations assume signal and idler are in the same plane (phi = 0°).

### Waist Positions

**Signal Focus** - Signal beam waist position in micrometers (µm)

The z-position of the signal beam waist along the crystal axis, measured from the end of the crystal. This parameter enables optimization of spatial mode matching between the pump and collection modes.

{% tabs %}
{% tab title="Auto-Calculate" %}
When auto-calculation is enabled (magic wand icon), SPDCalc determines the optimal signal focus position for maximum mode overlap with the SPDC emission.
{% endtab %}

{% tab title="Manual Entry" %}
Disable auto-calculation to specify a custom waist position. This is useful when modeling:
- Specific experimental configurations with fixed focusing optics
- Off-optimum collection geometries
- Fiber coupling at specific positions
{% endtab %}
{% endtabs %}

**Idler Focus** - Idler beam waist position in micrometers (µm)

Similar to signal focus, but for the idler photon. The idler parameters are typically symmetric with the signal in collinear degenerate SPDC but can differ for non-degenerate or non-collinear configurations.

### Refractive Indices

**ns** and **ni** - Signal and idler refractive indices (read-only)

These fields display the calculated refractive indices for signal and idler wavelengths at the current crystal temperature and phasematching configuration. Values are computed automatically using the crystal's Sellmeier equations.

### Optimum Idler

This section displays the calculated properties of the idler photon at perfect phasematching conditions:

**Wavelength** - Optimum idler wavelength in nanometers (nm)

The idler wavelength is determined by energy conservation from the pump and signal wavelengths. This is shown with 2 significant figures.

**Theta (θ) and Phi (ϕ)** - Optimum idler emission angles

The angles at which the idler photon is emitted for perfect phasematching. These values are calculated from momentum conservation and crystal properties.

{% hint style="info" %}
The optimum idler parameters are useful for aligning collection optics and understanding the geometric properties of your SPDC source. In collinear degenerate SPDC, the idler angle should be very close to the signal angle.
{% endhint %}

## Periodic Poling Settings

Periodic poling enables quasi-phasematching (QPM) in crystals where birefringent phasematching is not possible or optimal. This is particularly useful in materials like PPKTP (periodically-poled KTP).

<figure>
<img src="../.gitbook/assets/screenshots/settings/periodic-poling-panel.png" alt="Periodic poling settings panel">
<figcaption>Quasi-phasematching configuration including poling period and apodization options</figcaption>
</figure>

### Periodic Poling Toggle

Enable this option to activate quasi-phasematching through periodic poling. When enabled:
- The crystal structure is assumed to have alternating χ⁽²⁾ domains
- Phasematching can be achieved at crystal angles where birefringent phasematching is not possible
- If auto-calculation is enabled for crystal theta, it will be set to 90° (normal incidence)

Leave this disabled for standard birefringent phasematching in unpoled crystals.

### Poling Period

The period of the alternating domain structure in micrometers (µm), shown with 5 significant figures for precision.

The poling period compensates for the wavevector mismatch (Δk) and enables phasematching:
```
Λ = 2π/Δk
```

{% tabs %}
{% tab title="Auto-Calculate" %}
When auto-calculation is enabled (requires periodic poling to be active), SPDCalc computes the required poling period based on your wavelengths, crystal type, and phasematching type.

If the calculation returns zero or an error, it indicates that no poling period can achieve phasematching for the current configuration. Try adjusting the crystal theta angle or wavelengths.
{% endtab %}

{% tab title="Manual Entry" %}
Disable auto-calculation to specify a custom poling period. This is necessary when:
- You have a pre-fabricated periodically-poled crystal with a fixed period
- You want to explore quasi-phasematching at multiple orders
- You're designing a new poled crystal structure

The field displays "∞" when periodic poling is disabled, indicating infinite period (no poling).
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you see "(error)" in the poling period field, the auto-calculation could not find a valid poling period. This often means the current wavelength and angle combination cannot be phasematched with quasi-phasematching in the selected crystal.
{% endhint %}

### Apodization

Apodization applies a gradual variation to the poling duty cycle along the crystal length, which can be used to engineer the spectral properties of the SPDC emission.

**Apodization Toggle** - Enable or disable apodization (requires periodic poling to be active)

When enabled, you can select different apodization profiles that modify the effective nonlinearity along the crystal.

### Apodization Type

Choose from several standard apodization window functions:

- **Gaussian** - Smooth Gaussian envelope, reduces spectral side-lobes
- **Bartlett** - Triangular window (linear taper)
- **Blackman** - Minimizes side-lobes at the cost of main lobe width
- **Connes** - Cosine-squared window
- **Cosine** - Simple cosine taper
- **Hamming** - Raised cosine window, good side-lobe suppression
- **Welch** - Parabolic window
- **Interpolate** - Custom apodization defined by user-specified points

For detailed information on apodization functions, see the [MathWorld reference](https://mathworld.wolfram.com/ApodizationFunction.html).

### Apodization Parameters

**FWHM** (for Gaussian apodization) - Full-width at half-maximum in micrometers (µm)

When Gaussian apodization is selected, this parameter sets the width of the Gaussian envelope. The FWHM should typically be comparable to or slightly larger than the crystal length for smooth tapering.

**a** (for other apodization types) - Dimensionless parameter

For non-Gaussian apodization functions (except Interpolate), this parameter modifies the shape of the window function. The meaning depends on the specific window type:
- Blackman: Controls the zero-frequency coefficient
- Hamming: Modifies the raised-cosine weight

Consult the MathWorld reference for specific parameter meanings for each window type.

### Custom Apodization (Interpolate)

When "Interpolate" is selected, click the button showing the number of specified points to open a dialog where you can define a custom apodization profile.

Enter comma-separated values representing the apodization strength at evenly-spaced points along the crystal. The values are linearly interpolated between points.

Example: `1.0, 0.9, 0.7, 0.5, 0.7, 0.9, 1.0` creates a dip in the middle of the crystal.

{% hint style="warning" %}
At least 2 points must be specified for interpolation to work. The button displays in yellow if fewer than 2 points are defined.
{% endhint %}

## Integration Settings

Integration settings control the numerical calculation of the joint spectral intensity (JSI) and other integrated quantities. These parameters balance calculation accuracy against computation time.

<figure>
<img src="../.gitbook/assets/screenshots/settings/integration-settings-panel.png" alt="Integration settings panel">
<figcaption>Numerical integration method and wavelength range controls</figcaption>
</figure>

### Integration Method

Select the numerical integration algorithm used for computing the JSI:

**Simpson** - Simpson's rule composite integration
- Simple, fast, and robust
- Fixed grid spacing
- Best for smooth functions
- Recommended for most users

**ClenshawCurtis** - Clenshaw-Curtis quadrature
- Spectral method using Chebyshev polynomials
- Adaptive accuracy
- Excellent for smooth, well-behaved functions

**GaussLegendre** - Gauss-Legendre quadrature
- High accuracy for polynomial integrands
- Configurable degree (number of quadrature points)
- Good balance of speed and accuracy

**GaussKonrod** - Gauss-Kronrod adaptive quadrature
- Adaptive refinement for difficult integrals
- Automatic error estimation
- Slower but more robust for oscillatory or sharp features

**AdaptiveSimpson** - Adaptive Simpson's rule
- Automatically refines grid in regions of rapid change
- Good for functions with localized features
- Balance between Simpson and fully adaptive methods

{% hint style="info" %}
For most SPDC calculations, the default Simpson method provides a good balance of speed and accuracy. Consider adaptive methods (GaussKonrod or AdaptiveSimpson) if you observe artifacts in your JSI plots or are working with very narrow spectral features.
{% endhint %}

### Method-Specific Parameters

**Steps** (Simpson only) - Number of integration steps

Controls the grid resolution for Simpson's rule. More steps give higher accuracy but slower calculation.
- Minimum: 5 steps
- Typical: 50-200 steps
- High accuracy: 500+ steps

**Tolerance** (Adaptive methods) - Integration error tolerance

Sets the target accuracy for adaptive integration methods. Specified in exponential notation (e.g., 1e5).
- Larger values (e.g., 1e6): Faster, less accurate
- Smaller values (e.g., 1e4): Slower, more accurate
- Range: 1e-50 to 1e50

**Max Depth** (Adaptive methods) - Maximum recursion depth

Limits how many times the integration region can be subdivided. Higher values allow more refinement but increase computation time.
- Minimum: 10
- Typical: 1000-10000
- Maximum: Limited by computational resources

**Degree** (GaussLegendre only) - Quadrature degree

The number of quadrature points in the Gauss-Legendre scheme. Higher degree provides better accuracy for polynomial-like functions.
- Minimum: 2
- Typical: 20-60
- Higher values: More accurate but slower

### Grid Size (Resolution)

The number of grid points in each dimension for 2D JSI calculations. This parameter has a significant impact on both accuracy and computation time.

The total number of calculated points is (Grid Size)², so doubling the resolution quadruples the computation time.

Recommended values:
- **Quick preview**: 50-100 (2,500-10,000 points)
- **Standard**: 100-200 (10,000-40,000 points)
- **High resolution**: 200-500 (40,000-250,000 points)
- **Publication quality**: 500+ (250,000+ points)

{% hint style="warning" %}
Large grid sizes (> 500) can result in long calculation times, especially with adaptive integration methods. See the [Performance Considerations](../working-with-results.md#performance-considerations) section for optimization strategies.
{% endhint %}

### Auto Calculate Integration Limits

Enable this toggle to automatically determine appropriate wavelength ranges for the JSI calculation based on your pump bandwidth and crystal properties.

{% tabs %}
{% tab title="Auto-Calculate Enabled" %}
SPDCalc analyzes the pump spectrum and phasematching conditions to estimate where the JSI has significant amplitude. The signal and idler ranges are set to capture the relevant spectral features with some margin.

The range fields are read-only (display only) when auto-calculation is enabled. Values update automatically when you change pump bandwidth, wavelengths, or other parameters affecting the JSI extent.

This is recommended for initial setup and when exploring new parameter regimes.
{% endtab %}

{% tab title="Manual Entry" %}
Disable auto-calculation to specify custom integration ranges. This is useful when:
- You want to zoom in on specific spectral regions
- You're generating plots for publication and need specific axis limits
- The auto-calculated range is too large or too small for your needs
- You want to reduce computation time by limiting the integration domain

Enter the minimum and maximum wavelengths manually for signal and idler ranges.
{% endtab %}
{% endtabs %}

### Signal Range

**Minimum** and **Maximum** - Signal wavelength integration range in nanometers (nm)

Defines the wavelength limits for the signal photon in JSI calculations. The range should encompass the spectral region where the JSI has significant amplitude.

When auto-calculation is enabled, these values are determined automatically. When disabled, you can enter custom values with 2 significant figures precision.

### Idler Range

**Minimum** and **Maximum** - Idler wavelength integration range in nanometers (nm)

Defines the wavelength limits for the idler photon in JSI calculations. Like the signal range, this should cover the spectral region of interest.

{% hint style="info" %}
For degenerate SPDC (signal and idler at the same wavelength), the signal and idler ranges will be identical or very similar. For non-degenerate SPDC, the ranges will be centered at different wavelengths according to energy conservation.
{% endhint %}

## Auto-Calculation Features

SPDCalc includes several auto-calculation features (indicated by magic wand icons) that automatically compute optimal parameter values as you change other settings. Understanding these features helps you work more efficiently.

<figure>
<img src="../.gitbook/assets/screenshots/settings/auto-calculation-controls.png" alt="Auto-calculation toggle controls">
<figcaption>magic wand icons indicate auto-calculated parameters that can be manually overridden</figcaption>
</figure>

### How Auto-Calculation Works

Parameters with a magic wand icon can operate in two modes:

**Auto-Calculate Mode** (magic wand highlighted in yellow)
- The parameter is automatically recalculated when relevant settings change
- The input field is read-only
- The calculated value is always optimal for current conditions
- Recommended for initial exploration and parameter optimization

**Manual Override Mode** (magic wand not highlighted)
- Click the magic wand to disable auto-calculation
- The input field becomes editable
- You can specify exact values regardless of other parameters
- Useful for matching experimental constraints or exploring specific configurations

{% hint style="info" %}
When a parameter is in auto-calculate mode, you'll see "(auto-calculating)" in the tooltip when hovering over the field. The value updates automatically whenever dependencies change.
{% endhint %}

### Auto-Calculated Parameters

**Crystal Theta (θ)**
- **Depends on**: Pump wavelength, signal wavelength, crystal type, phasematching type, temperature
- **Calculates**: The crystal angle that achieves perfect phasematching
- **Special behavior**: Sets to 90° when periodic poling is enabled and auto-calculated

**Poling Period (Λ)**
- **Depends on**: Pump wavelength, signal wavelength, crystal type, crystal theta, phasematching type
- **Calculates**: The quasi-phasematching period needed for phasematching
- **Requirements**: Only available when periodic poling is enabled
- **Error conditions**: Displays "(error)" if no valid poling period exists for current settings

**Signal Focus Position**
- **Depends on**: Pump waist, signal waist, crystal length, wavelengths
- **Calculates**: The optimal signal waist position for maximum mode overlap

**Idler Focus Position**
- **Depends on**: Pump waist, idler properties, crystal length, wavelengths
- **Calculates**: The optimal idler waist position for maximum mode overlap

**Integration Limits** (Signal and Idler Ranges)
- **Depends on**: Pump wavelength, pump bandwidth, signal wavelength, crystal properties
- **Calculates**: Wavelength ranges that capture significant JSI amplitude
- **Includes**: Automatic margin around predicted features

### When to Use Auto-Calculation

{% tabs %}
{% tab title="Recommended Uses" %}
Auto-calculation is ideal when:

- **Initial setup**: Let SPDCalc find optimal starting parameters
- **Parameter exploration**: Quickly see how changing wavelengths or crystal type affects phasematching
- **Learning**: Understand relationships between parameters
- **Prototyping**: Design a new SPDC source without a fixed configuration
- **Comparison studies**: Evaluate different crystal types or wavelengths with optimal parameters for each
{% endtab %}

{% tab title="Manual Override Uses" %}
Disable auto-calculation when:

- **Matching hardware**: Your crystal is mounted at a fixed angle
- **Fixed fabrication**: You have a pre-fabricated periodically-poled crystal with a specific period
- **Controlled studies**: You want to study phasematching as a function of angle
- **Specific design**: You're modeling an existing experimental setup
- **Custom optics**: Your collection optics determine the focus positions
{% endtab %}
{% endtabs %}

### Auto-Calculation Dependencies

The auto-calculation system monitors parameter changes and automatically updates dependent values. Understanding these dependencies helps you predict what will change when you modify a parameter:

**When you change pump wavelength:**
- Crystal theta (if auto-calculated)
- Poling period (if auto-calculated)
- Integration limits (if auto-calculated)
- Refractive indices (always updated)
- Optimum idler properties (always updated)

**When you change signal wavelength:**
- Crystal theta (if auto-calculated)
- Poling period (if auto-calculated)
- Integration limits (if auto-calculated)
- Idler wavelength (always calculated from energy conservation)
- Refractive indices (always updated)
- Optimum idler properties (always updated)

**When you enable periodic poling:**
- Crystal theta (if auto-calculated) → set to 90°
- Poling period auto-calculation becomes available

**When you change pump bandwidth:**
- Integration limits (if auto-calculated) → widened or narrowed to match spectrum

{% hint style="warning" %}
Auto-calculations happen in sequence and may take a moment to complete for complex configurations. Wait for the calculations to finish (loading indicators will disappear) before exporting data or screenshots.
{% endhint %}

### Viewing Calculated Dependencies

Several read-only fields display automatically calculated values that always update:

- **Refractive indices** (np, ns, ni): Always calculated from Sellmeier equations
- **Optimum idler wavelength**: Always calculated from energy conservation
- **Optimum idler angles**: Always calculated from momentum conservation

These values provide immediate feedback about your configuration and help verify that parameters are physically reasonable.

---

With these parameter configuration tools, you can fully define your SPDC system for accurate simulation. Next, proceed to [Working with Calculation Panels](working-with-panels.md) to visualize and analyze your configured system.
