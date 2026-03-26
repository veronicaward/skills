---
name: powerbi-dataviz
description: Create data visualizations grounded in the Microsoft Power BI design language. Use this skill when the user asks to build charts, dashboards, data visualizations, KPI cards, reports, or any analytical UI — especially when they mention Power BI, business intelligence, data reporting, or Microsoft Fabric. Also apply when building React/web equivalents of BI visuals that should follow enterprise data visualization standards.
version: 1.0.0
---

# Power BI Data Visualization Design Language

This skill applies Microsoft Power BI's data visualization design language when creating charts, dashboards, and analytical interfaces. Power BI's design system is purpose-built for clarity in data-dense environments: it prioritizes legibility, accessibility, and communicating insight over decoration.

## Core Design Philosophy

Power BI's visual language is built on four principles:

- **Clarity** — Every element earns its place. Non-data ink is minimized; insight is immediate.
- **Consistency** — Shared tokens (colors, fonts, spacing) across every visual on a page.
- **Accessibility** — WCAG AA compliance built in; color is never the sole communicator.
- **Hierarchy** — Size, color, and position guide the eye from headline KPI to supporting detail.

## Color System

### Data Colors (default palette)
Used sequentially for categorical series. Never use raw hex — derive meaning from position in the sequence.

```
1. #118DFF  — Primary Blue       (first/most important series)
2. #12239E  — Deep Navy
3. #E66C37  — Orange
4. #6B007B  — Deep Purple
5. #E044A7  — Magenta
6. #744EC2  — Violet
7. #D9B300  — Amber
8. #D64550  — Crimson
```

**Rule**: Use a maximum of 5–6 data colors per visual. Beyond that, the chart is too complex — split it.

### Semantic / Status Colors
Used in KPI indicators, conditional formatting, waterfall charts, and gauge visuals:

| Role | Token Name | Value | Use |
|---|---|---|---|
| Positive / On Target | `good` | `#1AAB40` | Green — met goal, positive delta |
| Neutral / Warning | `neutral` | `#D9B300` | Amber — approaching threshold |
| Negative / Alert | `bad` | `#D64554` | Red — missed target, critical |

**Critical rule**: Always pair color with a secondary indicator (icon, label, or pattern). Never use color alone.

### Structural / UI Colors
These define the visual chrome — backgrounds, text, borders, gridlines:

| Role | Token | Light Value |
|---|---|---|
| Primary text, titles, axis labels | `firstLevelElements` | `#252423` |
| Secondary text, legends, subtitles | `secondLevelElements` | `#605E5C` |
| Gridlines, disabled states | `thirdLevelElements` | `#F3F2F1` |
| Dimmed labels, placeholders | `fourthLevelElements` | `#B3B0AD` |
| Canvas / page background | `background` | `#FFFFFF` |
| Card/table grid outlines | `secondaryBackground` | `#C8C6C4` |
| Table accent bar | `tableAccent` | `#118DFF` |

### Gradient / Conditional Formatting
For heatmaps, conditional color scales, and null handling:

| Role | Value |
|---|---|
| `maximum` | `#118DFF` |
| `center` | `#D9B300` |
| `minimum` | `#DEEFFF` |
| `null` | `#FF7F48` |

See `references/color-and-themes.md` for the full JSON theme structure.

## Typography

**Font stack**: `"Segoe UI", "DIN", -apple-system, sans-serif`
- **Segoe UI**: Body text, labels, legends, table values
- **DIN**: Titles, callout numbers (KPI card values)

### Text Class Hierarchy

| Class | Font | Size | Color | Use |
|---|---|---|---|---|
| `callout` | DIN | 45pt | `#252423` | KPI card primary value |
| `largeTitle` | DIN | 14pt | `#252423` | Visual titles |
| `title` | DIN | 12pt | `#252423` | Axis titles, category labels |
| `header` | Segoe UI Semibold | 12pt | `#252423` | Slicer headers, section labels |
| `label` | Segoe UI | 10pt | `#252423` | Data labels, table values |
| `boldLabel` | Segoe UI Bold | 10pt | `#252423` | Totals, grand totals |
| `lightLabel` | Segoe UI | 10pt | `#605E5C` | Legends, button labels |
| `smallLabel` | Segoe UI | 9pt | `#252423` | Reference lines, dense axes |
| `smallLightLabel` | Segoe UI | 9pt | `#605E5C` | Value axis ticks |

**Recommended size scale for web/React equivalents**:
- Report title: 24–32px
- Section header: 18–24px
- Visual title: 14–16px
- Body / labels: 10–14px
- Legends / small labels: 9–12px

## Chart Type Selection

Choose the right visual **before** styling. The best Power BI visual is the one that answers the question with the fewest cognitive steps.

See `references/chart-selection.md` for the complete decision guide.

**Quick reference:**

| Question type | Best visual |
|---|---|
| How does X rank vs others? | Horizontal bar chart |
| How did X change over time? | Line chart |
| What is X as a share of total? | Donut (≤5 categories) or stacked bar |
| How do X and Y relate? | Scatter / bubble chart |
| What is the current value of X? | KPI card |
| How far is X from target? | Gauge or bullet chart |
| What drives X? | Waterfall chart |
| How does X break down across two dimensions? | Matrix table |

## Layout & Composition

### Page Layout
- Follow **F-pattern reading order**: top-left KPIs → top-right supporting metrics → bottom detail charts
- Primary insight (the single most important takeaway) gets the largest, highest-contrast treatment
- Slicers always in the same position across pages (top or left rail)
- Max **5–7 visuals per page**; beyond that, split the page or redesign the question

