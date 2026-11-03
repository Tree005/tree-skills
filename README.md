# tree-skills

Portable Agent Skills for AI coding agents.

Turn repeated workflows into reusable skills: teach it once, use it across agents and projects. Every skill follows the open Agent Skill specification and stays agent-agnostic — it loads in Claude Code, Cursor, Codex, or any other environment that supports the spec.

## Skills

| Skill | What it does | Invoke |
| --- | --- | --- |
| [human-observer](human-observer/) | Reviews the day's conversations from an observer's perspective and writes a behavioral observation diary. | `/human-observer` |
| [exam-bootstrap](exam-bootstrap/) | One-time initialization of an exam-prep workspace: directory skeleton, AGENTS constraints, question-bank spec, and progress file. | `/exam-bootstrap` |

## Install

Ask a coding agent to install it for you:

```text
Install the skill from https://github.com/Tree005/tree-skills into your skills directory.
```

> The repository is the source; the installed copy is what the agent runs. Don't edit repo files to change personal settings.

## Configuration

Machine-specific settings live in environment variables, never in skill source:

| Skill | Variable | Description |
| --- | --- | --- |
| human-observer | `HUMAN_OBSERVER_DIARY_DIR` | Absolute path to the observation diary directory. |

Set once per machine; all agents share it:

```powershell
# Windows
[Environment]::SetEnvironmentVariable('HUMAN_OBSERVER_DIARY_DIR', 'D:\Notes\human-observer', 'User')
```

```bash
# macOS / Linux — add to your shell profile to persist
export HUMAN_OBSERVER_DIARY_DIR="$HOME/Notes/human-observer"
```

## Usage

### human-observer

```text
/human-observer
```

Reviews the day's conversations and records behavior, direct quotes, emotions, and patterns in the day's diary. Diaries are archived by month and shared across agents and windows. If `HUMAN_OBSERVER_DIARY_DIR` is not set, it asks for a path at invocation; that value applies to the current session only.

### exam-bootstrap

```text
/exam-bootstrap
```

Run it in an empty directory and answer five prompts: subject, structure template, question source, output location, and topic list. It generates the directory skeleton, `AGENTS.md`, question-bank spec, and progress file. Initialization only — no daily question generation or grading.

## Design principles

1. **Agent-agnostic** — no single product; only fields and capabilities in the open specification.
2. **Config outside source** — machine-specific settings go in environment variables; skill source stays distributable.
3. **Single responsibility** — one skill, one job.
4. **No proprietary tools** — file I/O and system commands only.

## Repository structure

```text
tree-skills/
├── human-observer/
│   ├── SKILL.md
│   └── references/
├── exam-bootstrap/
│   ├── SKILL.md
│   └── templates/
├── README.md
├── LICENSE
└── .gitignore
```

Only skill directories, `README.md`, `LICENSE`, and `.gitignore` are tracked. Personal configuration and tool caches stay out of the repository.

## Adding a skill

- Use a kebab-case folder name; the `name` field in `SKILL.md` must match.
- Add the folder to the `.gitignore` allowlist so its files are tracked.
- Write the `description` in English, one sentence on what the skill does. Quote the whole value if it contains a colon followed by a space.
- Put invocation details in the body; long rules go in `references/`, scaffolding in `templates/`.
- Run it on a real task before updating the Skills table.

## Naming and writing

- Folder and field names: English, kebab-case.
- Skill bodies: currently written in Chinese.
- `description`: English.

## License

MIT. See [LICENSE](LICENSE).
