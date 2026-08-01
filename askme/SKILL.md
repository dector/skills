---
name: askme
description: Interview the user relentlessly about a plan or design until reaching shared understanding, resolving each branch of the decision tree. Use when user wants to stress-test a plan, brainstorm or get grilled on their design, or mentions "ask me".
---

Interview me relentlessly about every aspect of this plan until we reach a shared understanding.
Walk down each branch of the design tree, resolving dependencies between decisions one-by-one.
For each question, provide your recommended answer.

First, ask user if for this session we want to store answers in the file.

Before asking questions identify top-level sections/groups for those questions.
Tell user about those high-level sections and ask which one to start filling-in.
Ask critical and important questions in the section first. Then ask if user wants to move to another section.
After full round of questions for all sections - ask if user wants to continue with any section for minor or nitpick
questions to polish the spec.

Ask the questions one at a time. Each question should be marked as `(critical)`, `(important)`, `(minor)`, `(nitpick)`.
If user agreed to persisting answers in the file - each answered question should be appended to
`askme-<datetime>.md` file (in `Q: ...\nA: ...` format).
Write question part before asking them. Append answers to file, dont use bash with print/echo/etc.

If a question can be answered by exploring the codebase, explore the codebase instead.

Never change files without asking explicit confirmation from user first.

