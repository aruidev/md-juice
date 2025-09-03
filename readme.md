# md-juice

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/c1032150-7b72-4159-8645-a978114b9346" alt="Light Mode" width="420"></td>
    <td><img src="https://github.com/user-attachments/assets/76df95ad-ca7b-4a30-a14b-85f48f517552" alt="Dark Mode" width="420"></td>
  </tr>
</table>

**md-juice** is a modern, fully customizable CSS theme for Markdown.

It works with any standard Markdown library or parser, including **ngx-markdown**, **marked.js**, and **markdown-it**, making it compatible with any framework like **Angular**, **React**, **Vue**, **Svelte**, **Astro**, or even **without a framework**.

Based on [github-markdown-css](https://github.com/sindresorhus/github-markdown-css), **md-juice is a fully tokenized alternative** designed for quick and easy customization using CSS variables.

## Features

- Fully customizable colors and styles using CSS variables.
- Supports both light and dark mode.
- Styled lists, tables, code blocks, links, footnotes, and more, all with a clean, modern look.
- Easy to integrate into any project, regardless of the framework.

## Tailwind Compatibility

md-juice works seamlessly alongside **Tailwind CSS**. Since it uses standard CSS with variables (design tokens), you can combine md-juice with Tailwind utility classes without conflicts.  

**Tips for integration:**

- **Load order matters:** Include md-juice **after Tailwind** if you want its styles to take precedence on Markdown elements.  
- **Class coexistence:** md-juice styles are applied to selectors like `.markdown-body h1` or `.markdown-body a`, which will not interfere with Tailwind classes. You can use Tailwind for layout, spacing, or responsive utilities while md-juice handles Markdown styling.  
- **Custom colors:** You can map md-juice CSS variables to Tailwind theme colors (`theme.extend.colors`) for a fully consistent design system across your project.  

This makes md-juice flexible for projects that already rely on Tailwind, allowing you to maintain a consistent look while keeping Markdown styling clean and modern.


## Installation

Install via npm:

```bash
npm install @arui/md-juice
```

Or add the stylesheet directly

## Usage

Wrap your rendered markdown with the `.markdown-body` class (or apply equivalent selector):

```html
<article class="markdown-body">
  <!-- rendered markdown -->
</article>
```

## Quick start

- Include `md-juice.css` in your page or build.
- Override tokens via `:root` or on a container element to theme.
- Toggle dark mode by setting `data-theme-dark` on a parent (for example `<body data-theme-dark>`).

Example overrides:

```html
<link rel="stylesheet" href="/path/to/md-juice.css">
<style>
  :root {
    --mdj-font-size: 18px;
    --mdj-link-color: #ff6b6b;
  }
</style>
```


## Design tokens (CSS custom properties)

The following tokens are exposed by `md-juice.css`. Override any of them in `:root` or on a wrapper element.

### Colors & surfaces

| Token | Default | Description |
|---|---:|---|
| `--mdj-background-color` | `#ffffff` | Page / surface background |
| `--mdj-background-secondary-color` | `#f6f8fa` | Alternate surface (table stripes, row backgrounds) |
| `--mdj-text-primary-color` | `#1f2328` | Main content text color |
| `--mdj-text-secondary-color` | `#59636e` | Muted / secondary text |
| `--mdj-border-color` | `#d1d9e0` | Borders, rules and separators |
| `--mdj-link-color` | `#0969da` | Links and primary accents |
| `--mdj-accent-color` | `#0969da` | Accent color used for focus outlines, highlights |
| `--mdj-code-bg` | `#f6f8fa` | Code block and inline-code background |
| `--mdj-kbd-bg` | `#f6f8fa` | `<kbd>` background |
| `--mdj-kbd-border` | `rgba(209,217,224,0.8)` | `<kbd>` border color |
| `--mdj-mark-bg` | `#fff8c5` | `<mark>` (highlight) background |

### Typography & sizing

| Token | Default | Description |
|---|---:|---|
| `--mdj-font-family` | `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif` | UI font stack |
| `--mdj-monospace` | `ui-monospace, SFMono-Regular, Menlo, Monaco, "Roboto Mono", "Courier New", monospace` | Monospace stack for code |
| `--mdj-font-size` | `16px` | Base font size |
| `--mdj-line-height` | `1.5` | Base line-height |
| `--mdj-radius` | `6px` | Border radius used for pre/code and `<kbd>` |
| `--mdj-hr-height` | `1px` | Horizontal rule thickness |

### Interaction

| Token | Default | Description |
|---|---:|---|
| `--mdj-focus-outline` | `2px solid var(--mdj-accent-color)` | Focus outline style |
| `--mdj-muted-bg` | `transparent` | Reserved muted background token |

### Dark theme

Set `[data-theme-dark]` on a parent element (for example `<body data-theme-dark>`) to switch to the provided dark token set.

Key dark defaults included in `md-juice.css`:

| Token | Dark default |
|---|---:|
| `--mdj-background-color` | `#0d1117` |
| `--mdj-background-secondary-color` | `#010409` |
| `--mdj-text-primary-color` | `#c9d1d9` |
| `--mdj-text-secondary-color` | `#8b949e` |
| `--mdj-link-color` | `#58a6ff` |
| `--mdj-code-bg` | `#0f1720` |

## How to customize

- Global changes: override tokens in `:root`.

  ```css
  :root {
    --mdj-background-color: #fffaf0;
    --mdj-link-color: #7c3aed;
  }
  ```

- Per-scope: set tokens on a wrapper element that contains `.markdown-body`.

  ```html
  <div class="docs" style="--mdj-font-size:17px; --mdj-accent-color:#e11d48;">
    <article class="markdown-body">…</article>
  </div>
  ```

- Dark mode toggle (JS):

  ```js
  document.documentElement.setAttribute('data-theme-dark', '');
  document.documentElement.removeAttribute('data-theme-dark');
  ```

## Syntax highlighting (tip)

`md-juice` includes minimal token classes for syntax colors, but it does not provide a full syntax highlighter. For proper code highlighting in fenced code blocks use a highlighter such as Prism.js or Highlight.js.

- [Prism.js](https://prismjs.com/)
- [Highlight.js](https://highlightjs.org/)


