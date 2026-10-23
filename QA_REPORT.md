# QA frontend — 17 Oktober 2026

## Unit P8: integrasi editor dan pemeriksaan regresi

Data profil dan tautan sekarang dibagikan melalui ProfileContext; validasi, pembuatan, penyuntingan, dan pengurutan tautan memakai editorService. Dashboard, editor tampilan, dan bio publik membaca data sesi yang sama. Username baru langsung dapat dibuka melalui navigasi aplikasi. Semua data kembali ke awal setelah reload; URL hasil perubahan tidak menyediakan penyimpanan atau publikasi lintas sesi.

Perbaikan lain: URL tautan hanya HTTP(S), validasi nama/username unik, empty state tautan, logout mobile, modal native dengan Escape/fokus, tombol loading tetap disabled, CTA tanpa elemen interaktif bersarang, target kebijakan privasi prototipe, pilihan avatar mock, dan preset tema.

Bio publik sekarang memuat melalui mock service dengan skeleton singkat. Route `/u/unavailable` sengaja menyimulasikan gangguan data untuk memeriksa state error; ini bukan kondisi produksi atau integrasi API.

## Pemeriksaan aktual

- ESLint: lulus tanpa warning.
- Build Vite: berhasil. Node lokal 20.15.0 masih mengeluarkan peringatan; Vite meminta 20.19+ atau 22.12+.
- Assertion service Node: validasi nama dan username, penolakan URL berbahaya/tidak valid, tambah/edit/urutan tautan, status admin, review laporan, dan log aktivitas lulus.
- Chromium headless: guard dashboard, login/logout, tambah/edit/hapus tautan, tautan baru di bio publik, perubahan username, simpan bentuk tombol, visibilitas halaman, modal Escape dan fokus kembali, filter/detail admin, profil tidak ditemukan/nonaktif lulus.
- Pemeriksaan overflow otomatis pada 375/768/1280 px: halaman tautan, landing, registrasi, lupa password, bio publik, dan 404 lulus. Logout terlihat pada ketiga ukuran.
- Tidak ada pageerror selama alur browser tersebut. Ini bukan audit semua pesan console, semua perangkat, atau semua kemungkinan interaksi.
- Pemeriksaan tambahan Chromium: skeleton/error bio, penyimpanan avatar mock dan preset tema ke preview publik, serta overflow mobile lulus tanpa pageerror.
- Pemeriksaan penutupan Chromium: route publik, dashboard pengguna, dan admin tidak meluber pada 375/768/1280 px. Submit keyboard, toggle kata sandi, preset tema, Escape pada modal, serta navigasi dashboard/admin lulus tanpa pageerror.
- Audit aksesibilitas otomatis Chromium: setiap route publik, user, dan admin memiliki satu landmark `main`; seluruh kontrol interaktif yang terlihat memiliki nama aksesibel melalui teks, label, atau `aria-label`.
- Unit polish produksi: halaman pengguna tidak lagi menampilkan copy “simulasi”, “dummy”, atau “prototipe”. Development menampilkan banner environment dan production preview menyembunyikan banner tersebut; kedua mode lulus pemeriksaan browser.
- Loading screen branded DeksLink tampil saat aplikasi dibuka, memiliki status yang dapat dibaca screen reader, animasi orbit/progress, fallback reduced-motion, lalu berpindah ke landing page setelah bootstrap selesai.
- Fondasi backend Node.js: lima server test lulus untuk health endpoint, structured error, request ID, header keamanan, dan permission matrix `visitor`, `user`, `moderator`, `admin`, `operator`. Smoke test proses server juga merespons `200` pada health endpoint dan mengembalikan role contract.
- Unit P1 backend: schema PostgreSQL baseline dan kontrak API v1 ditambahkan untuk user, session, profile, links, theme, media, reports, consent, dan audit events. Test server, lint, dan build lulus; `psql` tidak tersedia sehingga migration belum dijalankan pada database nyata.

## Batas pemeriksaan

- Pemeriksaan visual manual, screen reader, seluruh kombinasi keyboard/kontras, dan browser selain Chromium belum dilakukan.
- Field wajib memakai validasi native browser sebelum validasi React berjalan. Pesan kesalahan React tetap memiliki `role="alert"` untuk kondisi validasi yang lolos dari pemeriksaan native.
- Admin dan pengguna masih memakai dataset mock terpisah; perubahan status admin belum mengendalikan sesi pengguna atau bio publik. Ini konsisten dengan batas prototipe frontend, tetapi perlu dirancang ulang saat backend/otorisasi server ditambahkan.
- Node lokal 20.15.0 tetap menampilkan peringatan kompatibilitas Vite. Build saat ini berhasil, tetapi gunakan Node 20.19+ atau 22.12+ sebelum rilis produksi.

Unit berhenti di sini sesuai AGENTS.md §8. Tidak ada backend atau deployment.
