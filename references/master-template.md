# Project Documentation System — Session Logs + Tool Knowledge Logs

**Version:** 2.15  
**Created:** 2026-02-21  
**Updated:** 2026-03-26  
**For:** Multi-application projects across any creative/technical software

**⚠️ When updating this template:** 
1. Bump version number above (e.g., 2.11 → 2.12)
2. Update "Updated:" date
3. **Update version history file:** `readme_project_session_and_tool_knowledge_logs_VERSION_HISTORY.md` — add new version entry with changes, update "Last updated" date

---

## Purpose

Universal documentation system for tracking project work across any application. Two types of logs:

1. **Session Logs** — What happened in each work session
2. **Tool Knowledge Logs** — Tool-specific learnings (discoveries, understanding, and conceptual knowledge)

**Team benefit:** Consistent `YYYY-MM-DD-HHMM` timestamps enable instant cross-referencing and company-wide Dropbox search.

**Use with any AI or platform:** These instructions apply whether you use Cursor, Claude, Gemini, ChatGPT, or another AI. When you ask for a session log, have the AI follow the workflow in this template: review the session for notes to add, run the checklist (document later → knowledge logs, update project docs if applicable, AI rules log if rules/instructions were updated). If your platform uses a different place for rules (e.g. not `.cursor/rules/`), treat updates there the same way — create an AI rules log and reference it in the session log.

---

## The Two-Folder System

### Folder 1: Session Logs

**Naming:** `session_logs/`  
**Purpose:** Record what happened each session  
**Frequency:** One per session  
**File format:** `YYYY-MM-DD-HHMM-Session-Title.md`

### Folder 2: Tool Knowledge Logs

**Naming:** `resources/[tool]_knowledge_logs/`  
**Purpose:** Document tool-specific learnings - both discoveries (when stuck) and understanding (filling knowledge gaps)  
**Frequency:** Create when stuck, discover non-obvious solution, reveal tool principle, OR need to understand/learn concepts  
**File format:** `YYYY-MM-DD-HHMM-Brief-Title.md`

**Tool folder naming:** Lowercase with underscores (e.g., `touchdesigner_knowledge_logs`, `aftereffects_knowledge_logs`, `cinema4d_knowledge_logs`)

**Two types of knowledge logs:**
1. **Discovery Logs** — When AI got it wrong, hit impasse, found non-obvious behavior
2. **Learning Logs** — When filling knowledge gaps, understanding concepts, Q&A sessions

---

## Naming Convention

**Format:** `YYYY-MM-DD-HHMM-Brief-Title.md`

**Get timestamp:** `date "+%Y-%m-%d %H%M"`

**Why:** Session logs and knowledge logs use same format → instant cross-referencing via matching timestamps.

---

## Session Log Template

```markdown
# Session: [Session Title]

**Date:** YYYY-MM-DD  
**Time:** HHMM  
**AI Assistant:** WHAT_AI_MODEL_USED?  
**AI Platform:** [Claude/Cursor/Gemini/ChatGPT/etc.]

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
| `resources/[tool]_knowledge_logs/YYYY-MM-DD-HHMM-Title.md` | [Tool] | Discovery/Learning | [Brief description] |

**Note for AI:** Only create knowledge logs when user explicitly asks to document. The criteria below describe WHAT to document when asked, not when to automatically create logs:
- **Discovery Log:** Hit impasse, AI wrong, revealed tool principle
- **Learning Log:** Significant Q&A session, understanding concepts, filling knowledge gaps

When user requests documentation, ask which tool to document for, determine log type, then create in appropriate `[tool]_knowledge_logs` folder.

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
### [N]. [Task Name] ✅

**Summary:** [1-2 sentence overview]

**Application:** [Tool name]

**see notes:** `path/to/knowledge-log.md` for [what they'll find there]
```

**For detailed guidance:** See knowledge log about session log best practices for when to use "see notes:" vs full details, formatting patterns, and benefits.

---

## Documenting Code/Expressions in Session Logs

When documenting code snippets, expressions, scripts, or configurations in session logs:

**Always include context:**
- **Where used:** Which file/operator/parameter/location (e.g., "In the Constant CHOP `generation_animator`, pasted into **Const 0 Value** parameter", "In `config.py` line 45", "Shader code in Material node")
- **What it does:** Brief explanation of the code's purpose or behavior (e.g., "Shows different generation values depending on state", "Validates user input before saving", "Applies bloom effect to highlights")
- **How it connects:** How this code integrates with the rest of the system (e.g., "The L-system's Generations parameter reads from this CHOP's `generation` channel", "Called by the main render loop", "Triggered when user clicks Submit button")

**Example format:**

```markdown
**Where used:** In the **Constant CHOP** named `generation_animator` (inside `animation_controller`), pasted into the **Const 0 Value** parameter (set to Expression mode, purple button).

**What it does:**
- **IDLE (state 0):** Shows `index + 1` (current generation)
- **GROWTH (state 1):** Animates from `index + 1` to `index + 2`
- **HOLD/RETURN (state 2 or 3):** Shows `index + 2` (fully grown)

**Working expression:**
```
[code here]
```

**Connection:** The L-system SOP's **Generations** parameter is set to: `op('/project1/animation_controller/generation_animator')['generation'][0]`
```

**Why this matters:** Code without context is hard to reuse. Future readers (including you) need to know where to paste it, what it's supposed to do, and how it fits into the larger system. A snippet that says "use this expression" without explaining where or why is nearly useless months later.

**Applies to:**
- Expressions (TouchDesigner, After Effects, Houdini, etc.)
- Scripts (Python, JavaScript, MEL, etc.)
- Shader code (GLSL, HLSL, OSL, etc.)
- Configuration files (JSON, YAML, XML, etc.)
- SQL queries
- Command-line commands
- API calls

