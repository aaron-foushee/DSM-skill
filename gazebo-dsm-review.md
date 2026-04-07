# Gazebo DSM — Baseline & Decisions

> **Source:** Figma file "Gazebo • DSM • 2025" + EMAP Demo prototype + Marketing brand guidelines
> **Date:** March 27, 2026
> **Purpose:** Document the current MUI-based design system, decisions made so far, and open items for the Gazebo theme skill.

---

## How to read this doc

- ✅ = Decision made
- 🔶 = Proposed change (needs review)
- ⬜ = Not yet reviewed — carry forward as-is until next session

---

## 1. Color Palette

### 1.1 Primary ⬜

No value changes proposed. Usage strategy discussed — see section 1.8.

| Token | Hex | Usage |
|-------|-----|-------|
| `primary/main` | `#017bb1` | Primary actions, active states |
| `primary/dark` | `#0a5183` | Hover/pressed primary elements |
| `primary/light` | `#40bbf1` | Light primary backgrounds, highlights |
| `primary/contrastText` | `#ffffff` | Text on primary backgrounds |

**Interaction states** (auto-derived from main):

| State | Value | Opacity |
|-------|-------|---------|
| `hover` | `#017bb10a` | 4% |
| `selected` | `#017bb114` | 8% |
| `focus` | `#017bb11f` | 12% |
| `focusVisible` | `#017bb14d` | 30% |
| `outlinedBorder` | `#017bb180` | 50% |

### 1.2 Secondary ⬜

No changes. Matches brand Lagoon exactly (`#06B2B4`).

| Token | Hex |
|-------|-----|
| `secondary/main` | `#06b2b4` |
| `secondary/dark` | `#048184` |
| `secondary/light` | `#5ee0e2` |
| `secondary/contrastText` | `#ffffff` |

### 1.3 Error ⬜

No changes proposed.

| Token | Hex |
|-------|-----|
| `error/main` | `#cf4626` |
| `error/dark` | `#b0381c` |
| `error/light` | `#e78578` |
| `error/contrastText` | `#ffffff` |

### 1.4 Warning 🔶

**Problem:** Current burnt orange is muddy, trends toward brown. Feels dirty, not cautious.

**Proposal:** Shift from orange → amber/gold. Cleaner "caution" signal. The proposed light value (`#e6a817`) is already used in the EMAP demo for installation status.

| Token | Current | Proposed |
|-------|---------|----------|
| `warning/light` | `#f6882c` | `#e6a817` |
| `warning/main` | `#d06a13` | `#b8860b` |
| `warning/dark` | `#9e4901` | `#8a6508` |
| `warning/contrastText` | `#ffffff` | `#ffffff` (no change) |

States auto-derive from new main at same opacity percentages.

### 1.5 Info ⬜

No changes proposed.

| Token | Hex |
|-------|-----|
| `info/main` | `#0288d1` |
| `info/dark` | `#01579b` |
| `info/light` | `#03a9f4` |
| `info/contrastText` | `#ffffff` |

### 1.6 Success 🔶

**Problem:** Current sage green reads as "calm/natural," not "success." Light and main too close — not enough tonal range.

**Proposal:** Shift from desaturated sage → clear forest green. Wider tonal range. Still restrained and distinct from secondary teal.

| Token | Current | Proposed |
|-------|---------|----------|
| `success/light` | `#6dab7f` | `#4caf7c` |
| `success/main` | `#649a72` | `#2e7d5b` |
| `success/dark` | `#52816c` | `#1b5e43` |
| `success/contrastText` | `#ffffff` | `#ffffff` (no change) |

States auto-derive from new main at same opacity percentages.

### 1.7 Text, Action & Surface Colors ⬜

Not yet reviewed for changes.

**Text:**

| Token | Value | Description |
|-------|-------|-------------|
| `text/primary` | `#000000de` | 87% black |
| `text/secondary` | `#00000099` | 60% black |
| `text/disabled` | `#00000061` | 38% black |

**Action:**

| Token | Value | Description |
|-------|-------|-------------|
| `action/active` | `#0000008f` | 56% black |
| `action/hover` | `#0000000a` | 4% black |
| `action/selected` | `#00000014` | 8% black |
| `action/focus` | `#0000001f` | 12% black |
| `action/disabled` | `#00000061` | 38% black |
| `action/disabledBackground` | `#0000001f` | 12% black |

**Surfaces:**

