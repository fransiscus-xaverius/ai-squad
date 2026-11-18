---
name: Anti-Algorithm Taste
description: Avoid the safe, average first answer when a creative choice is open (visual style, layout, color, copy, naming, interface concept) and replace it with a choice specific to the actual product
---

# Anti-Algorithm Taste

Use when a creative decision is genuinely open: visual direction, layout concept, palette, interface concept, copy, naming, page structure, motion character. Skip when the user already decided, for code identifiers, bug fixes, or formats fixed by standing rules (commit messages, license text, release notes). Also skip when the user asks for the standard/expected version — give it then.

Adapted from `mankidev/antialgorithm` (MIT) and `nextlevelbuilder/ui-ux-pro-max-skill` (MIT).

## Framework alignment
- Follow `README.md` workflow, `harness/engineering-harness.md`, `core/artifacts.md`, and `design-principles` (the project's own rules always win over this skill).
- This skill changes *how the choice is made*, not what the workflow requires: no design moves past the plan/approval gates, and every decision still needs a reason plus evidence.
- Record the direction chosen and the rejected default in the design handoff so the choice is reviewable and reversible.

## The core move: find the default, then leave it
1. **Name the default out loud:** "the default here is X" (one line). Do not use X unless the context genuinely demands it.
2. **Move using what is specific to this case:** the product, its users, its constraints, its world, its odd details. A good choice could only belong here; a default choice could belong anywhere.
3. **Do not swap one cliché for its famous opposite** ("dark instead of bright", "minimal instead of busy") — that is the second-most-common answer, not a choice.
4. **Odd is not the goal.** A strange choice with no reason is as empty as a safe one. Every choice gets a one-sentence reason grounded in a fact about this project.

## Start from outside your own taste
The first idea that arrives is the average of everything already made. Start elsewhere:
- If the request carries real context (product, place, audience, purpose, constraint), start from that.
- If context is thin and the work is small, make the work from a stated seed or guess, then ask **one** short question at the end that would make it fit better (a fact about the case, not permission to redo the work).
- If context is thin and the work is large or costly (a full design), ask **one** short question first: who it is for, where it lives, what it is about.
- Never pick the starting point by asking what would be most interesting — that lands on the same place for everyone.

## Visual direction
- **Pick the look from the subject:** its material, place, time, and mood. One strong decision leads; the rest serve it.
- **Avoid the default finish:** smooth gradients, soft glow, perfect geometry, tiles that repeat with no change, clean edges everywhere, even spacing, one default font, uniform polish on every part. This finish is what makes generated work recognizable.
- **Give the piece a method with real marks:** print/paint (few inks, uneven ink, broken edges, paper grain), screens/machines (pixel or dot grid, scan lines, bloom, banding, machine type), camera/science (sensor grain, falloff, motion blur, instrument false color), material/light (seams, joints, thickness, light behaving like that material). Marks must be sparse and real, not a noise filter over a clean image.
- **Do not fake a method the subject does not have** (hand-drawn wobble on an LED board is a second default on top of the first).
- **Leave out what has no job:** decorative shapes, glows, frames, or icons that only fill space are signs of the default.
- Do not invent a texture that fights readability; the parts that must work stay whole, clear, and in place.

## Interfaces (the default shell is the tell)
A screen has a default shell: top bar with search/bell/avatar, sidebar, row of stat cards, rounded panels in a grid, chips, progress bars, table, one accent color on a dark or white ground. A new subject poured into that shell still reads as a template. Change **all three layers**, not one:
1. **Layout from the subject:** find the one question the user opens this screen to answer, and let the page be the shape of that answer (a schedule app can be the day itself; a tool about a place can be the place). Cards/tables/panels return only when this case needs them.
2. **A method that carries the data:** let the method show the states — light/dark, ink/paper, worn/new, on/off. If a state could be swapped for any color without losing meaning, the method is only paint.
3. **Type and color at poster scale:** one strong statement with small exact data beside it. Colors mean something (the hour, the zone, the state) rather than one accent on gray.

**The method never owns the working parts:** data aligns with its axis, labels sit inside their areas, buttons stay plain and pressable, small text stays readable. Roughness goes behind or below the data, never through it.

## Copy and naming
- Write only what this writer would write about this subject; if a sentence could be pasted into another project unchanged, rewrite it.
- Prefer the concrete detail over the general claim; the plain word over the impressive one; the unexpected-but-true angle over the expected summary.
- Do not use the default marks of generated copy: an offer to redo/tailor at the end, unrequested bold titles/headers, bullet feature lists where sentences would do, a closing CTA or cheer with an exclamation mark, a hype question to the reader, mirrored slogan pairs, items in threes by habit, set phrases that fit any product, named feelings where a detail could show them, a last line that summarizes or ties a bow, and long even sentences with one rhythm.
- Do not offer the most famous mechanic/name or a name built from the two most obvious words. When offering options, make them **different in kind**, not small variations of one safe idea; give one recommendation with the reason.
- Keep the length, format, and language the user set. Do not invent facts to make copy concrete — use real project details or ask; flag any made-up detail that could pass for real and cause harm (price, weight, claim).
- Write in the language the user wrote in, unless the project's standing rules say otherwise.

## Watch your escapes becoming defaults
An off-default move becomes the new safe pick if repeated. Avoid the recurring escape patterns: an analog/printed look chosen because it reads "not AI"; the same small palette/paper/texture/wobbly line every time; stock name material (sea and tide words, old trades, rope and salt, small English towns); a cream/beige/off-white ground taken from habit instead of the subject; precise times/dates/numbers used only to look concrete; a clever borrowed frame (table, map, form, schedule) laid over the subject; a small numbered corner label and a dry joke in fine print; a quiet magic rule or odd object in the last line.
- Keep a record of the main move of each accepted direction (a few plain words) so repeats are visible; upstream tooling for this lives in `mankidev/antialgorithm` (`scripts/moves.py`) and is optional.

## Check before showing
1. Could this answer belong to a different project? If yes, it is too general.
2. Is this what most people would make first? If yes, move it.
3. Can you say in one sentence, using a fact about this project, why this choice fits here? If not, the choice has no reason.

## References
- Upstream skill (MIT, adapted): https://github.com/mankidev/antialgorithm — `SKILL.md` and `visuals.md`
- UI/UX Pro Max skill (MIT, adapted, complementary): https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
- Framework skills: `design-principles`, `ui-ux-pro-max`, `blast-radius` (design changes ripple across screens)
