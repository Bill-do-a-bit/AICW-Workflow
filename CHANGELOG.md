# Changelog

All notable changes to AICW (AI Critic Collaboration Workflow) will be documented in this file.

## [4.3.1] - 2026-01-09

### Added

- P0判定尺：明确定义只有3种情况才能判为P0（无法开始/无法验收/红线风险）
- Stop Rule：硬性停机规则，防止无限循环
- 遗留风险承诺书：Executor拒绝修改时必须透明化风险
- P1-H标注：高概率失败的P1必须提供最小缓解动作

### Changed

- Round字段改为显式传递，Critic禁止靠上下文猜轮次
- C2模式增加逻辑锁，强制收敛

## [4.0.0] - 2026-01-01

### Added

- 引入两轮审查机制（C1全量扫描 + C2强制收敛）
- E1决策表：Executor必须逐条回应审查意见

### Changed

- 从单轮审查改为固定两轮
- Executor获得"拒绝修改权"

## [3.0.0] - 2025-12-15

### Added

- 遗留风险承诺书模板
- 方案卡标准格式

### Changed

- 优先级从5级简化为3级（P0/P1/P2）