| Token | Value |
|-------|-------|
| `background/default` | `#ffffff` |
| `background/paper-elevation-0` | `#ffffff` |
| `divider` | `#0000001f` |

**Note:** The EMAP demo uses a light gray page background (`#F5F6FA`) and opaque text colors (`#333840`, `#6B7280`) instead of the DSM's pure white + alpha approach. The demo approach may be more practical for the enterprise app. Worth discussing.

### 1.8 Color Strategy Discussion ✅

**Goal:** Mature enterprise look where colors are used sparingly and intentionally.

**Observations:**
- Primary blue (`#017bb1`) is currently over-applied — it handles brand identity, links, active states, icons, and data viz all at once.
- Blue closely resembles default link styling, which creates ambiguity.

**Proposed approach (not yet implemented in tokens):**
- **90% of the UI** — neutrals (text, borders, surfaces, cards)
- **Teal as the workhorse** — progress bars, active states, selected items, data highlights
- **Blue reserved for** — primary CTA buttons, brand header, key navigation only
- **Semantic colors only when needed** — success, warning, error appear only on status pills and alerts
- **Links** — consider underline + text color treatment instead of blue

### 1.9 Marketing Palette Reference ⬜

Documented for cross-reference — **not imported into the DSM**.

| Name | Hex | Relationship to DSM |
|------|-----|-------------------|
| Midnight | `#042F4D` | Darker than DSM primary/dark |
| Lagoon | `#06B2B4` | Exact match to secondary/main |
| Autumn | `#F6882C` | Identical to current warning/light — conflicts with warning semantics, do NOT use as brand accent |
| Azul | `#2DA1DB` | Lighter blue, not in DSM |
| Glacier | `#DFF3FC` | Light blue tint, not in DSM |
| Granite | `#DCDDDD` | Neutral gray, not in DSM |

---

## 2. Typography ⬜

Not yet reviewed for narrowing.

| Token | Value |
|-------|-------|
| `fontFamily` | `Source Sans 3` |
| `fontWeightRegular` | `400` |
| `fontWeightMedium` | `500` |

**Font size scale:**

| Token | Value |
|-------|-------|
| `_fontSize/0,75rem` | `12px` |
| `_fontSize/0,8125rem` | `13px` |
| `_fontSize/0,875rem` | `14px` |
| `_fontSize/1rem` | `16px` |
| `_fontSize/1,5rem` | `22px` |

**Composite styles captured:**

| Style | Size | Weight | Line Height | Letter Spacing |
|-------|------|--------|-------------|----------------|
| `typography/h5` | 22px | 400 | 1.334 | 0 |
| `typography/body2` | 14px | 400 | 1.43 | 0.17px |
| `typography/caption` | 12px | 400 | 1.66 | 0.4px |
| `alert/title` | 16px | 500 | 1.5 | 0.15px |
| `button/small` | 13px | 500 | 22px | 0.46px |
| `table/header` | 14px | 500 | 24px | 0.17px |

**Open:** Full type scale (h1–h4, subtitle1/2, body1, overline) not fully captured. Needs Figma verification.

---

## 3. Shape ⬜

| Token | Value |
|-------|-------|
| `borderRadius` | `4px` |

---

## 4. Elevation System ✅

Reduced from MUI's 24 levels to **4 semantic levels**. Two style options retained per level (whisper + light) — to be finalized after in-app testing.

| Level | Name | Use Cases |
|-------|------|-----------|
| 1 | Resting | Cards at rest, panels, content containers |
| 2 | Raised | Hovered cards, selected items, emphasized surfaces |
| 3 | Overlay | Menus, dropdowns, popovers, autocomplete panels |
| 4 | Modal | Dialogs, modal sheets, full-screen overlays |

**Level 1 — Resting**
- Whisper: `0 1px 2px 0 rgba(0,0,0,0.03), 0 0 0 0.5px rgba(0,0,0,0.04)`
- Light: `0 1px 2px 0 rgba(0,0,0,0.06), 0 1px 3px 0 rgba(0,0,0,0.04)`

**Level 2 — Raised**
- Whisper: `0 2px 4px 0 rgba(0,0,0,0.04), 0 0 0 0.5px rgba(0,0,0,0.04)`
- Light: `0 2px 4px 0 rgba(0,0,0,0.06), 0 1px 6px 0 rgba(0,0,0,0.04)`