---

## Knowledge Log Templates

### Template 1: Discovery Log (Problem-Solving)

**Use when:** AI got it wrong, hit impasse (>15 min), found non-obvious behavior

**Structure:** Gap → Working Example → Why → Questions to Explore

```markdown
# [Feature/Operator/Node Name]

**Date:** YYYY-MM-DD  
**Time:** HHMM  
**Application:** [Tool name + version]  
**Discovered in:** [Project name]  
**Type:** Discovery Log

---

## The Gap

**Trying to do:** [Goal]

**AI suggested:** `[wrong parameter/approach]`

**Where it broke:** [Specific error/failure]

**What works:** `[correct parameter/approach]`

---

## Working Example

```
Setup: Input → Step1 (Setting: Value) → Step2 → Output
```

**Key settings:**
- `param1`: `value` — [Why this matters]
- `param2`: `value` — [Why this matters]

**Expected result:** [What you should see]

---

## Why This Matters

**Why AI gets it wrong:** [Brief reason - outdated docs, version differences, etc.]

**Tool principle:** [What this reveals about how the tool works]

---

## Questions to Explore Next

1. [Experiment or variation]
2. [Related scenario]
3. [Edge case to test]

---

## Links

**Official docs:** [Link]  
**Version tested:** [Specific version]
```

---

### Template 2: Learning Log (Understanding/Education)

**Use when:** Filling knowledge gaps, understanding concepts, Q&A sessions, building foundational knowledge

**Structure:** What I Needed to Understand → Key Concepts → How It Works → Practical Examples → Related Topics

```markdown
# [Concept/Feature/System Name]

**Date:** YYYY-MM-DD  
**Time:** HHMM  
**Application:** [Tool name + version]  
**Project:** [Project name]  
**Type:** Learning Log

---

## What I Needed to Understand

**Knowledge gap:** [What you didn't understand]

**Why it matters:** [Why you need to understand this]

**Questions asked:**
- [Question 1]
- [Question 2]
- [Question 3]

---

## Key Concepts Learned

### [Concept 1]

**Definition:** [Clear explanation]

**Purpose:** [What it's used for]

**Example:** [Simple example]

### [Concept 2]

**Definition:** [Clear explanation]

**Purpose:** [What it's used for]

**Example:** [Simple example]

---

## How It Works

**Step-by-step explanation:**

1. [Step 1 with explanation]
2. [Step 2 with explanation]
3. [Step 3 with explanation]

**Visual/Mental Model:** [Analogy or diagram description]

---

## Practical Examples

### Example 1: [Scenario]

```
[Code/setup/configuration]
```

**What this does:** [Explanation]

**When to use:** [Use case]

### Example 2: [Scenario]

```
[Code/setup/configuration]
```

**What this does:** [Explanation]

**When to use:** [Use case]

---

## Common Patterns & Best Practices

**Pattern 1:** [Description and when to use]

**Pattern 2:** [Description and when to use]

**Things to avoid:** [Common mistakes or misconceptions]

---

## Test Your Understanding

**Purpose:** Use these questions to verify you truly understand the concept (Feynman Technique). If you can't answer them simply, revisit the sections above.

**Questions to answer in your own words:**

1. [Question testing core concept - e.g., "What does X do and why would you use it?"]
2. [Question about how it works - e.g., "How does X affect Y?"]
3. [Question about practical application - e.g., "When would you use X vs Z?"]
4. [Question about edge cases - e.g., "What happens if you set X to 0?"]

**Challenge yourself:** Try explaining this to someone who's never used the tool. What questions would they ask?

---

## Related Topics to Explore

1. [Related concept or feature]
2. [Advanced variation]
3. [Integration with other features]

---

## References

**Documentation:** [Links to official docs]  
**Resources used:** [What helped you understand this]  
**Version:** [Specific version this applies to]
```

---

## Cross-Referencing System

### Timestamp-Based Cross-Referencing

**Example:**
1. Session at `2026-02-21 16:26`
2. Session log: `session_logs/2026-02-21-1626-State-Machine-Fix.md`
3. Knowledge log: `resources/touchdesigner_knowledge_logs/2026-02-21-1626-Select-CHOP-Pattern.md`
4. Both share `2026-02-21-1626` → instant match

**Company Dropbox search:**
- `"touchdesigner_knowledge_logs"` → All TouchDesigner learnings across projects
- `"2026-02-21-1626"` → Session + knowledge logs from that exact time

### "see notes:" References

Use `"see notes:"` in session logs to link to detailed documentation:

**In session log:**
```markdown
**see notes:** `resources/touchdesigner_knowledge_logs/2026-02-21-1626-Concept.md` for complete guide
```

**Benefits:**
- Quick search: `Cmd+F "see notes:"` finds all references
- Avoids duplication between session and knowledge logs
- Clear pointer to detailed information

---

## AI Rules Logs

**Purpose:** Track how AI assistants learn to work with your documentation system. Capture improvements and corrections so they're portable across projects and platforms.

**Naming:** Follows same pattern as `session_logs/` and `[tool]_knowledge_logs/` for consistency.

### Folder Structure

```
project/
├── session_logs/               ← What happened each session
├── ai_rules_logs/              ← How AI learned the system (project-level for visibility)
│   ├── README.md              ← Template and guidelines
│   └── YYYY-MM-DD-HHMM-Brief-Description.md
├── .cursor/rules/              ← Cursor-specific (auto-applies)
├── .claude/                    ← Claude Projects (if using)
├── .ai_rules/                  ← Platform-agnostic rules (optional)
│   ├── README.md              ← How to use these rules
│   ├── session-log-workflow.md
│   └── knowledge-log-workflow.md
```

