# DeksLink — UI Guideline

**Versi:** 2.0 | **Status:** Target produksi | **Arah:** Professional editorial SaaS

Dokumen ini menjadi acuan visual untuk produk produksi DeksLink. Antarmuka harus terasa tenang, tepercaya, dan siap dipakai bekerja; elemen demo hanya boleh muncul pada environment staging yang diberi penanda jelas.

## 1. Prinsip desain

- **Clarity first:** satu layar memiliki satu tujuan utama dan satu tindakan utama.
- **Professional warmth:** cokelat brand, putih, dan warna netral memberi karakter tanpa terlihat dekoratif berlebihan.
- **Editorial hierarchy:** heading kuat, ruang kosong cukup, dan metadata tidak bersaing dengan konten utama.
- **Trust by design:** status, izin, publikasi, keamanan, dan error dijelaskan dengan bahasa langsung.
- **Quiet quality:** gunakan border, shadow, dan motion seperlunya. Jangan memakai neon, glassmorphism berat, atau ornamen yang mengganggu pekerjaan.
- **Consistent behavior:** pola form, tabel, modal, toast, loading, dan empty state sama di seluruh area produk.

## 2. Token warna

| Token | Nilai | Penggunaan |
|---|---|---|
| `--color-brand` | `#5C3B2E` | CTA utama, logo, link aktif |
| `--color-brand-hover` | `#493024` | Hover dan pressed state |
| `--color-brand-soft` | `#F1E7DF` | Selected state, tint ringan |
| `--color-accent` | `#A77B5B` | Aksen, focus ring, dekorasi terbatas |
| `--color-bg` | `#FFFFFF` | Latar utama |
| `--color-bg-muted` | `#F7F4F1` | Latar halaman dan section sekunder |
| `--color-surface` | `#FFFFFF` | Card, panel, dialog |
| `--color-surface-raised` | `#FCFBFA` | Panel yang membutuhkan pemisahan halus |
| `--color-text` | `#27231F` | Teks utama |
| `--color-text-muted` | `#6D625A` | Metadata dan bantuan |
| `--color-border` | `#E5DDD5` | Border dan divider |
| `--color-success` | `#237A4B` | Berhasil, aktif, terbit |
| `--color-warning` | `#946200` | Perlu perhatian |
| `--color-danger` | `#B42318` | Error dan tindakan destruktif |
| `--color-info` | `#175CD3` | Informasi dan bantuan |

Teks normal harus memiliki kontras minimal WCAG AA. Warna tidak boleh menjadi satu-satunya penanda status; sertakan label atau ikon dengan nama aksesibel.

## 3. Tipografi

- Font utama: Inter atau system sans yang setara; fallback `ui-sans-serif, system-ui, sans-serif`.
- Heading besar: 40–64 px desktop, 32–44 px mobile, berat 700–800, line-height 1.05–1.15.
- Heading halaman: 28–40 px, berat 700–800.
- Body: 15–16 px, line-height 1.5–1.7.
- Label dan metadata: 12–14 px, line-height 1.4.
- Angka statistik: gunakan tabular numerals dan label yang jelas.
- Maksimal sekitar 70 karakter per baris untuk paragraf panjang.

Jangan mencampur lebih dari dua keluarga font. Gaya serif hanya digunakan sebagai aksen editorial pada preset tema, bukan untuk label navigasi atau form.

## 4. Spacing, grid, dan bentuk

- Skala spacing: 4, 8, 12, 16, 24, 32, 40, 48, 64.
- Container desktop: maksimum 1180 px; content dashboard: 1120 px; form panjang: 640–720 px.
- Radius: 8 px untuk kontrol, 12 px untuk card, 16–20 px untuk panel hero atau preview.
- Tinggi kontrol: minimum 44 px; target sentuh mobile minimum 44 × 44 px.
- Shadow: satu shadow halus untuk surface yang terangkat; hindari shadow bertumpuk.
- Border digunakan untuk memisahkan area, bukan menghias setiap elemen.

## 5. Layout dan navigasi

- Public layout memakai navbar ringkas, CTA yang jelas, content container, dan footer informatif.
- Dashboard desktop memakai sidebar tetap dengan brand, navigasi berkelompok, status halaman, dan akun di bagian bawah.
- Dashboard mobile memakai top bar atau drawer yang dapat dibuka keyboard; jangan menyembunyikan tindakan penting tanpa akses alternatif.
- Admin memakai layout yang sama dengan label area Admin dan permission-aware navigation.
- Breadcrumb digunakan pada detail atau alur bertingkat, bukan pada halaman sederhana.
- Link aktif memiliki indikator visual dan `aria-current="page"`.

