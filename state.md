# Project State

## Current Version
v1.2.0

## Last Update
- **Date:** 2026-02-20
- **Commit:** feat: add brand_dna.md template, document CLAUDE.md convention, add Python line endings
- **Summary:** Added brand_dna.md template for client visual production standards, documented root CLAUDE.md convention in README, added Python line ending normalization to .gitattributes template.

## Completed
- [x] Global CLAUDE.md with AD-5 standards (security, TypeScript, Next.js, versioning, commit messages, workflow)
- [x] Global settings.json with PostToolUse and Stop hooks for state.md reminders
- [x] Global slash commands: /new-project, /update-state, /phase-gate, /handoff
- [x] Project template: .claude/CLAUDE.md, .claude/settings.json, state.md, .gitignore, .gitattributes, .env.example
- [x] README.md with installation instructions for Windows and Mac
- [x] Pushed to dragonjiujitsu/ad5-infrastructure (public repo)
- [x] Installed global files to ~/.claude/ on Windows machine
- [x] Added brand_dna.md template for client visual production standards (Layer 3)
- [x] Added *.py text eol=lf to project-template/.gitattributes
- [x] Documented Root CLAUDE.md Convention in README.md
- [x] Documented Layer 3: Client Production Standards in README.md

## In Progress
- [ ] Install global files to ~/.claude/ on Mac machine
- [ ] Test /new-project command on a fresh repo
- [ ] Test /update-state, /phase-gate, /handoff commands in a live session

## Key Decisions
- Public repo. No secrets or client data in any file. Community can benefit.
- File names are Claude Code conventions (CLAUDE.md, .claude/settings.json, .claude/commands/*.md). Not optional, not customizable.
- Global layer (~/.claude/) handles standards that apply everywhere. Project layer (.claude/) handles project-specific instructions. CLAUDE.local.md for personal machine-specific settings (auto-gitignored).
- Hooks are lightweight reminders, not blockers. PostToolUse reminds to update state.md. Stop reminds to verify state.md before ending.
- Project template .claude/settings.json includes TypeScript type check hook (PostToolUse on Edit/Write for .ts/.tsx files).
- Styling decision baked into global CLAUDE.md: Tailwind for websites, CSS Modules for internal tools.
- Explore, Plan, Code, Commit workflow from Anthropic best practices built into global CLAUDE.md.

## Known Issues
- Hooks not yet tested in live Claude Code sessions. May need tuning (especially the shell syntax on Windows vs Mac).
- /new-project command is natural language, not a script. Quality depends on Claude Code interpreting it correctly. May need refinement after testing.
- Global settings.json hook format may need adjustment. Anthropic docs show hooks nested under event names, but exact schema should be verified against Claude Code's current version.

## File Manifest
- `README.md` - Installation instructions, architecture explanation, reference links (v1.2.0)
- `brand_dna.md` - Brand DNA specification template for client visual production projects (copy manually into client repos)
- `state.md` - This file; project state tracking
- `global-claude/CLAUDE.md` - AD-5 global standards (installs to ~/.claude/CLAUDE.md)
- `global-claude/settings.json` - Global hooks (installs to ~/.claude/settings.json)
- `global-claude/commands/new-project.md` - /new-project slash command
- `global-claude/commands/update-state.md` - /update-state slash command
- `global-claude/commands/phase-gate.md` - /phase-gate slash command
- `global-claude/commands/handoff.md` - /handoff slash command
- `project-template/.claude/CLAUDE.md` - Template project instructions
- `project-template/.claude/settings.json` - Template project hooks (TypeScript type check)
- `project-template/state.md` - Template state tracking file
- `project-template/.gitignore` - Standard security entries
- `project-template/.gitattributes` - Line ending normalization, linguist overrides
- `project-template/.env.example` - Environment variable template

## References
- Claude Code Memory Docs: https://code.claude.com/docs/en/memory
- Claude Code Best Practices: https://www.anthropic.com/engineering/claude-code-best-practices
- Claude Code Settings: https://code.claude.com/docs/en/settings
- Anthropic blog post on how internal teams use Claude Code: https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf
