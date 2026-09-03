# 🌹 MBTQ / 360Magicians Full Source Collection & Architecture Audit
# Author: Jules, Lead Software Engineer
# Date: August 2026
# Status: MASTER COMPLETED (Audit Phase)

---

## Executive Summary

The **MBTQ / 360Magicians** ecosystem represents an advanced, Deaf-first development and execution platform. The foundational principle — **"Sign Leads, Text Follows"** — treats accessibility preferences as a first-class identity standard.

Historically fragmented across multiple specifications and individual reference repositories, the ecosystem has converged into an operational, highly cohesive deployment today. This audit acts as a comprehensive, historical, and current-source audit of all connected material.

---

## Part 1: Core Findings (The 16 Questions Answered)

### 1. What actually exists?
An operational, containerized, GKE-ready platform consisting of:
* An active, production-ready live public portal (**`vr4deaf.org`**).
* An identity provider service (**DeafAUTH**).
* An inclusive security framework (**NegraRosa**).
* An AI-powered universal professional verification engine (**FibonRoseTrust**).
* An accessibility middleware service (**PinkSync**).
* A specialized multi-domain Vertex AI agent hub (**360Magicians**).
* A client interface engine featuring the **Sign Visual System** state machine.
* A Web3-capable governance, staking, and project auditing dashboard (**MBTQ Universe**).
* A task-complexity and checkpoint validator (**Fibonrose**).
* A MicroVM code execution sandbox configuration (**PinkFlow**).

### 2. Where does it exist?
* **Live Real-World Portal**: **`vr4deaf.org`** (the ONLY active, production-ready live domain in the real world).
* **Runtime Implementations**: In the **`municipal-dao-v`** repository under `/services` (`deafauth-api`, `pinksync-middleware`, `360magicians-vertex-ai`, `mbtq-platform`, `mbtquniverse-dao`).
* **Security & Trust Layer**: In **`NegraRosa`** (NFT identity & zero-custody verification) and **`FibonRoseTrust`** (AI interpreter/provider verification).
* **Interactive Frontend Elements**: In the **`mbtq-dev`** repository (`client/src/components/SignVisualSystem/`).
* **GitHub Static & Endpoint Fallbacks**: GitHub Pages static endpoints (`https://Pmaster-dev.github.io/<repo>`), raw GitHub API endpoints, and static `src` code references.
* **Specifications**: In the **`deaf-first-platform`** repository.

### 3. What is historical?
* The **`deaf-first-platform`** repository (acts as an older, monolithic specification registry containing OpenAPI specs, but not the active production code).
* **`deafauth`**, **`pinksync-app`**, and **`fibonrose`** repositories: Separate, stand-alone reference applications that have drifted from the GCP Firestore-backed microservices.

### 4. What is currently active?
**`vr4deaf.org`** in live production. The GKE cluster deployment configurations, Google Cloud Terraform blueprints, Firestore NoSQL structures, and Express/Next.js files inside the **`municipal-dao-v`** repository. Also, `NegraRosa`, `FibonRoseTrust`, and active React visual state panels inside `mbtq-dev`.

### 5. What is duplicated?
* **Authentication**: Firestore-based registrations (`deafauth-api`) duplicate Next.js/Supabase auth methods (`deafauth` reference repository).
* **Staking Interfaces**: Live ethers.js contract dashboards (`mbtquniverse-dao`) duplicate mock local state components (`fibonrose` reference repository).
* **Validation**: Code checking classes inside `mbtq-dev/fibonrose/` duplicate Action files in the `trust-engine` repository.

### 6. What conflicts?
* **Database Mismatch (Critical)**: `deafauth` reference app uses Supabase/SQL. The production deployed service (`deafauth-api`) uses GCP NoSQL Firestore. Developers merging code between the two will trigger fatal database crashes.
* **Security Tokens**: Active services issue custom **JWT** strings, whereas monolithic specifications require **Paseto** headers.
* **Ports**: Port 3000 is double-assigned to `mbtq-platform` and local client servers. Port 8080 is double-assigned to `deafauth-api` and `vertex-ai-hub`.
* **Inactive Custom Domains**: Domain aliases (`mbtq.dev`, `360magicians.com`, `pinksync.io`, `mbtquniverse.com`, `deafauth.mbtq.dev`) are inactive/gone, requiring fallback to GitHub static endpoints and `vr4deaf.org`.

### 7. What is infrastructure versus architecture?
* **Architecture**: The multi-layered L0-L10 specifications defining WCAG-alternative visual sign frameworks, Fibonrose difficulty check-ins, NegraRosa NFT credentials, and one-layer synchronization.
* **Infrastructure**: The Google Cloud Platform resources (GKE cluster node-pools, GCP managed SSL Certificates, Global IP load balancers, Cloud DNS, Redis instances, and GCS buckets) detailed in `gcp-infrastructure/terraform/main.tf` in `municipal-dao-v`.

