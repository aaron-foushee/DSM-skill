# Gazebo Status Pills Reference

Status pills are custom variants of MUI's `<Chip>` component. They communicate project lifecycle state across four domains.

## Visual hierarchy rule

- **Pill (colored background)** = needs attention, active, in progress — draws the eye
- **Plain text (no background)** = terminal state, done, cancelled — fades to background

This ensures users can quickly scan for what needs their attention.

## Project status

| Status | Treatment | Background | Text | Icon |
|--------|-----------|-----------|------|------|
| Open | Light outline pill | #E1F2FF | #1A5490 | Clock |
| On Hold | Dark muted pill | #FFEAA7 | #B7791F | Pause bars |
| In Progress | Blue fill pill | #B3D9FF | #003D82 | Play triangle |
| Complete | Green fill pill | #ddeee2 | #3f4a47 | Filled circle |
| Cancelled | Plain text | transparent | #6c757d | X circle |

## Model status

| Status | Treatment | Background | Text | Icon |
|--------|-----------|-----------|------|------|
| Candidate | Light outline pill | #E1F2FF | #1A5490 | Clock |
| Incomplete | Gray fill pill | #E2E8F0 | #4A5568 | Circle-dash |
| Provisional | Blue fill pill | #B3D9FF | #003D82 | Gear |
| Active | Green fill pill | #bbddc5 | #3f4a47 | Play triangle |
| Retired | Light green pill | #ddeee2 | #3f4a47 | Filled circle |
| Cancelled | Plain text | transparent | #6c757d | X circle |

## Savings claims status

| Status | Treatment | Background | Text | Icon |
|--------|-----------|-----------|------|------|
| Forecast | Light outline pill | #E1F2FF | #1A5490 | Chart |
| Provisional | Blue fill pill | #B3D9FF | #003D82 | Gear |
| Final | Green fill pill | #ddeee2 | #3f4a47 | Lock |
| Cancelled | Plain text | transparent | #6c757d | X circle |

## Task status

| Status | Treatment | Background | Text | Icon |
|--------|-----------|-----------|------|------|
| In Progress | Blue fill pill | #B3D9FF | #003D82 | Play triangle |
| Complete | Green fill pill | #ddeee2 | #3f4a47 | Filled circle |

## Semantic color groupings

| Color family | Meaning | Statuses |
|-------------|---------|----------|
| Light blue outline | Available / waiting | Open, Candidate, Forecast |
| Medium blue fill | Active work happening | In Progress, Provisional |
| Green fill | Positive / done | Complete, Active, Final, Retired |
| Yellow/amber | Paused / needs attention | On Hold |
| Gray | Incomplete / neutral | Incomplete |
| Plain text | Terminal / background | All Cancelled states |

## Cross-domain equivalencies

These statuses are functionally equivalent across domains:
- **Complete** (Project) = **Final** (Savings Claims) = **Retired** (Model, for visual treatment)
- **In Progress** (Project/Task) = **Provisional** (Model/Claims)
- **Open** (Project) = **Candidate** (Model) = **Forecast** (Claims)
- **Cancelled** is consistent across all domains (plain text, no pill)

## Implementation notes

- Pills use `border-radius: 4px`, padding `3px 10px`, font-size `11px`, font-weight `600`
- Icons are 14px inline SVGs, placed before the label with 4px gap
- Plain text cancelled states use the same icon style but no background or border
- All pills should use the exact colors specified — do not derive from the semantic palette (error/warning/success) as the pill system has its own color logic
