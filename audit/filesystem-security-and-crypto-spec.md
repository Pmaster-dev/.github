# 🔒 MBTQ Ecosystem File System Access Tracking, Command Execution & Cryptographic Spec
# Target Maintainer: @pinkycollie
# Created: 2026-08-09
# Status: COMPLETED

This document defines the technical specification for **File System Access Tracking (`fs`)**, **Format Validation (`fmt`)**, **Internal Command Execution Control (`w internal cmd`)**, **Encryption & Decryption Pipelines (`enc n dec`)**, and **Special Character Escaping (`%?&~[]<>()`)** across the MBTQ / 360Magicians ecosystem.

---

## 1. File System Access Tracking (`fs`) & Format Control (`fmt`)

To track file system modifications, prevent path traversal attacks, and ensure format compliance:

### **Access Tracking & Traversal Guards**
1. **Path Normalization & Chroot Scoping**:
   * All file reads/writes must be resolved through `path.resolve()` and verified to reside strictly within allowed workspace boundaries.
   * Attempting to reference parent directories (`../`) or absolute paths (`/etc/passwd`, `/tmp`) outside the root is blocked by the path guard:
     ```typescript
     function validatePathGuard(filePath: string, allowedRoot: string): string {
       const resolved = path.resolve(allowedRoot, filePath);
       if (!resolved.startsWith(path.resolve(allowedRoot))) {
         throw new Error(`Security Violation: Path traversal blocked - ${filePath}`);
       }
       return resolved;
     }
     ```
2. **Format Enforcement (`fmt`)**:
   * **JSON/YAML**: Validated via strict JSON schemas (`schema.json`) and YAML parsers prior to file persistence.
   * **TypeScript/JavaScript**: Formatted via Prettier/ESLint rules defined in `.eslintrc.json`.

---

## 2. Internal Command Execution Control (`w internal cmd`)

When internal CLI commands (such as `vercel build`, `strip-magic.sh`, `git`, or `deno run`) are spawned by services or PMaster pipelines:

### **Execution Principles**
* **Safe Subprocess Spawning**: Use parameterized arrays (`execFile` / `spawn`) rather than raw string shell invocation (`exec`) to eliminate command injection.
* **Env Isolation**: Strip environment variables containing raw tokens before spawning third-party child processes.
* **Timeout & Resource Cgroups**: Impose strict execution timeouts (maximum 30s) and memory caps (512MB via Firecracker/cgroups in PinkFlow).

---

## 3. Encryption & Decryption Spec (`enc n dec`)

The ecosystem employs a dual AES-256-GCM / Web3 cryptographic model:

### **Data at Rest & Token Signing**
1. **AES-256-GCM Encryption**:
   * Sensitive profile payload fields (PII, accommodation records) are encrypted using AES-256-GCM with a unique 96-bit initialization vector (IV) and authentication tag.
     ```typescript
     import crypto from "crypto";

     export function encryptPayload(data: string, secretKey: Buffer): { ciphertext: string; iv: string; tag: string } {
       const iv = crypto.randomBytes(12);
       const cipher = crypto.createCipheriv("aes-256-gcm", secretKey, iv);
       let encrypted = cipher.update(data, "utf8", "hex");
       encrypted += cipher.final("hex");
       const tag = cipher.getAuthTag().toString("hex");
       return { ciphertext: encrypted, iv: iv.toString("hex"), tag };
     }

     export function decryptPayload(ciphertext: string, secretKey: Buffer, iv: string, tag: string): string {
       const decipher = crypto.createDecipheriv("aes-256-gcm", secretKey, Buffer.from(iv, "hex"));
       decipher.setAuthTag(Buffer.from(tag, "hex"));
       let decrypted = decipher.update(ciphertext, "hex", "utf8");
       decrypted += decipher.final("utf8");
       return decrypted;
     }
     ```
2. **DeafAUTH Token Signing**:
   * Tokens are signed using asymmetric Ed25519 keys or HMAC-SHA256 signatures validated via Redis caches.

---

## 4. Special Character Sanitization & Escaping (`%?&~[]<>()`)

Special characters in user inputs, search queries, webhook parameters, and prompt injections must be escaped before processing:

### **Character Escaping Rules**
| Special Character | Risk Vector | Sanitization / Escaping Method |
|---|---|---|
| `%` | URL Percent-encoding attacks / Format specifiers | Sanitize via `encodeURIComponent()` and strip unescaped `%` in SQL/NoSQL filters |
| `?`, `&` | Query parameter pollution / SSRF manipulation | Strict URL parsing using `new URL()` and URLSearchParams validation |
| `~` | Shell home directory expansion | Escape in CLI arguments and strip from file paths |
| `[` `]` | ReDoS regex injection / Array parameter smuggling | Escape square brackets in search queries and validate type schemas with Zod |
| `<` `>` | Cross-Site Scripting (XSS) / HTML Injection | HTML entity encoding (`&lt;` and `&gt;`) using DOMPurify / React auto-escaping |
| `(` `)` | Function invocation injection / SQL subquery injection | Escape in shell arguments and parameterized query bindings |

---

## 5. Summary Matrix for PMaster Execution

| Security Category | Implementation Rule | Active Location / Guard |
|---|---|---|
| **Path Guard (`fs`)** | Chroot boundary check via `path.resolve` | `server/src/utils/ssrfAgent.ts` & `validate-data` |
| **Cmd Control (`w internal cmd`)** | Array-based parameter spawning with timeouts | `Mbtq-sovereign.yml` & `pinkflow/container` |
| **Encryption (`enc n dec`)** | AES-256-GCM for PII + Ed25519 for DeafAUTH | `services/deafauth-api/src/server.ts` |
| **Sanitization (`%?&~[]<>()`)** | Entity encoding + encodeURIComponent + Zod schemas | `client/src/components/SignVisualSystem` & Express middleware |
