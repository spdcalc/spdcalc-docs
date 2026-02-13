# GitBook Documentation Guide for SPDCalc

This repository contains GitBook documentation for the SPDCalc application. This guide provides information about GitBook-specific features and conventions.

## Core GitBook Structure

### SUMMARY.md - Table of Contents
The `SUMMARY.md` file controls the navigation structure of your GitBook site. It must be kept up-to-date whenever pages are added or reorganized.

**Structure:**
```markdown
# Table of contents

* [Welcome](README.md)

## Section Name

* [Page Title](folder/page.md)
* [Another Page](folder/another-page.md)
```

### README.md - Home Page
The `README.md` file serves as the home page of the documentation site. It should provide an overview and navigation to key sections.

### Folder Organization
- Organize pages into logical folders (e.g., `basics/`, `getting-started/`, `advanced/`)
- Each page is a separate `.md` file
- Reference pages in SUMMARY.md using relative paths

## GitBook-Specific Markdown Features

### Frontmatter with Icons
Add icons to pages using YAML frontmatter at the top of any markdown file:

```markdown
---
icon: hand-wave
---

# Page Title
```

**Common icons:** `hand-wave`, `bolt`, `markdown`, `hand-pointer`, `image-landscape`, `plug-circle-plus`, `globe-pointer`, `pen-to-square`, `leaf`

### Hint Blocks
Use hint blocks to highlight important information:

```markdown
{% hint style="info" %}
This is an informational hint.
{% endhint %}
```

**Styles:** `info`, `warning`, `danger`, `success`

### Tabs
Create tabbed content for alternative options or multiple code examples:

```markdown
{% tabs %}
{% tab title="First tab" %}
Content for the first tab goes here. Can include any blocks.
{% endtab %}

{% tab title="Second tab" %}
Content for the second tab.

```javascript
// Code blocks work in tabs
console.log("Hello");
```
{% endtab %}
{% endtabs %}
```

### Stepper Blocks
Create step-by-step guides:

```markdown
{% stepper %}
{% step %}
#### Step 1 Title

Instructions for step 1.
{% endstep %}

{% step %}
#### Step 2 Title

Instructions for step 2.
{% endstep %}
{% endstepper %}
```

### Expandable Sections
Use HTML details/summary tags for collapsible content:

```markdown
<details>
<summary>Click to expand</summary>

Hidden content goes here. Great for FAQs and optional details.

</details>
```

### Embed Blocks
Embed external content (YouTube, CodePen, etc.):

```markdown
{% embed url="https://www.youtube.com/watch?v=VIDEO_ID" %}
```

GitBook supports thousands of embeddable sites via [iframely](https://iframely.com).

### Card Tables
Create visual card-based layouts using special table attributes:

```markdown
<table data-view="cards">
<thead>
<tr>
<th></th>
<th></th>
<th data-hidden data-card-target data-type="content-ref"></th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Card Title</strong></td>
<td>Card description</td>
<td><a href="link-to-page.md">link-to-page.md</a></td>
</tr>
</tbody>
</table>
```

**Attributes:**
- `data-view="cards"` - Display as cards
- `data-card-size="large"` - Large card size
- `data-card-target` - Makes column a link target
- `data-card-cover` - Makes column an image cover
- `data-hidden` - Hides column in display

### Figures with Captions
Add images with captions using figure tags:

```markdown
<figure>
<img src="path/to/image.png" alt="Alt text">
<figcaption>Caption text goes here</figcaption>
</figure>
```

## Standard Markdown Support

GitBook fully supports standard Markdown:
- Headings: `#`, `##`, `###`
- Lists: `-` or `*` for bullets, `1.` for numbered
- Links: `[text](url)`
- Code blocks: Triple backticks with language
- Emphasis: `**bold**`, `*italic*`, `~~strikethrough~~`
- Tables: Standard markdown tables
- Blockquotes: `>`

## Best Practices for SPDCalc Documentation

### Content Organization
1. Keep the home page (README.md) concise with clear navigation
2. Group related topics in folders
3. Update SUMMARY.md whenever adding/removing pages
4. Use descriptive file names (e.g., `quick-start-guide.md`)

### Writing Style
1. Use hint blocks for important notes and warnings
2. Use tabs for alternative approaches or language-specific examples
3. Use stepper blocks for sequential tutorials
4. Add icons to pages to improve visual navigation
5. Include alt text for all images
6. Use expandable sections to avoid overwhelming readers

### Images and Media
1. Store images in an `assets/` folder or reference them by URL
2. Always include alt text for accessibility
3. Add captions using `<figcaption>` to provide context
4. Images can be drag-and-dropped in the GitBook editor

### Code Examples
1. Use language-specific code blocks for syntax highlighting
2. Keep code examples concise and focused
3. Consider using tabs when showing the same operation in different languages/tools
4. Include comments in code to explain non-obvious parts

### Internal Links
- Link to other pages using relative paths: `[Page Title](../folder/page.md)`
- Link to sections using anchors: `[Section](#section-heading)`
- Ensure all links in SUMMARY.md point to valid files

### Git Sync Considerations
- GitBook can sync bidirectionally with GitHub/GitLab
- Keep markdown clean and valid for both GitBook and GitHub rendering
- Commit changes regularly
- Use meaningful commit messages for documentation updates

## Testing Your Documentation

Before publishing:
1. Check that all links in SUMMARY.md are valid
2. Verify all internal links work correctly
3. Test that images load properly
4. Review hint blocks render correctly
5. Ensure code blocks have proper syntax highlighting

## Publishing

Documentation can be published from the GitBook interface. Once published, the site will be accessible online to your selected audience.

## Additional Resources

- Press `/` in the GitBook editor to see available blocks
- GitBook supports importing existing Markdown files
- Check [iframely.com](https://iframely.com) for supported embed URLs
- GitBook integrations can add analytics, support widgets, and more
