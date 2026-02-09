# Project instructions

This repo is a collection of Software Engineering templates used to build **Solutions blueprints** as a Solutions Architect. Blueprints are built by selecting and mixing templates depending on the situation.

## Context

- AI context and scenario details go in **`contexts/`**. Use anything in that folder as input when generating or drafting.

## Output

- Generated documents go in **`output/`** and are always markdown. Use ReadySET templates in **`www/templates/`** as reference for structure and sections, but output markdown only.

## Writing style

- Follow the project writing principles in **`.cursor/rules/writing-principles.mdc`**: plain language, no AI giveaways, direct, conversational; output is always markdown.

## Templates

- Template library under **`www/templates/`** (e.g. design, SRS, QA plan). Use these as the basis for blueprints; mix and adapt as needed per situation.

## Subagents

- When delegating to a subagent (e.g. blueprint-writer or template-researcher), pass relevant context in the prompt: contents or paths from `contexts/`, and which templates or scenario to focus on. Subagents do not see prior conversation or full project context unless the parent includes it.
