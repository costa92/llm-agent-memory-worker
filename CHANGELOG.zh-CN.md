# Changelog

`github.com/costa92/llm-agent-memory-worker` 的所有重要变更都将记录在本文件中。

<!-- Keep a Changelog format: https://keepachangelog.com/en/1.1.0/ -->
<!-- Semver: https://semver.org/ -->

## [Unreleased]

## [0.2.1] - 2026-06-02

### Fixed

- 将 `llm-agent-memory-postgres` 版本提升至 `v0.1.1`，该版本修复了
  `ResolveDedupe` 的首写者竞态（C1）。工作进程在晋升前会调用 `ResolveDedupe`；
  此次提升将该修复引入工作进程二进制文件。

## [0.2.0] - 2026-06-02

### Changed

- 晋升资格、`0.7` 的重要性阈值以及去重键的构造方式，现在均来自
  `llm-agent-memory-contract` `v0.2.0`
  （`PromotionEligible` / `PromoteImportanceThreshold` / `DedupeKey`），
  取代了原先工作进程本地的副本（M8 D3）。行为保持不变；工作进程仍保留自己的
  晋升 `Reason` 字符串和幂等键盐值。

## [0.1.0] - 2026-05-26

### Added

- 从 SDK 模块中拆分出的初始异步合并工作进程：
  - 以中继驱动的发件箱（outbox）消费来完成合并
  - 工作记忆 → 情景记忆的晋升决策
  - 晋升前的持久去重
  - 工作进程启动与运行时配置
- `cmd/memory-worker` 二进制文件。

### Dependencies

- `github.com/costa92/llm-agent-memory` 提供由 SDK 拥有的合并抽象
- `github.com/costa92/llm-agent-memory-postgres` 提供持久后端 + 中继
- `github.com/costa92/llm-agent-memory-contract` 提供后端中立的契约类型

### Notes

- 需要 `LLM_AGENT_MEMORY_WORKER_PG_URL`；中继租约 TTL、最大尝试次数、
  批大小和轮询间隔均可通过环境变量配置（见 README）。
