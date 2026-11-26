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

1. Inspect the repo's entry points, start and test commands, owned dependencies, fixtures, and CI. Identify how to reach and observe the app's actual user-facing surface (web, API, CLI, or public library entry point). Reuse its harness, scripts, and selectors. Ask for essential inputs the repo cannot establish.
2. Locate an existing suitable verification skill first. Extend it where needed. Otherwise create `.agents/skills/verify-<project>/SKILL.md` in the target repo with valid name and description. Honor the repo's established skill location if different. Record:
   - **Launch and readiness.** Exact command and directory, required isolated resources, migrations or seeds where applicable, and a ready check for the actual use case.
   - **Doctor.** A read-only check of the intended build, instance, and required dependencies before driving it.
   - **Drive and evidence.** Reusable commands for the normal user entry point, expected states, evidence path, and any independent observable side effects. Index key feature recipes when more than one needs documentation.
   - **Cleanup.** Remove only processes and data owned by the run. Keep evidence and exclude credentials or user data from published artifacts.
3. Run a representative smoke through the real entry point when an isolated environment is available and authorized. Check expected outcome and cleanup. Record unmet prerequisites and which checks remain unverified when startup or access is blocked. Add a helper only if existing commands cannot express a repeated task.

## Maintain verification

Use the relevant diff or changed feature list to scope maintenance. Read the current source, existing recipe, test runner, and environment configuration. Recheck setup commands, selectors, data, assertions, and evidence only where they can be affected. Keep unrelated recipes stable.

Drive affected recipes through the real entry point when possible. Distinguish a stale recipe, a harness or environment failure, and a genuine product regression. Update the verification skill and helpers it owns for proven documentation or harness drift. Report product regressions for the implementation scope to address. Rerun updated recipes, preserve evidence, and verify teardown. Report the result and any unavailable coverage.

Inspired by pstack's [create-verification-skill](https://github.com/cursor/plugins/blob/main/pstack/skills/create-verification-skill/SKILL.md) and [maintain-verification-skill](https://github.com/cursor/plugins/blob/main/pstack/skills/maintain-verification-skill/SKILL.md).
