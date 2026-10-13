# tree-skills

我自己写的 AI Agent Skills 集合。

遵循开放的 Agent Skill 规范，每个 skill 是一个独立文件夹，包含 `SKILL.md` 入口文件和 `references/` 参考文档。

## Skill 清单

| Skill | 说明 | 状态 |
|-------|------|------|
| [human-observer](human-observer/) | AI 私人观察者：以第三方视角回顾对话，撰写观察日记，记录行为、情绪与模式 | 使用中 |

## 设计原则

1. **跨 agent 通用**——所有 skill 不绑定任何单一 agent 产品。任何支持 Agent Skill 规范的环境（CodeBuddy、Claude Code、Cursor、Codex 等）都能加载使用。
2. **规则通用，配置个人**——skill 的行为规则对所有用户通用；个人化配置（如文件路径）在文件内明确标注「移植提示」，换环境时修改该处即可。
3. **单一职责**——一个 skill 只做一件事。
4. **不依赖特定工具集**——只使用目标环境普遍具备的能力（读/写文件、执行系统命令），不假设某个产品独有的工具。

## 结构约定

```
tree-skills/
├── README.md
└── <skill-name>/          # kebab-case 命名（全小写 + 连字符）
    ├── SKILL.md           # 入口：name / description / 执行流程
    └── references/        # 详细规则文档
```

## 使用方式

将需要的 skill 文件夹复制到对应工具的 skills 目录：

- **CodeBuddy**：`~/.agent-a/skills/`
- **Claude Code**：`~/.claude/skills/`
- **其他产品**：对应产品的 skills 目录

## 命名规范

- 文件夹名：kebab-case（如 `human-observer`）
- `SKILL.md` 的 `name` 字段与文件夹名一致
- 文档正文可用中文，**命名一律英文**
