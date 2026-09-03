# 📦 MBTQ / 360Magicians Complete Artifact & License Classification Matrix
# Primary Maintainer: @pinkycollie
# Created: 2026-08-09
# Status: COMPLETED

This document catalogs and classifies all discovered ecosystem artifacts by technical category (Automated Resources, Snippets, Source Code, KV/Databases, Markdown Docs, Workflows, Types, Activities, Microservices, Potential Artifacts, Splash Screens/UI Assets) and delineates **Open-Source (MIT/Apache 2.0)** vs. **Proprietary/Sovereign** licensing boundaries.

---

## 1. Technical Artifact Categorization Matrix

| Category | Description / Scope | Discovered Locations | Primary File Formats |
|---|---|---|---|
| **Auto Resources** | Automatically provisioned cloud & infrastructure resources | `gcp-infrastructure/terraform/main.tf` in `municipal-dao-v` | HCL Terraform (`main.tf`), K8s YAML |
| **Snippets & Vppet** | Short reusable code/preset blocks & visual prompts | `client/src/components/SignVisualSystem/semantics.tsx` in `mbtq-dev` | TS, TSX, JSON |
| **Source Code (`src`)** | Production application logic & backend controllers | `services/` in `municipal-dao-v`, `client/src/` in `mbtq-dev` | TypeScript (`.ts`, `.tsx`), Python (`.py`), Node.js |
| **KV & Data Stores** | Key-Value caches, document databases, & session stores | Redis (`deafauth-cache`), Firestore (`deafauth-profiles`), MongoDB | Redis commands, Firestore JSON, MongoDB |
| **Markdown Docs (`md`)** | Architecture guides, specifications, & audit logs | `/docs` in `mbtq-dev`, `/audit` directory in `.github` | Markdown (`.md`) |
| **Workflows** | CI/CD pipelines, automated bots, & sync scripts | `.github/workflows/` in `.github` and `mbtq-dev` | YAML (`.yml`, `.yaml`), TypeScript |
| **Types & Interfaces** | Shared TypeScript interfaces & OpenAPI schemas | `lib/deafauth-sdk.ts`, `types.ts`, `Services/*/openapi.yaml` | TypeScript (`.ts`), OpenAPI YAML |
| **Activities & Jobs** | Background queues, scheduled crons, & event loops | `caching.json` in `deaf-first-platform`, `websocket-server.js` | Node.js, Bull/Redis Queues, Cron |
| **Microservices** | Standalone containerized backend applications | `deafauth-api`, `pinksync-middleware`, `vertex-ai-hub` | Express, FastAPI, Nest.js, Dockerfiles |
| **Potential Artifacts** | Compiled build outputs, bundles, & prebuilt trees | `.next/`, `dist/`, Vercel prebuilt outputs (`vercel build --prod`) | JS bundles, WASM, `.mjs` |
| **Splash Screens & UI** | Avatars, visual state panels, & splash graphics | `SignerPanel.tsx`, `placeholder-logo.png`, `icons/` SVG assets | TSX, SVG, PNG, WebP |

---

## 2. Licensing Boundaries: Open-Source vs. Proprietary / Sovereign

The MBTQ ecosystem enforces a strict dual-licensing boundary separating universal open-source utilities from proprietary sovereign assets.

### **A. Open-Source Component Boundary (MIT / Apache 2.0)**
The following infrastructure, SDKs, and developer utilities are published as **Open-Source** to foster community adoption:

1. **DeafAUTH SDK & Client Helpers (`@mbtq/deafauth-sdk`)**: MIT License
   * Universal client hooks (`useDeafAUTH`) and browser login popup integrations.
2. **Sign Visual System Engine (`SignVisualSystem`)**: MIT License
   * Reusable React panel visual state machine for agent communication.
3. **Fibonrose Task Validator (`FibonroseValidator`)**: MIT License
   * Fibonacci-based GitHub checklist and issue validation classes.
4. **Starter Workflows Mirror (`Pmaster-dev/.github`)**: MIT License / Unlicense
   * GitHub Actions templates and data validation scripts.

### **B. Proprietary / Sovereign Boundary (MBTQ Sovereign License)**
The core business logic, proprietary AI fine-tuning weights, and sovereign deployment pipelines are **Proprietary**:

1. **360Magicians Vertex AI Multi-Domain Engine**: Proprietary
   * Gemini-1.5-pro specialized prompt wrappers and visual-to-sign conversion weights.
2. **PinkSync Accessibility Transformer & Haptic Telemetry**: Proprietary
   * Proprietary transformation matrix for real-time visual-tactile adaptations and service worker sync logic.
3. **Mbtq-Sovereign Anti-Vendor-Lock Deployment (`Mbtq-sovereign.yml`)**: Sovereign
   * Script (`strip-magic.sh`) that scrubs background cloud telemetry to compile pure, vendor-independent binaries.
4. **NegraRosa NFT Identity Attestation Engine**: Sovereign
   * Zero-custody audit logging and "I AM WHO I AM" token minting parameters.

---

## 3. Rebuild & Re-compilation Checklist

When executing a clean forward rebuild:
* [x] **Source Code (`src`)**: Re-compile TypeScript services from `municipal-dao-v/services/` and client layouts from `mbtq-dev/client/`.
* [x] **Types**: Import strict interfaces from `lib/deafauth-sdk.ts` and `audit/schema.json`.
* [x] **Auto Resources**: Apply Terraform manifests in `gcp-infrastructure/terraform/main.tf` to provision GKE node pools, Firestore Native, and Redis caches.
* [x] **Potential Artifacts**: Run `Mbtq-sovereign.yml` to compile vendor-clean prebuilt trees (`vercel deploy --prebuilt`).
