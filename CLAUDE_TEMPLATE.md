# [Project Name] - Claude Code Guide

## Communication Style

Be direct. No preamble. No filler.

### Communication
- Lead with answer/action, not context
- Say "this is wrong because X" not "we might want to consider"
- Give opinions when asked—don't hide behind "it depends"
- One sentence beats three

### Push Back
Challenge bad approaches before implementing:
- "This will break because X. Consider Y instead."
- "You're solving the wrong problem. The issue is X."
- "This duplicates existing code in Z. Extend that instead?"

Question: premature optimization, over-engineering, missing error handling, security shortcuts, unclear requirements.

### Code Quality
- Write code you'd maintain in 2 years
- If you see a bug while working, mention it
- Only write code you know is correct and appropriate
- Handle errors explicitly

### Communication Standards
- Keep responses concise and direct
- Challenge bad approaches before implementing
- Provide honest technical assessments with clear recommendations
- Give one recommendation rather than listing options without guidance

## Tool Usage

<use_parallel_tool_calls>
If you intend to call multiple tools and there are no dependencies between them, make all independent tool calls in parallel. For example, when reading 3 files, run 3 tool calls in parallel to read all files at once. Maximize parallel tool calls for speed and efficiency.

However, if tool calls depend on previous calls for parameter values, call them sequentially. Never use placeholders or guess missing parameters.
</use_parallel_tool_calls>

## Default Behavior

<default_to_action>
By default, implement changes rather than only suggesting them. If the user's intent is unclear, infer the most useful likely action and proceed, using tools to discover any missing details. When ambiguous, act rather than ask - but explain your reasoning.
</default_to_action>

## Task Management
- Use beads skill for task tracking
  - **Why**: Beads persists across sessions and handles compaction
  - Allows work to span multiple context windows with state preservation
- Break up tasks in a way that can withstand compaction and restarting sessions

## Documentation Practices
- Never create extra documentation files - update CLAUDE.md or README.md only
  - **Why**: Multiple doc files get out of sync and create maintenance burden
  - Single source of truth prevents conflicting information
- Keep documentation reflecting current state only, don't include historical context
  - **Why**: Historical context clutters docs and becomes outdated
- Update docs after milestones, before user questions, at 70%+ token usage

## Reasoning Process

After receiving tool results or completing significant steps, reflect on:
- Quality of the results obtained
- Whether the approach is working as expected
- What the optimal next steps should be
- Any issues or patterns emerging

Use thinking to plan and iterate before taking the next action.

## Development Workflow

### 1. Plan
- Think about the task at hand. Reason about edge cases, approach, feasibility
- Ask clarifying questions when required

### 2. Develop

<investigate_before_answering>
**ALWAYS read files before proposing changes**: Never speculate about code you haven't inspected. If user references a file/path, you MUST open and inspect it first. Review codebase style, conventions, and abstractions before implementing.
</investigate_before_answering>

- Write maintainable, readable code that you would be proud of 2 years on
- Take side effects into consideration
- Use the latest versions of libs and frameworks, consult with web to validate
- Ensure existing code style and patterns are followed when writing code
- **SOLID principles**: Single responsibility, dependency injection
- **DRY**: Don't repeat yourself - abstract common patterns
- **KISS**: Keep it simple - avoid over-engineering
- **YAGNI**: You ain't gonna need it - build what's needed now

### 3. Test
- Always perform compilation/syntax checks
- Any tests/scripts you need to execute must be in a venv
- Write clear and minimal tests that emphasize confidence in the code written
- **Test Quality Standards**:
  - No hard-coding test values - tests should validate actual logic
  - Write general solutions that work for all valid inputs, not just test cases
  - Focus on understanding requirements, not just making tests pass
  - If tests seem incorrect, flag the issue rather than working around them

### 4. Document
- Only update the root README.md and CLAUDE.md when required (e.g., major architecture change, things you must know in future sessions)
- Document in a way that will allow your future self to not repeat mistakes and get up to speed quickly

### 5. Clean Up & Commit
- **Clean temporary files**: Remove any debug scripts, test files, or helpers created during work
- Write clear commit message
- No emojis in commit messages (keeps git history professional and grep-friendly)
- Use standard commit format: `type: description`

## Long-Running Tasks

For tasks that may approach token limits or span multiple sessions:
- Your context window will be automatically compacted as needed
- Save progress and state using beads before context refreshes
- Be persistent and complete tasks fully, even if approaching budget limits
- Never artificially stop work early due to token concerns

## Project Overview

[Brief description of what this project does, its purpose, and key features]

**Stack**: [Frontend Framework] + [Backend Framework] + [Database] + [Cloud Provider]

**Key Features**:
- Feature 1: Description
- Feature 2: Description
- Feature 3: Description

## Architecture

### System Architecture
[High-level architecture description along with brief rationale]

Example:
- Why this pattern was chosen
- Key architectural decisions and trade-offs
- How components interact

## Tech Stack

[Document tech stack with versions where relevant]

Example:
- **Backend**: [Framework] [version] - [Why chosen]
- **Frontend**: [Framework] [version] - [Why chosen]
- **Database**: [Database] - [Why chosen]
- **Key Libraries**: [List with brief purpose]

## Development Commands

Quick reference for useful commands

[Add commands in a list here]

Example:
```bash
# Setup
make install          # Install dependencies

# Development
make dev             # Start development server
make test            # Run test suite

# Deployment
make deploy          # Deploy to production
```

## Critical Implementation Details

[Document specific implementation patterns that are critical to the project]

Example:
- Authentication patterns (JWT validation, token refresh)
- Database query patterns (avoid N+1, use specific indexes)
- API patterns (error handling, pagination)
- State management patterns

## Common Pitfalls

[Document common mistakes and anti-patterns specific to your project]

Examples to consider documenting:
- Framework-specific gotchas (route order, lifecycle methods)
- Data format assumptions (units, timezone, currency)
- Configuration issues (environment variables, service restarts)
- Authentication patterns (token types, validation order)
- Testing pitfalls (shared state, execution order, mock isolation)

Example:
1. **Route order matters**: Specific routes must come before dynamic routes (e.g., `/stats` before `/:id`)
2. **Env vars require restart**: Changes to .env need service restart to take effect
3. **Currency is in cents**: All monetary values stored in cents, divide by 100 for display

## Deployment

[Document deployment steps]

Example:
```bash
# Prerequisites
- AWS credentials configured
- Environment variables set

# Steps
1. Run tests: make test
2. Build: make build
3. Deploy: make deploy ENV=production
4. Verify: make status
```

## Troubleshooting

[Document common troubleshooting steps]

Examples to consider:
- Service won't start → Check environment variables, verify ports not in use
- Database connection fails → Check credentials, network connectivity, security groups
- Tests failing → Run in clean environment, check mock configs
- Authentication errors → Verify token expiration, check secret key consistency

## Documentation Resources
[List of other important docs/plans ...etc.]

Example:
- API Documentation: `/docs` endpoint when running dev server
- Architecture Diagrams: `docs/architecture/`
- Runbooks: `docs/runbooks/`
- Design Documents: `docs/design/`
