# Fluent 2 Typography Reference

## Font Stacks by Platform

| Platform | Primary Font Stack |
|---|---|
| Web / Windows | `"Segoe UI Variable", "Segoe UI", -apple-system, BlinkMacSystemFont, sans-serif` |
| macOS | `-apple-system, "SF Pro Display", "SF Pro Text", sans-serif` |
| iOS | `-apple-system, "SF Pro Text", sans-serif` |
| Android | `"Roboto", sans-serif` |

For web apps targeting multiple OS: use `"Segoe UI Variable", "Segoe UI", -apple-system, sans-serif` — the system font will cascade naturally on macOS/iOS.

## Type Ramp — Web (Segoe UI)

| Role | Token Size | px | Line Height | Weight | Weight Token |
|---|---|---|---|---|---|
| Caption 2 | `fontSizeBase100` | 10px | 14px | Regular | `fontWeightRegular` (400) |
| Caption 1 | `fontSizeBase200` | 12px | 16px | Regular / Semibold | `fontWeightRegular` / `fontWeightSemibold` |
| Caption 1 Strong | `fontSizeBase200` | 12px | 16px | Semibold | `fontWeightSemibold` (600) |
| Body 1 | `fontSizeBase300` | 14px | 20px | Regular | `fontWeightRegular` (400) |
| Body 1 Strong | `fontSizeBase300` | 14px | 20px | Semibold | `fontWeightSemibold` (600) |
| Body 2 | `fontSizeBase400` | 16px | 22px | Regular | `fontWeightRegular` (400) |
| Subtitle 2 | `fontSizeBase500` | 20px | 28px | Semibold | `fontWeightSemibold` (600) |
| Subtitle 1 | `fontSizeBase600` | 24px | 32px | Semibold | `fontWeightSemibold` (600) |
| Title 3 | `fontSizeHero700` | 28px | 36px | Semibold | `fontWeightSemibold` (600) |
| Title 2 | `fontSizeHero800` | 32px | 40px | Semibold | `fontWeightSemibold` (600) |
| Title 1 | `fontSizeHero900` | 40px | 52px | Semibold | `fontWeightSemibold` (600) |
| Large Title | `fontSizeHero1000` | 68px | 92px | Semibold | `fontWeightSemibold` (600) |
| Display | *(hero)* | 68px+ | Auto | Bold | `fontWeightBold` (700) |

## Font Weight Tokens

| Token | Value |
|---|---|
| `fontWeightRegular` | 400 |
| `fontWeightMedium` | 500 |
| `fontWeightSemibold` | 600 |
| `fontWeightBold` | 700 |

## Font Size Tokens (Raw)

| Token | Value |
|---|---|
| `fontSizeBase100` | 10px |
| `fontSizeBase200` | 12px |
| `fontSizeBase300` | 14px |
| `fontSizeBase400` | 16px |
| `fontSizeBase500` | 20px |
| `fontSizeBase600` | 24px |
| `fontSizeHero700` | 28px |
| `fontSizeHero800` | 32px |
| `fontSizeHero900` | 40px |
| `fontSizeHero1000` | 68px |

## Line Height Tokens

| Token | Value |
|---|---|
| `lineHeightBase100` | 14px |
| `lineHeightBase200` | 16px |
| `lineHeightBase300` | 20px |
| `lineHeightBase400` | 22px |
| `lineHeightBase500` | 28px |
| `lineHeightBase600` | 32px |
| `lineHeightHero700` | 36px |
| `lineHeightHero800` | 40px |
| `lineHeightHero900` | 52px |
| `lineHeightHero1000` | 92px |

## Typography Usage Guidelines

### Case
- Always **sentence case** for UI text, labels, buttons, headings
- Never ALL CAPS for body or button text (exception: very short decorative labels in specific design contexts, use sparingly)
- Avoid Title Case for body text; reserve for proper nouns and product names

### Hierarchy
- One Title or Large Title per page/screen maximum
- Use Subtitle for section headers within a page
- Body 1 (14px) is the default for all body content
- Caption 1 (12px) for metadata, timestamps, secondary labels
- Caption 2 (10px) only for extreme density; use sparingly

### Color + Typography
- Primary text: `colorNeutralForeground1`
- Secondary/supporting text: `colorNeutralForeground2`
- Placeholder: `colorNeutralForeground4`
- Disabled: `colorNeutralForegroundDisabled`
- Links: `colorBrandForeground1` + underline on hover

### Accessibility
- Body text must meet **4.5:1** contrast against its background
- Large text (18px+ normal weight, 14px+ bold) must meet **3:1** contrast
- Do not set `font-size` below 10px
- Avoid justified text alignment (causes uneven word spacing for readers with dyslexia)

## React Usage

```tsx
import { Text, makeStyles, tokens } from '@fluentui/react-components';

// Use the Text component with preset variants
<Text size={300} weight="semibold">Section header</Text>
<Text size={200} style={{ color: tokens.colorNeutralForeground2 }}>Supporting detail</Text>

// Or with makeStyles
const useStyles = makeStyles({
  heading: {
    fontSize: tokens.fontSizeHero800,
    lineHeight: tokens.lineHeightHero800,
    fontWeight: tokens.fontWeightSemibold,
    color: tokens.colorNeutralForeground1,
  },
});
```