**Why project-level:**
- Matches `session_logs/` pattern (visible, not hidden)
- Searchable in Dropbox alongside other logs
- Self-documenting folder structure
- Easy to discover and reference

### When to Create AI Rules Logs

**Whenever rules or instructions that govern the AI are updated or created, create an AI rules log** for that change. Reference it in the session log with "see notes:". This applies to Cursor (`.cursor/rules/`), Claude Projects, ChatGPT custom instructions, Gemini project rules, or any project rules file or system prompt. Same workflow on any platform — keeps rule changes portable and auditable.

**Use with any AI or platform:** Create an AI rules log whenever you update instructions or rules that govern the AI — whether that's Cursor rules, another platform's custom instructions, a project rules file, or a system prompt. Document the change here, use the template below, and reference it in the session log with "see notes:".

**AI rules logs are also created when the session involved other documentation-system improvements.**

**Create when:**
- ✅ **You updated or created a Cursor rule** (`.cursor/rules/`) → create an AI rules log (don't skip)
- ✅ **You updated rules/instructions on another platform** (e.g. Claude Projects, ChatGPT custom instructions, Gemini project rules) → create an AI rules log the same way
- ✅ You corrected AI behavior about documentation workflows
- ✅ You updated/created README instructions (session_logs, knowledge logs, etc.)
- ✅ You clarified ambiguous phrasing in documentation system
- ✅ You added new workflow rules for session/knowledge logs
- ✅ You want to remember why a documentation rule exists

**Don't create when:**
- ❌ One-time correction specific to current project task
- ❌ Session was about project work (TouchDesigner, L-system, etc.) only
- ❌ AI made a simple mistake that won't repeat

**Workflow:** When the user asks for a session log after discussing rule improvements, the AI should recognize it and create the log in `ai_rules_logs/` (and reference in session log with "see notes:"). **If Cursor rules — or rules/instructions on any other AI platform — were updated, always create an AI rules log** — no need to ask. For README-only or phrasing changes, the AI may ask "Should I create an AI rules log for [the change]?" and create if yes.

### AI Rules Log Template

**Format:** `YYYY-MM-DD-HHMM-Brief-Description.md`

```markdown
# AI Rule Update: [Brief Description]

**Date:** YYYY-MM-DD  
**Time:** HHMM  
**Triggered by:** [What went wrong or what needed clarification]  
**Applies to:** [Session logs / Knowledge logs / Both / AI behavior]

---

## The Issue

**What happened:** [AI did X when it should have done Y]

**User expectation:** [What user expected to happen]

**Root cause:** [Why AI misunderstood - ambiguous wording, missing instruction, etc.]

---

## The Fix

**Rules updated:**
- [ ] `.cursor/rules/[filename].md`
- [ ] `.ai_rules/[filename].md`
- [ ] `session_logs/README.md`
- [ ] `resources/README-KNOWLEDGE-LOGS.md`
- [ ] Other: [specify]

**Changes made:**

1. **[File/Section]:** [What was changed]
   - **Before:** [Old instruction]
   - **After:** [New instruction]
   - **Why:** [Reasoning]

---

## New Behavior

**Now when user says:** "[trigger phrase]"

**AI should:** [Expected behavior]

**AI should NOT:** [What to avoid]

---

## Reusability

**Project-specific?** [Yes/No - explain why]

**Portable to other projects?** [Yes/No - if yes, which type of projects?]

**Platform-specific?** [Cursor only / Works in Claude, Gemini, etc.]

---

## Status

[✅ Resolved / 🔄 In Progress / ⚠️ Needs Testing]

---

## Related Updates

- See: `YYYY-MM-DD-HHMM-Previous-Related-Update.md` (if applicable)

---

## Evolution Pattern

[Optional: If this is part of a series of refinements, describe the progression]
```

### Portability Strategy

**Three-tier system:**

1. **Platform-specific rules** (`.cursor/rules/`, `.claude/`, etc.)
   - Auto-applied by that platform
   - Use platform conventions
   
2. **Universal rules** (`.ai_rules/`)
   - Markdown files any AI can read
   - Platform-agnostic instructions
   - Reference from platform-specific rules

3. **Project READMEs** (`session_logs/README.md`, `resources/README-KNOWLEDGE-LOGS.md`)
   - Self-documenting
   - Works across all platforms
   - AI reads before creating logs

### Archiving for Reuse

**When starting new project:**

1. **Review AI rules logs:**
   - Read `ai_rules_logs/` folder from previous project
   - Identify which rules apply to new project
   - Update new project's READMEs with relevant learnings

2. **Copy universal rules (optional):**
   ```bash
   cp -r old_project/.ai_rules/ new_project/.ai_rules/
   ```

3. **Create platform-specific rules:**
   - Cursor: `.cursor/rules/`
   - Claude: Add to project knowledge
   - Gemini: Add to system instructions

### Summary Command

**When you want to export/archive:**

"Summarize all AI rules logs from this project into a portable guide I can use in [new project / other platform]"

**AI should:**
1. Read all files in `ai_rules_logs/`
2. Identify patterns and key learnings
3. Create summary document with:
   - Core workflow principles
   - Common misunderstandings to avoid
   - Platform-agnostic instructions
   - Recommended rules for new project
4. Save as `ai_rules_logs/YYYY-MM-DD-HHMM-Summary-For-[New-Project].md`

---

## Setting Up a New Project

1. Create `session_logs/` folder
2. Create `session_logs/README.md` with the **full** session log template and guidelines in the file (copy from "Session Log Template" and "Session Log Best Practices" above). Do not create a stub that only links to this master.
3. Create `resources/README-KNOWLEDGE-LOGS.md` with master index + full templates
4. Create `resources/[tool]_knowledge_logs/` folders as needed (e.g., `touchdesigner_knowledge_logs/`)
5. Create short `README.md` in each knowledge logs folder (tool-specific conventions only)
6. **NEW:** Create `ai_rules_logs/` folder for tracking documentation system improvements
7. **NEW:** Create `ai_rules_logs/README.md` with AI rules log template and guidelines
8. **Optional:** Create `.ai_rules/` folder with platform-agnostic rules
9. Set up platform-specific AI rules (`.cursor/rules/` for Cursor, etc.)

**⚠️ Session log README must be full, not a stub:** Copy the template and best practices into `session_logs/README.md`; do not use a short README that only links to this master.

**First-time setup checklist:**
- [ ] `session_logs/README.md` exists and contains the full session log template and best practices (not just a link to the master)
- [ ] `resources/README-KNOWLEDGE-LOGS.md` exists
- [ ] At least one `resources/[tool]_knowledge_logs/` folder exists
- [ ] Each knowledge logs folder has its own `README.md`
- [ ] `ai_rules_logs/` folder exists (recommended for tracking system improvements)
- [ ] `ai_rules_logs/README.md` exists (if using AI rules logs)
- [ ] `.ai_rules/` folder exists (optional - for platform-agnostic rules)

**When agent creates first session log:**
- Agent should check if these READMEs exist
- If missing, agent should ask to create them before proceeding
- This ensures the system is properly set up and self-documenting

---

## README Naming Convention

**Rule of thumb:**
- **Single-purpose folder** (only session logs) → `README.md`
- **Multi-purpose folder** (resources with various things) → `README-[SPECIFIC-TOPIC].md`

**Examples:**
- `session_logs/README.md` ✅
- `resources/README-KNOWLEDGE-LOGS.md` ✅
- `touchdesigner_knowledge_logs/README.md` ✅

**For detailed explanation:** See knowledge log about README naming philosophy for why this matters, when to use each approach, and how it helps teams.

---

## When to Document

**Session Logs (Always):** End of every work session

**Knowledge Logs (Selective):**

**Discovery Logs - Create when:**
- ✅ Hit impasse (>15 min)
- ✅ AI repeatedly wrong
- ✅ Discovered non-obvious solution
- ✅ Version-specific behavior
- ✅ Found tool principle not in docs
- ❌ Worked first try, one-off issue, already obvious

**Learning Logs - Create when:**
- ✅ Had significant Q&A session about concepts
- ✅ Needed to understand how something works
- ✅ Filling knowledge gaps about tool/feature
- ✅ Building foundational understanding
- ✅ Want reference material for future use
- ✅ Meta-learning about the documentation system itself (why READMEs matter, naming conventions, etc.)
- ❌ Simple one-question clarification
- ❌ Information easily found in basic docs

**Meta-Learning Opportunities:**

Sometimes the most valuable knowledge logs are about **understanding the system itself**:
- Why certain conventions exist (e.g., README naming philosophy)
- How the documentation system works
- Best practices for organizing knowledge
- Insights about workflow and process

**When to document meta-learnings:**
- Team member asks "why do we do it this way?"
- You discover the reasoning behind a convention
- Understanding improves how you use the system
- Would help onboard new team members

**Where to put meta-learnings:**
- `resources/documentation_knowledge_logs/` — For documentation system itself
- `resources/general_development_knowledge_logs/` — For broader development practices

**Rule:** Keep building. Document when stuck OR when learning something substantial.

---

## Version Tracking

Always include:
- **Application:** Name + version (e.g., "TouchDesigner 2023.11760", "After Effects 2024.1")
- **AI Assistant:** Model + platform (e.g., "Claude 3.7 Sonnet (Cursor)")
- **Plugins/extensions:** If relevant

**Why:** Tools and AI models change. Version tracking prevents "works on my machine" issues and helps identify which AI gave which advice.

---

## Guidelines for AI Assistants

### CRITICAL: When to Create Documentation

**⚠️ ONLY create knowledge logs when the user explicitly asks for documentation.**

**DO create knowledge logs when user says:**
- "Document this" — ⚠️ ASSESS: Does the session content warrant a knowledge log? Ask user which tool/category!
- "Log this" — ⚠️ ASSESS: Does the session content warrant a knowledge log? Ask user which tool/category!
- "Log this as knowledge" ⭐ (clearest phrase - definitely create knowledge log)
- "Create a knowledge log" — (explicit, definitely create)
- "Add this to the knowledge logs" — (explicit, definitely create)
- "Document this later" — (means create knowledge log when session log is made)
- "Let's document what we learned" — ⚠️ ASSESS: Likely needs knowledge log, confirm with user
- "Create our session log" — ⚠️ ASSESS: Review session for learning/discovery moments, ask if knowledge log needed

**DO NOT create knowledge logs when user:**
- Asks a question (just answer it)
- Requests examples or explanations (provide in chat)
- Says "show me" or "give me examples" (respond in conversation)
- Wants to understand something (explain without creating files)

**The criteria in "When to Document" below are guidelines for WHAT to document when asked, not triggers to automatically create documentation.**

---

### ⚠️ IMPORTANT: "Document Later" Means Create Knowledge Log

**Common misunderstanding:** "Document later" could mean "add to session log" or "create knowledge log"

**Correct interpretation:** "Document later" = create **separate knowledge log file**

**User expectation:**
- When user says "document this later", they want a **knowledge log** created (not inline session log notes)
- Knowledge log should be created when session log is made
- Session log should reference the knowledge log with "see notes:" pattern

**Example:**

User says during session: "Document this later" (about keyboard shortcuts)

When creating session log:
1. ✅ Create knowledge log: `resources/touchdesigner_knowledge_logs/2026-02-27-0039-Keyboard-Shortcuts.md`
2. ✅ Reference in session log with "see notes:"
3. ❌ Do NOT include full details inline in session log

**Clearer phrases to avoid ambiguity:**
- "Log this as knowledge" — Clearly means create knowledge log
- "Add this to the knowledge logs" — Clearly means create knowledge log
- "Note this in the session" — Clearly means session log only

---

### When User Says "Document this" or "Log this"

1. Determine log type needed:
   - **Discovery Log:** If solving problem, AI was wrong, hit impasse
   - **Learning Log:** If Q&A session, understanding concepts, filling knowledge gaps
2. **List `resources/` folder** to discover existing `*_knowledge_logs/` folders
3. Ask which tool (if not clear)
   
   **Note on tool categorization:**
   - **Tool-specific knowledge:** Put in that tool's folder (e.g., TouchDesigner L-System behavior)
   - **General knowledge learned through a tool:** User's preference matters!
     - Option A: Create `resources/general_development_knowledge_logs/` for universal concepts
     - Option B: Put in primary tool's folder (e.g., file naming in `touchdesigner_knowledge_logs/` if that's your learning context)
   - **Meta-learning about documentation system itself:** 
     - Examples: Why READMEs matter, naming conventions, folder structure philosophy
     - Options: `resources/documentation_knowledge_logs/` or `general_development_knowledge_logs/`
     - This is valuable for teams to understand the "why" behind the system
     - Helps onboard new team members and makes system shareable
   - **Ask user:** "This applies to multiple tools. Should I create this in `touchdesigner_knowledge_logs/` (since that's your primary context) or `general_development_knowledge_logs/`?"

