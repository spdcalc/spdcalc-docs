# Calculation Panels Reference

This section provides detailed reference documentation for each type of calculation panel available in SPDCalc. Each panel computes and visualizes different properties of spontaneous parametric down-conversion (SPDC) crystals, helping you analyze and optimize your quantum optics experiments.

Panels can be added to your workspace from the panel selector and automatically update when you change parameters. Each panel type serves a specific analysis purpose and offers customizable visualization options.

## Joint Spectrum Intensity (JSI) Plot

The Joint Spectrum Intensity (JSI) panel visualizes the two-photon joint spectral amplitude, revealing the spectral correlations between signal and idler photons generated through SPDC. This is one of the most fundamental visualizations for understanding photon pair properties.

<figure>
<img src="../.gitbook/assets/screenshots/panels/jsi-plot.png" alt="Joint Spectrum Intensity plot showing signal vs idler wavelengths">
<figcaption>Joint Spectrum Intensity visualization with multiple axis options and display modes</figcaption>
</figure>

### What It Calculates

The JSI represents the two-photon quantum state in the frequency domain. The panel computes the joint spectral amplitude (JSA) by integrating over all possible emission angles within your collection geometry, accounting for:

- Phasematching conditions across the signal and idler wavelength ranges
- Pump spectral profile and bandwidth effects
- Crystal properties (length, type, temperature, orientation)
- Collection mode spatial overlap (based on waist sizes and positions)

The Schmidt decomposition of this JSA provides a measure of spectral entanglement.

### Visualization Options

The panel offers three complementary views accessible via tabs:

**Intensity Tab**: Displays |JSA|², showing the probability distribution of photon pair wavelengths. Bright regions indicate wavelength combinations with high pair production rates.

**Amplitude Tab**: Displays |JSA|, useful for identifying weak features that might be obscured in the squared intensity plot.

**Phase Tab**: Displays the complex phase of the JSA, revealing phase relationships important for quantum interference effects.

**Axis Type Selector**: Choose between three coordinate systems:

- **Wavelength** (default): Signal wavelength (nm) vs. Idler wavelength (nm) - most intuitive for experimental design
- **Frequency**: Signal frequency (THz) vs. Idler frequency (THz) - useful for analyzing bandwidth in frequency space
- **Sum-Difference**: ½(ωᵢ + ωₛ) vs. ½(ωᵢ - ωₛ) - reveals energy-time correlations, where vertical slices represent constant energy sum

### Interactive Features

- **Log Scale Toggle**: Enable logarithmic color scaling to reveal weak spectral features hidden in linear scale
- **Zero Highlighting**: Emphasize zero-valued regions to clearly identify phasematching boundaries
- **Zoom and Compute**: Click the target icon after zooming to recalculate with integration limits matching your current plot view, increasing resolution in your region of interest

### Interpreting the Output

**Elongated diagonal feature**: Indicates strong spectral correlations - signal and idler wavelengths are entangled. The tilt angle relates to group velocity matching.

**Circular/uncorrelated feature**: Photons are spectrally separable (low entanglement), typically achieved with very narrow pump bandwidth or long crystals.

**Schmidt Number**: Displayed in the results bar, this quantifies entanglement:
- K = 1: Pure state, completely separable photons
- K > 1: Mixed state, spectrally entangled photons
- Higher values indicate broader spectral correlations

{% hint style="info" %}
The Schmidt number provides a single metric for spectral entanglement. For heralded single-photon applications, lower Schmidt numbers (closer to 1) indicate higher purity. For quantum communication, controlled entanglement (K ≈ 2-10) may be desirable.
{% endhint %}

### Parameters That Affect This Panel

- **Pump bandwidth**: Narrower bandwidth reduces spectral correlations (lower K)
- **Crystal length**: Longer crystals increase spectral selectivity
- **Collection waist sizes**: Affect spatial mode overlap
- **Integration ranges**: Define the wavelength region to analyze
- **Phasematching geometry**: Collinear vs. non-collinear affects correlation structure

<details>
<summary>Technical Details</summary>

The computation performs a 2D integration over the signal and idler wavelength ranges specified in your Integration Settings. The calculation evaluates:

$$|\text{JSA}(\lambda_s, \lambda_i)|^2 = \left|\iint d\theta d\phi \, \text{PM}(\lambda_s, \lambda_i, \theta, \phi) \cdot A_p(\lambda_s, \lambda_i) \cdot \Phi(\lambda_s, \lambda_i, \theta, \phi)\right|^2$$

