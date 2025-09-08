# md-juice

<table>
  <tr>
    <td><img width="939" height="1031" alt="md-juice (light)" src="https://github.com/user-attachments/assets/af3ec429-9684-4b71-aebb-708bb8b2fdf4" width=400/>
</td>
    <td><img width="944" height="1038" alt="Captura de pantalla 2025-09-08 160931" src="https://github.com/user-attachments/assets/de6e91cd-69b5-403c-a46f-ca026276624b" width=400/>
</td>
  </tr>
</table>

**md-juice** is a tiny, token‑driven CSS theme for rendered Markdown. Drop it in, wrap output with a lightweight scope `.md-juice` + `.markdown-body`, override a few variables—done.

Framework agnostic — it can be used in any environment or setup. Compatible with popular Markdown renderers (ngx-markdown, marked, markdown-it, React Markdown) and works seamlessly within modern frameworks (React, Angular, Astro, plain HTML, etc.).

## Features

* Fast theming layer (`--juice-*`) – 8 tokens flip the whole look.
* Fine control layer (`--mdj-*`) – override only what you need.
* Light / dark via attribute or class (`[data-theme="dark"]` or `.juice-dark`).
* Optional system auto dark (prefers-color-scheme) fallback included.
* Clean GitHub‑like styles: headings, tables, code, alerts, footnotes, tasks.
* Zero JS required (JS only for toggling if you want a switch).

## Installation

```bash
npm install @aruidev/md-juice
```

## Basic usage

Recommended (scoped) HTML:

```html
<!-- Import via bundler (JS) or link tag (CDN/local) -->
<div class="md-juice">
  <article class="markdown-body">
    <!-- rendered markdown here -->
  </article>
</div>
```

Import options:
```js
// ESM (Vite, Next, Astro, etc.)
import '@aruidev/md-juice';
// or direct CSS entry if your bundler supports it
import '@aruidev/md-juice/md-juice.css';
```
CDN / manual link:
```html
<link rel="stylesheet" href="/node_modules/@aruidev/md-juice/md-juice.css">
```

Multiple independent instances (each can theme differently):
```html
<div class="md-juice">
  <article class="markdown-body"> ... </article>
</div>
<div class="md-juice" data-theme="dark">
  <article class="markdown-body"> ... </article>
</div>
```

Dark mode per container (no need to touch `<html>`):
```js
const scope = document.querySelector('.md-juice');
scope.setAttribute('data-theme','dark');   // force dark
scope.setAttribute('data-theme','light');  // force light
scope.removeAttribute('data-theme');       // fall back to prefers-color-scheme block
```

## Layer 1 – Fast tokens (`--juice-*`)

Set these to theme quickly. All granular tokens derive from them unless you override `--mdj-*` directly.

| Token | Light default | Dark default | Role |
|-------|---------------|--------------|------|
| `--juice-color-bg` | `#ffffff` | `#0d1117` | Base background |
| `--juice-color-bg-alt` | `#f6f8fa` | `#010409` | Secondary surface (tables, panels) |
| `--juice-color-text` | `#1f2328` | `#c9d1d9` | Primary text |
| `--juice-color-text-secondary` | `#59636e` | `#8b949e` | Muted text |
| `--juice-color-border` | `#d1d9e0` | `rgba(110,118,129,0.40)` | Borders / rules |
| `--juice-color-interactive` | `#0969da` | `#58a6ff` | Links & accent base |
| `--juice-color-accent` | =interactive | =interactive | Focus / accent alias |
| `--juice-color-surface-code` | `#f6f8fa` | `#0f1720` | Code blocks & inline code |

Example quick theme (all instances):

```css
/* After importing md-juice.css */
.md-juice { /* global override for all markdown scopes */
  --juice-color-bg: #ffffff;
  --juice-color-interactive: #4f46e5;
}
.md-juice[data-theme="dark"] {
  --juice-color-bg: #0d1117;
  --juice-color-interactive: #818cf8;
}
```

Instance‑only override:
```html
<div class="md-juice" style="--juice-color-bg:#fff7e6;--juice-color-interactive:#dc2626">
  <article class="markdown-body"> ... </article>
</div>
```

### Typography & layout primitives

These fast tokens drive base typography & spacing radii; granular `--mdj-*` counterparts reference them unless you override the granular ones directly.

| Token | Maps to granular | Purpose |
|-------|------------------|---------|
| `--juice-font-family-base` | `--mdj-font-family` | Base text font stack |
| `--juice-font-size-base` | `--mdj-font-size` | Root font size (affects rem) |
| `--juice-line-height-base` | `--mdj-line-height` | Global line height |
| `--juice-radius-base` | `--mdj-radius` | Shared corner radius (code, kbd, etc.) |
| `--juice-transition` | `--mdj-transition` | Theme transition duration |

Quick tweak example:

