---
name: daisyui
description: Skill for building UI with daisyUI on top of Tailwind CSS. Use when the user asks for daisyUI, semantic Tailwind components, themeable UI, or fast component-driven frontend implementation in React, Vue, Svelte, Astro, or plain HTML.
license: Refer to upstream docs and package license
metadata:
  authors: "Adapted locally from daisyUI docs, llms.txt, and skills.sh reference"
  version: "0.1.0"
  upstream:
    - "https://daisyui.com/llms.txt"
    - "https://daisyui.com/docs/install/"
    - "https://skills.sh/bobmatnyc/claude-mpm-skills/daisyui"
---

# DaisyUI Usage Guide

Use this skill when implementing UI with daisyUI components rather than hand-rolling every surface with raw Tailwind utilities.

## Summary

daisyUI is a component layer for Tailwind that provides semantic classes such as `btn`, `card`, `modal`, `drawer`, `alert`, and `input`. It works best when you want consistent UI primitives, theme tokens, and fast delivery without inventing a custom component system for every screen.

For this repository, prefer daisyUI when:

- the project already uses Tailwind CSS
- the user explicitly asks for daisyUI
- you need semantic UI primitives quickly
- a local design system can be mapped into a daisyUI theme

Do not assume daisyUI is installed. Verify the nearest manifest and CSS entrypoint first.

## Agent Rules

- Prefer daisyUI component classes plus Tailwind layout utilities over custom CSS.
- Prefer semantic tokens such as `primary`, `secondary`, `accent`, `base-100`, `base-200`, and `base-content` over raw palette classes for reusable UI.
- Use Tailwind utilities for spacing, layout, visibility, breakpoints, and small one-off adjustments.
- Keep implementations mobile-first and responsive.
- If the existing app already has a stronger local design system or component library, preserve that instead of forcing daisyUI.
- For daisyUI 5 with Tailwind CSS 4, prefer CSS-based plugin setup instead of older `tailwind.config.js`-only instructions.

## Installation

### daisyUI 5 with Tailwind CSS 4

Install the package:

```bash
npm install -D daisyui@latest
```

In the main CSS entrypoint:

```css
@import "tailwindcss";
@plugin "daisyui";
```

If you need a custom theme:

```css
@import "tailwindcss";
@plugin "daisyui";
@plugin "daisyui/theme" {
  name: "app";
  default: true;
  prefersdark: false;
  color-scheme: light;

  --color-base-100: #ffffff;
  --color-base-200: #f7f7f7;
  --color-base-300: #ebebeb;
  --color-base-content: #171717;
  --color-primary: #171717;
  --color-primary-content: #ffffff;
  --color-secondary: #4f46e5;
  --color-secondary-content: #ffffff;
  --color-accent: #e0e7ff;
  --color-accent-content: #171717;
  --color-neutral: #4b5563;
  --color-neutral-content: #ffffff;
  --color-success: #15803d;
  --color-success-content: #ffffff;
  --color-warning: #a16207;
  --color-warning-content: #ffffff;
  --color-error: #b91c1c;
  --color-error-content: #ffffff;
  --radius-field: 0.75rem;
  --radius-box: 1rem;
  --border: 1px;
  --depth: 0;
  --noise: 0;
}
```

### Older Projects

If the app is still on an older Tailwind generation, inspect the project before applying configuration. Some codebases still use `tailwind.config.js` plugin registration. Match the local version instead of upgrading implicitly.

## Core Patterns

### Buttons

```html
<button class="btn">Default</button>
<button class="btn btn-primary">Primary</button>
<button class="btn btn-secondary">Secondary</button>
<button class="btn btn-outline btn-primary">Outline</button>
<button class="btn btn-ghost">Ghost</button>
```

### Card

```html
<div class="card bg-base-100 shadow-sm border border-base-300">
  <div class="card-body">
    <h2 class="card-title">Card title</h2>
    <p>Card content.</p>
    <div class="card-actions justify-end">
      <button class="btn btn-primary">Continue</button>
    </div>
  </div>
</div>
```

### Form Fields

```html
<fieldset class="fieldset w-full max-w-md">
  <legend class="fieldset-legend">Email</legend>
  <input type="email" class="input w-full" placeholder="name@company.com" />
  <p class="label">We only use this for account updates.</p>
</fieldset>
```

### Alert

```html
<div role="alert" class="alert alert-success">
  <span>Changes saved.</span>
</div>
```

### Modal

