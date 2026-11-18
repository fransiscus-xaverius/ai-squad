---
name: Finishing a Development Branch
description: Complete implementation work with verified tests/evidence, finalized artifacts, and an explicit integration/closeout decision
---

# Finishing a Development Branch

Use when implementation reaches completion or a defined stopping point and requires safe closeout.

## Steps
1. **Verify state and evidence**
   - Run relevant checks/tests and confirm fresh evidence (`verification-before-completion`).
   - Ensure required QA verdicts/review outcomes for scope are recorded (or blockers/gaps explicitly documented).
2. **Finalize artifacts**
   - Update `implementation-state.md`, `feature-list.json`, `progress.md`, QA results/evidence, review artifacts, and tech notes with status, decisions, risks, and follow-ups.
3. **Confirm integration context**
   - Confirm repo/branch/worktree, base vs working branch, and any uncommitted/unmerged work.
4. **Choose and execute closeout path (with approvals as needed)**
   - Merge locally, push/create PR, keep branch/worktree for follow-up, or pause/escalate.
   - Respect environment capabilities and human decisions.
5. **Cleanup safely (only when appropriate)**
   - Remove temporary worktrees/branches only if safe, no unpreserved work, and explicitly approved when destructive/ambiguous.

## Guardrails
- Never claim done/ready without evidence and finalized state.
- No irreversible actions (force push, deleting work with risk) without explicit confirmation.
- Record integration outcome, remaining risks, and exact next actions.

## References
- Superpowers, *Finishing a Development Branch*: https://github.com/obra/superpowers
- Git worktree/branch basics: https://git-scm.com/docs
- Framework: `verification-before-completion`, `artifact-state`, `harness/engineering-harness.md`
