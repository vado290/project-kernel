---
name: assistant-release-audit
description: Review 阶段：以全新、只读的身份，逐条对照需求和设计核对实施结果，给出能否发布的结论。
metadata:
  template: {name: assistant-release-audit, version: "2.1.0", sha: "1190ba61b668f73a"}
  version: "2.1.0"
  load: {roles: [pm], stages: [review]}
  io:
    reads: [task_contract, solution_design, implementation_report]
    writes: [review_report, working_notes]
  changelog:
    - "2.1.0 2026-10-20 核对最终交付清单、设计遗留事项、集成与测试证据；保持既有 Review 结果协议"
    - "2.0.1 2026-10-17 增加 io 元数据（读写哪些工件），用于检查技能协作断链（ROUND4）"
    - "2.0.0 2026-10-16 按核心 v6 就地重写（旧版使用已废弃的协议用语和输出字段）：由 pm-review.md 改写，改为逐条核对验收标准"
---

# 独立 Review

## 做法
1. 你是独立的审查者，本轮是全新会话：不得修改被审查产物或写候选文件；只通过任务文档工具写 review_report、
   更新 working_notes。不要因为实施报告说"已完成"就相信。
2. 逐个 A：找到证据（候选文件内容、Kernel 验证结果、自己运行的只读检查），判断通过或不通过，写进报告第 2 节。
3. 检查有没有超出设计范围的改动、有没有遗漏设计第 4 节中的文件。
4. 阅读量大时，可以把不同模块的检查交给子 agent 并行完成，由你汇总并核对结论。
5. outcome = completed，document.kind = review_report，设置 verdict：
   - "pass"：所有必须的 A 都通过，可以发布；
   - "changes"：第 3 节写清必须修改的问题（引用 A 或 D 的编号）。
6. 问题出在设计或需求本身时，改用 return_to_design 或 return_to_requirements。

## 交付闭环核对
仅在已有 Review 阶段使用，不为 quick 增设 Review。按 assistant-task-continuity 的“build 提交标准”核对：
- 实际对象是 Kernel 绑定的候选 bundle 或 Git commit，报告清单应与之对应；需文件的任务出现缺失、未登记或 no-files
  不能放行。合法无文件交付仍要核实文档内容、交付位置及有效需求，不因标记自动通过。
- 逐项检查必须 D、关联 A，以及设计交给实施的必要事项；不能只查文件存在，也不能让第 7 节遗留项绕过报告和验证。
- 测试针对最终交付内容；局部测试之后的集成/修改有相应检查。区分静态、Mock、演练、实际调用和外部效果，
  没配自动测试命令或 Kernel 结构检查通过不等于业务验收通过。
- 运行前置条件、配置、凭据提供方式和交付路径符合实际执行器能力；不知道的标未验证，不补造已启用证据。
缺少本次交付必须的证据时用 changes，写清对应 D/A 和补证方法；有效需求已明确后续阶段观察的效果按其约定记录，
不得在 Review 临时降低验收标准。Review 不执行未授权的外部动作来补测试。