where PM is the phasematching function (crystal's sinc response), A_p is the pump spectral envelope, and Φ represents spatial mode overlap. The Schmidt decomposition then finds the eigenvalues of the reduced density matrix.

The three coordinate systems represent different slices through the same four-dimensional frequency space, each highlighting different physical properties.

</details>

---

## Phasematching Curves

The Phasematching Curves panel creates 2D heatmaps showing how any two SPDC parameters affect phasematching efficiency. This powerful tool helps you explore the parameter space and find optimal configurations for your experiment.

<figure>
<img src="../.gitbook/assets/screenshots/panels/phasematching-curves.png" alt="Phasematching curve showing signal theta vs idler theta">
<figcaption>Phasematching curve analyzing emission angle dependencies</figcaption>
</figure>

### What It Calculates

For each point in your selected 2D parameter grid, the panel computes the phasematching intensity - essentially the brightness of photon pair production at that configuration. This reveals:

- How parameters interact to satisfy energy and momentum conservation
- The width and shape of phasematching acceptance regions
- Optimal operating points for your configuration
- Trade-offs between different parameter choices

### Configurable Parameters

You can plot phasematching as a function of any two parameters from:

**Wavelengths**:
- Signal Wavelength (nm)
- Idler Wavelength (nm)
- Pump Wavelength (nm)

**Angles**:
- Signal Theta (external angle, degrees)
- Idler Theta (external angle, degrees)
- Crystal Theta (crystal cut angle, degrees)
- Crystal Phi (crystal rotation angle, degrees)

**Crystal Properties**:
- Crystal Length (µm)
- Crystal Temperature (°C)
- Poling Period (µm) - for periodically poled crystals

For each axis, you specify:
- **Min/Max range**: The parameter values to sweep
- **Steps**: Number of points to calculate (more steps = higher resolution but slower)

### Interactive Features

- **Log Scale Toggle**: View phasematching on logarithmic scale to reveal weak but acceptable regions
- **Zero Highlighting**: Clearly show boundaries between allowed and forbidden regions
- **Zoom and Compute**: Focus on a parameter region and recalculate with higher resolution
- **Dynamic Range Adjustment**: Change ranges on-the-fly to explore different parameter spaces

### Interpreting the Output

**Bright regions**: Excellent phasematching - high pair production efficiency

**Narrow bright lines**: Tight phasematching tolerances - requires precise control of these parameters

**Broad bright regions**: Relaxed tolerances - the configuration is robust to parameter variations

**Multiple bright spots**: Multiple phasematching solutions exist (common in certain crystal geometries)

**Dark regions**: Poor or no phasematching - photon pair production is suppressed

{% hint style="info" %}
When optimizing a configuration, look for bright regions with substantial area. A single bright pixel might indicate a perfect phasematching point, but it will be difficult to achieve experimentally. Broader features indicate more forgiving configurations.
{% endhint %}

### Common Use Cases

**Signal Theta vs. Idler Theta**: Visualize the emission cone structure, identify degenerate and non-degenerate emission angles

**Signal Wavelength vs. Idler Wavelength**: Map out the allowed wavelength pairs, verify energy conservation tuning curves

**Crystal Length vs. Pump Bandwidth**: Optimize the trade-off between brightness (longer crystal) and spectral purity (shorter crystal)

**Crystal Theta vs. Temperature**: Find temperature tuning curves for a given crystal cut

**Poling Period vs. Wavelength**: Design quasi-phasematching structures for specific wavelengths

<details>
<summary>Technical Details</summary>

The panel evaluates the phasematching function at each grid point by temporarily overriding the specified parameters while keeping all others fixed. For parameters that appear in phasematching conditions (wavelengths, angles, crystal properties), the computation directly affects the momentum conservation calculation.

The calculation is parallelized across CPU cores for efficiency. Coarse grids (50×50 or less) calculate quickly, while fine grids (200×200 or more) reveal subtle features but take longer.

</details>

---

## Schmidt Number Analysis

The Schmidt Number Analysis panel reveals how photon pair entanglement varies with pump bandwidth and crystal length. This helps you optimize your source for either heralded single-photon generation (low Schmidt number) or controlled entanglement generation.

<figure>
<img src="../.gitbook/assets/screenshots/panels/schmidt-number.png" alt="Schmidt number heatmap vs pump bandwidth and crystal length">
<figcaption>Schmidt number variation across pump bandwidth and crystal length parameter space</figcaption>
</figure>

### What It Calculates

For each point in the 2D grid (crystal length, pump bandwidth), the panel:
1. Computes the joint spectral amplitude (JSA) at that configuration
2. Performs Schmidt decomposition to find eigenvalues λₙ
3. Calculates the Schmidt number: K = 1 / Σ λₙ²

The result is a heatmap showing how these two critical parameters control spectral entanglement.

### Visualization

The panel displays a heatmap with:
- **X-axis**: Crystal Length (µm)
- **Y-axis**: Pump Bandwidth FWHM (nm)
- **Color**: Schmidt number (white = K≈1, red = high K)

The color scale uses white for low Schmidt numbers (spectrally pure photons) and transitions through red for higher values (more entanglement).

### Configurable Parameters

**X Range (Crystal Length)**:
- Default: 1000-25000 µm
- Set min/max to focus on realistic crystal lengths for your application

**Y Range (Pump Bandwidth)**:
- Default: 0.5-5 nm FWHM
- Adjust based on your pump laser specifications

**Grid Size**: Number of calculation points along each axis (applies to both X and Y)
- Lower values (5-10): Fast calculation, coarse overview
- Higher values (20-50): Slower calculation, reveals fine structure

**JSI Resolution**: Grid size for the underlying joint spectrum calculation
- Lower values (10-30): Faster but less accurate Schmidt number
- Higher values (50-100): Slower but more accurate decomposition

### Interactive Features

- **Zoom and Compute**: After identifying an interesting region, zoom in and click the target icon to recalculate with the new ranges for higher local resolution

### Interpreting the Output

**Lower-left region (short crystal, narrow bandwidth)**: Typically shows lowest Schmidt numbers. Short crystals have broad spectral acceptance, while narrow pumps limit correlations - these effects compete.

**Upper-right region (long crystal, broad bandwidth)**: Usually shows higher Schmidt numbers. Long crystals enforce tight spectral correlations, and broad pumps allow entanglement to develop.

**Diagonal features**: Often indicate optimal trade-off curves where crystal length and pump bandwidth balance each other.

**Vertical bands**: Regions where crystal length has minimal effect - pump bandwidth dominates.

**Horizontal bands**: Regions where pump bandwidth has minimal effect - crystal length dominates.

{% hint style="info" %}
For heralded single-photon sources, target K < 1.1 for high-purity heralded photons. This typically requires either very narrow-band pumps (<1 nm) or specific crystal lengths that balance phasematching acceptance with pump spectrum.
{% endhint %}

### Parameters That Affect This Panel

While crystal length and pump bandwidth are swept, the calculation depends on:
- **Signal/idler wavelengths**: Determines the phasematching condition
- **Pump wavelength**: Affects group velocity mismatch
- **Collection geometry**: Waist sizes affect spatial-spectral coupling
- **Crystal type and orientation**: Changes refractive index dispersion

### Design Workflow Example

1. Start with a coarse grid (grid size 10, resolution 30) to get an overview
2. Identify target Schmidt number region based on your application
3. Zoom into that region and increase grid size to 20
4. Increase JSI resolution to 50 for accurate Schmidt numbers
5. Note the crystal length and pump bandwidth combinations that meet your requirements
6. Update your main configuration with these values

<details>
<summary>Technical Details</summary>

The Schmidt decomposition finds the singular value decomposition of the JSA matrix:

$$\text{JSA}(\lambda_s, \lambda_i) = \sum_n \sqrt{\lambda_n} u_n(\lambda_s) v_n(\lambda_i)$$

The Schmidt number K = 1/Σλₙ² quantifies how many Schmidt modes contribute significantly. K = 1 means a single Schmidt mode (pure state), while K >> 1 means many modes contribute (mixed state).

This panel performs the full JSA calculation and Schmidt decomposition at each grid point, making it computationally intensive. The calculation is parallelized across available CPU cores for efficiency.

</details>

---

## Hong-Ou-Mandel Dip

The Hong-Ou-Mandel (HOM) Dip panel simulates two-photon quantum interference when photons from a single SPDC source are incident on a beamsplitter. The visibility of the interference dip characterizes photon indistinguishability.

<figure>
<img src="../.gitbook/assets/screenshots/panels/hom-dip.png" alt="Hong-Ou-Mandel dip showing coincidence rate vs time delay">
<figcaption>Hong-Ou-Mandel interference dip with visibility measurement</figcaption>
</figure>

### What It Calculates

The panel computes the coincidence counting rate as a function of the relative time delay (Δt) between the two photon paths in a Hong-Ou-Mandel interferometer. When photons are indistinguishable and arrive simultaneously at the beamsplitter, quantum interference causes them to bunch - both exit the same output port, creating a dip in coincidence counts.

The calculation accounts for:
- Spectral correlations in the photon pair (from the JSA)
- Temporal walkoff between signal and idler
- Collection mode properties
- Group velocity dispersion effects

### Visualization

The panel displays a line plot showing:
- **X-axis**: Time Delay Δt (femtoseconds)
- **Y-axis**: Coincidence Rate (normalized, arbitrary units)
- **Result Bar**: HOM Visibility - the depth of the interference dip

### Configurable Parameters

**Δt min/max**: The range of time delays to simulate
- Typical range: -400 fs to +800 fs
- Broader ranges show the full temporal profile
- Narrower ranges focus on the dip structure

**Steps**: Number of time delay points to calculate
- More steps give smoother curves but take longer
- 50-200 steps typically sufficient

**JSI Resolution**: Grid size for the underlying joint spectrum integration
- Lower values (20-50): Faster calculation
- Higher values (100-200): More accurate visibility calculation
- Trade-off between speed and accuracy

### Interactive Features

- **Zoom and Compute**: Zoom into a time delay region and click the target icon to recalculate with the new Δt range
- **Automatic Spline Smoothing**: The plot uses spline interpolation for smooth curves between calculated points

### Interpreting the Output

**HOM Visibility**: Displayed in the result bar, calculated as:
- V = (C_max - C_min) / C_max
- V = 1.0 (100%): Perfect indistinguishability, ideal quantum interference
- V = 0.5: Classical limit (distinguishable photons)
- V < 0.5: Usually indicates calculation issues or extreme parameter mismatch

**Dip Width**: The temporal width of the dip relates to photon coherence time:
- Narrow dip (~100 fs): Broadband photons, short coherence time
- Wide dip (>1000 fs): Narrowband photons, long coherence time

**Asymmetric Dip**: Indicates group velocity mismatch between signal and idler - they arrive at the beamsplitter at different times even when path lengths are equal

**Oscillations**: May appear in the wings if there are strong spectral correlations or beating effects

{% hint style="info" %}
High HOM visibility (>95%) is crucial for quantum information applications. Visibility is limited by spectral distinguishability, spatial mode mismatch, and any which-path information. The JSI panel's Schmidt number and this panel's visibility are closely related - lower Schmidt numbers generally yield higher visibility.
{% endhint %}

### Parameters That Affect This Panel

- **Pump bandwidth**: Narrower bandwidth typically increases visibility
- **Crystal length**: Affects spectral correlations and walkoff
- **Signal/idler wavelengths**: Non-degenerate photons have lower visibility due to distinguishability
- **Collection waist sizes**: Spatial mode mismatch reduces visibility
- **Integration ranges**: Must encompass the photon spectral content

### Physical Interpretation

The HOM effect arises from quantum interference of two-photon probability amplitudes:
1. Both photons reflected: |R⟩|R⟩
2. Both photons transmitted: |T⟩|T⟩
3. One reflected, one transmitted: |R⟩|T⟩ or |T⟩|R⟩

For indistinguishable photons at zero delay, amplitudes 3 and 4 interfere destructively, suppressing coincidences. The visibility measures how completely this interference occurs.

<details>
<summary>Technical Details</summary>

The HOM coincidence rate is computed by integrating the JSA with a phase factor accounting for the time delay:

$$C(\Delta t) = \iint d\omega_s d\omega_i |\text{JSA}(\omega_s, \omega_i)|^2 \left|1 + e^{i(\omega_s - \omega_i)\Delta t}\right|^2$$

The visibility is extracted by finding the maximum and minimum of this function. The calculation requires accurate JSA calculation, so JSI resolution significantly affects the result quality.

The panel parallelizes the calculation across available CPU cores by partitioning the time delay range.

</details>

---

## Two-Source HOM Dip

The Two-Source HOM Dip panel simulates Hong-Ou-Mandel interference between photons originating from two independent SPDC sources. This is critical for quantum networking applications where photons from separate sources must interfere.

<figure>
<img src="../.gitbook/assets/screenshots/panels/two-source-hom.png" alt="Two-source HOM showing three interference curves">
<figcaption>Two-source HOM interference showing signal-signal, idler-idler, and signal-idler correlations</figcaption>
</figure>

### What It Calculates

The panel computes three simultaneous Hong-Ou-Mandel interference curves corresponding to different photon pairing scenarios:

1. **Signal-Signal (ss)**: Both photons from the signal outputs of the two sources
2. **Idler-Idler (ii)**: Both photons from the idler outputs of the two sources
3. **Signal-Idler (si)**: One signal photon and one idler photon from different sources

Each curve shows the coincidence rate as a function of relative time delay between the sources.

### Visualization

The panel displays three overlaid line plots:
- **Red squares**: Signal-Signal interference
- **Blue circles**: Idler-Idler interference
- **Purple diamonds**: Signal-Idler interference (typically hidden by default)

The result bar shows visibilities for all three configurations: V(ss), V(ii), V(si)

### Configurable Parameters

**Δt min/max**: Range of time delays to simulate
- Typical range: -2000 fs to +2000 fs (broader than single-source HOM)
- Two independent sources may require larger ranges to see full features

**Steps**: Number of time delay points
- 50-100 steps usually sufficient for smooth curves
- Fewer steps recommended for initial exploration (faster calculation)

**JSI Resolution**: Grid size for joint spectrum integration
- Critical parameter affecting accuracy
- Lower values (10-20): Fast but approximate
- Higher values (50+): Slow but accurate

### Interactive Features

- **Legend Toggle**: Click legend entries to show/hide individual curves for clarity
- **Zoom and Compute**: Focus on specific time delay regions and recalculate
- **Automatic Spline Smoothing**: Curves interpolated for visual smoothness

### Interpreting the Output

**Signal-Signal Visibility**: Measures how well photons from two signal arms interfere
- High visibility: Sources produce indistinguishable signal photons
- Limited by signal wavelength matching and spectral purity

**Idler-Idler Visibility**: Measures idler photon indistinguishability
- May differ from signal-signal if wavelengths are non-degenerate
- Asymmetry between signal and idler visibility indicates spectral distinguishability

**Signal-Idler Visibility**: Typically lowest visibility
- Cross-source interference between spectrally different photons
- Low values expected - shown for completeness

**Relative Dip Widths**:
- ss and ii dips have similar widths if wavelengths are comparable
- Different widths indicate different coherence times

**Offset Dips**: Central dip position offset from zero indicates timing mismatch between sources

{% hint style="info" %}
For quantum networking, you want high and equal visibilities for signal-signal and idler-idler (>90% for both). This ensures photons from independent sources are indistinguishable and can be entangled through Bell-state measurements. Asymmetric visibilities indicate one photon type is more distinguishable than the other.
{% endhint %}

### Parameters That Affect This Panel

Since both sources use the same configuration in this simulation:
- **Pump bandwidth**: Narrower bandwidth improves visibility
- **Crystal parameters**: Length, type, and temperature must be identical between sources
- **Wavelength degeneracy**: Degenerate SPDC (signal = idler wavelength) maximizes visibility
- **Collection geometry**: Identical collection modes improve visibility

### Design Workflow for Quantum Networks

1. Start with current configuration to see baseline visibilities
2. Adjust parameters to maximize signal-signal and idler-idler visibility
3. Aim for V(ss) ≈ V(ii) > 0.9 for high-quality entanglement swapping
4. Use broader time ranges initially, then zoom into dip structure
5. Increase JSI Resolution if visibility numbers seem inaccurate

<details>
<summary>Technical Details</summary>

Two-source HOM interference involves the overlap of biphoton states from independent sources:

$$|\Psi\rangle = |\Psi_1\rangle |\Psi_2\rangle = \left(\iint d\omega_s d\omega_i \text{JSA}_1(\omega_s, \omega_i) |s_1 i_1\rangle\right) \left(\iint d\omega'_s d\omega'_i \text{JSA}_2(\omega'_s, \omega'_i) |s_2 i_2\rangle\right)$$

When photons from different sources meet at a beamsplitter, interference occurs if they are spectrally indistinguishable. The visibility depends on the spectral overlap integral of the two JSAs.

The calculation partitions the time delay range across CPU cores for parallel computation, as this is one of the most computationally intensive panels.

</details>

---

## Heralding Efficiency Analysis

The Heralding Efficiency Analysis panel provides comprehensive visualization of how collection mode waist sizes affect heralding efficiency and photon count rates. This helps optimize fiber coupling and collection optics design.

<figure>
<img src="../.gitbook/assets/screenshots/panels/heralding-efficiency.png" alt="Heralding efficiency plots and JSI visualization">
<figcaption>Heralding efficiency analysis showing efficiency curves, count rates, and interactive JSI modes</figcaption>
</figure>

### What It Calculates

The panel performs a series of calculations as you sweep the collection waist size:

1. **Heralding Efficiencies**: Signal, idler, and symmetric efficiency at each waist size
2. **Count Rates**: Singles and coincidence rates (photons per second)
3. **Joint Spectral Modes**: Coincidence JSI, signal singles JSI, and idler singles JSI at the currently selected waist size

These calculations reveal how tightly you should focus your collection optics to maximize heralding efficiency while maintaining reasonable count rates.

### Visualization

The panel contains three main sections:

**Top-Left: Efficiency vs. Waist Size**
- Three curves showing signal efficiency (red squares), idler efficiency (blue circles), and symmetric efficiency (purple diamonds)
- Symmetric efficiency = √(signal efficiency × idler efficiency)

**Middle-Left: Count Rates vs. Waist Size**
- Signal singles (red), idler singles (blue), and coincidences (purple)
- Y-axis in counts per second

**Bottom-Left: Interactive Slider and Results**
- Slider to select waist size for JSI visualization
- Detailed efficiency and count rate readout at selected waist

**Right: Combined JSI Visualization**
- Three overlaid heatmaps showing coincidence mode (purple), signal singles mode (red), and idler singles mode (blue)
- Reveals spatial-spectral mode structure at the selected waist size

### Configurable Parameters

**Min Waist**: Starting waist size (µm)
- Default: "auto" - automatically set to minimum valid waist size
- Manually set to focus on specific range
- Warning displayed if below the minimum physical waist size

**Max Waist**: Ending waist size (µm)
- Typical range: 50-200 µm
- Larger values show asymptotic behavior

**Steps**: Number of waist values to calculate
- 10-20 steps typical for smooth curves
- More steps increase calculation time significantly

**Resolution**: JSI grid size for mode calculations
- 20-30 sufficient for efficiency trends
- 30-50 needed for accurate JSI visualization
- Higher resolution much slower but more accurate

### Interactive Features

- **Efficiency Plot Zoom**: Click the target icon after zooming to recalculate over the new waist range
- **Waist Slider**: Drag to see JSI modes at different waist sizes without recalculation
- **Log Scale Toggle**: Enable logarithmic color scale on JSI heatmaps to reveal weak features
- **Legend Toggle**: Show/hide curves on the count rate plot

### Interpreting the Output

**Efficiency Curves**:
- **Rising region**: Too-small waists miss photons - efficiency increases as waist grows
- **Plateau region**: Optimal waist range - efficiency near maximum
- **Falling region**: Oversized waists (not usually seen unless max waist very large)

**Ideal Operating Point**: Where efficiency plateaus but count rates remain high (around the "knee" of the efficiency curve)

**Signal vs. Idler Asymmetry**: If curves differ significantly, signal and idler have different spatial mode structures - indicates waist position or size mismatch with pump

**Count Rate Behavior**:
- Singles rates increase with waist size (collecting more spatial modes)
- Coincidence rate peaks and may decrease (fewer well-matched modes)
- The ratio of coincidences to singles relates to efficiency

**JSI Mode Visualization**:
- **Purple (Coincidences)**: The joint mode of detected photon pairs
- **Red (Signal Singles)**: All signal photons, including unheralded ones
- **Blue (Idler Singles)**: All idler photons, including unheralded ones
- Good mode overlap (purple inside red/blue) indicates high efficiency
- Large red/blue regions outside purple indicate unheralded photons (low efficiency)

{% hint style="info" %}
For heralded single-photon sources, maximize symmetric efficiency (aim for >0.8 or 80% if possible). This ensures that most detected heralding photons indicate a photon is present in the heralded mode. The JSI overlay helps visualize why efficiency is limited - look for mismatch between the coincidence mode (purple) and the singles modes (red/blue).
{% endhint %}

### Parameters That Affect This Panel

Note: This panel sweeps signal and idler waist together. To analyze them independently, use other panels or adjust parameters manually.

- **Pump waist**: Determines the photon mode structure
- **Waist positions**: Offset between pump/signal/idler waists affects overlap
- **Crystal length**: Longer crystals have more spatial walkoff
- **Wavelengths**: Non-degenerate configurations may have asymmetric efficiencies
- **Collection angles**: Affects which spatial modes are selected

### Design Workflow

1. Start with a coarse scan (10 steps, resolution 20) to find the general efficiency curve shape
2. Identify the efficiency plateau region
3. Zoom into that region and increase steps to 20 for detail
4. Use the slider to explore JSI modes at different waist sizes
5. Select a waist size in the plateau with acceptable count rates
6. Increase resolution to 40-50 to verify JSI mode quality
7. Apply the chosen waist size to your main configuration

<details>
<summary>Technical Details</summary>

Heralding efficiency quantifies what fraction of detected photons successfully herald their partners:

$$\eta_s = \frac{\text{Coincidences}}{\text{Signal Singles}}, \quad \eta_i = \frac{\text{Coincidences}}{\text{Idler Singles}}$$

The symmetric efficiency η = √(ηₛηᵢ) is often reported as a single figure of merit.

The JSI calculation includes both:
- **Coincidence JSI**: The joint amplitude of detected photon pairs
- **Singles JSI**: Integrated over undetected photon wavelengths

The three overlaid heatmaps use different color channels with transparency, allowing visualization of mode overlap. Perfect overlap (all three coincide) would appear white; deviations show which spatial-spectral modes contribute to inefficiency.

Calculations are parallelized across CPU cores by partitioning the waist size range.

</details>

---

## Heralding Calculator

The Heralding Calculator provides a quick, focused calculation of heralding efficiency and count rates for a specific set of waist sizes without sweeping parameters. Use this for fast "what-if" scenarios.

<figure>
<img src="../.gitbook/assets/screenshots/panels/heralding-calculator.png" alt="Heralding calculator with results display">
<figcaption>Heralding calculator showing efficiency and count rate results for specified waist sizes</figcaption>
</figure>

### What It Calculates

For the specified signal, idler, and pump waist sizes, the panel computes:

- **Signal Efficiency**: ηₛ = Coincidences / Signal Singles
- **Idler Efficiency**: ηᵢ = Coincidences / Idler Singles
- **Symmetric Efficiency**: η = √(ηₛ × ηᵢ)
- **Signal Singles Rate**: Photons/second in the signal mode
- **Idler Singles Rate**: Photons/second in the idler mode
- **Coincidence Rate**: Photon pairs/second detected in coincidence

### Configurable Parameters

**Signal Waist** (µm): Collection mode waist size for signal photon
- Set to your signal fiber mode size or collection optics focal spot

**Idler Waist** (µm): Collection mode waist size for idler photon
- Set to your idler fiber mode size or collection optics focal spot

**Pump Waist** (µm): Pump beam waist size at the crystal
- Should match the pump waist parameter in your main configuration

After setting these values, click **Calculate** to run the computation.

### Visualization

The panel displays a formatted results card showing:
- Three efficiency percentages (signal, idler, symmetric)
- Three count rates in photons/second (signal singles, idler singles, coincidences)
- All values clearly labeled with units

### When to Use This Panel

**Quick Checks**: Rapidly evaluate efficiency at specific waist sizes without the overhead of sweeping ranges

**Fiber Mode Matching**: Input your fiber mode field diameters to see if they match well with the photon modes

**Asymmetric Collection**: Analyze cases where signal and idler waists differ (e.g., different fiber types)

**Verification**: Cross-check values from the Heralding Efficiency Analysis panel

### Interpreting the Output

**High Symmetric Efficiency (>80%)**: Excellent mode matching - most heralded photons are successfully collected

**Low Symmetric Efficiency (<50%)**: Poor mode matching - consider:
- Adjusting waist sizes
- Repositioning collection waists
- Modifying pump waist to better match collection modes

**Asymmetric Efficiencies**: If signal and idler efficiencies differ significantly:
- One photon type is better matched to its collection mode
- Check waist positions and crystal orientation
- Verify signal and idler wavelengths are as expected

**Count Rates**:
- Singles rates in the kHz-MHz range are typical for milliwatt pump powers
- Coincidence rates 10-1000× lower than singles are normal
- Very low rates (<1 Hz) suggest calculation issues or extreme parameter mismatch

{% hint style="info" %}
The calculated count rates depend on your pump average power setting. If rates seem too low, verify your pump power parameter. Note that experimental rates will also depend on detector efficiency, collection losses, and other real-world factors not included in this idealized calculation.
{% endhint %}

### Parameters That Affect This Panel

Besides the three waist inputs:
- **Pump power**: Directly scales all count rates
- **Crystal properties**: Length, type, phasematching affect pair generation rate
- **Wavelengths**: Determines phasematching and group velocity matching
- **Collection angles**: Affects spatial mode overlap
- **Integration ranges**: Must encompass spectral content

### Comparison with Heralding Efficiency Analysis Panel

| Feature | Heralding Calculator | Heralding Efficiency Analysis |
|---------|---------------------|------------------------------|
| Speed | Fast (single calculation) | Slower (multiple waist values) |
| Waist Input | Manual signal/idler/pump | Sweeps signal/idler together |
| Visualization | Numbers only | Efficiency curves + JSI modes |
| Use Case | Quick checks, asymmetric waists | Optimization, mode visualization |

<details>
<summary>Technical Details</summary>

The calculation performs a single JSI integration at the specified waist sizes with reduced resolution (grid size 20) for speed. This is sufficient for efficiency and rate estimates but not for detailed JSI visualization.

The panel uses the same underlying calculation as the Heralding Efficiency Analysis panel but skips the waist size sweep and complex JSI visualizations.

</details>

---

## Info Panel

The Info Panel displays calculated crystal and phasematching information, with a focus on periodic poling domain specifications for fabrication.

<figure>
<img src="../.gitbook/assets/screenshots/panels/info-panel.png" alt="Info panel showing poling domain specifications">
<figcaption>Info panel with poling domain data in fractional and physical length formats</figcaption>
</figure>

### What It Calculates

Based on your current crystal configuration, the panel computes:

**Poling Domain Structure**: The sequence of +/- poling domains along the crystal to achieve the specified phasematching, including:
- Domain boundaries as fractional positions along the crystal
- Domain boundaries as physical lengths in microns
- Total number of domains
- Domain widths for fabrication

The calculation accounts for:
- Specified poling period
- Apodization profile (if enabled) - gradual variation in poling to suppress side lobes
- Crystal length
- Phasematching requirements

### Visualization

The panel shows:

**Poling Domains Section**:
- Domain count
- Display format selector (Fractional vs. Physical Length)
- Text area with comma-separated domain boundaries
- Copy button to copy values to clipboard

**Domain Format Options**:

1. **Fractional**: Domain boundaries as fractions of the poling period (0.0 to 1.0 scale)
   - Example: 0.0000, 0.5000, 1.0000 (alternating ±z domains, 50% duty cycle)

2. **Physical Length (µm)**: Domain boundaries in microns
   - Example: 0.0000, 15.0000, 30.0000 (for 30 µm poling period)
   - Directly usable for fabrication specifications

### Interactive Features

**Display Format Toggle**: Switch between fractional and physical length representations

**Copy to Clipboard**: Click the copy icon to copy domain values for use in fabrication software or documentation

**Save as JSON**: Download a complete JSON file containing:
- Crystal length (µm)
- Poling period (µm)
- Poling domains in both fractional and physical formats
- Structured for easy integration with fabrication workflows

### Interpreting the Output

**Domain Count**:
- More domains = finer poling structure
- Typical: 10-1000 domains depending on crystal length and poling period

**Domain Pattern**:
- Regular alternating pattern (0.0, 0.5, 1.0, 0.0, 0.5...): Uniform poling, 50% duty cycle
- Irregular pattern with varying duty cycles: Apodized poling for spectral shaping
- Gradual duty cycle variation: Chirped or apodized grating

**Domain Width Consistency**:
- Similar domain widths: Uniform quasi-phasematching
- Varying widths at crystal ends: Apodization to reduce spectral side lobes

{% hint style="info" %}
The domain specifications output by this panel can be directly used for:
- Electric field poling fabrication (PPLN, PPKTP, etc.)
- Sharing crystal specifications with fabrication facilities
- Documenting crystal designs in publications
- Verifying that auto-calculated poling period produces the expected domain structure
{% endhint %}

### Parameters That Affect This Panel

- **Poling Period**: Directly determines domain spacing
- **Crystal Length**: Determines total number of domains
- **Apodization Profile**: Affects domain duty cycle variation
  - No apodization: Uniform 50% duty cycle
  - Gaussian apodization: Gradual duty cycle variation
  - Bartlett apodization: Linear duty cycle taper
- **Apodization Parameter**: Controls the strength of apodization

### Common Use Cases

**Fabrication Specification**: Generate the domain list for sending to a crystal fabrication facility

**Design Verification**: Confirm that the auto-calculated poling period produces the expected domain structure

**Publication Documentation**: Include domain specifications in methods sections

**Design Comparison**: Compare domain structures for different apodization schemes

### Understanding Quasi-Phasematching

Periodic poling compensates for the momentum mismatch Δk in SPDC:
- Without poling: Birefringent phasematching (limited wavelength/crystal choices)
- With poling: Quasi-phasematching (QP) in any crystal with χ⁽²⁾ nonlinearity

The poling period Λ satisfies:
$$\Delta k = k_p - k_s - k_i = \frac{2\pi}{\Lambda}$$

Domain reversal flips the sign of χ⁽²⁾, effectively adding 2π/Λ to the momentum balance every domain period.

<details>
<summary>Technical Details</summary>

The domain calculation uses the specified poling period and apodization profile to generate a domain inversion sequence along the crystal length. For uniform poling:

- Each domain has width Λ/2 (50% duty cycle)
- Alternating +z and -z domains
- Exact boundaries determined by crystal length and period

For apodized poling, the duty cycle d(z) varies along the crystal according to the apodization function (Gaussian, Bartlett, etc.):

$$d(z) = 0.5 \times [1 + A(z)]$$

where A(z) is the normalized apodization function. This creates longer +z domains near the crystal center and shorter ones near the ends (or vice versa), reducing spectral side lobes at the expense of peak efficiency.

The JSON export format is designed for interoperability with common fabrication software tools.

</details>

---

## Summary

This reference guide covers all eight calculation panel types in SPDCalc. Each panel serves a specific purpose in analyzing and optimizing SPDC configurations:

- **JSI Plot**: Fundamental two-photon state visualization and entanglement quantification
- **Phasematching Curves**: Parameter space exploration and optimization
- **Schmidt Number Analysis**: Entanglement vs. crystal length and pump bandwidth
- **HOM Dip**: Single-source quantum interference characterization
- **Two-Source HOM Dip**: Multi-source indistinguishability for quantum networks
- **Heralding Efficiency Analysis**: Collection mode optimization with full visualization
- **Heralding Calculator**: Quick efficiency and rate calculations
- **Info Panel**: Poling domain specifications for fabrication

Combine multiple panels in your workspace to gain comprehensive insight into your SPDC source design. Each panel auto-updates when you change parameters, enabling rapid iteration and optimization.
