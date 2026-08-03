---
name: askme-tree
description: Interview the user relentlessly about a plan or design until reaching shared understanding. Use dt_ decision-tree tools as the primary working memory for sections, decisions, priorities, answers, dependencies, status, and notes. Use when user wants to stress-test a plan, brainstorm, get grilled on a design, or mentions "askme-tree".
---

Interview me relentlessly about every aspect of this plan until we reach a shared understanding.
Drive the conversation through a structured decision tree. Resolve high-impact and blocking decisions first, then refine lower-impact details.
For each decision, provide your recommended answer.

Use the `dt_` tools as the source of truth for the session.

## Session setup

1. Initialize and inspect decision-tree state:
   - call `dt_init` when scaffolding may not exist;
   - call `dt_get_session` to understand the active tree and active item.
2. Reuse a suitable active decision tree when it clearly matches the current plan. Otherwise create a new tree with `dt_create_tree`.
3. Identify the main areas of the plan before asking detailed questions.
4. Create each area as a `group` item with an appropriate `priority` field.
5. Briefly tell the user the groups you created and ask which group to start with.

## Modeling rules

- Use `group` items for plan areas, subsystems, phases, or themes.
- Use `decision` items for concrete questions that need an answer.
- Use child decision items when a decision opens follow-up decisions or dependencies.
- Use the tool `priority` field for importance:
  - `critical`: blocking, high-risk, or irreversible decisions;
  - `important`: core design decisions that strongly shape the outcome;
  - `major`: meaningful but not immediately blocking decisions;
  - `minor`: polish or local tradeoffs;
  - `nitpick`: tiny refinements.
- Do not treat priority as only display text. It must be set on the tree item.
- Use notes for durable context:
  - `source: user` for user constraints, preferences, corrections, and rationale;
  - `source: tool` for codebase findings, inferred constraints, and agent observations.

## Asking decisions

Ask one decision question at a time.

Before asking:

1. Choose the next unresolved or highest-leverage topic, using `dt_next_unresolved` when useful.
2. Create or update the relevant `decision` item under the right parent.
3. Set its `priority` accurately.
4. Put the question in the `question` field.
5. Put your recommended answer in the `answer` field when you have one.
6. If the recommendation needs user confirmation, set `answer_stage: need_approval`.
7. If the answer is only a draft that needs agent cleanup, set `answer_stage: need_polishing`.

When asking the user, show a concise prompt with:

- the question;
- why it matters;
- your recommended answer;
- the kind of answer you need from the user.

You may mention the priority in prose, but the real priority is the item field.

## Capturing answers

After the user answers:

1. Update the same decision item.
2. Store the current best answer in the `answer` field. Prefer a clean, useful decision statement over verbatim transcript.
3. Add a `source: user` note for important wording, constraints, rationale, or uncertainty from the user.
4. Set status and answer stage intentionally:
   - `resolved` + `answer_stage: accepted` when the decision is good enough to rely on;
   - `answered` + `answer_stage: need_polishing` when the intent is known but wording/design needs cleanup;
   - `answered` + `answer_stage: need_approval` when the agent proposed an answer that still needs explicit approval;
   - `open` when the question is still unanswered;
   - `superseded` when a newer decision replaces it.
5. If the answer creates follow-up questions, create child decision items or ask the next dependent question.

## Traversal strategy

- Start with `critical` and `important` decisions in the selected group.
- Prefer dependencies before dependent decisions.
- After the high-impact pass in a group, ask whether to continue in that group or switch groups.
- After all groups have a high-impact pass, ask whether to continue with `major`, `minor`, or `nitpick` refinement.
- Use `dt_get_tree` overview for orientation and `dt_get_item` for focused context instead of loading the whole tree unless needed.

## Codebase-aware answers

If a question can be answered by inspecting the codebase, inspect it instead of asking the user.
Record findings on the relevant item as `source: tool` notes, and update the decision answer/status when appropriate.

## Safety

Never change project files unless the user explicitly asks for or approves that change.

