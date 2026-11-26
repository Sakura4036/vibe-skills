# Project verification

Use the project's existing verification skill and test selection rules first. Locate a project-local `verify-*` through the repository instructions and recognized skill roots. If several apply, use the one for the affected app or component, and clarify only when scope remains ambiguous. Follow the project test commands if a verification skill is unavailable.

## Test tiers

| Tier | Evidence |
| --- | --- |
| L1 · Unit | Deterministic decisions, state transitions, or error mapping in a small scope. |
| L2 · Integration | Real relevant collaborators for transactions, persistence, cache, or integration contracts. In-process HTTP and simulated DOM cover their own boundaries. |
| L3 · API or service end to end | The real network entry in an isolated environment with the dependencies the flow uses. Verify persisted effects separately when relevant. |
| L4 · Browser | The real user path through a browser. Full-stack acceptance uses the intended builds and real backend, with independent checks of persisted state where applicable. |

Match the tier to the guarantee and the repository's names. Prefer existing coverage, adding the smallest missing regression or critical contract check where needed. Assert observable results, rejections, and necessary side effects. Verify actual collection and execution. Report identified target, result, evidence, and blocked or skipped layers separately.

## Create verification

Use pstack's [create-verification-skill](https://github.com/cursor/plugins/tree/main/pstack/skills/create-verification-skill) for the launch, doctor, drive, evidence, and cleanup recipes. Use the feature-map example shipped with that skill.

- Extend the relevant existing verification skill first. For a new one use the project's established skill root, otherwise `.agents/skills/verify-<project>/` for Codex or `.claude/skills/verify-<project>/` for Claude Code. Write a valid `SKILL.md` with a name and description, then confirm the active host can discover it.
- If the upstream skill cannot run, derive those recipes from the project's actual entry points and existing harness. Link each documented flow to its recipe from `features/README.md` or an equivalent index.
- Exercise a representative user flow in an authorized isolated environment. Check the observable outcome, tear down only resources this run created, then confirm the evidence still exists. Exclude credentials and user data from published artifacts. Mark unexecuted recipes as drafts and name any missing prerequisite.

## Maintain verification

Use pstack's [maintain-verification-skill](https://github.com/cursor/plugins/tree/main/pstack/skills/maintain-verification-skill) for a full audit. Check the index against the recipes and drive every mapped feature. For a diff or named feature, use its maintenance checks on the affected recipes only. Report the checked scope and any blocked coverage. If the project has no verification skill, point to `create-verification`.

If the upstream skill cannot run, compare the in-scope recipes with current source and exercise them through the user entry point. Fix proven drift in the verification skill or its helpers, then rerun the corrected recipes. Report a product regression with the observed result and retain its assertion. Verify teardown and evidence after the last drive. Keep corrections local unless the user requested publication.
