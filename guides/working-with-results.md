# Working with Results

Once your calculations are complete, SPDCalc provides powerful visualization and data export tools to help you analyze and share your SPDC results. This guide covers how to interpret visualizations, export your data, and optimize performance for your computational needs.

## Interpreting Visualizations

SPDCalc uses interactive plots and heatmaps to visualize quantum optical properties. Understanding how to read these visualizations is essential for extracting meaningful insights from your calculations.

### Understanding Color Scales

Color scales translate numerical data into visual information. SPDCalc uses different color schemes depending on the type of data:

#### Intensity and Amplitude Plots

For intensity and amplitude data, the application uses a **gradient from white (low) to blue (high)**. This uses a [LAB](https://en.wikipedia.org/wiki/CIELAB_color_space) color gradient to present numerical changes in a perceptually uniform manner.

#### Phase Plots

Phase information uses a **cyclic diverging color scale** that transitions through:
- Dark gray (−π)
- Red (−π/2)
- White (0)
- Blue (+π/2)
- Dark gray (+π)

#### Zero Highlighting

When enabled via the "eye" icon, the "highlight zero" feature makes near-zero values stand out by coloring them **red** instead of white. This is particularly useful for spotting artifacts.

## Exporting Data

SPDCalc provides multiple export options to facilitate further analysis in external tools, publication preparation, or sharing with collaborators.

### Exporting Numerical Data (JSON)

Plots include a **Download Data** button (💾 icon) in the plot toolbar. This exports the complete numerical dataset underlying the visualization.

Find the plot toolbar at the top-right corner of any panel. The download button appears as a disk/save icon.

<figure>
<img src="../.gitbook/assets/screenshots/results/export-menu-location.png" alt="Plot toolbar with download button highlighted">
<figcaption>Download button location in the plot toolbar</figcaption>
</figure>

### Exporting Plot Images (PNG)

To export a high-resolution image of any plot for presentations or publications use the button with tha camera icon in the toolbar.

<figure>
<img src="../.gitbook/assets/screenshots/results/plotly-camera-icon.png" alt="Plotly mode bar with camera icon highlighted">
<figcaption>Plotly's camera icon exports high-resolution PNG images</figcaption>
</figure>

{% hint style="info" %}
The image export captures the plot exactly as displayed on screen. Adjust zoom, pan, and axis ranges before exporting to frame your data perfectly.
{% endhint %}
