# Fluent 2 Color Alias Tokens

These are the semantic alias tokens used throughout Fluent 2. Use these — never raw hex values.

## Neutral Foreground (Text)

| Token | Light Value | Use |
|---|---|---|
| `colorNeutralForeground1` | `#242424` | Primary body text |
| `colorNeutralForeground2` | `#424242` | Secondary text, labels |
| `colorNeutralForeground3` | `#616161` | Placeholder, disabled label |
| `colorNeutralForeground4` | `#707070` | Decorative / least emphasis |
| `colorNeutralForegroundDisabled` | `#BDBDBD` | Disabled text |
| `colorNeutralForegroundInverted` | `#FFFFFF` | Text on dark/filled surfaces |
| `colorNeutralForegroundOnBrand` | `#FFFFFF` | Text on brand background |

## Neutral Background (Surfaces)

| Token | Light Value | Use |
|---|---|---|
| `colorNeutralBackground1` | `#FFFFFF` | Page canvas, primary surface |
| `colorNeutralBackground2` | `#F5F5F5` | Cards, secondary surfaces |
| `colorNeutralBackground3` | `#F0F0F0` | Nested panels, nav rail |
| `colorNeutralBackground4` | `#E8E8E8` | Input fill (default) |
| `colorNeutralBackground5` | `#E0E0E0` | Deeply nested containers |
| `colorNeutralBackground6` | `#C8C8C8` | Hover on neutral bg |
| `colorNeutralBackgroundDisabled` | `#F0F0F0` | Disabled control surface |
| `colorNeutralBackgroundInverted` | `#242424` | Inverted surface (dark tooltip) |

## Neutral Stroke (Borders)

| Token | Light Value | Use |
|---|---|---|
| `colorNeutralStroke1` | `#D1D1D1` | Default border |
| `colorNeutralStroke2` | `#E0E0E0` | Subtle divider |
| `colorNeutralStroke3` | `#F0F0F0` | Barely-visible grid line |
| `colorNeutralStrokeAccessible` | `#616161` | Accessible border for controls |
| `colorNeutralStrokeDisabled` | `#E0E0E0` | Disabled border |
| `colorStrokeFocus1` | `#FFFFFF` | Focus inner ring |
| `colorStrokeFocus2` | `#000000` | Focus outer ring |

## Brand Colors (Communication Blue defaults)

| Token | Light Value | Use |
|---|---|---|
| `colorBrandBackground` | `#0F6CBD` | Primary brand fill |
| `colorBrandBackgroundHover` | `#115EA3` | Hover brand fill |
| `colorBrandBackgroundPressed` | `#0E4775` | Pressed brand fill |
| `colorBrandBackgroundSelected` | `#0E4775` | Selected brand fill |
| `colorBrandForeground1` | `#0F6CBD` | Brand text on light surface |
| `colorBrandForeground2` | `#115EA3` | Brand text hover |
| `colorBrandStroke1` | `#0F6CBD` | Brand border |
| `colorBrandStroke2` | `#B4D6FA` | Subtle brand border |

## Status Colors

### Success
| Token | Light Value |
|---|---|
| `colorStatusSuccessBackground1` | `#F1FAF1` |
| `colorStatusSuccessBackground2` | `#107C10` |
| `colorStatusSuccessForeground1` | `#107C10` |
| `colorStatusSuccessForeground2` | `#0E700E` |
| `colorStatusSuccessBorderActive` | `#107C10` |

### Warning
| Token | Light Value |
|---|---|
| `colorStatusWarningBackground1` | `#FFF9F0` |
| `colorStatusWarningBackground2` | `#F7630C` |
| `colorStatusWarningForeground1` | `#BC4B09` |
| `colorStatusWarningForeground2` | `#A13800` |
| `colorStatusWarningBorderActive` | `#F7630C` |

### Danger / Error
| Token | Light Value |
|---|---|
| `colorStatusDangerBackground1` | `#FDF3F4` |
| `colorStatusDangerBackground2` | `#C50F1F` |
| `colorStatusDangerForeground1` | `#C50F1F` |
| `colorStatusDangerForeground2` | `#B10E1C` |
| `colorStatusDangerBorder1` | `#C50F1F` |

### Info
| Token | Light Value |
|---|---|
| `colorStatusInfoBackground1` | `#F0F6FC` |
| `colorStatusInfoBackground2` | `#0078D4` |
| `colorStatusInfoForeground1` | `#004377` |
| `colorStatusInfoForeground2` | `#003966` |

## Presence / Availability Indicators

| Status | Token | Value |
|---|---|---|
| Available | `colorPresenceAvailable` | `#107C10` |
| Away | `colorPresenceAway` | `#F7630C` |
| Busy / DND | `colorPresenceBusy` | `#C50F1F` |
| Offline | `colorPresenceOffline` | `#8A8886` |
| Out of Office | `colorPresenceOOF` | `#B4009E` |
| Unknown | `colorPresenceUnknown` | `#8A8886` |

## Dark Theme Notes

In dark mode, Fluent 2 inverts the neutral scale:
- `colorNeutralBackground1` → `#1A1A1A`
- `colorNeutralBackground2` → `#141414`
- `colorNeutralForeground1` → `#F7F7F7`
- Brand colors remain close but adjust saturation for legibility

All @fluentui/react-components tokens handle this automatically via `webDarkTheme`.
