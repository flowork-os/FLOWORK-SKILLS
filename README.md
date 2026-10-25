# 🧠 Flowork OS Sovereign Skills Registry

Official repository for modular Flowork OS skills, following the **2-Letter Alphabetical Sharded Directory Pattern** (`skills/{c1c2}/{skill_id}/`) and Sparse Sharded Index (`index/{c1c2}/{c3c4}/{skill_id}.json`).

## 📦 Installed Skills in Registry
| ID | Category | Version | Sharded Path |
| :--- | :--- | :--- | :--- |
| `software_company_sop` | Engineering SOP | 1.0.0 | `skills/so/software_company_sop` |
| `ui_ux_pro_max` | Design System | 1.0.0 | `skills/ui/ui_ux_pro_max` |

## 🚀 Architectural Invariants
1. **Frontmatter Standard**: Exactly 20 English keywords in `SKILL.md`.
2. **Sparse Sharding**: Sharded indexes ensure zero rate limits and instant sparse lookups.
3. **Decoupled Architecture**: All skills live outside binary runtimes.