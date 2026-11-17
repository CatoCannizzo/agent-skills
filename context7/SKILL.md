---
name: context7
status: beta
description: >-
  Fetches version-accurate official documentation, API signatures, and verified links
  using the Context7 MCP server (resolve-library-id and get-library-docs), local node_modules
  type declarations (.d.ts), and domain-pinned web search. Activate whenever the user asks for
  official documentation, library reference links, version-specific API usage, or invokes /context7.
---

# Context7 Documentation & Verified Link Lookup Skill

Use this skill to retrieve **version-accurate documentation, API signatures, and verified links** without hallucinating URLs or relying on outdated training weights.

---

## 1. Core Guardrails (Zero-Hallucination Policy)

1. **Never Guess URLs from Training Weights**:
   - Documentation sites restructure paths across versions. Never fabricate or guess a documentation URL path from memory.
2. **Always Check Installed Version First**:
   - Before querying documentation, read the workspace manifest (`package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`) to determine the exact installed version of the target library.
3. **Cache Results in Session Artifact**:
   - Once documentation or links are fetched, record the verified URLs and key signatures in a session reference artifact so redundant network/MCP calls are not repeated.

---

## 2. Step-by-Step Lookup Workflow

### Step 1: Inspect Local Version & Type Definitions (`0 Network Latency`)
1. Read `package.json` (or language equivalent) to confirm the exact installed version (e.g., `@apollo/client: ^4.3.5`, `next: 16.3.8`).
2. Check if the package ships local docs or TypeScript declarations on disk:
   - Bundled docs (e.g., `node_modules/next/dist/docs/`).
   - Target symbol `.d.ts` file (via `grep_search` or `read_file` on the specific export).
3. Always include a clickable `file://` link to the local `.d.ts` signature or bundled doc so the user can open the exact installed definition in their IDE.

### Step 2: Query Context7 MCP (Primary External Source)
If the Context7 MCP server (`context7`) is available in your toolset:
1. **Resolve the Library ID**:
   - Call `resolve-library-id` with the package name (e.g., `libraryName: "vitest"`, `"@apollo/client"`, `"next"`).
   - Select the canonical official repository/docs match (and version-specific ID if available).
2. **Fetch Focused Documentation**:
   - Call `get-library-docs` (or `query-docs`) using the resolved `context7CompatibleLibraryID` and a focused `topic` string matching the user's question (e.g., `topic: "MockedProvider testing"`, `topic: "client preset graphql"`).

### Step 3: Domain-Pinned Web Search Fallback (Verified URLs Only)
If you need direct clickable web links or a package is not indexed in Context7:
1. Call `search_web` with:
   - `query`: `"<library> <version> <API/hook/method name>"`
   - `domain`: Pinned to the library's official documentation domain (e.g., `apollographql.com`, `vitest.dev`, `testing-library.com`, `react.dev`, `nextjs.org`, `the-guild.dev`).
2. Output **only** the exact URLs returned in `search_web` citations—never alter or extrapolate URL subpaths.

---

## 3. Output Format

Present documentation results in a concise, scannable block:

1. **Installed Version & Local Definition**:
   - Package & Version from manifest (e.g., `@apollo/client v4.3.5`)
   - Clickable `file://` link to the local `.d.ts` signature or bundled guide
2. **Official Documentation & Verified Links**:
   - Verified URL(s) from Context7 / `search_web`
   - **What to read on this page**: 1-line pointer to the specific section, prop, or hook parameter
   - **Version Caveat**: Any breaking change between legacy versions and the installed version
3. **Minimal API Signature / Usage Summary**:
   - Concise summary of parameters, return types, and required imports (if invoked from `/coding-tutor` Mode 7, keep examples domain-decoupled so the user's step is not spoiled).
