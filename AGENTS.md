# AGENTS.md - ECC Subagent & Multi-Agent Orchestration Protocol

This repository uses the Everything Claude Code (ECC) agent architecture adapted natively for Google Antigravity.

## Specialized Subagent Roles & Summoning Protocol

Antigravity can summon any of the 68 ECC specialized agents on-demand. When complex, cross-cutting tasks arise, decompose the objective and delegate to specialized subagents:

### Primary Subagent Roster

| Role | Subagent Name | Recommended Model | Best For |
| :--- | :--- | :---: | :--- |
| **System Architect** | `architect` | `pro` | System design, technical trade-offs, scalability planning |
| **Code Reviewer** | `code-reviewer` | `pro` / `inherit` | Auditing PRs, adherence to clean code & solid principles |
| **Security Auditor** | `security-reviewer` | `pro` | Vulnerability scanning, auth audits, input sanitization |
| **TDD Specialist** | `tdd-guide` | `pro` / `inherit` | Test-driven development, failing assertions, mocking |
| **Build Error Resolver** | `build-error-resolver` | `flash` | Rapidly diagnosing and fixing compilation & type errors |
| **Performance Engineer**| `performance-engineer`| `pro` | Profiling, query optimization, memory leak mitigation |
| **Database Specialist** | `database-optimizer` | `pro` | Schema design, indexing, migrations, SQL tuning |
| **Frontend Architect** | `frontend-specialist` | `inherit` | React/Next.js UI patterns, accessibility, component composition |
| **Docker & Cloud Ops** | `devops` | `pro` | Dockerfiles, container optimization, CI/CD pipelines |

## Subagent Invocation Workflow

To spawn a specialized ECC agent:
1. Query agent parameters:
   ```powershell
   python C:\Users\bhave\.gemini\config\skills\ECC_Expert\scripts\ecc_agent_bridge.py info <agent_name>
   ```
2. Define and invoke the subagent using `define_subagent` and `invoke_subagent`.
3. Receive findings and integrate the synthesized result into the primary workflow.

## Rule Files Active
All project-specific rules reside in `.agents/rules/`.
To stage rules for current technology stack:
```powershell
python C:\Users\bhave\.gemini\config\skills\ECC_Expert\scripts\ecc_rules_router.py apply
```
