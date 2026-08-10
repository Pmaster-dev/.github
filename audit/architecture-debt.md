# MBTQ / 360Magicians Full Ecosystem Architectural Debt
# Created: 2026-08-09
# Status: COMPLETED

This report catalogs architectural, configuration, and structural debt discovered within the available source material, labeled by priority levels:

---

## P0 — CRITICAL DEBT (Immediate Action Required)

### **1. Weak / Plaintext Secrets in Active Manifests**
* **Location**: `services/deafauth-api/src/server.ts`
* **Finding**: The server references `process.env.REDIS_URL` and GCP client keys. In `deaf-first-platform/Mbtq-sovereign.yml`, Vercel tokens are pulled down directly. There is a lack of automated secrets management (e.g. Hashicorp Vault or GCP Secret Manager integrations) in active manifests.
* **Impact**: Elevated risk of credential leakage in production logs or environment dumps.

### **2. Database and ORM Divergence**
* **Location**: `mbtq-dev/server/prisma/` vs `services/deafauth-api/src/server.ts`
* **Finding**: `mbtq-dev` contains an fully populated Prisma layout pointing to a relational SQL database. The active GKE deployment service uses Google Firestore (a NoSQL document database).
* **Impact**: Devs writing database schemas for SQL via Prisma are entirely disconnected from the actual production document store, leading to broken data access patterns upon merging.

---

## P1 — HIGH DEBT (Should Be Resolved in Next Phase)

### **1. Orphaned Reference Repositories**
* **Location**: `deafauth`, `pinksync-app`, `fibonrose` repositories.
* **Finding**: These reference projects contain outdated code configurations that have drifted significantly from the actively deployed services in `municipal-dao-v`.
* **Impact**: Developers looking at the reference repositories will build components using outdated Supabase-style models instead of the production GCP NoSQL structures.

### **2. Mismatched Token Standards**
* **Location**: Active Code (JWT) vs Spec Docs (Paseto).
* **Finding**: The code issues raw custom JWT strings, while the architectural guides in `deaf-first-platform` mandate Paseto tokens.
* **Impact**: Incompatible authentication handshakes between compliant downstream middleware and the active auth API.

---

## P2 — MODERATE DEBT (Refactor Scheduled)

### **1. Broken Internal Reference Domains**
* **Location**: `deafauth+pinksync.md` and `Mbtq-sovereign.yml`.
* **Finding**: The deployment scripts reference local hostnames like `http://auth:3002`, while active GKE manifests point to `https://deafauth.mbtq.dev`.
* **Impact**: Local developer integration scripts fail immediately because they query legacy ports and domains instead of the GKE ingress gateway.

### **2. Telemetry and Linter Drift**
* **Location**: Root `package.json` vs Workspaces.
* **Finding**: The `deaf-first-platform` Monorepo contains a package.json referencing ancient lint configurations that conflict with the stricter Vitest/TS rules in `mbtq-dev` and `municipal-dao-v`.
* **Impact**: Code compiles locally but fails CI pipelines because of mismatched static analysis settings.

---

## P3 — MINOR DEBT (Document and Monitor)

### **1. Duplicate UI Icon and Vector Assets**
* **Location**: `icons/` folder in `.github` vs `client/public/` folders.
* **Finding**: High amount of duplicate SVG icons (e.g. `ada.svg`, `black-duck.svg`, `frogbot.svg`) replicated across developer and asset repos.
* **Impact**: Minor bloat, easily consolidated by a unified asset CDN.
