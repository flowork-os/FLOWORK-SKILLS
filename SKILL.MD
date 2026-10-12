---
name: "sovereign_skills_registry_radar"
title: "Flowork OS Sovereign Skills Registry & Dual-Wing Skill Radar Architecture"
version: "2.1.0"
description: "Authoritative architectural specification for on-demand modular skills, Dual-Wing trigger radar, exclusion wings, YAML frontmatters, and autonomous binary reconstitution."
keywords: ["skills","runbooks","radar","triggers","exclude_keywords","frontmatter","pinned_skill","modular","manifest","autonomous","self_healing","enclave","hex_cipher","exit_code_0","flowork_os","registry","provenance","polyglot","hot_reload","sovereign"]
exclude_keywords: ["monolithic_prompt", "hardcoded_instructions", "ai_slop"]
provenance: "Engineered under Sovereign Flowork OS Standard. Verified with Exit Code 0 proof."
---

# 📚 Flowork OS — Sovereign Skills Registry & Dual-Wing Skill Radar Architecture (`skills/`)

> **Sovereign Flowork OS Doctrine:** *The Micro-Kernel functions strictly as an "Eternal Blank Slate". All specialized domain expertise, Standard Operating Procedures (SOPs), and operational runbooks reside 100% outside the binary kernel within the `skills/` directory in a modular, hot-reloadable, zero-bloat architecture.*  
> **Co-authored-by:** Flowork OS <agent@floworkos.com>

---

## 📌 1. Fundamental Principles of Skill Architecture

The `skills/` directory serves as the on-demand specialized runbook repository within the Flowork OS ecosystem.
Whenever an autonomous agent receives a task requiring deep domain knowledge (e.g., Reverse Engineering, Technical SEO, Security Auditing, Multi-OS Portability Enforcement):
1. **Mandatory Inspection Reflex (`view_file`):** The agent MUST read `skills/<skill_name>/SKILL.MD` via `view_file` prior to initiating technical actions.
2. **Anti-Hallucination & Empirical Discipline:** Agents are strictly forbidden from guessing complex workflows; execution must rigorously adhere to the official runbook.
3. **Mandatory Pinned Skill (Tiers 1–4):** The agent must pin relevant skills into the active session via `skill_control(action: "pin", skill_id: "...")` before executing non-anchor tasks.

---

## 🎯 2. YAML Frontmatter Standard: Exactly 20 English Keywords

Every `SKILL.MD` file MUST feature valid YAML Frontmatter at the very top adhering to strict specification:

```yaml
---
name: "web_traffic_seo_specialist"
description: "Standard operating procedure for web traffic analysis, technical SEO auditing, search engine indexation footprinting, backlink discovery, and Core Web Vitals profiling."
keywords: ["seo","traffic","backlinks","ranking","indexing","analytics","sitemap","robots","serp","keywords","performance","lighthouse","crawling","canonical","open_graph","schema_org","json_ld","ttfb","core_web_vitals","pageviews"]
exclude_keywords: ["youtube.com", "youtube,com", "youtube", "youtu.be", "yt spy"]
provenance: "Engineered under 4-Tier Sovereign Acquisition Hierarchy. Verified with Exit Code 0 proof."
---
```

### Sovereign Standards for Skill Creation:
1. **EXACTLY 20 ENGLISH KEYWORDS (`keywords`):**
   - The `keywords` array MUST contain **EXACTLY 20 KEYWORDS** in formal English.
   - Any skill with fewer or more than 20 keywords is considered **DEFECTIVE (INVALID)** and will be rejected by the *Preflight Gatekeeper*, `skill_control`, and the *Runtime Skill Radar*!
2. **STRICT ENGLISH FOR ALL METADATA:**
   - All `keywords`, `exclude_keywords`, `name`, and `description` fields MUST be 100% formal English. Non-English markers are strictly prohibited.
3. **STRICT ENGLISH FOR BODY CONTENT:**
   - When authoring a `SKILL.MD` file, **BOTH THE METADATA AND THE ENTIRE BODY OF THE DOCUMENT MUST BE 100% STRICT ENGLISH**.
   - All sections (Overview, Standard Execution Flow, Edge Cases & Recovery, Empirical QC Exit Code 0), technical SOPs, and code examples MUST NOT contain non-English markers.
   - The global standard of Flowork OS demands universal portability so that skills can be executed reliably by any model and runtime worldwide.

---

## ⚡ 3. Dual-Wing Skill Radar Architecture (Keywords & Negative Exclusion)

To prevent **Skill Collisions** and **Context Bloat**, the *Sovereign Skill Radar* (`core/src/trigger.rs`) evaluates candidate skills using the **Dual-Wing Trigger Architecture**:

```
                              ┌────────────────────────────────────────┐
                              │       INTENT / QUERY KEYWORDS          │
                              │    (e.g., "youtube.com" vs. "seo")     │
                              └───────────────────┬────────────────────┘
                                                  │
                               [Case-Insensitive Substring Scan]
                                                  │
                         ┌────────────────────────┴────────────────────────┐
                         ▼                                                 ▼
               [Negative Exclusion Wing]                         [Positive Keyword Wing]
                `query_lower.contains(&ex)`                       `query_lower.contains(&kw)`
                         │                                                 │
               Does query match exclude?                         Does query match keyword?
               (e.g., "youtube" in SEO skill)                    (e.g., "traffic" or "ranking")
                         │                                                 │
                 ┌───────┴───────┐                                 ┌───────┴───────┐
                 │ YES           │ NO                              │ YES           │ NO
                 ▼               ▼                                 ▼               ▼
            [DISQUALIFIED]   [Pass to Positive]                [RECOMMENDED]   [PASS / IGNORE]
             Score = -1000   (Evaluate Positive Score)         (Top-3 Radar    (Score 0 / Skip)
            (Short-Circuit)                                     Banner HUD)
```

