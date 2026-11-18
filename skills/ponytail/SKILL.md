---
name: Ponytail
description: Lazy senior dev mode - smallest complete change that solves the task with minimal bloat. Use for implementation and planning decisions; prioritize reuse, deletion, and verifiable simplicity
---

# Ponytail (Smallest Complete Change)

Default to the **simplest correct, verifiable solution** that satisfies the approved scope.

## Principles
- **Smallest complete change:** solve the stated problem end-to-end without speculative features or abstractions.
- **Reuse before adding:** prefer existing patterns, utilities, modules, and conventions in the codebase.
- **Subtract before adding:** remove dead/duplicate paths when safe and in scope before introducing new complexity.
- **Local, reversible edits:** minimize blast radius; isolate changes to what is necessary.
- **Evidence over elegance claims:** verify behavior with relevant checks/tests.

## Apply in practice
- Implement only acceptance criteria and required supporting work.
- Avoid premature generalization, unnecessary dependencies, and broad refactors unless required/approved.
- Prefer clear naming/structure and explicit contracts over cleverness.
- When tradeoffs exist, choose the option with lowest risk and complexity that meets requirements; record rationale if material.

## Framework alignment
- Works with `phase-execution`, `architect`, `boundary-discipline`, `correct`, and `verification-before-completion`.
- Does not override gates, required QA/review, evidence, or safety/compatibility constraints.

## References
- Anthropic, *Building effective agents* (start simple, add complexity only when needed): https://www.anthropic.com/engineering/building-effective-agents
- pstack simplicity/subtraction principles (adapted): https://github.com/cursor/plugins
- Go proverb/context: "Clear is better than clever" (idiomatic design influence)
