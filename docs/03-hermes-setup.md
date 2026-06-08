# Hermes Agent Integration

This guide covers how to integrate Brain Architecture with [Hermes Agent](https://hermes-agent.nousresearch.com).

## Three Mechanisms

Hermes provides three complementary mechanisms to enforce the entry protocol:

| Mechanism | Reliability | Effort | 
|-----------|-------------|--------|
| **Skill** (brain-entry-protocol) | Medium | Low |
| **Memory injection** | High | Medium |
| **Prefill message** | Highest | Medium |

**Best practice: use all three** — they form a defense-in-depth chain.

---

## 1. The Brain Entry Protocol Skill

Create a skill that contains the exact loading steps:

**Skill name:** `brain-entry-protocol`

```markdown
---
name: brain-entry-protocol
title: Brain Entry Protocol — Session Mandatory
version: 1.0
category: agent-architecture
description: |
  Load at every new session. Reads BRAIN.md → soul.md → user-rule.md
  in order. Enforces Soul → Rule → Brain loading sequence.
trigger: |
  • New session start
  • First user message
  • Any scenario where identity needs restoration
---

# Brain Entry Protocol

## Step 1: Read Constitution
```
read_file path/to/BRAIN.md
```

## Step 2: Read Soul
```
read_file path/to/wiki/identity/soul.md
```

## Step 3: Read Rules
```
read_file path/to/wiki/rules/user-rule.md
```

## Step 4: Skills Sync (fast glance)
- Familiar skill list → skip
- Unknown names → incremental update

## Step 5: Ready for user
```

## 2. Memory Injection

Persistent memory entries are **injected at every turn**, making them the most reliable trigger. Add to agent memory:

```
memory entry:
"每次新会话启动第一件事：skill_view('brain-entry-protocol') → 
读 BRAIN.md → soul.md → user-rule.md。这是强制流程。"

memory entry:
"Brain location: path/to/brain/"
"Entry protocol: Soul → Rule → Brain (in order)"
```

This way, even if the skill isn't auto-loaded, the memory instruction tells the agent to load it.

## 3. Prefill Message

Configure a prefill message that fires at session start. In Hermes `config.yaml`:

```yaml
# Prefill: inject a user message at every new session
prefill_messages_file: path/to/prefill-brain-entry.json
```

Contents of `prefill-brain-entry.json`:

```json
[
  {
    "role": "user",
    "content": "加载 brain-entry-protocol skill，执行入场协议：读 BRAIN.md → soul.md → user-rule.md。这是强制流程，先完成再处理其他请求。"
  }
]
```

This forces a simulated user message that triggers the skill chain at every session start.

## Complete Setup

### Directory Layout

```
hermes-home/
├── skills/
│   └── agent-architecture/
│       └── brain-entry-protocol/
│           └── SKILL.md         ← the skill from section 1
├── config.yaml                   ← with prefill_messages_file set
├── prefill-brain-entry.json      ← the prefill message from section 3
└── brain/                        ← your actual Brain
    ├── BRAIN.md
    └── wiki/
        ├── identity/soul.md
        └── rules/user-rule.md
```

### Config.yaml Changes

```yaml
# In prefill section:
prefill_messages_file: ~/.hermes/prefill-brain-entry.json

# Or inline:
prefill_messages:
  - role: user
    content: "加载 brain-entry-protocol skill，执行入场协议。"
```

## Testing the Setup

After configuration, start a new session and verify:

```
User: 你好
Agent: <loads skill, reads BRAIN.md → soul.md → user-rule.md>
       "我是 {{name}}。我的规则有三条..."
       "Ready."
```

If the agent responds without going through the protocol, the chain isn't working — check memory injection strength.

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Agent doesn't load skill | Memory trigger too weak | Add stronger memory directive |
| Agent loads skill but skips files | Protocol skill missing file paths | Add explicit read_file commands |
| Prefill fires but agent ignores | Model doesn't follow prefilled messages | Check model compatibility |
| Agent loads Brain but forgets mid-conversation | Missing on-demand reload | Add trigger: user says "check Brain" |
