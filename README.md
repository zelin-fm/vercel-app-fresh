# Skill Matrix Intelligence — Insentif Cutting Kulit (Live)

Dashboard statis (HTML/CSS/JS murni, tanpa build step) yang menarik data
**langsung dari Google Sheets "COBA INSENTIF"** saat halaman dibuka —
auto-sync tiap 5 menit, atau klik tombol "Sync Sekarang".

Kolom yang ditampilkan: SPV, NAMA, NO. ABSEN, LINE, MASA KERJA (TAHUN), TAHUN,
BULAN, STYLE, PROSES, RATA-RATA KAPASITAS, %EFFISIENSI, LEVEL SKILL, %REPAIR,
STATUS, REKOMENDASI TREATMENT, REKOMENDASI INSENTIF.

## ⚠️ WAJIB: sharing sheet harus publik (view-only)

Karena datanya ditarik langsung dari browser pengunjung (bukan dari server),
sheet **wajib** di-set:

1. Buka Google Sheets "COBA INSENTIF"
2. Klik **Share** (kanan atas) → **General access** → ubah jadi
   **"Anyone with the link"**, role **Viewer**
3. Simpan

Kalau ini belum di-set, dashboard akan menampilkan pesan error "Gagal ambil
data dari Google Sheets" dan meminta sharing diaktifkan. Datanya tetap
read-only untuk publik — orang yang cuma punya link tidak bisa mengedit.

## Penting soal nama kolom di Sheet

Aplikasi ini mencocokkan **nama header** kolom (case-insensitive), jadi kalau
nama kolom di sheet berubah, mapping ikut berubah otomatis. Yang penting:
- Kolom `REKOMENDASI` (atau `REKOMENDASI TREATMENT`) → tampil sebagai
  "Rekomendasi Treatment"
- Kolom `REKOMENDASI INSENTIF` harus persis bernama itu supaya terbaca.
  Kalau belum ditemukan, dashboard tetap jalan tapi kolom itu kosong dan
  ada banner pemberitahuan di atas.

## Deploy ke Vercel

### Opsi A — Vercel CLI
```
npm i -g vercel
cd vercel-app
vercel --prod
```

### Opsi B — Drag & drop
Buka https://vercel.com/new → drag folder ini → Deploy.

### Opsi C — GitHub (disarankan, biar auto-redeploy)
Repo git lokal sudah ada. Push ke GitHub:
```
git remote add origin https://github.com/USERNAME/insentif-cutting-kulit.git
git branch -M main
git push -u origin main
```
Lalu import repo itu di https://vercel.com/new (framework preset: Other,
tanpa build command).

## Update data

Karena live-sync langsung dari Sheets, **tidak perlu redeploy** untuk update
data — cukup edit sheet-nya, dashboard otomatis sinkron ulang (maks. 5 menit,
atau langsung klik "Sync Sekarang"). Redeploy hanya diperlukan kalau mau
mengubah tampilan/kode aplikasinya sendiri.

## Kalau live-fetch tetap gagal (CORS diblokir Google)

Sangat jarang terjadi untuk sheet yang publik, tapi kalau tetap gagal,
alternatifnya: di Google Sheets, pakai **File → Share → Publish to web**
(bukan cuma "Share" biasa), pilih format CSV, lalu ganti nilai `CSV_URL` di
`index.html` dengan link hasil publish tersebut.
