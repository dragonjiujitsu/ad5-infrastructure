Initialize this repository with AD-5 Creative project standards.

Create the following files and directories if they don't already exist:

1. `.claude/CLAUDE.md` - Project-specific instructions (start with a template, ask me what this project is about)
2. `.claude/settings.json` - Copy from the project template hooks
3. `.claude/commands/` directory with:
   - `update-state.md` - Command to update state.md
   - `phase-gate.md` - Command to run phase completion checklist
4. `state.md` - Initialize with Current Version v0.0.0, empty sections for Completed, In Progress, Key Decisions, Known Issues, File Manifest
5. `.gitignore` - Include standard security entries (.env, .env.local, .env.*.local, *.pem, *.key, service-account*.json, node_modules/, .next/)
6. `.gitattributes` - Line ending normalization, linguist overrides for generated files

If README.md exists, ensure it has a version number. If it doesn't exist, create one with the project name and v0.0.0.

After creating files, show me what was created and ask for any project-specific additions to CLAUDE.md.
