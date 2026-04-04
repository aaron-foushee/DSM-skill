# Gazebo Status Pills Reference

Status pills are custom variants of MUI's `<Chip>` component using Font Awesome 6 Pro icons. They communicate lifecycle state across four domains. Each domain is tied to a specific object type — always use the correct domain's pills for its object.

## Domain-to-object mapping

| Domain | Object | Where it appears |
|--------|--------|-----------------|
| **Project** | Energy conservation project | Project list, project detail status field, project cards |
| **Model** | Savings calculation model | Model list, model detail, model cards within a project |
| **Claims** | Savings claim (forecast/final) | Claims list, claims detail, claims table within a project |
| **Tasks** | Action item / to-do | Task table within a project detail page |

Never mix domains — a Task must never show a Project pill (e.g. "Open"), and a Project must never show a Task pill (e.g. "To Do").

## Visual hierarchy rule

- **Pill (colored background)** = needs attention, active, in progress — draws the eye
- **Plain text (no background)** = terminal state, cancelled — fades to background
- **White + border** = done/complete states — visible but muted

## Pill structure

All pills share this structure:
- `border-radius: 100px` (full capsule via `--gz-radius-pill`)
- `padding: 4px` outer
- **Avatar container**: 18x18px, centered, holds Font Awesome icon at `8px`
- **Label**: `font-size: 13px`, `font-weight: 400`, `line-height: 18px`, `letter-spacing: 0.16px`, `padding: 0 6px`, `min-height: 24px`
- **Small variant** (`.pill-sm`, for table rows): `padding: 2px`, avatar 16x16 at `7px`, label `font-size: 11px`, `min-height: 18px`

## Project status

| Status | Background | Border | Text/Icon Color | FA Icon | FA Style |
|--------|-----------|--------|----------------|---------|----------|
| Open | `#e3f2fd` | `#bfe8fa` | `#0a5183` | `fa-chart-line` | regular |
| On Hold | `#f6f7f7` | `#eceeef` | `#14191b` | `fa-pause` | solid |
| In Progress | `#bfe8fa` | `#80d1f5` | `#0a5183` | `fa-play` | solid |
| Complete | `#ffffff` | `#ddeee2` | `#416862` | `fa-circle-check` | solid |
| Cancelled | `transparent` | `transparent` | `#727576` | `fa-circle-xmark` | regular |

## Model status

| Status | Background | Border | Text/Icon Color | FA Icon | FA Style |
|--------|-----------|--------|----------------|---------|----------|
| Candidate | `#e3f2fd` | `#bfe8fa` | `#0a5183` | `fa-chart-line` | regular |
| Incomplete | `#f6f7f7` | `#eceeef` | `#14191b` | `fa-circle-dashed` | regular |
| Provisional | `#bfe8fa` | `#80d1f5` | `#0a5183` | `fa-circle-check` | regular |
| Active | `#bbddc5` | `#99cca8` | `#416862` | `fa-play` | solid |
| Retired | `#ffffff` | `#ddeee2` | `#416862` | `fa-circle-check` | solid |
| Cancelled | `transparent` | `transparent` | `#727576` | `fa-circle-xmark` | regular |

## Savings claims status

| Status | Background | Border | Text/Icon Color | FA Icon | FA Style |
|--------|-----------|--------|----------------|---------|----------|
| Forecast | `#e3f2fd` | `#bfe8fa` | `#0a5183` | `fa-chart-line` | regular |
| Provisional | `#bfe8fa` | `#80d1f5` | `#0a5183` | `fa-circle-check` | regular |
| Final | `#ffffff` | `#ddeee2` | `#416862` | `fa-lock` | solid |
| Cancelled | `transparent` | `transparent` | `#727576` | `fa-circle-xmark` | regular |

## Task status

| Status | Background | Border | Text/Icon Color | FA Icon | FA Style |
|--------|-----------|--------|----------------|---------|----------|
| To Do | `rgba(0,0,0,0.08)` | `transparent` | `rgba(0,0,0,0.87)` | `fa-pause` | solid |
| In Progress | `#bfe8fa` | `#80d1f5` | `#0a5183` | `fa-play` | solid |
| Complete | `#ffffff` | `#ddeee2` | `#416862` | `fa-circle-check` | solid |

## CSS class mapping

| Treatment | CSS Class |
|-----------|-----------|
| Open / Candidate / Forecast | `.pill-open` |
| On Hold / Incomplete | `.pill-hold` |
| In Progress / Provisional | `.pill-in-progress` |
| Active | `.pill-active` |
| Complete / Retired / Final (Done) | `.pill-done` |
| To Do | `.pill-todo` |
| Cancelled | `.pill-cancelled` |

## Semantic color groupings

| Color family | Meaning | Statuses |
|-------------|---------|----------|
| Light blue (`#e3f2fd`) | Available / waiting | Open, Candidate, Forecast |
| Medium blue (`#bfe8fa`) | Active work happening | In Progress, Provisional |
| Green (`#bbddc5`) | Active positive | Active |
| White + green border | Positive / done | Complete, Retired, Final |
| Light gray (`#f6f7f7`) | Paused / incomplete | On Hold, Incomplete |
| Dark gray (`rgba(0,0,0,0.08)`) | Not started | To Do |
| Transparent | Terminal | All Cancelled states |

## Cross-domain equivalencies

- **Complete** (Project) = **Final** (Savings Claims) = **Retired** (Model)
- **In Progress** (Project/Task) = **Provisional** (Model/Claims)
- **Open** (Project) = **Candidate** (Model) = **Forecast** (Claims)
- **Cancelled** is consistent across all domains

## Implementation notes

- Font: Font Awesome 6 Pro (regular and solid variants)
- `fa-circle-dashed` requires FA6 Pro; use `fa-circle-notch` as a free fallback
- All pills use the same HTML structure: avatar container + label + optional caret
- Icon and text color are always the same within a pill — one `color` declaration covers both
- Do not derive colors from the semantic palette (`--gz-error`, `--gz-success`, etc.) — the pill system has its own color tokens
