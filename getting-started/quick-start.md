# Getting Started

This guide will help you get started with the web interface and understand the key components of the application.

## Opening the Application

The [SPDCalc web app](https://app.spdcalc.org) is a web-based application that runs entirely in your browser, requiring no installation or downloads.

{% hint style="success" %}
SPDCalc runs entirely in your browser. Your configurations are saved in the URL, and you can share configurations via URL or export the parameters as JSON files.
{% endhint %}

## Understanding the Interface

SPDCalc's interface is organized into three primary areas:

<figure>
<img src=".gitbook/assets/screenshots/interface/main-window-overview.png" alt="SPDCalc main window showing the three-area layout with settings drawer, calculation panels, and toolbar">
<figcaption>The SPDCalc interface consists of three main areas: settings drawer (left), calculation panels (center), and toolbar (top)</figcaption>
</figure>

### Settings Drawer (Left Panel)

The settings drawer is your primary control center for configuring SPDC parameters. It contains five collapsible sections that organize all the configuration options you'll need.

<figure>
<img src=".gitbook/assets/screenshots/interface/settings-drawer-expanded.png" alt="Settings drawer showing all five collapsible sections: Crystal, Periodic Poling, Pump, Signal, and Integration">
<figcaption>The settings drawer organizes parameters into five logical groups</figcaption>
</figure>

**The five settings sections are:**

1. **Crystal** - Select your crystal type (BBO, KTP, LiNbO₃, etc.), configure phasematching type (Type 0, Type 1, Type 2), set crystal orientation angles (theta/phi), length, and temperature.

2. **Periodic Poling** - Enable quasi-phasematching for periodically poled crystals, configure the poling period, and set up apodization profiles if needed.

3. **Pump** - Configure your pump laser parameters including wavelength, bandwidth, beam waist size, power, and spectrum threshold settings.

4. **Signal** - Set signal photon properties including wavelength, collection angles (theta/phi), beam waist size, and waist position along the crystal.

5. **Integration** - Adjust numerical integration settings including wavelength ranges, grid resolution, and integration methods for calculations.

**Toggling the drawer:**

You can show or hide the settings drawer by clicking the menu icon (three horizontal lines) in the top-left corner of the toolbar. This gives you more space to view calculation results when you don't need to adjust parameters.

{% hint style="info" %}
Many parameters have auto-calculation features enabled by default. For example, the crystal theta angle can be automatically calculated based on your wavelength settings and phasematching type. Look for small indicators or buttons next to parameter fields that enable/disable auto-calculation.
{% endhint %}

### Calculation Panels (Center Area)

The center area is where your calculation results are displayed. This area uses a responsive grid layout that can contain multiple calculation panels simultaneously.

**Key features:**

- **Dynamic panel loading** - Start with an empty grid and add only the panels you need
- **Multiple panels** - View several different calculations at once (JSI plots, phasematching curves, Schmidt number analysis, etc.)
- **Responsive layout** - Panels automatically arrange themselves based on your screen size
- **Individual panel controls** - Each panel has its own toolbar with refresh, auto-update toggle, and close buttons

**Adding your first panel:**

When you first open SPDCalc, you'll see empty placeholder cards with dashed borders in the calculation area. These are panel loaders.

<figure>
<img src=".gitbook/assets/screenshots/interface/panel-loader-card.png" alt="Empty panel loader card with dashed border and 'load plot' text on hover">
<figcaption>Click any panel loader card to see the available calculation types</figcaption>
</figure>

{% stepper %}
{% step %}
#### Click a panel loader

Hover over any empty panel card (you'll see "load plot" appear) and click it.
{% endstep %}

{% step %}
#### Select a panel type

A list of available calculation panels will appear. Common starting points include:
- **JSI Plot** - Visualize the joint spectral intensity of your photon pairs
- **Phasematching Curves** - See how phasematching varies with wavelength
{% endstep %}

{% step %}
#### Wait for calculation

The panel will load and automatically perform its first calculation using your current parameter settings. You'll see a progress indicator while the calculation runs.
{% endstep %}
{% endstepper %}

**Panel toolbar controls:**

<figure>
<img src=".gitbook/assets/screenshots/interface/panel-toolbar-controls.png" alt="Close-up of panel toolbar showing lock icon, refresh button, and close button">
<figcaption>Each panel has controls for auto-update, manual refresh, and removal</figcaption>
</figure>

Each calculation panel includes these controls in its title bar:

- **Lock/Unlock icon** - Toggle auto-update behavior. When unlocked (default), the panel automatically recalculates whenever you change parameters. When locked, you must manually trigger recalculation.
- **Refresh button** - Manually trigger a recalculation of this panel
- **Cancel button** (appears during calculation) - Stop a running calculation
- **Close (X) button** - Remove this panel from the grid

{% hint style="warning" %}
Panels with auto-update locked will show a yellow border to remind you that they won't update automatically. This is useful when you want to freeze one calculation while exploring variations in other panels.
{% endhint %}

### Toolbar (Top)

The toolbar provides application-level controls and preset management.

<figure>
<img src=".gitbook/assets/screenshots/interface/toolbar-overview.png" alt="Application toolbar showing menu button, SPDCalc logo, preset control, and options menu">
<figcaption>The toolbar contains the menu toggle, preset controls, and application settings</figcaption>
</figure>

**Toolbar elements (left to right):**

1. **Menu icon** (☰) - Toggle the settings drawer open/closed
2. **SPDCalc logo**
3. **Preset control** (center) - A dropdown menu for managing saved configurations (on the current browser):
   - Select from previously saved presets
   - Create new presets by typing a name
   - See save status indicator (yellow alert icon when you have unsaved changes)
4. **Save button** - Saves your current configuration to the selected preset (yellow when changes are unsaved, green when saved)
5. **Options menu** (⋮) - Three-dot menu providing access to:
   - Import Settings - Load configuration from JSON file
   - Export Settings - Save configuration as JSON file
   - SPDCalc v1 - Link to the previous version
   - About - Version and credit information
