# MBTQ / 360Magicians Full Ecosystem Canonical Candidates
# Created: 2026-08-09
# Status: COMPLETED

This report establishes the authoritative (canonical) definitions of every major system, configuration, and interface within the connected available source repositories.

---

## 1. Core Ecosystem Configuration: `mbtq-ecosystem`

* **Canonical Candidate**: `ecosystem-architecture/mbtq-ecosystem.yaml` in the **`municipal-dao-v`** repository.
* **Evidence**: This is the only configuration mapping GKE replica bounds (5x Vertex AI hub, 3x PinkSync middleware, 4x platform servers), GCR container pathways, and exact environment contexts.
* **Alternatives / Duplicates**: None.
* **Verdict**: Authoritative Source of Truth.

---

## 2. DeafAUTH (Identity Cortex)

* **Canonical Candidate (Backend & Profiles API)**: `services/deafauth-api/src/server.ts` in the **`municipal-dao-v`** repository.
* **Evidence**: Implements actual Firestore/NoSQL queries, JWT logins, domain registrations, and stats counters.
* **Canonical Candidate (Client React SDK)**: `lib/deafauth-sdk.ts` in the **`municipal-dao-v`** repository.
* **Evidence**: Defines the active React SDK, `useDeafAUTH` hook, login popup event listener framework, and domain-registration connections.
* **Alternatives / Duplicates**:
  - `deafauth` (the repository): Extensively specified but operates as an older reference App (Next.js/Supabase/Postgres relational database).
  - `deaf-first-platform/Services/deafauth`: Abstract OpenAPI definitions.
* **Verdict**: GKE service code inside `municipal-dao-v` is the active, running candidate.

---

## 3. PinkSync (Accessibility Engine)

* **Canonical Candidate (Transformation Logic)**: `services/pinksync-middleware/src/accessibility-transformer.ts` in the **`municipal-dao-v`** repository.
* **Evidence**: Fully implements offline sync queues, web/mobile widgets, and Vertex AI translations.
* **Alternatives / Duplicates**:
  - `pinksync-app` (the repository): Outdated reference Next.js backend and Chrome extension configurations.
  - `deaf-first-platform/Services/pinksync`: OpenAPI v3.1 schema.
* **Verdict**: `AccessibilityTransformer` in `municipal-dao-v` is the canonical implementation.

---

## 4. 360Magicians AI Core

* **Canonical Candidate**: `services/360magicians-vertex-ai/src/multi-domain-ai.ts` in the **`municipal-dao-v`** repository.
* **Evidence**: Coded wrapper utilizing Google's native `@google-cloud/vertexai` SDK and Gemini-1.5-pro models to process localized domains (creative, design, content, accessibility).
* **Alternatives / Duplicates**:
  - `deaf-first-platform/Services/magicians`: OpenAPI specifications.
* **Verdict**: `MultiDomainVertexAI` class inside `municipal-dao-v` is the canonical engine.

---

## 5. Fibonrose Task Validator

* **Canonical Candidate**: `fibonrose/fibonrose-validator.ts` in the **`mbtq-dev`** repository.
* **Evidence**: Advanced TypeScript module establishing Fibonacci difficulty sequences, milestone confirmations, and GitHub comment parsers. Fully tested (100% test coverage verified).
* **Alternatives / Duplicates**:
  - `trust-engine` repository: Contains boilerplate TypeScript template files.
  - `fibonrose` repository: Reference dashboard files containing local mock states.
* **Verdict**: `fibonrose-validator.ts` inside `mbtq-dev` is the canonical validation candidate.

---

## 6. PinkFlow MicroVM Sandbox

* **Canonical Candidate**: `pinkflow/container` in the **`pinkflow`** repository.
* **Evidence**: Blueprint layout defining MicroVM Firecracker execution, FastAPI runners, Python subprocess runs, and Polygon proof anchors.
* **Alternatives / Duplicates**: None.
* **Verdict**: Authoritative Candidate.
