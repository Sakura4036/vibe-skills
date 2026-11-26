# Set up a target repository

1. Resolve the target root from the path the user provided or the current Git root. A directory explicitly named for a new project can be used before Git initialization. Read its governing instructions. In Git repositories, inspect status and staged and unstaged changes.
2. Discover the project facts for the [portable agent guide](portable-agent-guide.md). Fill **Find / Repository entry** from authoritative sources. Check runtime pins, lockfiles, package or build scripts, CI, architecture and contract docs, and existing tests. Record executable commands with their working directories and known environment requirements. Ask together for material details that the repo cannot answer, such as a required test entry point or isolated test environment. Keep unconfirmed entries open.
3. Inventory the active host's skills and existing user-level copies. Reuse installed companions, including plugin versions. Preserve existing disabled or undiscovered copies and report their status. Install missing skills at user scope. For Codex and the shared Agent Skills layout, use the commands below. Use the active host's installer target, for example `--agent claude-code` in Claude Code. Windows can use `npx.cmd` when PowerShell blocks the `npx` script.
   - Karpathy. Install `karpathy-guidelines` from `multica-ai/andrej-karpathy-skills` if missing.

     ```sh
     npx --yes skills@latest add multica-ai/andrej-karpathy-skills --global --agent codex --skill karpathy-guidelines --yes
     ```

   - Matt Pocock. Check `code-review`, `diagnosing-bugs`, `grilling`, `implement`, `pr`, `setup-matt-pocock-skills`, and `tdd`. Pass only the missing names after `--skill`. Skip the installer if the list is empty. This example covers a project missing only `tdd` and `grilling`.

     ```sh
     npx --yes skills@latest add mattpocock/skills --global --agent codex --skill tdd grilling --yes
     ```

   - pstack. Check `create-verification-skill`, `maintain-verification-skill`, and `unslop` by their skill names, including namespaced plugin copies. Install only missing names from the upstream pstack directory. If all three are missing, run:

     ```sh
     npx --yes skills@latest add https://github.com/cursor/plugins/tree/main/pstack/skills --global --agent codex --skill create-verification-skill maintain-verification-skill unslop --yes
     ```

4. Apply the filled guide to root `AGENTS.md` by default, or the user's requested in-project destination. Follow any active `AGENTS.override.md` and repository writing rules. When the destination is the root `AGENTS.md` and the host is Claude Code, reuse the existing guide import or add `@AGENTS.md` to the project’s `CLAUDE.md` once. Check which file the host loads and report when the new guide is shadowed. Create a new file from the bundled template. For existing guidance, retain its language, commands, and local rules, and merge compatible missing material. Leave equivalent guidance alone. Keep the setup facts in one place and limit edits to the requested target.
5. After the guide and dependencies have been prepared, invoke Matt's `setup-matt-pocock-skills` for tracker, triage, and domain docs. Use its discovery and propose only missing settings. Prefer existing config and suggest a local tracker for local-first work when the project has no choice recorded. Respect the host's explicit-invocation policy. If direct invocation is unavailable, read the installed skill and apply its authorized local setup steps, reporting any part that needs input. Treat tracker writes as separate authorized actions. Existing complete configuration can be reused. Use [planning](planning.md) for this workflow's local spec and plan paths.
6. Read back tracked and untracked changes, confirm the skill names and paths or plugin identities in host discovery where available, and report the guide, reused or installed dependencies, and the Matt setup status individually. Verify files and note pending session discovery when the host cannot refresh. Keep the working tree for the user's requested delivery.

Sources. [Karpathy Guidelines](https://github.com/multica-ai/andrej-karpathy-skills/tree/main/skills/karpathy-guidelines), [Matt Pocock setup](https://github.com/mattpocock/skills/tree/main/skills/engineering/setup-matt-pocock-skills), [Skills CLI](https://github.com/vercel-labs/skills/blob/main/docs/commands.md).