## 6. Responsive behavior

- `<640px`: satu kolom, tabel menjadi scroll container atau cards, form full width, CTA dapat menjadi full width.
- `640–1023px`: grid fleksibel, panel dapat ditumpuk, sidebar dapat menjadi drawer.
- `>=1024px`: sidebar dan grid multi-kolom bila membantu perbandingan atau preview.
- Tidak boleh ada horizontal overflow pada viewport 320 px ke atas.
- Modal pada mobile memakai hampir seluruh lebar dengan padding aman dan tombol mudah dijangkau.

## 7. Komponen dan pola

- **Button:** primary, secondary, outline, danger, ghost; memiliki hover, focus, pressed, disabled, dan loading.
- **Form field:** label terlihat, hint, error terhubung dengan `aria-describedby`, dan validasi dekat field.
- **Dialog:** judul jelas, fokus masuk ke dialog, Escape menutup jika aman, fokus kembali ke trigger, dan tindakan destruktif diberi label spesifik.
- **Toast:** untuk hasil tindakan yang tidak memerlukan keputusan; tidak menggantikan error field.
- **Table:** caption atau label region, header semantik, pagination, filter, empty state, dan mobile fallback.
- **Card:** satu tema konten; jangan menumpuk card tanpa hierarki.
- **Skeleton:** mengikuti bentuk konten, tidak menjadi dekorasi kosong.
- **Avatar:** foto dengan fallback inisial, alt text yang sesuai, dan crop aman.
- **Preview:** memakai renderer yang sama dengan halaman publik agar hasil tidak menipu.

## 8. State dan feedback

Setiap operasi data memiliki state loading, success, empty, error, dan retry bila relevan. Untuk perubahan draft gunakan indikator unsaved changes dan konfirmasi saat meninggalkan halaman bila data belum disimpan. Hindari spinner tanpa konteks; jelaskan apa yang sedang dimuat.

Produksi tidak menampilkan kata “simulasi”, “dummy”, atau “contoh login”. Environment staging boleh menampilkan banner kecil seperti “Staging environment” dan data uji tidak boleh tercampur dengan data produksi.

## 9. Halaman bio publik

- Fokus utama adalah identitas pemilik dan daftar tautan; jangan membebani halaman dengan dashboard-style controls.
- Avatar, nama, username, bio, dan tautan aktif tersusun dalam kolom terpusat dengan area klik besar.
- Tautan memakai judul yang bermakna, ikon hanya sebagai pendukung, dan indikator external link bila membuka tab baru.
- Tema harus menjaga kontras teks dan tombol; preset yang tidak memenuhi kontras tidak boleh tersedia.
- Sertakan metadata share dan footer brand secara halus.
- Status not found, unpublished, disabled, blocked, dan temporary error memakai pesan berbeda yang membantu pengguna.

## 10. Form, copy, dan tone

- Gunakan bahasa Indonesia yang ringkas, profesional, dan spesifik pada tindakan.
- Label tombol memakai kata kerja: “Simpan perubahan”, “Terbitkan halaman”, “Nonaktifkan tautan”.
- Pesan error menjelaskan masalah dan cara memperbaikinya.
- Konfirmasi destruktif menyebut objek dan konsekuensinya.
- Jangan gunakan teks internal seperti “mock”, “dummy”, “fixture”, atau “simulasi” di produk produksi.
- Jangan menjanjikan email, penyimpanan, analitik, atau keamanan yang belum benar-benar aktif.

## 11. Motion dan aksesibilitas

- Transisi 120–200 ms untuk perubahan kecil; tidak ada animasi yang menghalangi tugas.
- `:focus-visible` harus jelas pada semua kontrol.
- Semua aksi ikon memiliki accessible name; ikon dekoratif memakai `aria-hidden`.
- Urutan tab logis dan tidak ada keyboard trap selain dialog yang dikelola dengan benar.
- Hormati `prefers-reduced-motion`.
- Target aksesibilitas: WCAG 2.2 AA, termasuk zoom 200%, keyboard penuh, screen reader labels, dan kontras.

## 12. Quality bar visual

Sebelum layar disetujui, periksa hierarchy, alignment, spacing, copy, loading/error/empty state, keyboard focus, kontras, viewport mobile, dan apakah tindakan utama terlihat tanpa penjelasan tambahan. Screenshot staging harus dibedakan dari screenshot produksi melalui environment label, bukan melalui perubahan desain produk.
