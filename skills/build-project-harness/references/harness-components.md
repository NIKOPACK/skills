# Adaptive harness components

Read this reference only after the project decisions are confirmed or when auditing an existing harness. Select the smallest set that prevents observed recurring errors.

## Selection test

For every proposed component, identify:

1. the repeated failure or rediscovery cost it addresses;
2. why the repository or an existing document is not already the source of truth;
3. its exact inputs, output, and owner;
4. a checkable completion or validation criterion;
5. the existing artifact it updates or supersedes.

Omit a component that cannot pass this test.

## Decision index and topic contracts

Use an existing ADR index, product specification, or decision log when it already answers “which rule is current?” Create `docs/project-decisions.md` only when no equivalent authority exists.

The index owns status and routing, not full detail. A topic contract is justified when one domain needs substantial schemas, state transitions, interaction rules, or acceptance criteria. Keep each rule authoritative in exactly one contract.

Minimum decision-index shape:

```markdown
# Project decisions

## Status semantics

- 已确认
- 结构暂定
- 候选方案
- 已废止

## Current decisions

| Domain | Status | Current decision | Authoritative detail | Supersedes |
| --- | --- | --- | --- | --- |

## Update rule

Update status here first, then update the single owning contract and retire conflicting statements.
```

## `AGENTS.md`

Use `AGENTS.md` only for stable instructions that should affect nearly every task in its directory scope:

- authority order and required knowledge entry points;
- architectural or data-integrity invariants;
- safety and secret-handling boundaries;
- required validation gates;
- rules for preserving user-owned working-tree changes.

Keep temporary plans, UI preferences limited to one feature, current file inventories, and discoverable package scripts in their existing sources. Prefer pointers over copied contract text.

## Project skill

Create or update one project skill when agents repeatedly need a project-specific workflow or evidence-routing map. It should tell an agent what to read, how to trace the relevant execution path, how to choose structural versus local change, and how to validate.

Keep domain details in references loaded by branch. Do not create one skill per feature. Generate `agents/openai.yaml` and validate the skill with the available skill tooling.

## Hooks

Add a hook only when all are true:

- the rule is deterministic and machine-checkable;
- violations are costly or recurrent;
- existing formatter, linter, type checker, test, CI rule, or platform permission does not already enforce it;
- false positives can be kept low;
- the hook has automated tests and explicit failure output.

Good candidates include secret patterns, forbidden destructive commands, generated-file consistency, or a precise authority-file invariant. Product judgment, architectural taste, and fuzzy document conflicts belong in review, not hooks.

## Custom agents

Add a custom agent only for a recurring bounded role with a distinct context or permission profile, such as read-only path exploration or invariant review. Define its inputs, prohibited mutations, evidence format, and completion criterion.

Reuse a small number of roles across domains. Keep final product decisions and overlapping edits with the main agent. Do not create agents merely to mirror the project's feature list.

## Scripts

Add a script when the same deterministic transformation or consistency check would otherwise be rewritten. Use standard-library or existing project dependencies when practical. Test the script on representative valid and invalid cases.

Do not encode changing product judgment in a script. Keep secrets outside source and accept environment-specific values through explicit parameters or environment variables.

## Existing harness migration

Inventory current ownership before editing. Retain effective components, merge complementary content, and convert stale duplicates into pointers or explicit archived history. Avoid parallel names such as `new`, `v2`, or copied Skill directories.

Before deleting an artifact, include its exact replacement and deletion in the user-confirmed harness proposal. Preserve unrelated edits and verify the final authority graph has no cycles or competing current sources.

## Final harness proposal

Present the final structure as one confirmation topic:

```markdown
## Project harness structure

| Component | Action | Responsibility | Validation | Replaces |
| --- | --- | --- | --- | --- |
| <path/type> | create/update/retire | <single responsibility> | <check> | <old source or —> |
```

State explicitly which possible components are omitted and why. After confirmation, implement exactly this structure and no broader product changes.
