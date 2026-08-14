# D365 Consulting Assistant

This repository is a personal multi-agent setup for a Senior Consultant focused on **Dynamics 365 Sales, Dynamics 365 Field Service, Power Platform, Microsoft 365 Copilot, and Copilot Studio**. It uses Claude Code subagents (defined in [.claude/agents/](.claude/agents/)) so that requests get handled by the agent best suited to the topic, instead of one generic assistant trying to cover everything.

## How this works

- Each file in `.claude/agents/` is a Claude Code subagent with its own focus area, written so Claude delegates to it automatically based on the request — you don't need to invoke agents by name.
- Use this repo as a place to accumulate reusable knowledge (client-agnostic): functional/configuration know-how, customizing patterns, communication templates, estimation heuristics. Don't store client-confidential data here.
- When you learn something durable during a session (a useful pattern, a recurring pitfall, a template that worked well), add it to the relevant agent file instead of letting it stay only in chat history.

## Agents

- [functional-consultant.md](.claude/agents/functional-consultant.md) — D365 Sales & Field Service process & configuration, security model, fit-gap analysis, functional specs.
- [technical-consultant.md](.claude/agents/technical-consultant.md) — Power Platform (Power Apps, Power Automate, Dataverse), Copilot Studio, M365 Copilot extensibility, ALM/DevOps.
- [power-automate-developer.md](.claude/agents/power-automate-developer.md) — Power Automate flow refinement, solution design, implementation review, and documentation generated from a flow's exported JSON.
- [project-customer-manager.md](.claude/agents/project-customer-manager.md) — status reports, customer emails, meeting minutes, risk/issue tracking.
- [presales-architect.md](.claude/agents/presales-architect.md) — solution design, demos, estimates, RFP/proposal content for D365 Sales, Field Service, Power Platform, and Copilot.
- [certification-coach.md](.claude/agents/certification-coach.md) — Microsoft Business Applications certification path guidance, exam prep, and practice questions (Dynamics 365, Power Platform, Copilot/AI role-based certs).

## Global availability of agents

The agent files in `.claude/agents/` are hardlinked into `~/.claude/agents/` (user-level), so they're automatically available in any project folder you open Claude Code in — not just this repo. Edit either copy; both point to the same file content. If a hardlink ever breaks (e.g. OneDrive replaces a file during sync), re-create it: `New-Item -ItemType HardLink -Path <global path> -Target <repo path> -Force`.

## Project-specific context

Client/engagement context (current project, your role on it, stakeholders, status, decisions) does **not** belong in this repo — this repo is shared, client-agnostic knowledge. Keep each engagement's context in that project's own working folder, as its own `CLAUDE.md`, separate from this one. That folder picks up the global agents automatically (see above) without exposing client data here.

Use [templates/PROJECT-CONTEXT-TEMPLATE.md](templates/PROJECT-CONTEXT-TEMPLATE.md) as the starting point for a new project folder's `CLAUDE.md`.

## MCP servers

- `microsoft-learn` ([.mcp.json](.mcp.json)) — official Microsoft Learn MCP server (`microsoft_docs_search`, `microsoft_docs_fetch`, `microsoft_code_sample_search`), no auth required. Use it to verify current Microsoft docs/behavior instead of relying on potentially outdated knowledge, especially for Power Platform, Copilot Studio, and D365 Sales specifics that change frequently.

## Conventions

- Write everything in English.
- Keep agent files as living documents, organized by topic, not chronologically.
- Prefer concrete checklists and templates over abstract advice — these get reused under time pressure.
