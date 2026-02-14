# Sharing and Importing

SPDCalc provides two powerful methods for saving and sharing your SPDC configurations: automatic URL encoding and JSON file import/export. These features enable seamless collaboration, reproducible research, and easy configuration management without requiring user accounts or cloud storage.

## Sharing via URL

Every time you modify parameters or panels in SPDCalc, your complete configuration is automatically encoded into the URL in your browser's address bar. This means you can share your exact setup with colleagues simply by copying and pasting the URL.

### How URL Sharing Works

SPDCalc uses an intelligent state management system that:

1. **Automatically encodes** your complete configuration (all SPDC parameters and active panels) into the URL query string
2. **Compresses the data** using LZUTF8 compression to keep URLs reasonably short
3. **Updates in real-time** as you make changes - no manual save action required
4. **Maintains backward compatibility** with older URL formats from previous SPDCalc versions

The URL follows this format:

```
https://spdcalc.org/?s=[BASE64_ENCODED_STATE]
```

All your settings are contained in the `s` parameter, which includes:
- Crystal type, orientation, length, and temperature
- Pump laser configuration (wavelength, bandwidth, beam waist, power)
- Signal photon settings
- Periodic poling parameters
- Integration settings
- Active calculation panels and their configurations

### Sharing Your Configuration

{% stepper %}
{% step %}
#### Step 1: Configure Your Setup

Set up your SPDC parameters and add any calculation panels you want to share. Make all adjustments until your configuration is exactly as you want it.
{% endstep %}

{% step %}
#### Step 2: Copy the URL

Simply copy the URL from your browser's address bar. The URL will look something like:

```
https://spdcalc.org/?s=N4IgdghgtgpiBcIDO...
```

<figure>
<img src="../.gitbook/assets/screenshots/sharing/url-bar-encoded-state.png" alt="Browser address bar showing encoded state in URL">
<figcaption>The browser address bar contains your complete encoded configuration</figcaption>
</figure>
{% endstep %}

{% step %}
#### Step 3: Share the Link

Send the URL to colleagues via email, paste it into documentation, or save it in your research notes. Anyone who opens the link will see your exact configuration loaded automatically.
{% endstep %}
{% endstepper %}

### Benefits of URL Sharing

**No Account Required**: Share configurations instantly without creating accounts or logging in.

**Instant Loading**: Recipients simply click the link - no file downloads or manual imports needed.

**Version Control Friendly**: URLs can be stored in plain text files, lab notebooks, or version control systems.

**Permanent Links**: Share links in published papers to ensure reproducibility of your calculations.

**Always Up-to-Date**: The URL updates automatically as you work, so you can bookmark your current state.

### Important Limitations

{% hint style="warning" %}
**URL Length Restrictions**

While SPDCalc compresses the state data efficiently, very complex configurations with many panels and custom settings can produce long URLs. Be aware of these limitations:

- **Browser limits**: Most browsers support URLs up to 2,000+ characters without issues
- **Firefox limit**: Firefox has a stricter limit of approximately 65,000 characters
- **Server limits**: Some web servers may reject very long URLs (>2KB)
- **Email clients**: Some email programs may truncate URLs longer than 2,000 characters

SPDCalc monitors URL length and will display a warning in the browser console if your configuration approaches the 60KB threshold (60,000 characters).
{% endhint %}

{% hint style="info" %}
**When URLs Become Too Long**

If you have a very complex configuration with many panels and custom settings, consider using JSON export instead (see below). JSON files have no size restrictions and are better suited for archival storage and version control.
{% endhint %}

### URL Compatibility

SPDCalc maintains backward compatibility with older URL formats. If you have links from previous versions of SPDCalc, they will continue to work. The system automatically detects and migrates old URL formats to the current schema.

## Importing/Exporting JSON Settings

For complex configurations, long-term storage, or version control, you can export your SPDC parameters to a JSON file. This is especially useful when:

- URLs become too long for convenient sharing
- You want to save configurations to disk for archival purposes
- You're tracking configuration changes in version control (Git)
- You need to programmatically generate or modify configurations
- You want to share configurations as file attachments

{% hint style="info" %}
**What Gets Exported**

JSON export saves your SPDC **parameters only** (crystal settings, pump configuration, signal settings, integration parameters). Panel configurations and selections are **not** included in JSON files - use URLs for sharing complete application state with panels.
{% endhint %}

### Exporting Settings to JSON

{% stepper %}
{% step %}
#### Step 1: Open Options Menu

Click the three-dot menu icon (⋮) in the top-right corner of the application toolbar.

<figure>
<img src="../.gitbook/assets/screenshots/interface/options-menu.png" alt="Options menu in toolbar">
<figcaption>The options menu provides access to import and export functions</figcaption>
</figure>
{% endstep %}

{% step %}
#### Step 2: Select Export Settings

Choose "Export Settings" from the dropdown menu. The Export Settings dialog will open.

<figure>
<img src="../.gitbook/assets/screenshots/sharing/export-dialog.png" alt="Export Settings dialog showing JSON configuration">
<figcaption>The Export Settings dialog displays your configuration in JSON format</figcaption>
</figure>
{% endstep %}

{% step %}
#### Step 3: Copy or Save the JSON

