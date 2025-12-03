# Create .claude/commands Structure

> Automatically create the complete `.claude/commands/` directory structure with all command files for a new repository.

## Instructions

1. Create the `.claude/commands/` directory if it doesn't exist
2. Create all command files listed below with their exact content
3. Do NOT modify the content of any files
4. Report completion with list of created files

## Run

Execute the following steps to create the complete structure:

### Step 1: Create Directory Structure

```bash
mkdir -p .claude/commands
```

### Step 2: Create All Command Files

Create each file with the exact content specified below.

---

#### File: `.claude/commands/adapt.md`

```markdown
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
```

---

#### File: `.claude/commands/commit.md`

```markdown
# Generate Git Commit

Based on the `Instructions` below, follow the `Run` section to create a git commit with a properly formatted message. Then follow the `Report` section to report the results of your work.

## Instructions

- Generate a concise commit message in the format: `<agent_name>: <issue_class>: <commit message>`
- The `<commit message>` should be:
  - Present tense (e.g., "add", "fix", "update", not "added", "fixed", "updated")
  - 50 characters or less
  - Descriptive of the actual changes made
  - No period at the end
- Examples:
  - `sdlc_planner: feat: add user authentication module`
  - `sdlc_implementor: bug: fix login validation error`
  - `sdlc_planner: chore: update dependencies to latest versions`
- Extract context from the issue JSON to make the commit message relevant
- Don't include any 'Generated with...' or 'Authored by...' in the commit message. Focus purely on the changes made.

## Run

1. Run `git diff HEAD` to understand what changes have been made
2. Run `git add -A` to stage all changes
3. Run `git commit -m "<generated_commit_message>"` to create the commit

## Report

Return ONLY the commit message that was used (no other text)
```

---

#### File: `.claude/commands/implement.md`

```markdown
# Implement the following plan
Follow the `Instructions` to implement the `Plan` then `Report` the completed work.

## Instructions
- Read the plan, think hard about the plan and implement the plan.
- IMPORTANT: This command expects the plan to be a file path to a spec file (e.g., `specs/feature-name.md`).
- As you complete each phase and task in the Implementation Plan and Step by Step Tasks sections:
  1. Update the spec file by checking off the completed checkbox (- [ ] → - [x])
  2. Fill in the Status field with completion status (e.g., "Completed", "In Progress", "Partially Done")
  3. Fill in the Comments field with brief notes about what was done, any issues encountered, or important decisions made
- Update the spec file progressively after completing each phase/task, not just at the end.
- Use the Edit tool to update checkboxes and fields in the spec file as you progress.

## Plan
$ARGUMENTS

## Report
- Summarize the work you've just done in a concise bullet point list.
- Report the files and total lines changed with `git diff --stat`
- Note any checkboxes that were checked off and any Status/Comments added to the spec file
```

---

#### File: `.claude/commands/install.md`

```markdown
# Install & Prime

## Read and Execute
.claude/commands/prime.md

## Run
Install FE and BE dependencies
Run `./scripts/copy_dot_env.sh` to copy the .env file from the chief_ai_academy_workshop_1 directory.

## Report
Output the work you've just done in a concise bullet point list.
```

---

#### File: `.claude/commands/plan.md`

