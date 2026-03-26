# Power BI Chart Type Selection Guide

Choosing the right visual is the most important design decision. The wrong chart type obscures insight; the right one makes it obvious.

## The Core Question Framework

Before choosing a chart, answer: **What relationship am I showing?**

| Relationship | Chart Family |
|---|---|
| Ranking / comparison across categories | Bar / Column |
| Change over time | Line / Area |
| Part of a whole | Donut / Stacked Bar / Treemap |
| Correlation / distribution | Scatter / Bubble / Histogram |
| Single metric performance | KPI Card / Gauge |
| Contribution to change | Waterfall |
| Multi-dimensional breakdown | Matrix / Table |
| Geographic distribution | Map / Filled Map |
| Hierarchical composition | Treemap / Sunburst |

---

## Chart Types in Detail

### Bar & Column Charts

**Use when**: Comparing discrete categories, showing ranked values, displaying survey results.

**Rules:**
- **Horizontal bar**: Use when category labels are long or there are 6+ categories. Easier to read left-to-right.
- **Vertical column**: Use for time periods (months, quarters) or when categories are short (≤6).
- Sort bars by value (descending) unless the order has meaning (e.g., chronological, ordinal)
- 5–10 categories optimal. Beyond 15: use a table instead.
- No 3D. No gap width > 50%.
- Cluster for 2–3 series max; stack for showing composition.

**Color guidance**: Single-series bars use `--pbi-color-1` (#118DFF). Multi-series uses sequential palette positions. Highlight one bar with `--pbi-color-1`; mute the rest with `thirdLevelElements`.

---

### Line Charts

**Use when**: Showing trends over time, continuous data, multiple series across the same time axis.

**Rules:**
- Minimum 5 time points to justify a line (otherwise use a bar)
- Maximum 4–5 lines before the chart becomes unreadable
- Always use **distinct marker shapes** per series (for accessibility, not just color)
- Start Y-axis at zero unless the variation is the story and the range is justified
- Smooth curves are allowed but can hide data volatility — prefer straight segments for precision
- Area charts (filled line): use only for 1–2 series. Stacked area for part-of-whole over time.

**Color guidance**: Each line gets a unique position in the data color sequence. Use `secondLevelElements` (`#605E5C`) for reference/target lines.

---

### Scatter & Bubble Charts

**Use when**: Showing the relationship (correlation) between two continuous variables. Bubble adds a third dimension via dot size.

**Rules:**
- Label only the most important/outlier data points — not all
- Add a trend line to make the correlation explicit
- Bubble size should encode a meaningful, not decorative, value
- Avoid over-plotting: if > 200 data points, use density or hexbin instead
- Ensure bubble sizes scale by area, not radius

---

### Donut & Pie Charts

**Use when**: Showing one metric as a proportion of a meaningful total (e.g., market share, budget allocation).

**Rules:**
- **Hard limit: 5 slices maximum.** Merge smaller segments into "Other."
- If slices are close in size (within ~10% of each other), use a bar chart instead — humans cannot accurately judge angles
- Donut preferred over pie: center label shows total or primary metric
- Avoid exploded slices and 3D effects entirely
- Never use for more than one time period — shows composition, not change

---

### KPI Cards

**Use when**: Displaying a single headline metric with optional comparison to target or prior period.

**Structure:**
```
[Primary Value]          ← callout (DIN 45pt, #252423)
[Delta + Icon]           ← good/bad/neutral color + arrow icon
[Category Label]         ← largeLightLabel (12pt, #605E5C)
[Sparkline] (optional)   ← secondLevelElements color, no axes
```

**Rules:**
- One metric per card. Multiple metrics = multiple cards.
- Delta must include both direction (arrow) and magnitude (%, absolute, or both)
- Always show the comparison period in the label ("vs Prior Year", "vs Target")
- Align all KPI cards on a consistent grid (equal width, equal height)

---

### Gauge & Bullet Charts

**Use when**: Showing progress toward a single target (completion %, quota attainment, SLA).

**Gauge (arc)**:
- Three color zones for visual range: `bad` (red), `neutral` (amber), `good` (green)
- Target needle/line clearly distinct
- Use only when the range boundaries are meaningful — not arbitrary

**Bullet chart** (preferred for dashboard density):
- Shows actual vs target vs qualitative range in a compact horizontal form
- More information-dense than gauge; better for 4+ metrics on one page

---

### Waterfall Charts

**Use when**: Showing how individual positive and negative components sum to a total (e.g., revenue bridge, cost breakdown, variance analysis).

**Rules:**
- Use `good` color for increases, `bad` for decreases, `neutral` for subtotals/totals
- Always label the total bar
- Sort sub-components by magnitude when order doesn't have inherent meaning
- Include a "total" column on both ends if comparing two periods

---

### Matrix & Table Visuals

**Use when**: Exact values matter, multiple dimensions must be compared, or users need to look up specific data points.

**Rules:**
- Table for flat data; matrix for hierarchical/pivot data
- Limit to 10–15 visible columns before horizontal scrolling is required
- Use conditional formatting (color scales, data bars, icons) to add visual scanning aid
- Bold grand totals; use `tableAccent` color for the row-level accent bar
- Alternating row shading: `background` (#FFFFFF) and `thirdLevelElements` (#F3F2F1)
- Freeze the header row for tables with > 10 rows

**Icon sets for conditional formatting:**
- Directional: ▲ ▼ → (trend indicators)
- Status: ✓ ✗ ! (pass/fail/warning)
- Shapes: ● ◆ ■ (for color-blind safe status)

---

### Maps

**Use when**: Geography is a meaningful variable in the data (not just because data has a location column).

**Rules:**
- Filled Map (choropleth): comparing metrics across fixed regions (countries, states). Use a single-hue sequential scale — avoid multi-hue divergent scales unless showing positive/negative.
- Bubble Map: for point-level data with size encoding a metric
- Never encode more than one variable in map color — it creates ambiguity
- Always include a legend with clear min/max values
- Check for data aggregation errors (duplicate city names in different countries)

---

### Treemap

**Use when**: Showing hierarchical part-of-whole where both the structure and relative sizes matter (e.g., product portfolio by revenue).

**Rules:**
- Works well for 2 levels of hierarchy
- Avoid for more than 20 leaf nodes — readability breaks down
- Color by category (not by value in a treemap — use a heatmap for that)
- Label boxes only if they have room for full text

---

## Anti-Patterns to Avoid

| Visual | Why to Avoid |
|---|---|
| 3D bar/column/pie | Distorts proportions; no 3D in any PBI report |
| Pie with > 5 slices | Angles are impossible to compare accurately |
| Dual-axis line charts | Misleading unless axes are clearly labeled and intentional |
| Radar/spider charts | Hard to read; prefer parallel bar for same comparison |
| Word clouds | No quantitative meaning; use bar chart of term frequency |
| Funnel as decoration | Use only for true sequential drop-off processes |

---

## The "Squint Test"

After building any visual, squint until you can't read labels. Ask:
1. Can you still identify which values are highest/lowest?
2. Does the visual communicate the insight without labels?
3. Does your eye land on the data, not the chrome?

If any answer is no, simplify.
