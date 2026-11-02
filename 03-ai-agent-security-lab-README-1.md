# 3. AI Agent Security Lab

A hands-on security assessment of a tool-using AI agent — demonstrating how indirect prompt injection can manipulate an agent into attempting unauthorized actions, and how hard authorization boundaries can prevent those actions even when the model is successfully manipulated.

The project follows:

**Attack → Evidence → Finding → Mitigation → Retest**

> **Safety note:** This project is performed in an isolated lab using fictional data, fake credentials, and systems that I own or explicitly control. Never test AI agents, tools, files, APIs, or accounts without authorization.

## Business Scenario

A fictional internal IT-support agent for **Northwind Retail** can:

- Read internal support documents
- Create service tickets
- Query a fictional asset inventory

The agent is intentionally built with an insecure design first. A malicious instruction is placed inside a document the agent is expected to read.

The goal is to demonstrate that **model instructions alone are not a security boundary**.

## Architecture — Insecure Design

The initial agent trusts retrieved document content and has excessive access to its available tools.

A controlled malicious document attempts to make the agent:

- Ignore its original instructions
- Access restricted information
- Misuse an available tool
- Perform an action the user did not explicitly authorize

The vulnerable version is demonstrated first so the attack and its impact can be documented.

## Attack

### Indirect Prompt Injection

A malicious instruction is embedded inside a document consumed by the agent.

**Malicious Document → Agent Retrieval → Context → Prompt Injection → Tool Call → Unauthorized Action**

Evidence collected includes:

- Injection payload
- Agent response
- Tool call attempted
- Resource accessed
- Authorization result
- Successful or blocked action

## Security Risks Tested

| Risk | What Is Tested |
|---|---|
| Indirect Prompt Injection | Can untrusted document content manipulate the agent? |
| Goal Hijacking | Can the agent be redirected from the user's intended task? |
| Tool Misuse | Can the model invoke a tool for an unauthorized purpose? |
| Privilege Abuse | Can the agent access resources beyond its intended permissions? |
| Agent Authorization | Are tool/resource permissions enforced outside the model? |
| Sensitive Information Disclosure | Can restricted information be retrieved or exposed? |
| System Prompt Leakage | Can protected instructions be revealed? |

## Hardened Controls

1. **Dedicated Agent Identity** — separate identity for attribution and access control.
2. **Tool Allow-Listing** — only approved tools can be invoked.
3. **Resource-Level Authorization** — permissions are enforced by the application/tool layer.
4. **Least Privilege** — the agent receives only required permissions.
5. **Short-Lived Credentials** — scoped credentials instead of unnecessary standing access.
6. **Human Approval** — high-impact actions require explicit approval.
7. **Untrusted Content Labels** — retrieved documents and tool outputs are treated as untrusted data.
8. **Tool-Call Logging** — agent identity, tool, parameters, authorization result, and outcome are recorded.
9. **Emergency Revocation** — agent access can be disabled immediately.

## Retest

The exact same injection is executed against the hardened agent.

Expected result:

**Model Manipulated → Authorization Boundary Holds → Dangerous Tool Call Blocked**

This demonstrates an important security principle:

> **An AI model can be fooled without the attacker gaining the underlying authorization.**

The retest records the blocked action and authorization decision as evidence.

## Findings Mapping

| Finding / Risk | Framework Mapping |
|---|---|
| Indirect Prompt Injection | **OWASP LLM01 — Prompt Injection** |
| Goal Hijacking / Tool Misuse | **OWASP GenAI Security — Agentic AI Threats** |
| System Prompt Leakage | **OWASP LLM07 — System Prompt Leakage** |
| Privilege / Identity Abuse | **OWASP GenAI Security — Agentic AI Threats** |
| Adversary Behavior | **MITRE ATLAS** |
| Least Privilege / Authorization | **CISA AI Security Guidance** |

## Assessment Methodology

1. Define the agent's intended purpose and security boundary.
2. Identify available tools and accessible resources.
3. Build the intentionally vulnerable agent.
4. Introduce a controlled indirect prompt injection.
5. Observe the response and tool calls.
6. Capture evidence and assess impact.
7. Identify the root cause.
8. Implement authorization and least-privilege controls.
9. Repeat the exact same attack.
10. Compare before/after results.
11. Document residual risk.

## Portfolio Checklist

- [ ] Vulnerable agent implementation
- [ ] Demonstrated exploit with evidence
- [ ] Hardened agent implementation
- [ ] Before/after architecture diagrams
- [ ] Permission and authorization policy
- [ ] Attack test cases
- [ ] Tool-call logs
- [ ] OWASP / MITRE mapping
- [ ] Mitigation implementation
- [ ] Retest evidence
- [ ] Technical report
- [ ] Short demo

## Tools & References

| Tool / Standard | Purpose |
|---|---|
| **Ollama** | Run a local LLM in an isolated environment |
| **Python** | Build the agent and security controls |
| **LangChain / LlamaIndex** | Agent and retrieval components |
| **OWASP GenAI Security Project** | Agentic AI security risks |
| **OWASP Top 10 for LLM Applications** | LLM vulnerability classification |
| **MITRE ATLAS** | AI adversary tactics and techniques |
| **CISA AI Guidance** | AI security and least-privilege principles |

## Key Security Principle

**Do not rely on the LLM to enforce authorization.**

Prompt instructions can be manipulated. Hard authorization controls must exist outside the model so that even a successfully manipulated agent cannot perform actions beyond its permitted scope.
