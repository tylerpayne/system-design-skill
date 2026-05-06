# system-design-skill

A Claude Code **plugin marketplace** hosting the `system-design-skill` plugin: a structured system design interview that turns a rough software idea into a complete, installable Claude skill capturing everything needed to build it.

## Repo layout

```
.claude-plugin/
  marketplace.json                    # marketplace manifest (this repo as a marketplace)
plugins/
  system-design-skill/
    .claude-plugin/
      plugin.json                     # plugin manifest
    skills/
      system-design-interview/        # the skill itself
        SKILL.md
        references/
          interview-phases.md
          question-banks.md
          tech-decisions.md
          non-functional-checklist.md
          implementation-guidance.md
          output-template.md
```

## What it does

Adapted from the Hello Interview system design framework, but tuned for real-world building rather than interview performance. When triggered, the skill runs a focused conversation covering:

1. Context & goals
2. Functional requirements
3. Non-functional requirements
4. Capacity & scale
5. Core entities
6. API / interface
7. Data model
8. Architecture (incl. LLD bridge: domain classes + seed correctness expectations)
9. Deep dives
10. Build plan (acceptance criteria as concrete *given/when/then* conditions)
11. Decisions & open questions

The output is a new Claude skill (a directory with its own `SKILL.md` and references) that future Claude sessions can load to continue building the project with full context.

It defaults to the simplest architecture that meets requirements — no reaching for Kafka on a 100-user app — and enforces a **correctness-tests-first** rule for LLD: before implementing any non-trivial class or service, the test list (happy path, edge cases, error modes, invariants) is written down.

## Installing

### As a Claude Code plugin (recommended)

Add the marketplace, then install the plugin:

```
/plugin marketplace add tylerpayne/system-design-skill
/plugin install system-design-skill@tylerpayne
```

Or from the CLI:

```bash
claude plugin marketplace add tylerpayne/system-design-skill
claude plugin install system-design-skill@tylerpayne
```

The skill is invoked by trigger phrases (see below) or explicitly via `/system-design-skill:system-design-interview`.

### Manual install (no plugin system)

Copy the skill directory into a Claude skills location:

- **User-level (all projects):** `~/.claude/skills/system-design-interview/`
- **Project-level:** `.claude/skills/system-design-interview/` inside your repo

```bash
cp -r plugins/system-design-skill/skills/system-design-interview ~/.claude/skills/
```

Claude Code picks up skills automatically from either location.

## Using it

Trigger phrases include:

- "I want to build [an app / service / tool]"
- "Help me design [X]"
- "How should I architect [Y]"

The skill will ask one question at a time, recommend concrete choices with rationale, sketch the most important domain classes with seed invariants and edge cases, and produce an installable skill at the end.

## Adding more plugins to this marketplace

To add another plugin to this marketplace:

1. Create `plugins/<new-plugin>/.claude-plugin/plugin.json` and a sibling `skills/<skill>/`, `commands/`, `agents/`, etc. as needed
2. Add an entry to `.claude-plugin/marketplace.json` under `plugins`:
   ```json
   { "name": "new-plugin", "source": "./plugins/new-plugin", "description": "..." }
   ```

See the [Claude Code plugin marketplace docs](https://code.claude.com/docs/en/plugin-marketplaces) for the full schema.
