# Session Log Template

**Use for:** Recording what happened in each work session

**Naming:** `YYYY-MM-DD-HHMM-Session-Title.md`

**Get timestamp:** `date "+%Y-%m-%d %H%M"`

---

```markdown
# Session: [Session Title]

**Date:** YYYY-MM-DD  
**Time:** HHMM  
**AI Assistant:** USER_FILL_WHAT_AI_MODEL_NAME_WAS_USED  
**AI Platform:** [Claude/Cursor/Gemini/ChatGPT/etc.]

<!-- TODO: Fill in AI Assistant model name from your model selector (e.g., Claude 3.5 Sonnet, GPT-4, Gemini 1.5 Pro) -->

---

## Applications Used

| Application | Version | Purpose |
|-------------|---------|---------|
| [Tool Name] | [Version] | [What it was used for] |

---

## Session Focus

[One paragraph describing what this session was about]

---

## What We Accomplished

### 1. [Task Name] ✅

**Summary:** [1-2 sentence overview of what was accomplished]

**Application:** [Tool used]

**see notes:** [Link to knowledge log/resource/artifact if applicable - describe what's there]

---

**Note:** Keep tasks concise when knowledge logs exist. Use "see notes:" to reference detailed documentation. Only include full details for tasks without separate documentation.

---

## Key Learnings

### [Learning Topic]

**Application:** [Tool name]  
**Challenge:** [Issue addressed]  
**Solution:** [How it was solved]

---

## Files Created/Modified

| File | Application | Purpose |
|------|-------------|---------|
| `path/to/file` | [Tool] | [Description] |

**Note:** Only list project files that were part of the actual work (code, assets, configs, etc.). Do NOT list the session log itself or knowledge logs - that's redundant.

---

## Guides Updated

| Guide | Changes Made | Reason |
|-------|--------------|--------|
| `path/to/guide.md` | [Brief description] | [Version difference / Correction / Clarification] |

**Note:** Only include this section if implementation guides or reference documentation were updated during the session.

---

## Knowledge Logs Created

| Knowledge Log | Tool | Type | Topic |
|---------------|------|------|-------|
| `resources/[tool]-knowledge-logs/YYYY-MM-DD-HHMM-Title.md` | [Tool] | Discovery/Learning | [Brief description] |

**Note for AI:** Only create knowledge logs when user explicitly asks to document. The criteria below describe WHAT to document when asked, not when to automatically create logs:
- **Discovery Log:** Hit impasse, AI wrong, revealed tool principle
- **Learning Log:** Significant Q&A session, understanding concepts, filling knowledge gaps

When user requests documentation, ask which tool to document for, determine log type, then create in appropriate `[tool]-knowledge-logs` folder.

---

## Next Steps

- [ ] [Next task]

---

## Notes & Observations

[Additional notes, design decisions]

---

*Session ended: [Brief summary]*
```

---

## Session Log Best Practices

**Keep it concise:** When knowledge logs exist, use brief summaries with "see notes:" references instead of duplicating content.

**Format:**
```markdown
**see notes:** `resources/[tool]-knowledge-logs/YYYY-MM-DD-HHMM-Title.md` for [what's documented there]
```

**Cross-referencing:** Use matching timestamps between session logs and knowledge logs for instant cross-referencing.
