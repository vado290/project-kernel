---
name: assistant-model-routing
description: Plan which model capability and profile each step of a product uses, ask for model setup only in design (or the quick track's brief solution) and handle model change requests in operation — never handle vendor keys.
metadata:
  template: {name: assistant-model-routing, version: "1.0.0", sha: "953c51c738fdabe8", content_sha: "090337a4edd8f1d88f5ea9cb112b73e19f3d837c17efae44e671f8cd803d2670"}
  version: "1.0.0"
  load: {roles: [pm, supervisor], stages: [requirements, design, build, review, operate, evolution], purposes: [triage, consult, evaluate], on_demand: true}
  changelog:
    - "1.0.0 2026-11-16 New: model plan in design, model setup questions, model change requests in operation (kernel-models.v2)"
---

# Model routing

## What Kernel provides
Kernel owns every model choice and every vendor key. A call names a capability (agent, chat, vision, ocr, asr, tts,
embedding, rerank) and a purpose; Kernel resolves the profile (vendor, model, engine, parameters). Call
`kernel_model_catalog` to see the capabilities with their default profile and the tools or API that can call them today
(`available_via`), the profiles, whether each vendor is configured (true/false only), catalog prices with their date, and
this task's Model plan as Kernel parsed it. Never read provider or secret files, never ask for, print or store a vendor
key, and never call a vendor API directly from a shell or script.

## When model questions are asked
- Design (full track) and the brief solution (quick track): plan the model use and ask for missing setup there, so the
  build and the running product never stop for it.
- Operation: a user's request to change which model an existing capability uses, its tier, the mode or the budget is a
  model change, handled by the Supervisor without a delivery task. A request that adds a capability to the product is
  project work and gets planned like any design.
- Nowhere else. Kernel itself handles keys that stop working at run time.

## Planning (design or brief solution)
1. Prefer no model: rules, parsing and scripts come first.
2. Pick the capability: `chat` for summaries, extraction, classification and format conversion; `vision` to understand an
   image; `ocr` only to transcribe visible text; `asr` / `tts` for speech; `embedding` + `rerank` for retrieval; `agent`
   only where a step needs tools, files or multi-step judgement.
3. Use `profile: default` unless you can say why another profile is needed. Higher tiers are for steps whose mistakes are
   costly or hard to detect; the cost multiplies with every scheduled run. A step that needs image input must use a
   profile whose model takes images; there is no text-only fallback.
4. Write the Model plan in section 3 of the design (in the brief solution on the quick track): a table for the reader and
   one fenced `yaml` block starting with `model_plan:` for Kernel, one row per model call:
   ```yaml
   model_plan:
     - id: M1
       step: transcribe the daily voice memo
       used_by: job:daily-brief          # job id, agent name or script path
       capability: asr
       purpose: daily-brief.transcribe   # lowercase name the product code passes to Kernel
       profile: default
       why: speech-to-text, no judgement needed
       volume: {per_day: 1, unit: audio_minutes, size: 30}
       required: true
       when_unavailable: post the raw audio link with a note
       covers: [R2, D3]
   ```
   `volume` takes `per_day`, `per_week` or `per_month`, a `unit` (`tokens`, `audio_minutes`, `characters`, `calls`) and
   `size` per call; for `tokens` add `output_tokens`, for `calls` give `input_tokens` and `output_tokens`. Do not write a
   setup status; Kernel computes it. No block means the task calls no model.
5. Product code calls models only through what `kernel_model_catalog` lists under `available_via` for the capability,
   passing the purpose — never a vendor, model id, address or key. When nothing is listed, the capability cannot be called
   yet: say so in the design's risks and open items instead of working around it. Every purpose in the code appears in the
   plan.

## Asking for setup
- Only for rows whose vendor `kernel_model_catalog` shows as not configured, after the user has settled that the step is
  needed. One question per vendor, in the same round as the other questions of this stage:
  `{"id": "q3", "text": "<why the product needs it, in the user's language>", "model_setup": {"capability": "asr",
  "purpose": "daily-brief.transcribe", "recommended_vendor": "dashscope"}}`.
- Such a question goes straight to the user. Kernel shows its own input (key entry, validation against the vendor) and
  stores the key where no model can read it through tools. You receive only "configured", "rejected", "skipped" or
  "deferred until release".
- "rejected": the vendor refused the key; say so and ask once more in the next round. "skipped" on a required row is a
  design blocker in section 7. "deferred until release": add `defer_until: release` to the rows of that vendor and record
  "must be configured before release" in section 7.
- Never put a key, a console link with a key or a guessed model id in any question, document or file.

## What Kernel checks
- Moving to build (design → build, or requirements → build on the quick track) needs every required row without
  `defer_until: release` to resolve to a profile whose vendor is configured; release needs all required rows. A broken
  `model_plan` block blocks both. The Supervisor sees the reason in the stages it can move to.
- When a move is blocked by model setup, the Supervisor asks the PM to add the `model_setup` question (or the user to
  defer) — it never asks for a key itself.

## Model change requests (Supervisor, operation)
- Read `kernel_model_catalog` and the route's recent usage, then propose the change with scope, target, from, to, reason,
  expected effect and how to measure it. When the request is vague ("use a better one"), recommend one target with the
  reason and offer alternatives as options instead of asking a series of questions.
- Scope: in a project, change only that project's routes. Global defaults, the mode and the budget change only in the
  kernel project's Supervisor channel; elsewhere, hand the request to kernel.
- Changing the embedding model needs re-indexing; say so in the proposal.
- After a rejection, do not propose the same change again without new evidence.
- Until Kernel offers a model change decision, tell the user what would change and that an administrator applies it with
  `/models`; never edit configuration files yourself.

## Weekly review
Use the model usage section of the review material when it is present (cost, failure, fallback and escalation rates per
route). A model choice can be a root cause; propose the change as "route → profile" with a measurable effect.

## Failures
Report the capability and the error type Kernel returned. Do not retry with another vendor yourself; Kernel's fallback
already ran. On an authentication failure Kernel asks the user; never look for the key.
