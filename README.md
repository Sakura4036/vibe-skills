# Vibe Skills

把个人编码工作流带到不同项目。使用当前仓库的规范和验证入口，以最小改动交付可验证的结果。这个仓库提供一个技能 `coding-workflow`。

## 安装

选一种入口安装，同一技能由仓库里的 `skills/coding-workflow/` 提供。此仓库为私有仓库，安装环境需要能读取它。

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

## 常用入口

| 调用 | 用途 |
| --- | --- |
| `$coding-workflow setup` | 在目标仓库填充根目录 `AGENTS.md`，补齐缺失的 Karpathy 和 Matt 技能，再启动 Matt 的项目配置。 |
| `$coding-workflow repeat` / `grill` | 核对理解，或讨论实质性的未决问题。 |
| `$coding-workflow to-spec` / `to-plan` | 写入本地 `docs/vibe/specs/` 或分阶段的 `docs/vibe/plans/`。 |
| `$coding-workflow create-verification` / `maintain-verification` | 建立或维护仓库级 `verify-*`，复用真实启动、测试和证据入口。 |
| `$coding-workflow tdd` / `implement` / `review` | 使用 Matt 技能做测试驱动、实现或评审。 |
| `$coding-workflow pr` / `unslop` | 按实际改动写 PR 描述，或在保留原意的前提下改写文字。 |
| `$coding-workflow auto` | 按任务选最短流程。省略命令也是此模式。 |

例如 `$coding-workflow 修复重试后旧响应覆盖已完成状态的问题，先别提交。`

参考 [Matt Pocock 工程技能](https://github.com/mattpocock/skills/tree/main/skills/engineering)、[Karpathy Guidelines](https://github.com/multica-ai/andrej-karpathy-skills/tree/main/skills/karpathy-guidelines) 和 [pstack](https://github.com/cursor/plugins/tree/main/pstack)。
