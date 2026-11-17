---
name: assistant-kernel-maintenance
description: Extra rules when the kernel project changes itself — the running kernel and the code being changed stay strictly apart, changes keep the core principles and are covered by tests, and the user deploys.
metadata:
  template: {name: assistant-kernel-maintenance, version: "1.4.1", sha: "ca37c24cd412966f", content_sha: "06e2338654800f62d84923ac7b9955652e64d530b9bdbb79c0a8b9760df7c6fa"}
  version: "1.4.1"
  load: {roles: [pm, supervisor], stages: [design, build, review, evolution], purposes: [evaluate], capabilities: [kernel_maintenance]}
  changelog:
    - "1.4.1 2026-11-17 Keep shipped release inputs committed without including unrelated research artifacts"
    - "1.4.0 2026-11-17 Use approved forward-only deployment recovery; prioritize main workflows and bounded verification"
    - "1.3.0 2026-11-16 Separate platform counts from authorized project content; no legacy digest or background scans"
    - "1.2.0 2026-10-25 Model settings are production configuration in config/models.yaml: propose changes, never edit them (0.46.1)"
    - "1.1.0 2026-10-23 Written in English, the skills' source language; interface text lives in i18n/en.yaml (ROUND6, 0.46.0)"
    - "1.0.0 2026-10-16 Enabled (R4b): kernel maintains itself by code delivery; Kernel commits automatically, tests run on the commit, the user deploys after the merge"
    - "0.1.0 2026-10-16 Draft: enabled with R4b (kernel self-maintenance)"
---

# Maintaining the kernel itself

## Basic facts
- You are run by the current production kernel; you change the next version. Your changes do not affect the running
  system until the user deploys them.
- `AGENTS.md` at the repository root and `docs/ARCHITECTURE.md` describe the layout, the core principles and how to test;
  read them first. When you change the architecture or a principle, update both documents.
- Never change the production virtual environments, configuration or database, and never run the deploy script.
  That includes the model settings, `assistant-data/config/models.yaml` (which engine, provider, model and reasoning
  effort the agents use): when a change seems needed, propose it to the user with the reason; the user edits the file
  and checks the result with /models. Agent config.yaml files in the code (templates) do not set models.
- Kernel runs the test command on your commit during validation (the core tests create and drop their own temporary
  databases); during the build run the relevant tests in the workspace too — the command is in AGENTS.md. After the
  release main is fast-forwarded to your commit; it goes live only when the user runs `deploy.ps1`.
- Kernel's interface is English: text the user reads from Kernel itself comes from `src/assistant_kernel/i18n/en.yaml`;
  a new user-facing string gets a key there, never a literal in code. Prompt text for models is English; models reply in
  the user's language (the language note Kernel appends to every prompt).

## PM: design and build
1. The design document must say whether the change touches a core principle in `docs/ARCHITECTURE.md` (for example "each
   active task has exactly one cursor", "one card per project") and how it is kept intact.
2. A change to the state machine or to decision types adds or changes the matching scenario tests.
3. A change to prompt text or skills says which roles and occasions it affects, and updates versions and changelogs by
   assistant-capability-maintenance.
4. Database migrations only add files; a migration must run again on existing data without errors.

## Release preparation and recovery
- Review the complete change against existing project creation, routing, permissions, operations and skill loading.
  Prioritize normal user workflows and known failures. Keep rare-case remedies small; do not add a new state machine or
  compatibility framework for hypothetical failures. Ask the user when an actual requirement or ownership conflict remains.
- Working methods belong in skills; code enforces identity, permissions, state and delivery contracts. Update the affected
  skills and their versions together with implementation; a written rule alone does not prove runtime enforcement.
- For the approved 0.46.4 forward-only release, verify the packaged wheel and full tests in the existing AI environment.
  Do not create Docker containers or images for validation. Use temporary databases, never production data for tests.
- Before promotion, check the migration ledger without writes and ensure pg_dump/pg_restore are available. Stop Kernel
  writers, save a custom-format database backup and the current Supervisor configuration, and check the backup archive
  index. An index check is not a successful restore rehearsal; state that limitation honestly.
- Before production installation begins, a failed backup aborts deployment and restarts the original services. Once
  installation or migration starts, failure stops Kernel services and retains the candidate wheel and recovery artifacts.
  Repair forward on the compatible new code. Do not reinstall 0.46.3 against migration 0014 or restore a live database
  automatically. A restore requires a separate decision covering data written since the backup and other database users.
- Commit all tracked changes and new release inputs before promotion. Untracked research documents outside package,
  test and deployment inputs need not enter the release commit. Never hide an uncommitted source change to pass this gate.
- A passing source test is not a packaged release pass, deployment is not project creation, and mocked Discord tests are
  not live acceptance. Report each boundary explicitly; use normal approved bootstrap for CoS after deployment.

## Supervisor: evaluation and the release card
Assess the risk of the change (migrations, state machine, gateway, skills) and check that tests cover it; the release card
states the commit id, the test results, whether it includes a migration, and that the user must deploy after the merge.

## PM: polishing the shared templates in reviews
Besides this project's run records, Kernel maintenance receives bounded platform task/failure/retry counts. These are
not business-health verdicts. Project content is available only through approved Project Access tools; do not scan vaults,
background archives or raw project digests. Read the relevant authorized documents/history when available. A missing scope
means insufficient evidence, not a shared defect or permission to read another project's files.
Use authorized evidence to distinguish repeated template problems from project-specific changes. Propose concrete wording
only when the evidence supports the attribution; otherwise name the missing evidence and a way to obtain it.
State in the proposal which projects and data the evidence comes from. Once a template change is released, each project
decides in its own review whether to adopt it.
