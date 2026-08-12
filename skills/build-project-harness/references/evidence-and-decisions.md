# Evidence and decision governance

Use this reference while auditing history, reconciling conflicts, and updating decision knowledge.

## Separate intent from implementation

Maintain two truths instead of forcing one ranking to answer every question:

- **Desired state**: what the project should do, governed by the user's current explicit direction and current normative project documents.
- **Implemented state**: what the repository does now, demonstrated by code, tests, configuration, runtime output, and observed behavior.

When these differ, record an implementation gap. Do not let stale code overrule a newer confirmed decision, and do not describe an unimplemented decision as current behavior.

## Evidence order

Use this order when evidence speaks to the same kind of claim:

1. The user's current explicit requirement.
2. Applicable `AGENTS.md` instructions and current authoritative ADRs, specifications, or decision indexes.
3. Current code, tests, configuration, and reproducible runtime evidence for implementation facts.
4. Newer explicit confirmations in relevant user-owned project tasks.
5. Preferences repeated consistently across independent tasks.
6. Older conversations, exploratory questions, unconfirmed proposals, task summaries, and agent-authored suggestions.

A higher-ranked source does not erase lower-ranked evidence. Preserve contradictions long enough to identify what changed, whether documentation is stale, and which statement must be retired.

## History audit

- Start from the 50 most recent candidate tasks.
- Match tasks using project root, saved-project identity, referenced paths, and the subject under review.
- Read actual user and final-agent turns for relevant tasks; use titles and previews only to find candidates.
- Treat an agent proposal as a proposal until the user explicitly confirms it or later repository evidence shows it became authoritative.
- Group retries and continuations that represent the same decision sequence.
- Exclude subagent, worker, reviewer, guardian, or generated evaluation tasks from user-decision counts unless they contain direct user input.
- Prefer the later explicit confirmation when two confirmed decisions conflict. Record the earlier one as superseded rather than deleting its historical existence.
- Expand beyond 50 tasks only for a concrete missing link, conflict, or referenced earlier decision.

If task relationships cannot be proven, label the evidence uncertain. If history tools expose only a bounded set, report that bound.

## Decision states

- **已确认**: A user-approved invariant or behavior. Implementation and review must follow it until a newer confirmed decision replaces it.
- **结构暂定**: The capability or outcome is required, while naming, placement, hierarchy, layout, or interaction form remains adjustable.
- **候选方案**: An unapproved option. It may guide discussion or prototyping but cannot become an implementation requirement.
- **已废止**: A former rule explicitly replaced by a newer decision. Keep only the context needed to prevent accidental revival.

Confirmation applies only to the proposal visible in that turn. Do not widen a narrow “确认” to adjacent topics.

## Decision record shape

Keep the index compact. Use one row or entry per decision domain:

```markdown
| Domain | Status | Current decision | Authoritative detail | Supersedes |
| --- | --- | --- | --- | --- |
| <domain> | 已确认 | <one-sentence rule> | <ADR/spec/contract path> | <old rule or —> |
```

Store detailed state machines, schemas, interaction rules, and acceptance criteria in one topic contract, not in the index. Historical knowledge may record why a choice changed, but must link back to the index or contract for the current rule.

## Confirmation packet

Use this compact shape and adapt labels to the user's language:

```markdown
## <Topic>

**Current understanding — <建议确认为「已确认」 / 结构暂定 / 候选方案>**

<Complete, decision-ready proposal.>

**Evidence and boundary**

<Material repository/history evidence, conflicts, inclusions, and exclusions.>

**Replaces**

<Prior rule that becomes 已废止, or “None”.>

Please confirm this topic or identify the exact correction.
```

Do not attach the next topic, implementation plan, or final harness proposal to the same confirmation packet.
