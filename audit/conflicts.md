# MBTQ / 360Magicians Full Ecosystem Conflicts Report
# Created: 2026-08-09
# Status: COMPLETED

This report logs detected naming collisions, conflicting runtime assumptions, and mismatched architectural schemas.

---

## 1. Naming Collisions: The "deafauth" Identity Target

### **Findings**
There is a high-risk naming collision regarding `deafauth`:
1. **`deafauth` (the repository)**: Represents a client-side Next.js specification leveraging Supabase Auth.
2. **`deafauth-api` (in `municipal-dao-v`)**: Represents the active Node.js / Firestore backend.
3. **`deaf-first-platform/Services/deafauth`**: Represents the older monorepo OpenAPI specification.

### **Conflict & Risk**
If a developer references the `@mbtq/deafauth` package, they will download the Next.js library, which assumes a **Supabase SQL database layout**. However, the actual deployed GKE cluster utilizes **GCP Firestore (NoSQL)**. They are entirely incompatible. Calling SQL-style tables on NoSQL Firestore databases will lead to runtime crashes.

---

## 2. Naming Collisions: The "fibonrose" Token and Trust Target

### **Findings**
Mismatched definitions of `fibonrose`:
1. **`fibonrose` (the repository)**: Represents a Next.js Reference App focused on Web3 dashboards.
2. **`mbtq-dev/fibonrose`**: Represents the operational **Fibonrose Task Validator** used by developer magicians to check code check-ins.
3. **`deaf-first-platform/Services/fibonrose`**: Outlines a generic trust API spec.

### **Conflict & Risk**
The reference app utilizes local mock React state. The developer task validator parses commit SHAs and operates strictly inside GitHub Actions. If these are combined, task checklists on GitHub could block code pipelines because they are missing the on-chain metadata expected by the reference dashboards.

---

## 3. Conflicting Security Schemes: JWT vs Paseto

### **Findings**
The security tokens issued by identity blocks conflict:
* **Active Express.js Backend** (`services/deafauth-api/src/server.ts`): Uses signed **JWT** tokens (`accessToken: deafauth_${profile.id}_${Date.now()}`).
* **Monorepo Architecture Specification** (`deaf-first-platform/README.md`): Specifies the use of **Paseto** (Platform-Agnostic Security Tokens) as the standard cross-service authentication method.

### **Conflict & Risk**
Downstream middleware (e.g. `pinksync-middleware`) attempting to parse incoming headers using a Paseto library will crash or reject active connection requests from the JWT-issuing backend.

---

## 4. Conflicting Runtime Port Assumptions

### **Findings**
Multiple documents and service manifests assume the same port allocations:
* **Port 3000**:
  - Assigned to `mbtq-platform` in `mbtq-ecosystem.yaml` (GKE Deployment).
  - Assigned to local client dev servers in `client/package.json` in `mbtq-dev`.
* **Port 8080**:
  - Assigned to `deafauth-api` in `gcp-infrastructure/deafauth-deployment.yaml`.
  - Assigned to `vertex-ai-hub` (360magicians-vertex-ai) in `ecosystem-architecture/mbtq-ecosystem.yaml`.
* **Port 3002**:
  - Assigned to legacy `deafauth` server in `deafauth+pinksync.md` (`deafauthUrl = http://auth:3002`).

### **Conflict & Risk**
Deploying these services on the same local cluster or local host without containerized namespaces will trigger immediate **Port Already In Use** errors and halt execution.
