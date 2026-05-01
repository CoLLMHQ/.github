<div align="center">

# CoLLM

### The AI Agent Platform

[![Discussions](https://img.shields.io/badge/discussions-open-7c3aed?style=flat-square)](https://github.com/orgs/CoLLMHQ/discussions)
[![GitHub Org](https://img.shields.io/badge/org-CoLLMHQ-181717?style=flat-square&logo=github)](https://github.com/CoLLMHQ)
[![License: ISC](https://img.shields.io/badge/license-ISC-blue?style=flat-square)](https://opensource.org/licenses/ISC)

**Build, deploy, and manage AI agents at scale.**

Infrastructure for agent identity, memory, control, and cost management — so you can focus on what your agents *do*, not how they run.

</div>

---

## Open Source Projects

| Project | Description | Status |
|---------|-------------|--------|
| [**collm-registry-service**](https://github.com/CoLLMHQ/collm-registry-service) | Identity, auth, and control plane for AI agents — registration, telemetry, C2 commands, and FinOps | ![Release](https://img.shields.io/github/v/tag/CoLLMHQ/collm-registry-service?label=&color=0ea5e9&style=flat-square) |
| [**collm-index**](https://github.com/CoLLMHQ/collm-index) | Context database for AI agents — persistent, organized memory with tiered loading and filesystem-based retrieval | ![Release](https://img.shields.io/github/v/tag/CoLLMHQ/collm-index?label=&color=0ea5e9&style=flat-square) |
| [**collm-code**](https://github.com/CoLLMHQ/collm-code) | Multi-provider coding agent CLI — OpenAI, Gemini, DeepSeek, Ollama, and 200+ models | ![Release](https://img.shields.io/github/v/tag/CoLLMHQ/collm-code?label=&color=0ea5e9&style=flat-square) |
| [**collm-loop**](https://github.com/CoLLMHQ/collm-loop) | Structured AI-assisted development for Claude Code — Plan-Apply-Unify loop with session persistence and quality gates | ![Release](https://img.shields.io/github/v/tag/CoLLMHQ/collm-loop?label=&color=0ea5e9&style=flat-square) |
| [**collm-devops**](https://github.com/CoLLMHQ/collm-devops) | Code generation and deployment toolkit for the CoLLM platform | ![Release](https://img.shields.io/github/v/tag/CoLLMHQ/collm-devops?label=&color=0ea5e9&style=flat-square) |

---

## What We Build

### Core Infrastructure

- **Agent Identity** — Secure registration, authentication, and credential management with `collm_*` IDs, `csk_live_*` secret keys, and `ct_*` access tokens
- **Agent Memory** — Persistent context with intelligent retrieval, tiered loading, and filesystem-based access patterns
- **Agent Control** — Remote command dispatch (config updates, credential rotation, upgrades, session termination) with priority queues and acknowledgment flow
- **Agent Observability** — Telemetry ingestion, LLM usage tracking, latency monitoring, and cost analytics across providers
- **Agent Governance** — Multi-tenant organizations, team hierarchies, budget controls, and full audit trails

### Supported Providers

Works with the LLM providers you already use:

| Provider | Type |
|----------|------|
| Anthropic | API |
| OpenAI | API |
| AWS Bedrock | Cloud |
| Google Vertex | Cloud |
| Cerebras | API |
| Groq | API |
| Ollama | Local |

---

## Architecture

```
  ┌─────────────────────────────────────────────────────┐
  │                   Your AI Agents                    │
  └──────────────────────┬──────────────────────────────┘
                         │
          ┌──────────────▼──────────────┐
          │      CoLLM Control Plane    │
          │                             │
          │  ┌─────────┐  ┌──────────┐  │
          │  │  Auth   │  │  Memory  │  │
          │  │ Register│  │  Index   │  │
          │  │ Tokens  │  │ Retrieve │  │
          │  └─────────┘  └──────────┘  │
          │                             │
          │  ┌──────────┐  ┌──────────┐ │
          │  │   C2     │  │ FinOps   │ │
          │  │ Commands │  │ Budgets  │ │
          │  │ Heartbeat│  │ Telemetry│ │
          │  └──────────┘  └──────────┘ │
          └──────────────┬──────────────┘
                         │
     ┌───────────┬───────┼──────────────┬────────┐
     │           │       │              │        │
┌────▼────┐ ┌───▼───┐ ┌▼─────────┐ ┌────▼───┐ ┌──▼─────┐
│ MongoDB │ │ Redis │ │Click-    │ │Qdrant  │ │Kafka   │
│ (state) │ │(cache)│ │House     │ │(vector)│ │(events)│
└─────────┘ └───────┘ │(analytics) └────────┘ └────────┘
                      └──────────┘
```

---

## Quick Start

Get started with the registry service in under 5 minutes:

```bash
git clone https://github.com/CoLLMHQ/collm-registry-service.git
cd collm-registry-service
npm install
cp .env.example .env
docker compose up -d
node app.local.js
```

Then register your first agent:

```bash
curl -X POST http://localhost:9001/v1/collmreg/agents/registration/register \
  -H "Content-Type: application/json" \
  -d '{"name": "my-first-agent", "description": "Test agent"}'
```

Full documentation available in each project's README.

---

## Get Involved

- **[Discussions](https://github.com/orgs/CoLLMHQ/discussions)** — Ask questions, share ideas, and connect with other developers
- **[Issues](https://github.com/CoLLMHQ)** — Report bugs and request features across all projects
- **[Pull Requests](https://github.com/CoLLMHQ)** — Contributions welcome — see individual repos for guidelines

---

## Why CoLLM?

If you're building AI agents, you need infrastructure that handles the hard parts:

- **Agents need identity** — not just API keys, but proper registration, authentication, and lifecycle management
- **Agents need memory** — persistent context that survives restarts and scales with usage
- **Agents need control** — remote command dispatch, heartbeats, and upgrade paths without downtime
- **Agents need governance** — budgets, audit trails, multi-tenant isolation, and cost accountability

CoLLM provides all of this as open-source infrastructure you can run yourself.

---

<div align="center">

**Built for teams shipping AI agents to production.**

</div>
