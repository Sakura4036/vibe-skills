# Development commands

Use the installed specialist named below. Follow the active host's skill invocation policy. Consult the installed instructions as reference when the host permits it. If invocation requires the user, use the local steps below and identify which specialist did not run. A missing skill can be reported without installing it during ordinary work.

## Repeat and grill

- **Repeat.** Use pstack’s `in-your-own-words` when available. In your own words, state the problem, intended result, constraints, and observable acceptance. For an explicit `repeat`, wait for the user's confirmation before changing anything. In ordinary implementation, proceed on a clear request and confirm material ambiguity before committing to a solution.
- **Grill.** Use Matt Pocock's `grilling`. Resolve facts from code first and bring the user the decisions that remain. Record the settled outcome in the conversation or the requested artifact.

## TDD and implement

- **TDD.** Use Matt's `tdd`. Read the repo's existing verification skill and [L1–L4 test rules](verification.md#test-tiers). Prefer public seams and a repeatable failing case. Implement the smallest behavior, rerun the same case, and keep listed checks green while simplifying.
- **Implement.** Use Matt's `implement` for the agreed spec, plan, or user request. Proceed in independently verifiable slices through normal entry points. Keep the repo's test scope and gates, run the actual relevant checks, and report unverified layers. Commit, push, create a PR, or deploy within the authorized scope.

## Review, PR, and unslop

- **Review.** Use Matt's `code-review`. Determine the requested comparison and spec. For current edits, account for relevant staged and unstaged changes and new files. For a branch or PR, verify the base. Review standards and intended behavior, and return actionable findings with evidence. When a change affects a shared contract, also trace a consumer outside the diff and test the assumption its compatibility depends on. Use pstack’s `blast-radius` for an explicit impact review when available. Apply fixes when the user requests them.
- **PR.** Use Matt's `pr`. Verify the target, base and compare refs, diff, and test evidence. Draft a concise description with the user-visible change, evidence, and rollout concerns where applicable. Open or update the PR when the user authorizes delivery.
- **Unslop.** Use pstack's `unslop` if available. Preserve facts, claims, uncertainty, voice, terminology, and citations. Cut filler and artificial phrasing, keep concrete details, and check the rewrite against the source. Preserve the requested output format.

Sources. [Matt Pocock engineering skills](https://github.com/mattpocock/skills/tree/main/skills/engineering), [pstack in-your-own-words](https://github.com/cursor/plugins/blob/main/pstack/skills/in-your-own-words/SKILL.md), [pstack unslop](https://github.com/cursor/plugins/blob/main/pstack/skills/unslop/SKILL.md).