4. Check if `resources/[tool]_knowledge_logs/` exists
5. If missing, ask to create folder + short README (tool-specific conventions only)
6. **Read `resources/README-KNOWLEDGE-LOGS.md`** for full templates and folder index
7. Optionally read `resources/[tool]_knowledge_logs/README.md` for tool-specific conventions
8. Get timestamp: `date "+%Y-%m-%d %H%M"`
9. Create knowledge log using appropriate template from this master template:
   - **Discovery Log:** Include The Gap → Working Example → Why This Matters → Questions to Explore
   - **Learning Log:** Include all sections ESPECIALLY "Test Your Understanding" with 4-7 questions (Feynman Technique)

### When User Says "Create session log"

1. Check if `session_logs/` exists
2. **Read `session_logs/README.md`** (if exists) to understand structure
3. **List `resources/` folder** to discover existing `*_knowledge_logs/` folders
4. **Read `resources/README-KNOWLEDGE-LOGS.md`** (if exists) to get templates and folder index
5. **⚠️ CRITICAL: First, go through the session/conversation** for any notes the user asked to add. Don't start writing the log until you've reviewed the session for: "document later", "take note of this", "update the docs if this works", "remind me to document", and similar. It's easy to forget these if you skip the review.
6. **⚠️ CRITICAL: Check the session for "document later" requests** (see checklist below)
7. **Create the session log** with all sections filled in, including any "AI Rules to Create Later" or "Guides to Update Later" sections if applicable
8. **⚠️ POST-SESSION LOG WORKFLOW:** After session log is created, immediately check for undocumented items and offer to create them (see "Post-Session Log Workflow" section below)
9. **⚠️ PROACTIVE ASSESSMENT: Evaluate if session content warrants knowledge log**
   
   **Discovery process:**
   a. Review session to identify which tool(s) were primary focus
   b. Match session content to existing folders discovered in step 3:
      - TouchDesigner discussion → `touchdesigner_knowledge_logs/`
      - Unreal discussion → `unreal_knowledge_logs/`
      - General coding in TD context → user preference (ask)
   c. If multiple tools discussed, determine primary tool or ask user
   d. If no matching folder exists, ask to create it
   e. Assess if substantial learning or discovery occurred:
      - Extended Q&A (>3 questions about concepts) → suggest Learning Log
      - Problem solved (>15 min, non-obvious) → suggest Discovery Log
   
   **Then ask user:**
   "This session covered [topic] for [tool]. Should I create a knowledge log in `[tool]_knowledge_logs/`? It would be useful as reference material for [specific benefit]."
   
   - Wait for confirmation before proceeding

