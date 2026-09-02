# Centralized Ecosystem Synchronization, Renovate Dependency Management & Release Annotation Plan
# Author: Jules, Lead Software Engineer
# Target Account Maintainer: @pinkycollie
# Created: 2026-08-09
# Status: COMPLETED

This document outlines the master blueprint for centralizing automated ecosystem synchronization, Renovate/Dependabot dependency versioning, release annotations, and accurate forward rebuilding across all repositories under the `@pinkycollie` / `Pmaster-dev` accounts.

---

## 1. Centralized Ecosystem Synchronization (Centralized Auto-Sync)

To eliminate repository drift across satellite applications (`pinksync-app`, `deafauth`, `fibonrose`) and keep them synchronized with the canonical runtime (`municipal-dao-v` and `mbtq-dev`), a centralized **Ecosystem Sync Dispatcher** is established.

### **Architecture: Repository Dispatch & Matrix Actions**
A single, centralized GitHub Actions workflow inside `Pmaster-dev/.github` triggers downstream automated synchronization across all account repositories whenever a canonical core contract, schema, or API interface is modified.

```yaml
# .github/workflows/centralized-ecosystem-sync.yml
name: Centralized Ecosystem Sync

on:
  push:
    branches: [main, master]
    paths:
      - 'audit/schema.json'
      - 'audit/component-registry.json'
      - 'script/validate-data/**'

jobs:
  dispatch_sync:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        repo:
          - 'Pmaster-dev/mbtq-dev'
          - 'Pmaster-dev/municipal-dao-v'
          - 'Pmaster-dev/NegraRosa'
          - 'Pmaster-dev/FibonRoseTrust'
          - 'Pmaster-dev/accessibility-validator'
    steps:
      - name: Trigger Remote Ecosystem Sync
        uses: peter-evans/repository-dispatch@v3
        with:
          token: ${{ secrets.ECOSYSTEM_SYNC_PAT }}
          repository: ${{ matrix.repo }}
          event-type: ecosystem-schema-updated
          client-payload: '{"ref": "${{ github.sha }}", "actor": "centralized-sync"}'
```

---

## 2. Renovate & Dependabot Automated Dependency Versioning Strategy

### **Unified Renovate Configuration (`renovate.json`)**
To standardize package versions (Node, TypeScript, `@google-cloud/firestore`, `@google-cloud/vertexai`, `ethers`, `next`, `react`) across all account repositories, a central Renovate configuration is deployed:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "config:base",
    ":preserveSemverRanges",
    ":combineCommons"
  ],
  "packageRules": [
    {
      "matchPackageNames": ["@google-cloud/*", "@ai-sdk/*"],
      "groupName": "GCP and AI SDKs",
      "automerge": true
    },
    {
      "matchPackageNames": ["react", "react-dom", "next"],
      "groupName": "Frontend Core Frameworks",
      "schedule": ["before 5am on Monday"]
    },
    {
      "matchPackageNames": ["ethers", "web3"],
      "groupName": "Web3 Blockchain Engines"
    }
  ],
  "assignees": ["pinkycollie"]
}
```

---

## 3. Release Annotations & Semantic Versioning Framework

Every release across the MBTQ ecosystem must be annotated with semantic versions and automatic Fibonrose trust checkpoints:

### **Release Annotation Format**
```
v<MAJOR>.<MINOR>.<PATCH>-mbtq.<BUILD_NUMBER>
Example: v3.2.0-mbtq.104
```

### **Automated Release Annotator Pipeline**
```yaml
name: MBTQ Release Annotator

on:
  push:
    tags:
      - 'v*.*.*'

jobs:
  annotate_release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Generate Annotated Release Notes
        uses: softprops/action-gh-release@v2
        with:
          body: |
            ## 🤟 MBTQ Ecosystem Release Annotation

            **Maintainer:** @pinkycollie
            **Canonical Core:** `municipal-dao-v` (GKE/Firestore)
            **Client State Engine:** `mbtq-dev` (Sign Visual System)
            **Security Layer:** `NegraRosa` (NFT-based identity)
            **Trust Engine:** `FibonRoseTrust` (AI Provider Verification)

            ### 🌹 Fibonrose Task Checkpoints Confirmed:
            - [x] Pre-commit linting & schema validation passed
            - [x] Zero plain text secrets in manifests
            - [x] SSRF IP-parsing filters verified

            *Automated Release Annotation for @pinkycollie*
```

---

## 4. Accurate Forward Rebuild Strategy (The Master Roadmap)

To achieve the most accurate forward rebuild without losing historical context:

1. **Phase 1: Sync to Vault & Drive (Immediate)**
   - Sync all documentation, OpenAPI specs, and reference code to @pinkycollie's Obsidian vault and Proton Drive.

2. **Phase 2: Establish the Single Canonical Monorepo (`Pmaster-dev/mbtq-dev`)**
   - Import active GKE backend services from `municipal-dao-v/services/` (`deafauth-api`, `pinksync-middleware`, `360magicians-vertex-ai`, `mbtq-platform`, `mbtquniverse-dao`).
   - Retain the **Sign Visual System** React state engine from `mbtq-dev/client/`.
   - Embed **NegraRosa** NFT security logic into the `deafauth-api` profile handler.
   - Embed **FibonRoseTrust** AI taxonomy logic into the provider verification endpoints.

3. **Phase 3: Archive Historical / Messy Repositories**
   - Archive messy/historical repositories (`360-magicians` historical account, standalone `deafauth`, `pinksync-app`, `fibonrose` reference apps) after verifying all code is backed up and reflected in the central monorepo.
