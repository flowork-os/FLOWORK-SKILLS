<div align="center">

# 📚 Flowork OS Sovereign Skills Registry (`FLOWORK-SKILLS`)

**Curated Standardized Runbooks, Operational SOPs & On-Demand Skills for Autonomous AI Agents**

[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Standardized%20Runbooks-FF6F00?style=for-the-badge&logo=openai&logoColor=white)](https://floworkos.com)
[![Prompt Ops](https://img.shields.io/badge/Prompt%20Ops-Zero--Hallucination%20SOP-8A2BE2?style=for-the-badge)](https://floworkos.com)
[![Zero Token Bloat](https://img.shields.io/badge/Context%20Engine-Just--In--Time%20Delivery-00D26A?style=for-the-badge)](https://floworkos.com)
[![Architecture](https://img.shields.io/badge/Architecture-Nano--Modular%20Sharded-00F5FF?style=for-the-badge)](https://floworkos.com)
[![License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)](https://github.com/flowork-os/FLOWORK-SKILLS/pulls)

<br />

<a href="https://github.com/flowork-os/FLOWORK-AGENT">
  <img src="https://img.shields.io/badge/%E2%9A%A1%20DOWNLOAD%20FLOWORK%20AGENT-INSTALL%20NOW%20%E2%86%92-FF0055?style=for-the-badge&logo=rocket&logoColor=white&labelColor=0D1117" alt="Download Flowork Agent" height="54" />
</a>

<br /><br />

<p align="center">
  <a href="#-get-the-flowork-agent">Download Agent</a> •
  <a href="#-the-paradigm-shift">The Paradigm Shift</a> •
  <a href="#-dynamic-discovery--search">Discovery</a> •
  <a href="#-architecture--specs">Architecture</a> •
  <a href="#-the-sacred-20-keyword-standard">20-Keyword Standard</a> •
  <a href="#-zero-api-cdn-installation">Installation</a> •
  <a href="#-contributing-new-skills">Contributing</a>
</p>

---

</div>

## ⚡ Get the Flowork Agent

To execute operational runbooks, enable autonomous 20-keyword semantic skill interception, and run sovereign multi-agent loops with zero token bloat, download the official **Flowork Agent Engine**:

<div align="center">

[![Download Flowork Agent](https://img.shields.io/badge/%E2%9A%A1%20DOWNLOAD%20FLOWORK%20AGENT-CLICK%20TO%20GET%20STARTED-FF0055?style=for-the-badge&logo=github&logoColor=white&labelColor=0D1117)](https://github.com/flowork-os/FLOWORK-AGENT)

**[👉 https://github.com/flowork-os/FLOWORK-AGENT 👈](https://github.com/flowork-os/FLOWORK-AGENT)**

*Native support for Linux (x86_64, AArch64) • Windows 10/11 • macOS*

</div>

---

## 💡 The Paradigm Shift: On-Demand Skills vs Prompt Bloat

### The Flaw of Monolithic System Prompts
Stuffing dozens of domain-specific instructions into an LLM's system prompt leads to:
1. **Context Exhaustion**: Massive token overhead before the agent even begins the task.
2. **Attention Dilution & Hallucination**: Conflicting guidelines confuse LLM reasoning paths.
3. **Severe Rigidity**: Inability to update specialized runbooks without redeploying the entire agent stack.

### The Flowork OS Solution: Just-In-Time (JIT) Skill Ingestion
Flowork OS decouples agent operational intelligence into modular runbooks:
- 🎯 **Pure Off-Context Storage**: Skills reside in high-speed sharded indexes, consuming zero prompt tokens until required.
- ⚡ **Auto-Intercept Gate**: When a task is dispatched, the runtime matches user intents against the skill catalog and auto-injects **at most 1 active skill** into context.
- 🧹 **Instant Eviction**: Upon task completion (Exit Code 0), the skill is de-mounted, returning the context to baseline.

---

## 🔍 Dynamic Discovery & Search

To support unlimited runbook growth without bloating repository documentation, all skills are indexed dynamically:

### 1. Web Skills Explorer
Search and inspect verified runbooks interactively on the official portal:
👉 **[https://plugins.floworkos.com](https://plugins.floworkos.com)**

### 2. Edge Gateway API
Real-time JSON search endpoint powered by Cloudflare Workers:
```bash
# Search skills by domain or keyword
curl -s "https://plugins.floworkos.com/api/skills/search?q=cybersecurity"
```

### 3. Agent Semantic Recall & CLI
Flowork AI agents discover skills autonomously during reasoning:
```bash
# Query registry via Flowork CLI
flowork skill search "smart contract audit"
```

### 4. Sharded Metadata Index
Direct O(1) file lookups:
`index/<aa>/<bb>/<skill_id>.json`

---

## 🏛️ Architecture & Sharded Lookup

```
FLOWORK-SKILLS/
├── index/                        # O(1) Crates.io-style sharded lookup metadata
│   └── <aa>/<bb>/<skill_id>.json
├── skills/                       # Sovereign skill runbook repositories
│   └── <aa>/<skill_id>/
│       ├── SKILL.md              # Mandatory runbook with 20-keyword frontmatter
│       ├── scripts/              # Optional helper utilities
│       ├── examples/             # Implementation patterns & test cases
│       └── resources/            # Schemas, payloads & reference tables
├── skills.json                   # Root catalog index
└── README.md
```

### O(1) Sharding Algorithm
To guarantee instant Git and filesystem lookups across tens of thousands of skills:
$$\text{Skill Directory} = \text{skills}/\{id[0..2]\}/\{id\}$$
$$\text{Index Shard} = \text{index}/\{id[0..2]\}/\{id[2..4]\}/\{id\}.\text{json}$$

---

## 📜 The Sacred 20-Keyword Standard

Every skill MUST be authored as a markdown document (`SKILL.md`) beginning with YAML frontmatter containing **EXACTLY 20 ENGLISH KEYWORDS**. Skills failing this specification are automatically rejected by the preflight compiler and runtime gatekeeper.

### Why Exactly 20 English Keywords?
1. **Deterministic Vector Space**: Eliminates vector indexing skew caused by unbalanced keyword lengths.
2. **Cross-Model Semantic Alignment**: Ensures optimal retrieval across all frontier LLMs (Claude, GPT, Gemini, DeepSeek).
3. **Rigorous Scoping**: Forces runbook authors to precisely define target symptoms, root causes, tooling, and execution environments.

### Standard `SKILL.md` Template
```markdown
---
name: example_skill_name
description: Clear, concise explanation of when and why to activate this skill.
category: Architecture & System
version: 1.0.0
author: Flowork OS & Community
keywords:
  - keyword_01
  - keyword_02
  - keyword_03
  - keyword_04
  - keyword_05
  - keyword_06
  - keyword_07
  - keyword_08
  - keyword_09
  - keyword_10
  - keyword_11
  - keyword_12
  - keyword_13
  - keyword_14
  - keyword_15
  - keyword_16
  - keyword_17
  - keyword_18
  - keyword_19
  - keyword_20
---

# Operational Runbook: Example Skill

## 1. Trigger Conditions
- Exact symptoms and agent triggers.

## 2. Standard Operating Procedure (SOP)
1. Step-by-step verifiable actions.
2. Terminal commands and expected outputs.

## 3. Verification & Exit Code 0 Proof
- Mandatory checks to confirm task success.
```

---

## ⚡ Zero-API CDN Installation

Stream and extract runbooks directly via raw GitHub archive streaming without consuming GitHub API rate limits:

```bash
SKILL_ID="security_auditor"
PREFIX="${SKILL_ID:0:2}"

curl -sL "https://codeload.github.com/flowork-os/FLOWORK-SKILLS/tar.gz/main" | \
  tar -xz --strip-components=3 -C ./.agents/skills/ "FLOWORK-SKILLS-main/skills/${PREFIX}/${SKILL_ID}"
```

---

## 🤝 Contributing New Skills

We welcome battle-tested operational runbooks from the community!

### Quality Checklist:
1. **YAML Frontmatter**: Includes `name`, `description`, `category`, and **exactly 20 English keywords**.
2. **Empirical Verification**: Runbooks must mandate terminal proof with Exit Code 0.
3. **No Fluff**: Pure technical, actionable procedures. No conversational filler.
4. **Self-Contained**: Any helper scripts must live in the skill's `scripts/` directory.

### Submit via Pull Request
```bash
git checkout -b feature/add-skill
# Place skill in skills/{id[:2]}/{id}
git add skills/ index/ skills.json
git commit -m "feat(skills): publish <id> runbook"
git push origin feature/add-skill
```

---

## 📄 License

Licensed under the **MIT License**. Engineered for sovereign AI intelligence by Flowork OS.

Co-authored-by: Flowork OS <agent@floworkos.com>
