---
name: session-log-companion
description: Comprehensive project session companion for documenting work sessions, creating knowledge logs when discovering or learning something, teaching agent preferences, and improving collaboration. Use when user says "start a session", "create session log", "summarize this session", "document this discovery", "create a knowledge log", "I want to improve how you work with me", "remember this preference", "let's continue", "continue from last session", "pick up where we left off", "what should I work on next", or any session/documentation-related request. Also trigger when user mentions being stuck, hitting an impasse, needing to understand concepts, or wanting to capture learnings.
---

# Session Log Companion (SLC)

A comprehensive companion for project sessions that helps you document your work, capture discoveries and learnings, teach the agent your preferences, and build a knowledge base that improves collaboration over time.

**Abbreviation:** SLC - Use this when referencing this skill in documentation or conversation.

## When to Use This Skill

This skill triggers for four main scenarios:

1. **Starting a session** - "start a session", "begin session log", "let's work on X"
2. **Continuing a session** - "let's continue", "continue from last session", "pick up where we left off", "what should I work on next"
3. **Creating knowledge logs** - "document this", "create a knowledge log", "I'm stuck", "can you explain how X works"
4. **Teaching preferences** - "I want to improve how you work with me", "remember this preference", "I prefer X style"
5. **Ending a session** - "summarize this session", "create session log", "wrap up"

## Enforcement Rule

**When user requests any action covered by this skill's four workflows, you MUST follow the complete workflow steps - do not create files or take shortcuts directly.**

Key checkpoints:
- **Continue session** → Always ask intention first, then time available, before scanning session logs (Steps 1-2 of Workflow 1b)
- **Knowledge logs** → Always ask "Which tool should I document this for?" before creating (Step 3 of Workflow 2)
- **Preference logs** → Always offer Cursor rules integration after creating (Step 3 of Workflow 3)
- **Session logs** → Always check for undocumented items before finalizing (Step 2 of Workflow 4)

If you find yourself about to create a log file without following the workflow steps, stop and restart with Step 1 of the appropriate workflow.

**Why this matters:** Skipping workflow steps breaks folder organization, misses user preferences, and creates inconsistent documentation across projects.

## Core Workflows

### Workflow 1: Starting a Session

When the user wants to begin a work session:

1. **Capture session intent:**
   - Ask: "What's the focus of this session?"
   - Note the current timestamp: `date "+%Y-%m-%d %H%M"`
   - Identify the project context (current directory, open files)

2. **Set documentation expectations:**
   - Remind: "I'll help document discoveries and learnings as we work"
   - Explain: "Just say 'document this' when you hit something worth capturing"

3. **Begin work:**
   - Proceed with the user's stated goal
   - Stay alert for moments worth documenting (impasses, discoveries, learning opportunities)

**Note:** Starting a session does not create a session log file. Session logs are created in Workflow 4 when the user says "Summarize this session" at the end of a session.

**Example interaction:**

User: "Start a session for building a TouchDesigner particle system"

Agent: "Got it! We're starting a session on TouchDesigner particle systems. I'll help document any discoveries or learnings as we work. What's the first thing you want to tackle?"

---

### Workflow 1b: Continuing a Session

When the user says "let's continue", "pick up where we left off", "what should I work on next", or similar:

#### Step 1: Ask Intention

Ask: "What do you want to work on?"

The user may already know exactly what they want to do (from a session hours ago, or an idea they had offline). Let them state it first — don't dump a list of options before they've had a chance to think.

#### Step 2: Ask Time Available

Ask: "How much time do you have?"

This scopes what's realistic. A 10-minute session is different from an hour — don't suggest deep refactoring work for a quick session.

#### Step 3: Scan Recent Session Logs

Read the last 5 session logs in `session-logs/` (sorted by filename, most recent first). Extract the **Next Steps** section from each.

**If user stated a clear intention** → Match their intention against the collected Next Steps. Surface any relevant items and note which session they came from. This helps the user see connections they might have forgotten ("Oh right, that's related to what I was doing last week").

**If user draws a blank** → Present the Next Steps from recent sessions as a menu of options, grouped by session. Let the user pick what feels right.

#### Step 4: Scope to Time

