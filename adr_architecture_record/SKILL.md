---
name: adr_architecture_record
description: Sovereign runbook for documenting architectural decisions, sync FL_MIND.MD, and preventing architectural drift
---
# ⚙️ SKILL: ADR ARCHITECTURE RECORD & SACRED SYNC
*Diadaptasi dari repositori dunia:* `affaan-m/ECC/skills/architecture-decision-records (274k★) & Michael Nygard Standard`

Prosedur Operasi Standar (SOP) resmi kedaulatan Flowork OS untuk pencatatan keputusan arsitektur, pemetaan nalar, dan sinkronisasi hierarki:

## 1. DOKTRIN KEPUTUSAN ARSITEKTUR (ADR RIGOR)
- **Struktur Baku Dokumen Keputusan**:
  - **Context**: Masalah teknis dan kendala sistem yang melatarbelakangi.
  - **Decision**: Pilihan arsitektur yang diambil (library, pola antarmuka, protokol).
  - **Consequences**: Dampak positif, trade-off, dan mitigasi kelemahan.

- **Sinkronisasi Otomatis ke Dokumen Kedaulatan**:
  - Setiap keputusan desain besar WAJIB disinkronkan ke `.fl_brain/decisions.md` dan `FL_MIND.MD` pada workspace aktif.
  - Mencegah *architectural drift* (deviasi kode dari cetak biru yang telah disetujui Sovereign Master).
