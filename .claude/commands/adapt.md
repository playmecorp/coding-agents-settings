# Adapt Commands to Repository

> Analyze the current repository structure and update all commands in `.claude/commands/` to work with this specific codebase. Use interactive prompts when uncertain.

## Instructions

### Phase 1: Discovery
1. Run `git ls-files` to understand the project structure
2. Read `README.md` and any documentation files (CONTRIBUTING.md, docs/*)
3. Read config files: `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, etc.

### Phase 2: Identify & Confirm (Interactive)

For each of the following, attempt to auto-detect. If uncertain or multiple options exist, use AskUserQuestion to confirm with the user:

1. **Project Type**: Single app, monorepo, library, or other?
2. **Backend/Server Path**: Look for `server/`, `backend/`, `api/`, `src/`, `app/server/`
3. **Frontend/Client Path**: Look for `client/`, `frontend/`, `web/`, `app/client/`
4. **Scripts Path**: Look for `scripts/`, `bin/`, or package.json scripts
5. **Package Manager**: npm, yarn, pnpm, bun, uv, pip, poetry, cargo, go, etc.
6. **Test Command**: pytest, jest, vitest, cargo test, go test, etc.
7. **Start Command**: How to run the application (scripts, npm start, etc.)

### Phase 3: Update Commands (In Place)

#### Update plan.md
Using the Edit tool, update these sections:
- `## Relevant Files` - Replace paths with discovered paths for this repo
- `## Validation Commands` - Update test command (e.g., `cd <path> && <test_command>`)
- Package manager references (change `uv add` if using different package manager)

#### Update install.md
Using the Edit tool, rewrite to:
- Use correct package manager install commands for this repo
- Remove repo-specific references (like env file copy scripts)
- Add any setup steps discovered from README

#### Update start.md
Using the Edit tool, rewrite to:
- Use correct start/stop commands for this repo
- Update or remove API endpoints section (or make generic: "See README for endpoints")
- If no start scripts exist, provide instructions based on package.json or README

### Phase 4: Preserve These Commands
Do NOT modify: `prime.md`, `implement.md`, `commit.md`, `tools.md`, `adapt.md`
These are already repository-agnostic.

## Report

After completing adaptation, report:
- Repository type and tech stack detected
- Commands updated and key changes made
- Any items that need manual review
