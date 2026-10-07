---
name: agent_mesh_communicator
description: Sovereign runbook for peer-to-peer message routing and synchronization across active agent workers
---
# 🛠️ SKILL: AGENT MESH COMMUNICATOR & INTER-AGENT IPC
*Diadaptasi untuk tool Flowork:* `send_message` | *Referensi:* ECC Agentic Engineering & Messages Ops

Prosedur Operasi Standar (SOP) resmi kedaulatan Flowork OS untuk koordinasi pesan antar-agen.

## 1. DOKTRIN PERTUKARAN PESAN
- **High Signal Inter-Agent Payload**: Pesan antar-agen wajib berupa fakta terstruktur (JSON / ringkasan teknis padat), nol basa-basi.
- **Deadlock Defense**: Jangan buat komunikasi sirkular blocking antar dua agen aktif.
- **Event Acknowledgment**: Pastikan pesan konfirmasi tersampaikan.
