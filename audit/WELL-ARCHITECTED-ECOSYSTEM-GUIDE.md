# 🏛️ MBTQ / 360Magicians Well-Architected Ecosystem Guide
# Primary Maintainer: @pinkycollie
# Created: 2026-08-09
# Status: COMPLETED

This document defines the **GitHub Well-Architected Framework** for the MBTQ / 360Magicians ecosystem. It catalogs the roles of **QA Agents & Developer Magicians**, **GitHub Pages & Cloudflare Edge Status**, **Showcase & Demo Lifecycles**, and provides a detailed **Ecosystem Dependency & Cloud Cost Analysis**.

---

## 1. QA Agents & Autonomous Developer Magicians

The ecosystem employs a team of specialized AI agents and QA validators:

### **Agent Roster & Responsibilities**

| Agent / Bot Name | Primary Role | Trigger & Tools | Quality Gate / Output |
|---|---|---|---|
| **PMaster Auto-Dev Router** | Orchestrator & Request Router | `workflow_dispatch` / Issue events | Delegates task requests to specialized sub-agents based on domain/complexity. |
| **Quinn (Developer Magician)** | Task Complexity Assessor | Issue comments / Fibonrose | Calculates Fibonacci complexity (0-9) and generates evidence checklists. |
| **CodeValidationAgent** | MicroVM Sandbox Verifier | `pinkflow-sandbox` / FastAPI | Spawns Firecracker MicroVMs to test partner code safely before merging. |
| **Accessibility Auditor Agent** | Deaf-First UX Validator | `accessibility-validator` | Evaluates interfaces against "Sign Leads, Text Follows" rules and WCAG 2.1 AAA. |
| **Security Sentinel Agent** | Path Guard & SSRF Reviewer | `server/src/utils/ssrfAgent.ts` | Enforces IP parsing (`ipaddr.js`), path guards (`path.resolve`), and secret scrubbing. |

---

## 2. GitHub Pages & Cloudflare Edge Deployment Status

Since custom domain registrations (`mbtq.dev`, `360magicians.com`, `pinksync.io`) are inactive, static frontends and edge workers fall back to **GitHub Pages** and **Cloudflare Edge Workers**:

```
                       ┌─────────────────────────────────────┐
                       │     Production Live Domain          │
                       │          https://vr4deaf.org        │
                       └──────────────────┬──────────────────┘
                                          │
            ┌─────────────────────────────┴─────────────────────────────┐
            │                                                           │
┌───────────▼───────────┐                                   ┌───────────▼───────────┐
│ GitHub Pages Static   │                                   │ Cloudflare Edge       │
│ https://Pmaster-dev.  │                                   │ JSON API Workers      │
│ github.io/<repo>      │                                   │ https://api.mbtq.dev/ │
└───────────────────────┘                                   └───────────────────────┘
```

### **Deployment Matrix**

| Repository Scope | GitHub Pages Live URL | Cloudflare / Edge Function Target | Status |
|---|---|---|---|
| **`vr4deaf.org`** | `https://vr4deaf.org` | Cloudflare DNS & SSL Proxy | **ACTIVE LIVE PUBLIC PORTAL** |
| **`mbtq-dev`** | `https://Pmaster-dev.github.io/mbtq-dev` | Vercel Edge / GitHub Pages | Operational Static Demo |
| **`municipal-dao-v`** | `https://Pmaster-dev.github.io/municipal-dao-v` | Cloudflare Edge JSON Specs | Operational Static Showcase |
| **`deaf-first-platform`**| `https://Pmaster-dev.github.io/deaf-first-platform` | GitHub Pages (index.html) | Historical OpenAPI Registry |
| **`deafauth`** | `https://Pmaster-dev.github.io/deafauth` | Cloudflare Auth Worker | Historical Reference |
| **`pinksync-app`** | `https://Pmaster-dev.github.io/pinksync-app` | Service Worker (`pinksync-sw.js`) | Historical Reference |

---

## 3. Showcase & Interactive Demo Lifecycles

Interactive showcases demonstrate Deaf-first principles across the application lifecycle:

1. **Sign Visual System Demo (`mbtq-dev/client`)**:
   * Displays persistent, dockable `SignerPanel` mapping 8 agent states visually with zero reliance on audio notifications.
2. **Web3 Staking & DAO Showcase (`municipal-dao-v/services/mbtquniverse-dao`)**:
   * Interactive ethers.js interface providing visual staking progress, sign-language instruction videos, and real-time WebSocket voting charts.
3. **Justified Idea Generator (`Justifed-Idea-Generator`)**:
   * Interactive HTML tool generating business proposals for SBA, VR, and funding agencies.

---

## 4. Ecosystem Dependency & Monthly Cloud Cost Analysis

The ecosystem operates on a highly optimized, low-cost serverless and cloud footprint:

### **Monthly Cloud Infrastructure Cost Breakdown (Estimated)**

| Cloud Provider | Service / Resource | Instance Type / Tier | Monthly Est. Cost |
|---|---|---|---|
| **Google Cloud Platform (GCP)** | GKE Cluster (`deafauth-cluster`) | 2x `e2-medium` nodes | ~$48.00 / mo |
| **Google Cloud Platform (GCP)** | Firestore Native (`deafauth-profiles`) | Document Storage (1GB free tier) | $0.00 - $5.00 / mo |
| **Google Cloud Platform (GCP)** | Memorystore for Redis | 1GB `REDIS_6_X` cache | ~$15.00 / mo |
| **Google Cloud Platform (GCP)** | Cloud Run (`pinkflow-sandbox`) | Ephemeral MicroVMs (Pay-per-use) | $2.00 - $10.00 / mo |
| **Google Cloud Platform (GCP)** | Vertex AI Gemini-1.5-pro | API Calls (Pay-per-token) | $5.00 - $25.00 / mo |
| **Cloudflare** | DNS, SSL & Edge Workers | Free / Pro Plan | $0.00 - $20.00 / mo |
| **Vercel** | Sovereign Frontend Builds | Hobby / Pro Tier | $0.00 - $20.00 / mo |
| **GitHub Actions** | Runners & Workflow Artifacts | Public Open Source Free Minutes | $0.00 / mo |
| **Web3 Polygon RPC** | Infura / Alchemy Node Provider | Free Developer Tier | $0.00 / mo |
| **TOTAL ESTIMATED MONTHLY COST** | **All Ecosystem Components** | **Serverless + Prebuilt Hybrids** | **~$70.00 - $143.00 / mo** |

### **Cost Optimization Recommendations for @pinkycollie**
1. **Scale Cloud Run to 0**: Ensure `pinkflow-sandbox` container instances scale to 0 when no integration verifications are actively running.
2. **Utilize Free Tier Web3 RPCs**: Route Polygon JSON-RPC calls through public free endpoints (`polygon-rpc.com`).
3. **Static Caching via Cloudflare**: Serve static asset icons and Vite bundles directly from Cloudflare Edge Caches to minimize GCS bandwidth costs.
