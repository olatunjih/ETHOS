# ETHOS

# ETHOS v6.0 — Distributed Cognitive Fabric

![Version](https://img.shields.io/badge/version-6.0.0-blue)
![Status](https://img.shields.io/badge/status-phase_0-orange)
![License](https://img.shields.io/badge/license-proprietary-red)
![Security](https://img.shields.io/badge/security-zero--trust-green)

**Ethical Adaptive Cognitive Hub (ETHOS)** is a greenfield implementation of a Distributed Cognitive Fabric. This repository contains the core system modules (ETH-SYS) responsible for kernel execution, memory sharding, distributed coordination, and ethical governance.

> **⚠️ Critical Notice:** This system implements hard dependency chains. Violating build order will cause manifest resolution failures or runtime panics. See [Critical Dependencies](#critical-dependency-chain) before initializing modules.

---

## 📖 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [Architecture](#architecture)
- [Module Registry](#module-registry)
- [Getting Started](#getting-started)
- [Development Phases](#development-phases)
- [Safety & Ethics](#safety--ethics)
- [License](#license)

---

## 🌐 Overview

ETHOS v6.0 transforms the v6 specification from document into working software. Building from scratch eliminates migration risk and allows the architecture to be implemented in strict dependency order. The system adds **7 new top-level modules**, splits the monolithic memory module into **5 specialized shards**, and implements **Cognitive Thermodynamics** as a cross-cutting entropy protocol.

**Project Metrics:**
- **Duration:** 38 Weeks
- **Phases:** 6 Build Stages
- **Modules:** 21 New/Modified System Modules
- **Upgrades:** 9 v6 Feature Sets

---

## ✨ Key Features

- **Distributed Cognitive Fabric:** Horizontally scalable architecture supporting Standalone, Active-Passive, Cluster, and Edge deployment modes.
- **Cognitive Thermodynamics:** An entropy protocol woven across four modules to manage system instability, model disagreement, and cost overruns.
- **Self-Improvement Governor:** A 9-stage pipeline for autonomous knowledge enrichment with mandatory ethics scanning and rollback capabilities.
- **Model Arbitration Engine:** Genuinely model-agnostic routing with local/remote privacy guards and cost-optimized Pareto frontier selection.
- **Reasoning Virtualization:** Isolated speculative cognition containers with read-only memory snapshots and explicit promotion gates.
- **Zero-Trust Security:** mTLS handshake, JWT RS256 attestation, and MIME isolation sandboxes.

---

## 🛠 Technology Stack

All technology decisions are grounded in v6 manifest constraints (resource budgets, security tiers).

| Layer | Technology | Rationale |
| :--- | :--- | :--- |
| **Runtime** | TypeScript (Node.js 20 LTS) | Type safety for manifests; native JSON |
| **Monorepo** | Turborepo + pnpm workspaces | Fast incremental builds; shared tsconfig |
| **API Gateway** | Fastify + Zod schemas | High throughput; Zero-Trust boundary enforcement |
| **Auth** | jose (JWK/RS256) + mTLS | Cross-node attestation tokens |
| **Memory (Graph)** | Apache AGE on PostgreSQL | Full ACID graph DB; SQL fallback |
| **Memory (Vector)** | pgvector on PostgreSQL | Collocated with graph store; ANN search |
| **Memory (Ledger)** | PostgreSQL + BLAKE3 hash | Immutable; cryptographic integrity |
| **Coordination** | Custom Raft (`ethos-raft`) over gRPC | ETHOS-specific log entries; gossip protocol |
| **Event Bus** | NATS JetStream | Persistent; at-least-once; cron scheduling |
| **LLM Inference** | Ollama (local) / SDK (remote) | ModelTier-aware quantization; swappable |
| **Sandbox** | Node.js vm2 + seccomp | Process-level sandbox for PROCESS tier |
| **Observability** | OpenTelemetry + Prometheus | Span-level token tracking; Grafana dashboards |
| **CI/CD** | GitHub Actions + Docker/K8s | Matrix builds; blue-green deploy |

---

## 🏗 Architecture

### Critical Dependency Chain
The following dependencies are load-bearing. **Violating build order will cause manifest resolution failures.**

| Upstream Module | Relationship | Downstream Module / Rationale |
| :--- | :--- | :--- |
| `ETH-SYS-001–014` | **Must Precede** | **Everything** — Kernel, sandbox, auth, and execution engine are the boot layer |
| `ETH-SYS-011A–E` | **Must Precede** | `ETH-SYS-018` — Distributed Coordination replicates memory shards across nodes |
| `ETH-SYS-018` | **Must Precede** | `ETH-SYS-015` — Cognitive Mesh's manifest explicitly lists 018 as a system dep |
| `ETH-SYS-015 + 016` | **Must Precede** | `ETH-SYS-017` — Governor uses model arbitration and mesh for claim triangulation |
| `ETH-SYS-009 + 017` | **Must Precede** | `ETH-SYS-019` — Temporal Orchestrator submits plans to the Execution Engine |
| `ETH-SYS-021 + 016 + 015 + 001` | **Jointly Enable** | **Cognitive Thermodynamics** — Entropy protocol woven across all four modules |

> **💡 Sequencing Insight:** `ETH-SYS-018` (Distributed Coordination) must be fully operational before `ETH-SYS-015` (Cognitive Mesh) is initialized. The Mesh's Topology Manager depends on the gossip protocol to learn about peer nodes.

### System Diagram (Logical)

```text
[ Client ] 
    │
    ▼
[ ETH-SYS-002 API Gateway ] ── [ ETH-SYS-003 Auth (mTLS/JWT) ]
    │
    ▼
[ ETH-SYS-010 Kernel ] ──► [ ETH-SYS-015 Cognitive Mesh ] ◄── [ ETH-SYS-018 Coordination (Raft) ]
    │                             │
    ▼                             ▼
[ ETH-SYS-009 Execution ]   [ ETH-SYS-016 Model Arbitration ]
    │                             │
    ▼                             ▼
[ ETH-SYS-011 Memory ] ◄──────────┘
    ├── 011A Episodic (JSONL)
    ├── 011B Semantic (AGE)
    ├── 011C Working (LRU)
    ├── 011D Vector (pgvector)
    └── 011E Ledger (BLAKE3)
    │
    ▼
[ ETH-SYS-017 Governor ] ◄── [ ETH-SYS-021 Cost Profiler ]
    │
    ▼
[ ETH-SYS-019 Orchestrator (NATS) ]
```

---

## 📦 Module Registry

This repository contains the **21 new or modified system modules**. 
*Note: The 38 `ETH-COG-*` cognitive modules and 8 `ETH-INT-*` integration modules are unchanged from v6 and are excluded from this registry (Preservation Guarantee).*

| Module ID | Name | Tier | Phase | Key Dependency |
| :--- | :--- | :--- | :--- | :--- |
| `ETH-SYS-001–014` | v5 Base System Modules | CORE | 0 | None |
| `ETH-SYS-011A` | Episodic Store | CORE | 1 | `ETH-SYS-009` |
| `ETH-SYS-011B` | Semantic Graph Store | CORE | 1 | `ETH-SYS-011A` |
| `ETH-SYS-011C` | Working Memory Cache | CORE | 1 | `ETH-SYS-011B` |
| `ETH-SYS-011D` | Long-Term Vector Index | CORE | 1 | `ETH-SYS-011B` |
| `ETH-SYS-011E` | Causal Event Ledger | CORE | 1 | `ETH-SYS-011A` |
| `ETH-SYS-018` | Distributed Coordination | CORE | 2 | `ETH-SYS-011A–E` |
| `ETH-SYS-015` | Cognitive Mesh | CORE | 3 | `ETH-SYS-018`, `010` |
| `ETH-SYS-016` | Model Arbitration Engine | CORE | 3 | `ETH-SYS-010`, `008` |
| `ETH-SYS-017` | Self-Improvement Governor | CORE | 4 | `ETH-SYS-011B`, `016` |
| `ETH-SYS-019` | Temporal Task Orchestrator | STANDARD | 4 | `ETH-SYS-009`, `017` |
| `ETH-SYS-020` | Reasoning Virtualization | OPTIONAL | 5 | `ETH-SYS-015`, `016` |
| `ETH-SYS-021` | Cognitive Cost Profiler | STANDARD | 5 | `ETH-SYS-015`, `016` |

---

## 🚀 Getting Started

### Prerequisites

- **Node.js:** v20 LTS
- **Package Manager:** pnpm (`npm install -g pnpm`)
- **Database:** PostgreSQL 15+ (with `apache-age` and `pgvector` extensions)
- **Container Runtime:** Docker & Docker Compose
- **LLM Backend:** Ollama (for local inference)

### Installation

1.  **Clone the Repository**
    ```bash
    git clone https://github.com/ethos-ai/ethos-v6.git
    cd ethos-v6
    ```

2.  **Install Dependencies**
    ```bash
    pnpm install
    ```

3.  **Initialize Monorepo**
    ```bash
    pnpm turbo run build --filter=ETH-SYS-001...
    ```

4.  **Bootstrap Database**
    ```bash
    docker compose up -d postgres
    pnpm db:migrate
    ```

5.  **Start Phase 0 Services**
    ```bash
    pnpm dev:phase0
    ```

### Configuration

Copy the example environment file and configure secrets:
```bash
cp .env.example .env
```

**Critical Settings:**
- `ETHOS_DEPLOYMENT_MODE`: `STANDALONE` | `CLUSTER` | `EDGE`
- `ETHOS_RAFT_ENABLED`: `false` (Phase 0-1) | `true` (Phase 2+)
- `ETHOS_ENTROPY_MODE`: `SHADOW` | `LIVE`

---

## 📅 Development Phases

The build plan is organized into **6 phases over 38 weeks**. No phase can be compressed past its critical dependencies.

| Phase | Name | Timeline | Status | Goal |
| :--- | :--- | :--- | :--- | :--- |
| **0** | **Foundation** | Weeks 1–6 | 🟡 Active | Stand up v5 base layer (Kernel, Auth, Gateway). |
| **1** | **Memory Substrate** | Weeks 7–12 | ⚪ Pending | Replace monolithic memory with 5 specialized shards. |
| **2** | **Distributed Coordination** | Weeks 10–16 | ⚪ Pending | Implement Raft consensus & memory replication. |
| **3** | **Mesh + Arbitration** | Weeks 14–22 | ⚪ Pending | Cognitive Mesh & Model Agnostic routing. |
| **4** | **Gov + Orchestration** | Weeks 21–28 | ⚪ Pending | Self-Improvement Governor & Temporal Tasks. |
| **5** | **Advanced Cognition** | Weeks 27–34 | ⚪ Pending | Reasoning Virtualization & Cost Profiling. |
| **6** | **Integration & Launch** | Weeks 33–38 | ⚪ Pending | Security Audit, Entropy Activation, Go-Live. |

> **Note:** Phases 2 and 3 overlap by 3 weeks to allow Distributed Coordination to be hardened while Cognitive Mesh development begins.

---

## 🛡 Safety & Ethics

ETHOS v6 prioritizes operational safety and ethical constraints.

### 1. Kill-Switch (`ETH-SYS-001`)
- **Requirement:** Full system halt within **500ms** under maximum cognitive load.
- **Testing:** Validated during Phase 6 soak tests.

### 2. Self-Improvement Governor (`ETH-SYS-017`)
- **9-Stage Pipeline:** Non-negotiable. No claims skip stages.
- **Shadow Mode:** Runs in `OBSERVE` mode for 2 full sprints before enabling memory commits.
- **Adversarial Defense:** Ethics scan is Stage 5. All adversarial payloads must be blocked before entering `ETH-SYS-011B`.

### 3. Cognitive Thermodynamics
- **Entropy Protocol:** Monitors 5 signal sources (model disagreement, plan instability, memory ambiguity, retrieval divergence, cost overrun).
- **Escalation Levels (E0–E4):**
    - **E1:** Upgrade model tier.
    - **E2:** Additional retrieval.
    - **E3:** Fan-out reasoning branches.
    - **E4:** Trigger Human-In-The-Loop (HITL).

### 4. Sandbox (`ETH-SYS-008`)
- **Isolation:** MIME isolation; restricted module access.
- **Verification:** Formal plan verifier included.

---

## 🧪 Testing & Quality

### Acceptance Gates
Each phase ends with a strict acceptance gate.
- **Phase 0:** All 14 base modules pass integration suite; CI green.
- **Phase 1:** Full memory substrate integration; 011 facade routes correctly.
- **Phase 2:** All 4 deployment modes pass test matrix; gossip capability matrix propagated.
- **Phase 3:** Full v6 call path: Kernel → Mesh → [Runtime ×2] → Consensus.
- **Phase 4:** Governor + Orchestrator integration; 5 scheduled tasks run over 72h.
- **Phase 5:** Entropy shadow mode stable; cost profiler accurate ± 10%.
- **Phase 6:** Security audit pass; 72-hour cluster soak test; Launch authorization.

### Running Tests
```bash
# Unit Tests
pnpm test

# Integration Tests (Requires Docker)
pnpm test:integration

# Phase Specific Tests
pnpm test:phase1
```

---

### Branching Strategy
- `main`: Production-ready code (Phase 6)
- `develop`: Integration branch
- `feature/phase-X`: Specific phase development
- `hotfix/security`: Critical security patches

### Commit Convention
We use conventional commits. 
```bash
feat(011B): implement confidence aging decay formula
fix(018): resolve raft leader election timeout
docs: update architecture diagram
```

---

## ⚠️ Risk Register

| Risk | Likelihood | Impact | Mitigation |
| :--- | :--- | :--- | :--- |
| **Graph store performance** | HIGH | HIGH | Benchmark Apache AGE at 500K nodes in Phase 1. Define `PRUNE_THRESHOLD`. |
| **Raft consensus latency** | MEDIUM | HIGH | Test two-node active-passive before cluster mode. Budget 5s partition timeout. |
| **Token cost explosion** | HIGH | MEDIUM | Gate multi-model voting behind cost budget. Cost Profiler enforces 20% ceiling. |
| **Adversarial content** | LOW | CRITICAL | Ethics scan is Stage 5 of 9 — non-bypassable. Rollback index tested in Phase 4. |

---

## 📄 License & Classification

**Classification:** Confidential / Proprietary  
**Copyright:** © 2026 ETHOS AI Research. All Rights Reserved.

*This software contains cryptographic modules (BLAKE3, RS256) and is subject to export control regulations. Unauthorized distribution is prohibited.*

---
