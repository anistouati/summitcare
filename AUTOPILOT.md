# SummitCare Codex Autopilot

Use this as the single entrypoint for a Codex session.

## Objective
Advance `ROADMAP.md` one coherent item at a time without requiring feature-by-feature human prompts.

## Execution loop
1. Read `AGENTS.md`, `ROADMAP.md`, relevant code/tests and any nested AGENTS.md.
2. Select the first unblocked `TODO` item by priority/dependency order.
3. Mark only that item `IN_PROGRESS` in the working tree.
4. Use `summitcare-architect` for cross-cutting/domain analysis.
5. Delegate backend and frontend work to non-overlapping file areas.
6. Use `summitcare-security-qa` after implementation for independent acceptance/security verification.
7. Run all relevant builds/tests.
8. Mark the item `DONE` only if every acceptance criterion passes; otherwise leave `IN_PROGRESS`/`BLOCKED` with the exact reason.
9. Stop after one coherent item unless the next item is clearly independent and the parent session has sufficient context.

## Guardrails
- Never replace or break root `index.html` unless the selected roadmap item explicitly requires landing-page work.
- Never weaken authorization to make a test pass.
- Never silently change referral-attribution or commission semantics.
- Never add medical diagnosis/treatment behavior.
- Never autonomously execute payouts or financial transfers.

## Suggested invocation
```bash
codex "Read AUTOPILOT.md and advance the SummitCare roadmap. Use subagents where useful."
```
