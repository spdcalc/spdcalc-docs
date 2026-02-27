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

**Theta (θ)** - The crystal polar angle in degrees [0°, 180°)

This is the angle between the crystal's z axis and the pump beam propagation direction (the lab z axis). Crystal theta is the primary parameter for achieving phasematching without periodic poling.

{% tabs %}
{% tab title="Auto-Calculate" %}
When the auto-calculation toggle (magic wand icon) is enabled, SPDCalc automatically calculates the optimal theta angle for phasematching based on your pump and signal wavelengths.

The auto-calculation sets theta to 90° when periodic poling is enabled.
{% endtab %}

{% tab title="Manual Entry" %}
Disable auto-calculation to manually specify the crystal angle. This is useful when:
- You have a fixed crystal mount at a specific angle
- You want to explore off-phasematched conditions
- You're studying angle-dependent properties
{% endtab %}
{% endtabs %}

**Phi (ϕ)** - The crystal azimuthal angle in degrees [0°, 360°)

This parameter defines the azimuthal rotation around the pump beam axis. Phi will affect the orientation of signal/idler emission in non-collinear geometries.

### Physical Properties

**Length (L)** - Crystal length in micrometers (µm)

The interaction length of the crystal in micrometers. Longer crystals may increase spatial walk-off effects.

**Temperature (T)** - Crystal temperature in degrees Celsius (°C)

Temperature affects the refractive indices of _some_ crystals. The temperature response of some crystals is not known.

**deff** - Effective nonlinear coefficient in pm/V

The effective nonlinear coefficient characterizes the strength of the second-order nonlinear interaction. This value depends on both the crystal material and the phasematching type. Currently this must be set manually.

Default value is 1 pm/V. For accurate calculations, consult your crystal's datasheet for the deff value corresponding to your chosen phasematching configuration and wavelengths.

### Periodic Poling Toggle

Enable this option to activate quasi-phasematching through periodic poling. If auto-calculation is enabled for crystal theta, it will be set to 90° (normal incidence).

### Poling Period

The period of the alternating domain structure in micrometers (µm).

{% tabs %}
{% tab title="Auto-Calculate" %}
When auto-calculation is enabled (requires periodic poling to be active), SPDCalc computes the required poling period based on your wavelengths, crystal type, and phasematching type.
{% endtab %}

{% tab title="Manual Entry" %}
Disable auto-calculation to specify a custom poling period.
{% endtab %}
{% endtabs %}

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

{% hint style="info" %}
Calculated poling domains can be accessed through the "Info" panel.
{% endhint %}

### Apodization Parameters

**FWHM** (for Gaussian apodization) - Full-width at half-maximum in micrometers (µm)

When Gaussian apodization is selected, this parameter sets the width of the Gaussian envelope.

**a** (for other apodization types) - Dimensionless parameter

For non-Gaussian apodization functions (except Interpolate), this parameter modifies the shape of the window function. The meaning depends on the specific window type.

