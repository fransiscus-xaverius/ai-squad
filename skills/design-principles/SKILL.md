---
name: Design Principles
description: Project design rules for interface work - kill redundant badges and labels, use one design system, group with spacing, sharpen hierarchy and CTAs, fix contrast, wrapping, alignment, numbers, loading, motion, and mobile-first layout
---

# Design Principles

The project's own interface rules. Apply to any UI work — new screens, components, redesigns, or review findings — together with `ui-ux-pro-max` (breadth, accessibility and checklists) and `antialgorithm` (taste and defaults). Where a rule conflicts with an explicit user instruction, the user wins; record the conflict.

## Framework alignment
- Follow `README.md` workflow, `harness/engineering-harness.md`, `core/artifacts.md`, and `frontend-node` (implementation), `qa-playwright` (verification).
- These rules are reviewable: state which rules the work satisfies and which are intentionally broken (and why) in the design handoff.
- Apply them at design time and in code review; a violation found in implementation goes back through the normal phase/QA loop.

## The rules

### 1. Delete filter badges
Badges that only restate a filter, chip, or tab state ("Active" on the active filter) are noise.
- **Why:** the control already shows its state; the badge adds pixels and competing emphasis.
- **How:** if the badge carries no information not visible elsewhere, remove it; keep badges that carry independent meaning (count, severity, status of a record).
- **Verify:** the filter row reads once, without decoding label-plus-badge pairs.

### 2. Drop redundant labels
A visible label that repeats what the control already communicates (a magnifier plus "Search" label, "Email address" on an `email` input with a placeholder) is dead weight.
- **Why:** redundant labels push content down and slow scanning.
- **How:** keep a visible label when the field could be confused, the placeholder is the only label, or the form has no other structure; otherwise let type, icon, or context carry it.
- **Verify:** no label can be removed without losing meaning.

### 3. Monospace only where needed
Monospace is for code, identifiers, hashes, log output, diffs, and technical values that must align character-by-character.
- **Why:** mono everywhere is a costume of "technical", not a functional need; it hurts readability of running text.
- **How:** body/UI text uses the product's text face; mono is scoped to the specific elements listed above.
- **Verify:** no mono font outside those cases.

### 4. Use a design system
One source of truth for color, type scale, spacing, radii, elevation, borders, and motion. Components consume semantic tokens (`--color-surface`, `--space-4`), never raw hex, magic pixel values, or one-off shadows.
- **Why:** a token system is what makes a screen look designed rather than assembled; it also makes review and restyling possible.
- **How:** define/reuse tokens first; add a missing token instead of introducing a parallel value.
- **Verify:** grep the diff for raw color/spacing values — zero outside token definitions.

### 5. Know the actual product from a flow perspective before designing
Before drawing anything: what job does the user come to do, what data exists, what states occur, what comes before and after, who else touches this data.
- **Why:** most bad screens are misread products — the layout answers a question the user does not have.
- **How:** trace the flow (entry point → states → outcome → error/recovery) and list the real states before choosing a layout.
- **Verify:** every designed state maps to a real step in the flow; unused states are dropped.

### 6. Group with spacing
Group related items with space, not with boxes, borders, and shadows.
- **Why:** proximity communicates structure; containers add weight and fight the content.
- **How:** use a consistent spacing scale, with larger gaps between groups than within a group; keep dividers and cards for real separation.
- **Verify:** remove all borders/shadows — if the grouping still reads, spacing is doing the work.

### 7. Enlarge the main feature
The feature the screen exists for gets the size, contrast, and placement it deserves; supporting elements step back.
- **Why:** equal weight on everything means nothing is important.
- **How:** pick the one primary object/action per view and scale it up; demote the rest.
- **Verify:** squint test — the main feature is what remains legible.

### 8. Make headlines specific
Headlines say what this is about: "Invoices unpaid since March", not "Overview" or "Welcome".
- **Why:** specific headlines let the user decide to keep reading before investing attention.
- **How:** use real content (counts, names, dates, states) or a concrete verb; delete greetings and category labels.
- **Verify:** no headline could be swapped with another screen's headline unchanged.

### 9. Emphasize the CTA
One primary call to action per view or section, visually dominant and worded as the action itself ("Create invoice", not "Submit").
- **Why:** competing or vague CTAs stall the decision.
- **How:** style the primary action distinctly, keep secondary actions visually quiet, and place the CTA where the flow reaches it.
- **Verify:** a first-time viewer can name the next action without hesitation.

### 10. Add an accent color
One accent, used sparingly, marks what matters (primary action, selected state, key data). The rest stays neutral.
- **Why:** a single accent gives the interface a focal point; many accents give it none.
- **How:** pick one accent that survives light and dark; use it for emphasis, not decoration.
- **Verify:** accent usage is countable, and removing it would lose meaning.

### 11. Keep icons consistent
One icon set, one size grid, one stroke weight and style.
- **Why:** mixed sets and weights read as unfinished.
- **How:** choose one set (e.g. Phosphor/Lucide/Heroicons), standardize size and stroke, and never use emoji as icons.
- **Verify:** all icons trace to the same set; no mixed fills/strokes in one context.

### 12. Remove embellishments
Drop gradients, glows, glass effects, decorative blobs, double shadows, and animated flourishes that carry no meaning.
- **Why:** every effect is attention spent; effects that mean nothing spend the user's attention budget.
- **How:** for each effect ask what it communicates; if the answer is "it looks nice", remove it.
- **Verify:** every remaining effect has a stated purpose.

