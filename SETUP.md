# 🚀 PANDUAN SETUP — Aktivitas Harian Tim

Ikuti langkah-langkah berikut untuk menghubungkan aplikasi ke Google Sheets secara real-time.

---

## LANGKAH 1 — Buat Google Spreadsheet

1. Buka [sheets.google.com](https://sheets.google.com) → klik **+ Blank**
2. Beri nama spreadsheet, misalnya: **"Aktivitas Harian Tim 2026"**
3. Salin **ID Spreadsheet** dari URL browser:
   ```
   https://docs.google.com/spreadsheets/d/  >>>INI_ID_NYA<<<  /edit
   ```

---

## LANGKAH 2 — Deploy Google Apps Script

1. Di spreadsheet, klik menu **Extensions → Apps Script**
2. Hapus semua kode yang ada, lalu **salin-tempel seluruh isi file `Code.gs`**
3. Pada baris pertama yang bertuliskan:
   ```javascript
   const SPREADSHEET_ID = 'GANTI_DENGAN_ID_SPREADSHEET_ANDA';
   ```
   Ganti `GANTI_DENGAN_ID_SPREADSHEET_ANDA` dengan ID dari Langkah 1
4. Klik **💾 Save** (Ctrl+S)
5. Jalankan fungsi `initSheets` sekali untuk membuat sheet otomatis:
   - Dropdown fungsi → pilih **initSheets** → klik **▶ Run**
   - Izinkan akses saat diminta (klik **Allow**)
6. Klik **Deploy → New Deployment**
7. Pilih type: **Web App**
8. Isi form:
   - **Execute as:** Me
   - **Who has access:** Anyone ← *penting agar tim bisa akses*
9. Klik **Deploy** → **Authorize Access** → **Allow**
10. Salin **Web App URL** yang muncul (diawali `https://script.google.com/macros/...`)

---

## LANGKAH 3 — Hubungkan ke index.html

1. Buka file `index.html` dengan teks editor
2. Cari baris:
   ```javascript
   const API_URL = 'GANTI_DENGAN_URL_APPS_SCRIPT_ANDA';
   ```
3. Ganti nilainya dengan URL dari Langkah 2, contoh:
   ```javascript
   const API_URL = 'https://script.google.com/macros/s/AKfycbxXXXXX/exec';
   ```
4. Simpan file

---

## LANGKAH 4 — Hosting Online (Agar Tim Bisa Akses)

Pilih salah satu cara:

### Opsi A — GitHub Pages (Gratis, Mudah)
1. Buat akun [github.com](https://github.com) jika belum ada
2. Buat repository baru → upload `index.html`
3. Masuk Settings → Pages → Source: **main branch**
4. Akses via: `https://username.github.io/nama-repo/`

### Opsi B — Netlify (Drag & Drop)
1. Buka [netlify.com](https://netlify.com) → login
2. Drag & drop folder berisi `index.html` ke halaman Netlify
3. Dapat URL otomatis dalam hitungan detik

### Opsi C — Google Sites (Embed)
1. Buka [sites.google.com](https://sites.google.com)
2. Buat halaman baru → Insert → **Embed** → paste kode HTML

---

## STRUKTUR GOOGLE SHEETS (Otomatis Dibuat)

### Sheet "Laporan"
| Kolom | Isi |
|-------|-----|
| ID | ID unik laporan |
| Timestamp | Waktu pengiriman |
| Nama Staff | Nama pelapor |
| Tanggal | Tanggal aktivitas |
| Status Kehadiran | Hadir/WFH/Izin/Sakit/Cuti |
| Leads Baru Masuk | Angka |
| Leads Di-Follow-up | Angka |
| Leads Hasil Follow-up | Angka |
| Leads Terkonversi | Angka |
| **Conversion Rate (%)** | **Dihitung otomatis** |
| Metode Follow-up | Telepon, WA, Email, dst |
| Tindakan yang Dilakukan | Teks bebas |
| Checklist Aktivitas | Daftar centang |
| Aktivitas Lainnya | Teks opsional |
| Hambatan | Teks bebas |
| Rencana Besok | Teks bebas |

> 💡 **Kolom Conversion Rate otomatis berwarna:**
> - 🟢 Hijau: ≥ 70% (Tinggi)
> - 🟡 Kuning: 40–69% (Sedang)
> - 🔴 Merah: < 40% (Perlu perhatian)

### Sheet "Staff"
Berisi daftar nama staff yang muncul di dropdown. Tambah/edit langsung di sheet ini.

---

## CARA BUAT DASHBOARD EKSEKUTIF DI GOOGLE SHEETS

Setelah data masuk, buat sheet baru bernama **"Dashboard"**:

1. **Pivot Table**: Insert → Pivot Table → dari sheet Laporan
   - Rows: Nama Staff
   - Values: SUM Leads Baru, SUM FU, SUM Konversi, AVG CVR

2. **Chart Konversi per Staff**:
   - Pilih kolom Nama + CVR → Insert → Chart → Bar Chart

3. **Slicer untuk filter tanggal**:
   - Data → Add a Slicer → pilih kolom Tanggal

4. **Share dengan Pimpinan**: Klik Share → masukkan email → Viewer

---

## TIPS

- **Tim mengakses** `index.html` via URL hosting → isi form → data langsung masuk Sheets
- **Rekap otomatis refresh** setiap 30 detik
- **Conversion Rate** dihitung: `(Leads Terkonversi ÷ Leads Di-Follow-up) × 100%`
- Tambah staff baru langsung di sheet **"Staff"** kolom A
- Untuk backup: File → Download → Excel (.xlsx)

---

## BANTUAN

Jika ada kendala saat setup, hubungi tim IT atau cek:
- [Apps Script Docs](https://developers.google.com/apps-script)
- [Google Sheets API](https://developers.google.com/sheets)
