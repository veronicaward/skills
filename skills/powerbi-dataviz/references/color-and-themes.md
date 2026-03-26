# Power BI Color System & Theme Reference

## Default Data Color Sequence

Power BI assigns data colors sequentially. The first series always gets position 1.

```
Position 1  →  #118DFF   Primary Blue      (default first series, most prominent)
Position 2  →  #12239E   Deep Navy
Position 3  →  #E66C37   Orange
Position 4  →  #6B007B   Deep Purple
Position 5  →  #E044A7   Magenta
Position 6  →  #744EC2   Violet
Position 7  →  #D9B300   Amber
Position 8  →  #D64550   Crimson
```

When more than 8 series exist, Power BI auto-generates additional colors by shifting saturation/brightness. **This is a sign the visual needs to be simplified.**

---

## Semantic Status Colors

| Role | Hex | Usage |
|---|---|---|
| Good / Positive | `#1AAB40` | Target met, positive delta, upward trend |
| Neutral / Warning | `#D9B300` | Approaching threshold, moderate risk |
| Bad / Negative | `#D64554` | Target missed, critical alert, downward trend |

**Pair with icons or labels** — never let these colors stand alone as the only signal.

---

## Structural UI Colors

| Token Name | Hex | Purpose |
|---|---|---|
| `firstLevelElements` | `#252423` | Primary text, data labels, axis labels, trend lines |
| `secondLevelElements` | `#605E5C` | Secondary text, legends, subtitles, reference lines |
| `thirdLevelElements` | `#F3F2F1` | Gridlines, disabled state backgrounds, alternating rows |
| `fourthLevelElements` | `#B3B0AD` | Dimmed labels, placeholder text |
| `background` | `#FFFFFF` | Canvas and page background |
| `secondaryBackground` | `#C8C6C4` | Table grid outlines, separator lines, default shapes |
| `tableAccent` | `#118DFF` | Row accent bar in tables/matrices |

---

## Conditional Formatting Color Scale

Used for heatmaps, data bar fills, and divergent scales:

| Role | Hex |
|---|---|
| Maximum (highest value) | `#118DFF` |
| Center / Mid | `#D9B300` |
| Minimum (lowest value) | `#DEEFFF` |
| Null / Missing data | `#FF7F48` |

For negative-to-positive divergent scales: use `bad` → white → `good` (`#D64554` → `#FFFFFF` → `#1AAB40`).

---

## Color Accessibility Rules

**Never pair these combinations** (problematic for color-blind users):
- Red + Green (affects ~8% of males)
- Green + Brown
- Blue + Purple
- Blue + Grey
- Green + Grey
- Light Green + Yellow

**Always add a secondary cue**: icon, pattern, or text label alongside any color-coded status.

**Contrast minimums** (WCAG AA):
- Normal text: **4.5:1** against background
- Large text (18pt+ or 14pt bold): **3:1**
- Non-text UI elements (borders, icons): **3:1**

---

## Power BI JSON Theme Schema

### Minimal valid theme
```json
{
  "name": "My Theme"
}
```
Only `name` is required. All other properties are optional and inherit defaults.

### Full theme template
```json
{
  "name": "Custom Power BI Theme",
  "$schema": "https://powerbi.com/product/schema#reportTheme",

  "dataColors": [
    "#118DFF",
    "#12239E",
    "#E66C37",
    "#6B007B",
    "#E044A7",
    "#744EC2",
    "#D9B300",
    "#D64550"
  ],

  "good": "#1AAB40",
  "neutral": "#D9B300",
  "bad": "#D64554",

  "maximum": "#118DFF",
  "center": "#D9B300",
  "minimum": "#DEEFFF",
  "null": "#FF7F48",

  "firstLevelElements": "#252423",
  "secondLevelElements": "#605E5C",
  "thirdLevelElements": "#F3F2F1",
  "fourthLevelElements": "#B3B0AD",
  "background": "#FFFFFF",
  "secondaryBackground": "#C8C6C4",
  "tableAccent": "#118DFF",

  "textClasses": {
    "callout": {
      "fontSize": 45,
      "fontFace": "DIN",
      "color": "#252423"
    },
    "title": {
      "fontSize": 12,
      "fontFace": "DIN",
      "color": "#252423"
    },
    "header": {
      "fontSize": 12,
      "fontFace": "Segoe UI Semibold",
      "color": "#252423"
    },
    "label": {
      "fontSize": 10,
      "fontFace": "Segoe UI",
      "color": "#252423"
    }
  },

  "visualStyles": {
    "*": {
      "*": {
        "background": [{ "show": false }],
        "border": [{ "show": false }],
        "title": [{
          "fontColor": { "solid": { "color": "#252423" } },
          "fontSize": 14,
          "fontFamily": "DIN"
        }]
      }
    },
    "columnChart": {
      "*": {
        "categoryAxis": [{ "gridlineStyle": "none" }],
        "valueAxis": [{ "gridlineColor": { "solid": { "color": "#F3F2F1" } } }]
      }
    },
    "lineChart": {
      "*": {
        "valueAxis": [{ "gridlineColor": { "solid": { "color": "#F3F2F1" } } }]
      }
    }
  }
}
```

### Data type encoding in JSON

| Type | Format | Example |
|---|---|---|
| Color | `{ "solid": { "color": "#hex" } }` | `{ "solid": { "color": "#118DFF" } }` |
| Boolean | unquoted | `true` / `false` |
| String | double-quoted | `"Segoe UI"` |
| Number | unquoted | `45` |
| DateTime | ISO with single-quotes | `'datetime'2024-01-01T00:00:00.000Z''` |

---

## Built-in Accessible Themes

Use these as base themes when accessibility is a priority:

| Theme Name | Notes |
|---|---|
| Color Blind Safe | Palette tested for deuteranopia/protanopia |
| Accessible City Park | Green-based, high contrast |
| Accessible Tidal | Blue-teal palette, accessible |
| Accessible Neutral | Greyscale + one accent |
| Accessible Orchid | Purple-based palette |
| High Contrast | Windows high contrast compatible |

---

## Customizing for Brand Colors

When replacing the default blue with a brand primary color, follow these rules:

1. **Set position 1** in `dataColors` to your primary brand color
2. **Set `tableAccent`** to the same primary brand color
3. **Keep `maximum`** (gradient high end) aligned with your brand primary
4. **Verify contrast**: brand color text on white must pass 4.5:1
5. **Test `good`/`neutral`/`bad`**: these should remain semantically clear — avoid making your brand color the same hue as `good` (green) or `bad` (red)

### Brand color replacement example
```json
{
  "name": "Contoso Brand Theme",
  "dataColors": ["#0078D4", "#004578", "#F7630C", "#6B007B", "#E044A7", "#744EC2", "#D9B300", "#D64550"],
  "tableAccent": "#0078D4",
  "maximum": "#0078D4",
  "good": "#1AAB40",
  "neutral": "#D9B300",
  "bad": "#D64554"
}
```

---

## Dark Mode / Dark Background Reports

Power BI supports dark-background reports. When designing for dark:

| Token | Dark Value |
|---|---|
| `background` | `#1B1A19` |
| `firstLevelElements` | `#F3F2F1` |
| `secondLevelElements` | `#C8C6C4` |
| `thirdLevelElements` | `#323130` |
| `fourthLevelElements` | `#484644` |
| `secondaryBackground` | `#3B3A39` |

Data colors may need saturation/brightness adjustments for dark backgrounds — test each palette color at 4.5:1 contrast against your dark background.
