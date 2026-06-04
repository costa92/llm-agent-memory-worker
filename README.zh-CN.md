[English](./README.md) | [简体中文](./README.zh-CN.md)

# llm-agent-memory-worker

面向持久记忆的异步合并工作进程。

## 范围

本模块负责：

- 以中继驱动的发件箱（outbox）消费来完成合并
- 工作记忆到情景记忆的晋升决策
- 晋升前的持久去重
- 工作进程启动与运行时配置

本模块依赖：

- `github.com/costa92/llm-agent-memory`
- `github.com/costa92/llm-agent-memory-postgres`

## 运行时配置

- `LLM_AGENT_MEMORY_WORKER_PG_URL` 必填
- `LLM_AGENT_MEMORY_WORKER_POLL_INTERVAL` 可选，默认 `1s`
- `LLM_AGENT_MEMORY_WORKER_RELAY_LEASE_TTL` 可选，默认 `180s`
- `LLM_AGENT_MEMORY_WORKER_RELAY_MAX_ATTEMPTS` 可选，默认 `5`
- `LLM_AGENT_MEMORY_WORKER_RELAY_BATCH_SIZE` 可选，默认 `100`

## 运行

```bash
LLM_AGENT_MEMORY_WORKER_PG_URL=postgres://... GOWORK=off go run ./cmd/memory-worker
```
