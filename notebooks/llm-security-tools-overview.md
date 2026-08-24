# Open-Source Tools für gesicherte LLM-Entwicklung

*Stand: Februar 2026*

## Übersicht

Diese Referenz kategorisiert Open-Source-Tools nach ihrer primären Sprache/Plattform und ihrem Einsatzbereich in der LLM-Security-Pipeline (Preprocessing → LLM → Postprocessing).

---

## 1. Python-basierte Tools

### Guardrails & Input/Output-Schutz

| Tool | Fokus | Pipeline-Phase | GitHub |
|------|-------|----------------|--------|
| **Guardrails AI** | Deklarative Input/Output-Guards, Structured Output, 100+ Validators im Hub | Pre + Post | guardrails-ai/guardrails |
| **NeMo Guardrails** (NVIDIA) | Programmierbare Rails mit Colang DSL, Dialog-Steuerung, Jailbreak-Schutz, Fact-Checking | Pre + Post | NVIDIA-NeMo/Guardrails |
| **LLM Guard** (Protect AI) | Sanitization, PII-Erkennung, Toxicity, Prompt Injection Detection | Pre + Post | protectai/llm-guard |
| **LlamaFirewall** (Meta) | PromptGuard 2 (Jailbreak-Detector), Agent Alignment Checks, CodeShield | Pre + Post | meta-llama/llama-firewall |
| **Llama Guard** (Meta) | Fine-tuned Safety-Classifier basierend auf Llama, 6+ Unsafe-Kategorien | Pre + Post | Teil von PurpleLlama |
| **OpenGuardrails** | Enterprise AI Security Gateway, PII-Masking, Route-to-Private-LLM | Pre + Post | openguardrails/openguardrails |
| **Rebuff** | Self-hardening Prompt Injection Detector, lernt aus Angriffen | Pre | protectai/rebuff |
| **LangKit** (WhyLabs) | Monitoring-Toolkit, extrahiert Signale aus Prompts & Responses | Pre + Post | whylabs/langkit |

### Red Teaming & Vulnerability Scanning

| Tool | Fokus | GitHub |
|------|-------|--------|
| **Garak** (NVIDIA) | LLM Vulnerability Scanner ("nmap für LLMs"), testet Hallucination, Data Leakage, Prompt Injection, Toxicity | leondz/garak |
| **PyRIT** (Microsoft) | Red Teaming Framework für Generative AI, multi-turn Angriffe | Azure/PyRIT |
| **EasyJailbreak** | Framework zum Generieren adversarialer Jailbreak-Prompts | EasyJailbreak/EasyJailbreak |
| **ART (Adversarial Robustness Toolbox)** (IBM) | Adversarial Attacks & Defenses, auch für LLMs einsetzbar | Trusted-AI/adversarial-robustness-toolbox |
| **ARTKIT** | Automatisiertes multi-turn Red Teaming mit Pipeline-Design | BCG-X-Official/artkit |
| **PurpleLlama** (Meta) | Toolsammlung für LLM-Security-Assessment inkl. CyberSecEval | meta-llama/PurpleLlama |

### Observability & Monitoring

| Tool | Fokus | GitHub |
|------|-------|--------|
| **Langfuse** | Open-Source LLM-Observability, Tracing, Scoring, Security-Dashboard | langfuse/langfuse |
| **OpenLIT** | OpenTelemetry-native LLM Monitoring | openlit/openlit |
| **Traceloop (OpenLLMetry)** | OpenTelemetry-Instrumentierung für LLM-Calls | traceloop/openllmetry |

### Frameworks mit eingebauter Security

| Tool | Fokus | GitHub |
|------|-------|--------|
| **LangChain** | Moderation Chains, Output Parsers, Safety-Tools integrierbar | langchain-ai/langchain |
| **LlamaIndex** | RAG-Framework mit Guardrail-Integration (NeMo, LLM Guard) | run-llama/llama_index |
| **Haystack** (deepset) | RAG/Agent-Framework mit Pipeline-basierter Security | deepset-ai/haystack |

### Model Scanning & Supply Chain

| Tool | Fokus | GitHub |
|------|-------|--------|
| **ModelScan** (Protect AI) | Scannt ML-Modelle auf Serialization Attacks (Pickle etc.) | protectai/modelscan |
| **Picklescan** | Erkennt bösartige Pickle-Dateien (genutzt von Hugging Face) | mmaitre314/picklescan |

---

## 2. Nicht-Python / Polyglott Tools

### LLM Gateways (Go, Rust, Lua)

| Tool | Sprache | Fokus | GitHub |
|------|---------|-------|--------|
| **Envoy AI Gateway** | Go + C++ (Envoy) | Kubernetes-native LLM Gateway, Rate Limiting, Auth, Provider-Failover | envoyproxy/ai-gateway |
| **TensorZero** | **Rust** | Ultra-low-latency Gateway (<1ms P99), Structured Inference, Observability via ClickHouse | tensorzero/tensorzero |
| **Traceloop Hub** | **Rust** | High-scale LLM Gateway mit OpenTelemetry | traceloop/hub |
| **Kong AI Gateway** | **Lua + Go** | Enterprise API Gateway mit AI-Plugins für Routing, Security, Monitoring | Kong/kong |
| **Agent Gateway** | **Rust** | Kubernetes Gateway API für AI (A2A, MCP), High-Performance Dataplane | agentgateway/agentgateway |
| **LiteLLM** | Python (aber als Proxy-Server deploybar) | 100+ LLM-Provider über einheitliches API, Retry, Fallback, Cost Tracking | BerriAI/litellm |
| **Portkey** | TypeScript/Node.js | AI Gateway mit Guardrails, Caching, Observability | portkey-ai/gateway |

