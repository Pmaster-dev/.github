# MBTQ / 360Magicians Full Ecosystem Duplicates Report
# Created: 2026-08-09
# Status: COMPLETED

This report outlines detected system, code, and config duplications across the connected available source repositories.

---

## 1. Duplicate Authentication Implementations

### **Findings**
There are multiple independent auth configurations and mock implementations across repositories, which creates severe drift.

* **Implementation A: Active GKE Production Service**
  - **File**: `services/deafauth-api/src/server.ts` in `municipal-dao-v`
  - **Technology**: Node.js/Express querying Firestore Native `deafauth-profiles` and caching in Redis.
* **Implementation B: Next.js Reference Provider**
  - **File**: `deafauth` repository
  - **Technology**: Next.js App router using Supabase Auth client and Postgres triggers.
* **Implementation C: Monorepo Specification**
  - **File**: `Services/deafauth` directory in `deaf-first-platform`
  - **Technology**: Stateless OpenAPI YAML mappings and JSON schema files.

### **Risk / Evidence**
Security and user data models are implemented three different ways (Firestore, Supabase Postgres, and Swagger models). User profiles synced to one won't reflect in the other.

---

## 2. Duplicate Staking & DAO Interfaces

### **Findings**
DAO staking, proposal creations, and voting cards are duplicated across Next.js frontends.

* **Implementation A: Web3 Staking Showcase**
  - **File**: `services/mbtquniverse-dao/src/web3-staking-showcase.ts` in `municipal-dao-v`
  - **Technology**: Uses `ethers.js` pointing to environment contract addresses.
* **Implementation B: reference fibonrose**
  - **File**: `fibonrose` repository
  - **Technology**: Custom Next.js components (`components/VerificationDashboard.tsx`) with local React state and mock triggers.

---

## 3. Duplicate Task Validators

### **Findings**
Code validation, Fibonacci scaling rules, and evidence checking are duplicated:

* **Implementation A: Fibonrose Validator Module**
  - **File**: `fibonrose/fibonrose-validator.ts` in `mbtq-dev`
  - **Technology**: Advanced TypeScript validator class with robust unit testing suites.
* **Implementation B: Trust Engine Action**
  - **File**: `trust-engine` repository
  - **Technology**: Pre-packaged TypeScript action boilerplate.

---

## 4. Duplicate Environment & Configuration Files

### **Findings**
Multiple repositories define their own set of endpoints, resulting in conflicting URL defaults:

* **File A**: `.env.pinkflow` in `pinkflow` repository (`DEAFAUTH_ENDPOINT=https://deafauth.mbtq.dev`)
* **File B**: `deafauth-deployment.yaml` ConfigMap in `municipal-dao-v` (`DEAFAUTH_API_URL=https://deafauth.mbtq.dev`)
* **File C**: `deafauth+pinksync.md` specification guide (`deafauthUrl=http://auth:3002`)
* **File D**: `client/verify.js` in `mbtq-dev` (`http://localhost:3000`)
