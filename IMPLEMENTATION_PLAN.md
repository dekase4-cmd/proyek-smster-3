# DeksLink — Implementation Plan

**Versi:** 2.0 | **Status:** Roadmap target produksi | **Target:** produk web production-ready

## 1. Prinsip implementasi

PRD v2.0 dan UI Guideline v2.0 menjadi sumber kebenaran. Frontend yang telah dibuat adalah baseline alur dan visual. Fixture atau mock service hanya digunakan di development dan staging; setiap service harus memiliki kontrak yang dapat diganti API produksi.

Jangan menyimpan password, token, atau secret di browser. Route guard frontend hanya membantu UX. Otorisasi, validasi ownership, dan audit wajib dilakukan server sebelum launch.

## 2. Stack dan platform

- React + Vite, JavaScript/JSX, CSS design tokens, React Router, Lucide React.
- Backend API terpisah dengan kontrak OpenAPI atau dokumentasi setara.
- Database relasional untuk user, profile, links, themes, reports, sessions, consent, dan audit event.
- Object storage untuk avatar/foto dengan signed upload URL dan pemeriksaan tipe/ukuran.
- Queue atau worker untuk email, image processing, dan tugas asynchronous bila diperlukan.
- CI untuk lint, unit/integration test, build, dependency audit, dan deployment staging.
- Monitoring error, latency, availability, audit trail, backup, dan incident response.

## 3. Fase implementasi

### P0 — Fondasi dan design system

Stabilkan token, komponen, layout, route map, form primitives, error boundary, environment config, dan CI dasar. Selesai saat lint/build berjalan dan komponen memiliki state utama.

### P1 — Kontrak backend dan data

Tentukan skema entitas, ownership, migration, API contract, error format, pagination, idempotency, dan seed staging. Sediakan service adapter agar halaman tidak bergantung pada fixture.

### P2 — Identity dan session

Implementasikan register, email verification, login, reset password, session rotation/revocation, rate limit, MFA admin, consent, dan security logging. Uji token expiry, brute force, CSRF, dan account enumeration.

### P3 — Profil, media, draft, dan publish

Hubungkan profile editor ke API, upload avatar aman, username availability, draft/publish/unpublish, preview draft, metadata publik, dan cache invalidation.

### P4 — Tautan dan tema

Hubungkan CRUD, ordering, validation, URL safety, themes, accessible color constraints, optimistic/pessimistic state sesuai operasi, retry, dan unsaved changes.

### P5 — Halaman publik dan SEO

Implementasikan renderer data terbit, HTTP status, not found/unpublished/blocked, OG metadata, canonical, sitemap, caching/CDN, rate limit report, dan performance budget.

### P6 — Admin dan moderasi

Implementasikan RBAC server, admin dashboard berbasis data produksi, pengguna, laporan, detail, status, audit log append-only, pagination/filter, dan approval policy.

### P7 — Production hardening

Security review, dependency audit, accessibility audit, responsive QA, browser matrix, load test, backup/restore drill, observability, privacy review, legal copy, and runbook.

### P8 — Staging, launch, dan operasi

Deploy staging dengan data terisolasi, jalankan smoke/e2e test, soft launch terbatas, monitor SLO, siapkan rollback, lalu lakukan rollout bertahap. Setelah stabil, aktifkan fitur tambahan melalui feature flag.

## 4. Struktur folder target

```text
dekslink/
├── public/assets/
├── src/
│   ├── assets/
│   ├── components/{ui,forms,feedback}/
│   ├── layouts/{PublicLayout,DashboardLayout,AdminLayout}.jsx
│   ├── pages/{public,auth,dashboard,profile,links,appearance,admin}/
│   ├── routes/AppRoutes.jsx
│   ├── services/{api,fixtures,index.js}
│   ├── data/
│   ├── hooks/
│   ├── context/
│   ├── utils/
│   ├── styles/{tokens.css,global.css,responsive.css}
│   ├── App.jsx
│   └── main.jsx
├── .env.example
├── .gitignore
├── eslint.config.js
├── index.html
├── package.json
└── vite.config.js
```

## 5. Routing dan akses

Public: `/`, `/login`, `/register`, `/forgot-password`, `/u/:username`, `*`.

User: `/dashboard`, `/dashboard/profile`, `/dashboard/links`, `/dashboard/appearance`, `/settings/security`.

Admin: `/admin/login`, `/admin`, `/admin/users`, `/admin/reports`, `/admin/activity`.

Frontend route guard mengarahkan pengguna untuk pengalaman yang benar, tetapi semua route API dan tindakan server memeriksa session, role, ownership, dan status akun.

## 6. Kontrak state dan service

Halaman React → service adapter → API client → backend. Adapter fixture hanya aktif pada `development` atau `staging` dengan konfigurasi eksplisit. Bentuk success/error/pagination konsisten sehingga migrasi tidak mengubah komponen.

Setiap operasi memiliki loading, success, empty, error, retry, dan abort behavior sesuai kebutuhan. Request mutation menggunakan idempotency key bila risiko submit berulang ada.

## 7. Definition of Done produksi

- API, database, storage, auth, RBAC, audit, dan backup berjalan di staging.
- Tidak ada data fixture yang masuk ke production environment.
- Tidak ada credential atau secret di bundle, localStorage, log, atau source map publik.
- Semua acceptance criteria PRD terpenuhi dan diuji dengan unit, integration, e2e, security, accessibility, dan performance checks.
- Profil publik hanya menampilkan data yang sudah diterbitkan.
- Admin action memiliki permission server dan audit event.
- SLO, alert, rollback, restore, dan incident runbook tersedia.
- Privacy notice, retention, consent, dan deletion flow ditinjau sebelum launch.

## 8. Di luar rilis awal

Domain custom, marketplace template, kolaborasi multi-editor, pembayaran, import massal, integrasi pihak ketiga, dan aplikasi native memerlukan scope serta persetujuan terpisah.
