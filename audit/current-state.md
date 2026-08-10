# MBTQ / 360Magicians Full Ecosystem Current State
# Created: 2026-08-09
# Status: ACTIVE (Audit Summary)

## Executive Summary

As of August 2026, the connected MBTQ / 360Magicians ecosystem has transitioned from detached specifications and reference implementations into an operational, highly cohesive deployment.

The primary target repository representing what actually exists and runs TODAY is **`municipal-dao-v`**, which manages the GKE (Google Kubernetes Engine) configurations, GCP Terraform scripts, and active service codebases under its `services/` directory.

---

## 1. Active Services & Implementations (Today)

The following components represent the actively running runtime services of the ecosystem:

### 🔐 DeafAUTH (Identity Cortex)
* **Location**: `services/deafauth-api/src/server.ts` in `municipal-dao-v`
* **Technology**: Node.js, Express, Helmet, CORS, Firestore ("deafauth-profiles"), Redis ("deafauth-cache"), GCP Pub/Sub.
* **Role**: Universal identity system managing profiles containing user identity metadata, verification levels, preferred sign languages, and visual preferences.
* **Active Status**: Operational. Exposes user onboarding and domain statistic queries.

### 🔄 PinkSync Middleware (Accessibility Engine)
* **Location**: `services/pinksync-middleware/src/accessibility-transformer.ts` in `municipal-dao-v`
* **Technology**: TypeScript, Service Workers, offline caches.
* **Role**: Accessibility middleware transforming incoming content payloads into visual reading hierarchies, tactile patterns, sign language metaphors, or high-contrast styles. Supports offline task queues that automatically synchronize when online.
* **Active Status**: Operational. Embedded in the routing layers of downstream applications.

### 🎨 360Magicians AI Hub (Vertex AI Multi-Domain)
* **Location**: `services/360magicians-vertex-ai/src/multi-domain-ai.ts` in `municipal-dao-v`
* **Technology**: `@google-cloud/vertexai`, Gemini-1.5-pro.
* **Role**: Configures specialized sub-AI systems (Creative, Design, Content, Accessibility) using Google's generative models, enhancing prompt scopes with accessibility preferences.
* **Active Status**: Operational. Backed by Google Cloud Vertex AI infrastructure.

### 🏠 MBTQ Platform (Deaf-First UI Platform)
* **Location**: `services/mbtq-platform/src/v0-gemini-bridge.ts` in `municipal-dao-v`
* **Technology**: `@ai-sdk/google`, Gemini-1.5-pro, Google Studio Proxy.
* **Role**: Bridges interactive design prompts with generative models to compile pure React/Next.js files customized for visual accessibility.
* **Active Status**: Operational. Supported by the **Sign Visual System** React frontend suite running inside the `mbtq-dev` repository (mapping 8 agent states visually).

### 🌌 MBTQ Universe DAO (Governance & Staking)
* **Location**: `services/mbtquniverse-dao/src/web3-staking-showcase.ts` in `municipal-dao-v`
* **Technology**: Next.js, WebSockets, framer-motion, ethers.js.
* **Role**: Implements real-time proposal viewing, animated voting charts, quorum trackers, and Web3 staking dashboards that integrate with active Solidity contracts on Polygon.
* **Active Status**: Operational. Leverages active WebSocket rooms in `server/websocket-server.js`.

---

## 2. Satellite & Operational Tooling

Beyond GKE container deployments, the ecosystem has fully coded satellite assets:

### 🌹 Fibonrose Task Validator
* **Location**: `fibonrose/` in `mbtq-dev`
* **Technology**: TypeScript, Vitest, Octokit, Github Actions (`fibonrose-validator.yml`).
* **Role**: Evaluates task complexity levels (0-9) using the Fibonacci sequence, creating structured issue checklists on GitHub, and requiring precise evidence links before confirming checkpoints.
* **Active Status**: Operational. Actively runs unit tests with 100% code coverage.

### 🛡️ PinkFlow MicroVM Sandbox
* **Location**: `pinkflow/` repository
* **Technology**: Firecracker MicroVMs, FastAPI, Python subprocess, cgroups.
* **Role**: Spawns isolated, resource-constrained VMs to evaluate and verify partner-submitted integration scripts, grading and anchoring results directly to Fibonrose on-chain profiles.
* **Active Status**: Documented blueprint with operational FastAPI runner classes.

---

## 3. Deployment & Infrastructure

The actual GCP environment configurations exist inside the `gcp-infrastructure/` directory of `municipal-dao-v`:

1. **Kubernetes manifests** (`deafauth-deployment.yaml` and `ingress-config.yaml`): Manages replication factors (3x api instances), resource boundaries (256Mi-512Mi memory), LoadBalancers, and Ingress routing rules.
2. **Terraform blueprints** (`terraform/main.tf`): Automates GKE cluster creation, Firestore instances, Redis caches, Cloud DNS managed zones, global SSL certificates, and GCS assets buckets with customized CORS policies.
