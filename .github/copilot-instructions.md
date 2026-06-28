# Copilot Instructions for rill-make

This repository ships a Claude plugin and a Copilot prompt pack for authoring rill packages. When helping with package generation, preserve the same architecture and workflow used by the Claude skill.

## Core workflow

Use the same phase model as `skills/create-rill-package/SKILL.md`:

1. Verify prerequisites (`Node >= 22.16.0`, `@rcrsr/rill-cli >= 0.19.5`, Posix or WSL).
2. Fetch rill docs and extension index with `curl -sL`.
3. Gather requirements and clarifying answers.
4. Design extension plan.
5. Probe extension surfaces with `rill describe project --stubs`.
6. Produce a frozen blueprint at `<package>/.rill-design/blueprint.md`.
7. Implement strictly from blueprint.
8. Validate using `rill check` and `rill check --types`.

## Separation of concerns

Keep these boundaries explicit even when running as a single Copilot session:

- Architect role: extension selection, pipeline design, custom extension API design.
- Engineer role: write `rill-config.json`, `.rill`, `.prompt.md`, and TS extension files from blueprint.
- Reviewer role: run checks and grade conformance against the blueprint.

Do not redesign during implementation. If blueprint is incomplete, raise a "Blueprint gap" and resolve design first.

## Rill invariants

- Use rill closures with full `^("...")` decoration and typed params.
- Use `=>` capture, never `=` assignment.
- Use `list[...]` and `dict[...]` literals.
- Keep business logic in rill scripts; custom extensions are thin wrappers.
- Keep static config in `rill-config.json`, secrets as `${VAR_NAME}` placeholders.
- Externalize multiline or parameterized prompts to `prompts/*.prompt.md`.

## Repository references

- Architecture: `ARCHITECTURE.md`
- End-user flow: `GUIDE.md`
- Claude skill orchestration: `skills/create-rill-package/SKILL.md`
- Agents:
  - `agents/rill-architect.md`
  - `agents/rill-engineer.md`
  - `agents/rill-reviewer.md`
