# Power BI Accessibility Reference

Power BI reports must meet WCAG 2.1 AA standards. This reference covers every accessibility requirement for reports built in Power BI Desktop, Power BI Service, and equivalent web implementations.

## Contrast Requirements

| Element | Minimum Ratio | Standard |
|---|---|---|
| Body text / data labels | **4.5:1** | WCAG 2.1 AA |
| Large text (18pt+, or 14pt bold) | **3:1** | WCAG 2.1 AA |
| UI components (borders, icons, buttons) | **3:1** | WCAG 2.1 AA |
| Decorative elements only | No requirement | — |

**Test with**: Colour Contrast Analyser (TPGi), WebAIM Contrast Checker, or browser DevTools accessibility panel.

---

## Color Blindness

~8% of males and ~0.5% of females have color vision deficiency. Never let color be the sole indicator of meaning.

### Problematic color combinations to avoid:
- Red (#D64554) + Green (#1AAB40) — affects ~8% of males (deuteranopia)
- Green + Brown
- Blue + Purple
- Blue + Grey
- Green + Grey
- Light Green + Yellow

### Solutions:
1. **Add an icon** alongside colored status indicators: ✓ for good, ✗ for bad, ! for neutral
2. **Add a text label**: "On Track", "At Risk", "Off Track"
3. **Use distinct marker shapes** on line charts (●, ▲, ■, ◆ etc.)
4. **Use patterns or textures** in addition to color fills where the platform supports it
5. **Use the Color Blind Safe theme** as your base palette

---

## Alt Text for Visuals

Every visual that conveys information must have alt text.

**Power BI Desktop**: Format pane → General → Alt text

**Writing effective alt text:**
- Describe the **insight**, not the chart type
- ✅ Good: "Sales increased 23% YoY, driven primarily by Q4 growth in the North region"
- ❌ Bad: "Bar chart showing sales data by quarter"
- Maximum 250 characters
- Use conditional alt text (dynamic measures) for visuals that update with filter context

**Decorative visuals** (logo, background shape, divider line): set alt text to empty string to remove from screen reader tab order.

---

## Tab Order

Screen readers and keyboard users navigate by tab order. Set a logical reading sequence.

**Recommended order:**
1. Page title
2. Slicer / filter controls (top-to-bottom, left-to-right)
3. Primary KPI cards
4. Main chart(s)
5. Supporting/secondary charts
6. Navigation buttons

**In Power BI Desktop**: View tab → Tab Order panel → drag to reorder

**Remove from tab order**: Decorative shapes, background images, divider lines — set these to "hidden from tab order".

---

## Keyboard Navigation

All visuals must be fully operable by keyboard.

| Action | Keys |
|---|---|
| Move between visuals | Tab / Shift+Tab |
| Navigate data points within a visual | Arrow keys |
| Select a data point | Enter or Space |
| Open tooltip | hover or Ctrl+Shift+I (desktop) |
| Show data table (accessible view) | Alt+Shift+F11 |
| Display keyboard shortcut list | Shift+? |

---

## Screen Reader Support

Power BI reads: **visual title → visual type → alt text**

For full screen reader support:
- Every visual must have a **meaningful title** (not default "Visual")
- Alt text must be present and describe the insight
- Data table mode (Alt+Shift+F11) provides tabular fallback for all chart types

---

## Focus Indicators

Interactive elements must show a visible focus ring when keyboard-focused.

In web/React implementations using Power BI styling:
```css
:focus-visible {
  outline: 2px solid #118DFF;   /* tableAccent / primary brand */
  outline-offset: 2px;
}
```
Never suppress `:focus-visible` for aesthetic reasons.

---

## Titles and Labels

- Visual titles: required on all data visuals. Use clear, specific language. ❌ "Sales" → ✅ "Monthly Sales by Region (FY2024)"
- Avoid acronyms unless defined elsewhere on the page
- Avoid jargon — "Rev." → "Revenue"
- Axis labels: always show unit of measure. "Revenue ($M)", "Count (thousands)"
- Legend labels: spell out fully, don't abbreviate

---

## Tooltips

Tooltips are secondary — do not put essential information only in tooltips.

- Tooltip text must meet contrast requirements
- Do not rely on tooltips to explain what a color means
- Tooltips should confirm or expand, not replace, the main visual

---

## High Contrast Mode

Power BI detects Windows high contrast settings automatically.

When building for high contrast:
- Test with Windows High Contrast Black and White themes
- Do not use custom colors that override system high-contrast colors for interactive elements (buttons, links)
- The `High Contrast` built-in theme provides safe default overrides

---

## Motion and Animation

Power BI Desktop does not support CSS animation in reports. However:

- Do **not** auto-play video or audio on page load
- Play Axis custom visual: must require user interaction to start — never auto-play
- Provide transcripts for any video or audio content embedded
- Avoid the "scatter chart play axis" animation for published reports unless users can pause/stop

---

## Accessibility Checklist (Pre-Publish)

Before publishing any Power BI report:

**Contrast**
- [ ] All body text passes 4.5:1 against its background
- [ ] All large text (18pt+) passes 3:1
- [ ] All UI components (icons, borders) pass 3:1
- [ ] Status colors pass contrast on card/table backgrounds

**Color Blindness**
- [ ] No information is conveyed by color alone
- [ ] Status indicators have icon + color
- [ ] Multi-series charts have distinct marker shapes
- [ ] Tested with colorblind simulator (e.g., Coblis, Sim Daltonism)

**Alt Text**
- [ ] All meaningful visuals have descriptive alt text
- [ ] Alt text describes the insight, not the visual type
- [ ] Decorative elements are marked as decorative (empty alt text / hidden from tab order)

**Navigation**
- [ ] Tab order set logically (title → filters → KPIs → charts)
- [ ] All visuals reachable by keyboard
- [ ] Decorative elements removed from tab order

**Labels & Titles**
- [ ] All visuals have clear, specific titles
- [ ] Axes labeled with units
- [ ] No unexplained acronyms

**Screen Reader**
- [ ] Tested with Narrator (Windows) or NVDA
- [ ] Visual type + alt text reads correctly
- [ ] Data table mode (Alt+Shift+F11) works for all visuals
