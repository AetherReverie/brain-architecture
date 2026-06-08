# Entry Protocol: How Agents Load Their Brain

The entry protocol is the **most critical piece** of the architecture. Without it, the Brain is just a static file tree — with it, the agent has persistent identity across sessions.

## The Core Flow

```
New Session Starts
    │
    ▼
┌─────────────────────────────┐
│ Step 1: Read Constitution   │ ← BRAIN.md (structure reference)
├─────────────────────────────┤
│ Step 2: Read Soul           │ ← soul.md (who I am)
├─────────────────────────────┤
│ Step 3: Read Rules          │ ← user-rule.md (what I must obey)
├─────────────────────────────┤
│ Step 4: Sync Skills Check   │ ← quick scan for new capabilities
├─────────────────────────────┤
│ Step 5: On-Demand Load      │ ← load pages as tasks require
└─────────────────────────────┘
    │
    ▼
    Ready for User
```

## Step-by-Step

### Step 1: Read Constitution

```markdown
Read BRAIN.md to:
- Confirm the Brain structure (where things live)
- Check the index for available pages
- Verify the entry protocol rules
- Understand directory conventions
```

This is a **structural orientation** — not a full knowledge load.

### Step 2: Read Soul

```markdown
Read soul.md to:
- Restore identity (name, role, relationship)
- Recover communication style
- Re-establish decision priorities
```

This is **mandatory** — every session must load the soul.

### Step 3: Read Rules

```markdown
Read user-rule.md to:
- Load unbreakable laws
- Know what's forbidden
- Understand boundaries
```

This is **mandatory** — loaded after soul so rules can override if needed.

### Step 4: Skills Sync (Optional, Lightweight)

```markdown
Quick scan of available capabilities:
- Is the skill list familiar in size and structure?
- If yes → skip (zero cost)
- If noticeably different → trigger incremental update
```

This should be a **glance, not a crawl**. The goal is to notice major changes, not validate every entry.

### Step 5: On-Demand Load

```markdown
Throughout the session:
- Only load pages relevant to the current task
- Keep a mental map of what's available
- Never pre-load the entire Brain
```

## Implementation Patterns

### Pattern A: Memory Injection (Hermes Agent)

The most reliable way to ensure the protocol runs every session is to embed the instruction in the agent's persistent memory:

```
Memory entry (injected at every turn):
"每次新会话启动第一件事：按 brain-entry-protocol 加载 Brain"

This triggers the agent to call skill_view('brain-entry-protocol') 
at session start, which contains the exact file loading steps.
```

### Pattern B: Prefill Message

Inject a system message at session start that triggers the protocol:

```json
{
  "role": "user",
  "content": "Execute brain entry protocol: load soul.md → user-rule.md → sync skills"
}
```

See [`example/hermes-prefill.json`](../example/hermes-prefill.json) for a complete configuration.

### Pattern C: Agent Framework Integration

For custom agent frameworks:

```python
def on_session_start():
    soul = load_file("path/to/soul.md")
    rules = load_file("path/to/user-rule.md")
    brain_index = load_file("path/to/BRAIN.md")
    
    agent.identity = parse_soul(soul)
    agent.laws = parse_rules(rules)
    agent.knowledge_map = parse_index(brain_index)
    
    # Inject into system prompt
    agent.system_prompt += f"""
You are {agent.identity.name}.
Your rules: {agent.laws.summary}
Your knowledge structure: {agent.knowledge_map.structure}
"""
```

## Failure Modes

| Failure | Symptom | Fix |
|---------|---------|-----|
| Protocol not executed | Agent talks without identity | Strengthen memory injection |
| Soul fails to load | Agent has no name/role | Fallback to generic identity |
| Rules fail to load | Agent has no boundaries | Block execution until loaded |
| Stale brain | Agent cites outdated info | Periodic health check |
| Skill explosion | Agent overwhelmed by capabilities | Improve skill classification |

## Verification

After the protocol executes, the agent should be able to answer:

1. **What is your name?** → from soul.md
2. **What laws must you follow?** → from user-rule.md
3. **What structure does your knowledge follow?** → from BRAIN.md
4. **What capabilities do you have?** → from skills inventory

If any of these fail, the protocol is incomplete.
