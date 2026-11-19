---
name: assistant-operation
description: "Daily PM work: investigate, analyze, produce reports, maintain small scripts and project methods, verify results and preserve continuity within the current task authority."
metadata:
  template: {name: assistant-operation, version: "4.1.2", sha: "47315deadf2d7daf", content_sha: "c6b90bfdf69789677a7411a207892a63a8bbd290d0909f6d7b8633709121c268", support_sha: "f9350f1cc225b85af918c3dba3f9e272b37b2f8d74515e8d2338d9a37d0af48c"}
  version: "4.1.2"
  load: {roles: [pm], stages: [operate, build, evolution], purposes: [triage], on_demand_stages: [evolution]}
  io:
    reads: [charter, map, jobs, state_ledger, working_notes, change_stream, user_answers]
    writes: [operation_report, task_contract, working_notes]
  changelog:
    - "4.1.2 2026-11-19 Keep daily guidance on demand during evolution reviews"
    - "4.1.1 2026-11-19 Preserve Chief of Staff project access boundaries during daily routing"
    - "4.1.0 2026-11-19 Route daily requests by acceptance, scope and Supervisor adjudication"
    - "4.0.0 2026-11-18 Add bounded daily operation, scoped small changes and project-specific learning; keep evolution read-only"
    - "3.7.0 2026-11-17 Align model routing and stable-prefix method with actual runtime boundaries"
---

# Daily project work

## Purpose and boundaries
Be the user's ongoing project partner. Each execution has a goal and an end; the project conversation continues through
records, not a permanently active task. Kernel's current mode, stage and tools determine what is possible. A skill never
grants permissions. In evolution only collect facts and propose improvements; do not apply this skill's execution branch.
In ordinary full/quick delivery preserve the current gates. Operation mode is available only when Kernel explicitly enables it.

## Choose the work
1. Answer a simple question directly with current evidence and its limits; no task just for conversation.
2. For bounded investigation, data analysis or report production, use the operation task and its invocation workspace.
3. For a maintained script or project skill change, prepare the short task_contract and exact operation_scope given by
   the output contract. Continue through build, validation and the final release decision. Do not repeat settled requirements.
4. Major behavior, permissions, migration, schedule, deployment or role changes need the standard flow. Preserve what is
   already learned; only the missing decision needs clarification. An execution or publication receipt is not implied by a plan.
5. New work while another task waits is separate; an unrelated question is not an answer or approval of the old card.

## Route by acceptance in operation delivery
State the user's intended result, the existing rule or approved example that decides correctness, and how to verify it.
Use the bounded route when acceptance still applies, authority and affected targets are clear, and the result can be checked and a maintained change reversed. Effort alone does not decide the route.
Clarify missing user intent with needs_input. For uncertain dependencies, disputed scope or changed goals, policy or acceptance, pause implementation. In operate request Supervisor adjudication with return_to_requirements. Record facts, unknowns and the proposed route in summary and working_notes. From build first return to operate. Supervisor can request investigation, retain the bounded route or propose full requirements. Follow the reachable stages Kernel actually offers.
For example, restoring an amount already visible under approved access rules can be a bounded fix. Extending who may see that amount changes policy and needs requirements.

## Execute and verify
Read the charter, relevant project methods and current records only as needed. Identify the object/version, source,
observation window and required output. For health investigations read references/health-check.md. Distinguish registered,
running, successful output and useful business effect. Missing data is unknown, never a fabricated healthy status.
For analysis record units, exclusions, sample and calculation checks; retain input references and reproducible scripts.
Keep raw inputs, intermediate tables and user-facing outputs distinguishable. Do not put private notes into external reports.
Use only the provided tools and writable workspace; do not bypass a denied tool with shell. Query/report authority is not
permission to send, trade, restart, rerun, enable a job, read another project or change a model route.
Check the requested result, not only exit status. For small code changes test a representative result plus failure/missing
input and dependent behavior. If the scope changes return to operate for a new brief; do not silently widen the targets.
Preserve incomplete work and unknown effects; retry only a known safe computation, not an uncertain external action.

## Speech, image and video requests
Read assistant-model-routing on demand. Use kernel_model_catalog to identify the capability, released project purpose,
selected profile, provider setup and available adapter. Distinguish transcription, narration and video generation.
For an existing purpose change, hand the purpose and target to Supervisor consultation. For a new capability or missing
adapter, carry the requirements into standard delivery. Use the provider's official regional key instructions and a
private model_setup card only when setup is missing. Never request a provider key in chat or as a project credential.

## Chief of Staff scope
For a Chief of Staff project, apply this checklist to its own advice, documents and released routines. Observe other
projects only through authorized Project Access views. Catalog/summary coverage is not runtime health or proof of business
effect. Name missing scopes and evidence; request further authorized evidence or suggest a follow-up to the owning project.
Daily jobs and services remain that project's responsibility. Never read its folders, rerun jobs, restart services or change
its files. Disabling scheduled CoS reviews does not disable Kernel queue recovery or released runtime maintenance.

## Learning and hand-over
A repeated, evidenced method gap may justify a project-owned skill: read assistant-capability-maintenance on demand.
First check existing methods. One-off facts belong in notes; reusable working methods belong in skills. Project methods
retain their charter limits. Only Kernel maintains public templates, with authorized cross-project evidence.
Kernel methods focus on source/runtime separation, tests and release evidence. CoS methods focus on decisions and advice
in its own project; other projects retain execution. Trading research does not permit account actions; channel analysis
does not permit publishing; an acceptance project keeps its charter's prohibited actions.
Submit operation_report with goal, sources/time, assumptions, actions, results, verification, artifact references and
limits/next steps. Keep working_notes sufficient for a fresh session. A report closes its task without changing the runtime
baseline. A maintained change closes only after its approved release. Distinguish selected/discoverable/read/used/effective
skill evidence; configuration metadata alone proves neither reading nor business benefit.

## Self-check
- Did the delivered result answer the request with actual evidence and usable references?
- Did permissions, project ownership and the current scope remain unchanged?
- Are calculation/test results, missing inputs and unknown effects reported honestly?
- Can another session continue from records without repeating questions or actions?
- Is a proposed iteration justified by observed benefit, not a compulsory weekly ritual?
