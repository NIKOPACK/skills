---
name: build-project-harness
description: Govern cross-task project decisions by auditing a software repository and its Codex task history, reconciling conflicting or unsettled requirements one topic at a time, and creating or updating the project's authoritative knowledge and minimal Codex harness. Use when the user's goal is to stop repeating project decisions, turn prior project conversations into durable authority, or design or overhaul a project-level harness spanning multiple components such as AGENTS.md guidance, skills, hooks, and custom agents. Do not use for ordinary implementation, bug fixing, code review, routine documentation edits, isolated agent-file maintenance, or synthesizing an already-settled conversation into one spec.
---

# Build Project Harness

Build a project memory system that preserves decisions without turning historical conversation into unquestioned truth. Keep product code read-only unless the user separately requests implementation.

## 1. Audit before asking

1. Locate the project root and read every applicable `AGENTS.md` completely.
2. Inspect `git status --short` and relevant existing diffs. Treat pre-existing changes as user-owned.
3. Inventory current authority and harness artifacts: specifications, ADRs, decision logs, architecture and product documents, `.codex/**`, tests, validation commands, and equivalent agent configuration.
4. Trace the relevant implementation and tests far enough to distinguish intended behavior from current behavior. Code is implementation fact, not automatic product authority.
5. If project-task tools are available, list up to the 50 most recent candidate tasks, filter by project path or saved-project identity and subject relevance, then read the actual relevant turns. Treat titles and summaries only as discovery hints. Expand farther back when a current claim references older work, evidence conflicts, or the first pass is insufficient.
6. Exclude clearly derived subagent tasks, retry copies, and unrelated tasks from decision counts. Retain uncertain items as low-confidence evidence rather than silently discarding them.
7. If task history is unavailable or incomplete, state the exact gap and ask for task IDs or exported conversations when that gap blocks a reliable decision. Never claim complete historical coverage without evidence.
8. Read [evidence-and-decisions.md](references/evidence-and-decisions.md) before classifying evidence or persisting a decision.

Complete the audit only when the existing authority chain, current implementation facts, historical conflicts, unresolved topics, and current harness components are identified.

## 2. Build the topic map

Group unresolved decisions into coherent domains. Order foundational topics before dependent ones: product boundary and vocabulary, core invariants and data relationships, behavior and failure rules, user interaction, then implementation or rollout constraints.

Keep an internal ledger for every claim:

- proposed status;
- supporting evidence and confidence;
- contradictory evidence;
- current authoritative destination;
- decision it would supersede.

Do not create the final harness yet. Start with the highest-impact unresolved topic.

## 3. Confirm one topic at a time

Submit exactly one decision domain per user turn. Give the user a concrete proposal to approve, not an abstract question. Include only what is needed to decide:

- **Current understanding**: the complete proposed rule or product behavior;
- **Proposed status**: `建议确认为「已确认」`, `结构暂定`, or `候选方案`; never label an unconfirmed proposal simply `已确认`;
- **Evidence and gap**: the material facts or conflicts that shaped it;
- **Boundary**: what this decision includes and excludes;
- **Replacement**: any prior rule that would become `已废止`.

End the turn by asking the user to confirm or correct that topic. Do not advance to another topic in the same turn.

When the user corrects the proposal, rewrite the whole topic with the correction and request confirmation again. A correction is not persisted as confirmed merely because it is specific. When the user confirms, persist that topic before presenting the next one.

## 4. Persist each confirmation

After each explicit confirmation:

1. Reuse the project's existing authoritative ADR, specification, or decision index when one already owns the rule.
2. If no suitable authority exists, create `docs/project-decisions.md` as the decision index. Create a topic contract only when the index would otherwise contain substantial interaction, schema, or acceptance detail.
3. Record the current rule once, its status, its authoritative detail location, and the rule it supersedes. Mark superseded statements `已废止` or replace them with a pointer to the current authority.
4. Keep `结构暂定` and `候选方案` out of `AGENTS.md`. Put only confirmed, stable, cross-task invariants there, and only during the final harness stage.
5. Show the user what knowledge artifact changed, then present the next single topic.

Preserve one source of truth. Historical notes may explain evolution, but they must point to rather than duplicate current rules.

## 5. Propose the minimal harness

After every decision domain is confirmed, read [harness-components.md](references/harness-components.md). Audit recurring error patterns and propose one final topic: the exact harness structure, the responsibility of every component, files to update in place, obsolete sources to retire, and validation to add.

Require explicit confirmation of this structure. Then implement only justified components:

- a decision index when no equivalent authority exists;
- `AGENTS.md` for stable cross-task invariants;
- one project skill for project-specific evidence routing and execution workflow;
- hooks only for deterministic, high-confidence checks not covered by existing gates;
- custom agents only for recurring, bounded roles;
- scripts only for repeated deterministic work or validation.

Update an existing harness in place. Consolidate duplicate authority instead of creating a parallel version. Preserve useful content and unrelated user changes. Retire obsolete statements explicitly; delete an artifact only when its replacement and deletion scope were included in the confirmed harness proposal.

## 6. Validate and finish

1. Parse every added or modified JSON, YAML, and TOML file.
2. Run the relevant skill validator and actual tests for every hook or script.
3. Run existing project checks that directly validate changed harness behavior; do not use product-code edits to make harness checks pass.
4. Inspect the final diff for duplicated authority, project-specific facts leaked into a global skill, hidden fallbacks, stale rules, broad error swallowing, secret exposure, and unapproved product-code changes.
5. Report the resulting authority chain, created or updated components, validation evidence, and any history or runtime checks that could not be completed.

Finish only when every confirmed topic has one authoritative home, every superseded rule is retired or clearly marked, the implemented harness matches the confirmed structure, and validation passes or remaining failures are explicitly attributed.
