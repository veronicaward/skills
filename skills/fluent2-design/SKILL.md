---
name: fluent2-design
description: Apply Microsoft Fluent 2 design language when building UI components or applications. Use this skill when the user asks to build anything with "Fluent", "Fluent 2", "Microsoft design", "Teams-style", "Office-style", or "WinUI" aesthetics, or when creating components using @fluentui/react-components, @fluentui/web-components, or similar Fluent UI libraries.
version: 1.0.0
---

# Fluent 2 Design System Skill

This skill applies the Microsoft Fluent 2 design language when building web UI components and applications. Fluent 2 is Microsoft's cross-platform design system used in Teams, Outlook, Office, and Windows — built around clarity, accessibility, and natural interaction.

## Core Design Philosophy

Fluent 2 is grounded in four values:

- **Accessible** — WCAG AA (minimum 4.5:1 contrast for body text, 3:1 for large text/UI components), keyboard-navigable, screen-reader friendly
- **Coherent** — Consistent tokens across surfaces; one visual language regardless of platform
- **Delightful** — Purposeful motion, depth through elevation, smooth transitions
- **Adaptive** — Works across light/dark modes, high-contrast themes, and varying screen densities

## Design Token System

Use the Fluent 2 token hierarchy for all styling decisions:

```
Global tokens → Alias tokens → Component tokens
```

- **Global tokens**: Raw values (e.g., `colorPaletteBlueForeground1: #0F6CBD`)
- **Alias tokens**: Semantic roles (e.g., `colorBrandForeground1`, `colorNeutralBackground1`)
- **Component tokens**: Component-specific overrides built on alias tokens

**Never hardcode raw hex values.** Always use alias tokens for colors, spacing, and typography.

Reference `references/color-tokens.md` for the full alias token palette.
Reference `references/typography.md` for the full type ramp.
Reference `references/motion.md` for animation guidance.

## Color System

### Light Theme Background Layers (elevation order)
| Token | Use |
|---|---|
| `colorNeutralBackground1` | Page/canvas background |
| `colorNeutralBackground2` | Cards, panels |
| `colorNeutralBackground3` | Nested containers |
| `colorNeutralBackground4` | Input fill, subtle surfaces |
| `colorNeutralBackground6` | Hover states on neutral |

### Brand Colors
- Primary action: `colorBrandBackground` / `colorBrandForeground1`
- Hover: `colorBrandBackgroundHover`
- Pressed: `colorBrandBackgroundPressed`
- Communication Blue (`#0F6CBD`) is the default brand color for Microsoft 365

### Semantic/Status Colors
| State | Background Token | Foreground Token |
|---|---|---|
| Success | `colorStatusSuccessBackground1` | `colorStatusSuccessForeground1` |
| Warning | `colorStatusWarningBackground1` | `colorStatusWarningForeground1` |
| Error/Danger | `colorStatusDangerBackground1` | `colorStatusDangerForeground1` |
| Info | `colorStatusInfoBackground1` | `colorStatusInfoForeground1` |

## Typography

**Font stack:**
- Web/Windows: `"Segoe UI Variable", "Segoe UI", -apple-system, sans-serif`
- macOS: `"SF Pro Display", "SF Pro Text", -apple-system, sans-serif`
- Android: `"Roboto", sans-serif`

**Type ramp (web):**
| Token | Size | Line Height | Weight |
|---|---|---|---|
| `fontSizeBase100` / Caption2 | 10px | 14px | 400 |
| `fontSizeBase200` / Caption1 | 12px | 16px | 400/600 |
| `fontSizeBase300` / Body1 | 14px | 20px | 400/600/700 |
| `fontSizeBase400` / Body2 | 16px | 22px | 400/600 |
| `fontSizeBase500` / Subtitle2 | 20px | 28px | 600 |
| `fontSizeBase600` / Subtitle1 | 24px | 32px | 600 |
| `fontSizeHero700` / Title3 | 28px | 36px | 600 |
| `fontSizeHero800` / Title2 | 32px | 40px | 600 |
| `fontSizeHero900` / Title1 | 40px | 52px | 600 |
| `fontSizeHero1000` / LargeTitle | 68px | 92px | 600 |

Always use **sentence case**. Never uppercase body or UI text.

## Spacing & Layout

Fluent 2 uses a **4px base grid**:
| Token | Value |
|---|---|
| `spacingHorizontalXXS` | 2px |
| `spacingHorizontalXS` | 4px |
| `spacingHorizontalS` | 8px |
| `spacingHorizontalM` | 12px |
| `spacingHorizontalL` | 16px |
| `spacingHorizontalXL` | 20px |
| `spacingHorizontalXXL` | 24px |
| `spacingHorizontalXXXL` | 32px |

Vertical spacing tokens mirror the horizontal set (`spacingVertical*`).

## Border Radius

| Token | Value | Use |
|---|---|---|
| `borderRadiusNone` | 0px | Square elements |
| `borderRadiusSmall` | 2px | Compact/dense components |
| `borderRadiusMedium` | 4px | Default (buttons, inputs, cards) |
| `borderRadiusLarge` | 6px | Dialogs, panels |
| `borderRadiusXLarge` | 8px | Cards, overlays |
| `borderRadiusCircular` | 10000px | Avatars, badges, pills |

## Elevation & Shadow

Fluent 2 expresses depth with layered shadows, not flat borders alone.

