# 1. AI Red Teaming Lab

A repeatable hands-on lab for assessing an LLM application through controlled adversarial testing. The project demonstrates real attack evidence, root-cause analysis, mitigation, and retesting.

**Attack → Evidence → Finding → Mitigation → Retest**

> **Safety note:** This project runs in an isolated lab against systems that I own or explicitly control. All secrets and data are fictional. Never test these techniques without authorization.

## Business Scenario

A fictional customer-support chatbot for **Northwind Retail** runs on a local LLM through Ollama.

The chatbot has a defined purpose, system instructions, prohibited behavior, and a planted fake secret used only as a controlled disclosure target.

## Architecture

**User → Chat Application → Security Controls → LLM → Response**

The assessment focuses on the boundaries between untrusted input, application instructions, model context, and generated output.

## Attack Catalogue

### Direct Prompt Injection
Test whether malicious user instructions can override intended behavior.

### Jailbreaking
Test controlled role-play, persona, and multi-step techniques for bypassing safety boundaries.

### System Prompt Extraction
Attempt to reveal protected system instructions or hidden configuration.

### Sensitive Information Disclosure
Attempt to make the model reveal the planted fake secret or restricted test data.

### Encoding / Obfuscation Evasion
Test Base64, ROT13, character-level and similar transformations against security controls.

### Unsafe Output
Test whether generated content is safely handled before reaching downstream components.

For every test, document **what happened, why it happened, and what evidence proves it**.

## Methodology

**Garak** — run relevant LLM security probes and review hit logs.

**PyRIT** — organize adversarial prompt testing with targets, orchestrators, converters, and scorers.

**Promptfoo** — perform fast repeatable security evaluations and regression tests.

**Manual Testing** — perform targeted prompt injection, extraction, disclosure, and evasion tests.

**CI Testing** — run selected security tests through GitHub Actions after changes to the model, prompts, application, or guardrails.

## Findings Mapping

| Attack / Finding | OWASP LLM Category |
|---|---|
| Prompt Injection | **LLM01 — Prompt Injection** |
| Sensitive Data Disclosure | **LLM02 — Sensitive Information Disclosure** |
| System Prompt Extraction | **LLM07 — System Prompt Leakage** |
| Unsafe Model Output | **LLM05 — Improper Output Handling** |

Relevant behavior can also be mapped to **MITRE ATLAS**.

## Mitigation → Retest

For each successful attack:

1. Preserve the original evidence.
2. Identify the root cause.
3. Implement a security control.
4. Repeat the exact same attack.
5. Compare before/after behavior.
6. Document residual risk.

Possible controls include prompt hardening, input/output validation, guardrails, sensitive-data removal, rate limiting, and stronger authorization boundaries.

**Retest evidence is a key deliverable — not simply the fact that a fix was implemented.**

## Portfolio Checklist

- [ ] Local LLM application
- [ ] Controlled system prompt with fictional test secret
- [ ] Attack catalogue and manual test cases
- [ ] Garak results / hit logs
- [ ] PyRIT results
- [ ] Promptfoo results
- [ ] Security findings with evidence
- [ ] OWASP LLM mapping
- [ ] MITRE ATLAS mapping where applicable
- [ ] Mitigation implementation
- [ ] Before/after retest evidence
- [ ] GitHub Actions workflow
- [ ] Technical assessment report
- [ ] Short demonstration

## Tools & References

| Tool / Standard | Purpose |
|---|---|
| **Ollama** | Run a local LLM in an isolated environment |
| **Garak** | Automated LLM vulnerability scanning and probing |
| **PyRIT** | Adversarial prompt orchestration |
| **Promptfoo** | LLM security testing and evaluation |
| **GitHub Actions** | Automated repeatable security testing |
| **OWASP Top 10 for LLM Applications** | LLM vulnerability classification |
| **MITRE ATLAS** | AI adversary tactics and techniques |
