# MBTQ / 360Magicians Full Ecosystem Security Findings
# Created: 2026-08-09
# Status: COMPLETED

This report outlines key security vulnerabilities, exposed attack patterns, and authorization gaps identified during the source audit.

**NOTE: Real passwords, private keys, or actual token hashes have been omitted to maintain system integrity.**

---

## 1. SSRF (Server-Side Request Forgery) in Webhooks [RESOLVED / COMPLETED]

### **The Finding**
Historically, the `/api/webhooks/register` endpoint accepted any valid URL. An attacker could register loopback (`127.0.0.1`), metadata services (`169.254.169.254`), or private local addresses, enabling them to map ports or exfiltrate GCP credentials.

### **Remediation & Present State**
* **File**: `.jules/sentinel.md` & `server/src/utils/ssrfAgent.ts` (in `mbtq-dev`)
* **Solution**: Fully patched. The server now integrates `ipaddr.js` to parse and natively convert mapped IPv6 addresses (e.g. `0:0:0:0:0:ffff:127.0.0.1` and `::ffff:`) and restricts connections to internal subnets, localhost, and AWS/GCP metadata endpoints. Redirects are configured to be strictly validated or disabled.
* **Severity**: Formerly High, currently **RESOLVED**.

---

## 2. Overly Permissive CORS Headers in Development Files [MEDIUM DEBT]

### **The Finding**
Multiple reference scripts and active development server scripts configure CORS to allow all incoming origins (`*`).
* **Location**: `server/src/index.ts` in `mbtq-dev` (as logged in `.jules/sentinel.md`).

### **Remediation & Current State**
* **Solution**: In GKE production manifests (`services/deafauth-api/src/server.ts`), CORS is securely restricted using origin validators checking the `SUPPORTED_DOMAINS` array (`*.mbtquniverse.com`, `pinksync.io`, etc.).
* **Recommendation**: Dev environments should port these strict origin checks to prevent security drift from localhost testing to live deployments.
* **Severity**: **Medium**.

---

## 3. Absence of Strict RBAC in Community Verification [LOW DEBT]

### **The Finding**
The community verification endpoint allows users to endorse or verify other users to increase their reputation levels.
* **Location**: `services/deafauth-api/src/server.ts` -> `/api/verification` route.
* **Code**:
  ```typescript
  app.post("/api/verification", async (req, res) => {
    const { targetUserId, verifierUserId, verificationType, evidence, domain } = req.body;
    ...
  ```

### **Vulnerability & Threat**
Although the endpoint issues a Pub/Sub event for review, it lacks strict server-side authentication verifying that the `verifierUserId` matches the user signing the request. An attacker could spoof endorsements on behalf of trusted community members to artificially inflate user reputation scores.

### **Recommendation**
Restrict verifier validation strictly to the authenticated user ID extracted from the signature token.
* **Severity**: **Low-Medium**.

---

## 4. Hardcoded Database Identifiers in Manifests [LOW DEBT]

### **The Finding**
GKE environment ConfigMaps and deployment configurations hardcode database IDs:
* **Location**: `gcp-infrastructure/deafauth-deployment.yaml` (`FIRESTORE_DATABASE: "deafauth-profiles"`).
* **Recommendation**: While not a secret key, the database name should be dynamically populated via deployment values to prevent profiling of internal cloud infrastructure.
* **Severity**: **Low**.
