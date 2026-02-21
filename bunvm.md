# bunvm

## 🔹 Apa itu bunvm?

bunvm (BunVM) adalah alat baris perintah (command-line tool) komunitas yang ringan dan cepat untuk mengelola beberapa versi Bun di sistem yang sama. Dibangun dengan pure shell script dan zero dependencies, bunvm fokus pada kesederhanaan, kecepatan, dan pengalaman developer yang mulus tanpa perlu instalasi tambahan.

## 🔹 Fungsi Utama bunvm

- Menginstal berbagai versi Bun (runtime + package manager + bundler + test runner).
- Beralih antar versi Bun per sesi shell atau per proyek.
- Menetapkan versi default atau global.
- Mendukung file .bun-version untuk auto-switch otomatis saat masuk folder proyek.
- Tidak mengganggu instalasi Bun sistem atau global.
- Melihat daftar versi yang tersedia (termasuk canary/beta).
- Tab completion cerdas untuk Bash dan Zsh.
- Zero dependencies: murni shell script, tidak butuh Rust/Node.js runtime.

## 🔹 Cara Menginstall bunvm

### Di macOS, Linux, WSL

```bash
# 1. Install bunvm
# via curl
curl -fsSL https://install.bunvm.com | bash

# Alternatif: gunakan wget
wget -qO- https://install.bunvm.com | bash

# 2. Restart terminal atau jalankan:
source ~/.bashrc
# atau
source ~/.zshrc
# atau
source ~/.bash_profile

# 3. Mengecek versi bunvm
bunvm --version

# 4. (Opsional) Install versi Bun pertama kali
bunvm install latest
bunvm alias default latest
```

💡 Alternatif Native Bun (tanpa bunvm):
Jika hanya butuh satu versi aktif, gunakan perintah resmi Bun:

```bash
# Update ke versi terbaru
bun upgrade

# Install versi spesifik
bun upgrade --bun 1.1.0

# Cek versi
bun --version
```

## 🔹 Cheat Sheet bunvm

```bash
# Lihat semua versi Bun yang sudah terinstal di bunvm (lokal)
bunvm list --local

# Melihat versi Bun yang digunakan saat ini
bunvm current
# atau
bun --version

# Lihat versi Bun yang tersedia untuk diinstall (remote)
bunvm list

# Install Bun versi tertentu
bunvm install 1.0.25
bunvm install 1.1.0
bunvm install 1.2.3

# Instal versi terbaru dari Bun (latest)
bunvm install latest

# Gunakan Bun versi tertentu (switch session - persisten)
bunvm use 1.1.0
bunvm use 1.2.3

# Buat alias versi (misal: 'stable' untuk 1.1.0)
bunvm alias stable 1.1.0
bunvm alias beta 1.2.0

# Gunakan alias
bunvm use stable

# Hapus versi Bun tertentu
bunvm uninstall 1.0.25

# Update bunvm ke versi terbaru
bunvm selfupdate

# Auto-switch berdasarkan folder proyek (buat file .bun-version)
echo "1.1.0" > .bun-version
# Saat cd ke folder ini, bunvm otomatis switch ke 1.1.0! 🎉
```

### 🔹 Bonus: Integrasi dengan Shell Hook (Auto-Switch)

bunvm sudah mendukung auto-switching otomatis saat kamu cd ke folder proyek yang memiliki file .bun-version. Pastikan inisialisasi shell sudah terpasang (biasanya otomatis saat install):

```bash
# Untuk ~/.zshrc atau ~/.bashrc (jika belum otomatis)
if command -v bunvm &> /dev/null; then
  eval "$(bunvm init)"
fi
```

Setelah restart terminal, setiap kali kamu masuk ke folder dengan file .bun-version, bunvm akan otomatis:

1. Mendeteksi versi di file .bun-version
2. Switch ke versi tersebut (jika sudah terinstall)
3. Restore versi sebelumnya saat keluar dari folder

## Perbandingan Singkat: Native vs bunvm

| Fitur                  | bun upgrade (Native)         | bunvm (Version Manager)    |
| ---------------------- | ---------------------------- | -------------------------- |
| Install versi spesifik | ✅ `bun upgrade --bun x.y.z` | ✅ `bunvm install x.y.z`   |
| Simpan banyak versi    | ❌ (hanya 1 aktif)           | ✅ (multi versi tersimpan) |
| Switch instan          | ❌ (harus download ulang)    | ✅ (langsung pakai)        |
| Auto-switch per folder | ❌                           | ✅ (via `.bun-version`)    |
| Support versi canary   | ✅                           | ✅                         |
| Dependencies           | Tidak ada                    | ✅ Zero (pure shell)       |
| Tab completion         | ❌                           | ✅ Bash & Zsh              |
| Rekomendasi            | Pemula / 1 proyek            | Multi-proyek / Profesional |

### 🎯 Rekomendasi

Gunakan bunvm jika kamu bekerja di banyak proyek dengan requirement versi Bun berbeda. Gunakan bun upgrade jika kamu hanya butuh versi terbaru dan ingin setup yang lebih sederhana.
