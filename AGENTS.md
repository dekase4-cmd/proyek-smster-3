# AGENTS.md — DeksLink Project Contract

## 1. Source of Truth
Urutan acuan: `PRD.md` (kebutuhan produk), `UI-GUIDELINE.md` (visual/UX), `IMPLEMENTATION_PLAN.md` (arsitektur dan tahapan), lalu dokumen ini (kontrak agent). Jika instruksi bertentangan, jangan menebak atau memperluas scope; jelaskan konflik dan minta persetujuan.

## 2. Stack
React + Vite, JavaScript/JSX, CSS3 design tokens, React Router DOM, Lucide React, mock data/service. Jangan menambahkan library besar, backend, atau database tanpa kebutuhan dan persetujuan.

## 3. Scope Guard
Kerjakan hanya fitur PRD. Jangan mulai backend, database, auth server, deployment produksi, atau analytics nyata pada fase frontend. Jangan menyebut simulasi sebagai fitur produksi. Jika syarat penting tidak jelas, tanyakan sebelum mengubah arsitektur.

## 4. Hemat Token dan Perubahan
Baca hanya dokumen/file relevan. Periksa implementasi sebelum membuat file. Hindari duplikasi. Jangan menulis ulang file yang tidak terkait. Gunakan komponen reusable dan service layer. Laporan ringkas; jangan menyalin ulang seluruh kode. Rujuk bagian SOT daripada mengulang isi.

## 5. UI/UX
Ikuti `UI-GUIDELINE.md`. Warna brand `#5C3B2E`, latar `#FFFFFF`, sekunder `#F5F0EA`. Desain modern, minimalis, profesional, cokelat-putih. Semua tombol/form harus berfungsi dalam konteks prototipe. Tangani state yang relevan, responsivitas, keyboard focus, dan `prefers-reduced-motion`. Ikon aksi penting harus memiliki accessible name.

## 6. Keamanan dan Data
Autentikasi frontend hanya simulasi. Jangan simpan password, secret, atau credential di localStorage, source code, atau bundle frontend. Jangan masukkan API secret ke environment variable yang terekspos browser. Mock data bukan penyimpanan permanen. Route guard frontend bukan otorisasi server.

## 7. Arsitektur
Gunakan React Router DOM. Pisahkan pages, components, layouts, routes, services, data, hooks, utils, styles sesuai kebutuhan. Halaman memakai service layer. Buat folder saat dibutuhkan; hindari abstraksi berlebihan.

## 8. Execution Gate
Setiap phase coding membutuhkan persetujuan pengguna. Persetujuan SOT final tidak berarti seluruh coding boleh berjalan otomatis. Kerjakan satu phase/unit, lalu berhenti dan laporkan:
1. Ringkasan perubahan.
2. File dibuat/diubah.
3. Pemeriksaan dan hasil sebenarnya.
4. Kendala.
5. Unit berikutnya yang menunggu persetujuan.
Jangan lanjut tanpa persetujuan eksplisit.

## 9. Quality Gate
Jalankan lint/build atau pemeriksaan relevan jika tersedia. Jangan mengklaim tes lulus jika belum dijalankan. Perbaiki error yang diperkenalkan. Laporkan pemeriksaan yang tidak bisa dijalankan.

## 10. Definition of Done
Pekerjaan memenuhi kriteria relevan dari PRD dan plan, tidak memperluas scope tanpa izin, dan melaporkan secara jujur apa yang sudah/belum diverifikasi.
