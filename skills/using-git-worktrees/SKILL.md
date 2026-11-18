---
name: Using Git Worktrees
description: Set up or recognize an isolated workspace/branch for implementation work safely, with baseline verification and clean handoff
---

# Using Git Worktrees

Use when work should be isolated in a separate branch/worktree or when confirming a safe workspace for phased execution.

## Detect before creating
- Confirm repo root, current branch, and whether already in an appropriate isolated worktree.
- Respect confirmed repo/directory, base branch, and working branch from intake/PRD; do not guess or switch implicitly.
- Check for uncommitted changes and existing worktree state before actions.

## Isolation approach
1. Prefer provider/environment-supported isolation mechanisms when available and approved.
2. For git worktrees: choose a clear path/name aligned with project practice, ensure target branch/base is correct, and keep worktree directories out of commits as appropriate.
3. If isolation cannot be created safely, report limitation, proceed only with explicit approval in the confirmed workspace, and record constraint in `implementation-state.md`.

## Baseline and safety
- Run required setup and establish baseline (install/build/lint/tests/smoke as relevant) before changes; record commands/results.
- Do not attribute pre-existing failures to new work without evidence.
- **No destructive git operations** (delete branches/worktrees with unmerged/uncommitted risk, force reset/push, discard changes) without explicit confirmation (`autonomy-with-gates`).
- Keep commits/checkpoints descriptive and aligned to verified increments when used (subject to policy).

## Recording
- Document workspace/branch/worktree decisions, baseline status, and any limitations in artifacts (`implementation-state.md`, `progress.md`).
- Apply `verification-before-completion` before claiming setup/readiness.

## References
- Git documentation (worktree): https://git-scm.com/docs/git-worktree
- Superpowers, *Using Git Worktrees* (isolation/baseline pattern): https://github.com/obra/superpowers
- Framework: `harness/session-lifecycle.md`, `autonomy-with-gates`