```markdown
# Feature Planning

Create a new plan in specs/*.md to implement the `Feature` using the exact specified markdown `Plan Format`. Follow the `Instructions` to create the plan use the `Relevant Files` to focus on the right files.

## Instructions

- You're writing a plan to implement a net new feature that will add value to the application.
- Create the plan in the `specs/*.md` file. Name it appropriately based on the `Feature`.
- Use the `Plan Format` below to create the plan. 
- Research the codebase to understand existing patterns, architecture, and conventions before planning the feature.
- IMPORTANT: Replace every <placeholder> in the `Plan Format` with the requested value. Add as much detail as needed to implement the feature successfully.
- Use your reasoning model: THINK HARD about the feature requirements, design, and implementation approach.
- Follow existing patterns and conventions in the codebase. Don't reinvent the wheel.
- Design for extensibility and maintainability.
- If you need a new library, use `uv add` and be sure to report it in the `Notes` section of the `Plan Format`.
- Respect requested files in the `Relevant Files` section.
- Start your research by reading the `README.md` file.

## Relevant Files

Focus on the following files:
- `README.md` - Contains the project overview and instructions.
- `app/server/**` - Contains the codebase server.
- `app/client/**` - Contains the codebase client.
- `scripts/**` - Contains the scripts to start and stop the server + client.

Ignore all other files in the codebase.

## Plan Format

```md
# Feature: <feature name>

## Feature Description
<describe the feature in detail, including its purpose and value to users>

## User Story
As a <type of user>
I want to <action/goal>
So that <benefit/value>

## Problem Statement
<clearly define the specific problem or opportunity this feature addresses>

## Solution Statement
<describe the proposed solution approach and how it solves the problem>

## Relevant Files
Use these files to implement the feature:

<find and list the files that are relevant to the feature describe why they are relevant in bullet points. If there are new files that need to be created to implement the feature, list them in an h3 'New Files' section.>

## Implementation Plan
IMPORTANT: Each phase should be a checkbox that will be checked off during implementation. Include Status and Comments fields for tracking progress.

- [ ] **Phase 1: Foundation** - <describe the foundational work needed before implementing the main feature>
  - Status:
  - Comments:

- [ ] **Phase 2: Core Implementation** - <describe the main implementation work for the feature>
  - Status:
  - Comments:

- [ ] **Phase 3: Integration** - <describe how the feature will integrate with existing functionality>
  - Status:
  - Comments:

## Step by Step Tasks
IMPORTANT: Execute every step in order, top to bottom. Each task should be a checkbox that will be checked off during implementation. Include Status and Comments fields for tracking progress.

<list step by step tasks as checkboxes with h3 headers for grouping. Format each task as:
- [ ] **Task description** - <detailed explanation>
  - Status:
  - Comments:

Use as many h3 headers as needed to organize the tasks. Order matters, start with the foundational shared changes required then move on to the specific implementation. Include creating tests throughout the implementation process. Your last step should be running the `Validation Commands` to validate the feature works correctly with zero regressions.>

## Testing Strategy
### Unit Tests
<describe unit tests needed for the feature>

### Integration Tests
<describe integration tests needed for the feature>

### Edge Cases
<list edge cases that need to be tested>

## Acceptance Criteria
<list specific, measurable criteria that must be met for the feature to be considered complete>

## Validation Commands
Execute every command to validate the feature works correctly with zero regressions.

<list commands you'll use to validate with 100% confidence the feature is implemented correctly with zero regressions. every command must execute without errors so be specific about what you want to run to validate the feature works as expected. Include commands to test the feature end-to-end.>
- `cd app/server && uv run pytest` - Run server tests to validate the feature works with zero regressions

## Notes
<optionally list any additional notes, future considerations, or context that are relevant to the feature that will be helpful to the developer>
```

## Feature
$ARGUMENTS
```

---

#### File: `.claude/commands/prime.md`

```markdown
# Prime
> Execute the following sections to understand the codebase then summarize your understanding.

## Run
git ls-files

## Read
README.md
```

---

#### File: `.claude/commands/start.md`

```markdown
IMPORTANT: ALWAYS execute this command when /start is invoked. Do NOT skip running the command.

Use the Bash tool to execute:
sh ./scripts/stop_apps.sh && sh ./scripts/start.sh 300s

After the Bash command completes, parse the output from start.sh to determine which ports were actually used for the frontend and backend, then report:

The Natural Language SQL Interface application is now running!

## Access URLs:
- Frontend Application: http://localhost:[FRONTEND_PORT]
- Backend API: http://localhost:[BACKEND_PORT]
- API Documentation (Swagger): http://localhost:[BACKEND_PORT]/docs
- API Documentation (ReDoc): http://localhost:[BACKEND_PORT]/redoc

Where [FRONTEND_PORT] and [BACKEND_PORT] are extracted from the start.sh output.

## Available API Endpoints:
- POST /api/upload - Upload CSV or JSON files to create SQLite tables
- POST /api/query - Convert natural language questions to SQL queries
- GET /api/schema - Retrieve database schema and table information
- POST /api/insights - Generate statistical insights from data
- GET /api/health - Check service health and database status
- DELETE /api/table/{table_name} - Delete a specific table

Note: The script automatically kills any existing processes on the required ports before starting to ensure a clean launch.
```

---

#### File: `.claude/commands/tools.md`

```markdown
# List Built-in Tools

List all core, built-in non-mcp development tools available to you. Display in bullet format. Use typescript function syntax with parameters.
```

---

## Report

After creating all files, report:
- Total number of files created
- List of all created files with their paths
- Confirmation that all files were created with exact content

