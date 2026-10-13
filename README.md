# tree-skills

我自己写的 AI Agent Skills 集合。

遵循开放的 Agent Skill 规范，每个 skill 是一个独立文件夹，包含 `SKILL.md` 入口文件和 `references/` 参考文档。

## Skill 清单

| Skill | 说明 | 状态 |
|-------|------|------|
| [human-observer](human-observer/) | AI 私人观察者：以第三方视角回顾对话，撰写观察日记，记录行为、情绪与模式 | 使用中 |

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

## 命名规范

- 文件夹名：kebab-case（如 `human-observer`）
- `SKILL.md` 的 `name` 字段与文件夹名一致
- 文档正文可用中文，**命名一律英文**
