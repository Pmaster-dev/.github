# 🚀 PMaster Auto-Dev Orchestrator: Expert Routers, Autonomous Coders & Serverless/CI Spec
# Primary Maintainer: @pinkycollie
# Created: 2026-08-09
# Status: COMPLETED

This document defines the specification for **PMaster Auto-Dev**: an autonomous software engineering pipeline combining **Expert Request Routers**, **Autonomous Coding Agents (Developer Magicians)**, and **Serverless/CI Execution Infrastructure** across GitHub Actions, Google Cloud Run, and Firecracker MicroVMs.

---

## 1. PMaster Request Router & Expert Delegation Matrix

When a user request or issue is ingested by PMaster Auto-Dev, the **Expert Request Router** analyzes the task domain, accessibility constraints, security implications, and complexity score to delegate execution to specialized autonomous sub-agents:

```
                  ┌──────────────────────────────────────────────┐
                  │          PMaster Auto-Dev Router             │
                  │  (Analyzes Intent, Complexity & Constraints) │
                  └──────────────────────┬───────────────────────┘
                                         │
       ┌──────────────────┬──────────────┴───────┬──────────────────┐
       │                  │                      │                  │
┌──────▼──────┐    ┌──────▼──────┐        ┌──────▼──────┐    ┌──────▼──────┐
│  DeafAUTH   │    │ PinkSync    │        │  360Magi-   │    │ Fibonrose   │
│ Security    │    │ Accessibility│       │ cians AI    │    │  Trust &    │
│ Expert      │    │ Expert      │        │ Expert      │    │  Validator  │
└─────────────┘    └─────────────┘        └─────────────┘    └─────────────┘
```

### **Expert Sub-Agent Roles & Capabilities**

| Expert Agent Role | Subsystem Domain | Primary Capabilities & Responsibilities |
|---|---|---|
| **DeafAUTH Security Expert** | `services/deafauth-api`, `NegraRosa` | Validates authentication handshakes, NFT profile attestations, AES-256-GCM encryption, and token integrity. |
| **PinkSync Accessibility Expert** | `services/pinksync-middleware`, `accessibility-validator` | Ensures "Sign Leads, Text Follows" UX, haptic vibration patterns, visual alerts, and WCAG AAA compliance. |
| **360Magicians AI Expert** | `services/360magicians-vertex-ai`, `mbtq-platform` | Routes multi-domain requests (creative, design, content, accessibility) via Vertex AI Gemini-1.5-pro models. |
| **Fibonrose Trust Expert** | `mbtq-dev/fibonrose`, `FibonRoseTrust` | Assesses task complexity (0-9), generates Fibonacci checklists, and verifies commit SHAs/evidence. |
| **PinkFlow Sandbox Coder** | `pinkflow`, `services/pinkflow-sandbox` | Spawns isolated Firecracker MicroVMs on Cloud Run to evaluate partner integration scripts safely. |

---

## 2. Autonomous Coding Agent Protocol (Developer Magicians)

Autonomous Coders operate under strict execution rules (`agent-config/repo-runtime.yml`):

### **Execution Directives & Guardrails**
1. **Fail-Closed Runtime (`fail_closed: true`)**: Any unverified security exception, unhandled error, or invalid path traversal halts execution immediately.
2. **Prohibit Direct Execution on Main**: All autonomous coding changes must be staged on category-prefixed branches (e.g. `service/api:in/deafauth-auth-route`) and submitted via Pull Requests.
3. **Fibonacci Task Checkpoints**: Every multi-file change requires Fibonacci-scaled verification checkpoints (e.g., Complexity 3 = 3 confirmed evidence checkpoints) verified by `FibonroseValidator`.

---

## 3. Serverless & CI Infrastructure (`ciserverless`)

PMaster Auto-Dev leverages a three-tier serverless execution matrix:

### **Tier 1: GitHub Actions (CI & Workflow Automation)**
* **Role**: Primary CI execution engine running workflow linting (`script/validate-data`), YAML syntax validation, GHES branch syncing (`script/sync-ghes`), and Fibonrose comment parsing (`fibonrose-validator.yml`).
* **Environment**: GitHub-hosted Linux runners with Node.js 20 & Python 3.12 environments.

### **Tier 2: Google Cloud Run (Serverless Microservices)**
* **Role**: Runs containerized, stateless backend services (`deafauth-api`, `pinksync-middleware`, `vertex-ai-hub`) that auto-scale from 0 to N instances based on incoming HTTP/WebSocket traffic.
* **Environment**: Containerized Docker images stored in Google Container Registry (`gcr.io/mbtq-dev/*`).

### **Tier 3: Firecracker MicroVMs (Isolated Partner Execution)**
* **Role**: Executes un-trusted or partner-submitted integration code inside lightweight, ephemeral virtual machines with isolated cgroups, restricted memory (512MB), and a strict 30-second timeout.
* **Environment**: FastAPI runner invoking Firecracker microVMs on Google Cloud Run (`pinkflow-sandbox`).

---

## 4. PMaster Auto-Dev Complete Lifecycle Flow

```
1. Request Ingestion ──▶ 2. Expert Delegation ──▶ 3. Autonomous Coding
     (Issue / Dispatch)       (Security/AI/A11y)       (Branch & Fibonrose)
                                                                │
                                                                ▼
6. Deployment / Sync ◀── 5. Code Review & ◀── 4. Serverless Sandbox
   (GKE / Cloud Run)       Validate Data         (Firecracker / CI)
```
