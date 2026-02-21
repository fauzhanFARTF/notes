# bum

## 🔹 Apa itu bum?

bum (Bun Version Manager) adalah alat baris perintah (command-line tool) komunitas untuk mengelola beberapa versi Bun di sistem yang sama, ditulis dengan Rust untuk performa maksimal. Karena Bun adalah all-in-one JavaScript runtime (menggantikan Node.js, npm, yarn, webpack, dll), maka dengan mengganti versi Bun, kamu juga secara otomatis mengganti versi runtime, package manager, bundler, dan test runner yang digunakan.

## 🔹 Fungsi Utama bum

- Menginstal berbagai versi Bun (runtime + package manager + bundler + test runner).
- Beralih antar versi Bun per sesi shell atau per proyek.
- Menetapkan versi default atau global.
- Mendukung file .bumrc untuk auto-switch versi berdasarkan folder proyek.
- Tidak mengganggu instalasi Bun sistem atau global.
- Melihat daftar versi yang tersedia (termasuk canary/beta).
- Performa tinggi karena ditulis dengan Rust (zero overhead).

## 🔹 Cara Menginstall bum

### Di macOS, Linux, WSL

```bash
# 1. Install bum
# via Script (Disarankan untuk performa CLI terbaik)
curl -fsSL https://github.com/owenizedd/bum/raw/main/install.sh | bash

# Alternatif: via npm/npx (Jika sudah ada Node.js)
npm install -g @owenizedd/bum
# Atau tanpa install global:
npx @owenizedd/bum use 1.1.0

# 2. Restart terminal atau jalankan:
source ~/.bashrc
# atau
source ~/.zshrc
# atau
source ~/.bash_profile

# 3. Mengecek versi bum
bum --version

# 4. (Opsional) Install versi Bun pertama kali
bum install latest
```

💡 Alternatif Native Bun (tanpa bum):
Jika hanya butuh satu versi aktif, gunakan perintah resmi Bun:

```bash
# Update ke versi terbaru
bun upgrade

# Install versi spesifik
bun upgrade --bun 1.1.0

# Cek versi
bun --version
```

## 🔹 Cheat Sheet bum

```bash
# Lihat semua versi Bun yang sudah terinstal di bum
bum list

# Melihat versi Bun yang digunakan saat ini
bum current
# atau
bun --version

# Lihat versi Bun yang tersedia untuk diinstall
bum list-remote

# Install Bun versi tertentu
bum install 1.0.25
bum install 1.1.0
bum install 1.2.3

# Instal versi terbaru dari Bun (latest)
bum install latest

# Gunakan Bun versi tertentu (switch session)
# Jika versi belum terinstall, bum akan otomatis download dulu
bum use 1.1.0
bum use 1.2.3

# Hapus versi Bun tertentu
bum remove 1.0.25

# Auto-switch berdasarkan folder proyek (buat file .bumrc)
echo "1.1.0" > .bumrc
# Saat cd ke folder ini dan jalankan 'bum use' tanpa argumen,
# bum akan otomatis menggunakan versi dari .bumrc
```

### 🔹 Bonus: Integrasi dengan Shell Hook (Auto-Switch)

Agar bum bisa otomatis switch versi saat kamu cd ke folder proyek yang memiliki file .bumrc, tambahkan hook berikut di konfigurasi shell kamu:

```bash
# Untuk ~/.zshrc atau ~/.bashrc
if command -v bum &> /dev/null; then
  # Inisialisasi bum untuk auto-detect .bumrc
  eval "$(bum init)"
fi
```

Setelah restart terminal, setiap kali kamu masuk ke folder dengan file .bun-version, bum akan otomatis:

1. Mendeteksi versi di file .bun-version
2. Switch ke versi tersebut (jika sudah terinstall)
3. Restore versi sebelumnya saat keluar dari folder

## Perbandingan Singkat: Native vs bum

| Fitur                  | bun upgrade (Native)         | bum (Version Manager)      |
| ---------------------- | ---------------------------- | -------------------------- |
| Install versi spesifik | ✅ `bun upgrade --bun x.y.z` | ✅ `bum install x.y.z`     |
| Simpan banyak versi    | ❌ (hanya 1 aktif)           | ✅ (multi versi tersimpan) |
| Switch instan          | ❌ (harus download ulang)    | ✅ (langsung pakai)        |
| Auto-switch per folder | ❌                           | ✅ (via `.bumrc`)          |
| Support versi canary   | ✅                           | ✅                         |
| Performa CLI           | Native                       | ⚡ Rust (sangat cepat)     |
| Rekomendasi            | Pemula / 1 proyek            | Multi-proyek / Profesional |

### 🎯 Rekomendasi

Gunakan bum jika kamu bekerja di banyak proyek dengan requirement versi Bun berbeda dan menginginkan performa CLI terbaik (Rust-based). Gunakan bun upgrade jika kamu hanya butuh versi terbaru dan ingin setup yang lebih sederhana.
