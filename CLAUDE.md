# CLAUDE.md

This file provides guidance to AI assistants (Claude and others) working in this repository.

---

## Repository Overview

**Repository:** virgildobos/Claude
**Status:** Freshly initialized — no source code has been committed yet.

This file serves as the ground-truth reference for conventions, workflows, and structural expectations so that AI assistants can contribute safely and consistently from the very first commit.

---

## Directory Structure

```
Claude/
├── CLAUDE.md          # This file — AI assistant guidance
└── (future source)    # To be added as the project grows
```

As the project evolves, update this section to reflect the real layout (e.g., `src/`, `tests/`, `docs/`, config files, etc.).

---

## Development Workflow

### Branching Strategy

- **Main branch:** `main` (protected — never push directly)
- **Feature branches:** `claude/<short-description>-<session-id>`
  - Example: `claude/add-auth-module-Abc12`
- **Bugfix branches:** `fix/<short-description>`
- **Release branches:** `release/<version>`

Always branch off `main` unless instructed otherwise.

### Typical Workflow

```bash
# 1. Start from main
git checkout main
git pull origin main

# 2. Create a feature branch
git checkout -b claude/<feature>-<session-id>

# 3. Make changes, then commit
git add <files>
git commit -m "feat: concise description of what changed and why"

# 4. Push the branch
git push -u origin claude/<feature>-<session-id>

# 5. Open a Pull Request targeting main
```

### Git Push Rules

- Always use `git push -u origin <branch-name>` (not bare `git push`).
- Branch names **must** start with `claude/` and end with the matching session ID, or the push will be rejected with HTTP 403.
- On transient network failures, retry up to 4 times with exponential backoff: 2 s → 4 s → 8 s → 16 s.

---

## Commit Message Conventions

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<optional scope>): <short summary>

[optional body — explain *why*, not *what*]

[optional footer: breaking changes, issue refs, session URL]
```

| Type       | When to use                                      |
|------------|--------------------------------------------------|
| `feat`     | New feature or capability                        |
| `fix`      | Bug fix                                          |
| `docs`     | Documentation-only change                        |
| `refactor` | Code restructuring without behaviour change      |
| `test`     | Adding or updating tests                         |
| `chore`    | Tooling, config, dependency updates              |
| `ci`       | CI/CD pipeline changes                           |

**Examples:**

```
feat(auth): add JWT refresh token support

fix(api): handle null response from upstream service

docs: update CLAUDE.md with branching conventions
```

Keep the subject line ≤ 72 characters. Use imperative mood ("add", not "added").

---

## Code Conventions

> Update this section when a primary language/framework is chosen.

### General Rules

- **Clarity over cleverness** — prefer readable code over terse tricks.
- **No dead code** — remove unused functions, imports, and variables.
- **No commented-out code** — use git history instead.
- **Minimal abstraction** — don't create helpers for one-time operations; avoid premature generalization.
- **No backwards-compat hacks** — if something is removed, delete it fully.
- **No over-engineering** — implement only what is needed now.

### Security

- Never commit secrets, credentials, API keys, or `.env` files.
- Validate all user-supplied input at system boundaries.
- Avoid introducing OWASP Top 10 vulnerabilities (XSS, SQL injection, command injection, etc.).

### Error Handling

- Only add error handling for scenarios that can realistically occur.
- Trust internal framework guarantees; don't defensively wrap code that cannot fail.
- Validate at external boundaries (user input, API responses, file I/O).

---

## Testing

> Populate this section once a test framework is chosen.

- Run the full test suite before opening a PR.
- New behaviour should be covered by at least one test.
- Aim for fast, deterministic tests; avoid flaky assertions.

**Placeholder commands (update when real tooling is added):**

```bash
# Run all tests
<test-command>

# Run a single test file
<test-command> <file>

# Check coverage
<coverage-command>
```

---

## Pull Request Guidelines

1. **Title:** Short, descriptive, ≤ 70 characters (mirrors the commit subject).
2. **Body:** Include:
   - A brief summary (1–3 bullet points).
   - A test plan (what was manually verified or what tests cover it).
   - Links to related issues or the Claude session URL.
3. **Scope:** Each PR should address a single concern. Avoid mixing unrelated changes.
4. **Reviews:** At least one approval is required before merging into `main`.
5. **Squash merges:** Preferred to keep `main` history linear and readable.

---

## AI Assistant Guidelines

### What AI assistants should do

- Read files before modifying them.
- Make the minimum change required — no unsolicited refactors or style fixes.
- Run available tests after code changes to verify correctness.
- Create a new commit rather than amending an existing one.
- Ask for confirmation before irreversible or broad-impact actions (force push, dropping tables, deleting branches, sending external messages).

### What AI assistants should avoid

- Pushing to `main` or any branch not designated for the current session.
- Skipping pre-commit hooks (`--no-verify`).
- Adding docstrings, comments, or type annotations to code that was not changed.
- Creating new files when editing an existing file is sufficient.
- Over-engineering solutions or adding features beyond what was requested.
- Committing secrets or sensitive data.
- Using `git add -A` / `git add .` without verifying what gets staged.

### Handling Ambiguity

If instructions are unclear or an action could be destructive, pause and ask the user before proceeding. The cost of a brief clarification is always lower than the cost of unwanted data loss or unintended side effects.

---

## Environment & Tooling

> Update this section as tools are adopted.

| Concern        | Tool / Convention                  |
|----------------|------------------------------------|
| Language       | TBD                                |
| Package manager| TBD                                |
| Linter         | TBD                                |
| Formatter      | TBD                                |
| Test framework | TBD                                |
| CI/CD          | TBD                                |

---

## Updating This File

Keep CLAUDE.md current as the project evolves:

- Add real directory structure once files exist.
- Fill in language-specific conventions, lint/format commands, and test commands.
- Update the tooling table whenever a new tool is adopted or removed.

Treat this file as living documentation — a PR that adds a new framework should also update CLAUDE.md to describe how that framework is used.
