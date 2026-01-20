# Claude TEACH

Meta-skill for Claude Code that enables recognition of emergent patterns and formalization into reusable skills.

**Give Claude a fish, and you feed it for a day; teach Claude to fish, and you feed it for a lifetime.**

## What It Does

TEACH.md shifts you from **skill author** to **skill curator**. Instead of writing skills yourself, Claude:

1. **Recognizes** patterns worth formalizing
2. **Proposes** skill structure for your approval
3. **Formalizes** into SKILL.md with proper structure
4. **Iterates** based on usage feedback

## Recognition Triggers

| Trigger | Signal |
|---------|--------|
| Repeated workflow | Same multi-step pattern appears 2+ times |
| Emergent capability | Claude discovers it can do something unexpected |
| Ceremony frustration | Detailed instructions for something that could be one phrase |
| Explicit request | "This should be a skill" |

## Installation

```bash
# Copy to Claude config directory
cp TEACH.md ~/.claude/

# Add to CLAUDE.md (so it's always loaded)
cat >> ~/.claude/CLAUDE.md << 'EOF'

<Meta_Skills>
## Meta-Skills — Self-Improving Skill Creation

Always load: `~/.claude/TEACH.md`
</Meta_Skills>
EOF
```

## How It Works

### The Loop

```
Emergence → Recognition → Proposal → Formalization → Usage → Iteration
                ↑                                              |
                └──────────────────────────────────────────────┘
```

### Example Flow

**Session 1:**
```
User: "Search for auth patterns, also check login flow, and find middleware"
Claude: [does 3 separate searches manually]
```

**Session 2:**
```
User: "I need to understand the database layer thoroughly"
Claude: [does multiple searches manually]

Claude (via TEACH.md): "I noticed you often want comprehensive understanding.
                        Should this become a /research skill?"
User: "Yes"
Claude: Creates ~/.claude/skills/research/SKILL.md
```

**Session 3:**
```
User: "research how auth works"
Claude: [uses /research skill automatically]
```

## SKILL.md Template

Skills created by TEACH.md follow this structure:

```markdown
---
name: [skill-name]
version: 1.0.0
description: |
  [2-3 line description]
allowed-tools:
  - [tools needed]
---

# [Skill Name]

## When to Use
[Recognition patterns / trigger phrases]

## Protocol
[Step-by-step execution]

## Examples
[Concrete usage examples]
```

## Quality Criteria

### Good Skills
- Compress ceremony into intent
- Clear triggers (user doesn't memorize syntax)
- Handle edge cases gracefully
- Synthesize results (hide machinery)
- Have escape hatches for control

### Bad Skills
- Require user to manage state
- Unclear or overlapping triggers
- Force specific phrasing
- Expose implementation details

## Files

- `TEACH.md` — The meta-skill protocol
- `README.md` — This documentation

## Related

- [claude-supervisor](https://github.com/kanoliban/claude-supervisor) — First skill created through this pattern

## License

MIT