10. **If creating knowledge log:**
   - Read `resources/README-KNOWLEDGE-LOGS.md` for full templates (if not already read)
   - Optionally read `resources/[tool]_knowledge_logs/README.md` for tool-specific conventions
   - Get timestamp: `date "+%Y-%m-%d %H%M"`
   - Create knowledge log using appropriate template
   - Create session log with "see notes:" reference to knowledge log

11. **If no knowledge log needed:**
   - Get timestamp: `date "+%Y-%m-%d %H%M"`
   - Create session log with full details inline

12. Cross-reference any knowledge logs created during session

**⚠️ SESSION ASSESSMENT: Before Creating Session Log**

**Ask yourself these questions:**

1. **Was there substantial Q&A?** (>3 questions about concepts/how things work)
   - If YES → Likely needs Learning Log
   
2. **Did we solve a non-obvious problem?** (>15 min debugging, AI was wrong, discovered tool behavior)
   - If YES → Likely needs Discovery Log
   
3. **Did user learn foundational concepts?** (understanding principles, best practices, "why" explanations)
   - If YES → Likely needs Learning Log
   
4. **Is this knowledge reusable?** (Would user benefit from having this as reference material?)
   - If YES → Suggest knowledge log

**If any of these are YES, ask user BEFORE creating session log:**
"This session covered [topic]. Should I create a knowledge log for [tool/category]? It would be useful as reference material for [specific benefit]."

