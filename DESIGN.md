---
name: AAHQ Foundation
description: Editorial, high-clarity design system for product, docs, and marketing surfaces in this repository.
colors:
  ink: "#171717"
  text: "#2E2A26"
  muted: "#6B625C"
  accent: "#C65A3D"
  accentSoft: "#F3D7CD"
  line: "#D8D0C8"
  surface: "#F7F3EE"
  background: "#FFFDF9"
  success: "#2F6B4F"
  warning: "#A66A1F"
  danger: "#A64232"
typography:
  h1:
    fontFamily: "Fraunces"
    fontSize: "52px"
    fontWeight: 600
    lineHeight: 1.02
    letterSpacing: "-0.03em"
  h2:
    fontFamily: "Fraunces"
    fontSize: "36px"
    fontWeight: 600
    lineHeight: 1.08
    letterSpacing: "-0.02em"
  h3:
    fontFamily: "Fraunces"
    fontSize: "24px"
    fontWeight: 600
    lineHeight: 1.15
    letterSpacing: "-0.01em"
  body:
    fontFamily: "Instrument Sans"
    fontSize: "16px"
    fontWeight: 400
    lineHeight: 1.55
    letterSpacing: "0em"
  small:
    fontFamily: "Instrument Sans"
    fontSize: "14px"
    fontWeight: 400
    lineHeight: 1.45
    letterSpacing: "0em"
spacing:
  xs: "4px"
  sm: "8px"
  md: "16px"
  lg: "24px"
  xl: "40px"
  xxl: "64px"
rounded:
  sm: "6px"
  md: "12px"
  lg: "20px"
elevation:
  soft: "0 8px 24px rgba(23, 23, 23, 0.08)"
  strong: "0 18px 50px rgba(23, 23, 23, 0.12)"
components:
  button-primary:
    backgroundColor: "{colors.ink}"
    textColor: "#FFFFFF"
    rounded: "{rounded.md}"
    padding: "12px 20px"
  button-secondary:
    backgroundColor: "transparent"
    textColor: "{colors.ink}"
    rounded: "{rounded.md}"
    padding: "12px 20px"
    borderColor: "{colors.line}"
  card:
    backgroundColor: "#FFFFFF"
    textColor: "{colors.text}"
    rounded: "{rounded.lg}"
    borderColor: "{colors.line}"
    padding: "{spacing.lg}"
    shadow: "{elevation.soft}"
---

## Context and Goals
Design intent: deliver a clean, editorial interface system that maximizes clarity and usability through whitespace, legible typography, and restrained color usage.

- Must prioritize clarity and accessibility over novelty.
- Must keep guidance implementation-ready for engineers and designers.
- Should feel authored and warm, not generic or template-like.
- Should maintain consistency across product UI, docs, and marketing surfaces.

## Implementation Stack
- Base implementation stack: `Astro 5/6` + `Tailwind CSS 4`.
- Component and theme system: `daisyUI` (core components + theme configuration).
- Default implementation target should use this stack unless a product-local override defines another frontend setup.

## Design Tokens and Foundations

### Visual Direction
- Minimal, clean, and high-clarity UI with generous whitespace.
- Hierarchy should come from typography, spacing, and contrast before decorative effects.
- Accent should behave as a signal for important actions and states, not as broad decoration.

### Color Foundation
- Must use semantic tokens over raw color literals in component implementations.
- Must keep page canvas on `background` and low-emphasis sections on `surface`.
- Must use `ink` for primary emphasis and `text` for core copy.
- Should reserve `muted` for support text and metadata.
- Must validate contrast for text and controls against WCAG 2.2 AA.

### Typography Foundation
- Must use Fraunces for headings and Instrument Sans for interface/body text.
- Must preserve readable rhythm: body text at `16px` with `1.55` line-height by default.
- Should keep headlines concise and avoid oversized paragraph-like headings.
- Must avoid fallback to generic system stacks on new screens unless legacy constraints require it.

### Spacing and Layout Foundation
- Must follow an 8px rhythm using the defined spacing tokens.
- Must separate sections with spacing before introducing borders or color blocks.
- Should keep content width readability-first rather than edge-to-edge.
- Must reduce columns before collapsing spacing on mobile.

### Shape and Elevation Foundation
- Must use `rounded.md` for standard containers and `rounded.lg` for feature cards.
- Must keep depth subtle; prefer border + spacing over heavy shadows.
- Should avoid stacked shadow recipes and glassmorphism.

## Component-Level Rules

### Global Component Expectations
- Every interactive component must define these states when relevant: default, hover, focus-visible, active, disabled, loading, error.
- Every component with user input must define empty, loading, and error handling.
- Every state rule must be token-anchored (color token, spacing token, or typography token), not adjective-only.
- Keyboard, pointer, and touch behavior must be explicitly defined.

### Buttons (`button-primary`, `button-secondary`)
- Anatomy: container, label, optional leading/trailing icon.
- Primary button:
  - Must use `colors.ink` background and white text.
  - Must preserve minimum touch target of 44px height.
  - Hover should increase contrast subtly (no glow).
  - Focus-visible must show a high-contrast ring independent of hover style.
- Secondary button:
  - Must use transparent surface with visible border token.
  - Must not visually resemble disabled state in default appearance.
- Disabled:
  - Must reduce emphasis while preserving readable label contrast.
  - Must remove pointer affordance but remain semantically disabled.
- Loading:
  - Must keep width stable and expose progress affordance.
  - Must prevent duplicate submissions.

