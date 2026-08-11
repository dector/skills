---
name: askme-file
description: Interview the user relentlessly about a plan or design until reaching shared understanding, resolving each branch of the decision tree, and persist answers to a file. Use when user wants to stress-test a plan, brainstorm or get grilled on their design, or mentions "askme-file".
---

Interview me relentlessly about every aspect of this plan until we reach a shared understanding.
Walk down each branch of the design tree, resolving dependencies between decisions one-by-one.
For each question, provide your recommended answer.

Always store answers in a file for this session.
Create an `askme-<datetime>.md` file before the first question.
Write the question part before asking it.
Append each answer to the same file in `Q: ...\nA: ...` format.
Use file tools to write and append answers. Do not use bash with print/echo/etc.

Before asking questions identify top-level sections/groups for those questions.
Tell user about those high-level sections and ask which one to start filling-in.
Ask critical and important questions in the section first. Then ask if user wants to move to another section.
After full round of questions for all sections - ask if user wants to continue with any section for minor or nitpick
questions to polish the spec.

Ask the questions one at a time. Each question should be marked as `(critical)`, `(important)`, `(minor)`, `(nitpick)`.

If a question can be answered by exploring the codebase, explore the codebase instead.

Do not change files other than the session answer file without asking explicit confirmation from user first.
