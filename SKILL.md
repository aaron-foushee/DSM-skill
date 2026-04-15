---
name: gazebo-theme
description: Apply the Gazebo design system theme when building UI prototypes, widgets, dashboards, navigation, or any front-end components for the Gazebo energy management platform. Use this skill whenever the user mentions Gazebo, EMAP, energy management UI, Cascade Energy prototypes, or asks to build something that should look like the Gazebo app. Also trigger when building MUI-themed components, status pills, metric cards, or enterprise energy dashboards. Even if the user just says "build me a dashboard" or "prototype this page," use this skill if the context suggests Gazebo work.
---

# Gazebo Theme Skill

Apply the Gazebo design system when building prototypes. Gazebo is an enterprise energy management SaaS platform built on MUI (Material UI). This skill provides the theme tokens, color strategy, component guidance, and patterns needed to produce on-brand output.

## Before you start — ask questions

If the user's request is ambiguous, ask about:
- Which page/section of Gazebo this is for (dashboard, project detail, facility view, etc.)
- Whether this needs status pills, and if so which domain (Project, Model, Savings Claims, Task)
- Whether data values are present (to apply the blue = data rule correctly)
- Light or dark header preference (default: primary dark #0a5183)

## Color strategy

This is the most important section. Gazebo uses color sparingly and intentionally. Every color has a specific job.

### The rules

| Color | Hex | Role | Where it appears |
|-------|-----|------|-----------------|
| Primary blue | `#017bb1` | Data values | KPI numbers, progress bars, chart data, metric highlights |
| Teal (Lagoon) | `#06b2b4` | Navigation & active states | Active tab indicators, selected nav items, "changes" count badges, avatar accents |
| Black + bold | `#333840` / font-weight 600 | Links at rest | Customer names, clickable table items, navigable list items |
| Primary blue | `#017bb1` | Links on hover | Hover state for links — reveals blue to confirm clickability |
| Error red | `#cf4626` | Problems only | Overdue counts, off-track status, error alerts |
| Success green | `#2e7d5b` | Positive status only | On-track pills, complete status, verified savings |
| Warning amber | `#b8860b` | Caution only | Behind-on-goal pills, at-risk status, needs-attention alerts |
| Info blue | `#0288d1` | Informational | Info alerts, help tooltips |
| Neutrals | `#333840` / `#6B7280` / `#8a96a3` | Everything else | Body text, labels, metadata, borders, surfaces |

### What this means in practice

- **90% of the UI is neutral** — text, borders, surfaces, cards. Color is the exception, not the default.
- **Blue never means "clickable."** Blue means "this is a data value." Links are black+bold, turning blue on hover.
- **Teal never means "data."** Teal means "this is where you are" or "this is a navigation element."
- **Semantic colors only appear on status pills and alerts.** Never use success green for a button, warning amber for a border, or error red for emphasis.
- **When in doubt, use neutral.** If a number isn't a key metric, render it in `#333840`, not blue. If an element isn't navigational, don't make it teal.

## CSS variables

Always use CSS custom properties for theming. Name them with the `--gz-` prefix.

```css
:root {
  /* Primary palette */
  --gz-primary: #017bb1;
  --gz-primary-dark: #0a5183;
  --gz-primary-light: #40bbf1;
  --gz-secondary: #06b2b4;
  --gz-secondary-dark: #048184;
  --gz-secondary-light: #5ee0e2;

  /* Semantic */
  --gz-error: #cf4626;
  --gz-error-dark: #b0381c;
  --gz-error-light: #e78578;
  --gz-warning: #b8860b;
  --gz-warning-dark: #8a6508;
  --gz-warning-light: #e6a817;
  --gz-success: #2e7d5b;
  --gz-success-dark: #1b5e43;
  --gz-success-light: #4caf7c;
  --gz-info: #0288d1;
  --gz-info-dark: #01579b;
  --gz-info-light: #03a9f4;

  /* Text */
  --gz-text-primary: #333840;
  --gz-text-secondary: #6B7280;
  --gz-text-light: #8a96a3;
  --gz-text-disabled: #b0b5bd;
  --gz-text-on-dark: #ffffff;

  /* Surfaces */
  --gz-bg-page: #F7F7F8;
  --gz-bg-card: #ffffff;
  --gz-bg-header: #021726;
  --gz-border: #ebebed;
  --gz-border-light: #f0f1f5;
  --gz-divider: #e0e3ea;

  /* Shape */
  --gz-radius: 4px;
  --gz-radius-pill: 100px;

  /* Typography */
  --gz-font: 'Source Sans 3', 'Segoe UI', system-ui, sans-serif;
  --gz-weight-regular: 400;
  --gz-weight-medium: 500;
  --gz-weight-bold: 600;
}
```

## Elevation

Use 4 semantic levels. Default to **whisper** (minimal shadow + subtle border) unless the user requests more prominent shadows (**light**).

```css
/* Whisper (default) */
--gz-shadow-1: 0 1px 2px 0 rgba(0,0,0,0.03), 0 0 0 0.5px rgba(0,0,0,0.04);  /* Cards at rest */
--gz-shadow-2: 0 2px 4px 0 rgba(0,0,0,0.04), 0 0 0 0.5px rgba(0,0,0,0.04);  /* Raised/hover */
--gz-shadow-3: 0 4px 12px 0 rgba(0,0,0,0.05), 0 0 0 0.5px rgba(0,0,0,0.04); /* Menus/dropdowns */
--gz-shadow-4: 0 8px 24px 0 rgba(0,0,0,0.06), 0 0 0 0.5px rgba(0,0,0,0.05); /* Modals */

/* Light (alternative) */
--gz-shadow-1-light: 0 1px 2px 0 rgba(0,0,0,0.06), 0 1px 3px 0 rgba(0,0,0,0.04);
--gz-shadow-2-light: 0 2px 4px 0 rgba(0,0,0,0.06), 0 1px 6px 0 rgba(0,0,0,0.04);
--gz-shadow-3-light: 0 4px 12px 0 rgba(0,0,0,0.08), 0 1px 4px 0 rgba(0,0,0,0.04);
--gz-shadow-4-light: 0 8px 24px 0 rgba(0,0,0,0.1), 0 2px 8px 0 rgba(0,0,0,0.04);
```

## Typography

Font: **Source Sans 3**. Fall back to Segoe UI, then system-ui.

| Style | Size | Weight | Line height | Letter spacing | Use |
|-------|------|--------|-------------|---------------|-----|
| Page title | 22px | 400 | 1.33 | 0 | Page headings ("Welcome, Eric Strand") |
| Section title | 16px | 600 | 1.5 | 0 | Card headers, section labels |
| Body | 14px | 400 | 1.43 | 0.17px | Default text |
| Body small | 13px | 400 | 1.5 | 0.16px | Table cells, secondary content |
| Caption | 12px | 400 | 1.66 | 0.4px | KPI labels, metadata |
| Overline | 11px | 500 | 1.5 | 0.03em | Table headers (uppercase) |
| KPI value | 26px | 400 | 1.2 | 0 | Dashboard metric numbers |
| Button | 13px | 500 | 22px | 0.46px | Button labels |

## Components — what to use

Gazebo uses these MUI components. If you need a component not on this list, ask.

**Inputs:** Button, IconButton, ButtonGroup, ToggleButton, TextField, Multiline, Select, Autocomplete, Checkbox, Radio, Switch, Slider, Fab, Date/Time Pickers

**Data display:** Table, Chip (+ custom status pills), Typography, Divider, Icon, Tooltip, List, Avatar, Date/Time

**Feedback:** Alert, Dialog, Progress, Snackbar

**Surfaces:** Card, Paper, AppBar, Accordion

**Navigation:** Tabs, Breadcrumbs, Link, Menu, Drawer, Pagination, Stepper, TreeView

**Custom Gazebo components:** Status Pills, Metric Card, Labeled Progress Bar

## Status pills

Status pills are variants of MUI Chip. They follow a strict visual hierarchy: **pills for active states** (needs attention), **plain text for terminal states** (done/cancelled).

For full status pill definitions including all four domains (Project, Model, Savings Claims, Task), colors, icons, and styling rules, read `references/status-pills.md`.

## Patterns

### App header
```
Background: var(--gz-bg-header) (#021726)
Text: white
Avatar: teal (#06b2b4) circle with white initials
Height: ~48px with 12px vertical padding
Logo: SVG wordmark in white + teal chevron (see below), followed by a divider and utility program name

Logo placement:
- Left-aligned, 24px margin from the left edge and 24px margin top/bottom
- Centered vertically within the appbar height
- Do not scale or recolor — render at native 100×24px
```

### Logo SVG

The Gazebo logo is a wordmark ("gazebo") in white with a teal (`#00B3B4`) right-pointing chevron bracket. Render it at 100×24 on the dark header background. Do not recolor it — the white paths and teal chevron are fixed brand assets.

```svg
<svg width="100" height="24" viewBox="0 0 100 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<g clip-path="url(#clip0_15015_3648)">
<path d="M33.1416 9.00312H38.6126L32.5962 17.4617V17.5532H43.6576V14.9969H37.6113L43.6576 6.49256V6.44684H33.1416V9.00312Z" fill="white"/>
<path d="M72.517 7.01628C71.6435 6.50502 70.6847 6.25147 69.6366 6.25147C68.5117 6.25147 67.5402 6.50086 66.7093 6.99549C66.2917 7.24489 65.921 7.54832 65.6057 7.89747V2.01593H62.7594V17.5532H65.6057V16.1108C65.9253 16.46 66.2917 16.7593 66.7093 17.0128C67.5359 17.5074 68.5202 17.7568 69.6579 17.7568C70.7061 17.7568 71.6648 17.4991 72.5383 16.992C73.4118 16.4808 74.1063 15.7825 74.6219 14.893C75.1374 14.0035 75.3974 13.0433 75.3974 12.0042C75.3974 10.965 75.1374 10.0048 74.6133 9.11534C74.0892 8.22584 73.3904 7.52753 72.517 7.01628ZM72.1036 13.6543C71.8096 14.1489 71.4006 14.548 70.885 14.8431C70.3694 15.1382 69.7985 15.2878 69.1764 15.2878C68.4946 15.2878 67.8811 15.1424 67.3442 14.8556C66.803 14.5688 66.3855 14.1697 66.0787 13.6668C65.7761 13.1638 65.6228 12.6069 65.6228 12C65.6228 11.3931 65.7761 10.8362 66.0787 10.3332C66.3812 9.83027 66.803 9.4354 67.3442 9.14444C67.8811 8.85763 68.4946 8.71215 69.1764 8.71215C69.7985 8.71215 70.3694 8.86179 70.885 9.15691C71.4006 9.45202 71.8054 9.85105 72.1036 10.3457C72.3977 10.8403 72.5468 11.3931 72.5468 12C72.5468 12.6069 72.3977 13.1597 72.1036 13.6543Z" fill="white"/>
<path d="M90.4554 9.10284C89.9143 8.22165 89.1729 7.52335 88.2227 7.00378C87.2725 6.48421 86.2328 6.2265 85.0909 6.2265C83.949 6.2265 82.888 6.48421 81.9378 7.00378C80.9876 7.52335 80.2462 8.22165 79.7051 9.10284C79.1682 9.98404 78.8955 10.9484 78.8955 12C78.8955 13.0516 79.1639 14.0159 79.7051 14.8971C80.242 15.7783 80.9876 16.4766 81.9378 16.9962C82.888 17.5157 83.9362 17.7734 85.0909 17.7734C86.2456 17.7734 87.2725 17.5157 88.2227 16.9962C89.1729 16.4766 89.9143 15.7783 90.4554 14.8971C90.9923 14.0159 91.265 13.0516 91.265 12C91.265 10.9484 90.9966 9.98404 90.4554 9.10284ZM87.9713 13.6543C87.6773 14.1489 87.2683 14.5438 86.7527 14.8306C86.2371 15.1174 85.6747 15.2629 85.0696 15.2629C84.4646 15.2629 83.8851 15.1174 83.3865 14.8306C82.8837 14.5438 82.4875 14.1489 82.1892 13.6543C81.8952 13.1596 81.7461 12.6068 81.7461 12C81.7461 11.3931 81.8952 10.8403 82.1892 10.3457C82.4875 9.85103 82.888 9.45615 83.3951 9.16935C83.9021 8.88255 84.4688 8.73707 85.0909 8.73707C85.713 8.73707 86.2542 8.88255 86.7655 9.16935C87.2725 9.45615 87.6773 9.85103 87.9713 10.3457C88.2653 10.8403 88.4144 11.3931 88.4144 12C88.4144 12.6068 88.2653 13.1596 87.9713 13.6543Z" fill="white"/>
<path d="M26.0343 8.0679C25.719 7.7229 25.3526 7.42779 24.9393 7.17839C24.1169 6.69208 23.1539 6.44684 22.0504 6.44684C21.0363 6.44684 20.0946 6.69623 19.2296 7.19918C18.3647 7.70212 17.6744 8.38795 17.1588 9.26083C16.6432 10.1337 16.3876 11.0814 16.3876 12.0998C16.3876 13.1181 16.6432 14.0658 17.1503 14.9387C17.6573 15.8116 18.3433 16.5016 19.2083 17.0004C20.0733 17.5033 21.0235 17.7527 22.0504 17.7527C23.1539 17.7527 24.1169 17.5075 24.9393 17.0211C25.3569 16.7717 25.7233 16.4766 26.0343 16.1316V17.5532H28.8338V6.64635H26.0343V8.0679ZM25.5443 13.7416C25.2461 14.2362 24.8328 14.627 24.3001 14.9096C23.7718 15.1922 23.1753 15.3336 22.5191 15.3336C21.8629 15.3336 21.326 15.1881 20.819 14.8971C20.3119 14.6062 19.9114 14.2155 19.6216 13.7291C19.3319 13.2428 19.187 12.6983 19.187 12.1039C19.187 11.5095 19.3319 10.965 19.6216 10.4787C19.9114 9.99239 20.3119 9.60167 20.819 9.31071C21.326 9.01975 21.8927 8.87427 22.5191 8.87427C23.1454 8.87427 23.7675 9.0156 24.3001 9.29824C24.8285 9.58089 25.2418 9.9716 25.5443 10.4662C25.8426 10.9609 25.9917 11.5054 25.9917 12.1039C25.9917 12.7025 25.8426 13.247 25.5443 13.7416Z" fill="white"/>
<path d="M9.64677 6.64635V8.0679C9.33146 7.7229 8.96502 7.42779 8.55171 7.17839C7.72934 6.69208 6.76637 6.44684 5.66279 6.44684C4.64869 6.44684 3.70702 6.69623 2.84205 7.19918C1.97708 7.70212 1.2868 8.38795 0.77123 9.26083C0.255656 10.1337 0 11.0814 0 12.0998C0 13.1181 0.255656 14.0658 0.762708 14.9387C1.26976 15.8116 1.95577 16.5016 2.82074 17.0004C3.68571 17.5033 4.6359 17.7527 5.66279 17.7527C6.76637 17.7527 7.72934 17.5075 8.55171 17.0211C8.96928 16.7717 9.33572 16.4766 9.64677 16.1316V17.0294C9.64677 17.7568 9.48059 18.3596 9.14398 18.8417C8.80736 19.3239 8.34718 19.6813 7.75491 19.9224C7.1669 20.1635 6.47663 20.284 5.68409 20.284C5.10035 20.284 4.52086 20.2217 3.94989 20.097L3.28518 22.3291C4.12033 22.5203 4.95121 22.62 5.77357 22.62C7.10299 22.62 8.27048 22.3956 9.27607 21.9425C10.2816 21.4894 11.0614 20.8327 11.6153 19.9681C12.1692 19.1036 12.4419 18.0727 12.4419 16.8798V6.64635H9.64251H9.64677ZM9.15676 13.7416C8.85849 14.2362 8.44518 14.627 7.91257 14.9096C7.38421 15.1922 6.78768 15.3336 6.13149 15.3336C5.47531 15.3336 4.93843 15.1881 4.43138 14.8971C3.92433 14.6062 3.5238 14.2155 3.23405 13.7291C2.94431 13.2428 2.79944 12.6983 2.79944 12.1039C2.79944 11.5095 2.94431 10.965 3.23405 10.4787C3.5238 9.99239 3.92433 9.60167 4.43138 9.31071C4.93843 9.01975 5.50513 8.87427 6.13149 8.87427C6.75785 8.87427 7.37995 9.01559 7.91257 9.29824C8.44092 9.58089 8.85423 9.9716 9.15676 10.4662C9.45503 10.9609 9.60416 11.5054 9.60416 12.1039C9.60416 12.7025 9.45503 13.247 9.15676 13.7416Z" fill="white"/>
<path d="M55.4093 15.2213C54.7872 15.3834 54.1182 15.4665 53.4024 15.4665C52.5502 15.4665 51.8216 15.3169 51.2165 15.0218C50.6072 14.7267 50.147 14.3193 49.8275 13.7998C49.6442 13.5047 49.5207 13.1846 49.444 12.8438H58.7541C58.784 12.5777 58.801 12.2951 58.801 12C58.801 10.9193 58.5411 9.93832 58.0255 9.05713C57.5099 8.17594 56.7984 7.48595 55.8865 6.97885C54.9747 6.4759 53.9265 6.22235 52.7462 6.22235C51.5659 6.22235 50.5007 6.4759 49.559 6.98716C48.6173 7.49842 47.8802 8.18841 47.3518 9.06544C46.8192 9.93832 46.5551 10.9151 46.5551 11.9958C46.5551 13.0765 46.832 14.0367 47.3859 14.9179C47.9399 15.7991 48.7281 16.4932 49.755 17.0045C50.7776 17.5157 51.9579 17.7693 53.2959 17.7693C54.3014 17.7693 55.2261 17.6446 56.0655 17.3994L55.4135 15.2172L55.4093 15.2213ZM49.7721 10.1794C50.0533 9.64736 50.4496 9.22755 50.9651 8.92412C51.4807 8.62069 52.0815 8.4669 52.7632 8.4669C53.445 8.4669 54.0202 8.61653 54.5273 8.91165C55.0343 9.20676 55.4263 9.62658 55.699 10.1669C55.8183 10.4039 55.9078 10.6616 55.976 10.9317H49.4866C49.5548 10.6657 49.6485 10.4122 49.7721 10.1752V10.1794Z" fill="white"/>
<path d="M92.897 24H78.8998V21.2484H91.2693L96.7403 12L91.2693 2.7558H78.8998V0H92.897L100 12L92.897 24Z" fill="#00B3B4"/>
</g>
<defs>
<clipPath id="clip0_15015_3648">
<rect width="100" height="24" fill="white"/>
</clipPath>
</defs>
</svg>
```

### KPI / metric cards
```
Background: var(--gz-bg-card)
Border: 1px solid var(--gz-border)
Border-radius: var(--gz-radius) (6px for cards)
Padding: 14px 16px
Label: 12px, var(--gz-text-secondary)
Value: 26px, weight 400, var(--gz-primary) for data values
Sub-text: 11px, var(--gz-text-light)
Progress bar: 5px height, track #E8ECF0, fill var(--gz-primary)
```

### Overdue / error card
Same as metric card but with `border-color: var(--gz-error)` and value in `var(--gz-error)`.

### Data table
```
Header: 11px uppercase, weight 500, var(--gz-text-secondary), letter-spacing 0.03em
Cells: 13px, var(--gz-text-primary)
Row border: 1px solid var(--gz-border-light)
Row hover: background #fafafa
Links in tables: font-weight 600, color var(--gz-text-primary), hover color var(--gz-primary)
```

### Tab bar
```
Active tab: color var(--gz-secondary), border-bottom 2px solid var(--gz-secondary)
Inactive tab: color var(--gz-text-secondary)
Bar border: 2px solid var(--gz-divider)
Font: 13px, weight 500
```

### Links
```
Default: color var(--gz-text-primary), font-weight 600, no underline
Hover: color var(--gz-primary)
Never use blue as the resting state for links. Blue at rest means data.
```

### Page layout
```
Page background: var(--gz-bg-page) (#F7F7F8)
Card background: var(--gz-bg-card) (#ffffff)
Content padding: 24px
Card gap: 10-14px
Cards lift off the gray background via white fill + subtle border
```

## Modals

Modals follow a consistent structure across Gazebo. Match this pattern exactly.

### Structure
```
┌──────────────────────────────────────┐
│ Modal Title                        ✕ │
│ ──────────────────────────────────── │
│                                      │
│ Label                                │
│ ┌──────────────────────────────────┐ │
│ │ Input value                      │ │
│ └──────────────────────────────────┘ │
│                                      │
│ Label                                │
│ ┌──────────────────────────────────┐ │
│ │ Input value                      │ │
│ └──────────────────────────────────┘ │
│                                      │
│                    [ Save ] [Cancel] │
└──────────────────────────────────────┘
```

### Styling rules
- **Title**: 22px, weight 400, var(--gz-text-primary)
- **Close button**: X icon (fa-xmark), top-right, var(--gz-text-light)
- **Divider**: 1px solid var(--gz-divider) below header
- **Labels**: 14px, weight 600, var(--gz-primary-dark) (#0a5183) — stacked above inputs, not floating
- **Inputs**: full-width outlined, 40px height, 14px font, MUI hover/focus states
- **Save button**: var(--gz-primary) background, white text
- **Cancel button**: var(--gz-text-secondary) background (#6B7280), white text — **never use teal for cancel**
- **Danger button** (delete): var(--gz-error) background, white text
- **Button alignment**: right-aligned (justify-content: flex-end)
- **Modal width**: 460px, border-radius 8px, padding 28px 32px
- **Overlay**: rgba(0,0,0,0.4) backdrop

## Buttons

| Variant | Background | Text | Use |
|---------|-----------|------|-----|
| Primary | var(--gz-primary) | white | Main action (Save, Add, Submit) |
| Cancel / Secondary | var(--gz-text-secondary) | white | Cancel, dismiss, close |
| Danger | var(--gz-error) | white | Delete, remove, destructive actions |
| Ghost | white + 1px var(--gz-border) | var(--gz-text-secondary) | Tertiary actions (+ CREATE, filter toggles) |

**Never use teal (--gz-secondary) for buttons.** Teal is for navigation and active tab states only.

## Avatars / assignee badges

Use muted tinted backgrounds, not solid color fills. Each team member has an assigned color.

```css
/* Muted avatar — tinted background, colored initials */
background: {memberColor}22;   /* color + 22 hex alpha = ~13% opacity */
color: {memberColor};           /* full color for initials text */
border-radius: 50%;
font-size: 9px;
font-weight: 600;
```

Do not use solid saturated backgrounds for avatars — they're too visually heavy for the Gazebo aesthetic. The tinted approach keeps avatars identifiable without competing with status pills and data values.

## Overdue indicator

Use a custom alarm clock SVG icon in var(--gz-error) for overdue dates. Do not use Font Awesome's fa-alarm-clock (it requires FA Pro). The custom SVG is embedded inline:

```
Size: 10x11px (list/table views), 9x10px (board cards)
Color: currentColor (inherits from parent, which should be var(--gz-error))
Vertical-align: -1px
Only show on overdue dates — never on future or completed task dates
```

## Inline editing

Editable fields should give visual cues on hover to indicate interactivity:

```css
/* Hover cue for editable text */
.editable:hover {
  background: var(--gz-bg-page);  /* subtle gray highlight */
  border-radius: 2px;
}

/* Active edit state — inline input */
.edit-input {
  border: 1px solid var(--gz-primary);
  border-radius: var(--gz-radius);
  font-size: 13px;
  font-family: var(--gz-font);
}
```

- Task descriptions: click or double-click to edit inline
- Due dates: click to open date picker
- Assignees: click to open dropdown

## Search highlighting

When search/filter is active, highlight matching text with a warm yellow background:

```css
mark.search-match {
  background: #fff3cd;
  color: inherit;
  border-radius: 2px;
  padding: 0 1px;
}
```

Apply highlighting to task descriptions, project names, assignee names, and site names across all views (list, table, board).

## Figma vs. code reality

The Gazebo DSM lives in a Figma MUI kit. The Figma kit is a static visual reference — it cannot represent interactive behavior. When building prototypes or production code, follow these rules:

### Use the skill for: visual styling
Colors, typography, spacing, elevation, border radius, status pill colors, layout patterns — all of these come from this skill and the Gazebo DSM. The Figma file is the visual source of truth for these.

### Use MUI's actual component API for: interactions
The Figma kit shows static snapshots of interactive components. Many of these don't work correctly in Figma (date pickers, hover state transitions, focus rings, etc.). **Do not try to reverse-engineer interaction behavior from Figma screenshots.** Instead, use MUI's documented component behavior:

| Component | Figma shows | Code should use |
|-----------|------------|-----------------|
| DatePicker / DateRangePicker | Static calendar screenshot | MUI's `@mui/x-date-pickers` with full keyboard nav, mobile/desktop variants, opening animations |
| Select / Autocomplete | Static dropdown snapshot | MUI's actual dropdown with filtering, keyboard navigation, scroll, clear button |
| Button hover/press | Sometimes a separate variant, sometimes missing | MUI's built-in ripple effect + color transition (override ripple color with Gazebo primary) |
| Focus states | Approximated with a ring variant | MUI's native `:focus-visible` with `outline` — use `2px solid var(--gz-primary)` with `2px offset` |
| Tooltip | Static positioned label | MUI Tooltip with default enter/leave delays and smart positioning |
| Drawer | Static open state | MUI Drawer with slide transition |
| Dialog | Static centered card | MUI Dialog with fade + backdrop |
| Accordion | Static expanded state | MUI Accordion with expand/collapse animation |
| Snackbar | Static toast | MUI Snackbar with auto-hide (default 5s), slide-up enter, fade exit |
| Tabs | Static selected state | MUI Tabs with indicator slide animation |
| Progress (linear) | Static bar | MUI LinearProgress with animation for indeterminate state |

### Key interaction overrides for Gazebo theme

When creating a `createTheme()` override for MUI, these are the interaction-specific values:

```js
const gazeboTheme = createTheme({
  palette: {
    primary: { main: '#017bb1', dark: '#0a5183', light: '#40bbf1' },
    secondary: { main: '#06b2b4', dark: '#048184', light: '#5ee0e2' },
    error: { main: '#cf4626', dark: '#b0381c', light: '#e78578' },
    warning: { main: '#b8860b', dark: '#8a6508', light: '#e6a817' },
    success: { main: '#2e7d5b', dark: '#1b5e43', light: '#4caf7c' },
    info: { main: '#0288d1', dark: '#01579b', light: '#03a9f4' },
  },
  shape: { borderRadius: 4 },
  typography: { fontFamily: "'Source Sans 3', 'Segoe UI', system-ui, sans-serif" },
  components: {
    MuiButton: {
      styleOverrides: {
        root: { textTransform: 'none', fontWeight: 500 },
      },
    },
  },
});
```

### Color drift warning

The Figma MUI kit has drifted from npm MUI defaults for error, warning, and success. The Figma values are the Gazebo-intended values. Developers must apply the `createTheme()` overrides above — do not rely on MUI defaults for these three semantic colors. Info is the only semantic color that matches MUI defaults exactly.

| Color | MUI npm default | Gazebo / Figma value | Notes |
|-------|----------------|---------------------|-------|
| error/main | `#d32f2f` | `#cf4626` | Gazebo is warmer/more orange |
| warning/main | `#ed6c02` | `#b8860b` (proposed) | Intentional shift to amber |
| success/main | `#2e7d32` | `#2e7d5b` (proposed) | Very close to MUI default |
| info/main | `#0288d1` | `#0288d1` | Exact match — no override needed |

## What NOT to do

- Do not use blue for links at rest — blue means data
- Do not use teal for data values — teal means navigation
- Do not use semantic colors (success/warning/error) decoratively
- Do not use MUI's default 24-level elevation — use the 4-level Gazebo system
- Do not use the marketing palette's Autumn orange (#F6882C) — it conflicts with warning semantics
- Do not use more than 2-3 colors on any single view — lean on neutrals
- Do not bold mid-sentence text — bold is for labels, headings, and link names only
- Do not use a pure white page background — use #F7F7F8 (light gray) so cards have natural separation
- Do not try to replicate Figma interaction behavior — use MUI's actual component API for hover states, transitions, focus rings, date pickers, and all interactive patterns
- Do not assume MUI defaults match the Figma DSM for error, warning, or success — always apply the Gazebo theme overrides
