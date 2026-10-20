# Assistant Kernel · 项目章程

> 项目 ID：`kernel`。由 Round 2 迁移根据原 project.yaml 和业务背景生成（2026-10-16），请在运营中补充完善。
> PM 和 Supervisor 每一轮都会读本章程；第 1、5、7 节同时用于 kernel 的项目路由。背景信息存档在 `knowledge/background.md`，由 Kernel 自动追加。

## 1 项目用途
维护执行内核及项目管理：创建、路由、公共模板和确认背景

## 2 业务目标与成功标准
（待补充）

## 3 使用者与使用场景
（待补充）

## 4 组织与行业背景

见公共背景（knowledge/shared/organization.md）：每个安装各自维护，不随本项目公开。

## 5 范围
- 负责：
- Kernel Python、数据库状态机、Worker、Session、Harness、API和Kernel MCP
- 不负责：
- 修改大管家的表达方式、入口判断或Project路由体验
- 执行普通业务Project的内部工作

## 6 约束
（待补充）

## 7 路由信息
- 别名：kernel、内核、助理核心
- 主题：消息与Run状态机、Session恢复与轮换、Worker、Lease和故障协调、Harness、API和MCP运行时
- 典型请求：
- 修复Session无法恢复或错误轮换
- 修改四表状态、Worker或Codex Harness
- 排查Kernel API、MCP和部署恢复问题
- 不负责的请求：
- 调整大管家的说话方式或项目匹配规则文本
- 具体交易、知识库或其他业务项目实施

## 8 变更记录
- 2026-10-16 由 Round 2 迁移生成
