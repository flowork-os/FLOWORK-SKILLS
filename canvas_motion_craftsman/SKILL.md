---
name: canvas_motion_craftsman
description: Sovereign runbook for purposeful micro-interactions, smooth CSS transitions, toast/modal entrance animations, and zero-jank UI
---
# 🎨 SKILL: CANVAS MOTION CRAFTSMAN & MICRO-INTERACTION ENGINEER
*Diadaptasi dari repositori dunia:* `affaan-m/ECC/skills/motion-patterns (274k★) & Liquid Glass Interaction`

Prosedur Operasi Standar (SOP) resmi kedaulatan Flowork OS untuk animasi mikro yang halus, transisi transparan, dan interaktivitas elegan:

## 1. DOKTRIN MOTION & INTERAKSI
- **Motion with Purpose (No Gimmick)**:
  - Animasi hanya digunakan untuk memberi feedback terhadap aksi user (klik tombol, ekspansi menu, munculnya toast, transisi tab).
  - Dilarang membuat animasi berputar atau slide-in konstan yang mengganggu fokus kerja operator.

- **Performa 60 FPS (Hardware Accelerated)**:
  - Hanya animasikan properti `transform` dan `opacity`.
  - Hindari menganimasikan `height`, `width`, `margin`, atau `top/left` yang memicu reflow berat browser Canvas.

- **Timing & Easing Baku**:
  - Durasi mikro: 150ms - 200ms untuk hover dan tombol feedback (`cubic-bezier(0.4, 0, 0.2, 1)`).
  - Durasi modal/drawer: 250ms - 300ms untuk entrance dan exit.
  - Exit animation wajib sama mulusnya dengan enter animation.
