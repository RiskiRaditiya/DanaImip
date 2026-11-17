# DanaImip — Sistem Informasi Manajemen Kas & Generator Persuratan Resmi Organisasi

![DanaImip Preview](banner_perbaikan.png)

> **DanaImip** adalah aplikasi web PWA (*Progressive Web App*) terpadu untuk tata kelola keuangan, pencatatan transaksi kas organisasi mahasiswa, serta generator berkas persuratan resmi berbasis format A4 presisi (PDF & Word `.doc`).

---

## 🌟 Fitur Utama

### 1. 📑 Generator Surat Resmi & SBA Presisi A4
- **Surat Undangan Resmi (SUD):** Lengkap dengan penomoran otomatis, metadata, penandatangan berlapis, dan tabel rundown lampiran.
- **Surat Perizinan Fasilitas (SPZ):** Terintegrasi dengan daftar fasilitas kampus, rundown peminjaman, serta lembar pengesahan.
- **Surat Permohonan (SPM):** Format modular 2 halaman A4 dengan rincian acara dan otorisasi bertingkat.
- **Surat Berita Acara (SBA):** Laporan pertanggungjawaban kegiatan, rincian susunan panitia, tabel prestasi, hambatan, hingga integrasi laporan realisasi anggaran.
- **Ekspor Dokumen:**
  - **Cetak / PDF 100% Bersih:** Layout standar A4 presisi tanpa watermark berulang ataupun pergeseran margin.
  - **Microsoft Word (.doc MHTML Engine):** Format `.doc` dengan tabel native, kop surat proporsional, serta watermark sentral berbasis header VML Word.

### 2. 💳 Manajemen Kas & Pembayaran Digital
- Pencatatan pembayaran uang kas anggota per bulan dengan nominal fleksibel.
- Dukungan metode pembayaran transfer & QRIS/E-Wallet (GoPay, OVO, ShopeePay).
- Unggah bukti pembayaran dan sinkronisasi otomatis ke Google Drive.

### 3. 📊 Dashboard Keuangan & Laporan Real-Time
- Visualisasi kas masuk, kas keluar, dan saldo operasional.
- Rekapitulasi per program kerja (Proker) dan kategori pengeluaran.
- Riwayat transaksi real-time dengan status verifikasi admin (Menunggu, Disetujui, Ditolak).

### 4. 📱 Progressive Web App (PWA) & Responsif
- Mendukung mode instalasi PWA di smartphone (Android/iOS) dan desktop.
- Dual theme (*Dark Mode* & *Light Mode* bernuansa Warm Cream).
- Mode offline dasar dengan Service Worker caching.

---

## 🛠️ Tech Stack & Arsitektur

- **Frontend:** Vanilla HTML5, Modern CSS / Tailwind CSS, JavaScript (ES6+)
- **Icons & UI:** Font Awesome 6, SweetAlert2, Plus Jakarta Sans & Times New Roman
- **Backend / Database:** Google Apps Script (`code.gs`) yang terhubung dengan Google Sheets & Google Drive
- **Penyimpanan Berkas:** Google Drive API (via Apps Script DriveApp)
- **Notifikasi:** Firebase Cloud Messaging (FCM HTTP v1)

---

## 🚀 Panduan Setup & Konfigurasi Mandiri

Jika Anda ingin menjalankan atau mengembangkan proyek ini:

### 1. Clone Repository
```bash
git clone https://github.com/RiskiRaditiya/DanaImip.git
cd DanaImip
```

### 2. Konfigurasi Backend (Google Apps Script)
1. Buat **Google Spreadsheet** baru di Google Drive Anda.
2. Buat lembar kerja dengan nama sheet sesuai kebutuhan: `users`, `transaksi`, `program_kerja`, `detail_kas_bulan`.
3. Buka menu **Extensions > Apps Script**, lalu salin isi file [`code.gs`](code.gs) ke editor skrip.
4. Di Apps Script, masuk ke **Project Settings > Script Properties** dan tambahkan properti:
   - `ADMIN_SECRET_KEY`: Token rahasia otentikasi admin Anda.
   - `FIREBASE_PROJECT_ID` *(opsional)*: Untuk notifikasi push Firebase.
   - `FIREBASE_CLIENT_EMAIL` *(opsional)*.
   - `FIREBASE_PRIVATE_KEY` *(opsional)*.
5. Lakukan **Deploy as Web App**:
   - *Execute as:* **Me**
   - *Who has access:* **Anyone**
6. Salin URL Deployment yang dihasilkan (misal: `https://script.google.com/macros/s/AKfycb.../exec`).

### 3. Konfigurasi Frontend
Perbarui konstanta `GOOGLE_SCRIPT_URL` pada file HTML terkait (atau gunakan referensi `config.example.js`) dengan URL Deployment Apps Script Anda:
```javascript
const GOOGLE_SCRIPT_URL = "https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec";
```

### 4. Menjalankan Aplikasi
Aplikasi ini berjalan sebagai *client-side static web app*. Anda bisa menjalankannya langsung:
- Menggunakan ekstensi **Live Server** di VS Code.
- Menggunakan server lokal sederhana:
  ```bash
  npx serve .
  # atau
  python -m http.server 8080
  ```
- Deploy ke penyedia hosting statis seperti **Netlify**, **Vercel**, atau **GitHub Pages**.

---

## 📂 Struktur Proyek

```text
├── index.html                 # Halaman utama / portal login
├── dasboard.html              # Dashboard keuangan & ringkasan kas
├── buat-surat.html            # Generator surat resmi (SUD, SPZ, SPM, SBA)
├── folder-surat.html          # Manajemen arsip dokumen surat
├── pembayaran-kas.html        # Form pembayaran kas anggota
├── laporan-keuangan.html      # Rekapitulasi laporan keuangan komprehensif
├── lihat-kegiatan.html        # Daftar kegiatan & timeline proker
├── detail-kegiatan.html       # Rincian per kegiatan & anggaran
├── riwayat-transaksi.html     # Daftar seluruh mutasi transaksi kas
├── Admin/                     # Halaman khusus pengelolaan & verifikasi admin
├── code.gs                    # Backend REST API Google Apps Script
├── config.example.js          # Contoh konfigurasi URL deployment
├── data-sample/               # Skema & data tiruan (dummy data) untuk testing
│   ├── users.sample.csv
│   ├── transaksi.sample.csv
│   └── program_kerja.sample.csv
├── sw.js                      # Service Worker (PWA offline caching)
├── manifest.json              # Web App Manifest PWA
└── surat/assets/              # Aset kop surat resmi, stempel & watermark
```

---

## 🔒 Kebijakan Privasi & Keamanan (Open Source Sanitization)
Repository ini telah disanitasi khusus untuk portofolio publik:
- Seluruh data anggota, riwayat transaksi nyata, serta berkas CSV produksi telah dikeluarkan dan digantikan dengan data contoh (*mock data* di folder `data-sample/`).
- Token autentikasi dan ID deployment backend telah diganti dengan *placeholder template* agar aman dari penyalahgunaan.

---

## 👤 Penulis / Pengembang
**Riski Raditiya**  
*Bendahara & Pengembang Web Organisasi*  
GitHub: [@RiskiRaditiya](https://github.com/RiskiRaditiya)

---

## 📄 Lisensi
Proyek ini dilisensikan di bawah [MIT License](LICENSE) — bebas digunakan dan dipelajari untuk pengembangan sistem informasi organisasi mahasiswa.
