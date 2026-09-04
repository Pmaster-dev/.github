# ⚡ PMaster Powerful Pipeline Orchestrator Specification
# Primary Maintainer: @pinkycollie
# Created: 2026-08-09
# Status: COMPLETED

This document defines the specification and UI picker options for the **PMaster Powerful Pipeline Orchestrator** implemented in `.github/workflows/pmaster-orchestrator.yml`.

---

## 1. Interactive UI Stage Pickers (`workflow_dispatch`)

The orchestrator enables `@pinkycollie` and PMaster to execute individual stage pipelines or the full multi-stage rebuild sequence using interactive UI dropdown pickers in GitHub Actions:

### **Picker Parameters & Options**

| Picker Input Name | Type | Description | Available Choices / Options |
|---|---|---|---|
| **`stage`** | Choice Dropdown | Select specific orchestrator stage or run all | `all-stages`, `audit-validation`, `centralized-sync`, `sovereign-build`, `fibonrose-verify`, `security-scan`, `deployment-check` |
| **`environment`** | Choice Dropdown | Target deployment or backup environment | `production`, `staging`, `sandbox`, `obsidian-backup` |
| **`component`** | Choice Dropdown | Ecosystem component scope | `all-components`, `deafauth-api`, `negrarosa-security`, `fibonrose-trust`, `pinksync-middleware`, `360magicians-vertex-ai`, `mbtq-platform`, `mbtquniverse-dao`, `pinkflow-sandbox` |
| **`dry_run`** | Boolean Toggle | Simulation mode without applying live changes | `false` (default), `true` |

---

## 2. Stage Execution Details

```
┌─────────────────────────────────────────────────────────────┐
│               1. Stage: Audit & Schema Validation           │
│   (Validates Draft-07 JSON Schema, PyYAML & Data Scripts)   │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│               2. Stage: Centralized Ecosystem Sync          │
│     (Triggers Repository Dispatch across satellite repos)   │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│               3. Stage: Sovereign Build & Anti-Lock         │
│      (Runs strip-magic.sh & vercel deploy --prebuilt)       │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│               4. Stage: Fibonrose Task Verification         │
│     (Validates Fibonacci complexity 0-9 checkpoints)        │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│               5. Stage: Security & SSRF Protection Scan     │
│   (Path Guards, ipaddr.js IP filters, secret scrubbing)     │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│               6. Stage: Deployment & Ingress Gate           │
│  (Targeting vr4deaf.org live portal & GKE container nodes)  │
└─────────────────────────────────────────────────────────────┘
```

---

## 3. How to Trigger via GitHub UI & CLI

### **Via GitHub Actions UI:**
1. Navigate to the **Actions** tab in `Pmaster-dev/.github`.
2. Select **PMaster Powerful Pipeline Orchestrator** on the left panel.
3. Click **Run workflow**, choose your desired `stage`, `environment`, `component`, and toggle `dry_run`.

### **Via GitHub CLI (`gh`):**
```bash
gh workflow run pmaster-orchestrator.yml \
  -f stage=sovereign-build \
  -f environment=production \
  -f component=deafauth-api \
  -f dry_run=true
```
