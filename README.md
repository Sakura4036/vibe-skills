# Vibe Skills

把个人编码工作流带到不同项目。使用当前仓库的规范和验证入口，以最小改动交付可验证的结果。技能入口是 [coding-workflow](skills/coding-workflow/SKILL.md)。

## 安装

从以下三种方式中任选一种。仓库公开可读。

### npx skills

```sh
npx skills add Sakura4036/vibe-skills --global --agent codex --skill coding-workflow
```

这条命令把技能装入 `~/.agents/skills/`。需要为其他受支持的客户端安装时，选择对应的 `--agent`。Windows PowerShell 无法运行 `npx` 脚本时可使用 `npx.cmd`。

### Codex 原生插件

```sh
codex plugin marketplace add Sakura4036/vibe-skills
codex plugin add vibe-skills@vibe-skills
```

可先用 `codex plugin list` 确认已配置的入口。已有个人版时，把它迁移到选定的安装渠道，保留已有自定义内容，并核对发现结果。

### Claude Code 插件

在 Claude Code 会话中运行：

```text
/plugin marketplace add Sakura4036/vibe-skills
/plugin install vibe-skills@vibe-skills
```

在目标项目用 `/vibe-skills:coding-workflow setup` 初始化。通过 `npx skills` 单独安装到 Claude Code 时，入口是 `/coding-workflow setup`。

## 常用入口

| 调用 | 用途 |
| --- | --- |
| `$coding-workflow setup` | 在目标仓库填充根目录 `AGENTS.md`，补齐缺失的 Karpathy、Matt 和 pstack 依赖，再启动 Matt 的项目配置。 |
| `$coding-workflow repeat` / `grill` | 核对理解，或讨论实质性的未决问题。 |
| `$coding-workflow to-spec` / `to-plan` | 写入本地 `docs/vibe/specs/` 或分阶段的 `docs/vibe/plans/`。 |
| `$coding-workflow create-verification` / `maintain-verification` | 建立或维护仓库级 `verify-*`，复用真实启动、测试和证据入口。 |
| `$coding-workflow tdd` / `implement` / `review` | 使用 Matt 技能做测试驱动、实现或评审。 |
| `$coding-workflow pr` / `unslop` | 按实际改动写 PR 描述，或在保留原意的前提下改写文字。 |
| `$coding-workflow auto` | 按任务选最短流程。省略命令也是此模式。 |

例如 `$coding-workflow 修复重试后旧响应覆盖已完成状态的问题，先别提交。`

## 上游分工

| 任务 | 工作流如何选择 |
| --- | --- |
| 澄清、排错、TDD、实现、评审、PR | 使用 Matt 的对应技能。一次 TDD 只用 Matt 的版本。 |
| 规格与计划 | 规格可复用 Matt `to-spec` 的用户故事和测试边界。默认交付到本地 Markdown，计划按可独立验证的阶段组织。 |
| 项目验证 | 调用 pstack 的 `create-verification-skill` 或 `maintain-verification-skill`。针对改动时复验受影响的功能，明确要求全量审计时逐项验证。 |
| 文字与影响分析 | `unslop` 使用 pstack 原版。评审涉及共享契约时追踪实际调用方；明确要求影响分析且已安装时可用 `blast-radius`。 |

`setup` 复用宿主已发现的技能，只从上游安装缺项。验证创建、验证维护和 `unslop` 是默认 pstack 依赖，其他 pstack 技能按需使用。源文件位于 `skills/coding-workflow/`，三种安装方式共享同一份内容。

参考 [Matt Pocock 工程技能](https://github.com/mattpocock/skills/tree/main/skills/engineering)、[Karpathy Guidelines](https://github.com/multica-ai/andrej-karpathy-skills/tree/main/skills/karpathy-guidelines) 和 [pstack](https://github.com/cursor/plugins/tree/main/pstack)。
