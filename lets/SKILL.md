---
name: lets
description: Clarify a requested change together, then implement after explicit approval; a request starting with "do" grants immediate approval. Use for quick-feedback development with no unrequested tests, Markdown documentation, or commits.
---

# Collaborative implementation

Apply this workflow to the user's requested change. If no change is provided, ask what they want to build or change.

## Immediate approval with `do`

- A new request beginning with the standalone word `do` (case-insensitive), such as `do this and that`, grants immediate implementation approval for that request. This is especially useful for small follow-up changes. Quoted examples or incidental uses of `do` do not count.
- Read relevant project code and instructions, then briefly state your understanding of the task and any suggestions or recommendations you are making. Proceed immediately without waiting for an additional `go` or confirmation of non-blocking recommendations.
- If a critical ambiguity blocks implementation, ask for clarification first; do not invent a material scope or behavior decision. Otherwise, skip the approval wait in steps 1–2 and proceed to step 3. All other workflow restrictions still apply.

## 1. Establish a shared vision

- Read relevant project code and instructions first where possible, so questions are grounded in the project rather than asking the user for information you can discover.
- Before implementing, ask a few critical questions about the desired behavior, scope, constraints, and acceptance criteria. Focus on decisions that materially affect the result; do not overwhelm the user with a questionnaire.
- Use plain language. Include a concrete example when it makes a question easier to answer.
- For every question, provide your recommendation and briefly explain why you recommend it. Clearly distinguish recommendations from agreed decisions.
- Ask follow-up questions if important ambiguity remains. Do not assume that your recommended option has been accepted.

## 2. Confirm understanding and offer optional refinements

Once the critical decisions are clear:

- Briefly summarize the agreed outcome, scope, and any relevant exclusions so the user can confirm your understanding.
- Suggest a few less important, optional questions or refinements when useful. Label them optional, and give a recommendation and reason for each. Do not invent questions just to prolong the conversation.
- Explain that the user can answer these questions or approve proceeding with the stated recommendations.
- Unless the request qualifies for immediate approval with `do` above, wait for explicit implementation approval. A direct reply such as `go`, `lets go`, `let's go`, or `go on` means you may implement the agreed scope. Equivalent unambiguous approval also counts; quoted examples or incidental uses of these words do not.
- Answers to clarification questions alone are not implementation approval. Before approval, limit work to read-only investigation and discussion; do not change project files or run commands that modify project state.

## 3. Implement in quick-feedback mode

After approval:

- Implement the agreed scope in small, focused changes. Avoid unrelated cleanup or speculative additions.
- If a newly discovered issue requires a material scope or behavior decision, pause and ask rather than silently changing the agreement. Use the same plain-language question, example when useful, recommendation, and reason format.
- Do not create or expand tests unless the user explicitly requests or approves them.
- If a useful behavior can be covered with simple unit tests, ask whether the user wants to take that opportunity. Explain what they would cover and why they would help. Do not suggest UI tests as part of this opportunity, and do not create tests while awaiting an answer.
- Existing tests and non-destructive checks may be run when appropriate; distinguish running existing tests from adding tests. Follow any project-specific execution restrictions.
- Do not create or update Markdown documentation unless the user explicitly requests or approves it. Prefer clear names, structure, and focused code comments that explain non-obvious intent and decisions.
- If something critically needs documentation outside the code, first ask whether the user wants that documentation. Explain what needs documenting, where, and why code alone is insufficient. Wait for approval before writing it.
- Finish with a concise summary of changes, checks actually performed, and any remaining limitations. Do not claim verification that was not performed.

## Commits

- Commit only when the user asks you to commit.
- When asked, use Conventional Commits, for example `feat(scope): add requested behavior` or `fix(scope): handle missing input`.
- Keep the commit scoped to the requested work and do not include unrelated user changes.
- After completing a user-requested commit, ask whether the user wants to add tests or update documentation for the committed change. Mention any relevant coverage or documentation gaps briefly, and avoid re-asking about work already completed or explicitly declined. Wait for explicit approval before adding tests or updating documentation; do not automatically create another commit.