### Visual Sizing
- KPI cards: small, uniform grid (e.g., 4 across, equal width)
- Primary chart: largest element, takes ~50% of canvas
- Secondary charts: ~25% each
- Leave breathing room — whitespace is data visualization's silence

### Gridlines
- Use **minimal gridlines**: horizontal only for column/bar charts, none for cards/KPIs
- Gridline color: `thirdLevelElements` (`#F3F2F1`) — subtle, not dominant
- Remove all chart borders and background fill from individual visuals; let the canvas be the container

### Data Labels
- Add labels only when the exact value is required to understand the insight
- Apply the **squint test**: squint at your visual — your eyes should go to the data, not the labels
- Never overlap labels with series
- Use `smallLightLabel` style (9pt, `#605E5C`) to keep labels subordinate to data

## Accessibility Requirements

See `references/accessibility.md` for the full checklist.

**Non-negotiable minimums:**
- **4.5:1 contrast ratio** for all text against its background (WCAG AA)
- **3:1 contrast ratio** for large text (18pt+) and non-text UI elements
- Every visual that conveys meaning needs descriptive **alt text** (max 250 chars; write the insight, not "bar chart showing…")
- Multi-series charts must use **distinct marker shapes** in addition to color
- Never use red + green as the only way to show bad vs good — add an icon or label
- Set **logical tab order**: title → filters/slicers → primary KPIs → supporting charts

**Color-blind safe combinations** (avoid these pairings):
Green + Red, Green + Brown, Blue + Purple, Blue + Grey, Green + Grey, Light green + Yellow

**Use Power BI's built-in accessible themes** as your starting point:
`Color Blind Safe`, `Accessible City Park`, `Accessible Tidal`, `Accessible Neutral`

## KPI Cards

The most used component in Power BI dashboards. Design rules:

- **One number per card** — the metric value in `callout` style (DIN 45pt)
- **Category label** below in `largeLightLabel` (12pt, `#605E5C`)
- **Delta indicator**: colored chevron/arrow + percentage. Use `good`/`bad`/`neutral` colors + an icon
- **Sparkline** (optional): small trend line, `secondLevelElements` color, no axes
- **No borders** on cards themselves — whitespace creates separation
- For 4+ KPIs, use a matrix visual (more performant than stacked individual cards)

## Slicers & Filters

- Consistent position and style across all report pages
- Title in `header` class (Segoe UI Semibold 12pt)
- Button slicers preferred over dropdown for ≤8 options (faster scanning)
- Single slicer should control all related visuals on the page
- Slicer styling: no border, background `thirdLevelElements` on hover

## Data Tables & Matrix Visuals

- Header row: `secondLevelElements` color (`#605E5C`), `header` font class
- Data rows: `firstLevelElements` (`#252423`), `label` font class, alternating row shading using `thirdLevelElements`
- Totals / Grand Totals: `boldLabel` (Segoe UI Bold)
- Table accent (left border bar on selected row): `tableAccent` (`#118DFF`)
- Column padding: 8–12px horizontal, 6–8px vertical

## Power BI JSON Theme

When generating or modifying a Power BI JSON theme file, use this structure. See `references/color-and-themes.md` for the complete schema.

```json
{
  "name": "Custom Theme",
  "$schema": "https://powerbi.com/product/schema#reportTheme",
  "dataColors": ["#118DFF","#12239E","#E66C37","#6B007B","#E044A7","#744EC2","#D9B300","#D64550"],
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
    "callout": { "fontSize": 45, "fontFace": "DIN", "color": "#252423" },
    "title": { "fontSize": 12, "fontFace": "DIN", "color": "#252423" },
    "header": { "fontSize": 12, "fontFace": "Segoe UI Semibold", "color": "#252423" },
    "label": { "fontSize": 10, "fontFace": "Segoe UI", "color": "#252423" }
  }
}
```

## Implementing in React / Web

When building Power BI-style visuals in React:

**Libraries that align with Power BI's design language:**
- `@fluentui/react-components` — for the surrounding UI chrome (cards, filters, layout)
- `recharts` or `victory` — for charts (style with Power BI color tokens)
- `@microsoft/fast-components` — for low-level components
- `@nivo/bar`, `@nivo/line` etc. — highly configurable, maps well to PBI defaults

**CSS token mapping** (set these as CSS custom properties):
```css
:root {
  --pbi-color-1: #118DFF;
  --pbi-color-2: #12239E;
  --pbi-color-3: #E66C37;
  --pbi-color-4: #6B007B;
  --pbi-color-5: #E044A7;
  --pbi-color-6: #744EC2;
  --pbi-color-7: #D9B300;
  --pbi-color-8: #D64550;

  --pbi-good: #1AAB40;
  --pbi-neutral: #D9B300;
  --pbi-bad: #D64554;

  --pbi-text-primary: #252423;
  --pbi-text-secondary: #605E5C;
  --pbi-bg-canvas: #FFFFFF;
  --pbi-bg-subtle: #F3F2F1;
  --pbi-border: #C8C6C4;
  --pbi-accent: #118DFF;

  --pbi-font-body: "Segoe UI", -apple-system, sans-serif;
  --pbi-font-display: "DIN", "Segoe UI", sans-serif;
}
```

## What NOT to Do

- Do not use decorative gradients or drop shadows on charts
- Do not use 3D chart effects — they distort data perception
- Do not use pie charts with more than 5 slices
- Do not rely on color alone to convey positive/negative/neutral
- Do not use more than 6 colors in a single visual
- Do not skip axis labels or visual titles to save space — use abbreviated labels instead
- Do not auto-play animations or add looping motion to dashboards
- Do not remove gridlines entirely from quantitative charts (minimal is OK; zero is not)
- Do not use font sizes below 9pt in any data label
