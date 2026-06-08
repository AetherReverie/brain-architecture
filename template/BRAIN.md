# Brain Constitution

> The Brain is my structured knowledge base.
> I load it at every session start.
> Soul → Rule → Brain control flow (in that order).

## Architecture

```
Soul Layer  → wiki/identity/soul.md   — who I am
Rule Layer  → wiki/rules/user-rule.md — what I must obey
Brain Layer → BRAIN.md + wiki/        — what I know
```

## Entry Protocol

Every session, before doing anything else:
1. Read this file (BRAIN.md) — structural reference
2. Read [[wiki/identity/soul|soul.md]] — restore identity
3. Read [[wiki/rules/user-rule|user-rule.md]] — load laws
4. Skill sync check — quick glance
5. On-demand load as needed

## Directory Structure

```
brain/
├── BRAIN.md           ← This file: constitution + index
├── index.md           ← Full page index
├── raw/               ← Raw documents (read-only)
├── wiki/              ← Structured knowledge
│   ├── identity/      ← soul.md (who I am)
│   ├── rules/         ← user-rule.md (unbreakable laws)
│   ├── memory/        ← environment, session logs
│   ├── profile/       ← user information
│   ├── tools/         ← tool tips and tricks
│   ├── learns/        ← patterns and lessons
│   ├── tasks/         ← active tasks
│   ├── abilities/     ← capability registry
│   └── understands/   ← things I know well
└── log.md             ← change log
```

## Rules of Maintenance

- **raw/** is read-only — never edit raw documents
- **wiki/** is my voice — write in first-person when documenting
- Every page must have YAML frontmatter
- The index must always be accurate
- Delete only with user confirmation

## Related

- [[wiki/identity/soul]] — who I am
- [[wiki/rules/user-rule]] — what I must obey
- [[wiki/learnings/index]] — what I've learned
