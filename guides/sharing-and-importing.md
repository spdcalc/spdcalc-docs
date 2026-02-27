# Sharing and Importing

SPDCalc provides two methods for saving and sharing your SPDC configurations: automatic URL encoding and JSON file import/export.

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