### Security-Scanner & Red Teaming (nicht Python-only)

| Tool | Sprache | Fokus | GitHub |
|------|---------|-------|--------|
| **Agentic Radar** | TypeScript | CLI Security Scanner für Agentic Workflows | splx-ai/agentic-radar |
| **CodeShield** (Teil von LlamaFirewall) | Multi-lang Static Analysis | Online Static Analysis Engine für unsicheren generierten Code | Teil von LlamaFirewall |

### Infrastructure & Access Control

| Tool | Sprache | Fokus | GitHub |
|------|---------|-------|--------|
| **Pomerium** | **Go** | Identity-aware Access Proxy, sitzt vor LLM-Gateways | pomerium/pomerium |
| **Open Policy Agent (OPA)** | **Go** | Policy-as-Code Engine, nutzbar für LLM-Access-Policies | open-policy-agent/opa |

### Observability (nicht Python-only)

| Tool | Sprache | Fokus |
|------|---------|-------|
| **Helicone** | TypeScript | Drop-in Proxy für OpenAI-APIs, Monitoring, Cost Tracking |
| **Langfuse** | TypeScript (Server) + Python (SDK) | LLM Observability (polyglott einsetzbar) |

---

## 3. Vergleichsmatrix nach Pipeline-Phase

```
                    Python                          Non-Python
                    ───────                         ──────────
PREPROCESSING       ┌─────────────────────┐         ┌──────────────────────┐
(Input Guard)       │ LLM Guard           │         │ Kong AI Gateway      │
                    │ Guardrails AI       │         │ Envoy AI Gateway     │
                    │ NeMo Guardrails     │         │ Portkey              │
                    │ LlamaFirewall       │         │ OPA (Policy)         │
                    │ Rebuff              │         │ Pomerium (Access)    │
                    └─────────────────────┘         └──────────────────────┘

LLM LAYER           ┌─────────────────────┐         ┌──────────────────────┐
(Hardening)         │ LangChain Guards    │         │ TensorZero (Routing) │
                    │ NeMo Dialog Rails   │         │ LiteLLM Proxy        │
                    └─────────────────────┘         └──────────────────────┘

POSTPROCESSING       ┌─────────────────────┐         ┌──────────────────────┐
(Output Guard)      │ Guardrails AI       │         │ Kong AI Plugins      │
                    │ LLM Guard           │         │ Envoy AI Gateway     │
                    │ NeMo Guardrails     │         │ Portkey              │
                    │ LlamaFirewall       │         │                      │
                    └─────────────────────┘         └──────────────────────┘

MONITORING           ┌─────────────────────┐         ┌──────────────────────┐
                    │ Langfuse            │         │ Helicone             │
                    │ LangKit             │         │ Traceloop Hub (Rust) │
                    │ OpenLIT             │         │ Langfuse (TS Server) │
                    └─────────────────────┘         └──────────────────────┘

RED TEAMING          ┌─────────────────────┐         ┌──────────────────────┐
                    │ Garak               │         │ Agentic Radar (TS)   │
                    │ PyRIT               │         │                      │
                    │ PurpleLlama         │         │                      │
                    │ ARTKIT              │         │                      │
                    └─────────────────────┘         └──────────────────────┘
```

---

## 4. Empfehlungen für den Einstieg

### Minimales Setup (Python-only)
Ideal für Prototyping und Bootcamp-Projekte:
- **Guardrails AI** für Input/Output-Validierung
- **Garak** zum Testen deines Modells auf Schwachstellen
- **Langfuse** für Observability

### Production Setup (Polyglott)
Für reale Deployments:
- **Envoy AI Gateway** oder **Kong** als Infrastruktur-Layer (Rate Limiting, Auth, Routing)
- **NeMo Guardrails** oder **LlamaFirewall** für inhaltliche Sicherheit
- **OPA** für Policy Enforcement
- **Langfuse** + **OpenTelemetry** für End-to-End-Monitoring
- **Garak** + **PyRIT** für regelmäßiges Red Teaming

### Kernbeobachtung
Das Python-Ökosystem dominiert bei inhaltlicher Sicherheit (Prompt Injection, Toxicity, PII), während Non-Python-Tools (Go, Rust) bei Infrastruktur-Security (Gateway, Access Control, Low-Latency Routing) stark sind. In der Praxis kombiniert man beides.

---

## 5. Wichtige Links

- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [Guardrails AI Hub & Index](https://www.guardrailsai.com/)
- [NeMo Guardrails Docs](https://docs.nvidia.com/nemo/guardrails/)
- [Awesome LLM Security (curated list)](https://github.com/corca-ai/awesome-llm-security)
- [OSS LLM Security (curated list)](https://github.com/kaplanlior/oss-llm-security)