Based on the time available, help the user pick a realistic slice:
- **10 min** → one small, contained task (a single next step item, a quick note, a review)
- **20-30 min** → one substantial task or 2-3 small ones
- **1+ hour** → a full work block, potentially spanning multiple next steps

Don't over-plan — just confirm the focus and begin.

#### Step 5: Begin Work

Proceed with Workflow 1 (set documentation expectations, stay alert for moments worth documenting). The continue workflow feeds into the regular session flow.

**Example interactions:**

User: "Let's continue"

Agent: "What do you want to work on?"

User: "The deep modules thing for TD containers"

Agent: "How much time do you have?"

User: "About 20 minutes"

Agent: *Scans last 5 session logs, finds relevant Next Steps from 2026-05-20-0219*

Agent: "From your last session, you had these next steps related to that:
- Decide whether to create a separate `/td-deepen-architecture` skill or fold it into TSC
- Adapt the vocabulary mapping into a proper SKILL.md
- Test the deletion test against real TD scaffold outputs

With 20 minutes, we could tackle the first decision and sketch the outline if you go separate skill. Want to start there?"

---

User: "What should I work on next?"

Agent: "What are you thinking? Anything specific on your mind?"

User: "Not really, just have some time"

Agent: "How much time?"

User: "Like an hour"

Agent: *Scans last 5 session logs, presents Next Steps grouped by session*

Agent: "Here's what's open from recent sessions:
**From 2026-05-20 (Deep Modules Research):**
- Decide on separate skill vs folding into TSC
- Test deletion test against real TD scaffolds