### Cards (`card`)
- Anatomy: container, heading region, content region, optional action row.
- Must use white card surface, token border, and soft elevation.
- Must maintain consistent internal padding using spacing tokens.
- Should support long content without clipping controls or metadata.
- Responsive:
  - Must preserve readable padding on mobile.
  - Must avoid dense multi-column card grids below mobile breakpoint.

### Form Controls (input, textarea, select)
- Anatomy: label, control, helper text, validation message.
- Must always render a visible label (not placeholder-only labeling).
- Must keep vertical alignment stable across empty, filled, error, and disabled states.
- Focus-visible must be clearly distinct from hover and default.
- Error:
  - Must include text guidance, not color-only indication.
  - Must map to `danger` token for border/support message with compliant contrast.
- Long labels and overflow:
  - Should wrap labels instead of clipping.
  - Must prevent helper/error overlap with adjacent fields.

## daisyUI Mapping
- When implementing this design system with daisyUI, prefer a custom daisyUI theme instead of mixing raw Tailwind palette classes across the UI.
- Recommended semantic mapping:
  - `base-100`: `#FFFDF9`
  - `base-200`: `#F7F3EE`
  - `base-300`: `#D8D0C8`
  - `base-content`: `#2E2A26`
  - `primary`: `#171717`
  - `primary-content`: `#FFFFFF`
  - `secondary`: `#C65A3D`
  - `secondary-content`: `#FFFDF9`
  - `accent`: `#F3D7CD`
  - `accent-content`: `#2E2A26`
  - `neutral`: `#6B625C`
  - `neutral-content`: `#FFFDF9`
  - `success`: `#2F6B4F`
  - `warning`: `#A66A1F`
  - `error`: `#A64232`
- Prefer daisyUI component primitives for common UI: `btn`, `card`, `input`, `textarea`, `select`, `badge`, `alert`, `navbar`, `menu`, `modal`, `drawer`.
- Keep component styling mostly in daisyUI classes plus Tailwind utilities for spacing, layout, and small one-off adjustments.
- Avoid reintroducing a separate handcrafted button or form system unless the product needs a component daisyUI does not cover.

## daisyUI Theme Example
```css
@import "tailwindcss";
@plugin "daisyui";
@plugin "daisyui/theme" {
  name: "aahq";
  default: true;
  prefersdark: false;
  color-scheme: light;

  --color-base-100: #FFFDF9;
  --color-base-200: #F7F3EE;
  --color-base-300: #D8D0C8;
  --color-base-content: #2E2A26;

  --color-primary: #171717;
  --color-primary-content: #FFFFFF;
  --color-secondary: #C65A3D;
  --color-secondary-content: #FFFDF9;
  --color-accent: #F3D7CD;
  --color-accent-content: #2E2A26;
  --color-neutral: #6B625C;
  --color-neutral-content: #FFFDF9;

  --color-success: #2F6B4F;
  --color-success-content: #FFFDF9;
  --color-warning: #A66A1F;
  --color-warning-content: #FFFDF9;
  --color-error: #A64232;
  --color-error-content: #FFFDF9;

  --radius-field: 0.75rem;
  --radius-box: 1.25rem;
  --border: 1px;
  --depth: 0;
  --noise: 0;
}
```

## Accessibility Requirements and Testable Acceptance Criteria
- Must meet WCAG 2.2 AA contrast and interaction requirements.
- Must support keyboard-only use for all interactive controls.
- Must provide visible focus indicators on every focusable element.
- Must use semantic HTML before ARIA enhancements.
- Must support reduced motion preferences for non-essential animation.
- Must keep touch targets at 44px by 44px minimum where interaction is expected.

Acceptance criteria for implementation review:
- All controls are reachable in logical tab order and operable with Enter/Space when applicable.
- Focus ring is visible at 200% zoom and not hidden by overflow clipping.
- Error states include text and are announced where required for assistive technology.
- Motion-heavy transitions are disabled or simplified under reduced motion.

## Content and Tone Standards
- Voice should be clear and friendly.
- Labels must be specific and action-oriented.
- Helper and error copy should explain what happened and what to do next.

Examples:
- Prefer: "Continue to checkout"
- Avoid: "Submit"
- Prefer: "Email is required"
- Avoid: "Invalid"

## Anti-Patterns and Prohibited Implementations
- Do not use low-contrast text as a stylistic choice.
- Do not use decorative motion that does not communicate state or feedback.
- Do not introduce inconsistent spacing rhythm between adjacent sections.
- Do not rely on placeholder-only labels in forms.
- Do not introduce one-off local color choices outside semantic tokens.

## Migration Notes for Existing UI
- When existing views use raw Tailwind colors, migrate first to semantic daisyUI tokens (`primary`, `base-*`, `error`, etc.).
- When existing components lack explicit states, add focus-visible and error behavior before visual restyling.
- When old layouts are dense, migrate by increasing spacing rhythm first, then simplifying decoration.

## QA Checklist
- Context: design intent is stated and reflected in implementation.
- Tokens: colors, spacing, radius, and typography come from system tokens.
- Components: default/hover/focus-visible/active/disabled/loading/error states are implemented as applicable.
- Responsiveness: mobile layout reduces columns before reducing readability-critical spacing.
- Accessibility: keyboard flow, focus visibility, contrast, reduced-motion behavior, and touch targets are verified.
- Content: labels and validation copy are clear, specific, and non-ambiguous.
- Consistency: no one-off visual patterns conflict with system rules.