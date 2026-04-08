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
  --gz-bg-header: #0a5183;
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
Background: var(--gz-bg-header) (#0a5183)
Text: white
Avatar: teal (#06b2b4) circle with white initials
Height: ~48px with 12px vertical padding
Logo: "gazebo" in white, followed by a divider and utility program name
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
