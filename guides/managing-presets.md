# Managing Presets

Presets allow you to save your current SPDC parameter configuration for later use and quick switching between different experimental setups. Instead of manually re-entering crystal settings, wavelengths, and other parameters each time you switch between configurations, you can save them as named presets and load them with a single click. The preset system stores all your configurations locally in your browser, making it easy to maintain a library of commonly used setups.

## Saving Configurations

When you've configured your SPDC parameters to represent a specific experimental setup, you can save that configuration as a preset for future use.

### Creating a New Preset

{% stepper %}
{% step %}
#### Enter a Preset Name

Click on the preset dropdown in the top toolbar (labeled "select/create preset"). Type a name for your new preset in the text field. Choose descriptive names that help you identify the configuration later, such as "KTP Type-II 810nm" or "BBO Collinear Degenerate".

<figure>
<img src="../.gitbook/assets/screenshots/presets/preset-name-entry.png" alt="Typing a new preset name in the dropdown field">
<figcaption>Enter a descriptive name for your preset in the dropdown field</figcaption>
</figure>
{% endstep %}

{% step %}
#### Create the Preset

Once you've typed a name that doesn't match any existing preset, a "Create [preset name]" option appears at the bottom of the dropdown menu. Click this option to save your current parameter configuration under the new name.

<figure>
<img src="../.gitbook/assets/screenshots/presets/create-preset-button.png" alt="Create preset option in dropdown menu">
<figcaption>Click the "Create" option to save your configuration</figcaption>
</figure>

The preset is immediately saved and becomes the currently loaded preset. You can now modify parameters and create additional presets as needed.
{% endstep %}
{% endstepper %}

### What Gets Saved in a Preset

When you create a preset, SPDCalc saves a complete snapshot of your parameter configuration, including:

- Crystal type, phasematching type, orientation angles (theta/phi), length, and temperature
- Pump laser wavelength, bandwidth, beam waist, and power settings
- Signal photon wavelength, collection angles, and beam waist configuration
- Periodic poling settings (if enabled), including period and apodization
- Integration settings such as wavelength ranges and grid resolution
- Auto-calculation toggle states for derived parameters

{% hint style="info" %}
Presets do NOT save which calculation panels you have open or their individual settings. Only the SPDC parameter configuration is stored. Panel state is managed separately through the URL sharing feature.
{% endhint %}

### Updating an Existing Preset

If you've loaded a preset and then modified its parameters, you can update the preset to reflect your changes.

{% stepper %}
{% step %}
#### Modify Your Parameters

Make changes to any SPDC parameters while a preset is loaded. The save button in the toolbar will change appearance to indicate unsaved changes (see Understanding the Dirty State section below).
{% endstep %}

{% step %}
#### Save Your Changes

Click the save icon in the top toolbar (next to the preset dropdown). This icon appears as a floppy disk and changes color when there are unsaved modifications.

<figure>
<img src="../.gitbook/assets/screenshots/presets/save-preset-button.png" alt="Save button in toolbar">
<figcaption>Click the save icon to update the currently loaded preset with your changes</figcaption>
</figure>

The preset is immediately updated with your current parameter values. The dirty state indicator disappears, confirming the save was successful.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Saving updates overwrites the existing preset. There is no undo functionality, so if you want to preserve the original configuration, create a new preset with a different name instead of updating the existing one.
{% endhint %}

### Best Practices for Naming Presets

Clear, consistent naming conventions help you maintain an organized preset library:

- **Include key parameters**: "BBO-Type1-405nm-pump" is more informative than "Setup 1"
- **Reference experiments**: "HOM-visibility-test" or "Heralding-optimization-run3"
- **Use consistent format**: Establish a pattern like "Crystal-Type-Wavelength" across all presets
- **Keep names concise**: Very long names may be truncated in the dropdown display
- **Use dates when iterating**: "KTP-810nm-2026-02-10" helps track configuration evolution

## Loading Presets

Once you've created presets, you can quickly switch between different parameter configurations using the preset selector.

### Selecting a Preset

{% stepper %}
{% step %}
#### Open the Preset Dropdown

Click on the preset dropdown in the top toolbar. If you currently have a preset loaded, it displays that preset's name. Otherwise, it shows "(select/create preset)".

<figure>
<img src="../.gitbook/assets/screenshots/presets/preset-dropdown.png" alt="Preset dropdown menu showing available presets">
<figcaption>The preset dropdown displays all your saved configurations</figcaption>
</figure>
{% endstep %}

{% step %}
#### Choose Your Configuration

Click on any preset name in the dropdown list. SPDCalc immediately loads all parameters from that preset, replacing your current configuration.

All calculation panels with auto-update enabled will automatically recalculate using the newly loaded parameters.
{% endstep %}
{% endstepper %}

### What Happens When You Load a Preset

Loading a preset performs these actions:

1. **Replaces all parameters**: Every SPDC parameter is set to the value stored in the preset
2. **Triggers recalculation**: Panels with auto-update enabled immediately recalculate with the new parameters
3. **Clears dirty state**: The configuration matches the saved preset, so the dirty state indicator (if present) disappears
4. **Updates the dropdown**: The preset selector displays the name of the loaded preset

{% hint style="info" %}
Loading a preset does not change which calculation panels are open. If you want to save both parameters and panel configuration, use the URL sharing feature described in the Sharing and Importing section.
{% endhint %}

### Deselecting a Preset

You can work with parameters without having any preset loaded. To deselect the current preset:

1. Click on the preset dropdown
2. Click on the dropdown field itself (where the preset name is shown)
3. Delete the text or select the empty option at the top of the list

