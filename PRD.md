# DeksLink — Product Requirements Document

**Versi:** 2.0 | **Status:** Target produksi | **Cakupan:** Produk web end-to-end

## 1. Ringkasan produk

DeksLink adalah platform bio-link profesional yang membantu individu, kreator, profesional, dan bisnis kecil mengelola identitas digital serta tautan mereka dari satu dashboard. Setiap pengguna memiliki halaman publik yang cepat, mudah ditemukan, dapat disesuaikan, dan aman untuk dibagikan.

Dokumen ini menggantikan PRD prototipe. Frontend yang sudah tersedia menjadi baseline UI dan alur; data mock, login lokal, serta route guard frontend hanya digunakan selama pengembangan sampai service produksi tersedia.

## 2. Tujuan dan hasil yang diukur

- Pengguna dapat membuat dan menerbitkan halaman bio-link dalam waktu kurang dari lima menit.
- Pengguna dapat mengelola tautan, profil, dan tampilan tanpa coding.
- Halaman publik memuat cepat, responsif, mudah dibagikan, dan aman.
- Admin dapat menjaga kualitas konten, akun, laporan, dan audit aktivitas.
- Arsitektur memungkinkan penggantian service pengembangan dengan API produksi tanpa menulis ulang halaman.

Indikator produk yang disiapkan sejak awal: profil yang berhasil diterbitkan, tautan aktif per profil, waktu pembuatan profil, rasio halaman publik yang berhasil dimuat, laporan yang terselesaikan, dan error rate. Pengukuran analitik hanya diaktifkan setelah persetujuan privasi dan implementasi layanan yang sesuai.

## 3. Pengguna dan peran

- **Pengunjung:** melihat halaman publik, membuka tautan, dan melaporkan tautan yang bermasalah.
- **Pemilik akun:** mendaftar, mengelola profil, menerbitkan halaman, mengatur tautan, dan mengubah tampilan.
- **Admin/moderator:** mengelola akun, memproses laporan, melihat audit aktivitas, dan menjaga kebijakan platform.
- **Operator teknis:** mengelola konfigurasi, deployment, monitoring, backup, dan incident response. Operator tidak memperoleh akses konten pengguna kecuali melalui prosedur yang diaudit.

## 4. Ruang lingkup produk

### 4.1 Situs publik dan onboarding

- Landing page dengan penjelasan nilai produk, contoh bio-link, pricing atau paket bila sudah ditetapkan, FAQ, kontak, dan kebijakan.
- Registrasi melalui email dan kata sandi; verifikasi email wajib sebelum publikasi.
- Login, logout, lupa kata sandi, reset dengan token sekali pakai, dan sesi yang dapat dicabut.
- Onboarding singkat: nama, username, tujuan penggunaan, dan tautan pertama.
- Username memiliki aturan karakter, pengecekan ketersediaan, reserved words, dan redirect yang konsisten.

### 4.2 Dashboard pengguna

- Ringkasan status halaman, jumlah tautan, tautan aktif, dan alamat publik.
- Navigasi desktop dan mobile yang konsisten.
- State loading, empty, error, retry, success, dan unsaved changes.
- Preview publik yang menggunakan data draft atau data terbit sesuai konteks.

### 4.3 Profil dan publikasi

- Nama tampilan, username, bio, avatar/foto, metadata sosial, dan visibilitas halaman.
- Upload avatar dengan validasi tipe, ukuran, dimensi, dan penghapusan file.
- Draft dan publish eksplisit. Perubahan draft tidak tampil ke publik sebelum diterbitkan.
- Unpublish sementara tanpa menghapus data.
- Validasi server untuk username unik dan izin perubahan username.

### 4.4 Manajemen tautan

- Tambah, edit, hapus dengan konfirmasi, aktif/nonaktif, dan pengurutan drag atau kontrol keyboard.
- Judul, URL HTTP(S), ikon, deskripsi opsional, dan target tautan.
- Validasi server dan pemeriksaan keamanan URL.
- Status tautan: draft, aktif, nonaktif, diblokir, atau dihapus.
- Import dan export CSV menjadi kandidat fase berikutnya, bukan syarat peluncuran awal.

### 4.5 Kustomisasi halaman

- Preset tema yang terkurasi, warna latar dan tombol dengan batas aksesibilitas, bentuk tombol, tipografi terbatas, dan layout yang stabil.
- Preview langsung yang sama dengan renderer halaman publik.
- Reset ke tema awal dan indikator perubahan yang belum disimpan.
- Tidak menyediakan CSS atau JavaScript arbitrer dari pengguna pada fase awal.

### 4.6 Halaman publik

- URL `/u/:username` dengan metadata SEO, Open Graph, favicon, canonical URL, dan status HTTP yang benar.
- Avatar, nama, username, bio, tautan aktif, dan footer brand.
- Responsif, dapat diakses keyboard dan screen reader, serta tetap terbaca pada semua tema yang tersedia.
- Halaman tidak ditemukan, belum diterbitkan, dinonaktifkan oleh pemilik, dan diblokir moderator memiliki pesan yang berbeda.
- Pengunjung dapat melaporkan tautan atau halaman dengan rate limit dan perlindungan spam.

### 4.7 Admin dan moderasi