| Token | CSS Shadow | Use |
|---|---|---|
| `shadow2` | `0 1px 2px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)` | Resting cards |
| `shadow4` | `0 2px 4px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)` | Hover cards |
| `shadow8` | `0 4px 8px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)` | Dropdowns, menus |
| `shadow16` | `0 8px 16px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)` | Flyouts, tooltips |
| `shadow28` | `0 14px 28px rgba(0,0,0,.24), 0 0 8px rgba(0,0,0,.2)` | Dialogs, modals |
| `shadow64` | `0 32px 64px rgba(0,0,0,.24), 0 0 8px rgba(0,0,0,.2)` | Full-screen panels |

## Motion & Animation

Reference `references/motion.md` for full easing curves and duration values.

### Duration Scale
| Token | Value | Use |
|---|---|---|
| `durationUltraFast` | 50ms | Micro-interactions (focus ring) |
| `durationFaster` | 100ms | Icon swaps, small state changes |
| `durationFast` | 150ms | Component state transitions |
| `durationNormal` | 200ms | Most transitions (default) |
| `durationGentle` | 250ms | Content appearing |
| `durationSlow` | 300ms | Page sections, drawers |
| `durationSlower` | 400ms | Complex orchestrated sequences |
| `durationUltraSlow` | 500ms | Full-page transitions |

### Easing
- **Ease Out** (`cubic-bezier(0, 0, 0, 1)`): Elements entering the screen
- **Ease In** (`cubic-bezier(1, 0, 1, 1)`): Elements leaving the screen
- **Ease In-Out** (`cubic-bezier(0.8, 0, 0.2, 1)`): Elements moving within the screen
- **Linear** (`linear`): Only for continuous rotation/looping

### Motion Principles
- **Functional first**: Every animation serves a purpose (orient, respond, feedback)
- **Enter with ease-out**: Decelerate into place
- **Exit with ease-in**: Accelerate out, don't linger
- **No decorative-only motion**: If removing the animation doesn't hurt UX, remove it
- **Respect `prefers-reduced-motion`**: Always provide a no-motion fallback

```css
@media (prefers-reduced-motion: reduce) {
  * { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
}
```

## Key Component Patterns

### Buttons
Three primary variants with three sizes:
- **Primary**: Filled brand color background, white text
- **Secondary/Outline**: Transparent background, brand border and text
- **Subtle**: No border/background, brand text only
- **Sizes**: Small (24px h), Medium (32px h, default), Large (40px h)

All buttons: `borderRadiusMedium`, `fontWeightSemibold`, `fontSizeBase300`

### Inputs / Text Fields
- Background: `colorNeutralBackground1` with `colorNeutralStroke1` border
- Focused: `colorBrandStroke1` bottom border (2px underline style by default)
- Error: `colorStatusDangerForeground1` label + `colorStatusDangerBorder1` stroke
- Always pair with a visible label (no placeholder-only patterns)

### Cards
- Background: `colorNeutralBackground1`
- Border: `1px solid colorNeutralStroke1` or elevation shadow (`shadow4`)
- Radius: `borderRadiusXLarge` (8px) for standalone cards
- Interactive cards get `shadow8` on hover

### Navigation
- Top-level nav uses `colorNeutralBackground3` or brand color surface
- Active item: `colorBrandBackground` indicator + `colorBrandForeground1`
- Inactive: `colorNeutralForeground1`

### Badges / Presence Indicators
- Always `borderRadiusCircular`
- Status colors: Available (green), Busy (red), Away (yellow), Offline (gray)

## Accessibility Requirements

- **Focus indicators**: Always visible, use `colorStrokeFocus2` (2px solid) — never remove `:focus-visible`
- **Touch targets**: Minimum 44×44px interactive area (WCAG 2.5.8)
- **Color + icon**: Never convey state through color alone — always add icon or text
- **ARIA**: Use proper roles (`button`, `dialog`, `menu`, `menuitem`, `tab`, etc.)
- **Keyboard**: All interactive elements reachable and operable via keyboard
- **Contrast**: 4.5:1 for body text, 3:1 for large text (18px+/14px bold+) and UI components

## Dark Mode

All alias tokens automatically invert for dark mode. When implementing dark mode:
- Use `colorNeutralBackground1` through `colorNeutralBackground6` — they adapt automatically
- Do NOT use fixed light/dark hex values; use tokens
- Test both themes before shipping
- Dark mode backgrounds go from `#1A1A1A` (base) to `#141414` (deep)

## Implementation with @fluentui/react-components

When using the React library:

```tsx
import { FluentProvider, webLightTheme, webDarkTheme } from '@fluentui/react-components';
import { Button, Input, Card, Text, Badge } from '@fluentui/react-components';

// Wrap app with provider
<FluentProvider theme={webLightTheme}>
  <App />
</FluentProvider>

// Use makeStyles for token-based styling
import { makeStyles, tokens } from '@fluentui/react-components';

const useStyles = makeStyles({
  card: {
    backgroundColor: tokens.colorNeutralBackground1,
    borderRadius: tokens.borderRadiusXLarge,
    padding: tokens.spacingHorizontalXL,
    boxShadow: tokens.shadow4,
  },
});
```

## What NOT to Do

- Do not hardcode `#0078D4` or any other hex value — use tokens
- Do not use `border-radius: 50%` — use `tokens.borderRadiusCircular`
- Do not use `font-family: Arial, Helvetica` — use the Segoe UI stack
- Do not remove focus outlines for aesthetics
- Do not use color as the only way to communicate state
- Do not create animations longer than 500ms for typical UI transitions
- Do not use uppercase text in body copy or buttons
- Do not rely on `box-shadow` alone for interactive affordance — combine with color change
