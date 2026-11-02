# 2. Secure RAG Security Assessment

A hands-on security assessment of a Retrieval-Augmented Generation (RAG) application. The project focuses on the security boundaries created by document ingestion, embeddings, vector retrieval, access control, model context, and generated responses.

**Threat Model → Attack → Evidence → Finding → Mitigation → Retest**

> **Safety note:** This project runs in an isolated lab using fictional documents, identities, and data. Test only systems that I own or have explicit permission to assess.

## Business Scenario

A fictional **Northwind Retail** RAG assistant answers questions using internal company documents.

Two test roles are defined:

- **General Employee** — general company information
- **HR User** — HR-restricted information

The application contains document ingestion, chunking, embeddings, a vector database, similarity retrieval, authorization, and LLM generation.

The primary objective is to determine whether a user can cross an authorization boundary through retrieval manipulation or malicious document content.

## Architecture & Trust Boundaries

1. **User → Application** — authentication and role determination
2. **Document → Ingestion** — untrusted content enters
3. **Retriever → Vector Database** — role/tenant filtering
4. **Retrieved Context → LLM** — data enters model context
5. **LLM Output → User** — response validation

> **Similarity determines relevance; authorization determines access.**

The model must not be trusted to enforce access control.

## Attack Catalogue

### Indirect Prompt Injection
Place malicious instructions inside a document and test whether retrieved content can influence model behavior.

### Cross-Role / Cross-Tenant Leakage
Attempt to retrieve HR-restricted documents while authenticated as a general employee.

### Context Exfiltration
Attempt to make the model reveal restricted retrieved content or hidden context.

### Data Poisoning
Introduce controlled malicious or misleading content and observe its effect on later retrieval or responses.

### Retrieval Manipulation
Craft documents or queries that influence which chunks appear in Top K results.

### Embedding Weaknesses
Test whether crafted inputs surface unintended semantic neighbours.

### Top-K Exposure
Increase retrieval scope and determine whether additional sensitive documents become available to the model.

### Stale Embeddings
Test whether deleted or revoked documents remain retrievable through old vector records.

## Findings Mapping

| Attack / Finding | OWASP LLM Category |
|---|---|
| Indirect Prompt Injection | **LLM01 — Prompt Injection** |
| Cross-Role / Context Leakage | **LLM02 — Sensitive Information Disclosure** |
| Retrieval / Embedding Weakness | **LLM08 — Vector and Embedding Weaknesses** |
| Data Poisoning | **LLM08 — Vector and Embedding Weaknesses** |

Relevant behavior can also be mapped to **MITRE ATLAS**.

## Mitigations

**Document Trust Labels** — treat retrieved content as untrusted data.

**Query-Time Access Control** — apply role, tenant, department, and classification filters before similarity ranking.

**Vector Store Isolation** — use strong tenant or role separation where appropriate.

**Metadata Filtering** — enforce authorization using metadata such as user/tenant ID, role, classification, and document status.

**Output Validation** — inspect responses for unauthorized sensitive information.

**Structural Prompt Separation** — keep retrieved data separate from trusted instructions.

**Retention and Deletion** — remove embeddings when source documents are deleted and update indexes/caches.

## Mitigation → Retest

For every successful attack:

1. Preserve the vulnerable behavior and evidence.
2. Identify the broken trust boundary.
3. Implement the security control.
4. Repeat the exact same attack.
5. Compare retrieval and response behavior.
6. Document residual risk.

The goal is to demonstrate:

**Unauthorized Retrieval → Security Control → Authorized Retrieval Only**

## Portfolio Checklist

- [ ] RAG application code
- [ ] Document ingestion pipeline
- [ ] Embedding generation
- [ ] Vector database
- [ ] Two test roles with different permissions
- [ ] Data-flow / trust-boundary diagram
- [ ] Threat model
- [ ] Attack scripts and test queries
- [ ] Retrieval evidence
- [ ] Cross-role leakage tests
- [ ] Indirect prompt injection tests
- [ ] Data poisoning tests
- [ ] Embedding / retrieval weakness tests
- [ ] Security findings
- [ ] OWASP LLM mapping
- [ ] MITRE ATLAS mapping where applicable
- [ ] Mitigation implementation
- [ ] Before/after retest evidence
- [ ] Technical report
- [ ] Short demonstration

## Tools & References

| Tool / Standard | Purpose |
|---|---|
| **LangChain** | RAG and application components |
| **LlamaIndex** | Retrieval and indexing workflows |
| **Chroma** | Local vector database for controlled testing |
| **Ollama** | Run a local LLM in an isolated environment |
| **OWASP Top 10 for LLM Applications** | LLM vulnerability classification |
| **MITRE ATLAS** | AI adversary tactics and techniques |
