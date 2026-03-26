# Fluent 2 Motion Reference

## Motion Principles

1. **Functional** — Animation communicates meaning. It orients users, confirms actions, and provides feedback. Never animate purely for decoration.
2. **Natural** — Motion follows the physics of the real world: things decelerate when they arrive, accelerate when they leave.
3. **Consistent** — Shared duration and easing tokens create a unified feel across all components.
4. **Accessible** — Always respect `prefers-reduced-motion`. Provide instant transitions as the fallback.

## Duration Tokens

| Token | Value | Best For |
|---|---|---|
| `durationUltraFast` | 50ms | Focus rings, micro feedback |
| `durationFaster` | 100ms | Icon state swaps, badge updates |
| `durationFast` | 150ms | Button press, toggle, checkbox |
| `durationNormal` | 200ms | **Default** — most hover/focus/state transitions |
| `durationGentle` | 250ms | Content revealing, tooltip appear |
| `durationSlow` | 300ms | Drawer open, panel slide-in |
| `durationSlower` | 400ms | Complex orchestrated sequences |
| `durationUltraSlow` | 500ms | Full-page transitions, hero reveals |

**Rule**: Default to `durationNormal` (200ms). Only increase for larger spatial movement.

## Easing Curves

| Token | CSS Value | Use |
|---|---|---|
| `curveEasyEase` | `cubic-bezier(0.33, 0, 0.67, 1)` | Elements moving within viewport |
| `curveEasyEaseMax` | `cubic-bezier(0.8, 0, 0.2, 1)` | Emphasis / dramatic repositioning |
| `curveAccelerate` (Ease In) | `cubic-bezier(0.9, 0.1, 1, 0.2)` | Elements **exiting** the screen |
| `curveDecelerate` (Ease Out) | `cubic-bezier(0.1, 0.9, 0.2, 1)` | Elements **entering** the screen |
| `curveLinear` | `linear` | Looping animations, progress spinners only |

### Which curve to use?

```
Element appearing (entering):  → curveDecelerate (ease out) — arrive naturally, decelerate into place
Element disappearing (exiting): → curveAccelerate (ease in)  — accelerate away, don't linger
Element moving within UI:       → curveEasyEase              — smooth repositioning
Continuous spinner/rotation:    → curveLinear                — constant speed for loops
```

## Transition Types

### Enter / Exit
Used for elements appearing/disappearing (toasts, tooltips, dialogs, dropdowns):

```css
/* Enter */
.entering {
  animation: fadeSlideIn 200ms cubic-bezier(0.1, 0.9, 0.2, 1) forwards;
}
@keyframes fadeSlideIn {
  from { opacity: 0; transform: translateY(-4px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* Exit */
.exiting {
  animation: fadeSlideOut 150ms cubic-bezier(0.9, 0.1, 1, 0.2) forwards;
}
@keyframes fadeSlideOut {
  from { opacity: 1; transform: translateY(0); }
  to   { opacity: 0; transform: translateY(-4px); }
}
```

### Elevation (Drag / Lift)
For drag-and-drop, card picks, and interactive lift states:

```css
.card {
  transition: box-shadow 200ms cubic-bezier(0.33, 0, 0.67, 1),
              transform 200ms cubic-bezier(0.33, 0, 0.67, 1);
}
.card:hover {
  box-shadow: 0 4px 8px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12); /* shadow8 */
  transform: translateY(-2px);
}
.card.dragging {
  box-shadow: 0 14px 28px rgba(0,0,0,.24), 0 0 8px rgba(0,0,0,.2); /* shadow28 */
  transform: translateY(-4px) scale(1.02);
}
```

### Page / Top-Level Transitions
Use a quick cross-fade for SPA page navigation:

```css
.page-enter { animation: pageFadeIn 300ms cubic-bezier(0.1, 0.9, 0.2, 1); }
.page-exit  { animation: pageFadeOut 200ms cubic-bezier(0.9, 0.1, 1, 0.2); }

@keyframes pageFadeIn  { from { opacity: 0; } to { opacity: 1; } }
@keyframes pageFadeOut { from { opacity: 1; } to { opacity: 0; } }
```

### Container Transform
For expanding a small element (card) into a larger surface (panel/modal):

```css
.panel-opening {
  animation: containerExpand 300ms cubic-bezier(0.1, 0.9, 0.2, 1);
  transform-origin: top left;
}
@keyframes containerExpand {
  from { transform: scale(0.95); opacity: 0; }
  to   { transform: scale(1);    opacity: 1; }
}
```

## Staggering / Choreography

When animating lists of items, stagger entry by 30–50ms per item (max ~5 items; beyond that, animate the container):

```css
.list-item:nth-child(1) { animation-delay: 0ms; }
.list-item:nth-child(2) { animation-delay: 30ms; }
.list-item:nth-child(3) { animation-delay: 60ms; }
.list-item:nth-child(4) { animation-delay: 90ms; }
.list-item:nth-child(5) { animation-delay: 120ms; }
```

## Reduced Motion

Always include this — no exceptions:

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

In React with Motion library or Framer Motion:

```tsx
const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

const transition = prefersReducedMotion
  ? { duration: 0 }
  : { duration: 0.2, ease: [0.1, 0.9, 0.2, 1] };
```

## Common Anti-Patterns to Avoid

- **Bounce/spring physics** on business UI — use Fluent curves instead
- **Duration > 500ms** for any single UI transition
- **Animating layout properties** (`width`, `height`, `top`, `left`) — use `transform` and `opacity` only
- **Blocking user interaction** during animation — transitions should never lock UI
- **Looping decorative animations** that aren't paused on `prefers-reduced-motion`
- **Staggering more than 5–6 items** individually — animate the container instead
