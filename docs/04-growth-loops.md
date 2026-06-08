# Growth Loops: Knowledge that Evolves

A Brain that never changes is a tomb, not a living knowledge base. This document covers how knowledge enters, grows, and stays healthy.

## The Ingest Loop

```
User says something new
        │
        ▼
┌─────────────────────┐
│  Is this knowledge?  │
│  (fact, preference,  │
│   lesson, convention)│
└──────┬──────┬───────┘
       │      │
      Yes     No
       │      │
       ▼      └──→ Ignore (transient)
┌─────────────────┐
│  Categorize     │
│  Where does it  │
│  belong in the  │
│  wiki?          │
└──────┬──────────┘
       │
       ▼
┌─────────────────┐
│  Write or Update│
│  → create page  │
│  → update index │
│  → link related │
└──────┬──────────┘
       │
       ▼
┌─────────────────┐
│  Verify          │
│  → correct?      │
│  → complete?     │
│  → consistent?   │
└─────────────────┘
```

### Decision: Should I Save This?

| If the user says... | Is it knowledge? | Action |
|-----------|----------|--------|
| "My name is Alice" | ✅ Yes | Save to profile |
| "I prefer dark mode" | ✅ Yes | Save to preferences |
| "Can you fix bug #42?" | ❌ Task | Track in tasks/ |
| "That's correct" | ❌ Feedback | Update confidence |
| "The API changed to v3" | ✅ Yes | Update relevant page |

## The Insert Loop (Structured)

For new capabilities or topics you learn:

```
1. Discover          → "I learned something new"
2. Create page       → Write with YAML frontmatter
3. Categorize        → Find the right wiki/ subsection
4. Link              → Connect to related pages via wikilink
5. Update index     → Add to the relevant index
6. Optional: verify  → Confirm with user
```

### Page Lifecycle

```
Created     → confidence: low
Validated   → confidence: medium
Proven      → confidence: high (multiple uses, user confirmed)
Stale       → needs review (timestamp too old)
Deprecated  → marked as replaced by newer knowledge
Archived    → moved to raw/ or deleted with user confirmation
```

## Health Checks

Periodically audit the Brain for integrity:

### Dimensions

| Dimension | What to check | How |
|-----------|--------------|-----|
| **Orphan pages** | Zero incoming or outgoing links | Traverse all wikilinks, build matrix |
| **Contradictions** | Same fact said differently | Cross-compare related pages |
| **Stale data** | Old timestamps, outdated versions | Compare against reality |
| **Gaps** | Empty sections, broken links | Match index against actual files |

### Fix Priority

1. 🔴 Dead references + fact contradictions → fix immediately
2. 🟡 Orphan pages → add links
3. 🟡 Stale information → update
4. 🟡 Gaps → fill or mark as "not yet known"

## Example: Learning a New Skill

**User:** "I installed `ruff` for linting. Use it instead of pylint."

**Agent's internal process:**

```
1. Evaluate: This is knowledge (tool preference)
2. Categorize: wiki/tools/ → update or create tool entry
3. Write:
   ---
   title: Ruff Linter
   type: tool
   tags: [linting, python, tools]
   confidence: medium
   ---
   # Ruff
   - Command: ruff check .
   - Replaces: pylint
   - Installed by user on: YYYY-MM-DD
4. Link: from wiki/tools/index.md add link
5. Verify: "I've updated my tools knowledge. For future linting, I'll use `ruff`."
```

## Anti-Patterns

| Anti-pattern | Why it's bad | Better |
|-------------|--------------|--------|
| Saving everything | Bloat, hard to find | Save only durable knowledge |
| Missing index updates | Orphan pages | Always update index on create |
| Overwriting without | Losing history | Keep confidence field, update, don't delete |
| No verification | Hallucinated knowledge | Cross-check before saving |
| Personal data in knowledge | Privacy leak | Keep personal info in profile/ only |
