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

## Overview
AAHQ Foundation is clean, editorial, and deliberate. The visual language should feel authored rather than generic: warm paper backgrounds, dark ink text, restrained use of terracotta accent, and generous spacing. Avoid the default AI tendency toward glossy gradients, dense dashboards, or interchangeable SaaS layouts.

## Brand & Style
- Use contrast and typography as the primary source of hierarchy.
- Prefer calm, tactile surfaces over high-saturation UI chrome.
- Accent color is a signal, not a wash. Use it for emphasis, active states, and key highlights only.

## Colors
- Backgrounds should stay warm and bright: `background` for page canvas, `surface` for bands and low-emphasis panels.
- Use `ink` for high-importance actions and dark anchors.
- Use `muted` only for support text, metadata, and dividers paired with whitespace.
- Validate contrast before using `accent` on light backgrounds for body-size text.

## Typography
- Headlines use Fraunces for character and memorability.
- Interface and body text use Instrument Sans for clarity.
- Do not mix in default system stacks when implementing new screens unless the existing product already does.
- Keep headline copy tight. Long paragraphs should rely on body styles, not oversized text.

## Layout & Spacing
- Favor vertical rhythm and obvious section breaks.
- Standard content width should feel readable first, not maximal.
- Use whitespace to separate ideas before adding borders or tinted containers.
- On mobile, preserve hierarchy by reducing columns before reducing spacing too aggressively.

## Elevation & Depth
- Depth should be subtle and mostly reserved for cards, floating panels, and callouts.
- Avoid stacked shadow systems and glassmorphism.
- Borders plus spacing are preferred over heavy shadow for most UI.

## Shapes
- Corners are rounded but not playful.
- Default containers use `rounded.md`; larger feature cards can use `rounded.lg`.
- Avoid pill-heavy interfaces unless a component specifically needs that treatment.

## Components
- Primary buttons are dark and confident; keep them visually simple.
- Secondary buttons should read as calm alternatives, not disabled controls.
- Cards should feel structured and breathable, with enough padding for mixed content.
- Forms should prioritize legibility and stable alignment over decorative styling.

## Do's and Don'ts
- Do create layouts that feel intentional, spacious, and typographically led.
- Do keep motion minimal and meaningful.
- Do reuse these tokens consistently across app UI, docs, and landing pages.
- Do not default to purple gradients, neon shadows, or generic startup visuals.
- Do not overload a screen with multiple accent colors.
- Do not trade clarity for novelty.