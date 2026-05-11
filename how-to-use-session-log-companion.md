# How to Use the Session Log Companion Skill

The **session-log-companion** is a comprehensive tool for documenting your work sessions, capturing discoveries, teaching the AI your preferences, and building a knowledge base. Here's how to use it.

## Four Main Use Cases

### 1. Starting a Session

Say things like:

- "Start a session"
- "Begin session log"
- "Let's work on [project name]"

The AI will capture your session intent and help document discoveries as you work.

### 2. Creating Knowledge Logs

Use when you want to document something important:

**Discovery Logs** (for problems/solutions):

- "I'm stuck"
- "Document this"
- "This isn't working"
- When you find a non-obvious solution or when AI suggestions don't work

**Learning Logs** (for understanding concepts):

- "Can you explain how X works?"
- "I need to understand..."
- "What is [concept]?"
- When building foundational knowledge

### 3. Teaching Agent Preferences

Tell the AI how you want it to work with you:

- "I want to improve how you work with me"
- "Remember this preference"
- "I prefer [style/approach]"

The AI will create preference logs that persist across sessions.

### 4. Ending a Session

Wrap up your work:

- "Summarize this session"
- "Create session log"
- "Wrap up"

The AI will review what you accomplished and create a comprehensive session summary.

## File Structure Created

The skill creates organized documentation:

```
your-project/
├── session-logs/
│   └── 2026-03-08-1430-Session-Title.md
├── resources/
│   ├── [tool]-knowledge-logs/
│   │   ├── 2026-03-08-1430-Discovery-Title.md
│   │   └── 2026-03-08-1445-Learning-Title.md
│   └── agent-companion-preference-logs/
│       └── 2026-03-08-1500-Preference-Title.md
└── references/
    ├── discovery-log-template.md
    ├── learning-log-template.md
    └── session-log-template.md
```

## Key Features

- **Timestamp-based cross-referencing**: All logs use timestamps (YYYY-MM-DD-HHMM) for easy linking
- **Tool-specific organization**: Knowledge logs are organized by tool (TouchDesigner, After Effects, etc.)
- **Portable preferences**: Preference logs work across all AI platforms (Claude, ChatGPT, Cursor, etc.)
- **Cursor integration**: Can optionally add preferences to `.cursor/rules/` for automatic enforcement

## Important Notes

- The AI **won't auto-create logs** — you need to explicitly ask
- You stay in control — the AI will ask which type of log and where to save it
- Logs are just markdown files — easy to read, edit, and version control
- The system improves collaboration over time as you build your knowledge base

## Quick Example

```
You: "Start a session for building an Unreal Engine UI panel"
AI: "Got it! Starting a session on Unreal Engine UI panels.
     I'll document discoveries as we work. What's first?"

[work happens...]

You: "I'm stuck - the widget isn't binding to the actor. Document this."
AI: "This sounds like a Discovery Log. Should I document this
     for Unreal Engine?"

You: "Yes"
AI: [Creates discovery log with problem/solution details]

[more work...]

You: "Summarize this session"
AI: [Reviews work, creates session log with cross-references]
```

To get started, just say **"start a session"** and tell the AI what you're working on!
