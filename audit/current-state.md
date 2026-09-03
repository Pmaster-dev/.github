# MBTQ / 360Magicians Full Ecosystem Current State
# Created: 2026-08-09
# Status: ACTIVE (Audited Real-World Status)

## Executive Summary

As of August 2026, the connected MBTQ / 360Magicians ecosystem has its codebases fully intact in GitHub repositories under `Pmaster-dev`.

**Real-World Production Live Domain Status**:
* **`vr4deaf.org`**: **THE ONLY ACTIVE, PRODUCTION-READY LIVE PUBLIC DOMAIN IN THE REAL WORLD**. Serves as the primary operational gateway for vocational rehabilitation, deaf learners, business development, and funding justifications.
* **Custom Domain Aliases (`mbtq.dev`, `360magicians.com`, `pinksync.io`, `mbtquniverse.com`, `deafauth.mbtq.dev`)**: Custom domain registrations are inactive/gone.
* **GitHub Static & Endpoint Fallbacks**: On GitHub, all working endpoints fall back to GitHub Pages static hosts (`https://Pmaster-dev.github.io/<repo>`), raw GitHub API endpoints, local GKE ingress IP configurations in `municipal-dao-v`, and static `src` code references.

---

## 1. Active Services & Implementations (Today)

The following components represent the actively running runtime services of the ecosystem:

### 🌐 VR4Deaf Vocational Rehabilitation Portal
* **Live Domain**: `https://vr4deaf.org` (**Live & Operational**)
* **Technology**: Next.js, Supabase, DeafAUTH SDK, Business Formation API.
* **Role**: Primary real-world production portal providing vocational rehabilitation, IEP pods, and accommodation tracking for deaf clients.

### 🔐 DeafAUTH (Identity Cortex)
* **Location**: `services/deafauth-api/src/server.ts` in `municipal-dao-v`
* **Static Fallback**: `https://Pmaster-dev.github.io/deafauth`
* **Technology**: Node.js, Express, Helmet, CORS, Firestore ("deafauth-profiles"), Redis ("deafauth-cache"), GCP Pub/Sub.
* **Role**: Universal identity system managing profiles containing user identity metadata, verification levels, preferred sign languages, and visual preferences.

### 🔄 PinkSync Middleware (Accessibility Engine)
* **Location**: `services/pinksync-middleware/src/accessibility-transformer.ts` in `municipal-dao-v`
* **Static Fallback**: `https://Pmaster-dev.github.io/pinksync-app`
* **Technology**: TypeScript, Service Workers, offline caches.
* **Role**: Accessibility middleware transforming incoming content payloads into visual reading hierarchies, tactile patterns, sign language metaphors, or high-contrast styles.

### 🎨 360Magicians AI Hub (Vertex AI Multi-Domain)
* **Location**: `services/360magicians-vertex-ai/src/multi-domain-ai.ts` in `municipal-dao-v`
* **Technology**: `@google-cloud/vertexai`, Gemini-1.5-pro.
* **Role**: Configures specialized sub-AI systems (Creative, Design, Content, Accessibility) using Google's generative models.

### 🏠 MBTQ Platform (Deaf-First UI Platform)
* **Location**: `services/mbtq-platform/src/v0-gemini-bridge.ts` in `municipal-dao-v`
* **Static Fallback**: `https://Pmaster-dev.github.io/mbtq-dev`
* **Technology**: `@ai-sdk/google`, Gemini-1.5-pro, Google Studio Proxy.
* **Role**: Bridges interactive design prompts with generative models, supported by the **Sign Visual System** React frontend suite in `mbtq-dev`.

### 🌌 MBTQ Universe DAO (Governance & Staking)
* **Location**: `services/mbtquniverse-dao/src/web3-staking-showcase.ts` in `municipal-dao-v`
* **Static Fallback**: `https://Pmaster-dev.github.io/municipal-dao-v`
* **Technology**: Next.js, WebSockets, framer-motion, ethers.js.
* **Role**: Implements real-time proposal viewing, animated voting charts, quorum trackers, and Web3 staking dashboards.

---

## 2. Satellite & Security Tooling

* **`NegraRosa`**: NFT-based identity ("I AM WHO I AM" token) and zero-custody credential sharing.
* **`FibonRoseTrust`**: AI-powered universal professional verification engine for interpreters and deaf community service providers.
* **`fibonrose/` (in `mbtq-dev`)**: Fibonrose Task Validator evaluating Fibonacci complexity levels (0-9) via GitHub issue comments.
* **`pinkflow/`**: Ephemeral MicroVM (Firecracker) sandboxing for partner integration code verification.
