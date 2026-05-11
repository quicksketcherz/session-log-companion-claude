# Session Log Companion — Claude Code Install Guide

**Version:** 1.0  
**Platform:** Claude Code (CLI)  
**Created:** 2026-04-01

---

## What Gets Installed

```
~/.claude/skills/session-log-companion-claude-v1/
├── SKILL.md                    # Main skill file with 4 workflows
├── README.md                   # Usage guide and quick reference
├── TEST-SCENARIOS.md           # Test cases
├── INSTALL.md                  # This file
└── references/
    ├── COMMANDS.md                  # Command reference
    ├── discovery-log-template.md    # Discovery log structure
    ├── learning-log-template.md     # Learning log structure
    ├── session-log-template.md      # Session log structure
    └── master-template.md           # Complete system guide
```

---

## Install

Open Terminal and run:

```bash
mkdir -p ~/.claude/skills
cp -r session-log-companion-claude-v1 ~/.claude/skills/session-log-companion-claude-v1
```

No restart needed — Claude Code picks up new skills immediately.

---

## Verify Installation

```bash
ls ~/.claude/skills/session-log-companion-claude-v1/
```

You should see `SKILL.md`, `README.md`, `references/`, etc.

---

## Test It

Open Claude Code in any project and say:

> "Start a session for my project"

Claude should acknowledge the session and offer to document discoveries as you work.

---

## How the References Work

The skill reads log templates from `references/` when creating discovery logs, learning logs, and session summaries. It checks your **project directory first**, then falls back to the global install at `~/.claude/skills/session-log-companion-claude-v1/references/`.

This means the skill works out of the box in any project — no per-project setup needed.

If you want project-local templates (useful for customizing per project):

```bash
cp -r ~/.claude/skills/session-log-companion-claude-v1/references ./references
```

---

## Usage

| Say this... | What happens |
|---|---|
| "Start a session" | Claude captures session intent and stays alert for documentation opportunities |
| "Document this" / "I'm stuck" | Creates a Discovery or Learning log |
| "Remember this preference" | Creates a preference log for future sessions |
| "Summarize this session" | Creates a full session log with cross-references |

---

## Uninstall

```bash
rm -rf ~/.claude/skills/session-log-companion-claude-v1
```

Your session logs and knowledge logs in your projects are not affected.

---

## Update

To update to a newer version, copy the new folder and overwrite:

```bash
cp -r session-log-companion-claude-v1 ~/.claude/skills/session-log-companion-claude-v1
```
