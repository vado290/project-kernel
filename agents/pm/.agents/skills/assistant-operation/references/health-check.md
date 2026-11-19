# Operating health check

## Purpose
A review answers two questions: did the last improvements work, and is the product itself running well. This checklist
answers the second. It gathers facts; daily analysis goes into operation_report, while an evolution review's
conclusions and proposals go into improvement_proposal. Neither output authorizes runtime changes.

## When to use it
When the project has released or actually used products (scripts, jobs, services, reports, documents), check the items
that apply before the review looks for problems. For pure documents check timeliness, completeness, delivery location and
use, and mark the runtime items as not applicable; no registered jobs does not mean nothing is in operation. First read
the released change entry point Kernel gives you with the matching requirements/design, implementation and review
evidence, and confirm the agreements in effect together with the charter and the current product list. The latest
incremental task is not the whole project; without a Kernel release record verify manual or outside delivery evidence,
naming sources and unknowns — never invent an approval. Release, registration, enabling, successful runs and business
effect are checked separately; gather facts read-only — never re-run jobs, restart or retire services, or change business
files yourself.

## Chief of Staff scope
For a Chief of Staff project, apply this checklist to its own advice, documents and released routines. Observe other
projects only through authorized Project Access views. Catalog/summary coverage is not runtime health or proof of business
effect. Name missing scopes and evidence; request further authorized evidence or suggest a follow-up to the owning project.
Daily jobs and services remain that project's responsibility. Never read its folders, rerun jobs, restart services or change
its files. Disabling scheduled CoS reviews does not disable Kernel queue recovery or released runtime maintenance.

## Checklist (item by item; each problem becomes an F with its evidence)
1. **Jobs**: from the registered state, planned times, last run and statistics, tell enabled, paused, retired, not yet
   due, overdue or unknown apart; no run record is not by itself a failure. For repeated failures, missing results when a
   run was due, or unusual durations, read the latest logs under `runs/jobs/<id>/` and verify the actual output.
2. **Services**: check the registered state, state changes and alerts; `last_at` is the time of the last state change,
   not a health-check heartbeat. It does not refresh while the state stays the same, so a long stable service may show an
   old or empty value — that alone does not mean a check is overdue or something is wrong. A job's `last_at` is the time of
   its last result; the material's `observed_at` is only when the database was read — neither replaces live health
   evidence. Without live evidence say it is not verified and judge from the logs and receipts you have; read the end of
   `runs/services/<id>.err.log` when needed — never invent a check time.
3. **Is data and output on time**: by the success criteria in effect in the charter (for example "the daily report before
   9:00"), check the output's timeliness, completeness, location and evidence of receipt; choose the window and samples by
   the output's cycle, risk and recent changes, and state coverage and limits; with too few samples mark it to be
   observed — never claim everything is fine from it.
4. **Does anyone use it**: whether anyone reads or responds to the output (user messages in the channels, card actions);
   for output nobody has used for long, ask the user in the proposal whether it is still needed.
5. **User feedback**: complaints in the selected observation window, change requests and recurring topics (changes and rejections in the run
   records).
6. **Are the map and charter still right**: spot-check that key files listed in the map still exist and that the job list
   matches jobs.yaml; a mismatch is a problem. Tell the charter's long-term agreements, the map's current index and runtime
   receipts apart by assistant-task-continuity; for old projects without folder descriptions check the existing
   configuration against the actual files — non-standard names or missing descriptions are not failures in themselves,
   and the latest incremental list does not stand for the whole project. Check whether the output in focus reaches the
   agreed location with the required timeliness and usability, and whether references still point to valid inputs;
   periodic output can be sampled by folder — not every output needs its own map entry or release. Watch for persistent
   data saved in scratch areas, half-finished output taken as final, unusual growth or leftovers against agreed retention;
   record only the evidence and impact — never clean up, move, change the charter or set retention periods for the project
   yourself. Necessary fixes go to follow-up tasks.

## Output
This checklist produces no document of its own: problems found go into the review's "problems found (F)", with the sources
of the evidence (job id, log path, file path, date). Without data write "no data" — never guess. When handing a problem to
the Supervisor, state the object/version, trigger, impact, evidence, the actual effect known, the next step and the
recovery condition. Verify the version actually in use, any rollback or substitute and the applicable window — never hold
old tasks to new rules; report fix verification, runtime recovery and business effect separately. Service registration or
retirement is checked against the actual supervised configuration and processes — a database flag does not mean the
action is done; Kernel retries approved but unfinished service configuration, you only check state and receipts, and
persistent failures go to the maintainer — never work around unfinished handling by releasing again. Changes to the
product go through follow-up tasks; when a release result is uncertain, check the receipt and the actual targets first —
never blindly publish again or treat a cancelled task as an undone side effect.

## Common mistakes
- Taking "the job succeeded" as "all is well": a successful job does not mean correct output — sample the output.
- Using counts instead of risk: a single data corruption, permission breach or failed key delivery must be handled too;
  for ordinary occasional fluctuations state the impact and the basis of observation.

## Model selection and prompt reuse
For model-backed products, distinguish the configured profile, effective route and successful capability evidence.
Evaluate quality, failure and known invocation costs; context occupancy and session totals are not per-call bills.
A model-only change for an existing purpose goes through Supervisor consultation and its model-change card; adding a
capability or migrating embedding indexes remains product work. Keep scheduled review switches unchanged.
