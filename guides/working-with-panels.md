# Working with Calculation Panels

Calculation panels are the primary interface for visualizing and analyzing SPDC properties in SPDCalc. Each panel displays a different aspect of your crystal configuration, from joint spectral intensities to Hong-Ou-Mandel interference patterns. You can add multiple panels simultaneously to compare different analyses side-by-side, and panels automatically update when you change parameters (unless you disable this behavior).

## Adding and Removing Panels

SPDCalc uses a flexible panel system that lets you customize your workspace by adding only the calculation panels you need.

### Adding a Panel

{% stepper %}
{% step %}
#### Locate the Panel Loader

When you first open SPDCalc or after removing panels, you'll see a dotted-border card labeled "load plot" in the main workspace area. This is the panel loader.

<figure>
<img src="../.gitbook/assets/screenshots/interface/panel-loader.png" alt="Panel loader card with dotted border">
<figcaption>The panel loader appears as a dotted-border card that says "load plot" when you hover over it</figcaption>
</figure>
{% endstep %}

{% step %}
#### Open the Panel Menu

Click on the panel loader card to reveal a list of all available panel types. The menu displays each panel with its descriptive name.

<figure>
<img src="../.gitbook/assets/screenshots/interface/panel-menu-open.png" alt="Open panel selection menu">
<figcaption>Click the panel loader to see all available calculation panels</figcaption>
</figure>
{% endstep %}

{% step %}
#### Select Your Panel

Click on any panel type from the list to add it to your workspace. The panel will immediately load and begin calculating based on your current parameter configuration.

Once added, a new panel loader will automatically appear, allowing you to add additional panels without limit.
{% endstep %}
{% endstepper %}

### Removing a Panel

Each panel includes a close button (red "X" icon) in the top-right corner of its toolbar. Click this button to remove the panel from your workspace. There is no confirmation dialog, so the panel will be removed immediately.

<figure>
<img src="../.gitbook/assets/screenshots/interface/panel-close-button.png" alt="Panel close button highlighted">
<figcaption>Click the red X button to remove a panel from your workspace</figcaption>
</figure>

{% hint style="info" %}
Removing a panel does not affect your parameter configuration. If you re-add the same panel type later, it will recalculate using the current parameters.
{% endhint %}

### Arranging Panels

Panels are arranged in a responsive grid layout. SPDCalc automatically positions panels to make efficient use of available screen space. When you add or remove panels, the remaining panels will reflow to fill the workspace.

## Available Panel Types

SPDCalc offers several specialized calculation panels, each designed to visualize a specific aspect of SPDC behavior. Below is a complete list of available panel types with brief descriptions.

### Joint Spectrum Intensity (JSI) Plot

Visualizes the two-photon joint spectral amplitude, showing correlations between signal and idler photons. This panel displays both intensity and amplitude distributions and calculates the Schmidt number to quantify entanglement. You can view the spectrum in wavelength space, frequency space, or sum-difference coordinates.

### Phasematching Curves

Displays phasematching conditions as a function of wavelength. This panel helps you understand and optimize your crystal configuration by showing where phasematching occurs across the spectral range of interest.

### Schmidt Number Analysis

Analyzes photon pair entanglement through Schmidt decomposition as a function of both pump bandwidth and crystal length. This 2D plot helps you understand how these parameters affect the degree of entanglement in your SPDC source.

### Hong-Ou-Mandel Dip

Calculates the Hong-Ou-Mandel interference visibility for single-source setups. This panel plots coincidence rates versus time delay and computes the visibility parameter, which characterizes photon indistinguishability. Use this panel to assess the quality of single-photon sources for quantum information applications.

### Two-Source HOM Dip

Simulates Hong-Ou-Mandel interference from two independent SPDC sources. This analysis is particularly useful for quantum networking applications where you need to interfere photons from separate sources.

### Heralding Efficiency Analysis

Analyzes heralding efficiency versus signal and idler beam waist sizes (or pump versus signal/idler waist sizes, depending on the variant selected). This 2D heatmap helps you optimize collection mode matching by identifying the optimal waist size combinations for maximum heralding efficiency.

