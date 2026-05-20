# Agent-Guard external attack protection boundary

Agent-Guard is the runtime protection layer for defending AGenNext agents from external attacks and unsafe inputs.

## Decision

Agent-Guard protects agents, tools, runtime, memory, context, and platform workflows from adversarial or unsafe external influence.

This includes prompt injection, malicious documents, unsafe links, malware, poisoned files, untrusted tool outputs, and hostile web or repository content.

## Scope

Agent-Guard owns:

- prompt-injection detection
- indirect prompt-injection protection
- malicious document screening
- unsafe URL/link screening
- malware/virus scanning integration points
- suspicious file detection
- untrusted content isolation
- external tool-output sanitization
- data exfiltration checks
- instruction hierarchy protection
- quarantine decisions
- guard verdicts and evidence

Agent-Guard does not own:

- final platform approval
- runtime execution orchestration
- deployment machinery
- identity issuance
- compliance mapping
- security hardening implementation

## Protected surfaces

Agent-Guard should inspect or gate:

- user inputs
- uploaded files
- retrieved web pages
- repository content
- tool outputs
- RAG chunks
- drive files
- webhook payloads
- A2A handoff context
- generated code before execution
- shell commands before execution
- deployment manifests before release

## Threat classes

```txt
prompt_injection
indirect_prompt_injection
malicious_file
malware_or_virus
unsafe_link
credential_exfiltration_attempt
data_exfiltration_attempt
poisoned_rag_context
malicious_tool_output
unsafe_code_execution
unsafe_shell_command
unsafe_deployment_manifest
```

## Runtime flow

```txt
external input/content arrives
  ↓
Agent-Input or Agent-Hooks normalizes envelope
  ↓
Agent-Guard inspects content and references
  ↓
if safe:
    runtime may continue
else:
    content is blocked/quarantined and traced
```

## Relationship

| Component | Responsibility |
|---|---|
| Agent-Guard | Runtime protection from external attacks and unsafe content |
| Agent-Input | Normalized external input envelopes |
| Agent-Drive | File/artifact references that Guard may scan |
| Agent-RAG | Retrieval chunks that Guard may sanitize |
| Agent-Hooks | External webhook payloads that Guard may inspect |
| Agent-Handoff | A2A context that Guard may validate before delivery |
| Agent-Runtime | Enforces Guard verdicts before execution |
| Agent-Traces | Records Guard verdicts and quarantine decisions |
| Agent-Platform | Final authority for overrides or escalation |

## Rule

Agents must not directly trust external content.

External content must pass through Agent-Guard before it can influence agent reasoning, memory, context, tools, or execution.
