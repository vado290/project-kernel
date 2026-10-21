# kernel · the default project of Super Assistant

English · [中文](README.zh-CN.md)

This is the project every installation of [Super Assistant](https://github.com/vado290/superAssistant) (the Assistant Kernel) starts
with. Its PM and Supervisor maintain the Kernel itself (its source is delivered as code through git worktrees),
create new projects, route requests to the right project, and look after the shared background that all projects
read.

## What is in this repository

| Path | Content |
|---|---|
| `project.yaml` | capabilities (routing, project management, shared background) and code delivery settings |
| `knowledge/charter.md` | the project's purpose, scope and routing information |
| `agents/pm/`, `agents/supervisor/` | `role.md`, `config.yaml`, and each agent's skills in `.agents/skills/` |
| `.gitignore` | what each installation keeps to itself (below) |

The skills are copies of the Kernel's templates; Kernel refreshes the copies a project never edited each time a
new Kernel version is deployed.

## What is not in this repository, and why

This project is public, so everything personal to an installation is ignored by its git and created by each
installation as it is used:

| Path | Content | Created by |
|---|---|---|
| `knowledge/shared/` | shared background: organization and user, technical environment, working conventions | Kernel copies the templates when missing; Supervisor proposes changes on a card, you approve them |
| `knowledge/background.md` | background archive: facts collected in tasks | Kernel, when a requirements document is approved |
| `knowledge/user-profile.md` | how you like to work with the assistant | Kernel, from approved documents and things you tell Supervisor |
| `knowledge/domain-brief.md`, `knowledge/archive/` | industry research and its older versions | Kernel |
| `runtime/` | Kernel internals, including the credential store `runtime/credentials.json` | Kernel, on first use |
| `runs/` | per-task working files | Kernel |
| `archive/` | files kept from earlier versions of an installation | — |

How credentials are asked for, stored and used, and who can see them, is described in the Kernel's README
("Sensitive data").

## Rules for this project

- Charter, roles and skills here contain only general content. Facts about a particular user, organization or
  machine go into the shared background or the background archive, which stay in the installation.
- The project's repository is pushed like any project's; check its content before making it public.
