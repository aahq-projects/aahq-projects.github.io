# AGENTS.md

## Purpose
- This file defines the default operating rules for AI coding agents in this repository.
- Treat this repository as an early-stage workspace: do not assume a framework, runtime, or package manager until a manifest or user instruction confirms it.

## Current Repository State
- Root files currently present: `.gitignore`, `aahq-projects.code-workspace`.
- No verified app source tree, package manifest, build config, or CI workflow is present yet.
- When new subprojects appear, prefer adding a closer `AGENTS.md` inside that subdirectory instead of overloading this root file.

## Commands
- Install deps: infer from the nearest manifest only after verifying it exists.
- Run dev: infer from the nearest manifest or task config only after verifying it exists.
- Run tests: use the narrowest available command for the touched area.
- If no executable validation exists, state that explicitly and validate via focused file review or diff.

## Working Rules
- Start from the most local anchor: file, symbol, failing command, failing test, or nearby implementation.
- Prefer small reversible edits over broad refactors.
- Preserve existing style and public APIs unless the task requires a change.
- Do not invent folders, scripts, env vars, or workflows that are not present in the repo or requested by the user.

## Project Structure
- Root context files live in the repository root: `AGENTS.md`, `DESIGN.md`, `MARKETING.md`.
- Product-specific code should live in explicit subdirectories when introduced.
- If the repo becomes a monorepo, keep global rules here and place local overrides inside each app or package.

## Code Style
- Follow the style already established in the touched files.
- Prefer explicit names over short names.
- Keep comments sparse and only when they add real explanatory value.
- Avoid unrelated formatting churn.

## Testing
- Validate the smallest changed surface first.
- Prefer behavior-scoped tests over full-suite runs.
- If the repository has no tests yet, do not add speculative test infrastructure unless requested.

## PR Instructions
- Keep changes focused and easy to review.
- Include the user-visible effect, touched files, and validation performed.
- Call out assumptions when the repository lacks concrete runtime or business context.

## Boundaries
- Always: verify local context before editing, keep changes minimal, and preserve user work.
- Ask first: adding dependencies, introducing new apps or services, changing project structure substantially.
- Never: commit secrets, fabricate product facts, rewrite unrelated files, or replace user changes without permission.