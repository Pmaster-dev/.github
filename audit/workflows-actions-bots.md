# MBTQ / 360Magicians Ecosystem Workflows, Bots, Copilot & Branch Sync Audit
# Created: 2026-08-09
# Status: COMPLETED

This report audits the GitHub Actions workflows, Copilot guidelines, automated bot triggers, and branch synchronization mechanisms across the `Pmaster-dev` account.

---

## 1. GitHub Copilot & AI Agent Guidelines

### **Copilot Instructions**
* **Location**: `.github/co-pilot-instruction.md` in `deaf-first-platform`
* **Purpose**: Provides baseline project guidelines for GitHub Copilot when generating code snippets or suggesting PR reviews:
  - **Code Style**: Mandatory semantic HTML5 elements (`<header>`, `<main>`, `<section>`, `<article>`), modern ES6+ JS features.
  - **Naming Conventions**: `PascalCase` for React components/interfaces, `camelCase` for functions/variables, `_` prefix for private members, `ALL_CAPS` for constants.
  - **Quality & Accessibility**: Mandatory error handling for API calls, explicit ARIA labels, and explanatory comments for complex logic.

### **Agent System Instructions**
* **Location**: `.github/agents.md` in `mbtq-dev` and `agent-config/` in `mbtq-dev`
* **Purpose**: Configures dynamic agent selection, execution rules (`fail_closed: true`, prohibiting direct execution on `main`), and Fibonrose checklist generation.

---

## 2. Automated Bots & Triage Systems

### **Dependabot (Automated Dependency Updates)**
* **Active Repositories**: `.github`, `mbtq-dev`, `deaf-first-platform`, `deafauth`, `accessibility-validator`.
* **Config**: `.github/dependabot.yml` configured to scan ecosystem npm, pnpm, and GitHub Actions dependencies weekly/daily.

### **Auto-Assign Bot**
* **Location**: `.github/auto_assign.yml` and `.github/workflows/auto-assign-issues.yml` in `.github`
* **Trigger**: `issues: [opened]`, `pull_request: [opened]`
* **Role**: Automatically assigns new issues and pull requests to designated maintainers.

### **Labeler & Triage Bot**
* **Location**: `.github/labeler.yml` and `.github/workflows/labeler-triage.yml`, `label-feature.yml`, `label-support.yml`
* **Trigger**: `issues: [opened, edited]`, `pull_request: [opened]`
* **Role**: Categorizes incoming issues and pull requests based on body keywords (e.g. `feature`, `support`, `bug`) and applies appropriate triage labels.

### **Stale Bot**
* **Location**: `.github/workflows/stale.yml` in `.github` and `mbtq-dev`
* **Role**: Automatically marks inactive issues and PRs as stale and closes them after a configurable grace period.

---

## 3. Branch Synchronization Mechanisms

### **1. Starter Workflows GHES Sync**
* **Location**: `script/sync-ghes/index.ts` & `.github/workflows/sync-ghes.yaml` in `.github`
* **Trigger**: Pushes to `main` branch
* **Logic**:
  - Checks if a remote `ghes` (GitHub Enterprise Server) branch exists.
  - Filters out starter workflows containing unsupported third-party GitHub Actions or partner-specific integrations.
  - Automatically downgrades `actions/upload-artifact@v4` and `actions/download-artifact@v4` to `v3` for compatibility with GHES environments.
  - Synchronizes compatible workflow files directly to the `ghes` branch.

### **2. Ecosystem Sync Workflow**
* **Location**: `.github/workflows/ecosystem-sync.yml` in `accessibility-validator`
* **Trigger**: Pushes to `main` / Scheduled cron
* **Logic**: Synchronizes validation rules and shared accessibility testing schemas across peripheral repos.

### **3. DeafAUTH Schema Sync**
* **Location**: `.github/workflows/sync.yml` in `deafauth`
* **Trigger**: Workflow dispatch / upstream changes
* **Logic**: Syncs identity schema updates across client SDKs.

---

## 4. Specialized Ecosystem Workflows

### **Fibonrose Task Validator Workflow**
* **Location**: `.github/workflows/fibonrose-validator.yml` in `mbtq-dev`
* **Trigger**: `issue_comment: [created]`
* **Role**: Listens for confirmation comments (e.g., `Confirm checkpoint 1: commit abc123`), parses evidence, updates the Fibonrose task checklist, and posts visual progress reports.

### **Sovereign Build Workflow**
* **Location**: `Mbtq-sovereign.yml` in `deaf-first-platform`
* **Trigger**: `push: [main, master]`
* **Role**: Anti-vendor-lock build workflow. Executes `./scripts/strip-magic.sh` to scrub vendor telemetry, compiles sovereign artifacts locally in the runner, and deploys using `vercel deploy --prebuilt --prod`.

### **Workflow Dataset Validation**
* **Location**: `.github/workflows/validate-data.yaml` in `.github`
* **Trigger**: `push`, `pull_request`
* **Role**: Runs `script/validate-data/index.ts` to ensure all starter workflow JSON properties and YAML descriptors are valid and error-free.
