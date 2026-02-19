# AD-5 Creative - Global Standards

## Identity
- Organization: AD-5 Creative
- Owner: Shawn
- Skills repo: dragonjiujitsu/ad5_claude_skills (read relevant skills before writing code for that area)

## Required Files in Every Repo
- `CLAUDE.md` (or `.claude/CLAUDE.md`) with project-specific instructions
- `state.md` tracking version, completed work, in-progress, decisions, issues, file manifest
- `README.md` with semantic version (vX.Y.Z), bumped on every commit
- `.gitignore` with security entries
- `.gitattributes` for line ending normalization

## state.md is the Handoff Document
- Updated after every implementation session
- If it's not in state.md, it didn't happen
- Sections: Current Version, Last Update, Completed, In Progress, Key Decisions, Known Issues, File Manifest

## Workflow: Explore, Plan, Code, Commit
1. Read relevant files and state.md. Do not write code yet.
2. Make a plan. Use "think hard" for complex problems. Document the plan if the task is large.
3. Implement. Verify as you go.
4. Commit with descriptive message. Update state.md and README version.

## Commit Messages
- Prefix: `feat:`, `fix:`, `refactor:`, `docs:`, `deprecate:`, `chore:`
- Descriptive: `feat: add Serper.dev image search integration` not `feat: update`

## Versioning
- vMAJOR.MINOR.PATCH in README.md
- MAJOR: breaking changes or phase completion
- MINOR: new features
- PATCH: bug fixes, docs

## Security (NON-NEGOTIABLE)
- NEVER hardcode API keys, tokens, or secrets
- Use environment variables via `.env.local`
- Server-only keys: no `NEXT_PUBLIC_` prefix
- `.gitignore` MUST include: `.env`, `.env.local`, `.env.*.local`, `*.pem`, `*.key`, `service-account*.json`

## TypeScript Standards
- Strict mode always
- No `any` without justification comment
- Types in `types/` directory, not inline
- camelCase variables/functions, PascalCase components/types

## Next.js Standards
- App Router only. Never Pages Router.
- Server Components by default. `"use client"` only when needed.
- External API calls through `/api` routes only
- `error.tsx` and `loading.tsx` for every route segment

## Styling
- Websites (marketing): Tailwind CSS
- Internal tools/pipelines: CSS Modules
- Never dynamic Tailwind classes (`bg-${color}-500`)

## Context Management
- Use `/clear` between unrelated tasks
- Use "think hard" or "ultrathink" for complex planning
- Keep CLAUDE.md concise. Refine it like a prompt.
- Use sub-agents for investigation to preserve main context

## Phase Gate
- Complete each phase before starting the next
- Run `/phase-gate` before marking complete
- After each phase: update state.md, bump version, commit

## Forbidden
- Hardcoded secrets
- `any` without comment
- Client-side external API calls
- Committing .env files
- Pages Router
- console.log in production
- Skipping state.md updates
- Writing code before reading CLAUDE.md and state.md
