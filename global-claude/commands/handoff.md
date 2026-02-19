Generate a session handoff summary for the next Claude Code session.

1. Read state.md for current project state
2. Read recent git log (last 10 commits)
3. Identify what was accomplished this session
4. Identify what's next (In Progress items from state.md)
5. Note any blockers or decisions that need to be made
6. Update state.md with this session's work

Output format:
```
## Session Summary - [today's date]
### Accomplished
- [list of completed work]

### Next Steps
- [prioritized list of what to do next]

### Blockers
- [anything blocking progress]

### Decisions Needed
- [any open questions for Shawn]
```

Ensure state.md is updated before generating this summary.
