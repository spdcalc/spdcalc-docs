# Managing Presets

Presets allow you to save your current SPDC parameter configuration for later use and quick switching between different experimental setups. Instead of manually re-entering crystal settings, wavelengths, and other parameters each time you switch between configurations, you can save them as named presets and load them with a single click. The preset system stores all your configurations locally in your browser, making it easy to maintain a library of commonly used setups.

## Saving Configurations

When you've configured your SPDC parameters to represent a specific experimental setup, you can save that configuration as a preset for future use.

### Creating a New Preset

Click on the preset dropdown in the top toolbar (labeled "select/create preset"). Type a name for your new preset in the text field.

<figure>
<img src="../.gitbook/assets/screenshots/presets/preset-name-entry.png" alt="Typing a new preset name in the dropdown field">
<figcaption>Enter a descriptive name for your preset in the dropdown field</figcaption>
</figure>

Once you've typed a name that doesn't match any existing preset, a "Create [preset name]" option appears at the bottom of the dropdown menu. Click this option to save your current parameter configuration under the new name.

<figure>
<img src="../.gitbook/assets/screenshots/presets/create-preset-button.png" alt="Create preset option in dropdown menu">
<figcaption>Click the "Create" option to save your configuration</figcaption>
</figure>

The preset is immediately saved and becomes the currently loaded preset. You can now modify parameters and create additional presets as needed.

### What Gets Saved in a Preset

When you create a preset, SPDCalc saves a complete snapshot of your parameter configuration.

{% hint style="info" %}
Presets do NOT save which calculation panels you have open or their individual settings. Only the SPDC parameter configuration is stored. Panel state is managed separately through the URL sharing feature.
{% endhint %}

### Updating an Existing Preset

If you've loaded a preset and then modified its parameters, you can update the preset to reflect your changes.

Make changes to any SPDC parameters while a preset is loaded. The save button in the toolbar will change appearance to indicate unsaved changes (see Understanding the Dirty State section below).

Click the save icon in the top toolbar (next to the preset dropdown). This icon appears as a floppy disk and changes color when there are unsaved modifications.

<figure>
<img src="../.gitbook/assets/screenshots/presets/save-preset-button.png" alt="Save button in toolbar">
<figcaption>Click the save icon to update the currently loaded preset with your changes</figcaption>
</figure>

The preset is immediately updated with your current parameter values. The dirty state indicator disappears, confirming the save was successful.

{% hint style="warning" %}
Saving updates overwrites the existing preset. There is no undo functionality, so if you want to preserve the original configuration, create a new preset with a different name instead of updating the existing one.
{% endhint %}
