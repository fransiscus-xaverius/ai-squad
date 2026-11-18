---
name: UI/UX Pro Max
description: Structured UI/UX design intelligence for web, mobile, and desktop — product-type reasoning, palettes, typography, style, UX rules, accessibility, responsive layout, and a pre-delivery checklist
---

# UI/UX Pro Max

Use for UI structure and quality work: new pages, components, design systems, visual direction, interaction patterns, accessibility, responsive layout, typography, color, charts, and UI review. Skip for pure backend/API/database/infra work or non-visual performance tasks — unless the change affects how the interface looks, feels, moves, or is interacted with.

Adapted from `nextlevelbuilder/ui-ux-pro-max-skill` (MIT).

## Framework alignment
- Follow `README.md` workflow, `harness/engineering-harness.md`, `core/artifacts.md`, and `design-principles` + `antialgorithm` (this skill supplies breadth and checklists; those two supply taste and house rules).
- The designer's output is the frontend design doc (`tech-notes/<session-id>/<title>-<date>-design.md`) plus its `prototypes/*.html`; tokens, fonts, libraries/CSS, states, and interaction notes must be implementable by the frontend engineer and checkable by QA.
- Verify what you claim: contrast ratios, focus visibility, responsive behavior, and reduced-motion handling are verifiable facts — do not assert them without a check.

## Rule categories by priority
Focus on the highest-priority category that the task actually touches:

| # | Category | Impact | Must have | Avoid |
|---|---|---|---|---|
| 1 | Accessibility | critical | contrast ≥ 4.5:1 body text, alt text, keyboard navigation, labels on icon-only controls | removing focus rings, unlabeled icon buttons |
| 2 | Touch & interaction | critical | ≥ 44×44px targets, ≥ 8px spacing, visible loading feedback | hover-only affordances, instant (0ms) state changes |
| 3 | Performance | high | modern image formats, lazy loading, reserved space (CLS < 0.1) | layout thrashing, cumulative layout shift |
| 4 | Style selection | high | match product type, consistent style, SVG icons | mixing flat and skeuomorphic, emoji as icons |
| 5 | Layout & responsive | high | mobile-first breakpoints, viewport meta, no horizontal scroll | fixed-px containers, disabled zoom |
| 6 | Typography & color | medium | 16px base, 1.5 line-height, semantic color tokens | body text < 12px, gray-on-gray, raw hex in components |
| 7 | Animation | medium | timing matched to context, motion carries meaning, spatial continuity | one duration for everything, animating width/height, ignoring reduced motion |
| 8 | Forms & feedback | medium | visible labels, error next to the field, helper text, progressive disclosure | placeholder-only labels, errors only at the top, upfront overload |
| 9 | Navigation | high | predictable back behavior, ≤ 5 bottom-nav items, deep links | overloaded nav, broken back, no deep links |
| 10 | Charts & data | low | legends, tooltips, accessible color pairs | conveying meaning by color alone |

## Search-driven design intelligence (optional tool)
The upstream project ships a searchable local catalog (styles, product reasoning profiles, palettes, typography pairings, UX guidelines, icons, charts, stacks) queried with a Python 3 script (`search.py`, installed via the `ui-ux-pro-max-cli` npm package). **Use it when present; it is optional.**

```bash
# new page / product-wide direction
python3 <skill-dir>/scripts/search.py "<product> <industry> <keywords>" --design-system -p "Project Name"
# one focused concern
python3 <skill-dir>/scripts/search.py "error summary validation" --domain ux
# implementation guidance for the real stack
python3 <skill-dir>/scripts/search.py "form validation" --stack react
```

Query contract:
- One dominant intent, 2–5 meaningful terms, plus one constraint (product, platform, interaction).
- `--design-system` for a new page or system-wide direction; a single `--domain` for a focused concern; `--stack` for the detected stack (detect it from the repo — `package.json`, `pubspec.yaml`, `*.xcodeproj`, `composer.json`, `app.json` — never assume one).
- If a search returns nothing: retry **once** with a narrower query or an explicit domain/stack. If still empty, fall back to the built-in defaults above and **say the guidance came from defaults, not a catalog match**. Never present an empty search as data, and never persist unverified output.
- Optional dials: `--variance` (centered → bold/asymmetric), `--motion` (subtle → choreographed), `--density` (spacious → dense dashboard).
- Right-to-left interfaces: check `--rtl` levels — `full` mirrors unchanged, `partial` mirrors but needs per-component checks, `caveats` encodes reading direction (say so and offer a mirrorable alternative).

### Persisted design system (master + overrides)
When the tool is available, persist decisions so later work stays consistent:
```
design-system/<project-slug>/MASTER.md      # colors, typography, spacing, components (source of truth)
design-system/<project-slug>/pages/<page>.md # page-specific deviations only
design-system/<project-slug>/preview.html    # static preview
design-system/<project-slug>/tokens.json     # W3C DTCG tokens (optional)
design-system/<project-slug>/tokens.css      # :root custom properties (optional)
```
Read an existing `MASTER.md` before regenerating; never overwrite it without explicit authorization.

## Pre-delivery checklist (run before declaring a design done)
- [ ] No emoji as icons — use a single SVG icon set (Heroicons, Lucide, Phosphor).
- [ ] Clickable elements show a pointer cursor and a visible focus state.
- [ ] Interaction timing matches the platform and component, not one global duration.
- [ ] Light mode body text contrast ≥ 4.5:1; disabled/placeholder text still legible.
- [ ] Keyboard navigation reaches every interactive element; focus is never hidden.
- [ ] `prefers-reduced-motion` is respected; motion is not the only signal of state.
- [ ] Text, chips, and badges reflow without clipping or broken labels at narrow widths, zoom, and text scaling.
- [ ] Responsive verified at 375, 768, 1024, and 1440px with no horizontal scroll.
- [ ] Every async surface has a loading, empty, error, and success state designed (not improvised in code).
- [ ] Badge meaning never relies on color alone; live counts have context.

## Anti-patterns to reject in review
- "AI purple/pink gradient" styling, neon on dark as a default, harsh animation for its own sake.
- Mixing flat and skeuomorphic treatments at random; emoji used as icons; raw hex values and magic spacing inside components.
- Gray-on-gray text, body copy under 12px, one duration for all transitions, animating `width`/`height`.
- Placeholder-only labels, validation errors only at the top of a form, wall-of-options disclosure.
- Default dashboard shell (top bar + sidebar + stat-card row + grid of rounded panels) applied without reason — see `antialgorithm`.

## Verification expectations
- Contrast: compute ratios for text/background pairs and record them.
- Responsive/reflow: exercise narrow widths (and zoom/text scaling) before calling a layout done.
- Interaction: verify focus order, keyboard operation, and reduced-motion behavior.
- For browser-checkable items, hand them to QA as explicit cases with expected outcomes (`qa-playwright`, `qa-agent`); if the app cannot run, report the design item as unverified rather than passed.

## References
- Upstream project (MIT, adapted): https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
- Upstream docs site: https://www.uupm.cc/
- WCAG 2.2 Quick Reference (W3C WAI): https://www.w3.org/WAI/WCAG22/quickref/
- MDN Web Accessibility: https://developer.mozilla.org/en-US/docs/Web/Accessibility
- web.dev Learn Accessibility: https://web.dev/learn/accessibility
- Design tokens (W3C DTCG): https://www.designtokens.org/
- Framework skills: `design-principles`, `antialgorithm`, `frontend-node`, `qa-playwright`
