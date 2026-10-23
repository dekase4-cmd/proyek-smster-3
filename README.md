# DeksLink

DeksLink adalah platform bio-link profesional. Dokumen produk dan desain saat ini menargetkan implementasi production-ready:

- `PRD.md` — requirement produk produksi, keamanan, data, dan acceptance criteria.
- `UI-GUIDELINE.md` — sistem visual editorial SaaS, responsive behavior, accessibility, dan copy.
- `IMPLEMENTATION_PLAN.md` — roadmap dari baseline frontend menuju API, auth, staging, dan launch.
- `AGENTS.md` — kontrak kerja perubahan pada repository.
- `QA_REPORT.md` — pemeriksaan aktual baseline frontend.

## Menjalankan baseline frontend

Gunakan Node yang memenuhi kebutuhan Vite (20.19+ atau 22.12+), lalu:

```sh
npm install
npm run dev
```

Buka alamat Local yang dicetak Vite. Baseline yang ada masih memakai fixture di memori untuk pengembangan. Itu bukan penyimpanan produksi dan belum menyediakan backend, session server, email, media storage, atau deployment.

## Jalur menuju produksi

Ikuti fase P1–P8 pada `IMPLEMENTATION_PLAN.md`: kontrak API dan data, identity/session, profile/media/publish, links/theme, public SEO, admin/RBAC, hardening, lalu staging dan launch. Frontend tidak boleh menyebut fixture sebagai data produksi.

## Pemeriksaan baseline

```sh
npm run lint
npm run build
```

Sebelum launch, tambahkan unit/integration/e2e, security, accessibility, performance, backup/recovery, dan observability checks sesuai PRD produksi.
