---
name: "speckit-specify"
description: "Create or update the feature specification from a natural language feature description."
compatibility: "Requires spec-kit project structure with .specify/ directory"
metadata:
  author: "github-spec-kit"
  source: "templates/commands/specify.md"
---


## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Pre-Execution Checks

**Check for extension hooks (before specification)**:
- Check if `.specify/extensions.yml` exists in the project root.
- If it exists, read it and look for entries under the `hooks.before_specify` key
- If the YAML cannot be parsed or is invalid, do not skip silently: tell the user that `.specify/extensions.yml` could not be read (include the parser error) and that no hooks were checked, including any mandatory (`optional: false`) hooks registered there, then continue normally
- Filter out hooks where `enabled` is explicitly `false`. Treat hooks without an `enabled` field as enabled by default.
- For each remaining hook, do **not** attempt to interpret or evaluate hook `condition` expressions:
  - If the hook has no `condition` field, or it is null/empty, treat the hook as executable
  - If the hook defines a non-empty `condition`, skip the hook and leave condition evaluation to the HookExecutor implementation
- When constructing command invocations from hook command names, replace dots (`.`) with hyphens (`-`). For example, `speckit.git.commit` → `$speckit-git-commit`.
- For each executable hook, output the following based on its `optional` flag:
  - **Optional hook** (`optional: true`):
    ```
    ## Extension Hooks

    **Optional Pre-Hook**: {extension}
    Command: `/{command}`
    Description: {description}

    Prompt: {prompt}
    To execute: `/{command}`
    ```
  - **Mandatory hook** (`optional: false`):
    ```
    ## Extension Hooks

    **Automatic Pre-Hook**: {extension}
    Executing: `/{command}`
    EXECUTE_COMMAND: {command}

    Wait for the result of the hook command before proceeding to the Outline.
    ```
    After emitting the block above you MUST actually invoke the hook and wait for it to finish before continuing. Run it the same way you would run the command yourself in this agent/session (the invocation may differ from the literal `{command}` id shown above, e.g. a skills-mode agent runs it as `/skill:speckit-...` or `$speckit-...`). Emitting the block alone does not run the hook.
- If no hooks are registered or `.specify/extensions.yml` does not exist, skip silently

## Outline

The text after `$speckit-specify` is the feature description. If it is empty, stop with `No feature description provided`.

1. Create one feature directory under `specs/` unless the user supplied `SPECIFY_FEATURE_DIRECTORY`. Use `.specify/init-options.json` numbering and the next available sequence; keep the feature name separate from the Git branch name.
2. Resolve `spec-template` through the project override/preset resolver, create `spec.md` from it, and persist the relative directory to `.specify/feature.json`. Do not create or switch branches unless an enabled hook does so.
3. Read `.specify/memory/constitution.md` and follow its project constraints.
4. Write a concise, user-focused spec using the active template:
   - Keep the goal and scope brief; include only requirements needed to define the feature.
   - Use only distinct user stories needed to organize implementation. One story is enough for a small feature; retain priorities and acceptance criteria for task traceability.
   - Do not repeat acceptance criteria in a separate functional-requirements list. Add cross-cutting requirements only when they add information.
   - Include success metrics, edge cases, assumptions, entities, or open questions only when they materially help define or verify the feature.
   - Avoid generic background, duplicated rationale, filler examples, and implementation architecture unless requested.
   - Treat significant performance, rendering, platform, multiplayer-authority, dependency, and monetization decisions as explicit decisions; ask the user when no safe default is clear.
   - Aim for about 40–70 lines for a typical feature. Exceed this only to capture distinct requirements or risks.
5. If a material choice is unresolved, use no more than three `[NEEDS CLARIFICATION: ...]` markers. Present concise options and wait for the user before treating the spec as ready. Make and label reasonable low-impact assumptions.
6. Create `checklists/requirements.md` as a separate, concise review artifact. Check that the goal/scope are clear, stories and acceptance criteria are testable, constraints and non-goals are explicit, important edge cases and assumptions are covered, Constitution rules are respected, and unresolved material questions are surfaced. Mark an item complete only after checking it.
7. Review the spec against the checklist. Fix clear omissions without expanding unrelated scope; ask the user about material ambiguities. Do not claim readiness while a material decision is unresolved.

## Mandatory Post-Execution Hooks

**You MUST complete this section before reporting completion to the user.**

Check if `.specify/extensions.yml` exists in the project root.
- If it does not exist, or no hooks are registered under `hooks.after_specify`, skip to the Completion Report.
- If it exists, read it and look for entries under the `hooks.after_specify` key.
- If the YAML cannot be parsed or is invalid, do not skip silently: tell the user that `.specify/extensions.yml` could not be read (include the parser error) and that no hooks were checked, including any mandatory (`optional: false`) hooks registered there, then continue to the Completion Report.
- Filter out hooks where `enabled` is explicitly `false`. Treat hooks without an `enabled` field as enabled by default.
- For each remaining hook, do **not** attempt to interpret or evaluate hook `condition` expressions:
  - If the hook has no `condition` field, or it is null/empty, treat the hook as executable
  - If the hook defines a non-empty `condition`, skip the hook and leave condition evaluation to the HookExecutor implementation
- When constructing command invocations from hook command names, replace dots (`.`) with hyphens (`-`). For example, `speckit.git.commit` → `$speckit-git-commit`.
- For each executable hook, output the following based on its `optional` flag:
  - **Mandatory hook** (`optional: false`) — **You MUST emit `EXECUTE_COMMAND:` for each mandatory hook**:
    ```
    ## Extension Hooks

    **Automatic Hook**: {extension}
    Executing: `/{command}`
    EXECUTE_COMMAND: {command}
    ```
    After emitting the block above you MUST actually invoke the hook and wait for it to finish before continuing. Run it the same way you would run the command yourself in this agent/session (the invocation may differ from the literal `{command}` id shown above, e.g. a skills-mode agent runs it as `/skill:speckit-...` or `$speckit-...`). Emitting the block alone does not run the hook.
  - **Optional hook** (`optional: true`):
    ```
    ## Extension Hooks

    **Optional Hook**: {extension}
    Command: `/{command}`
    Description: {description}

    Prompt: {prompt}
    To execute: `/{command}`
    ```

## Completion Report

Report completion to the user with:
- `SPECIFY_FEATURE_DIRECTORY` — the feature directory path
- `SPEC_FILE` — the spec file path
- Checklist results summary
- Readiness for the next phase (`$speckit-clarify` or `$speckit-plan`)

**NOTE:** Branch creation is handled by the `before_specify` hook (git extension). Spec directory and file creation are always handled by this core command.

## Quick Guidelines

- Describe what the player or contributor needs and how success is observed; leave architecture to the approved plan.
- Keep the spec concise and avoid repeating the Constitution or the same behavior in multiple sections.
- Preserve the separate quality checklist and the user's opportunity to resolve material questions.

## Done When

- [ ] `spec.md` is concise, scoped, and checked against `checklists/requirements.md`
- [ ] Material clarifications are resolved or explicitly left for the user
- [ ] Required extension hooks were dispatched or skipped per the hook rules
- [ ] The feature directory, spec path, checklist result, and next step are reported