- Admin login dengan MFA untuk role sensitif.
- Statistik operasional yang bersumber dari data produksi, bukan angka hard-coded.
- Daftar pengguna dengan pencarian, filter, pagination, detail, status, dan tindakan yang diaudit.
- Laporan dengan detail bukti, status, assignee, catatan moderator, dan riwayat tindakan.
- Activity log append-only dengan actor, waktu, target, tindakan, dan request ID.
- Role-based access control; setiap endpoint memeriksa izin di server.

### 4.8 Akun, privasi, dan keamanan

- Password disimpan hanya sebagai hash kuat di server; password mentah tidak pernah dicatat atau dikirim ke log.
- Session cookie aman dengan HttpOnly, Secure, SameSite, expiry, rotasi, dan pencabutan.
- Rate limiting, CSRF protection bila memakai cookie, validasi input, output encoding, dan sanitasi konten.
- Pengaturan akun: email, kata sandi, sesi aktif, ekspor data, dan penghapusan akun sesuai kebijakan retensi.
- Persetujuan kebijakan, privacy notice, dan pengelolaan data mengikuti regulasi yang berlaku untuk wilayah operasi.

## 5. Persyaratan nonfungsional

- **Performa:** target Core Web Vitals yang baik pada halaman publik; aset dikompresi, lazy loading digunakan bila relevan, dan tidak ada JavaScript yang tidak perlu.
- **Ketersediaan:** health check, logging terstruktur, monitoring, alerting, backup, dan prosedur pemulihan terdokumentasi.
- **Aksesibilitas:** WCAG 2.2 AA sebagai target; keyboard penuh, focus visible, nama kontrol, pesan error terhubung, kontras, dan reduced motion.
- **SEO dan shareability:** metadata per halaman, sitemap, robots policy, canonical, dan preview sosial yang benar.
- **Kompatibilitas:** dua versi utama browser modern pada desktop dan mobile; layout diuji pada breakpoint produk.
- **Privasi:** minimisasi data, retensi terukur, akses internal least privilege, dan audit akses data.
- **Observability:** error tracking tanpa password/token, request ID, metrik latency, dan audit tindakan penting.

## 6. Arsitektur dan kontrak service

Frontend React + Vite menggunakan React Router, design tokens CSS, komponen reusable, dan service layer. Service development boleh mengembalikan fixture lokal, tetapi kontraknya harus sama dengan API produksi. API produksi menjadi sumber kebenaran untuk akun, profil, tautan, tema, laporan, dan audit.

Tidak ada secret di bundle browser. Konfigurasi publik memakai environment variable yang aman; credential server, database, storage key, dan signing key hanya berada di backend atau secret manager. Frontend route guard membantu UX, tetapi otorisasi hanya berlaku setelah pemeriksaan server.

Entitas minimum: `User`, `Session`, `Profile`, `Link`, `Theme`, `Report`, `AuditEvent`, `MediaAsset`, dan `Consent`. Setiap entitas memiliki ID, timestamp, status, dan aturan ownership yang jelas.

## 7. Aturan produk

- Produksi tidak menampilkan teks “simulasi”, “dummy”, atau kredensial contoh kepada pengguna akhir.
- Lingkungan staging boleh memiliki banner environment yang jelas dan data uji yang terisolasi.
- Semua perubahan publik melalui draft/publish dan dapat ditelusuri.
- Penghapusan destruktif meminta konfirmasi dan mengikuti kebijakan pemulihan/retensi.
- Tautan aktif saja yang dirender pada halaman publik.
- Setiap tindakan utama memiliki feedback yang dapat dipahami dan dapat diakses.
- Fitur baru harus memiliki owner data, aturan izin, state error, dan kriteria penerimaan.

## 8. Kriteria penerimaan produksi

- Pengguna dapat mendaftar, memverifikasi email, login, reset password, dan mencabut sesi.
- Profil dan tautan tersimpan melalui API, tervalidasi server, dan dapat dipublish/unpublish.
- Halaman publik mengambil data terbit, memiliki status HTTP/SEO yang benar, dan menangani kondisi tidak ditemukan/nonaktif.
- Upload media melewati validasi dan storage yang aman.
- Admin hanya dapat melakukan tindakan sesuai role; semua tindakan moderasi tercatat di audit log.
- Tidak ada password, token, atau secret di localStorage, source map publik, log, atau bundle.
- Target aksesibilitas, performa, keamanan, monitoring, backup, dan recovery diuji sebelum launch.
- CI menjalankan lint, unit/integration test, build, dependency audit, dan pemeriksaan route utama.

## 9. Tahap peluncuran

1. Stabilkan kontrak API, skema data, autentikasi, dan environment staging.
2. Migrasikan service fixture ke API produksi dengan feature flag dan observability.
3. Uji keamanan, aksesibilitas, performa, backup/recovery, dan moderasi.
4. Soft launch terbatas, pantau error dan feedback, lalu buka secara bertahap.
5. Setelah stabil, tambah analitik dengan persetujuan privasi dan fitur lanjutan.

## 10. Di luar rilis awal

Marketplace template, kolaborasi multi-editor, domain custom, pembayaran berlangganan, import massal, integrasi pihak ketiga, dan aplikasi native memerlukan PRD serta persetujuan terpisah.
