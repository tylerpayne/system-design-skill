# system-design-skill

A Claude skill that runs a structured system design interview to turn a rough software idea into a complete, installable Claude skill capturing everything needed to build it.

## What's in this repo

```
system-design-interview/
  SKILL.md
  references/
    interview-phases.md
    question-banks.md
    tech-decisions.md
    non-functional-checklist.md
    implementation-guidance.md
    output-template.md
```

`system-design-interview/` is the skill itself. `SKILL.md` is the entry point; the `references/` files are loaded on demand during the interview.

## What it does

Adapted from the Hello Interview system design framework, but tuned for real-world building rather than interview performance. When triggered, the skill runs a focused conversation covering:

1. Context & goals
2. Functional requirements
3. Non-functional requirements
4. Capacity & scale
5. Core entities
6. API / interface
7. Data model
8. Architecture
9. Deep dives
10. Build plan
11. Decisions & open questions

The output is a new Claude skill (a directory with its own `SKILL.md` and references) that future Claude sessions can load to continue building the project with full context.

It defaults to the simplest architecture that meets requirements — no reaching for Kafka on a 100-user app.

## Installing

Copy the `system-design-interview/` directory into your Claude skills location:

- **User-level (all projects):** `~/.claude/skills/system-design-interview/`
- **Project-level:** `.claude/skills/system-design-interview/` inside your repo

Claude Code picks up skills automatically from either location.

## Using it

Trigger phrases include:

- "I want to build [an app / service / tool]"
- "Help me design [X]"
- "How should I architect [Y]"

Or invoke it explicitly with `/system-design-interview`.

The skill will ask one question at a time, recommend concrete choices with rationale, and produce an installable skill at the end.