**Level 3 — Overlay**
- Whisper: `0 4px 12px 0 rgba(0,0,0,0.05), 0 0 0 0.5px rgba(0,0,0,0.04)`
- Light: `0 4px 12px 0 rgba(0,0,0,0.08), 0 1px 4px 0 rgba(0,0,0,0.04)`

**Level 4 — Modal**
- Whisper: `0 8px 24px 0 rgba(0,0,0,0.06), 0 0 0 0.5px rgba(0,0,0,0.05)`
- Light: `0 8px 24px 0 rgba(0,0,0,0.1), 0 2px 8px 0 rgba(0,0,0,0.04)`

**MUI mapping:** 0 = flat, 1–2 → Resting, 3–4 → Raised, 5–12 → Overlay, 13–24 → Modal

---

## 5. Components

### 5.1 MUI Base Components ✅

Narrowed from 44 → 34 keep + 3 custom. 8 components cut.

**Inputs — keep 12, cut 2:**

| Component | Status | Notes |
|-----------|--------|-------|
| Button | ✅ Keep | Core — heavy use across app |
| IconButton | ✅ Keep | Toolbars, table actions, nav |
| ButtonGroup | ✅ Keep | View switchers, grouped actions |
| ToggleButton | ✅ Keep | View mode toggles (table/board/list) |
| TextField | ✅ Keep | Forms everywhere |
| Multiline TextField | ✅ Keep | Notes, descriptions, comments |
| Select | ✅ Keep | Filters, dropdowns |
| Autocomplete | ✅ Keep | Customer/facility search |
| Checkbox | ✅ Keep | Multi-select, filters, forms |
| Radio | ✅ Keep | Single-select in forms and settings |
| Switch | ✅ Keep | Toggle settings, view modes |
| Slider | ✅ Keep | Future use planned |
| Fab | ✅ Keep | Future use planned |
| Rating | ❌ Cut | Not an energy mgmt pattern |
| LoadingButton | ❌ Cut | Nice-to-have, not core |
| TransferList | ❌ Cut | No use case in Gazebo |

**Data display — keep 9, cut 1:**

| Component | Status | Notes |
|-----------|--------|-------|
| Table | ✅ Keep | Core — projects, tasks, facilities |
| Chip | ✅ Keep | Core — status pills built on this |
| Typography | ✅ Keep | Foundation |
| Divider | ✅ Keep | Section separators |
| Icon | ✅ Keep | Used everywhere |
| Tooltip | ✅ Keep | Data-dense UI needs these |
| List | ✅ Keep | Navigation, menus, task lists |
| Avatar | ✅ Keep | User profiles, assignee initials |
| Date/Time Pickers | ✅ Keep | MUI pickers used in app |
| Badge | ❌ Cut | Not currently used |

**Feedback — keep 4, cut 1:**

| Component | Status | Notes |
|-----------|--------|-------|
| Alert | ✅ Keep | Notifications, validation, status |
| Dialog | ✅ Keep | Confirmations, modals |
| Progress | ✅ Keep | Loading states, savings bars |
| Snackbar | ✅ Keep | Toast notifications |
| Skeleton | ❌ Cut | Not core to theme |

**Surfaces — keep 4:**

| Component | Status | Notes |
|-----------|--------|-------|
| Card | ✅ Keep | Dashboard cards, project cards |
| Paper | ✅ Keep | Base surface component |
| AppBar | ✅ Keep | Top navigation bar |
| Accordion | ✅ Keep | Expandable/collapsible sections |

**Navigation — keep 7, cut 2:**

| Component | Status | Notes |
|-----------|--------|-------|
| Tabs | ✅ Keep | Core — customer/project detail views |
| Breadcrumbs | ✅ Keep | Nav hierarchy in EMAP |
| Link | ✅ Keep | Text links |
| Menu | ✅ Keep | Context menus, user dropdown |
| Drawer | ✅ Keep | Side navigation |
| Pagination | ✅ Keep | Large table paging |
| Stepper | ✅ Keep | Wizard/setup flows |
| BottomNavigation | ❌ Cut | Mobile only |
| SpeedDial | ❌ Cut | Mobile FAB pattern |

**Layout — keep 1, cut 1:**

| Component | Status | Notes |
|-----------|--------|-------|
| TreeView | ✅ Keep | Currently in use |
| Timeline | ❌ Cut | No timeline UI in Gazebo |

### 5.2 Custom Gazebo Chip / Status Pill System ✅

