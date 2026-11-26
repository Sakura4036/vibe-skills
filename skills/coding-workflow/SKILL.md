---
name: coding-workflow
description: "Use my coding workflow to prepare repositories, clarify a task, plan changes, implement features or bug fixes, verify behavior, review a diff, or polish prose. Accepts setup, repeat, grill, to-spec, to-plan, create-verification, maintain-verification, tdd, implement, pr, review, unslop, and auto as commands after the skill name. With no command, choose the shortest workflow that fits the request."
---

# Coding workflow

Use a named command when the user requests it as the first argument, such as `$coding-workflow setup`. Otherwise use `auto`. If the user explicitly requests an unknown command, show the supported names and ask what they meant.

| Command | Action |
| --- | --- |
| `setup` | [Discover project facts, install missing companions, fill the root guide, and set up Matt's repo configuration](references/setup.md). Run on explicit request. |
| `repeat` | [Restate the goal and wait for confirmation](references/development.md#repeat-and-grill). |
| `grill` | [Use Matt Pocock's `grilling` to settle open decisions](references/development.md#repeat-and-grill). |
| `to-spec` | [Write a local specification](references/planning.md#to-spec). |
| `to-plan` | [Write a staged local plan](references/planning.md#to-plan). |
| `create-verification` | [Create or complete a repository-local verification skill](references/verification.md#create-verification). |
| `maintain-verification` | [Check and update affected verification instructions or helpers](references/verification.md#maintain-verification). |
| `tdd` | [Use Matt's `tdd` with the project's verification skill and test tiers](references/development.md#tdd-and-implement). |
| `implement` | [Use Matt's `implement` for an agreed change](references/development.md#tdd-and-implement). |
| `pr` | [Use Matt's `pr` to draft the description](references/development.md#review-pr-and-unslop). |
| `review` | [Use Matt's `code-review` to check standards and intent](references/development.md#review-pr-and-unslop). |
| `unslop` | [Edit prose with pstack's `unslop` approach](references/development.md#review-pr-and-unslop). |
| `auto` | Choose a route below. |

## Auto

- A clear local change goes straight to the smallest verifiable patch. For a hard bug, flake, or performance regression, use `diagnosing-bugs` to create a repeatable failing signal, then fix and rerun it. Add `tdd` when the user asks or a real regression or material risk needs a test.
- A design question with material open decisions can use `grill`. An agreed multi-step change can use `implement` and a short checked plan. Write spec or plan files when the task or local workflow calls for them.
- Route review, PR drafting, and prose edits to their commands. For a standalone question, answer from evidence at the requested scope.
- Treat setup, dependency installation, and verification initialization as explicit actions. Follow the requested scope for tracker writes, commits, pushes, PR creation, and release. Match a specialist to the current phase and continue with the compatible local steps if the host cannot invoke it.

## Before changing a project

Read the nearest applicable repository instructions, current code, callers, and tests. Consult both sides of a shared contract. State assumptions that can change the result. Preserve staged, unstaged, and untracked work. Use the current checkout by default. If a worktree is requested, prefer `.wt/` inside the repository unless a different location is specified.

Change the behavior in its owning module. Prefer an existing function, type, or file and keep unrelated cleanup out of the diff. Preserve existing callers and data unless a contract change is in scope. For writes, keep related checks and updates under one transaction owner where applicable, with external I/O outside the transaction. Account for partial failure, concurrency, and retry when they affect the result.

Use the [verification rules](references/verification.md#test-tiers) to pick the lowest-cost test that observes the guarantee. Verify actual collection and execution at the affected entry point. Review the final diff and report what changed, which checks ran, and which layers remain unverified.
