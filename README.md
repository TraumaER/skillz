# skillz

A collection of AI agent skills, portable across any harness that supports the [Agent Skills spec](https://agentskills.io/specification) (Claude Code, Codex, and others).

## Skills

| Skill | Description |
|---|---|
| [teach-me](skills/teach-me/SKILL.md) | Hands-on instructor for a software engineering topic: teaches with overview/ELI5/real-world tie-in, scaffolds a starter app, assigns TDD-style exercises, and tracks progress across sessions and repos. |

## Using a skill

### Claude Code (as a plugin)

This repo is also a Claude Code plugin marketplace — installing it pulls in every skill above at once:

```
/plugin marketplace add TraumaER/skillz
/plugin install skillz@skillz
```

### Any other harness

Each skill is a self-contained directory under `skills/<name>/` with a `SKILL.md`. Point your harness's skills directory at it — either copy the directory in, or symlink it so this repo stays the single source of truth:

```sh
# Claude Code (manual, without the plugin above)
ln -s /path/to/skillz/skills/teach-me ~/.claude/skills/teach-me

# Codex, Copilot CLI, Gemini CLI (cross-runtime path)
ln -s /path/to/skillz/skills/teach-me ~/.agents/skills/teach-me
```

On Windows, use `New-Item -ItemType SymbolicLink` instead of `ln -s`.

## Adding a skill

New skills live at `skills/<name>/SKILL.md`, with `name` and `description` frontmatter per the spec. Add a row to the table above when it's ready.