```css
.md-juice {
  --juice-font-family-base: system-ui, sans-serif;
  --juice-font-size-base: 15px; /* slightly denser */
  --juice-radius-base: 4px;
  --juice-transition: 150ms; /* Default Tailwind transitions duration */
}
```

## Layer 2 – Granular tokens (`--mdj-*`)

Override only when a specific surface must differ from the fast mapping.

| Token | Default (maps from fast layer) | Description |
|-------|--------------------------------|-------------|
| `--mdj-background-color` | `--juice-color-bg` | Page / main background |
| `--mdj-background-secondary-color` | `--juice-color-bg-alt` | Alt surface |
| `--mdj-text-primary-color` | `--juice-color-text` | Main text |
| `--mdj-text-secondary-color` | `--juice-color-text-secondary` | Muted text |
| `--mdj-border-color` | `--juice-color-border` | Borders & dividers |
| `--mdj-link-color` | `--juice-color-interactive` | Links |
| `--mdj-accent-color` | `--juice-color-accent` | Accent & focus |
| `--mdj-code-bg` | `--juice-color-surface-code` | Code block / inline background |
| `--mdj-kbd-bg` | `--juice-color-surface-code` | `<kbd>` background |
| `--mdj-kbd-border` | `--juice-color-border` | `<kbd>` border |
| `--mdj-mark-bg` | `--juice-color-bg-alt` | `<mark>` highlight |
| `--mdj-table-th-bg` | `--juice-color-bg-alt` | Table header |
| `--mdj-table-tr-bg` | `--juice-color-bg` | Table rows |
| `--mdj-font-family` | system stack | Base font |
| `--mdj-monospace` | monospace stack | Code font |
| `--mdj-font-size` | `16px` | Root font size |
| `--mdj-line-height` | `1.5` | Base line height |
| `--mdj-radius` | `6px` | Radius (pre/code/kbd) |
| `--mdj-hr-height` | `1px` | Rule thickness |
| `--mdj-focus-outline` | `2px solid var(--mdj-accent-color)` | Focus style |
| `--mdj-muted-bg` | `transparent` | Reserved token |
| `--mdj-transition` | `150ms` | Theme transition speed |
| `--mdj-syntax-*` | fixed colors | Minimal syntax hues |

## Dark mode

Two approaches:
* Explicit: `<html data-theme="dark">` or add `.juice-dark` to a wrapper.
* Auto (optional block in CSS): remove the attribute to let `prefers-color-scheme: dark` apply.

Granular overrides for dark should target the scoped container:
```css
.md-juice[data-theme="dark"] { --mdj-code-bg:#0f1422; }
```

## Transitions

By default md-juice uses Tailwind's default transition values (`150ms` + `cubic-bezier(0.4,0,0.2,1)`) so it visually blends into projects already using Tailwind. All color/background/border transitions inside `.markdown-body` inherit that.

If the rest of your app (e.g. layout, buttons) uses a different speed/easing and you notice a mismatch, just override after loading the stylesheet:

> If your app's global transitions (e.g. body, layout, buttons) use a different duration or easing than the rendered markdown, either set --juice-transition and --juice-transition-timing to match your app. 

```css
/* Unify duration with the rest of the app (all instances) */
.md-juice { --juice-transition: 200ms; }

/* Or change only easing globally (markdown inherits) */
.md-juice { --juice-transition-timing: ease-in-out; }
```

### Disable transitions:

> You can also disable transitions completely.

```css
.md-juice { --juice-transition: 0ms; }
```

## Alerts

Use TWO classes: base + variant.

```html
<blockquote class="markdown-alert markdown-alert-warning">
  <p class="markdown-alert-title">Warning</p>
  <p>Something notable.</p>
</blockquote>
```
Variants: `note`, `important`, `warning`, `tip`, `caution`.

## Footnotes

Renderer should wrap them:

```html
<div class="footnotes">
  <ol>
    <li id="fn1"><p>Small footnote text…</p></li>
  </ol>
</div>
```
Font size scales (0.75em). Add the wrapper if your generator omits it.

## Tailwind compatibility

* Works side by side; md-juice only styles descendants of `.markdown-body` inside a `.md-juice` scope.
* Load order: include **after** Tailwind if you want md-juice to win on Markdown semantics (or use cascade layers to control ordering).

## Syntax highlighting

md-juice ships only minimal color tokens (`.pl-*`). Use a highlighter for full language scopes:

* Prism.js
* Highlight.js

You can still override `--mdj-syntax-*` for custom hues.

## FAQ quick answers

| Need | Do this |
|------|---------|
| Faster theme | `.md-juice { --juice-color-* overrides }` |
| Precise tweak | `.md-juice { --mdj-code-bg:#faf7ff }` (or inline style on one instance) |
| Disable animation | `.md-juice { --mdj-transition:0ms }` |
| Custom code bg only | `.md-juice { --mdj-code-bg: #faf7ff }` |
| Dark toggle JS | `scope.setAttribute('data-theme','dark')` (where scope = `.md-juice`) |

---
Enjoy rapid theming. PRs welcome.


