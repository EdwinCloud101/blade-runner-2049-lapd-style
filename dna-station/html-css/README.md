# LAPD Console UI Kit

A pure HTML + CSS component kit styled after the **Blade Runner 2049** LAPD
console — phosphor‑teal readouts, chromatic‑aberration glow, scanlines, film
grain, edge halation, and corner registration marks. No JavaScript, no build
step, no dependencies beyond two Google Fonts.

> Part of the `blade-runner-2049-lapd-style` project. Extracted and modularised
> from the original single‑file `basic-controls.html` reference.

---

## Layout

```
dna-station/html-css/
├── index.html              # full showcase of every control (+ theme switcher)
├── css/
│   ├── core.css            # framework: tokens, reset, atmosphere, themes, chrome
│   └── controls/           # one stylesheet per control
│        ├── textarea.css        textbox.css      checkbox.css
│        ├── radio.css           combobox.css     tabs.css
│        ├── datagrid.css        slider.css       image-display.css
│        ├── image-upload.css    button.css       toggle.css
│        ├── progress.css        spinner.css      badge.css
│        ├── tooltip.css         tree.css         color-picker.css
│        └── multiselect.css     autocomplete.css
└── examples/               # one minimal demo page per control
     └── textarea.html, textbox.html, … autocomplete.html
```

- **`css/core.css`** is the framework. Load it once. It defines the design
  tokens (CSS custom properties), the reset, the page atmosphere layers, the
  seven hue‑rotation themes, and the console chrome (masthead, section headers,
  footer bar, scrollbar, edge glow).
- **`css/controls/*.css`** — each file styles exactly one control and requires
  `core.css`. A few extend another control (noted in the file header):
  - `multiselect.css` requires `combobox.css`
- **`examples/*.html`** — a clean, standalone demo of a single control. Open any
  of them directly in a browser.

---

## Usage

Load the framework, then any control(s) you need:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@500;600&family=Share+Tech+Mono&display=swap" rel="stylesheet">

<link rel="stylesheet" href="css/core.css">
<link rel="stylesheet" href="css/controls/textbox.css">
```

The atmosphere layers are inert overlays. Drop them in once, at the end of
`<body>`, after your content:

```html
<div class="bg"></div>            <!-- behind everything; place first -->
<main class="console"> … </main>  <!-- your UI -->

<div class="mottle"></div>
<div class="scanlines"></div>
<div class="grain"></div>
<div class="vignette"></div>
<div class="edge-glow"><i></i><i></i></div>
```

Each control's required markup is documented in a comment at the top of its
stylesheet. The matching `examples/` page shows it in context.

---

## Controls

| # | Control | Stylesheet | Notes |
|---|---------|-----------|-------|
| 01 | Textarea | `textarea.css` | |
| 02 | Textbox | `textbox.css` | |
| 03 | Checkbox | `checkbox.css` | |
| 04 | Radio button | `radio.css` | |
| 05 | Combobox | `combobox.css` | CSS‑only (`<details>` + radios) |
| 06 | Tab control | `tabs.css` | CSS‑only (radios) |
| 07 | Datagrid | `datagrid.css` | |
| 08 | Slider | `slider.css` | |
| 09 | Image display | `image-display.css` | framed well + corner ticks |
| 10 | Image upload | `image-upload.css` | dashed drop zone |
| 11–12 | Button (text / ghost / icon) | `button.css` | |
| 13 | Toggle switch | `toggle.css` | |
| 14 | Progress bar | `progress.css` | |
| 15 | Spinner | `spinner.css` | |
| 16 | Status badge | `badge.css` | |
| 17 | Tooltip | `tooltip.css` | CSS‑only (`data-tip`) |
| 18 | Tree view | `tree.css` | CSS‑only (nested `<details>`) |
| 19 | Color picker | `color-picker.css` | |
| 20 | Multi‑select | `multiselect.css` | extends `combobox.css` |
| 21 | Autocomplete | `autocomplete.css` | focus‑driven suggestions |

### A note on the CSS‑only controls

Combobox, tab control, multi‑select and autocomplete are driven purely by
radio/checkbox `:checked` state — no JavaScript. That requires a small block of
**per‑instance wiring** rules that map each option `id` to its selected display.
Those rules live at the bottom of the relevant stylesheet, clearly commented,
using the demo ids (`cb1…`, `tb1…`, `ms1…`, `ac1…`). To add another instance,
copy that block and renumber the ids. A future JS build can replace this wiring.

---

## Themes

`core.css` ships seven themes, switched by the `#th1…#th7` radios at body level
(see the theme combobox in `index.html`): **Phosphor Teal** (default), Teal
Blue, Teal Blue V2, Amber, Crimson, Violet, and **Zion Dashboard** (inverted
light mode). They work by hue‑rotating the three colored layers (`.bg`,
`.console`, `.edge-glow`).

---

## Roadmap

- [ ] Publish as an npm package (`@…/lapd-ui`) shipping the CSS.
- [ ] Optional JS layer to remove the per‑instance wiring for stateful controls.
- [ ] Design tokens exported as a standalone `tokens.css` / JSON.

## License

To be decided before public release.
