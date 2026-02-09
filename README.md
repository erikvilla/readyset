# ReadySET – Solutions Architect blueprint templates

This repository is a collection of **Software Engineering templates** used to build **Solutions blueprints** as a Solutions Architect. Blueprints are built by selecting and mixing templates from the library depending on the situation.

- **Templates**: ReadySET document templates live in `www/templates/` (e.g. SRS, plan, design, QA, use cases, release checklist). See [ReadySET project overview](www/index.html) for the full list.
- **Context**: Put scenario details and AI context in the `contexts/` folder.
- **Output**: Generated documents go in `output/` and are always markdown. Templates in `www/templates/` are HTML and are used as reference for structure and sections; output is markdown only.

---

## Cursor setup

This project is configured for [Cursor](https://cursor.com) with rules, commands, and subagents so the AI follows project conventions and writing style.

### Rules (`.cursor/rules/`)

- **project-conventions.mdc** – Always applied. Where to read context (`contexts/`), where to write output (`output/`), template location (`www/templates/`), example template paths, and how to delegate to subagents (pass context in the prompt).
- **writing-principles.mdc** – Always applied. Core writing principles: plain language, no AI giveaways, direct, conversational, no buzzwords; output always markdown (templates used as reference); tone guidelines.

### Commands (`.cursor/commands/`)

Trigger with `/` in Agent chat. You can add extra context after the command name (e.g. `/generate-blueprint for the security review scenario`).

- **/generate-blueprint** – Use `contexts/`, choose or mix templates, produce a blueprint in `output/`.

### Subagents (`.cursor/agents/`)

Custom subagents the main Agent can delegate to (each runs in its own context):

- **blueprint-writer** – Writes full Solutions blueprint documents from context and templates.
- **template-researcher** – Explores `www/templates/` and recommends which templates to mix.
- **mermaid-expert** – Expert in Mermaid.js; creates and refines flowcharts, sequence diagrams, class/state/ER diagrams, and other Mermaid charts for blueprints or architecture.

When delegating to a subagent, the parent Agent should pass relevant context in the prompt (e.g. contents or paths from `contexts/`, which scenario or templates to use). Subagents do not see prior conversation or full project context unless the parent includes it.

### AGENTS.md

Project root instructions for the Agent: role, `contexts/`, `output/`, writing style pointer, templates, and subagent delegation note. Kept short; details live in `.cursor/rules/`.

### Optional: .cursorignore

To exclude files from Cursor’s semantic search and AI context (e.g. secrets or large directories), add a `.cursorignore` file in the project root using [.gitignore-style syntax](https://cursor.com/docs/context/ignore-files). Example:

```
.DS_Store
# **/.env
# **/secrets.json
```

### Optional: Skills and nested AGENTS.md

- **Skills**: Project commands can be migrated to [Agent Skills](https://cursor.com/docs/context/skills) (e.g. via `/migrate-to-skills` in Agent chat) for the open Skills standard and optional scripts/references.
- **Nested AGENTS.md**: Cursor supports `AGENTS.md` in subdirectories. Add one in a subfolder if that area has different conventions.

---

## Quick start

1. Put your scenario or context in `contexts/`.
2. In Cursor Agent chat, run `/generate-blueprint` (optionally add context after the command).
3. Generated documents appear in `output/` in markdown.

All generated content follows the project writing principles (plain, direct, no AI giveaways, professional tone).
