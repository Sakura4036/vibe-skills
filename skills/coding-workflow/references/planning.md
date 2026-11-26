# Local specifications and plans

Resolve the target repository and read its instructions, current code, relevant tests, and decisions before writing. Use the paths below as defaults and honor the target's path and document-index rules. If a requested path conflicts with a strict project rule, surface the actual conflict and resolve it before writing.

## To spec

Write `docs/vibe/specs/YYYY-MM-DD-<slug>.md`. Use a short topic slug and the user's local date. Update a specified existing spec when the task is a revision. State:

- Problem, current behavior and evidence, goal, and scope.
- User-visible behavior, scenarios, and affected public contracts.
- Relevant constraints, decisions, compatibility, and open questions.
- Observable acceptance criteria with a verification layer for each material behavior.

Distinguish decisions from assumptions. Resolve material open requirements through `grill` when the user wants that discussion. Keep the spec local and link related source, decisions, and tests. Check the final path, links, and content.

## To plan

Build from the accepted spec or decisions and inspect the actual implementation and verification entrances. Use a staged tree even for one task.

```text
docs/vibe/plans/YYYY-MM-DD-<slug>/
  00-index.md
  01-<stage>/
    00-index.md
    01-task-<task>.md
```

- **Root index.** Link the spec if present. Record goals, non-goals, current evidence, target design, constraints, stage order and dependencies, file ownership, verification strategy, and requirement coverage.
- **Stage index.** Record its goal and scope, prerequisites, ordered tasks and file ownership, predecessor and successor stages, checkpoint, and exit criteria. Link to the task files.
- **Task.** Describe one independently verifiable slice. Name required files or interfaces, ordered steps, relevant compatibility and failure paths, exact available test commands with the expected result, and a reviewable stopping point. Record a missing test prerequisite explicitly.

Verify structure, required content, links, and traceability to acceptance criteria. Keep writes local. A separate implementation request is the entry to executing the plan.
