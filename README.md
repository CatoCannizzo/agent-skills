# Custom Agent Skills

Personal repository of global AI agent skills for Google Antigravity (`~/.gemini/config/skills`), organized by a **Software Release Lifecycle** (`draft` → `beta` → `stable` → `deprecated`).

---

## 🚀 Skill Release Lifecycle

All active global skills live one level deep (`<skill-name>/SKILL.md`) for Antigravity's automatic skill discovery and declare their maturity via `status: draft | beta | stable | deprecated` in their YAML frontmatter.

### Lifecycle Stages & Promotion Criteria

| Status | Stage | Criteria to Enter / Promote |
| :--- | :--- | :--- |
| **`draft`** | **Ideation / Untested** | Initial prompt design or rough concept. Has **0–1 live runs**; edge cases, token efficiency, and failure modes are not yet validated. |
| **`beta`** | **Validated / Iterating** | Used in **2+ real coding sessions**. Core workflow works reliably; actively refining triggers, guardrails, and output structure based on session transcripts. |
| **`stable`** | **Production-Ready** | Battle-tested across multiple sessions, audited against conversation transcripts (`transcript.jsonl`) for **token efficiency**, includes strict guardrails, contrastive non-examples (`❌` vs `✅`), and multi-mode workflows. |
| **`deprecated`** | **Retired / Superseded** | Replaced by a newer skill, built-in capability, or moved to a workspace-specific `.agents/skills/` directory. |

---

## 📊 Global Skill Catalog

| Skill | Status | Path | Summary & Capabilities |
| :--- | :--- | :--- | :--- |
| **`coding-tutor`** | `stable` | [`coding-tutor/SKILL.md`](./coding-tutor/SKILL.md) | Socratic coding mentor with 6 modes (Syntax, Elaborate, Check, Answer, Isomorphic + Non-Examples, Faded Skeleton), JIT file reading, Repetitive Work Sectioning ("Prove 1–3, Automate Rest"), Pre-Flight Calibration, Predict-Before-Run, and Post-Step Synthesis. |
| **`project-capsule-generator`** | `draft` | [`project-capsule-generator/SKILL.md`](./project-capsule-generator/SKILL.md) | Initial draft for extracting database, pipeline, and architecture metrics into standardized portfolio project capsules. |

*(Note: Project-specific skills, such as `query-testing` for `real-estate-map`, live inside their respective workspace `.agents/skills/` directories rather than the global config.)*

---

## 🔄 Workflow: Auditing & Promoting a Skill

1. **Author as `draft`**:
   - Create `<new-skill>/SKILL.md` with `status: draft` in the YAML frontmatter.
2. **Validate in Live Sessions (`draft` → `beta`)**:
   - Run the skill in a real workspace task (`/<new-skill>`).
   - Inspect the conversation transcript (`transcript.jsonl`) to identify where the agent needed extra prompting, misunderstood boundaries, or made redundant tool calls.
   - Update to `status: beta`.
3. **Token & Pedagogy Audit (`beta` → `stable`)**:
   - Eliminate upfront context bloat (enforce Just-In-Time file inspection and on-demand reference generation).
   - Add contrastive non-examples (`❌ DON'T` vs `✅ DO`) and explicit edge-case guardrails.
   - Update to `status: stable` and commit the diff.
