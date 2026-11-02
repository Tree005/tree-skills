---
name: human-observer
description: "AI private observer. Reviews the day's conversations as an observer and writes an observation diary."
---

# Human Observer

AI 作为私人观察者，将对话中用户的行为、思维与情绪写成观察日记。**此 skill 只做一件事：记录。**
多个 agent、多个窗口共用同一 `DIARY_DIR`，各自写入独立段落，统一归档。

---

## 激活后立即执行：确认日记目录

**配置来源**：环境变量 `HUMAN_OBSERVER_DIARY_DIR`。
本文件不保存实际路径，避免安装源（GitHub 仓库）被反向修改。

### 判定流程

| 环境变量状态 | 处理 |
|---------------|------|
| 已设置，且目录存在 | 直接使用，继续 |
| 已设置，但目录不存在 | 询问「配置的目录 `<路径>` 不存在——在此创建，还是重新指定？」→ 按回答处理（创建目录 / 让用户修改环境变量） |
| 未设置 | 询问用户「请指定观察日记的存储目录（绝对路径）」→ 本次会话使用该路径，并提示用户设置环境变量（见下方命令） |

**设置命令**（用户执行一次，所有 agent 共用）：

- Windows：`[Environment]::SetEnvironmentVariable('HUMAN_OBSERVER_DIARY_DIR', '<路径>', 'User')`
- macOS / Linux：`export HUMAN_OBSERVER_DIARY_DIR='<路径>'`（写入 shell 配置）

> 配置不写入 skill 文件；换机器或换用户时重新设置一次。

### 目录结构（按月份归档）

```
<DIARY_DIR>/
├── _topics.md          ← Agent 与话题注册表（写入前必查）
├── _followups.md       ← 待跟进汇总（写完后同步）
├── 2026-06/            ← 按月归档
│   └── 2026-06-04.md
├── 2026-07/
├── 2026-10/
│   └── 2026-10-13.md
└── ...
```

| 状态 | 处理 |
|------|------|
| 根目录不存在 | 按上方判定流程处理 |
| 当月子目录不存在 | 写入前自动创建 `YYYY-MM/` |

**写入路径规则**：`<DIARY_DIR>/YYYY-MM/YYYY-MM-DD.md`（YYYY-MM 取自系统命令日期）

---

## 激活后只做一件事

用户说任何话 → 执行 `references/diary-write-flow.md`。

> 若用户意图不明确，推断一个话题候选，向用户确认后开始写。

> ⚠️ 日期必须来自系统命令（`date +%Y-%m-%d` 或 `Get-Date -Format 'yyyy-MM-dd'`），禁止用已有文件名推断日期，禁止用 env 中的 Today's date（可能是会话开始时间，跨天不更新）。
