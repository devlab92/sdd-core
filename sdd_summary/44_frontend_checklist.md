# 44_frontend_checklist.md — Pre-Delivery UI Checklist

> A generic gate to run before calling any UI work "done". Applies when
> `design_system: true` in [`sdd.config.md`](../sdd.config.md). Extend per project.
> Pairs with [`DESIGN.md.template`](../DESIGN.md.template).

---

## Structure & reuse
- [ ] Used an **existing component** or extended the library — no needless inline UI (Layer 3).
- [ ] Every interactive element has a **semantic `id`** and **BEM class**.
- [ ] No hard-coded colors/spacing — only **semantic design tokens**.

## Accessibility (WCAG AA)
- [ ] Text contrast ≥ **4.5:1** (≥ **3:1** for large text and UI components).
- [ ] Fully **keyboard navigable**; visible focus states.
- [ ] Images have `alt`; icons have accessible labels.
- [ ] Forms have associated `<label>`s and clear error messaging.

## Responsive & state
- [ ] Works mobile-first (test at 360px) up through desktop.
- [ ] Handles **loading**, **empty**, and **error** states — not just the happy path.
- [ ] No layout shift / content jump on load.

## Theming
- [ ] Correct in **light and dark** themes.
- [ ] Respects `prefers-color-scheme` and any in-app theme toggle.

## Polish
- [ ] Consistent spacing scale; aligned to the grid.
- [ ] Transitions are subtle and consistent.
- [ ] No console errors or warnings.
