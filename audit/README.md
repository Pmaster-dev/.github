# MBTQ / 360Magicians Full Source Collection & Architecture Audit

This directory contains the complete architectural audit, source inventory, component registry, and security findings for the connected **MBTQ / 360Magicians** full-stack ecosystem.

## 📂 Deliverables Registry

* **[MASTER-AUDIT.md](MASTER-AUDIT.md)**: The master report detailing answers to the 16 core questions, current status, and proposed consolidation pathways.
* **[source-inventory.yaml](source-inventory.yaml)**: Complete mapping of source, reference, and deployment repositories.
* **[component-registry.yaml](component-registry.yaml)**: Precise specifications, APIs, dependencies, and confidence scores for every discovered system.
* **[architecture-graph.yaml](architecture-graph.yaml)**: L0-L10 layering classification mapping visual-first and trust principles.
* **[dependency-map.yaml](dependency-map.yaml)**: Direct and indirect coupling relationships across microservices.
* **[domain-map.yaml](domain-map.yaml)**: Host domain scopes mapping services and code repos.
* **[historical-timeline.yaml](historical-timeline.yaml)**: Chronological milestones charting the platform's evolutionary transitions.
* **[current-state.md](current-state.md)**: active deployment configurations, Firestore models, and GKE states.
* **[conflicts.md](conflicts.md)**: Deep-dive into naming collisions, port overlaps, and mismatched security schemes.
* **[duplicates.md](duplicates.md)**: Duplicated auth modules, staking frontends, and database interfaces.
* **[architecture-debt.md](architecture-debt.md)**: Labeled backlog of architectural and security debt items categorized as P0-P3.
* **[accessibility-audit.md](accessibility-audit.md)**: Verifies visual-first and sign-language claims against active code bases.
* **[security-findings.md](security-findings.md)**: Documented analysis of SSRF protections and developer-drift CORS permissions.
* **[canonical-candidates.md](canonical-candidates.md)**: Declares the authoritative source of truth for all modules.

---

## 🛠️ Validation

All YAML schemas in this directory are syntactically validated and parsed using active compiler pipelines.
