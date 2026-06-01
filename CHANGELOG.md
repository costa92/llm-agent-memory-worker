# Changelog

All notable changes to `github.com/costa92/llm-agent-memory-worker` will be
documented in this file.

<!-- Keep a Changelog format: https://keepachangelog.com/en/1.1.0/ -->
<!-- Semver: https://semver.org/ -->

## [Unreleased]

## [0.1.0] - 2026-05-26

### Added

- Initial asynchronous consolidation worker split out from the SDK module:
  - relay-driven outbox consumption for consolidation
  - working → episodic promotion decisions
  - durable dedupe before promotion
  - worker process startup and runtime configuration
- `cmd/memory-worker` binary.

### Dependencies

- `github.com/costa92/llm-agent-memory` for SDK-owned consolidation abstractions
- `github.com/costa92/llm-agent-memory-postgres` for the durable backend + relay
- `github.com/costa92/llm-agent-memory-contract` for backend-neutral contract types

### Notes

- Requires `LLM_AGENT_MEMORY_WORKER_PG_URL`; relay lease TTL, max attempts,
  batch size, and poll interval are env-configurable (see README).