**From 2026-05-20 (First Complete Draft):**
- [items from that session's next steps]

What catches your eye?"

---

### Workflow 2: Creating Knowledge Logs

When the user wants to document something or you detect a documentation opportunity:

#### Step 1: Detect Log Type

Analyze the user's language and context to suggest the appropriate log type:

**Discovery Log indicators:**
- User says: "stuck", "not working", "error", "impasse", "AI suggested X but Y works"
- Context: Spent >15 min on problem, found non-obvious solution, AI was wrong
- Pattern: Problem → Solution flow

**Learning Log indicators:**
- User says: "explain", "how does", "understand", "what is", "can you teach me"
- Context: Q&A session, building foundational knowledge, filling gaps
- Pattern: Question → Understanding flow

**If unclear:** Ask the user which type fits better.

#### Step 2: Gather Information

**For Discovery Logs:**
- What were you trying to do?
- What did the AI suggest (if applicable)?
- What broke or didn't work?
- What actually works?
- What tool/version are you using?

**For Learning Logs:**
- What did you need to understand?
- Why does it matter to your project?
- What questions did you have?
- What concepts did we cover?

#### Step 3: Determine Folder Location

Ask: "Which tool should I document this for?"

**Folder naming convention:** `resources/[tool]-knowledge-logs/`

Examples:
- TouchDesigner → `resources/touchdesigner-knowledge-logs/`
- After Effects → `resources/aftereffects-knowledge-logs/`
- General development → `resources/general-development-knowledge-logs/`

Create the folder if it doesn't exist.

#### Step 4: Create the Knowledge Log

1. Generate timestamp: `date "+%Y-%m-%d %H%M"`
2. Ask for a brief title (or suggest one based on topic)
3. Read the appropriate template:
   - Discovery: `references/discovery-log-template.md`
   - Learning: `references/learning-log-template.md`
   - **If not found in the project directory**, read from the global install: `~/.claude/skills/session-log-companion-v1/references/`
4. Fill in the template with information gathered
5. Include any commands used in the "Commands Used" section
6. Save to: `resources/[tool]-knowledge-logs/YYYY-MM-DD-HHMM-Brief-Title.md`

#### Step 5: Offer to Update COMMANDS.md

After creating the knowledge log, if commands were used:

Ask: "Would you like me to add any of these commands to `references/COMMANDS.md` for future reference?"

If yes:
1. Read `references/COMMANDS.md`
2. Add the command(s) to the "Custom Commands" table
3. Include context about when/why to use them

**Example interaction:**

User: "I'm stuck with this camera CHOP chain - it's not driving the camera. Document this."

Agent: "This sounds like a Discovery Log (you hit an impasse). Which tool should I document this for - TouchDesigner?"

User: "Yes"

Agent: *Creates discovery log at `resources/touchdesigner-knowledge-logs/2026-03-07-1430-Camera-CHOP-Chain-Not-Driving-Camera.md`*

Agent: "I noticed you used `touchdesigner -debug` to solve this. Want to add it to COMMANDS.md?"

---

### Workflow 3: Teaching Agent Preferences

When the user wants to teach you their preferences or improve collaboration:

#### Step 1: Identify the Preference

Listen for preferences about:
- **Communication style:** Technical depth, formality, verbosity
- **Documentation patterns:** How detailed, what structure
- **Code commenting:** When and how to comment
- **Explanation style:** Analogies vs theory, examples vs concepts
- **Workflow patterns:** How they like to work, what to assume

#### Step 2: Create Preference Log

1. Generate timestamp: `date "+%Y-%m-%d %H%M"`
2. Create folder if needed: `resources/agent-companion-preference-logs/`
3. Document the preference with:
   - What the preference is
   - Why it matters to the user
   - Examples of good vs bad
   - When to apply it
4. Save to: `resources/agent-companion-preference-logs/YYYY-MM-DD-HHMM-Preference-Title.md`

**Template for preference logs:**

```markdown
# [Preference Title]

**Date:** YYYY-MM-DD  
**Time:** HHMM  
**Category:** [Communication/Documentation/Code/Explanation/Workflow]  
**Type:** Agent Preference

---

## The Preference

**What:** [Clear statement of the preference]

**Why:** [Why this matters to the user]

---

## Good Examples

**Example 1:**
[What this looks like when done right]

**Example 2:**
[Another good example]

---

## Avoid

**Example 1:**
[What NOT to do]

**Why it's wrong:** [Explanation]

---

## When to Apply

[Contexts where this preference matters]

---

## Notes

[Any additional context or exceptions]

---

## Commands (if applicable)

**If this preference involves commands, list them here:**
- `[command]` - [When/how to use it]

**see commands:** `references/COMMANDS.md` for full command reference
```

#### Step 3: Check for Command Preferences

If the preference involves commands or workflows:

Ask: "Should I add this command to `references/COMMANDS.md` for easy reference?"

If yes:
1. Read `references/COMMANDS.md`
2. Add the command to the "Custom Commands" table
3. Note the preference in the command's "Notes" column

#### Step 4: Offer Cursor Rules Integration

If the user is in Cursor, ask:

"Would you like me to also add this to `.cursor/rules/` so it's automatically enforced in Cursor?"

If yes:
1. Create or update `.cursor/rules/preferences.md`
2. Add a rule that references the preference log
3. Format: "See `resources/agent-companion-preference-logs/[filename]` for details"

**Example interaction:**

User: "I prefer more technical explanations with less hand-holding. Don't explain basic concepts unless I ask."

Agent: "Got it. I'll document this preference. This is about communication style - you want me to assume technical knowledge and skip basics unless requested."

*Creates preference log*

Agent: "Would you like me to also add this to `.cursor/rules/` so it's automatically enforced in Cursor?"

---

### Workflow 4: Ending/Summarizing a Session

When the user wants to wrap up and create a session log:

#### Step 1: Prepare

1. Check if `session-logs/` exists
2. **Read `session-logs/README.md`** (if exists) to understand structure
3. **List `resources/` folder** to discover existing `*-knowledge-logs/` folders
4. **Read `resources/README-KNOWLEDGE-LOGS.md`** (if exists) to get templates and folder index

#### Step 2: Review the Session for "Document Later" Requests

**⚠️ CRITICAL: Go through the entire session/conversation BEFORE writing the log.** Don't start writing until you've reviewed for items the user asked to add.

**Check for these phrases:**
- "document this later" / "document later"
- "log this as knowledge"
- "create a knowledge log" / "add this to the knowledge logs"
- "will document this" / "remind me to document"
- "take note of this" / "note this" / "note it"
- "update the docs (if this works)" / "add to the project docs"
- "update the guide" / "fix the guide" / "update instructions"
- "this doesn't match the guide" / "the guide says X but Y works"
- User shared screenshots/files and said to document
- User asked to retrieve info from another chat for documentation

**If found:** These become **separate knowledge log files**, referenced in the session log with "see notes:" — NOT included inline in the session log.

#### Step 3: Session Assessment

**Ask yourself these questions before creating the session log:**

1. **Was there substantial Q&A?** (>3 questions about concepts) → Likely needs Learning Log
2. **Did we solve a non-obvious problem?** (>15 min debugging, AI was wrong) → Likely needs Discovery Log
3. **Did user learn foundational concepts?** (understanding principles, "why" explanations) → Likely needs Learning Log
4. **Is this knowledge reusable?** (Would user benefit from reference material?) → Suggest knowledge log

**If any are YES, ask user BEFORE creating session log:**
"This session covered [topic] for [tool]. Should I create a knowledge log in `[tool]-knowledge-logs/`? It would be useful as reference material for [specific benefit]."

Wait for confirmation before proceeding.

#### Step 4: Generate Session Log

1. Generate timestamp: `date "+%Y-%m-%d %H%M"`
2. Read the session log template: `references/session-log-template.md` (if not found in project, use `~/.claude/skills/session-log-companion-v1/references/session-log-template.md`)
3. Fill in all sections based on session review
4. Use "see notes:" pattern to reference any knowledge logs created
5. Include "AI Rules to Create Later" or "Guides to Update Later" sections if applicable
6. **Always include an "Honest Self-Assessment" section** — see required sections below
7. **Always end with a "Session Insight" section** — see required sections below
8. Save to: `session-logs/YYYY-MM-DD-HHMM-Session-Title.md`

**Required sections (always include):**

- **Honest Self-Assessment** — placed after testing/accomplishments and before "Carry Forward to Next Session." Names what didn't work, what's untested, what's parked, and what the agent or user might be pattern-matching ahead of evidence. The point is to prevent future-self from reading the log and assuming everything was settled when it wasn't. Keep it short — 2–4 honest bullet points or a short paragraph. If the session genuinely had no caveats worth flagging, write "No significant caveats — everything tested was validated by results" rather than skipping the section.

- **Session Insight** — the final section of every session log. One sentence (not a list, not a paragraph) on what changed about how the user works, or what design principle the session surfaced. The constraint of "one sentence" is the design — it forces a *meta* observation rather than a recap. If you can't condense it to one sentence, the insight isn't ready yet.

**Key principles for session logs:**
- Keep it concise - use "see notes:" to reference detailed documentation
- Cross-reference knowledge logs by timestamp
- Only list project files in "Files Created/Modified" (not the logs themselves)
- Capture the "why" behind decisions, not just the "what"
- Capture the texture of the session, not just the outputs — the *how* of the work is what makes logs worth re-reading later
- Leave "USER_FILL_WHAT_AI_MODEL_NAME_WAS_USED" as-is (the agent cannot detect the model name in Cursor; the user will fill it in manually from their model selector)

**Note on template file:** If `references/session-log-template.md` exists in the project, it should also be updated to include the Honest Self-Assessment and Session Insight sections so the template and this SKILL.md stay aligned.

**Documenting code/expressions:** When including code snippets, expressions, scripts, or configurations in session logs, always include context: **Where used** (which file/operator/parameter), **What it does** (brief explanation), and **How it connects** (integration with the rest of the system). Code without context is hard to reuse.

#### Step 5: Update Project Docs

If the project maintains reference documentation (setup guides, quick reference, troubleshooting, implementation guides, etc.), apply any **new discoveries or solutions that worked** from this session to those docs. Update only relevant sections — do not rewrite entire docs.

**Living Documentation Principle:** Guides should reflect reality through real-world testing, not just initial research. Check for guide updates needed:

- Did we discover version-specific differences? (parameters, pages, behavior)
- Did we find corrections to existing documentation?
- Did implementation steps need clarification based on actual usage?
- Are there inaccuracies between guide and current tool version?

**If YES:** Update the guide with corrections. Document what was wrong vs what actually works. Add to the "Guides Updated" section of the session log.

#### Step 6: Check for AI Rules Log Need

**Did this session involve improving the documentation system or updating AI rules?**

- Updated or created **Cursor rules** (`.cursor/rules/`) or **rules/instructions on another platform** → **Always create an AI rules log** (don't ask, don't skip)
- Corrected AI behavior about session/knowledge log workflow → Create AI rules log
- Updated/created README instructions → Ask if AI rules log is needed
- Clarified ambiguous phrasing in documentation system → Ask if AI rules log is needed

**When creating:** Save to `ai_rules_logs/YYYY-MM-DD-HHMM-Brief-Description.md` using the template in `ai_rules_logs/README.md`, and reference in session log with "see notes:".

#### Step 7: Post-Session Log Workflow

**⚠️ CRITICAL: After the session log is created, immediately check for undocumented items and offer to create them.**

This workflow prevents breaking the user's flow during discovery while ensuring everything gets documented.

**Check these sections of the session log:**

1. **"AI Rules to Create Later" section** — If any rules are listed with "📝 To document" status:
   - Say: "I noticed we have [N] AI rules to document. Want me to create those AI rules logs now?"
   - If yes, create each AI rule log in `ai_rules_logs/` folder using same timestamp
   - Update session log's section to show ✅ status

2. **"Knowledge Logs Created" section** — If discoveries/learnings happened but no logs were created:
   - Say: "I noticed we discovered [X]. Should I create a knowledge log for this?"
   - If yes, create appropriate knowledge log in `resources/[tool]-knowledge-logs/`
   - Update session log to include the new knowledge log

3. **"Guides to Update Later" section** — If guide corrections are listed:
   - Say: "Should I update the guides now with the corrections we found?"
   - If yes, apply corrections to guides
   - If no, note for next session

**Why this matters:** Doesn't interrupt flow during active discovery/implementation. Converts "to do later" items into actual documentation. User can choose to defer if in a hurry.

#### Step 8: Offer to Update COMMANDS.md

After creating the session log, if useful commands were used:

Ask: "Would you like me to add any of the commands from this session to `references/COMMANDS.md`?"

If yes:
1. Read `references/COMMANDS.md`
2. Add the command(s) to the "Custom Commands" table
3. Include context about the session where they were useful

#### Step 9: Confirm Completion

Summarize what was documented:
- Session log location
- Knowledge logs created (with links)
- Preference logs created (if any)
- AI rules logs created (if any)
- Guides updated (if any)

#### Post-Session Knowledge Log Creation

**If user requests additional knowledge logs AFTER session log is written:**

1. **Create the knowledge log** — Use same timestamp as session log
2. **Update the session log** — Add new knowledge log to "Knowledge Logs Created" section with "see notes:" reference and "(added post-session)" notation
3. **Keep it accurate** — Session log should reflect ALL knowledge logs from that session

**Example interaction:**

User: "Summarize this session"

Agent: *Reviews conversation, checks for "document later" items, identifies accomplishments*

Agent: "Before I create the session log — this session had substantial Q&A about [topic]. Should I create a knowledge log for that?"

User: "Yes"

Agent: *Creates knowledge log, then session log with "see notes:" cross-reference*

Agent: *Checks post-session items:* "I noticed we have 2 AI rules to document from this session. Want me to create those now?"

User: "Yes"

Agent: *Creates AI rules logs, updates session log*

Agent: "Session documented! Created:
- Session log: `session-logs/2026-03-07-1430-TouchDesigner-Particle-System-Build.md`
- Knowledge log: `resources/touchdesigner-knowledge-logs/2026-03-07-1430-Camera-CHOP-Chain-Fix.md`
- AI rules log: `ai_rules_logs/2026-03-07-1430-Session-Log-Timing-Rule.md`"

---

## AI Rules Logs

**Purpose:** Track how AI assistants learn to work with your documentation system. Capture improvements and corrections so they're portable across projects and platforms.

**Folder:** `ai_rules_logs/` at project level (visible, not hidden — matches `session-logs/` pattern)

**File format:** `YYYY-MM-DD-HHMM-Brief-Description.md`

**Create when:**
- Updated or created Cursor rules (`.cursor/rules/`) → always create (don't skip)
- Updated rules/instructions on another platform (Claude Projects, ChatGPT, Gemini) → always create
- Corrected AI behavior about documentation workflows
- Updated/created README instructions (session_logs, knowledge logs, etc.)
- Clarified ambiguous phrasing in documentation system

**Don't create when:**
- One-time correction specific to current project task
- Session was about project work only (no documentation system changes)
- AI made a simple mistake that won't repeat

**Workflow:** When creating a session log after discussing rule improvements, create the AI rules log in `ai_rules_logs/` and reference in session log with "see notes:". If Cursor rules or rules on any other AI platform were updated, always create an AI rules log. For README-only or phrasing changes, ask the user first.

**Template:** Read `ai_rules_logs/README.md` in the project for the full template.

---

## Use with Any AI or Platform

These instructions apply whether using Cursor, Claude, Gemini, ChatGPT, or another AI. The core workflow is the same: review the session for notes to add, run the checklist (document later → knowledge logs, update project docs if applicable, AI rules log if rules/instructions were updated). If your platform uses a different place for rules (e.g. not `.cursor/rules/`), treat updates there the same way — create an AI rules log and reference it in the session log with "see notes:".

---

## Smart Defaults

To make the workflows smooth, use these smart defaults:

**Timestamps:**
- Always generate with: `date "+%Y-%m-%d %H%M"`
- Use same timestamp for cross-referencing related logs

**Project context:**
- Detect current directory and open files
- Suggest tool based on file extensions (.toe = TouchDesigner, .aep = After Effects, etc.)

**Pre-fill known info:**
- AI model: Leave as `WHAT_AI_MODEL_USED?` (agent cannot detect model in Cursor; user fills in manually)
- AI platform: Cursor (or current platform)
- Date: Current date

**Folder creation:**
- Create `session-logs/` if it doesn't exist
- Create `resources/[tool]-knowledge-logs/` as needed
- Create `resources/agent-companion-preference-logs/` as needed
- Create `ai_rules_logs/` as needed

---

## Cross-Referencing System

Use timestamp-based cross-referencing to link related documentation:

**Example:**
1. Session at `2026-03-07 14:30`
2. Session log: `session-logs/2026-03-07-1430-Session-Title.md`
3. Knowledge log: `resources/touchdesigner-knowledge-logs/2026-03-07-1430-Discovery-Title.md`
4. Both share `2026-03-07-1430` → instant match

**In session logs, use "see notes:" pattern:**

```markdown
**see notes:** `resources/touchdesigner-knowledge-logs/2026-03-07-1430-Discovery-Title.md` for complete technical details
```

---

## Platform Awareness

### Cursor-Specific Features

When the user is in Cursor:
- Offer to create `.cursor/rules/` files for preferences
- Reference `.cursor/rules/` in examples
- Explain that rules persist across all Cursor sessions

### Platform-Agnostic Core

The core system works everywhere:
- Preference logs are portable (work with Claude.ai, ChatGPT, Gemini, etc.)
- Session logs and knowledge logs are just markdown files
- Other platforms have similar systems:
  - **Claude.ai:** Project instructions
  - **ChatGPT:** Custom instructions
  - **Windsurf/Cline:** Similar to Cursor

---

## Reference Files

This skill bundles several reference files for detailed templates:

- `references/discovery-log-template.md` - Full Discovery Log structure
- `references/learning-log-template.md` - Full Learning Log structure
- `references/session-log-template.md` - Full Session Log structure
- `references/master-template.md` - Complete documentation system guide

Read these files when you need the full template structure or additional guidance.

---

## Important Notes

**Do NOT auto-create logs without user request:**
- Only create knowledge logs when user explicitly asks
- The criteria (impasse, AI wrong, etc.) describe WHAT to document, not WHEN to automatically create logs
- Always wait for user to say "document this" or similar

**Keep the user in control:**
- Ask which log type if unclear
- Ask which tool to document for
- Confirm before creating Cursor rules
- Let user review and edit logs

**Explain the "why":**
- Help users understand why they might want to document something
- Explain the benefit of different log types
- Show how the system improves collaboration over time

---

## Success Criteria

This skill succeeds when:

1. Users can start sessions with clear documentation intent
2. Knowledge logs are created quickly without thinking about structure
3. Preferences are captured in a portable, reusable way
4. Session summaries are comprehensive yet concise
5. Cross-referencing via timestamps works seamlessly
6. The knowledge base improves collaboration over time