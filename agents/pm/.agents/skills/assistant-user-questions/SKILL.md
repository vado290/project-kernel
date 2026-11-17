---
name: assistant-user-questions
description: Design and arrange questions for the user (multi-question cards) — when to ask, what to ask and how, so the user answers quickly and accurately; both the PM's questions and the Supervisor's relaying follow it.
metadata:
  template: {name: assistant-user-questions, version: "1.2.0", sha: "32ee4dfa19b9d1c0", content_sha: "1f1769efb01ae05e3673d51be290b55da15673e32c40734ce714b56da5812c5b"}
  version: "1.2.0"
  load: {roles: [pm, supervisor]}
  changelog:
    - "1.2.0 2026-11-05 Ask only what is needed now and minimise user-supplied material"
    - "1.1.0 2026-10-23 Written in English, the skills' source language; questions are written in the user's language (ROUND6, 0.46.0)"
    - "1.0.0 2026-10-16 First version: users often cannot say clearly what they need, so the quality of the questions decides how well requirements are collected"
---

# Asking the user

## Purpose
The user's answers are the main source of requirements, but the user's time is the most valuable. A good question takes
the user seconds to answer, and the answer can be used directly.

## When to ask
- Ask only what changes the solution, scope, acceptance criteria or business result; find out yourself first what you
  can (read files, read the charter, look things up).
- Combine independent questions needed for the next decision in one round; do not fill a quota. Ask none when the
  information suffices, or one when only one decision is missing. Follow the user's collaboration preferences; do not
  ask dependent questions before their prerequisites are settled.
- When the user's answers contradict each other, you must clarify — never pick one yourself.

Before requesting material, distinguish decisions or access only the user can provide from facts you can obtain within
the current grants. Check relevant available tools and existing evidence first; a failed access route is not proof that
all routes are unavailable. When help is still needed, request the smallest sufficient input, state what it enables and
why you cannot obtain it. Do not ask for full documents by default when a relevant excerpt or reference suffices.

## Writing each question
Format: `{"id": "q1", "text": "…", "required": true, "options": ["…"], "recommended": "…"}`, written in the user's
language.
1. **The first 40 characters must make sense alone**: the card's input title shows only the first 45 characters; put
   explanations in the second half.
2. **Give options**: 2–5 concrete options where possible, plus "other (please explain)"; when you are confident, give
   recommended with a one-sentence reason in the question.
3. **Say why you ask**: a second half like "(used for …)" says what the answer affects, so the user answers carefully.
4. **One thing per question**; never ask an open question as a yes/no question.
5. **Allow "not sure"**: when the user cannot answer, accept "not sure", record it under the document's open items and
   state your default assumption.
6. **required**: only questions without which you cannot continue are required; the rest are optional, to spare the user.

## Order of questions
First locating questions (who, in what situation, solving what), then details, then trade-offs and confirmations. Earlier
answers may make later questions moot, so do not ask locating questions and details that depend on them in the same
round.

## Handling contradictions
Put the two statements side by side and ask which one holds, for example: "You first said the daily report is for the
team, later that it is only for you. Which holds? (options: the team / only me / both)". Record the user's decision in
the requirements document under resolved contradictions.

## When the Supervisor relays the PM's questions
- Merge duplicates, reword them so the user can answer easily, and keep which PM question ids each covers (covers).
- Where existing material settles an answer, give it with its basis in suggested — but still let the user confirm.
- Never drop a required PM question; for one the user need not answer, give a suggested answer and its basis.

## Common mistakes
- Open questions like "any other requirements?": the user does not know where to start. List likely directions to pick
  from instead.
- Splitting independent necessary questions across rounds, or adding questions merely to fill a batch.
- Questions in technical jargon: use the user's industry language.