**Then proceed based on user's answer.**

---

**⚠️ CHECKLIST: Before Writing Session Log**

**FIRST: Go through the session/conversation** for any notes the user asked to add. Don't skip this — things like "document this later", "take note of this", "update the docs if this works", or "remind me to document" are easy to miss if you start writing the log without reviewing the session.

**Then run the checklist below.**

**ALWAYS check the conversation for these phrases:**
- [ ] "document this later"
- [ ] "document later"
- [ ] "log this as knowledge"
- [ ] "create a knowledge log"
- [ ] "add this to the knowledge logs"
- [ ] "will document this"
- [ ] "remind me to document"
- [ ] "take note of this" / "note this" / "note it"
- [ ] "update the docs (if this works)" / "add to the project docs"
- [ ] "update the guide" / "fix the guide" / "update instructions"
- [ ] "this doesn't match the guide" / "the guide says X but Y works"
- [ ] User shared screenshots/files and said to document
- [ ] User asked to retrieve info from another chat for documentation

**If found, CREATE SEPARATE KNOWLEDGE LOGS for those items, then reference them in the session log with "see notes:"**

**Update project docs with working solutions from this session:**

If the project maintains reference documentation (setup guides, quick reference, troubleshooting, etc.), apply any **new discoveries or solutions that worked** from this session to those docs. Update only **relevant sections** (new steps, fixes, wiring, parameters). Do not rewrite entire docs.

**Example checklist (adapt to your project):**
- [ ] Apply updates to:
  - `../resources/[Project]_Quick_Reference.md` (if exists)
  - `../resources/[Project]_Setup_Guide.md` (if exists)
  - `../resources/[Project]_Implementation_Guide.md` (if exists)
  - `../resources/[Project]_Troubleshooting.md` (if exists)
  - `../resources/[Project]_Network_Diagram.md` (if exists)
  - [Other project-specific reference docs]

**Why:** This keeps the main reference docs current so you don't have to manually update them later. When starting a new session, the setup guide already has the latest working approach.

**Living Documentation Principle:**

Guides should reflect reality through real-world testing, not just initial research. When following implementation guides:
- Note discrepancies between guide and actual tool behavior
- Say "update the guide" when you find inaccuracies  
- During session log creation, apply corrections to keep guides accurate

**Check for guide updates needed:**
- [ ] Did we discover version-specific differences? (parameters, pages, behavior)
- [ ] Did we find corrections to existing documentation?
- [ ] Did implementation steps need clarification based on actual usage?
- [ ] Are there inaccuracies between guide and current tool version?

**If YES:** Update the guide with corrections when creating session log. Document what was wrong vs what actually works.

**Also check: Did this session involve improving the documentation system?**
- [ ] We corrected AI behavior about session/knowledge log workflow
- [ ] We updated or created **Cursor rules** (`.cursor/rules/`) or **rules/instructions on another platform** → **Create an AI rules log** for the rule change and reference in session log with "see notes:"
- [ ] We updated or created README instructions (session_logs, knowledge logs, etc.)
- [ ] We clarified ambiguous phrasing in documentation system

**Whenever rules or instructions that govern the AI were updated or created:** Create an AI rules log in `ai_rules_logs/` (same timestamp as session log), document the change using the template in `ai_rules_logs/README.md`, and reference it in the session log with "see notes:". Do not skip this — applies to Cursor rules, Claude/Gemini/ChatGPT instructions, or any project rules file.

**For other documentation improvements** (README-only, phrasing clarifications): Ask user "Should I create an AI rules log for [the change]?" Then create in `ai_rules_logs/` if yes and reference in session log.

**Common "document later" items:**
- Custom rules or parameters (with screenshots)
- Keyboard shortcuts or workflow tips
- Solutions that worked after trial and error
- Information retrieved from previous chats
- Settings or configurations that user wants to remember

**Workflow:**
1. Create knowledge log in `resources/[tool]_knowledge_logs/` with same timestamp
2. Use appropriate template (Discovery Log or Learning Log)
3. Reference in session log with "see notes:" pattern

---

### Post-Session Log Workflow

**⚠️ CRITICAL: After creating a session log, automatically create undocumented items without asking.**

**This workflow prevents breaking the user's flow during discovery while ensuring everything gets documented.**

**🔧 ENFORCEMENT: For this workflow to work reliably in every conversation (even fresh ones), create a Cursor rule:**

Create `.cursor/rules/session-log-workflow.mdc` with `alwaysApply: true` that enforces these steps automatically. Without this rule, the workflow only works if the AI happens to have the project READMEs in context.

**After session log is created, automatically do this:**

