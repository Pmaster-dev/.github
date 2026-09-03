# MBTQ / 360Magicians Full Ecosystem Canonical Candidates
# Created: 2026-08-09
# Status: COMPLETED

This report establishes the authoritative (canonical) definitions of every major system, configuration, and interface within the connected available source repositories.

---

## 1. Live Public Production Domain Gateway

* **Canonical Candidate**: **`vr4deaf.org`**
* **Evidence**: `vr4deaf.org` is the **ONLY active, production-ready live public domain in the real world**. Custom domain aliases (`mbtq.dev`, `360magicians.com`, `pinksync.io`, `mbtquniverse.com`, `deafauth.mbtq.dev`) are inactive/gone.
* **GitHub Static Fallbacks**: `https://Pmaster-dev.github.io/<repo>`, raw GitHub API endpoints, and static `src` code references.
* **Verdict**: Authoritative Live Public Gateway.

---

## 2. Core Ecosystem Configuration: `mbtq-ecosystem`

* **Canonical Candidate**: `ecosystem-architecture/mbtq-ecosystem.yaml` in the **`municipal-dao-v`** repository.
* **Evidence**: This is the configuration mapping GKE replica bounds (5x Vertex AI hub, 3x PinkSync middleware, 4x platform servers), GCR container pathways, and environment contexts.
* **Alternatives / Duplicates**: None.
* **Verdict**: Authoritative Source of Truth.

---

## 3. DeafAUTH (Identity Cortex)

* **Canonical Candidate (Backend & Profiles API)**: `services/deafauth-api/src/server.ts` in the **`municipal-dao-v`** repository.
* **Evidence**: Implements actual Firestore/NoSQL queries, JWT logins, domain registrations, and stats counters.
* **Canonical Candidate (Client React SDK)**: `lib/deafauth-sdk.ts` in the **`municipal-dao-v`** repository.
* **Evidence**: Defines the active React SDK, `useDeafAUTH` hook, login popup event listener framework, and domain-registration connections.
* **Alternatives / Duplicates**:
  - `deafauth` (the repository): Extensively specified reference App (Next.js/Supabase/Postgres relational database).
  - `deaf-first-platform/Services/deafauth`: Abstract OpenAPI definitions.
* **Verdict**: GKE service code inside `municipal-dao-v` and `lib/deafauth-sdk.ts` are the active candidates.

---

## 4. Inclusive Security: NegraRosa

* **Canonical Candidate**: **`NegraRosa`** repository.
* **Evidence**: Provides NFT-based identity attestation ("I AM WHO I AM" token), zero-custody credential sharing, and append-only audit logging.
* **Verdict**: Authoritative Security Framework.

---

## 5. Universal Verification: FibonRoseTrust

* **Canonical Candidate**: **`FibonRoseTrust`** repository.
* **Evidence**: AI-powered universal professional verification engine authenticating deaf community service providers, interpreters, and capabilities.
* **Verdict**: Authoritative Trust & Matching Engine.

---

## 6. PinkSync (Accessibility Engine)

* **Canonical Candidate (Transformation Logic)**: `services/pinksync-middleware/src/accessibility-transformer.ts` in the **`municipal-dao-v`** repository.
* **Evidence**: Fully implements offline sync queues, web/mobile widgets, and Vertex AI translations.
* **Alternatives / Duplicates**:
  - `pinksync-app` (the repository): Reference Next.js backend and Chrome extension configurations.
  - `deaf-first-platform/Services/pinksync`: OpenAPI v3.1 schema.
* **Verdict**: `AccessibilityTransformer` in `municipal-dao-v` is the canonical implementation.

---

## 7. 360Magicians AI Core

* **Canonical Candidate**: `services/360magicians-vertex-ai/src/multi-domain-ai.ts` in the **`municipal-dao-v`** repository.
* **Evidence**: Coded wrapper utilizing Google's native `@google-cloud/vertexai` SDK and Gemini-1.5-pro models to process localized domains (creative, design, content, accessibility).
* **Alternatives / Duplicates**:
  - `deaf-first-platform/Services/magicians`: OpenAPI specifications.
* **Verdict**: `MultiDomainVertexAI` class inside `municipal-dao-v` is the canonical engine.

---

## 8. Fibonrose Task Validator

* **Canonical Candidate**: `fibonrose/fibonrose-validator.ts` in the **`mbtq-dev`** repository.
* **Evidence**: Advanced TypeScript module establishing Fibonacci difficulty sequences, milestone confirmations, and GitHub comment parsers. Fully tested (100% test coverage verified).
* **Alternatives / Duplicates**:
  - `trust-engine` repository: Contains boilerplate TypeScript template files.
  - `fibonrose` repository: Reference dashboard files containing local mock states.
* **Verdict**: `fibonrose-validator.ts` inside `mbtq-dev` is the canonical validation candidate.

---

## 9. PinkFlow MicroVM Sandbox

* **Canonical Candidate**: `pinkflow/container` in the **`pinkflow`** repository.
* **Evidence**: Blueprint layout defining MicroVM Firecracker execution, FastAPI runners, Python subprocess runs, and Polygon proof anchors.
* **Verdict**: Authoritative Sandbox Candidate.
