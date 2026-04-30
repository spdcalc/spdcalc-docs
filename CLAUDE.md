# Documentation Guide for SPDCalc

This repository contains documentation for the SPDCalc Web application.

## Full docsify reference

Docsify documentation itself is rendered by docsify. Fetch the following reference when more context is needed: https://docsify.js.org/_sidebar.md

Treat it like an llms.txt.

## CI

Pushes to main will automatically deploy to production. Pull requests and other branches will get a preview deployment.

## Dev preview options

```bash
# any of these...
bunx serve
npx serve
python3 -m http.server
```

## Sidebar Navigation

Sidebar content is defined in `_sidebar.md` at the project root. The `loadSidebar: true` option in `index.html` enables it.

**Format:**

```markdown
- Section Heading
  - [Page Title](folder/page.md)
  - [Another Page](folder/another-page.md)

- Another Section
  - [Topic](folder/topic.md)
```

## Callout Boxes

Provided by the `docsify-plugin-flexible-alerts` plugin. Uses blockquote syntax with a type tag.

**Syntax:**

```markdown
> [!NOTE]
> This is a note callout.

> [!TIP]
> This is a tip callout.

> [!WARNING]
> This is a warning callout.

> [!DANGER]
> This is a danger callout.
```

**Available types:** `NOTE`, `TIP`, `WARNING`, `DANGER`

You can also add a custom title on the first line:

```markdown
> [!WARNING]
> **Heads up**
> Something important to know before proceeding.
```

## Tabs

Provided by the `docsify-tabs` plugin. Tabs are delimited by HTML comments and use level-4 bold headings as tab titles.

**Syntax:**

```markdown
<!-- tabs:start -->

#### **First Tab**

Content for the first tab.

#### **Second Tab**

Content for the second tab.

```python
# Code blocks work inside tabs
print("hello")
```

<!-- tabs:end -->
```

- The comment delimiters `<!-- tabs:start -->` and `<!-- tabs:end -->` mark the tab group.
- Each `#### **Tab Title**` heading starts a new tab.
- Any block-level content (text, code, lists, images) is valid inside a tab.

## Images with Captions

Use HTML `<figure>` and `<figcaption>` tags for images that need captions.

```markdown
<figure>
  <img src="../assets/example.png" alt="Description of the image">
  <figcaption>Caption text displayed below the image.</figcaption>
</figure>
```

Standard Markdown image syntax (`![alt](path)`) works for images without captions.

## Internal Links

**Linking to another page** (path relative to the project root):

```markdown
[Page Title](folder/page.md)
```

**Linking to a section on another page:**

```markdown
[Section Title](folder/page.md#section-heading)
```

**Linking to a section on the current page:**

```markdown
[Section Title](#section-heading)
```

Anchor slugs are derived from heading text: lowercase, spaces replaced with hyphens, punctuation removed.

## LaTeX math

The [docsify-latex](https://scruel.github.io/docsify-latex/#/) plugin provides math rendering via mathjax 3.

**Block math:**

```markdown
$$
E = mc^2
$$
```

**Inline math:**

```markdown
$ F = ma $
```