### A. Substring Matching Principle
Trigger evaluation operates via **case-insensitive substring contains** (`query.to_lowercase().contains(&kw)`):
* **Why Substring?**
  - **URLs & TLDs:** Input domains such as `example.com` or `target.org` instantly match `.com` or `domain`.
  - **Typo Tolerance:** Accidental comma typing (`youtube,com`) still resolves accurately through the substring `youtube`.
  - **Sub-paths:** Routes such as `watch?v=`, `shorts/`, or `@handle` match immediately without fragile regular expressions.

### B. Short-Circuit Negative Rejection
Negative exclusions are evaluated **FIRST** before calculating any positive keyword scores:
```rust
// 0. EXCLUSION CHECK (Short-circuit): Substring matching
let exclude_vals = skill.get("exclude_keywords")
    .or_else(|| skill.get("exclude"))
    .or_else(|| skill.get("excludes"));
if let Some(arr) = exclude_vals.and_then(|v| v.as_array()) {
    for ex in arr {
        if let Some(ex_str) = ex.as_str() {
            let ex_clean = ex_str.trim().to_lowercase();
            if !ex_clean.is_empty() && query_lower.contains(&ex_clean) {
                return -1000; // IMMEDIATE DISQUALIFICATION!
            }
        }
    }
}
```
If any exclusion keyword matches, the score instantly drops to `-1000`, disqualifying the candidate skill from radar recommendations.

### C. Concrete Collision Prevention Matrix:
* **Web Traffic SEO vs. YouTube Intelligence:**
  - `web_traffic_seo_auditor`: Contains keywords `seo`, `traffic`, `ranking`, `domain`. Declares `exclude_keywords: ["youtube.com", "youtube,com", "youtube", "youtu.be"]`.
  - When the user asks for traffic analysis of `example.com`: The SEO skill is recommended.
  - When the user queries `youtube.com/watch?v=123`: The SEO skill is **INSTANTLY DISQUALIFIED**, cleanly passing execution to specialized YouTube intelligence tools (`youtube_spy_*`).

---

## 📂 4. Canonical Directory Structure for Modular Skills

Every skill resides in its isolated directory:

```
skills/
└── <skill_name>/
    ├── SKILL.MD       # (Mandatory) YAML Frontmatter (20 keywords) + Complete SOP
    ├── scripts/       # (Optional) Automation helper scripts / tooling
    ├── templates/     # (Optional) Code templates and schemas
    └── resources/     # (Optional) Reference data, offline dictionaries, CVE matrices
```

---

## 🏛️ 5. 4-Tier Acquisition Hierarchy & Pinned Skill Lifecycle

1. **Tier 1 (Local Workspace / Installed Skills):** Highest priority. The radar scans the local `skills/` directory first.
2. **Tier 2 (Official Flowork OS Registry):** If fewer than 3 local candidates exist, the radar queries the official `flowork-os/FLOWORK-SKILLS` catalog.
3. **Tier 3 (Model Context Protocol / Community):** External MCP skill adapters.
4. **Tier 4 (Zero-Precedent Sovereign Crafting):** If no matching skill exists, the agent crafts a new skill from scratch with exactly 20 English keywords via `skill_control(action: "create")`.

### Pinned Skill Lifecycle Rules:
* The agent must inspect candidate runbooks via `view_file` prior to pinning.
* The active skill is pinned via `skill_control(action: "pin", skill_id: "<id>")`.
* Once pinned, the skill SOP is dynamically injected into `<PINNED_ACTIVE_SKILL>` on subsequent turns.
* Upon task completion, the agent MUST unpin via `skill_control(action: "unpin")`.

---

## 🚀 6. Mandatory Official GitHub Contribution Post-Verification (Exit Code 0)

Whenever an agent engineers or updates a Skill:
1. **Self-Verification (Exit Code 0):** The agent must test all scripts, SOPs, and commands until verified with terminal Exit Code 0.
2. **Mandatory Upload to Official Registry:** Following empirical validation, the agent **MUST PUBLISH AND UPLOAD THE SKILL TO THE OFFICIAL GITHUB REGISTRY** (`flowork-os/FLOWORK-SKILLS`) using:
   ```bash
   skill_control(action: "publish", skill_id: "<skill_name>", notes: "feat: add <skill_name> sovereign runbook")
   ```
3. **Attestation Guard (Hash Integrity):** The kernel binary automatically validates local binary and core UI SHA-256 hashes against GitHub `release_checksums.json`. If hashes are tampered or unauthorized, uploads are immediately blocked.

---

## 🔄 7. Autonomous Binary Self-Healing Reconstitution

This authoritative governance runbook (`skills/SKILL.MD`) is cryptographically sealed inside the **Cryptographic Bytecode Enclave** of the `flowork` / `x-flow` kernel binary:
* **Fresh Installation:** The compiled binary automatically generates `skills/SKILL.MD` if the `skills/` directory does not contain it.
* **Accidental Deletion:** If `skills/SKILL.MD` is deleted by user or external processes, the `flowork` / `x-flow` kernel binary detects the absence during runtime turns and instantly reconstitutes the file with 100% fidelity without requiring server restarts or internet downloads.