Custom status pills are built as variants of the MUI `<Chip>` component using a `Status` property. These extend the base chip with Gazebo-specific status semantics. Each status has an icon, background color, and text color. "Cancelled" statuses use plain text with no pill background.

**Design principles:**
- **Pill = needs attention/action** — draws the eye
- **Plain text = done/background** — fades to background, provides context without competing
- Icons differentiate statuses that share similar colors

#### Project Status

| Status | Style | Icon | Description |
|--------|-------|------|-------------|
| Open | Light outline | Clock | Available to work on |
| On Hold | Dark muted fill | Pause bars | Paused, needs attention |
| In Progress | Blue fill | Play triangle | Active work happening |
| Complete | Green fill/border | Filled circle | Finished |
| Cancelled | Plain text (no pill) | X circle | Terminated — no action needed |

#### Model Status

| Status | Style | Icon | Description |
|--------|-------|------|-------------|
| Candidate | Light outline | Clock | Available to work on |
| Incomplete | Gray fill | Circle-dash | Missing data |
| Provisional | Blue/teal fill | Gear | Temporary, in validation |
| Active | Green fill | Play triangle | Currently in use |
| Retired | Light green border | Filled circle | Previously used, replaced |
| Cancelled | Plain text (no pill) | X circle | Never used — no action needed |

#### Savings Claims Status

| Status | Style | Icon | Description |
|--------|-------|------|-------------|
| Forecast | Light outline | Chart | Projected savings |
| Provisional | Blue/teal fill | Gear | Temporary claim |
| Final | Green fill | Lock | Verified and locked |
| Cancelled | Plain text (no pill) | X circle | Voided — no action needed |

#### Task Status

| Status | Style | Icon | Description |
|--------|-------|------|-------------|
| In Progress | Blue fill | Play triangle | Active work |
| Complete | Green fill | Filled circle | Done |

#### Color Logic (semantic grouping)

| Color Family | Semantic Meaning | Used For |
|-------------|-----------------|----------|
| Light outline (white/light gray) | Available / waiting | Open, Candidate, Forecast |
| Blue fill | Active work | In Progress, Provisional |
| Green fill | Positive / done | Complete, Active, Final, Retired |
| Dark gray fill | Paused | On Hold |
| Gray fill | Incomplete / neutral | Incomplete |
| Plain text | Background / terminal | All Cancelled states |

#### Additional Chip Variants in DSM

The base `<Chip>` component also includes standard MUI variants:
- **Color:** Default, Primary, Success (filled + outlined)
- **Avatar chips:** With image or initials
- **Sizes:** Standard MUI medium

---

## 6. EMAP Demo Color Divergences (Reference)

The EMAP demo prototype uses its own color system that doesn't fully align with the DSM. Documented here for reconciliation.

| Demo Token | Demo Value | DSM Equivalent | Notes |
|-----------|-----------|----------------|-------|
| `C.teal` | `#1C826E` | `secondary/main` `#06b2b4` | Demo is much darker/greener — lost brand vibrance |
| `C.link` | `#0077B6` | `primary/main` `#017bb1` | Close but not identical |
| `C.headerBg` (actual) | `#021726` | `primary/dark` `#0a5183` | Demo header is darker than both DSM and brand Midnight |
| `C.overdue` | `#C62828` | `error/main` `#cf4626` | Same family, demo is cooler/darker red |
| `C.statusInstall` | `#E6A817` | (none) | Demo-only; proposed as new `warning/light` |
| `C.statusApproved` | `#7C3AED` | (none) | Purple — not in DSM at all |
| `C.pageBg` | `#F5F6FA` | `background/default` `#ffffff` | Demo uses gray bg — worth considering |

**Status colors in EMAP demo (not in DSM):** Identified (gray), In Development (blue), Approved (purple), Installation (yellow), Complete (green) — these use a different status vocabulary than the DSM's Project/Model/Claims system.

---

## 7. Figma vs. MUI npm Drift ✅

The MUI Figma kit has drifted from the actual `@mui/material` npm package defaults for several semantic colors. This affects both prototyping accuracy and developer handoff. Developers **must** apply `createTheme()` overrides — they cannot rely on MUI defaults.

### Color value comparison

