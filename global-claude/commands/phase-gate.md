Run the AD-5 phase gate checklist before marking a phase complete.

Check all of the following:

## Build
- [ ] TypeScript compiles without errors (`npm run build`)
- [ ] No hardcoded secrets in code (grep for API keys, tokens, passwords)
- [ ] All API routes handle errors with proper status codes

## Standards
- [ ] state.md is current and accurate
- [ ] README.md version number is updated
- [ ] All new files are listed in state.md File Manifest
- [ ] Commit messages use proper prefixes (feat:, fix:, etc.)
- [ ] No `any` types without justification comments

## UI (if applicable)
- [ ] Loading states implemented for async operations
- [ ] Error boundaries in place (error.tsx)
- [ ] Works on mobile viewport

## Security
- [ ] No API keys in code (only in .env.local)
- [ ] .env files are in .gitignore
- [ ] External API calls only through /api routes
- [ ] Environment variables documented in .env.example

Report results. Flag any failures. Do not mark the phase complete until all checks pass.

$ARGUMENTS