Two variants are available:
- **Signal vs Idler waist**: Shows efficiency as signal waist varies against idler waist
- **Pump vs S/I waist**: Shows efficiency as pump waist varies against signal/idler waist (assuming equal signal and idler waists)

### Heralding Calculator

A quick calculation tool that displays the heralding efficiency and expected coincidence counts for your specific configuration. Unlike the analysis panels that sweep parameters, this calculator provides instant results for the current parameter values.

### Info Panel

Displays calculated crystal information including refractive indices, optimum idler wavelength and angle, and periodic poling domain specifications. This panel also allows you to export poling domain data as JSON for fabrication purposes.

{% hint style="info" %}
For detailed explanations of each panel's calculations, interpretation of results, and advanced usage, see the Calculation Panels Reference section.
{% endhint %}

## Understanding Auto-Update

Each calculation panel includes an auto-update feature that controls whether the panel automatically recalculates when you change SPDC parameters.

### Auto-Update Behavior

By default, all panels have auto-update **enabled**. This means:

- Whenever you modify any parameter in the settings drawer (crystal type, wavelength, angles, etc.), the panel immediately recalculates
- Changes are debounced by 100 milliseconds, so rapid parameter adjustments don't trigger excessive calculations
- The panel displays a "calculating..." status message and shows a loading indicator during recalculation
- Results automatically update when the calculation completes

This behavior provides immediate visual feedback as you explore the parameter space, making it easy to understand how different settings affect SPDC properties.

### Disabling Auto-Update

For some workflows, automatic recalculation can be disruptive or slow, especially with:
- High-resolution calculations that take several seconds
- Complex parameter sweeps where you're adjusting multiple settings sequentially
- Exploratory analysis where you want to freeze one panel while experimenting with parameters for another

To disable auto-update for a panel:

{% stepper %}
{% step %}
#### Click the Lock Icon

Locate the lock icon in the panel's toolbar (top-right area, next to the refresh button). When auto-update is enabled, the icon shows an open lock.

<figure>
<img src="../.gitbook/assets/screenshots/interface/auto-update-enabled.png" alt="Auto-update enabled showing open lock icon">
<figcaption>Open lock icon indicates auto-update is enabled</figcaption>
</figure>
{% endstep %}

{% step %}
#### Toggle to Locked State

Click the lock icon to disable auto-update. The icon changes to a closed lock and turns yellow. The panel's border also changes appearance to indicate the locked state.

<figure>
<img src="../.gitbook/assets/screenshots/interface/auto-update-disabled.png" alt="Auto-update disabled showing closed lock icon in yellow">
<figcaption>Closed yellow lock icon indicates auto-update is disabled</figcaption>
</figure>
{% endstep %}

{% step %}
#### Manual Refresh

With auto-update disabled, the panel will not recalculate when parameters change. To update the panel manually, click the refresh icon (circular arrow) in the panel toolbar.

<figure>
<img src="../.gitbook/assets/screenshots/interface/manual-refresh-button.png" alt="Manual refresh button">
<figcaption>Click the refresh button to manually recalculate when auto-update is disabled</figcaption>
</figure>
{% endstep %}
{% endstepper %}

### Tooltips

Hover over the lock icon to see a tooltip explaining the current state:
- **Open lock**: "This plot will auto-update with parameter changes"
- **Closed lock**: "Not auto-updating, unless manually requested"

### Canceling Calculations

If a calculation is taking longer than expected, you can cancel it at any time by clicking the red cancel button (X icon) that appears in the toolbar during calculation. This immediately stops the computation and allows you to adjust parameters or disable auto-update before trying again.

{% hint style="warning" %}
Canceling a calculation stops the work in progress but does not preserve partial results. If you cancel, you'll need to recalculate to see updated data.
{% endhint %}

### Performance Considerations

Auto-update settings are saved per-panel and persist across sessions (when using URL-based state sharing or saved presets). This allows you to create optimized workspace configurations where, for example, fast panels like the Info Panel auto-update while slower panels like high-resolution JSI plots remain locked.

For guidance on optimizing calculation performance, see the Performance Considerations section in Working with Results.