### 8. What is canonical?
* **Live Gateway**: `vr4deaf.org`.
* **Configuration**: `ecosystem-architecture/mbtq-ecosystem.yaml` in `municipal-dao-v`.
* **Services**: The Node.js and TypeScript services inside `municipal-dao-v/services/`.
* **Security**: `NegraRosa` (inclusive NFT identity framework).
* **Trust & Verification**: `FibonRoseTrust` (AI universal verification system).
* **Client SDK**: `municipal-dao-v/lib/deafauth-sdk.ts`.
* **State Machine**: `client/src/components/SignVisualSystem/` in `mbtq-dev`.
* **Validator**: `fibonrose/fibonrose-validator.ts` in `mbtq-dev`.
* **Sandbox**: `pinkflow/container` in `pinkflow`.

### 9. What is uncertain?
* **360-Magicians vs 360magicians**: Mismatched documentation references and loose GitHub account contexts. **`360magicians`** is cleaner, more modern, and closer to current goals, while **`360-magicians`** is messier but contains historical context.
* **Physical Hardware Integration**: Failover flash triggers and haptic vibrator pipelines exist as modular mock abstractions but lack actual hardware-driver integrations.

### 10. What should NOT be touched?
* The live `vr4deaf.org` portal endpoints.
* The GKE/Kubernetes deployment structures and active database routes inside `municipal-dao-v`.
* The **Sign Visual System** React layout and **Fibonrose Task Validator** classes inside `mbtq-dev`.

### 11. What should be consolidated?
* All custom authentication methods across reference and specifications repos must be aligned to the GKE Firestore native profile schema, NegraRosa NFT identity standard, and `vr4deaf.org` portal.
* All duplicate vector icons and SVGs (`icons/` folder, etc.) should be routed to a centralized, unified asset CDN.

### 12. What should be retired?
* **Supabase relational database logic** in `deafauth` and `fibonrose` reference apps (to prevent SQL developer-drift).
* **Legacy, unmaintained directories** in the `deaf-first-platform` monorepo that have been replaced by GKE service backends.

### 13. What foundational pieces are missing?
* A unified, centralized configuration repository managing shared environment variables and secrets dynamically (instead of duplicating plain text `.env` parameters across repos).
* Direct Web3 wallet signing integrations mapped into the server-side DeafAUTH login profile flow.

### 14. What should PMaster do next?
1. **Approve this Master Audit** to lock down the ecosystem boundaries.
2. **Synchronize all documents and files** across the 360magicians and 360-magicians scopes.
3. **Download and backup verified assets** into a secure Obsidian vault and Proton Drive.
4. **Archive the historical/messy accounts** and focus strictly on `360magicians` aligned repos.
5. **Execute a structured consolidation phase** merging GKE-native services, NegraRosa security, FibonRoseTrust, and the React visual state engine into a single, clean canonical repo.

---

## Part 2: Discovered Repository Registry

1. **`vr4deaf.org` [LIVE PRODUCTION GATEWAY]**
   * *Status*: Active Production. The primary operational real-world gateway.
2. **`municipal-dao-v` [CANONICAL PRODUCTION BACKEND]**
   * *Status*: Active. Contains GCP infrastructure scripts, GKE deployment files, and current operational service code.
3. **`mbtq-dev` [CANONICAL CLIENT & VALIDATOR]**
   * *Status*: Active. Houses the React-based Sign Visual System and the fully tested Fibonrose Task Validator module.
4. **`NegraRosa` [CANONICAL SECURITY]**
   * *Status*: Active. Inclusive security framework providing NFT-based identity and zero-custody credential sharing.
5. **`FibonRoseTrust` [CANONICAL TRUST & VERIFICATION]**
   * *Status*: Active. AI-powered universal professional verification engine for interpreters, professionals, and community capabilities.
6. **`pinkflow` [CANONICAL SANDBOX]**
   * *Status*: Active. Houses blueprints and sandboxing VM specifications for code verification.
7. **`deafauth` [REFERENCE / DEPRECATED]**
   * *Status*: Historical. Reference Next.js client providers using Supabase. Needs DB model refactoring.
8. **`pinksync-app` [REFERENCE / DEPRECATED]**
   * *Status*: Historical. Next.js widget and Chrome extension workspace.
9. **`fibonrose` [REFERENCE / DEPRECATED]**
   * *Status*: Historical. Reference staking dashboard templates.
10. **`deaf-first-platform` [SPECIFICATIONS MONOREPO]**
    * *Status*: Historical. Contains older OpenAPI schemas.
11. **`accessibility-validator` [EXPERIMENTAL]**
    * *Status*: Experimental. AI accessibility CLI tool written in Python.
12. **`Aegis` [EXPERIMENTAL]**
    * *Status*: Experimental. Next.js AI security proof-of-concept.
13. **`business-service`, `Job-service`, `Justifed-Idea-Generator` [WORKFORCE SUITE]**
    * *Status*: Active. Services supporting business and vocational rehabilitation goals.
