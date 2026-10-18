# Antigravity Operating Directives (Improvised ECC Architecture)

This document establishes the project engineering standards, behavioral protocols, and harness optimizations for Google Antigravity, powered by the **Everything Claude Code (ECC)** agent ecosystem.

---

## 1. The 7-Step Engineering Loop

Every software engineering task must adhere to the structured ECC discipline:

```text
Plan ──> Test ──> Implement ──> Review ──> Verify ──> Remember ──> Improve
```

1. **Plan**: Formulate clear contracts, evaluate architectural trade-offs, and map dependencies before modifying files.
2. **Test (TDD Discipline)**: Write failing unit/integration assertions first. Validate that tests fail for expected reasons before writing implementation code.
3. **Implement**: Write minimal, idiomatic, and maintainable implementation code that satisfies the tests.
4. **Review**: Audit code quality, edge cases, type safety, and security vulnerabilities from a critical perspective.
5. **Verify**: Execute test suites, linters, and type checkers using `run_command` to establish empirical evidence of correctness.
6. **Remember**: Document architectural decisions, bug roots, and patterns in session artifacts.
7. **Improve**: Continuously refine workflows, prevent regressions, and eliminate technical debt.

---

## 2. Dynamic ECC Skill & Agent Ecosystem Access

Antigravity is connected to the full offline repository of **293 domain skills**, **68 specialized agents**, and **122 language/framework rules** located at `C:\Users\bhave\.gemini\ecc\`.

### Context Window Optimization
Rather than polluting the context window with hundreds of skill definitions, Antigravity uses progressive on-demand discovery:
- **Search Skills**: `python C:\Users\bhave\.gemini\config\skills\ECC_Expert\scripts\manage_ecc.py search "<keyword>"`
- **Read Skill**: `view_file AbsolutePath='C:\Users\bhave\.gemini\ecc\skills\<skill_name>\SKILL.md'`
- **Install Pack into Workspace**: `python C:\Users\bhave\.gemini\config\skills\ECC_Expert\scripts\manage_ecc.py install-pack <pack_name>`
- **Summon Specialized Agent**: Use `ecc_agent_bridge.py` to inspect or define any of the 68 specialized agents:
  `python C:\Users\bhave\.gemini\config\skills\ECC_Expert\scripts\ecc_agent_bridge.py info <agent_name>`
- **Auto-Stage Tech Stack Rules**: `python C:\Users\bhave\.gemini\config\skills\ECC_Expert\scripts\ecc_rules_router.py apply`

---

## 3. Tool Usage & Modification Standards

- **Surgical Edits**: ALWAYS use `replace_file_content` for editing existing files. Replace the exact minimal contiguous block. NEVER rewrite an entire file when only changing a few lines.
- **Inspect Before Editing**: Always view the relevant lines using `view_file` to verify the exact whitespace, imports, and surrounding context.
- **Empirical Verification**: Never assume changes work without running tests or syntax checks via `run_command`. Check exit codes and compiler output.
- **User Clarification**: When architectural choices or requirements are ambiguous, use `ask_question` with structured, direct options instead of guessing.

---

## 4. Security & Safety Protocol (AgentShield)

- **Zero Secret Exposure**: Never output, hardcode, or commit API keys, GitHub tokens, passwords, private certificates, or secrets.
- **Data Protection**: Obtain explicit user confirmation before executing any irreversible deletion (`DROP TABLE`, `rm -rf`, `git reset --hard` on uncommitted work).
- **Injection Defense**: Always use parameterized queries for SQL, sanitize shell arguments, and validate untrusted input at boundaries.
- **Defensive Error Handling**: Fail loudly with informative error messages; never silently catch and suppress exceptions.

---

## 5. Git & GitHub Workflow

- **Conventional Commits**: Format commit messages as `feat: ...`, `fix: ...`, `refactor: ...`, `test: ...`, `docs: ...`.
- **Branch Cleanliness**: Keep commits focused and self-contained. Verify `git status` and `git diff` before committing.
- **GitHub CLI Integration**: Leverage `gh` for pull requests (`gh pr create`), issues (`gh issue list`), and repo inspections.
- **GitHub MCP Tools**: Leverage the native `github` MCP server for direct API actions when enabled.
