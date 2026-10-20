# kernel · Assistant Kernel 的默认项目

[English](README.md) · 中文

[Assistant Kernel](https://github.com/vado290/assistant-kernel) 的每一套安装都从这个项目开始。它的 PM 和 Supervisor
负责：维护 Kernel 本身（Kernel 源码以代码交付的方式，通过 git worktree 修改），创建新项目，把请求路由到合适的项目，
以及维护所有项目都会读取的公共背景。

## 本仓库包含什么

| 路径 | 内容 |
|---|---|
| `project.yaml` | 能力（路由、项目管理、公共背景）和代码交付设置 |
| `knowledge/charter.md` | 项目章程：用途、范围和路由信息 |
| `agents/pm/`、`agents/supervisor/` | `role.md`、`config.yaml`，以及各 agent 自己的技能（`.agents/skills/`） |
| `.gitignore` | 每套安装各自保留、不进仓库的内容（见下） |

这些技能是 Kernel 技能模板的副本；每部署一个新版本的 Kernel，项目没改过的副本会自动刷新。

## 本仓库不包含什么，以及原因

这个项目是公开的，所以凡是属于某一套安装的个人内容，都被它的 git 忽略，由每套安装在使用中自己生成：

| 路径 | 内容 | 由谁生成 |
|---|---|---|
| `knowledge/shared/` | 公共背景：组织与用户、技术环境、工作约定 | 缺少时 Kernel 从模板复制；之后 Supervisor 用卡片提议修改，你批准后写入 |
| `knowledge/background.md` | 背景信息存档：任务中收集到的事实 | Kernel，在需求文档获批时 |
| `knowledge/user-profile.md` | 你和助理协作的习惯与偏好 | Kernel，来自已批准的文档和你对 Supervisor 说的话 |
| `knowledge/domain-brief.md`、`knowledge/archive/` | 行业调研及其旧版本 | Kernel |
| `runtime/` | Kernel 内部数据，包括凭据库 `runtime/credentials.json` | Kernel，第一次使用时 |
| `runs/` | 各任务的工作文件 | Kernel |
| `archive/` | 一套安装早期版本留下的文件 | — |

凭据怎么询问、怎么保存、怎么使用，以及谁能看到，见 Kernel 的 README（“敏感数据”一节）。

## 本项目的规则

- 这里的章程、角色和技能只写通用内容；关于某个用户、组织或机器的具体事实，写进公共背景或背景信息存档，
  这些内容只留在各自的安装里。
- 本项目的仓库和其他项目一样会被推送；改为公开之前，先检查里面的内容。
