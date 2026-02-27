# Working with Calculation Panels

Calculation panels are the primary interface for visualizing and analyzing SPDC properties in SPDCalc. Each panel displays a different calculations based on your crystal configuration, from joint spectral intensities to Hong-Ou-Mandel interference plots. You can add multiple panels simultaneously to compare different analyses side-by-side, and panels automatically update when you change parameters (unless you disable this behavior).

## Adding and Removing Panels

SPDCalc uses a flexible panel system that lets you customize your workspace by adding only the calculation panels you need.

### Adding and Removing Panels

Panels are added by clicking the blue "empty" panel space. To remove a panel you can click the red "x" at the top right of the panel.

### Arranging Panels (not possible yet)

Panels are arranged in the order they are added. Unfortunately for now, there is no way to drag and drop to reorder them.

## Available Panel Types

SPDCalc offers several specialized calculation panels, each designed to visualize a specific aspect of SPDC behavior. Below is a complete list of available panel types with brief descriptions.

### Joint Spectrum Intensity (JSI) Plot

Visualizes the two-photon joint spectral amplitude, showing correlations between signal and idler photons. This panel displays both intensity and amplitude distributions and calculates the Schmidt number to quantify entanglement. You can view the spectrum in wavelength space, frequency space, or sum-difference coordinates.

### Phasematching Curves

Displays a histogram (like the JSI) for various customizable parameter sweeps like photon angles, wavelengths, crystal length, etc.

### Schmidt Number Analysis

Analyzes photon pair entanglement through Schmidt decomposition as a function of both pump bandwidth and crystal length.

### Hong-Ou-Mandel Dip

Calculates the Hong-Ou-Mandel interference visibility for single-source setups. This panel plots coincidence rates versus time delay.

### Two-Source HOM Dip

Calculates Hong-Ou-Mandel interference from two independent SPDC sources.

### Heralding vs Waist Size

A double sized panel showing line plots of efficiency and counts/s vs waist size, and a JSI showing the signal/idler singles and coincidences overlap. The singles/coincidences data can be shown or hidden by clicking on the legend above the JSI.

### Counts vs Fiber Theta

A plot showing signal, idler, and coincidences rates for signal theta values. There is also a slider to calculate exact values for efficiency and counts for a specific signal theta.

### Heralding Efficiency Analysis

Analyzes heralding efficiency versus signal and idler beam waist sizes (or pump versus signal/idler waist sizes, depending on the variant selected). This 2D heatmap helps you optimize collection mode matching by identifying the optimal waist size combinations for maximum heralding efficiency.

Two variants are available:
- **Signal vs Idler waist**: Shows efficiency as signal waist varies against idler waist
- **Pump vs S/I waist**: Shows efficiency as pump waist varies against signal/idler waist (assuming equal signal and idler waists)

### Heralding Calculator

A quick calculation tool that displays the heralding efficiency and expected coincidence counts for your specific configuration. Unlike the analysis panels that sweep parameters, this calculator provides instant results for the current parameter values and specific waist sizes.

### Info Panel

Shows the calculated poling domains for periodic poling.

## Understanding Auto-Update

Each calculation panel includes an auto-update feature that controls whether the panel automatically recalculates when you change SPDC parameters.

### Auto-Update Behavior

By default, all panels have auto-update **enabled**. This means:

- Whenever you modify any parameter in the settings drawer (crystal type, wavelength, angles, etc.), the panel immediately recalculates
- Updates are throttled so rapid parameter adjustments don't trigger excessive calculations
- The panel displays a "calculating..." status message and shows a loading indicator during recalculation
- Results automatically update when the calculation completes

### Disabling Auto-Update

For some workflows, automatic recalculation can be disruptive or slow, especially with:
- High-resolution calculations that take several seconds
- Adjusting multiple settings sequentially
- Exploratory analysis where you want to freeze one panel while experimenting with parameters for another

To disable auto-update for a panel click the "lock" icon.

<figure>
<img src="../.gitbook/assets/screenshots/interface/auto-update-disabled.png" alt="Auto-update disabled showing closed lock icon in yellow">
<figcaption>Closed yellow lock icon indicates auto-update is disabled</figcaption>
</figure>

### Manual Refresh

With auto-update disabled, the panel will not recalculate when parameters change. To update the panel manually, click the refresh icon (circular arrow) in the panel toolbar.

<figure>
<img src="../.gitbook/assets/screenshots/interface/manual-refresh-button.png" alt="Manual refresh button">
<figcaption>Click the refresh button to manually recalculate when auto-update is disabled</figcaption>
</figure>

### Canceling Calculations

If a calculation is taking longer than expected, you can cancel it at any time by clicking the red cancel button that replaces the refresh button.

{% hint style="warning" %}
Canceling a calculation stops the work in progress but does not preserve partial results. If you cancel, you'll need to recalculate to see updated data.
{% endhint %}
