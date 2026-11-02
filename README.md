# ai-security-lab

Four hands-on projects for building a practical portfolio in AI security — demonstrating the ability to assess, attack, and secure modern AI applications through controlled, repeatable security testing. The focus is on producing evidence of real security work rather than simply listing courses, certifications, or AI security concepts.

Each project follows a practical security workflow:

Attack → Evidence → Finding → Mitigation → Retest

«Safety note: Every project is performed in an isolated lab environment against systems that I own or have explicit permission to test. All data, credentials, secrets, and organizations used in these projects are fictional and created specifically for security testing. Never use these tools or techniques against systems, models, or accounts without authorization.»

Projects

#| Project| Focus| Key Security Areas| Status
1| AI Red Teaming Lab| Attack and assess an LLM application using automated and manual techniques| Prompt Injection, Jailbreaking, Sensitive Information Disclosure, System Prompt Leakage| In Progress
2| Secure RAG Security Assessment| Threat-model and attack a retrieval-augmented generation application| Indirect Prompt Injection, Data Leakage, Data Poisoning, Vector & Embedding Weaknesses| Planned
3| AI Agent Security Lab| Attack and harden a tool-using AI agent| Goal Hijacking, Tool Misuse, Privilege Abuse, Agent Authorization| Planned
4| AI Supply Chain Security Lab| Assess the security of AI models, dependencies, and artifacts| Model Poisoning, Unsafe Deserialization, Dependency Confusion, Model Integrity| Planned

Each project contains its own documentation covering the security scenario, architecture, trust boundaries, threat model, attack methodology, findings, mitigations, and retest evidence.

Standards and Frameworks

Framework| Purpose
OWASP Top 10 for LLM Applications| Classifying vulnerabilities in LLM applications
OWASP GenAI Security Project| Security risks in generative and agentic AI
MITRE ATLAS| Adversary tactics and techniques targeting AI systems
NIST AI Risk Management Framework| AI security and risk-management guidance

Tools

Tool| Purpose
Ollama| Run open-weight LLMs locally in an isolated environment
Garak| Automated LLM vulnerability scanning and probing
PyRIT| Adversarial prompt orchestration and AI red teaming
Promptfoo| LLM security testing and evaluation
LangChain| Building and testing RAG/agent applications
LlamaIndex| RAG and retrieval pipeline development
Chroma| Local vector database for RAG security testing
Fickling| Static analysis of potentially malicious Python pickle files
ModelScan| Security scanning of machine-learning model artifacts

How Each Project Is Documented

Business scenario — The fictional organization and purpose of the AI system.

Architecture — Components, data flows, trust boundaries, and security controls.

Threat model — Assets, attack surfaces, trust boundaries, threats, and assumptions.

Attack methodology — The techniques, tools, test cases, and conditions used during assessment.

Findings — Vulnerability description, evidence, impact, severity, and affected component.

Framework mapping — Relevant OWASP LLM and MITRE ATLAS classifications.

Mitigation — Security control implemented to address the finding.

Retest — The same attack is repeated to verify whether the mitigation actually works.

Portfolio Deliverables

Each completed project aims to include:

- Source code
- Architecture diagram
- Threat model
- Attack scripts / test cases
- Tool outputs and evidence
- Security findings
- OWASP / MITRE mapping
- Mitigation implementation
- Retest results
- Screenshots or demonstration
- Technical report
- Concise project README

The goal is not to build as many projects as possible, but to build a small number of projects deeply enough to demonstrate practical AI security assessment skills.