### 13. Inner radius must be outer − padding
For nested rounded surfaces, the inner radius equals the outer radius minus the padding between them, so the curves stay concentric.
- **Why:** mismatched inner/outer radii break the concentric-curve illusion and look subtly wrong.
- **How:** `inner-radius = outer-radius − padding` (e.g. outer 16px, padding 8px → inner 8px); keep it consistent across nested components.
- **Verify:** no nested surface shows non-concentric corners.

### 14. Improve text contrast
Body text ≥ 4.5:1 against its background; large text ≥ 3:1; never gray-on-gray; disabled/placeholder text stays legible.
- **Why:** low contrast text is the most common accessibility failure and is invisible to designers looking at their own screen.
- **How:** compute contrast for every text/background pair, including hover, active, disabled, and dark-mode states.
- **Verify:** ratios are recorded in the handoff; secondary text is not decorative gray.

### 15. Wrap headlines properly
Headlines wrap deliberately: balanced lines, no orphans, no one-word last lines, and no hard-coded breaks that break at other widths.
- **Why:** ragged wrapping looks unconsidered and shifts the perceived hierarchy.
- **How:** use balance/pretty wrapping (`text-wrap: balance` / `pretty`) plus sensible max widths; avoid manual `<br>` as a substitute for responsive behavior.
- **Verify:** check wrapping at 320/375/768/1024px and with enlarged text.

### 16. Align by eye, not pixels
Optical alignment beats mathematical alignment.
- **Why:** identical pixel offsets look misaligned when shapes differ (round vs square, icon vs text, cap height vs x-height).
- **How:** align by perceived edge — nudge optically, match cap heights, and center icons on the text's optical center rather than its box.
- **Verify:** check alignment at 100% zoom with squinted eyes; a 1px nudge often fixes what a rule cannot.

### 17. Use tabular numerals
Numbers in tables, lists, prices, timers, and counters use tabular figures so digits occupy equal width.
- **Why:** proportional digits cause columns to shimmer and totals to look misaligned.
- **How:** `font-variant-numeric: tabular-nums` on numeric contexts; keep prose numbers proportional.
- **Verify:** digit columns line up when values change.

### 18. Add loading states
Every async surface designs its loading, empty, error, and success states — no spinners invented in code.
- **Why:** loading is a state users experience on every visit; unreserved space causes layout jump.
- **How:** skeletons that match final content shape (or an inline progress indicator), reserved space to prevent CLS, and a real empty state (not a blank panel).
- **Verify:** loading → content transition does not shift layout (CLS stays near zero).

### 19. Animate useful feedback
Motion explains change and state — what happened, where to look, what is now available.
- **Why:** decoration-only animation delays the interface and annoys repeat users.
- **How:** short and purposeful durations (fast for micro-feedback, slower for entrances), exit faster than enter, animate transform/opacity rather than layout properties, and honor `prefers-reduced-motion`.
- **Verify:** every animation answers "what does this tell me?"; with reduced motion enabled, no information is lost.

### 20. Design mobile-first
Every screen is designed for a phone first and then scaled up — never a desktop layout squeezed down to fit a narrow screen.
- **Why:** mobile is the tightest constraint (width, thumb reach, touch accuracy, slower networks). A design that only works at 1440px breaks on the device most people actually hold.
- **How:** specify the narrow layout first (375px, and 320px for small phones), then add breakpoints upward; touch targets ≥ 44×44px with ≥ 8px spacing; never depend on hover — provide focus/press equivalents; keep the primary action and essential content above the fold on a phone; stack content in a sensible reading order; respect safe areas (notch, home indicator); keep inputs at ≥ 16px so mobile browsers do not zoom on focus; assume a slow network.
- **Verify:** check 320 / 375 / 768 / 1024 / 1440px with no horizontal scroll, no clipped or overlapping controls, no hover-only affordances, sized tap targets, and the primary action reachable without scrolling on 375px.

## Self-check before handing off
1. Which rules does this design satisfy? Which are intentionally broken, and why?
2. Contrast ratios, focus visibility, reduced-motion behavior, and responsive widths: verified or explicitly unverified?
3. Are the loading, empty, error, and success states of every async surface specified?
4. Does the design come from this product's flow (rule 5), or from a default shell (`antialgorithm`)?
5. Are tokens used everywhere, with zero raw values in the diff?
6. Does the mobile-first layout (rule 20) hold at 320/375px, with tap targets sized and the primary action reachable?

## References
- WCAG 2.2 (W3C) — contrast and target size: https://www.w3.org/TR/WCAG22/
- MDN, `border-radius` (nested radius): https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius
- MDN, `font-variant-numeric` (tabular figures): https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-numeric
- MDN, `text-wrap` (balance/pretty): https://developer.mozilla.org/en-US/docs/Web/CSS/text-wrap
- MDN, `prefers-reduced-motion`: https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion
- web.dev, *Cumulative Layout Shift*: https://web.dev/articles/cls
- Apple Human Interface Guidelines (tap targets, alignment): https://developer.apple.com/design/human-interface-guidelines/
- Material Design 3 (tap targets, type scale): https://m3.material.io/
- Framework skills: `ui-ux-pro-max`, `antialgorithm`, `frontend-node`, `qa-playwright`
