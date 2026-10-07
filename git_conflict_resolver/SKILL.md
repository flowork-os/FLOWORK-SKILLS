---
name: git_conflict_resolver
description: Sovereign runbook for advanced Git merge conflict resolution, interactive rebase, cherry-pick tree integrity, bisect debugging, and reflog disaster recovery
keywords: ["git conflict resolver", "merge conflict", "interactive rebase", "cherry pick", "git bisect", "git reflog", "three way merge", "commit history cleanup", "squash commits", "branch reconciliation", "detached head recovery", "fast forward merge", "merge abort", "rebase continue", "git patch apply", "tree hygiene", "stash pop", "commit authorship", "merge conflict markers", "working tree restore"]
---

# ⚙️ SKILL: GIT CONFLICT RESOLVER

## 1. Intent & Trigger Boundaries
- **Intent**: Penyelesaian konflik merge git tingkat lanjut, rekonsiliasi cabang fitur dengan branch utama via `git rebase`, cherry-pick presisi, pelacakan commit biang bug via `git bisect`, dan pemulihan commit hilang via `git reflog`.
- **Trigger**: Terjadi benturan merge conflict saat pull/merge/rebase, kebutuhan merapikan riwayat commit (squash/fixup), pembatalan commit yang salah tanpa kehilangan progres, atau investigasi commit yang menyebabkan regresi sistem.
- **Boundaries**: Tidak mengurusi pembuatan rilis SemVer tagging dan changelog otomatis (gunakan `git_release_sentinel`). Fokus pada manipulasi pohon commit Git dan resolusi konflik internal.

## 2. Standard Operating Procedures (SOP)
1. **Three-Way Conflict Anatomy & Inspection**:
   - Deteksi seluruh file yang berstatus conflicted via `git status --porcelain | grep "^UU"`.
   - Periksa ketiga versi snapshot: `git diff --theirs`, `git diff --ours`, dan file dasar ancestory.
   - Bedah penanda konflik `<<<<<<< HEAD`, `=======`, dan `>>>>>>> [branch/commit]` tanpa menghapus logika penting milik kedua belah pihak secara membabi buta.
2. **Interactive Rebase & Commit Tidying**:
   - Jalankan `git rebase -i HEAD~n` untuk merapikan urutan commit.
   - Gunakan `squash` atau `fixup` untuk menggabungkan commit checkpoint kecil menjadi satu commit atomik bermakna.
   - Jika terjadi konflik saat rebase: selesaikan file, tandai via `git add <file>`, lalu lanjutkan dengan `git rebase --continue`. Jangan gunakan `git commit` di tengah rebase.
3. **Disaster Recovery with Git Reflog**:
   - Jika rebase atau merge berantakan dan ingin membatalkan total: eksekusi `git merge --abort` atau `git rebase --abort`.
   - Jika commit hilang atau salah reset hard: buka `git reflog`, cari posisi SHA commit sebelum kecelakaan, lalu pulihkan melalui `git reset --hard HEAD@{n}` atau `git checkout -b recovered-branch HEAD@{n}`.
4. **Bisect Root Cause Hunting**:
   - Jalankan `git bisect start`, tentukan `git bisect bad` (commit saat ini rusak) dan `git bisect good <commit-sha>` (commit terakhir yang diketahui stabil).
   - Jalankan test suite otomatis: `git bisect run <test_script.sh>` hingga Git mengisolasi commit penyebab kerusakan pertama kali.

## 3. Strict Prohibitions & Edge Cases
- **PROHIBITION**: Dilarang menggunakan opsi berbahaya `git push --force` di branch shared/utama (`main`, `master`). Selalu gunakan `git push --force-with-lease` jika rebase branch pribadi.
- **PROHIBITION**: Dilarang menyelesaikan konflik dengan meninggalkan sisa karakter penanda (`<<<<<<<`, `=======`, `>>>>>>>`).
- **EDGE CASE**: Terperangkap di detached HEAD state: segera buat branch baru untuk menampung pekerjaan sebelum beralih branch: `git checkout -b rescue-temp-branch`.

## 4. Verification & Exit Code 0 Proof
- Conflict Marker Audit: Memastikan nol file dengan penanda konflik: `git diff --check` menghasilkan exit code 0.
- Clean Working Tree: `git status --porcelain` mengembalikan output kosong (clean tree) dan exit code 0.
- Test Suite Validation: Seluruh test unit berhasil dieksekusi pasca-resolusi merge dengan exit code 0.
