# Coding agent guide

## Repository setup

Fill in this table when adopting the guide. Use repository-relative paths and commands that work from the stated directory. For blank entries, consult the repository's checked-in configuration and CI.

| Find | Repository entry |
| --- | --- |
| Runtime, package manager, install | <!-- Version file, lockfile, install command --> |
| Module owners, API contracts, decisions | <!-- Handbook, schemas, architecture decisions --> |
| Focused tests and isolated dependencies | <!-- Selectors, tier commands, test environment setup --> |
| Format, lint, type check, build, CI | <!-- Actual script names, working directory, required gates --> |

## Before editing

1. Read the nearest applicable `AGENTS.md`, then the changed code, its callers, and the relevant tests. For an API, schema, or event change, inspect both producers and consumers. Code and configuration show current behavior. If they conflict with an accepted contract, resolve the intended behavior and update the affected source in the same change.
2. Identify the user-visible outcome, the entry point that exercises it, and the smallest check that can prove it. For a bug, capture a failing case when practical. Use the repository's runtime, package manager, lockfile, and supported shell.
3. Check the working-tree diff before editing. Preserve unrelated edits and untracked files. Follow the repository's Git workflow and keep the diff limited to the requested behavior and its verification.

## Implement the smallest change

- Fix the behavior in the module that owns it. Prefer editing an existing function, type, or file. Add an abstraction when a current boundary, multiple implementations, or meaningful duplication calls for it. Reuse the repository's public interfaces and keep dependency direction intact.
- Preserve public behavior and existing data unless the task changes the contract. For an intentional contract change, update the schema or events, affected callers, and verification together. Plan deployment order or compatibility when versions can overlap.
- Validate inputs and enforce authorization at the trusted boundary. Reuse the existing authentication, request validation, and structured error handling. Keep public errors safe and redact credentials and sensitive data in logs and artifacts. Use parameterized database queries.
- Give each write operation one transaction owner. Check write-dependent invariants and persist the related changes atomically. Keep slow external I/O outside the database transaction. Run dependent side effects after commit, using the project's durable delivery mechanism when recovery requires it. Check retry, concurrent execution, partial failure, and idempotency where they affect correctness.
- For a schema change, follow the migration workflow and add a forward migration. Verify the upgrade with representative existing data against the target database when the migration affects that data.
- In the frontend, reuse the existing API client, state ownership, routing, UI primitives, and translation resources where applicable. For async changes, check the affected loading, error, retry, and out-of-order response paths. Keep server-side authorization authoritative.

## Choose tests by what they must prove

Add or update tests for a reported regression, an intentional public contract change, or a material risk involving permissions, money, state, concurrency, or destructive actions. Reuse existing coverage when it already proves the changed behavior. Start with representative success and the boundary that decides the outcome. Parameterize equivalent inputs.

Use the cheapest tier that can observe the actual behavior. Map these tiers to the repository's runners and naming.

| Tier | What to run | Evidence |
| --- | --- | --- |
| L1 · Unit | Pure logic with deterministic inputs and controlled doubles | Decision, validation, state transition, or error mapping |
| L2 · Integration | Real collaborators for the boundary under test, such as a database engine, cache, or frontend state and query providers | Transaction, rollback, query, cache, or collaboration behavior. A request issued in-process proves the handler contract at this tier. |
| L3 · API or service end to end | Real network entry point in an isolated test environment, with the worker, storage, or other dependencies needed by the flow | Status and response, plus independently observed persistence or side effects where relevant |
| L4 · Browser | Real browser through the user entry point. Use a production build and real backend for full-stack acceptance. | Visible result and user interaction. For full-stack cases, confirm the corresponding backend state independently. |

- Exercise the normal entry point and assert an observable result, rejection, or necessary side effect. Assert calls where delivery, exact arguments, or absence of a side effect is itself the contract. Prefer real collaborators inside the boundary and put doubles at external seams. Match their real signatures and data shapes.
- For frontend component tests, use fresh state and cache per case, exercise the rendered result, and stub only the declared network operations. A simulated DOM run provides component evidence. Use a real browser for browser behavior, layout, and browser-specific regressions.
- Use deterministic fixtures that satisfy real constraints. For live tests, verify the target environment and seed, create data owned by the run, and confirm cleanup even on failure. Preserve the first failure and treat a retry as diagnostic evidence.

## Verify before handing off

1. Run the focused checks through the repository's normal entry points. Verify that the intended tests were collected and executed. Run the relevant format, lint, type, architecture, or build checks. Limit auto-formatting to the files you changed. For a documentation-only change, check the diff, local links, and referenced paths.
2. Expand verification when a changed contract crosses modules, repos, or deployment boundaries. Bind cross-repo acceptance to the tested frontend and backend versions, environment, and relevant seed/configuration. Local tests, build checks, and live acceptance each carry their own evidence.
3. Review the final diff for scope and contract compatibility. Fix new gate failures where they originate and keep existing thresholds and baselines intact. Report pre-existing failures with evidence.
4. Report the behavior delivered, assumptions that affect it, the exact checks run, and any failed, skipped, or blocked checks with reasons. Empty collection and skipped required cases leave the behavior unverified. Claim completion only for the scope supported by the evidence.

## Maintain these instructions

Keep repository-wide rules here and link to area guides with a trigger such as schema changes, test fixtures, or release steps. Keep each rule in one place. Put mechanically checkable constraints in the repository's existing lint or CI gates and point to those gates here.
