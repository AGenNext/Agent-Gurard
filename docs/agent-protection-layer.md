# Agent Protection Layer

## Purpose

Agent-Guard is the active protection layer for AGenNext agents.

It works like a firewall, antivirus, and policy enforcement layer for agentic systems.

## Responsibility

Agent-Guard protects agents, users, tools, data, secrets, and runtime environments from unsafe or unauthorized behavior.

It owns:

- prompt injection detection
- data exfiltration detection
- tool-call policy checks
- secret access protection
- unsafe action blocking
- malware-like behavior detection for agents
- suspicious loop detection
- anomalous tool usage detection
- policy firewall rules
- quarantine triggers
- runtime block decisions
- safe/unsafe content routing
- protection event logging

## Relationship to Agent Runtime

```text
Agent request/action/tool call
  → Agent-Guard inspection
  → allow / warn / block / quarantine
  → Agent-Runtime enforcement
  → Agent-Traces evidence
```

## Protection Decisions

```text
allow
warn
redact
block
quarantine
kill_switch
```

## Guarded Surfaces

Agent-Guard should inspect:

- prompts
- messages
- tool inputs
- tool outputs
- file reads/writes
- secret access requests
- API calls
- A2A handoffs
- generated artifacts
- deployment actions
- external web access

## Detection Categories

- prompt injection
- jailbreak attempt
- secret leakage
- data exfiltration
- unsafe tool use
- unauthorized access
- policy violation
- suspicious repetition
- unexpected privilege escalation
- malicious artifact generation
- supply-chain risk

## Final Rule

```text
Agent-Guard decides whether an action is safe.
Agent-Runtime enforces the decision.
Agent-Traces records the evidence.
```