| Color | MUI npm default | Figma DSM value | Status |
|-------|----------------|-----------------|--------|
| `primary/main` | `#1976d2` | `#017bb1` | Intentional Gazebo override |
| `secondary/main` | `#9c27b0` | `#06b2b4` | Intentional Gazebo override |
| `error/main` | `#d32f2f` | `#cf4626` | Drifted — Figma is warmer/more orange |
| `warning/main` | `#ed6c02` | `#d06a13` (current) / `#b8860b` (proposed) | Drifted — both Figma and proposed differ from npm |
| `info/main` | `#0288d1` | `#0288d1` | Exact match — no override needed |
| `success/main` | `#2e7d32` | `#649a72` (current) / `#2e7d5b` (proposed) | Drifted — proposed realigns close to MUI default |

**Key finding:** The proposed success values (`#2e7d5b`) are very close to MUI's actual defaults (`#2e7d32`). The "sage green problem" was a Figma kit issue, not a MUI issue.

### Interaction behavior gaps

The Figma kit is a static visual reference — it cannot represent interactive behavior. Many components (date pickers, hover transitions, focus rings, ripple effects, accordion animations, etc.) either don't work or are approximated in Figma.

**Rule:** Figma is the source of truth for *visual styling* (colors, typography, spacing, layout). MUI's component API is the source of truth for *interaction behavior*. The Gazebo theme skill includes a full table mapping each component to the correct code approach.

### Developer `createTheme()` snippet

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
    MuiButton: { styleOverrides: { root: { textTransform: 'none', fontWeight: 500 } } },
  },
});
```

---

## 8. Color Strategy ✅

Finalized hybrid approach — blue for data, teal for navigation, neutral links with blue on hover.

| Color | Role | Where it appears |
|-------|------|-----------------|
| Blue `#017bb1` | Data values | KPI numbers, progress bars, chart data |
| Teal `#06b2b4` | Navigation / active states | Active tab indicators, selected nav items, avatar accents |
| Black + bold `#333840` | Links at rest | Customer names, clickable items |
| Blue `#017bb1` | Links on hover | Reveals blue to confirm clickability |
| Semantic colors | Status only | Error, warning, success — only on pills and alerts |
| Neutrals | Everything else | 90% of the UI — text, borders, surfaces |

Shareable prototype demonstrating this approach: `gazebo-theme-hybrid.html`

---

## 9. Open Items for Next Session

### High priority
- [ ] **Finalize warning/success colors** — Review proposed values with co-designer, commit or adjust
- [ ] **Button variants needed** — Are there custom Gazebo button styles beyond standard MUI?
- [ ] **Build project overview page** — Test the skill against a more complex layout

### Medium priority
- [ ] **Typography narrowing** — Which type scale levels does Gazebo actually use?
- [ ] **Dark mode** — Pull dark mode token values (file supports mode switching)
- [ ] **Status pill colors** — Verify exact hex values from Figma match this documentation
- [ ] **Stress-test skill** — Build more component types to find where the skill breaks

### Lower priority
- [ ] **Spacing scale** — Not yet captured
- [ ] **Breakpoints** — Not yet captured
- [ ] **EMAP demo reconciliation** — Align demo colors with DSM
- [ ] **Status vocabulary alignment** — EMAP uses different status names than DSM chip system

### Decided (no longer open)
- [x] ~~Surface color strategy~~ → Light gray `#F7F7F8` page background, white cards
- [x] ~~Link styling~~ → Black + bold at rest, blue on hover
- [x] ~~Primary blue usage audit~~ → Blue = data values only, not links/nav
- [x] ~~Component narrowing~~ → 34 keep + 3 custom, 8 cut

---

## 10. Gazebo Theme Skill — Complete ✅

The skill has been created and tested. It includes:

1. Full CSS variable system with `--gz-` prefix
2. Color strategy rules (blue = data, teal = nav, black+bold links)
3. 4-level elevation system (whisper default)
4. Typography scale and font guidance
5. 34 approved components + 3 custom (status pills, metric card, progress bar)
6. Pattern recipes for header, KPI cards, data tables, tabs, links, page layout
7. Figma vs. code reality guidance with interaction behavior table
8. `createTheme()` snippet for developer handoff
9. Color drift warnings with exact Figma vs. npm values
10. "What NOT to do" guardrails

**Files:**
- Skill: `gazebo-theme/SKILL.md` + `gazebo-theme/references/status-pills.md`
- Install: Place `gazebo-theme/` folder at `.claude/skills/gazebo-theme/` in project repo for Claude Code, or upload to Claude.ai
- Test prototype: `gazebo-project-detail.html` (project detail page with 5 tabs)
- Theme comparison: `gazebo-theme-hybrid.html` (final hybrid approach demo)
