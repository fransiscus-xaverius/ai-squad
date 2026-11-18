# <TITLE> — Frontend Design Doc

- **Title:** <title>
- **Date:** <YYYY-MM-DD>
- **Status:** `draft | in-review | approved`
- **Author/role:** designer-ui-ux
- **Session:** <session-id>
- **Surfaces in scope:**
- **Related artifacts:** `tech-notes/<session-id>/{implementation-plan,tech-spec}.md`

## 1. Product and flow context
- The job the user is doing here:
- Data involved (entities, states, volumes):
- Entry point → steps → outcome → error/recovery:
- Who else touches this data:

## 2. Direction
- Direction in one sentence:
- The default we deliberately did **not** take:
- Why this direction fits this product (one sentence, from a product fact):

## 3. Rules applied
- `design-principles` rules satisfied:
- Rules intentionally broken (rule → reason):
- `antialgorithm` notes (default avoided, visual method used):
- `ui-ux-pro-max` checks performed (accessibility, layout, animation, forms, nav):

## 4. Tokens
| Role | Value | Notes |
|---|---|---|
| Color roles (background/surface/foreground/muted/primary/accent/border/danger/success) |  |  |
| Type scale (display/heading/body/caption) |  |  |
| Spacing scale |  |  |
| Radii / elevation / borders |  |  |
| Motion (durations/easings) |  |  |
| Icon set |  |  |

- Token source of truth (file/system) and deviations:

## 5. Fonts
| Family | Weights | Source (self-hosted/CDN/system) | License note | Fallback stack | Loading notes |
|---|---|---|---|---|---|
|  |  |  |  |  |  |

- Preload/`font-display`/subsetting notes:

## 6. Libraries and CSS
| Kind | Name | Version | Path / CDN | Why it is here | Engineer action (port / replace / drop) |
|---|---|---|---|---|---|
| Library |  |  |  |  |  |
| Custom CSS |  |  |  |  |  |

- Project styling system integration points (which existing tokens/components to reuse):

## 7. Prototype files
| Prototype file | Purpose | Screen/state shown | How to open | What to copy from it |
|---|---|---|---|---|
| `prototypes/<surface>.html` |  |  | open in a browser |  |

- Prototype caveats (dependency-light, reference only, not production code):
- Prototypes are local-only by default (excluded from version control via `.gitignore`); list every file here so the work is reproducible and can be shared deliberately with `git add -f <path>`:

## 8. Surface specs
| Surface | Purpose / primary question | Layout | Hierarchy | Primary CTA | States covered |
|---|---|---|---|---|---|
|  |  |  |  |  | loading/empty/error/success/disabled/permission |

### Copy
| Surface | Headline | Supporting text | Button labels | Notes (specific, no filler) |
|---|---|---|---|---|
|  |  |  |  |  |

## 9. Mobile-first behavior
- Narrow layout (320–375px) — what it looks like:
- Breakpoints and what changes at each:
- Tap targets (≥44×44px) and spacing:
- Navigation/structure at small width:
- Safe areas / notch handling:
- Primary action reachable at 375px without scrolling:

## 10. Accessibility
| Item | Requirement | Verified (how) | Result |
|---|---|---|---|
| Text contrast (body/large/secondary) | ≥ 4.5:1 / ≥ 3:1 |  |  |
| Keyboard order and focus visibility |  |  |  |
| Icon-only control labels |  |  |  |
| Touch target sizes | ≥ 44×44px |  |  |
| Reflow / zoom / text scaling |  |  |  |
| Reduced motion |  |  |  |

## 11. Interaction and motion
| Interaction | What it communicates | Duration/easing | Reduced-motion fallback |
|---|---|---|---|
|  |  |  |  |

## 12. QA notes
- `data-testid` suggestions for QA-critical flows:
- Flows to verify and expected outcomes:
- Prototype references for expected look/behavior:
- Known gaps (what could not be verified in this environment):

## 13. Change log
| Date | Change | Impact (what depends on it) | Approved by |
|---|---|---|---|
|  |  |  |  |

## 14. Open questions and assumptions
- Assumptions (and what would invalidate them):
- Questions for technical lead / product:
- Deviations from the spec/plan (and who approved):
