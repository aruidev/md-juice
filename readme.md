# md-juice

**A drop-in CSS theme for rendered Markdown HTML**.  
Works with any framework, any renderer, or plain HTML. Two layers of customization let you theme quickly or fine-tune elements. 

<table>
  <tr>
    <td><img alt="Captura de pantalla 2025-09-18 162047" src="https://github.com/user-attachments/assets/7a4a6bdf-eb28-411a-b657-ddb86a91f75d" alt="md-juice demo (light)" width=400 />

</td>
    <td><img alt="Captura de pantalla 2025-09-18 162102" src="https://github.com/user-attachments/assets/b2b7a6e1-fc14-4906-8e1f-7aece68d3e34" alt="md-juice demo (dark)" width=400 />

</td>
  </tr>
</table>

## Table of Contents

- [Why MD-Juice?](#why-md-juice)
- [Installation](#installation)
- [Basic Usage](#basic-usage)
- [Theming (CSS Variables)](#theming)
- [Transitions](#transitions)
- [Tailwind Compatibility](#tailwind-compatibility)
- [Syntax Highlighting](#syntax-highlighting)


## Why md-juice?

Quickly style Markdown HTML with **conflict-free, framework-agnostic CSS**. 

**Use cases:** Docs, blogs, wikis, notes apps, README previews, static sites  
**Key benefits:** Fast theming, framework-agnostic, conflict-free styling 

### Features: 
- Token-driven theming with two customization layers
- Built-in light/dark theme support
- Zero JavaScript dependency
- GitHub-like default styling 

## Getting Started

### Installation

To get started, install md-juice:  

```bash
npm install @aruidev/md-juice
```

### Basic setup

#### Import the Styles  
Import the md-juice CSS to your global styles by updating the global styles.css file. This ensures the styles are available application-wide without conflicts.

```css
@import '@aruidev/md-juice';
```

### Basic usage

#### Quick example  

These high-level tokens control the overall look and feel:

```css
.md-juice {
  --juice-color-bg: #fefefe;
  --juice-color-text: #2d2a3e;
}
```

### Dark Mode Support  
Add dark mode variants in the same CSS file:  

```css
.md-juice[data-theme="dark"] {
  --juice-color-bg: #1a1625;
  --juice-color-text: #e4e2f0;
}
```  

## Theming

### Layer 1 – Fast tokens (`--juice-*`)

These high-level tokens control the overall look and feel.  
Set these to theme quickly.

| Token | Light default | Dark default | Role |
|-------|---------------|--------------|------|
| `--juice-color-bg` | `#ffffff` | `#0d1117` | Base background |
| `--juice-color-bg-alt` | `#f6f8fa` | `#010409` | Secondary surface (tables, panels) |
| `--juice-color-text` | `#1f2328` | `#c9d1d9` | Primary text |
| `--juice-color-text-secondary` | `#59636e` | `#8b949e` | Muted text |
| `--juice-color-border` | `#d1d9e0` | `rgba(110,118,129,0.40)` | Borders / rules |
| `--juice-color-interactive` | `#0969da` | `#58a6ff` | Links & accent base |
| `--juice-color-accent` | `var(--juice-color-interactive)` | `var(--juice-color-interactive)` | Focus / accent alias |
| `--juice-color-surface-code` | `var(--juice-color-bg-alt)` | `var(--juice-color-bg-alt)` | Code blocks & inline code |

#### Typography & layout primitives

| Token | Default | Maps to granular | Purpose |
|------|---------|------------------|---------|
| `--juice-font-family-base` | system stack | `--mdj-font-family` | Base text font stack |
| `--juice-font-family-monospace` | monospace stack | `--mdj-monospace` | Code / monospace font stack |
| `--juice-font-size-base` | `16px` | `--mdj-font-size` | Root font size (affects rem) |
| `--juice-line-height-base` | `1.5` | `--mdj-line-height` | Global line height |
| `--juice-radius-base` | `6px` | `--mdj-radius` | Shared corner radius (code, kbd, etc.) |
| `--juice-transition` | `150ms` | `--mdj-transition` | Theme transition duration |
| `--juice-transition-timing` | `cubic-bezier(0.4, 0, 0.2, 1)` | `--mdj-transition-timing` | Theme transition timing |

---

### Layer 2 – Granular tokens (`--mdj-*`)

Override **only** when a specific surface must differ from the fast mapping. 

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

### Transitions

By default md-juice uses Tailwind's default transition values (`150ms` + `cubic-bezier(0.4,0,0.2,1)`) so it visually blends into projects already using Tailwind.

If the rest of your app (e.g. layout, buttons) uses a different speed/easing and you notice a mismatch, just override after loading the stylesheet.

Set `--juice-transition` and `--juice-transition-timing` to match your app:

```css
.md-juice { --juice-transition: 200ms; }
.md-juice { --juice-transition-timing: ease-in-out; }
```

#### Disable transitions:

You can also disable transitions completely:

```css
.md-juice { --juice-transition: 0ms; }
```

### Tailwind compatibility

* Works side by side; md-juice only styles descendants of `.markdown-body` inside a `.md-juice` scope.
* Load order: include **after** Tailwind if you want md-juice to win on Markdown.

### Syntax highlighting

md-juice ships only minimal color tokens. Use a highlighter for full language scopes.  
You can still override `--mdj-syntax-*` for custom hues.

---
Enjoy rapid theming. PRs welcome.


