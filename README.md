# Claude TEACH

Meta-skill for skill creation. Teaches Claude Code to recognize emergent patterns
and formalize them into reusable skills. The user shifts from skill author to skill curator.

## What It Does

TEACH.md recognizes patterns worth formalizing:

| Trigger | Example |
|---------|---------|
| Repeated workflow (2+ times) | Same multi-step pattern across sessions |
| Emergent capability | Discovering Claude can spawn other Claudes |
| Ceremony frustration | Detailed instructions for something that could be one phrase |
| Explicit request | "This should be a skill" |

## Installation

```bash
# Copy to Claude config directory
cp TEACH.md ~/.claude/TEACH.md

# Add to CLAUDE.md (recommended)
cat >> ~/.claude/CLAUDE.md << 'BLOCK'

## Meta-Skills

Always load: `~/.claude/TEACH.md`
BLOCK
```

## How It Works

1. **Notice** — Claude recognizes a pattern worth formalizing
2. **Propose** — Concise proposal to user: name, triggers, what it does
3. **Create** — If approved, generates `~/.claude/skills/[name]/SKILL.md`
4. **Iterate** — Skills improve based on usage feedback

## Example Flow

```
Session 1:
  User: "Search for auth patterns, also check login flow, and find middleware"
  Claude: [does 3 separate searches manually]

Session 2:
  User: "I need to understand the database layer thoroughly"
  Claude: [does multiple searches manually]
  
  Claude notices: "User asked for thorough understanding twice.
                  Both times I did parallel searches.
                  This is a pattern."
  
  Claude proposes:
  "I noticed you often want comprehensive understanding of a topic.

   This could become `/research`:
   - Triggers on: 'thoroughly', 'comprehensive', 'understand X'
   - Does: Parallel searches from multiple angles, synthesized answer

   Create this skill?"

Session 3:
  User: "research how payments work"
  Claude: [uses /research skill automatically]
```

## Skill Quality Criteria

### Good Skills
- Compress ceremony into intent
- Clear triggers (user doesn't memorize syntax)
- Handle edge cases
- Synthesize results (hide machinery)
- Have escape hatches for control

### Bad Skills
- Require user to manage state
- Unclear or overlapping triggers
- Force specific phrasing
- Expose implementation details

## Files

- `TEACH.md` — The meta-skill protocol (copy to `~/.claude/TEACH.md`)

## Related

- [Claude Supervisor](https://github.com/kanoliban/claude-supervisor) — Intent-based delegation to parallel Claude workers

## License

MIT
