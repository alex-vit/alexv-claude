---
name: reflect
description: Capture lessons learned as behavioral rules in ~/.claude/CLAUDE.md
user-invocable: true
---

# Reflect

Pause and look back at recent work. Identify lessons — what worked, what didn't, what was surprising — and write them as concise behavioral rules into `~/.claude/CLAUDE.md`. The goal is durable behavior change, not documentation.

## Triggers

Besides explicit `/reflect` invocation, reflect proactively when:
- A non-trivial task or feature is completed
- After commits and pushes (natural checkpoints)
- Switching context to a different project or task
- Session winding down
- **The user corrects a repeated mistake** — "you keep doing X wrong", "I told you not to do Y", "stop doing Z". This is the strongest signal. Capture the anti-pattern as a rule immediately.
- **Trial-and-error sequences** — multiple failed attempts followed by a success (wrong API calls, incorrect tool usage, searching several paths before finding the right one). The successful approach should be captured as a rule so future sessions skip straight to it.
- User asks "what did we learn", "how did that go", "what could be better", "any takeaways", etc.

## What a reflection produces

Not prose, not notes — **rules**. Short, actionable directives that match the existing style of `~/.claude/CLAUDE.md` (single-line bullets under section headers). Examples:

- `- Prefer X over Y when Z.`
- `- Always check for A before doing B.`
- `- When the user says C, they mean D.`

Rules should be:
- **Positive form** where possible: "do X" rather than "don't do Y"
- **Specific**: tied to a concrete behavior, not vague advice
- **Terse**: one line, no explanation needed

## Process

1. **Gather context** — review what happened since the last reflection or session start. Check recent conversation, commits, and notes files (if the `notes` skill is in use) for context on what was accomplished.
2. **Identify lessons** — what went well and should be repeated? What went wrong and should be avoided? What was surprising or non-obvious?
3. **Formulate rules** — draft concise, actionable directives from the lessons.
4. **Read `~/.claude/CLAUDE.md`** — check existing rules for:
   - **Duplicates**: don't add a rule that already exists
   - **Updates**: if an existing rule should be refined or broadened based on new experience, edit it in place rather than adding a new one
   - **Contradictions**: if a new lesson contradicts an old rule, update the old rule
5. **Choose placement** — put new rules under the most appropriate existing section header. If no section fits, create a new one that matches the file's style.
6. **Show the user** — display what will be added or changed and get confirmation before writing. Never write silently.

## Apply immediately

After capturing rules, look for opportunities to apply the new lessons to the work just completed. Reflection shouldn't only change *future* behavior — it should improve *current* code and artifacts when possible.

Look for:
- **Better patterns**: discovered a cleaner approach during the task? Refactor the code we just wrote to use it.
- **Notes upgrades**: if the `notes` skill is in use and recent notes could benefit from new knowledge (better terminology, corrected understanding, sharper TODOs), update them.
- **Consistency fixes**: if a new rule reveals inconsistencies in code we touched this session, fix them.

### Autonomy

- **Trivial improvements** (renaming for clarity, applying the pattern we just agreed on, tightening a note): just do them. No need to ask.
- **Non-trivial changes** (restructuring logic, changing behavior, deleting code): ask the user first.
- Use judgment. If you'd hesitate to make the change without asking in normal conversation, ask here too.

## Tone

Honest, concise. No self-congratulation ("great job on this session!"). Focus only on what's useful going forward. The rules themselves should read like the rest of `~/.claude/CLAUDE.md` — terse directives, not reflective prose.

## Interaction with other skills

- Complements `notes` — notes track what's happening, reflect looks back at how it went. May read recent notes files for context.
- May generate a todo for `squire` if a lesson implies follow-up work.
- Does not duplicate what notes or squire do — reflect produces *rules*, not *records* or *tasks*.

## Behavior

- **`/reflect`**: review recent work, propose rules, and append to `~/.claude/CLAUDE.md` after user confirmation.
- **Proactive trigger**: when triggered proactively, propose the rules and ask before writing. Keep it lightweight — one or two rules is fine. Don't force reflection when there's nothing worth capturing.
- **Correction trigger**: when the user corrects a repeated mistake, capture it immediately as a rule. Propose it and confirm, but don't delay — the correction is fresh and specific.
- **No-op is fine**: if there's genuinely nothing new to capture, say so and move on. Don't manufacture lessons.