```html
<button onclick="settings_modal.showModal()" class="btn btn-primary">Open</button>

<dialog id="settings_modal" class="modal">
  <div class="modal-box">
    <h3 class="text-lg font-semibold">Settings</h3>
    <p class="py-4">Update your workspace preferences.</p>
    <div class="modal-action">
      <form method="dialog">
        <button class="btn">Close</button>
      </form>
    </div>
  </div>
</dialog>
```

### Drawer Layout

```html
<div class="drawer lg:drawer-open">
  <input id="app-drawer" type="checkbox" class="drawer-toggle" />
  <div class="drawer-content">
    <label for="app-drawer" class="btn drawer-button lg:hidden">Menu</label>
  </div>
  <div class="drawer-side">
    <label for="app-drawer" aria-label="close sidebar" class="drawer-overlay"></label>
    <ul class="menu bg-base-200 min-h-full w-72 p-4">
      <li><a>Overview</a></li>
      <li><a>Settings</a></li>
    </ul>
  </div>
</div>
```

## Theme Guidance

- Set theme via `data-theme` on the `html` element when you need theme switching.
- Prefer one product theme plus an optional dark theme, not a random grab bag of built-in themes.
- Map brand tokens into a custom theme instead of overriding random component styles ad hoc.
- Avoid raw text colors like `text-gray-800` on themed surfaces. Use semantic tokens such as `text-base-content`, `text-primary-content`, or `text-secondary-content`.

### Theme Generator

daisyUI provides a visual theme generator: https://daisyui.com/theme-generator/

Use it when you need to quickly create or refine a custom theme palette and then copy the generated CSS variables into a `@plugin "daisyui/theme"` block.

Practical workflow:

1. Start with a built-in theme close to your target mood.
2. Tune semantic tokens (`base-*`, `primary`, `secondary`, `accent`, `neutral`, `info`, `success`, `warning`, `error`).
3. Verify contrast for `*-content` tokens.
4. Export theme CSS and commit it in the app stylesheet.
5. Set `data-theme` to the exported theme name and validate key UI states.

Example:

```html
<html data-theme="app">
```

## Composition Rules

- Use daisyUI for component shape and state.
- Use Tailwind utilities for layout: `grid`, `flex`, `gap-*`, `px-*`, `py-*`, `max-w-*`, `hidden`, `md:*`, `lg:*`.
- Prefer responsive variants directly on the component when the size or placement must adapt, for example `btn-sm md:btn-md` or `modal-bottom sm:modal-middle`.
- Avoid long chains of utility classes that fight the default component behavior unless there is a clear reason.
- If a component does not exist in daisyUI, build it with Tailwind utilities instead of forcing an unrelated daisyUI primitive.

## Accessibility

- Use semantic HTML elements first: `button`, `dialog`, `label`, `fieldset`, `nav`, `ul`, `table`.
- Keep form labels explicit.
- For dialogs, prefer native `dialog` plus `showModal()` and a `form method="dialog"` close action.
- For tabs, menus, and dropdowns, preserve keyboard focusability and ARIA attributes when needed.
- Ensure status and feedback components remain readable under all enabled themes.

## Common Pitfalls

### Styles not appearing

- Verify `daisyui` is installed in the relevant package.
- Verify the CSS entrypoint includes `@plugin "daisyui";` for Tailwind 4 setups.
- Verify Tailwind is actually compiling the file where component classes are used.

### Theme not applying

- Check that `data-theme` is set on the intended root element.
- Check that the custom theme name matches the configured theme name exactly.
- Check that you are using semantic colors in components instead of hardcoded raw colors.

### Modal not opening

- Confirm the element is a native `dialog`.
- Confirm the open trigger calls `showModal()` on the dialog element.
- Confirm IDs are unique.

### Layout feels generic

- Map the product brand into theme tokens.
- Pair daisyUI components with stronger typography, spacing, and composition.
- Do not rely on default theme plus default spacing for every screen.

## Repository-Specific Guidance

For this repository, align daisyUI work with the root design instructions:

- warm light surfaces rather than cold default SaaS styling
- restrained accent usage
- typography-led hierarchy
- minimal shadow depth

If the local design system defines a specific theme, use that theme instead of daisyUI defaults.

## Validation Checklist

- daisyUI is actually installed in the touched app
- configuration style matches the local Tailwind version
- components use semantic tokens instead of arbitrary raw colors
- layout works on mobile and desktop
- dialog, drawer, menu, and form controls remain keyboard-usable
- custom CSS is minimal and justified

## Resources

- Official docs: https://daisyui.com/
- Component catalog: https://daisyui.com/components/
- Install guide: https://daisyui.com/docs/install/
- Config guide: https://daisyui.com/docs/config/
- llms.txt: https://daisyui.com/llms.txt
- Theme generator: https://daisyui.com/theme-generator/