1. **Check "Knowledge Logs to Create Later" section** - If any items have "📝 To document" status:
   - **Automatically create** all knowledge logs in `resources/[tool]_knowledge_logs/` (don't ask)
   - Use same timestamp as session log
   - Update session log's "Knowledge Logs to Create Later" section to "Knowledge Logs Created" with ✅ status

2. **Check "AI Rules to Create Later" section** - If any rules have "📝 To document" status:
   - **Automatically create** all AI rules logs in `ai_rules_logs/` (don't ask)
   - Use same timestamp as session log
   - Update session log's "AI Rules to Create Later" section to "AI Rules Logs Created" with ✅ status

3. **Check "Guides to Update Later" section** - If guide corrections are listed:
   - Ask: "Should I update the guides now with the corrections we found?"
   - If yes, apply corrections to guides
   - If no, note for next session

**Do NOT ask for confirmation on steps 1-2** - user already said "document" when requesting session log. Only ask for guide updates (step 3) since those modify existing documentation.

**Exception:** If 5+ items to create, confirm first: "I have 6 knowledge logs to create. Proceed?"

**Why this matters:** 
- Doesn't interrupt flow during active discovery/implementation
- Ensures all preferences, discoveries, and learnings get properly documented
- Converts "to do later" items into actual documentation
- No redundant confirmation questions
- Works consistently across all conversations via Cursor rule

**User's insight:** "I want to make sure that whenever I was asking to document this and that and create ai rules will be done after the session logs. Sure I can ask to do it on the spot but that breaks the flow of our session to discover what works or not."

---

### Post-Session Knowledge Log Creation

**If user requests additional knowledge logs AFTER session log is written:**

**Scenario:** User reviews session log and says: "I liked [specific solution/approach]. Should we create a knowledge log for that?"

**Workflow:**
1. **Create the knowledge log** — Use same timestamp as session log (YYYY-MM-DD-HHMM)
2. **Update the session log** — Add new knowledge log to "Knowledge Logs Created" section with "see notes:" reference
3. **Keep it accurate** — Session log should reflect ALL knowledge logs from that session

**Example:**
```markdown
## Knowledge Logs Created

- `resources/touchdesigner_knowledge_logs/2026-03-04-2213-Script-CHOP-Callback-Names.md` — `cook` vs `onCook`, `onGetCookLevel`, API fixes.
- `resources/touchdesigner_knowledge_logs/2026-03-04-2213-Constant-CHOP-With-Expression.md` — Constant CHOP approach for simple outputs (added post-session).
```

**Why:** Future reference shows complete picture of session's knowledge output; timestamp matching makes cross-referencing easy.

**Note for project-specific READMEs:** When setting up a new project, include this post-session workflow in both `session_logs/README.md` and `resources/README-KNOWLEDGE-LOGS.md` so the AI knows to update session logs when additional knowledge logs are created later.

**Format in session log:**
```markdown
### 1. Documented [Item Name] ✅

**Summary:** User requested documentation of [what it is]. Created knowledge log with [what's included].

**Application:** [Tool name]

**see notes:** `../resources/[tool]_knowledge_logs/YYYY-MM-DD-HHMM-Title.md` for [complete details, examples, analysis, etc.]
```

**DO NOT include full details inline in session log - use "see notes:" to reference the knowledge log.**

---

### Enforcing Post-Session Workflow with Cursor Rules

**Problem:** The Post-Session Log Workflow only works if the AI has the project READMEs in context. In fresh conversations, the AI might not know to automatically create knowledge logs after the session log.

**Solution:** Create a Cursor rule that enforces the workflow in every conversation.

**Create `.cursor/rules/session-log-workflow.mdc`:**

```markdown
---
description: Post-session log workflow - automatically create knowledge logs after session log
alwaysApply: true
---

# Post-Session Log Workflow

When user says "create session log" or "document this session":

## Step 1: Create the Session Log

Follow the template in `session_logs/README.md`

## Step 2: Immediately Check for Undocumented Items

After creating the session log, check these sections:

### Check "Knowledge Logs to Create Later"
- If any items have "📝 To document" status
- Create each knowledge log in appropriate folder (`resources/[tool]_knowledge_logs/`)
- Use same timestamp as session log

### Check "AI Rules to Create Later"  
- If any items have "📝 To document" status
- Create each AI rule log in `ai_rules_logs/`
- Use same timestamp as session log

### Check "Guides to Update Later"
- Ask: "Should I update the guides now?"
- Apply corrections if yes

## Step 3: Update Session Log

After creating the logs, update the session log:
- Convert "To Create Later" sections to "Created" sections
- Change "📝 To document" to ✅ with file paths

## Important

- Do NOT ask "want me to create those logs?" - just create them
- User already said "document" when requesting session log
- Only exception: if 5+ items, confirm first
```

**Why this is necessary:**
- Cursor rules are loaded into every conversation automatically
- Project READMEs are only loaded if recently viewed or explicitly referenced
- The rule ensures consistent behavior regardless of conversation history
- Makes the workflow reliable and automatic

**When to create this rule:** During project setup, or when you notice the AI isn't following the Post-Session Log Workflow consistently.

---

### ⚠️ Common Mistake: Missing Knowledge Log Opportunities

**Scenario:** User says "document this and create session log" after a substantial conversation

**What AI might miss:** The session itself contained learning or discovery that warrants a separate knowledge log, not just a session log.

**Pattern to recognize:**

| Session Type | Indicators | What Gets Missed |
|--------------|------------|------------------|
| **Extended Q&A** | User asks 2-3+ "why" or "how" questions about concepts | Learning Log opportunity |
| **Problem-solving** | Tried multiple approaches, AI suggestions didn't work initially | Discovery Log opportunity |
| **Best practices discussion** | User asks about conventions, workflows, or "right way to do X" | Learning Log opportunity |
| **Tool behavior exploration** | User curious about why tool works a certain way | Learning Log for that tool |

**Example pattern:**
1. User asks conceptual question ("Why does X work this way?")
2. AI provides detailed explanation with examples and context
3. User follows up with clarifying questions
4. Conversation reaches 5-10+ message exchanges
5. User says: "Document this and create session log"

**What AI incorrectly does:**
- Creates only session log with inline details
- Misses that this substantial Q&A is reusable reference material

**Correct workflow:**
1. **Pause and assess:** "This was a substantial learning conversation about [topic]"
2. **Ask user:** "Should I create a knowledge log for [tool/category]? This would be useful as reference material when you encounter [related situation] in future projects."
3. **Offer tool categorization:** "Since you're learning this in the context of [primary tool], I can put it in `[tool]_knowledge_logs/` even though it applies more broadly."
4. **Wait for confirmation**, then create both logs with cross-references

**Key insight:** When user says "document this" after multiple exchanges, it often signals "this whole conversation was valuable" — not just "record that we talked."

---

### When User Says "Document later" or "Log this as knowledge"

**IMPORTANT CLARIFICATION:** These phrases mean create a **knowledge log**, not just add to session log.

**Phrases that mean "create knowledge log":**
- "Document this later"
- "Document later"  
- "Log this as knowledge"
- "Create a knowledge log for this"
- "Add this to the knowledge logs"
- "Document this in a knowledge log"

**What it means:** Document later = create a **knowledge log** when they ask for the session log, not now. We're still learning/discovering, so don't create files yet.

**Workflow:**

1. **When they say "document later" or "log this as knowledge":** 
   - Note what they want documented (track it mentally or in context)
   - Don't create knowledge logs or files yet
   - Remember this is for a **knowledge log**, not just session log notes

2. **When they ask for a session log:** 
   - Look back in the session/conversation for any "document later" or "log as knowledge" requests
   - **Create separate knowledge logs** for those items in `resources/[tool]_knowledge_logs/`
   - Reference the knowledge logs in the session log using **"see notes:"** pattern
   - Write the session log for the **whole** session: reference the knowledge logs + everything that happened after

**Key point:** "Document later" items should become **separate knowledge log files**, referenced in the session log with "see notes:", not included inline in the session log.

### Critical Reminder for Learning Logs

**NEVER skip the "Test Your Understanding" section in Learning Logs!**

This section is essential for verifying comprehension (Feynman Technique). Include:
- 4-7 questions testing different aspects (core concept, how it works, practical use, edge cases)
- "Challenge yourself" prompt to explain in simple terms
- Questions should reveal gaps if user can't answer them simply

### Cross-Platform Usage

**Cursor:** `.cursor/rules/` for auto-triggering  
**Claude Projects:** Add to project knowledge  
**ChatGPT:** Add to custom instructions  
**Gemini:** Add to system instructions  

**Session log and AI rules log workflows apply on any platform.** When you ask for a session log, the AI should: review the session for notes to add, run the checklist, update project docs if the project maintains them, and create an AI rules log whenever rules/instructions were updated (whether Cursor rules, platform custom instructions, or a project rules file). Same "see notes:" pattern everywhere.

**Universal convention:**
- File naming: `YYYY-MM-DD-HHMM-Title.md`
- Session logs: `session_logs/`
- Knowledge logs: `resources/[tool]_knowledge_logs/`
- Always read folder READMEs before creating files

---

## Folder Structure Example

```
project/
├── session_logs/                                    ← What happened each session
│   ├── README.md                                    ← Session log template and guidelines
│   └── 2026-02-21-1530-Initial-Setup.md
├── ai_rules_logs/                                   ← How AI learned the system
│   ├── README.md                                    ← AI rules log template and guidelines
│   ├── 2026-02-24-1120-Session-Log-Timing.md
│   └── 2026-02-28-1910-Document-Later-Clarification.md
├── resources/
│   ├── README-KNOWLEDGE-LOGS.md                     ← Master index + full templates (READ THIS FIRST)
│   ├── [other resource files/folders]               ← Unrelated to knowledge logs
│   ├── touchdesigner_knowledge_logs/
│   │   ├── README.md                                ← Tool-specific conventions (short)
│   │   └── 2026-02-21-1545-Feature-Discovery.md
│   └── unreal_knowledge_logs/
│       ├── README.md                                ← Tool-specific conventions (short)
│       └── 2026-02-22-0915-Workflow-Pattern.md
├── .cursor/rules/                                   ← Cursor-specific rules (auto-applies)
│   ├── knowledge-log-use-project-system.mdc
│   └── check-document-later-requests.md
├── .ai_rules/                                       ← Platform-agnostic AI rules (optional)
│   ├── README.md                                    ← How to use these rules
│   ├── session-log-workflow.md                      ← Session log creation rules
│   └── knowledge-log-workflow.md                    ← Knowledge log creation rules
└── [project files]
```

**Hybrid README Approach:**

- **`session_logs/README.md`** — Standard name (folder is single-purpose)
- **`resources/README-KNOWLEDGE-LOGS.md`** — Specific name (resources/ contains other things)
- **`[tool]_knowledge_logs/README.md`** — Standard name (folder is single-purpose)

**Token efficiency:**
- Read `README-KNOWLEDGE-LOGS.md` once → get full templates + see all folders (~200-300 lines)
- Read tool README only if needed → get tool conventions (~30-40 lines)
- Don't re-read full template for each tool

**Why this structure:**
- Self-documenting: Each folder explains itself
- Shareable: Folders can be shared with team independently
- Discoverable: List `resources/` to see all `*_knowledge_logs/` folders
- Efficient: Master README prevents duplication of full templates

---

## Multi-Tool Projects

When projects span multiple applications, create separate knowledge log folders for each tool. Cross-reference related logs:

```markdown
**Related logs:**
- `resources/tool_a_knowledge_logs/2026-02-21-1530-Export-Settings.md`
- `resources/tool_b_knowledge_logs/2026-02-21-1545-Import-Settings.md`
```

---

**Last updated:** 2026-03-25  
**Version history:** See `readme_project_session_and_tool_knowledge_logs_VERSION_HISTORY.md` (same folder) — kept in a separate file to reduce token load when using this master for project setup and logs.
