# 🤝 Official Ecosystem Handoff: Repository Owners to PMaster Pipeline
# Primary Maintainer: @pinkycollie
# Recipient: PMaster Pipeline Orchestration Engine
# Created: 2026-08-09
# Status: READY FOR PMASTER PIPELINE INGESTION

---

## Executive Summary & Handoff Scope

This handoff document provides a formal, authoritative bridge between repository owners (@pinkycollie and the 360Magicians ecosystem team) and the **PMaster Pipeline Execution Engine**.

With the discovery, collection, classification, and validation audit complete, this handoff details the exact repository disposition matrix, environment secrets transfer specifications, canonical target pointers, and the step-by-step execution protocol for PMaster's upcoming consolidation and rebuild tasks.

---

## 1. Repository Disposition & Handoff Matrix

Every repository in the `@pinkycollie` / `Pmaster-dev` account is assigned an explicit disposition rule:

| Repository Name | Canonical Role | Action for PMaster Pipeline | Sync Target |
|---|---|---|---|
| **`municipal-dao-v`** | **CANONICAL PRODUCTION BACKEND** | **MAINTAIN & MERGE** — Primary target for GCP/GKE container microservices (`deafauth-api`, `pinksync-middleware`, `360magicians-vertex-ai`, `mbtq-platform`, `mbtquniverse-dao`). | Production GKE / Obsidian |
| **`mbtq-dev`** | **CANONICAL FRONTEND & VALIDATOR** | **MAINTAIN & MERGE** — Primary target for the **Sign Visual System** React UI engine and **Fibonrose Task Validator**. | Production Vercel / Obsidian |
| **`NegraRosa`** | **CANONICAL SECURITY FRAMEWORK** | **MAINTAIN & MERGE** — Provides NFT-based identity ("I AM WHO I AM" token) and zero-custody verification. | Security Pipeline / Proton Drive |
| **`FibonRoseTrust`** | **CANONICAL TRUST & MATCHING** | **MAINTAIN & MERGE** — AI universal professional verification for deaf community service providers. | Trust Engine / Proton Drive |
| **`pinkflow`** | **CANONICAL SANDBOX** | **MAINTAIN** — Firecracker MicroVM execution environment for verifying partner code. | Cloud Run / Proton Drive |
| **`deafauth`** | Reference Next.js App | **SYNC & ARCHIVE** — Export unique prompts and UI hooks to Obsidian/Drive, then set to Read-Only/Archived. | Obsidian / Proton Drive |
| **`pinksync-app`** | Reference App & Extension | **SYNC & ARCHIVE** — Export Chrome Extension (`browser-extension/`) and UI widgets to Obsidian/Drive, then Archive. | Obsidian / Proton Drive |
| **`fibonrose`** | Reference Staking App | **SYNC & ARCHIVE** — Export verification UI templates to Obsidian/Drive, then Archive. | Obsidian / Proton Drive |
| **`deaf-first-platform`** | OpenAPI Specifications Monorepo | **SYNC & ARCHIVE** — Sync OpenAPI v3.1 schemas and `Mbtq-sovereign.yml` to Obsidian/Drive, then Archive. | Obsidian / Proton Drive |
| **`360-magicians` Account Repos** | Legacy Messy Context Repos | **SYNC & ARCHIVE** — Sync historical context files to Obsidian/Proton Drive, then archive the account repositories. | Obsidian / Proton Drive |

---

## 2. Environment Secrets & Credentials Handoff Spec

The PMaster pipeline must securely inject environment variables into the canonical runtime using GCP Secret Manager rather than plaintext `.env` files:

### **Secrets Injection Mapping**
```yaml
# PMaster Secrets Injection Map
secrets:
  GCP_PROJECT_ID: "mbtq.dev"
  FIRESTORE_DATABASE: "deafauth-profiles"
  REDIS_URL: "redis://deafauth-redis:6379"
  VERTEX_AI_PROJECT: "mbtq.dev"
  VERTEX_AI_LOCATION: "us-central1"
  GOOGLE_AI_STUDIO_API_KEY: "secret:mbtq-google-ai-studio-key"
  DEAFAUTH_CLIENT_ID: "secret:deafauth-client-id"
  STAKING_CONTRACT_ADDRESS: "secret:polygon-mbtq-staking-address"
  DAO_CONTRACT_ADDRESS: "secret:polygon-mbtq-dao-address"
  NEGRAROSA_NFT_CONTRACT: "secret:negrarosa-nft-address"
```

---

## 3. Step-by-Step Execution Protocol for PMaster Pipeline

Upon receiving user approval, PMaster should execute the consolidation in four strict, sequential phases:

### **Step 1: Backup & Sync Phase**
1. Sync all markdown documentation, OpenAPI specifications, and Chrome Extension files to @pinkycollie's **Obsidian Vault** and **Proton Drive**.
2. Generate an immutable git tag `audit-handoff-v1.0` on all source repositories.

### **Step 2: Canonical Consolidation Phase**
1. Merge `services/` from `municipal-dao-v`, `NegraRosa` security hooks, and `FibonRoseTrust` AI taxonomy modules into a unified monorepo structure inside `mbtq-dev`.
2. Connect `deafauth-api` token issuance to `lib/deafauth-sdk.ts` and the **Sign Visual System** React state engine.

### **Step 3: Verification & Test Phase**
1. Run `FibonroseValidator.createTask()` on all consolidation PRs to generate Fibonacci checkpoints.
2. Run `script/validate-data` and Python YAML schema checkers to guarantee zero configuration regressions.

### **Step 4: Archival Phase**
1. Update repository settings for `deafauth`, `pinksync-app`, `fibonrose`, `deaf-first-platform`, and legacy `360-magicians` account repos to **Archived (Read-Only)**.
2. Set `mbtq-dev` and `municipal-dao-v` as the primary active repositories.

---

## 4. Handoff Sign-off

* **Auditor / Lead Engineer:** Jules
* **Target Account Owner:** @pinkycollie
* **Status:** AUDIT COMPLETE & HANDOFF READY FOR PMASTER PIPELINE.
