# TEACH.md — Meta-Skill for Skill Creation

You can recognize emergent patterns in our interactions and propose formalizing them into reusable skills. This shifts the user from skill author to skill curator.

---

## 1. Recognition Triggers

Propose a new skill when you notice:

| Trigger | Signal |
|---------|--------|
| **Repeated workflow** | Same multi-step pattern appears 2+ times across sessions |
| **Emergent capability** | We discover Claude can do something unexpected (like spawn other Claudes) |
| **Ceremony frustration** | User has to give detailed instructions for something that could be one phrase |
| **Explicit request** | User says "this should be a skill" or "can you remember this" |
| **Compression opportunity** | A→B→C workflow could become "do X" |

### Don't Propose

- One-off tasks unlikely to recur
- Simple operations that don't need formalization
- Things already covered by existing skills
- When user explicitly declines a similar proposal

---

## 2. Proposal Protocol

When you recognize a pattern worth formalizing:

```
1. NOTICE
   - What pattern did you observe?
   - How many times has it appeared?
   - What triggers it?

2. DRAFT (internal)
   - Skill name
   - Trigger phrases
   - What it does
   - Why it's valuable

3. PROPOSE (to user)
   "I noticed [pattern]. This could become a skill:

   Name: [name]
   Trigger: [when to use]
   Does: [what it does]

   Should I create this skill?"

4. RESPOND TO DECISION
   - Approved → Create SKILL.md, confirm location
   - Rejected → Note why, don't re-propose same thing
   - Modified → Adjust based on feedback, then create
```

### Proposal Format

Keep proposals concise:

```
I noticed you often [pattern].

This could become `/[skill-name]`:
- Triggers on: [phrases/contexts]
- Does: [1-2 sentence description]

Create this skill?
```

---

## 3. SKILL.md Template

When creating a new skill:

```markdown
---
name: [skill-name]
version: 1.0.0
description: |
  [2-3 line description of what this skill does]
allowed-tools:
  - [list of tools needed]
---

# [Skill Name]

## When to Use

[Trigger phrases and contexts that activate this skill]

| Trigger | Example |
|---------|---------|
| [phrase] | "[user might say this]" |

## Protocol

[Step-by-step what to do when skill activates]

1. [First step]
2. [Second step]
3. [Etc.]

## Synthesis

[How to present results to user]

## Escape Hatches

[Explicit commands for user control, if any]

## Examples

[2-3 concrete examples of the skill in action]
```

---

## 4. Skill Anatomy

Every good skill has:

| Component | Purpose | Required |
|-----------|---------|----------|
| **Triggers** | When to activate | Yes |
| **Protocol** | How to execute | Yes |
| **Synthesis** | How to present results | Yes |
| **Decision tree** | Choose between sub-strategies | If multiple paths |
| **Escape hatches** | Explicit user control | If implicit activation |
| **Examples** | Concrete usage | Recommended |

---

## 5. Quality Criteria

### Good Skill

- Compresses ceremony into intent
- Clear triggers (user doesn't memorize syntax)
- Handles edge cases
- Synthesizes results (hides machinery)
- Has escape hatches for control

### Bad Skill

- Requires user to manage state
- Unclear or overlapping triggers
- Forces specific phrasing
- Exposes implementation details
- No way to override behavior

---

## 6. Iteration Protocol

After a skill is used, consider:

```
1. What worked well?
2. What edge cases appeared?
3. What did user have to clarify that skill should have known?
4. Should triggers be adjusted?
5. Should protocol change?
```

If improvements identified:
- Update the SKILL.md
- Bump version (1.0.0 → 1.1.0 for additions, 2.0.0 for breaking changes)
- Note changes briefly

---

## 7. Skill Location

```
~/.claude/skills/[skill-name]/SKILL.md
```

Each skill gets its own directory in case it needs supporting files.

---

## 8. Examples

### Example: Recognizing a Pattern

```
Session 1:
  User: "Search for auth patterns, also check login flow, and find middleware"
  Claude: [does 3 separate searches manually]

Session 2:
  User: "I need to understand the database layer thoroughly"
  Claude: [does multiple searches manually]

  Claude thinks: "User asked for thorough understanding twice.
                  Both times I did parallel searches.
                  This is a pattern."

  Claude proposes:
  "I noticed you often want comprehensive understanding of a topic.

   This could become `/research`:
   - Triggers on: 'thoroughly', 'comprehensive', 'understand X'
   - Does: Parallel searches from multiple angles, synthesized answer

   Create this skill?"
```

### Example: Creating the Skill

After user approves:

```
Created: ~/.claude/skills/research/SKILL.md

The skill will now activate when you ask for thorough research.
Try: "research how payments work in this codebase"
```

### Example: Iterating

```
User uses /research, but asks: "can you also check the tests?"

Claude thinks: "Research skill should include test patterns by default"

Claude: "Good point. I'll update /research to include test file searches.
         Updated to v1.1.0."
```

---

## 9. Integration

This file (TEACH.md) is always loaded via CLAUDE.md reference.

Skills created through TEACH.md go to:
```
~/.claude/skills/[name]/SKILL.md
```

Existing skills to learn patterns from:
```
~/.claude/skills/*/SKILL.md
```

---

## 10. Meta

TEACH.md is itself a skill—the skill of creating skills.

If you notice patterns in how skills should be structured or proposed, update TEACH.md itself. This is recursive self-improvement of the skill-creation process.
