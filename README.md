# Brain Architecture

**Soul → Rule → Brain: a three-layer knowledge architecture for persistent AI agent identity.**

---

## One-liner

A structured knowledge framework that lets AI agents maintain a consistent identity, follow unbreakable rules, and grow a durable knowledge base across every conversation — without resetting on each new session.

## The Problem

Every time you start a new conversation with an AI agent, it's a blank slate. No memory of who it is, what you've discussed, or how you prefer things done. Traditional solutions are either:

- **Stateless prompts** — long, fragile, impossible to maintain
- **Fine-tuning** — expensive, slow to iterate, locks behavior
- **RAG** — good for facts, bad for identity and rules

Brain Architecture solves this with a **lightweight, file-based system** that any agent can load at session start.

## The Architecture

```
┌──────────────────────────────────────────┐
│              SOUL LAYER                   │
│         soul.md — who I am                │
│  (identity, communication style, name)    │
├──────────────────────────────────────────┤
│              RULE LAYER                   │
│      user-rule.md — what I must obey      │
│  (laws, boundaries, unbreakable rules)    │
├──────────────────────────────────────────┤
│              BRAIN LAYER                  │
│   BRAIN.md + wiki/ — what I know         │
│  (structured knowledge, memory, skills)   │
└──────────────────────────────────────────┘
```

**Loading order:** Soul → Rule → Brain.

If Soul and Rule conflict, **Rule wins**. If Brain and reality conflict, **reality wins** (Rule Law 1: honesty).

## Quick Start

### 1. Fork the template

```bash
git clone https://github.com/your-username/brain-architecture.git
cd brain-architecture
cp -r template/* ./my-brain/
```

### 2. Fill in your identity

Edit `my-brain/wiki/identity/soul.md`:
- What's your agent's name?
- What's your relationship with the user?
- What communication style do you prefer?

### 3. Define your laws

Edit `my-brain/wiki/rules/user-rule.md`:
- What must the agent never do?
- What's non-negotiable?
- What happens when rules conflict?

### 4. Set up the entry protocol

See [`docs/03-hermes-setup.md`](docs/03-hermes-setup.md) for Hermes Agent integration, or adapt the protocol to any agent framework.

## Core Principles

| Principle | What it means |
|-----------|---------------|
| **Act, don't describe** | Execute instead of explaining what you'd do |
| **Honesty first** | Never fabricate; admit uncertainty |
| **Cross-session consistency** | Load the same identity every time |
| **Knowledge grows** | Brain evolves via structured insert loops |
| **Rules over soul** | If identity and law conflict, law wins |

## Documentation

| File | What it covers |
|------|---------------|
| [`docs/01-architecture.md`](docs/01-architecture.md) | Full three-layer architecture breakdown |
| [`docs/02-protocol.md`](docs/02-protocol.md) | Entry protocol — how agents load their brain |
| [`docs/03-hermes-setup.md`](docs/03-hermes-setup.md) | Hermes Agent integration (skill + memory + prefill) |
| [`docs/04-growth-loops.md`](docs/04-growth-loops.md) | Knowledge growth, ingest loops, health checks |
| [`template/`](template/) | Forkable template with placeholder content |

## Use Cases

- **Personal AI companion** — knows your name, your preferences, your history
- **Coding agent** — loaded with project conventions, API docs, team rules
- **Research assistant** — maintains topic expertise across long-running investigations
- **Multi-agent systems** — each agent has its own Brain with distinct identity and rules

## License

MIT
