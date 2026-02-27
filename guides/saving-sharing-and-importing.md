# Saving, Sharing, and Importing

SPDCalc provides several ways to save your SPDC configurations, share them with colleagues, and import settings from files or URLs.

## Saving Configurations as Presets

Presets allow you to save your current SPDC parameter configuration for later use and quick switching between different experimental setups. The preset system stores all your configurations locally in your browser, making it easy to maintain a library of commonly used setups.

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

The preset is immediately saved and becomes the currently loaded preset.

### What Gets Saved in a Preset

When you create a preset, SPDCalc saves a complete snapshot of your parameter configuration.

{% hint style="info" %}
Presets do NOT save which calculation panels you have open or their individual settings. Only the SPDC parameter configuration is stored. Panel state is managed separately through the URL sharing feature.
{% endhint %}

### Updating an Existing Preset

If you've loaded a preset and then modified its parameters, you can update the preset to reflect your changes.

Make changes to any SPDC parameters while a preset is loaded. The save button in the toolbar will change appearance to indicate unsaved changes.

Click the save icon in the top toolbar (next to the preset dropdown). This icon appears as a floppy disk and changes color when there are unsaved modifications.

<figure>
<img src="../.gitbook/assets/screenshots/presets/save-preset-button.png" alt="Save button in toolbar">
<figcaption>Click the save icon to update the currently loaded preset with your changes</figcaption>
</figure>

The preset is immediately updated with your current parameter values.

{% hint style="warning" %}
Saving updates overwrites the existing preset. There is no undo functionality, so if you want to preserve the original configuration, create a new preset with a different name instead of updating the existing one.
{% endhint %}

## Sharing via URL

Every time you modify parameters or panels in SPDCalc, your complete configuration is automatically encoded into the URL in your browser's address bar. This means you can share your exact setup with colleagues simply by copying and pasting the URL.

## Importing/Exporting JSON Settings

For complex configurations, long-term storage, or version control, you can export your SPDC parameters to a JSON file. This is especially useful when:

- You want to use JSON with the python or rust libraries
- You want to save configurations to disk for archival purposes
- You're tracking configuration changes in version control (Git)
- You need to programmatically generate or modify configurations

{% hint style="info" %}
JSON export saves your SPDC **parameters only** (crystal settings, pump configuration, signal settings, integration parameters). Panel configurations and selections are **not** included in JSON files - use URLs for sharing complete application state with panels.
{% endhint %}

### Exporting Settings to JSON

Click the three-dot menu icon (⋮) in the top-right corner of the application toolbar.

<figure>
<img src="../.gitbook/assets/screenshots/interface/options-menu.png" alt="Options menu in toolbar">
<figcaption>The options menu provides access to import and export functions</figcaption>
</figure>

Choose "Export Settings" from the dropdown menu. The Export Settings dialog will open showing the JSON.

### Importing Settings from JSON

Click the three-dot menu icon (⋮) in the top-right corner of the toolbar. Choose "Import Settings" from the dropdown menu. The Import Settings dialog will open.

<figure>
<img src="../.gitbook/assets/screenshots/sharing/import-dialog.png" alt="Import Settings dialog with text area for JSON">
<figcaption>The Import Settings dialog accepts JSON configuration text</figcaption>
</figure>

Paste your JSON configuration text into the text area.
