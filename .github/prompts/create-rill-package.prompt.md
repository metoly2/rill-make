---
mode: agent
description: Create a complete rill package from a specification using the rill-make architecture.
---

Create a complete rill package in this workspace, following the same architecture and guardrails as the `rill-make` Claude plugin.

Input specification:

${input:Describe the package or paste a spec path (for example ./spec.md)}

Execution requirements:

1. Follow the 8-phase orchestration in `skills/create-rill-package/SKILL.md`.
2. Use `ARCHITECTURE.md` as the source of truth for the blueprint schema and architect/engineer/reviewer split.
3. Write the blueprint to `<package>/.rill-design/blueprint.md` before implementation.
4. Implement from blueprint only. If unclear, stop and report `Blueprint gap` instead of guessing.
5. Use these file ownership boundaries:
   - Design: extension plan, prompt inventory, pipeline blueprint, custom extension API designs.
   - Implementation: `rill-config.json`, `prompts/*.prompt.md`, `.rill` scripts, and `extensions/*.ts`.
   - Validation: run checks and conformance review.
6. Ensure custom extensions are thin wrappers around SDK/API calls. Keep business logic in rill scripts.
7. Validate with:
   - `rill check` on each `.rill` script
   - `rill check --types` when `extensions/` exists
8. End with:
   - package tree
   - generated file list
   - provisioning checklist for required external credentials/resources
   - exact run commands (`npm run dev`, and `npm run build && npm run serve` if HTTP serve requested)

Use Posix-compatible shell commands in examples. On Windows, target WSL paths and commands.