Consult the [MathWorld reference](https://mathworld.wolfram.com/ApodizationFunction.html) for specific parameter meanings for each window type.

### Custom Apodization (Interpolate)

When "Interpolate" is selected, click the button showing the number of specified points to open a dialog where you can define a custom apodization profile.

Enter comma-separated values representing the apodization strength at evenly-spaced points along the crystal. The values are linearly interpolated between points.

Example: `1.0, 0.9, 0.7, 0.5, 0.7, 0.9, 1.0` creates a dip in the middle of the crystal.

## Pump Configuration

Pump settings define the properties of the laser used to generate photon pairs through the SPDC process.

<figure>
<img src="../.gitbook/assets/screenshots/settings/pump-configuration-panel.png" alt="Pump configuration panel">
<figcaption>Pump laser parameters including wavelength, bandwidth, beam profile, and power</figcaption>
</figure>

### Wavelength

The central wavelength of the pump laser in nanometers (nm).

### Bandwidth FWHM

The full-width at half-maximum spectral bandwidth of the pump laser in nanometers (nm).

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

### Spectrum Cutoff

A dimensionless threshold value (exponential notation) that sets the minimum pump spectrum amplitude to include in calculations.

When the pump's spectral amplitude falls below this threshold, the joint spectral intensity (JSI) is treated as effectively zero at those wavelengths. This optimization speeds up calculations by ignoring negligible contributions.

Default value: 1e-2 (1%)
- Higher values (e.g., 2e-1): Faster calculation, may miss weak spectral features
- Lower values (e.g., 1e-4): More accurate, slower calculation

{% hint style="info" %}
Setting this to be a larger value can help speed up expensive calculations at the risk of discarding data.

If you're seeing unexpected cutoffs in your JSI plots, try decreasing the spectrum cutoff value to include more of the pump spectral wings.
{% endhint %}

### Power

The pump laser power in milliwatts (mW). This parameter affects:
- Absolute coincidence count rates in the Heralding Calculator
- Brightness estimates for the SPDC source
- Pair generation rates

{% hint style="warning" %}
Absolute rate counts have not been vetted against experimental results and should not be trusted. Relative values like efficiency are more reliable.
{% endhint %}

### Refractive Index (np)

This read-only field displays the calculated refractive index of the pump beam in the crystal.

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

The signal photon wavelength in nanometers (nm).

### Waist 1/e²

The signal beam waist (radius at 1/e² intensity) in micrometers (µm).

This parameter defines the spatial mode of signal photon collection, typically matching the mode of your single-mode fiber or spatial filter.

### Collection Angles

**Theta (θ)** - Signal polar angle in degrees [-180°, 180°]

The angle between the signal photon collection direction and the pump beam axis. For collinear SPDC, this is typically 0°.

{% hint style="info" %}
For counter-propagating setups this may be set to angles near 180° to counter-propagate the signal rather than the idler.
{% endhint %}

{% hint style="warning" %}
The phasematching algorithms use a small-angle approximation for signal and idler angles. For accurate results, keep signal theta within ±10° of the pump direction.
{% endhint %}

**Phi (ϕ)** - Signal azimuthal angle in degrees [0°, 360°]

The azimuthal angle around the pump beam. This field is currently disabled as most calculations assume signal and idler are in the same plane (phi = 0°).

### Waist Positions

**Signal Focus** - Signal beam waist position in micrometers (µm)

The z-position of the signal beam waist along the crystal axis, measured from **the end** of the crystal. This parameter enables optimization of spatial mode matching between the pump and collection modes.

{% tabs %}
{% tab title="Auto-Calculate" %}
When auto-calculation is enabled (magic wand icon), SPDCalc determines the optimal signal focus position for maximum mode overlap with the SPDC emission.
{% endtab %}

{% tab title="Manual Entry" %}
Disable auto-calculation to specify a custom waist position. Values should be negative as they are measured from the end of the crystal (z=0).
{% endtab %}
{% endtabs %}

**Idler Focus** - Idler beam waist position in micrometers (µm)

Similar to signal focus, but for the idler photon. The idler parameters are typically symmetric with the signal in collinear degenerate SPDC but can differ for non-degenerate or non-collinear configurations.

### Refractive Indices

**ns** and **ni** - Signal and idler refractive indices (read-only)

These fields display the calculated refractive indices for signal and idler wavelengths at the current crystal temperature and phasematching configuration.

### Optimum Idler

This section displays the calculated properties of the idler photon at perfect phasematching conditions:

**Wavelength** - Optimum idler wavelength in nanometers (nm)

The idler wavelength is determined by energy conservation from the pump and signal wavelengths.

**Theta (θ) and Phi (ϕ)** - Optimum idler emission angles

The angles at which the idler photon is emitted for perfect phasematching. These values are calculated from momentum conservation and crystal properties.

## Periodic Poling Settings

Periodic poling enables quasi-phasematching (QPM) in crystals where birefringent phasematching is not possible or optimal. This is particularly useful in materials like PPKTP (periodically-poled KTP).

<figure>
<img src="../.gitbook/assets/screenshots/settings/periodic-poling-panel.png" alt="Periodic poling settings panel">
<figcaption>Quasi-phasematching configuration including poling period and apodization options</figcaption>
</figure>

## Integration Settings

Integration settings control the numerical calculation of the joint spectral intensity (JSI) and other integrated quantities. Use these parameters to balance calculation accuracy against computation time.

<figure>
<img src="../.gitbook/assets/screenshots/settings/integration-settings-panel.png" alt="Integration settings panel">
<figcaption>Numerical integration method and wavelength range controls</figcaption>
</figure>

### Integration Method

Select the numerical integration algorithm used for computing the JSI. The default is Simpson's rule with fixed grid spacing. This is recommended for most cases.

The other methods are provided for flexibility and testing.

### Method-Specific Parameters

**Steps** (Simpson only) - Number of integration steps

Controls the grid resolution for Simpson's rule. More steps give higher accuracy but slower calculation.

**Tolerance** (Adaptive methods) - Integration error tolerance

Sets the target accuracy for adaptive integration methods.

**Max Depth** (Adaptive methods) - Maximum recursion depth

Limits how many times the integration region can be subdivided. Higher values allow more refinement but increase computation time.

**Degree** (GaussLegendre only) - Quadrature degree

The number of quadrature points in the Gauss-Legendre scheme. Higher degree provides better accuracy for polynomial-like functions.

### Grid Size (Resolution)

The number of grid points in each dimension for 2D JSI calculations. This parameter has a significant impact on both accuracy and computation time.

This applies to panels that do not have their own "JSI Resolution" setting. Panels that do provide their own resolution setting tend to be those that involve many JSI calculations, such as a Hong-Ou-Mandel Time Series.

{% hint style="warning" %}
The total number of calculated points is (Grid Size)², so doubling the resolution quadruples the computation time.
{% endhint %}

### Auto Calculate Integration Limits

Enable this toggle to automatically determine appropriate wavelength ranges for the JSI calculation based on your pump bandwidth and crystal properties.

### Signal Range

**Minimum** and **Maximum** - Signal wavelength integration range in nanometers (nm)

### Idler Range

**Minimum** and **Maximum** - Idler wavelength integration range in nanometers (nm)

---

With these parameter configuration tools, you can fully define your SPDC system for accurate simulation. Next, proceed to [Working with Calculation Panels](working-with-panels.md) to visualize and analyze your configured system.
