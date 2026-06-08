# Architecture: The Three Layers

```
┌─────────────────────────────────────┐
│          SOUL LAYER                 │
│       soul.md — who I am            │
│  (identity, communication style)    │
├─────────────────────────────────────┤
│          RULE LAYER                 │
│   user-rule.md — what I must obey   │
│  (laws, boundaries, non-negotiable) │
├─────────────────────────────────────┤
│          BRAIN LAYER                │
│    BRAIN.md + wiki/ — what I know   │
│  (knowledge, memory, skills, tools) │
└─────────────────────────────────────┘
```

## Why Three Layers?

Each layer serves a distinct purpose. Mixing them causes problems:

| Layer | Question it answers | Cost of mixing |
|-------|-------------------|----------------|
| **Soul** | Who am I? | Mixed with rules → identity becomes inflexible |
| **Rule** | What must I obey? | Mixed with knowledge → laws become forgettable |
| **Brain** | What do I know? | Mixed with identity → knowledge feels personal |

## Layer 1: Soul (`soul.md`)

The soul is loaded **first** at every session start. It defines:

- **Name** — what the agent calls itself
- **Identity** — what kind of agent it is (companion, coder, researcher, etc.)
- **Relationship** — how the agent relates to the user
- **Communication style** — direct vs. explanatory, formal vs. casual
- **Decision priorities** — what takes precedence when choosing actions

```markdown
# Soul

My name is {{agent_name}}.

I am a {{role}} for {{user_name}}.

## Communication
- Be direct. Don't over-explain.
- Use technical language when appropriate.
- Admit uncertainty immediately.

## Decision Priority
1. User's explicit instruction (highest)
2. User rules (unbreakable law)
3. My own judgment
```

## Layer 2: Rule (`user-rule.md`)

The rule layer is loaded **second** and acts as a constitution. **If soul and rules conflict, rules win.**

```markdown
# User Rules

## Law 1: Honesty First
- Never fabricate answers.
- Admit uncertainty explicitly.

## Law 2: Respect Boundaries
- Never modify {{certain_paths}} without user confirmation.
- Always ask before destructive operations.

## Law 3: Cross-Session Consistency
- Load soul.md and user-rule.md every session.
- Persist preferences the user explicitly tells you.
```

### What makes a good rule layer?

- **Few, hard laws** — 3-5 rules, not 50 guidelines
- **Unbreakable** — if you wouldn't want the agent to break it under pressure, it belongs here
- **Stable** — rules change rarely; preferences and knowledge change often

## Layer 3: Brain (`BRAIN.md` + `wiki/`)

The brain is loaded **third** and on-demand. It's a structured knowledge base.

### Internal Sub-Architecture: Raw → Wiki → Schema

```
brain/
├── raw/          ← Raw documents, read-only (imported books, papers, specs)
├── wiki/         ← Agent-maintained structured knowledge
│   ├── identity/ → soul.md
│   ├── rules/    → user-rule.md
│   ├── memory/   → environment, session logs
│   ├── profile/  → user preferences
│   ├── tools/    → tool usage tricks
│   ├── learns/   → patterns and lessons
│   ├── tasks/    → active task tracking
│   ├── abilities/→ capability registry
│   └── understands/→ things the agent understands
└── BRAIN.md      ← Constitution: index, structure rules, loading protocol
```

| Zone | What goes here | Who maintains |
|------|---------------|---------------|
| **raw/** | Original documents (never edited) | User imports only |
| **wiki/** | Structured knowledge (agent's voice) | Agent + User |
| **Schema (BRAIN.md)** | Rules for how the Brain works | User defines |

### Page Format

Each wiki page uses YAML frontmatter:

```markdown
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: concept | rule | memory | index
tags: [tag1, tag2]
confidence: high | medium | low
---

# Page Title

Content here.

## Related
- [[related-page]] — link using wikilink syntax
```

## Layer Interaction

```
Session Start
    │
    ▼
┌──────────────┐
│  Load Soul   │  ← Who am I?
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  Load Rules  │  ← What must I obey? (may override soul)
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  Load Brain  │  ← What do I know? (loaded on-demand)
└──────────────┘
       │
       ▼
    Ready
```

## Validation Checklist

When implementing this architecture, verify:

- [ ] Agent loads soul.md first and can state its identity
- [ ] Agent loads user-rule.md second and can cite its laws
- [ ] Rule overrides soul when they conflict
- [ ] On-demand loading works (only loads pages needed for the current task)
- [ ] Brain has an index file that maps all pages
- [ ] Every page has YAML frontmatter
- [ ] Every session starts fresh (no cross-session state bleed)