The dialog displays your configuration as formatted JSON text. You can:

- **Copy to clipboard**: Click the copy icon (📋) to copy the JSON to your clipboard
- **Select and copy**: Manually select all text and copy it
- **Save to file**: Copy the text and paste it into a text editor, then save with a `.json` extension

**Example filename**: `my-spdc-config.json` or `KTP-typeII-1550nm.json`
{% endstep %}
{% endstepper %}

### Importing Settings from JSON

{% stepper %}
{% step %}
#### Step 1: Open Options Menu

Click the three-dot menu icon (⋮) in the top-right corner of the toolbar.
{% endstep %}

{% step %}
#### Step 2: Select Import Settings

Choose "Import Settings" from the dropdown menu. The Import Settings dialog will open.

<figure>
<img src="../.gitbook/assets/screenshots/sharing/import-dialog.png" alt="Import Settings dialog with text area for JSON">
<figcaption>The Import Settings dialog accepts JSON configuration text</figcaption>
</figure>
{% endstep %}

{% step %}
#### Step 3: Paste JSON Configuration

Paste your JSON configuration text into the text area. You can:

- Open a `.json` file in a text editor, copy the contents, and paste
- Paste JSON that was shared with you via email or collaboration tools
- Paste from a version control system or lab notebook

{% endstep %}

{% step %}
#### Step 4: Import

Click the "Import" button. SPDCalc will:

1. Parse the JSON configuration
2. Validate the parameters using the WASM computation engine
3. Apply the settings to your current session
4. Display any errors if the JSON is invalid or incompatible

{% hint style="success" %}
After successful import, your SPDC parameters will be updated to match the imported configuration. Any active calculation panels will automatically recalculate with the new parameters.
{% endhint %}
{% endstep %}
{% endstepper %}

### Understanding the JSON Structure

<details>
<summary>Click to expand: JSON configuration structure</summary>

SPDCalc's JSON export follows this general structure:

```json
{
  "crystal": "KTP",
  "pm_type": "Type2_e_eo",
  "crystal_theta": 47.5,
  "crystal_phi": 0,
  "crystal_length": 10,
  "crystal_temperature": 20,
  "pump_wavelength": 775,
  "pump_bandwidth": 5.3,
  "pump_waist": 100,
  "pump_spectrum_threshold": 0.01,
  "signal_wavelength": 1550,
  "ls_auto": true,
  "li_auto": true,
  "periodic_poling_enabled": false,
  "poling_period": 1,
  "integrator": {
    "method": "Simpson",
    "tolerance": 100000,
    "max_depth": 10000
  }
}
```

**Key fields**:
- `crystal`: Crystal material type (e.g., "KTP", "BBO", "PPKTP")
- `pm_type`: Phase-matching type (Type 0, Type 1, Type 2 variants)
- `crystal_theta`, `crystal_phi`: Crystal orientation angles in degrees
- `pump_wavelength`, `pump_bandwidth`: Pump laser parameters in nanometers
- `signal_wavelength`: Signal photon wavelength in nanometers
- `periodic_poling_enabled`: Whether quasi-phase-matching is used
- `integrator`: Numerical integration method and tolerances

All wavelength values are in **nanometers**, angles in **degrees**, lengths in **millimeters**, and temperatures in **degrees Celsius**.

</details>

### Use Cases for JSON Export

**Archival Storage**: Save configurations to disk for long-term preservation. Unlike URLs which depend on the web application remaining available, JSON files can be stored independently.

**Version Control**: Track configuration changes over time using Git or other version control systems. JSON files produce readable diffs showing exactly what parameters changed.

**Programmatic Generation**: Write scripts to generate SPDCalc configurations automatically. For example, you could create a Python script that generates configurations for parameter sweeps.

**Collaboration**: Share configurations as email attachments or via file sharing platforms when URLs are too long or when recipients prefer file-based workflows.

**Documentation**: Include configuration files alongside research data, publications, or lab reports to ensure reproducibility.

### Differences Between URL and JSON Sharing

| Feature | URL Sharing | JSON Export |
|---------|-------------|-------------|
| **What's saved** | Parameters + Panels + Panel Settings | Parameters only |
| **How to share** | Copy/paste URL | Save file, email attachment |
| **Loading** | Automatic (click link) | Manual (paste into Import dialog) |
| **Size limits** | ~60KB browser limit | No practical limit |
| **Best for** | Quick sharing, bookmarks | Archival, version control, complex configs |
| **Backward compatibility** | Yes (old URLs still work) | Yes (validated on import) |

{% hint style="success" %}
**Best Practice**: Use URL sharing for quick collaboration and bookmarking. Use JSON export for long-term storage, documentation, and version control.
{% endhint %}

## Related Sections

- **Managing Presets** - Save frequently-used configurations for quick access
- **Working with Results** - Export calculation data as CSV files
- **Configuring SPDC Parameters** - Detailed parameter reference

---

For questions about sharing configurations or compatibility issues, please report bugs at:
- UI issues: [github.com/spdcalc/spdcalc-ui](https://github.com/spdcalc/spdcalc-ui)
- Calculation issues: [github.com/spdcalc/spdcalc](https://github.com/spdcalc/spdcalc)
