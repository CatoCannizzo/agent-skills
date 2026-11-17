# Custom Agent Skills (Medallion Architecture)

Personal repository of custom AI agent skills for Google Antigravity (`~/.gemini/config/skills`).

---

## 🏅 Skill Medallion Architecture

Because Antigravity's skill loader scans `skills/<skill-name>/SKILL.md` one level deep, all active skills live in `skills/<skill-name>/` while being categorized and tracked across three maturity tiers via:
1. **`tier: bronze | silver | gold`** in each skill's YAML frontmatter
2. **The Medallion Registry Table** below

### Tier Definitions & Graduation Criteria

| Tier | Stage | Criteria to Enter / Graduate |
| :--- | :--- | :--- |
| **🥉 Bronze** | **Draft / Ideation** | Initial prompt design or rough concept. Has **0–1 live runs**; edge cases, token efficiency, and failure modes are not yet validated. |
| **🥈 Silver** | **Validated / Iterating** | Used in **2+ real coding sessions**. Core workflow works reliably; actively refining triggers, guardrails, and output structure based on session transcripts. |
| **🥇 Gold** | **Polished / Production** | Battle-tested across multiple sessions, audited against conversation transcripts for **token efficiency**, includes strict guardrails, anti-patterns, and multi-mode workflows. |

---

## 📊 Current Skill Catalog

| Skill | Medallion Tier | Path | Status & Notes |
| :--- | :--- | :--- | :--- |
| **`coding-tutor`** | 🥇 **Gold** | [`coding-tutor/SKILL.md`](./coding-tutor/SKILL.md) | Socratic coding mentor with 6 modes (Syntax, Elaborate, Check, Answer, Isomorphic + Non-Examples, Faded Skeleton), JIT file reading, Repetitive Work Sectioning ("Prove 1–3, Automate Rest"), Pre-Flight Calibration, Predict-Before-Run, and Post-Step Synthesis. |
| **`query-testing`** | 🥈 **Silver** | [`query-testing/SKILL.md`](./query-testing/SKILL.md) | Proactive GraphQL & REST query verification workflows for VS Code REST Client and Postman. |
| **`project-capsule-generator`** | 🥉 **Bronze** | [`project-capsule-generator/SKILL.md`](./project-capsule-generator/SKILL.md) | Initial draft for extracting database, pipeline, and architecture metrics into portfolio capsules. Untested in live sessions. |

---

## 🔄 Workflow: Promoting & Testing a Skill

1. **Create in Bronze (`tier: bronze`)**:
   - Create `<new-skill>/SKILL.md` with `tier: bronze` in the YAML frontmatter and add it to the Bronze section of this table.
2. **Test & Audit (Bronze → Silver)**:
   - Run the skill in a real workspace task (`/<new-skill>`).
   - Review the conversation transcript (`transcript.jsonl`) to spot where the agent misunderstood instructions, needed extra prompting, or wasted tokens.
   - Update `tier: silver` in `SKILL.md` and commit the diff.
3. **Polish & Optimize (Silver → Gold)**:
   - Eliminate upfront context bloat (use Just-In-Time file inspection and on-demand reference generation).
   - Add contrastive non-examples (`❌` vs `✅`) and edge-case guardrails.
   - Update `tier: gold` in `SKILL.md` and commit the diff.