When no preset is loaded, you can still modify parameters freely. The save button will be disabled since there's no preset to update.

## Editing and Deleting Presets

As your preset library grows, you'll need to rename presets for clarity or remove configurations you no longer use.

### Renaming a Preset

{% stepper %}
{% step %}
#### Enter Edit Mode

Click on the preset dropdown to view your preset list. Each preset has a pencil (edit) icon on the right side. Click the edit icon for the preset you want to rename.

<figure>
<img src="../.gitbook/assets/screenshots/presets/preset-edit-icon.png" alt="Edit icon next to preset name">
<figcaption>Click the edit icon to rename a preset</figcaption>
</figure>

The preset name changes to an editable text field, allowing you to modify it.
{% endstep %}

{% step %}
#### Enter the New Name

Type the new name for your preset in the text field. You can use any characters, but avoid extremely long names that may be truncated in the display.

<figure>
<img src="../.gitbook/assets/screenshots/presets/preset-rename-field.png" alt="Text field for renaming preset">
<figcaption>Edit the preset name directly in the text field</figcaption>
</figure>
{% endstep %}

{% step %}
#### Save the New Name

Click the checkmark icon that appears next to the text field, or press Enter on your keyboard. The preset is immediately renamed, and the dropdown returns to normal display mode.

If you want to cancel the rename operation, click outside the dropdown without clicking the checkmark.
{% endstep %}
{% endstepper %}

### Deleting a Preset

{% stepper %}
{% step %}
#### Enter Edit Mode

Click the edit icon next to the preset you want to delete. The preset name becomes editable, and a delete icon (trash can) appears.

<figure>
<img src="../.gitbook/assets/screenshots/presets/preset-delete-icon.png" alt="Delete icon in edit mode">
<figcaption>The delete icon appears when you enter edit mode for a preset</figcaption>
</figure>
{% endstep %}

{% step %}
#### Confirm Deletion

Click the red delete icon. The preset is immediately removed from your preset library.

{% hint style="danger" %}
Deletion is permanent and there is no confirmation dialog. Once deleted, a preset cannot be recovered unless you saved it externally using JSON export or URL sharing.
{% endhint %}
{% endstep %}
{% endstepper %}

### Managing the Loaded Preset

If you delete the currently loaded preset, SPDCalc automatically deselects it. Your current parameter values remain unchanged, but you're no longer working with a saved preset. You can create a new preset to save those parameters if needed.

## Understanding the Dirty State

The dirty state indicator helps you track when your current parameter configuration differs from the loaded preset. This prevents accidental loss of work and helps you understand whether your changes have been saved.

### What Is the Dirty State?

The dirty state occurs when:

1. You have a preset loaded (shown in the preset dropdown)
2. You modify one or more SPDC parameters
3. The current parameter values no longer match the saved values in the preset

SPDCalc detects this mismatch and displays a visual indicator to warn you that your changes haven't been saved to the preset.

### Recognizing the Dirty State Indicator

When the dirty state is active, the save button in the toolbar changes appearance:

- **Normal state** (clean): The save button shows a standard floppy disk icon in green and is disabled
- **Dirty state**: The save button shows a floppy disk with an alert symbol in orange/yellow and becomes clickable

<figure>
<img src="../.gitbook/assets/screenshots/presets/dirty-state-indicator.png" alt="Dirty state indicator showing orange save button with alert">
<figcaption>The orange save icon with alert symbol indicates unsaved parameter changes</figcaption>
</figure>

This visual feedback makes it immediately clear whether your current configuration matches the loaded preset.

### When the Dirty State Appears

The dirty state indicator appears in these situations:

- **Parameter modification**: You change any SPDC parameter while a preset is loaded
- **Auto-calculated changes**: Even changes to auto-calculated parameters (like crystal theta angle) trigger the dirty state if they differ from the preset
- **Small floating-point differences**: Due to floating-point precision, even seemingly identical values might trigger the indicator if they differ at a very small decimal place

### When the Dirty State Disappears

The dirty state clears when:

- **You save changes**: Clicking the save button updates the preset and clears the indicator
- **You reload the preset**: Selecting the same preset again from the dropdown restores the saved values
- **You load a different preset**: Loading another preset replaces all parameters, and the indicator shows the state relative to the new preset
- **You deselect the preset**: Clearing the preset selection removes the reference point, so there's no dirty state to track

### Working with the Dirty State

The dirty state indicator is informational only. You can continue working with unsaved changes for as long as you want. SPDCalc never automatically saves or prompts you to save changes.

**Common workflows:**

1. **Experimental exploration**: Load a preset, modify parameters to explore variations, then reload the preset to reset without saving changes
2. **Iterative refinement**: Load a preset, make small adjustments, save to update the preset, repeat as you optimize your configuration
3. **Branching configurations**: Load a preset, modify it, then save as a new preset (by typing a new name) to create variations while preserving the original

{% hint style="info" %}
If you navigate away from SPDCalc or close the browser tab while in a dirty state, your changes will be lost. The preset system only stores saved presets, not temporary modifications. Use the save button before leaving if you want to preserve your changes.
{% endhint %}

### Dirty State and URL Sharing

The dirty state only affects preset saving. Your current parameter configuration (including unsaved changes) is always reflected in the URL if you use the sharing feature. This means:

- The URL always represents your current state, regardless of dirty status
- Sharing a URL in dirty state shares your modified parameters, not the saved preset values
- Loading a shared URL may result in a dirty state if it differs from the loaded preset

For more information on URL-based configuration sharing, see the Sharing and Importing section.
