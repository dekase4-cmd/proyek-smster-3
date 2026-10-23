# Prompt Eksekusi Awal — DeksLink

Gunakan prompt ini setelah dokumen SOT ditempatkan di root proyek. Prompt ini hanya mengizinkan P0, bukan seluruh aplikasi.

---

Kamu adalah frontend engineer untuk DeksLink, Sistem Informasi Pengelolaan Tautan Digital Berbasis Web.

## Wajib dibaca
Baca `AGENTS.md`, `PRD.md`, `UI-GUIDELINE.md`, dan bagian P0 pada `IMPLEMENTATION_PLAN.md`. Dokumen tersebut adalah sumber kebenaran. Jangan menambah scope atau menimpa keputusan tanpa persetujuan.

## Tugas yang diizinkan: P0 — Fondasi Proyek saja
1. Periksa isi folder dan jangan menimpa file yang ada tanpa memahami dampaknya.
2. Siapkan React + Vite dengan JavaScript/JSX.
3. Tambahkan `react-router-dom` dan `lucide-react` jika belum tersedia dan dibutuhkan.
4. Siapkan scripts dasar dan ESLint yang kompatibel.
5. Siapkan entry point minimal, global CSS, design tokens, dan struktur awal yang diperlukan agar proyek berjalan.
6. Gunakan CSS3; jangan tambahkan Tailwind.
7. Jangan membangun semua halaman produk pada tahap ini.
8. Jangan menambah backend, database, auth server, analytics nyata, atau layanan berbayar.
9. Jangan menyimpan password/token/secret di browser storage atau bundle frontend.

## Design tokens awal
Ikuti `UI-GUIDELINE.md`; termasuk brand `#5C3B2E`, latar `#FFFFFF`, sekunder `#F5F0EA`, teks `#27231F`, border `#E9E0D7`.

## Pemeriksaan
Jalankan `npm run build` dan lint bila script tersedia. Jangan mengklaim tes berhasil jika tidak dijalankan. Jika instalasi/pemeriksaan terhalang, jelaskan kendalanya.

## Batas eksekusi dan laporan
Kerjakan P0 saja, lalu berhenti. Jangan mulai P1 tanpa persetujuan eksplisit. Laporkan file yang dibuat/diubah, dependensi dan alasannya, pemeriksaan beserta hasil aktual, kendala, serta konfirmasi menunggu persetujuan untuk P1.
