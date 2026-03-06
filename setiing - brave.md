# 🌐 Panduan Setup & Sinkronisasi Browser

Dokumentasi ini berisi prosedur standar untuk pengaturan browser (Brave, Chrome, Arc) di berbagai perangkat, termasuk sinkronisasi data, migrasi, dan keamanan.

---

## 📋 Daftar Isi

1. [Tujuan](#tujuan)
2. [Prasyarat](#prasyarat)
3. [Skenario 1: Sinkronisasi Brave Multi-PC](#skenario-1-sinkronisasi-brave-multi-pc)
4. [Skenario 2: Migrasi Data (Chrome/Arc ↔ Brave)](#skenario-2-migrasi-data-chromearc--brave)
5. [Skenario 3: Manajemen Password Cross-Browser](#skenario-3-manajemen-password-cross-browser)
6. [Keamanan & Privasi](#keamanan--privasi)
7. [Troubleshooting](#troubleshooting)
8. [Checklist Setup Awal](#checklist-setup-awal)

---

## 🎯 Tujuan

- Memastikan konsistensi data (bookmark, password, history) across devices.
- Memudahkan migrasi saat mengganti browser atau perangkat baru.
- Menjaga keamanan data sensitif selama proses transfer.

---

## ✅ Prasyarat

- [ ] Browser terinstal (Brave, Chrome, atau Arc) versi terbaru.
- [ ] Koneksi internet stabil.
- [ ] Aplikasi Password Manager (disarankan: Bitwarden/1Password) untuk cross-browser sync.
- [ ] Media penyimpanan aman untuk backup file ekspor (`.html`, `.csv`).

---

## 🔄 Skenario 1: Sinkronisasi Brave Multi-PC

_Digunakan untuk menyinkronkan beberapa perangkat yang semuanya menggunakan Brave Browser._

### Langkah Setup Sync Chain

1. **PC Utama (Inisiator):**
   - Buka `Menu` → **Brave Sync**.
   - Pilih **Start a new Sync Chain** → **Computer**.
   - **PENTING:** Salin **Kode Sync 24 Kata**. Simpan di tempat aman (Password Manager).
2. **PC Tambahan (Client):**
   - Buka `Menu` → **Brave Sync**.
   - Pilih **Enter a sync code**.
   - Masukkan 24 kata dari PC Utama.
   - Pastikan status terhubung ✅.

### Data yang Disinkronkan

- [ ] Bookmark
- [ ] Password
- [ ] History
- [ ] Extensions
- [ ] Tab Terbuka

> ⚠️ **Catatan:** Sync ini hanya bekerja antar perangkat Brave. Tidak bisa sinkron live dengan Chrome/Arc.

---

## 📥 Skenario 2: Migrasi Data (Chrome/Arc ↔ Brave)

_Digunakan untuk pindah browser atau menggabungkan data dari browser lain. Ini adalah proses satu kali (one-time import), bukan sync live._

### A. Dari Chrome ke Brave

1. Tutup browser Chrome sepenuhnya.
2. Di Brave: Buka `Menu` → **Import Bookmarks and Settings**.
3. Pilih **Google Chrome**.
4. Centang data yang diinginkan (Bookmark, Password, History).
5. Klik **Import**.

### B. Dari Brave ke Arc

1. Tutup browser Brave sepenuhnya.
2. Di Arc: Buka **Menu** → **Import from Another Browser**.
3. Pilih **Brave**.
4. Pilih data yang ingin dipindahkan.
5. Klik **Import**.

### C. Export/Import Manual (Bookmark)

Jika import otomatis gagal:

1. **Export:** `Browser` → Bookmark Manager → Export to `.html`.
2. **Import:** `Browser Tujuan` → Bookmark Manager → Import `.html`.

---

## 🔐 Skenario 3: Manajemen Password Cross-Browser

_Karena Brave, Chrome, dan Arc tidak bisa sinkron password secara native antar satu sama lain, gunakan Password Manager Pihak Ketiga._

### Rekomendasi

- **Bitwarden** (Gratis, Open Source, Enkripsi End-to-End)
- **1Password** (Berbayar, Fitur Lengkap)
- **KeePassXC** (Local Storage, Offline)

### Langkah Migrasi Password

1. **Export dari Browser Lama:**
   - Masuk ke pengaturan Password.
   - Pilih **Export Passwords** (Format `.csv`).
   - ⚠️ **Peringatan:** File ini tidak terenkripsi!
2. **Import ke Password Manager:**
   - Buka vault Bitwarden/1Password.
   - Pilih **Import Data** → Upload file `.csv`.
3. **Hapus File CSV:**
   - Segera hapus file `.csv` dari komputer dan kosongkan Trash/Recycle Bin.
4. **Instal Extension:**
   - Pasang extension Password Manager di semua browser (Brave, Chrome, Arc).

---

## 🛡️ Keamanan & Privasi

1. **Kode Sync Brave:** Jangan pernah membagikan kode 24 kata kepada siapa pun.
2. **File Ekspor:** Selalu hapus file `.html` (bookmark) dan `.csv` (password) setelah proses selesai.
3. **Enkripsi:** Jika harus menyimpan backup, enkripsi file menggunakan VeraCrypt atau zip password.
4. **Perangkat Terpercaya:** Hanya lakukan sync pada perangkat yang Anda miliki secara fisik.

---

## 🛠️ Troubleshooting

| Masalah                   | Solusi                                                                                           |
| ------------------------- | ------------------------------------------------------------------------------------------------ |
| **Sync tidak terhubung**  | Pastikan versi Brave sama di semua PC. Coba "Leave Sync Chain" lalu ulang.                       |
| **Password tidak muncul** | Cek apakah fitur sync password diaktifkan di pengaturan Sync.                                    |
| **Import Gagal**          | Pastikan browser sumber (misal: Chrome) sedang **tidak berjalan** (close process di background). |
| **Bookmark Duplikat**     | Gunakan extension seperti "Bookmark Dupes" untuk membersihkan setelah import.                    |

---

## ✅ Checklist Setup Awal

### PC Baru / Install Ulang

- [ ] Instal Browser Utama (Brave/Arc).
- [ ] Instal Extension Password Manager.
- [ ] Lakukan Sync Chain (Jika sesama Brave).
- [ ] Import Bookmark (Jika dari browser lain).
- [ ] Verifikasi Login Website Penting (Email, Bank, Sosmed).
- [ ] Hapus file backup sementara (`.csv`, `.html`).
- [ ] Update Browser ke versi terbaru.

---

## 📞 Kontak & Dukungan

Jika terjadi kendala teknis yang tidak tercover di sini, hubungi tim IT atau kunjungi:

- [Brave Support](https://support.brave.com/)
- [Arc Support](https://arc.net/support)
- [Chrome Help](https://support.google.com/chrome/)

---

_Last Updated: Oktober 2023_
