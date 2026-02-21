# bvm

## 🔹 Apa itu bvm?

bvm (Bun Version Manager) adalah alat baris perintah (command-line tool) komunitas untuk mengelola beberapa versi Bun di sistem yang sama. Karena Bun adalah all-in-one JavaScript runtime (menggantikan Node.js, npm, yarn, webpack, dll), maka dengan mengganti versi Bun, kamu juga secara otomatis mengganti versi runtime, package manager, bundler, dan test runner yang digunakan.

## 🔹 Fungsi Utama bvm

- Menginstal berbagai versi Bun (runtime + package manager + bundler + test runner).
- Beralih antar versi Bun per sesi shell atau per proyek.
- Menetapkan versi default atau global.
- Mendukung file .bvmrc untuk auto-switch versi berdasarkan folder proyek.
- Tidak mengganggu instalasi Bun sistem atau global.
- Melihat daftar versi yang tersedia (termasuk canary/beta).

## 🔹 Cara Menginstall bvm

### Di macOS, Linux, WSL

```bash
# 1. Install bvm
# via curl
curl -fsSL https://bvm.cometkim.kr/install.sh | bash

# Alternatif: gunakan wget
wget -qO- https://bvm.cometkim.kr/install.sh | bash

# 2. Restart terminal atau jalankan:
source ~/.bashrc
# atau
source ~/.zshrc
# atau
source ~/.bash_profile

# 3. Mengecek versi bvm
bvm --version

# 4. (Opsional) Install versi Bun pertama kali
bvm install latest
bvm alias default latest
```

💡 Alternatif Native Bun (tanpa bvm):
Jika hanya butuh satu versi aktif, gunakan perintah resmi Bun:

```bash
# Update ke versi terbaru
bun upgrade

# Install versi spesifik
bun upgrade --bun 1.1.0

# Cek versi
bun --version
```

## 🔹 Cheat Sheet bvm

```bash
# Lihat semua versi Bun yang sudah terinstal di bvm
bvm ls

# Melihat versi Bun yang digunakan saat ini
bvm current
# atau
bun --version

# Lihat versi Bun yang tersedia untuk diinstall
bvm ls-remote

# Hanya tampilkan versi LTS atau stable
bvm ls-remote --stable

# Install Bun versi tertentu
bvm install 1.0.25
bvm install 1.1.0
bvm install 1.2.3

# Instal versi terbaru dari Bun (latest)
bvm install latest

# Instal versi canary/experimental
bvm install canary

# Gunakan Bun versi tertentu (switch session)
bvm use 1.1.0
bvm use 1.2.3

# Set versi default (untuk terminal baru)
bvm alias default 1.2.3

# Lihat semua alias yang tersedia
bvm alias

# Hapus versi Bun tertentu
bvm uninstall 1.0.25

# Auto-switch berdasarkan folder proyek (buat file .bvmrc)
echo "1.1.0" > .bvmrc
# Saat cd ke folder ini, bvm akan otomatis menggunakan versi 1.1.0
```

### 🔹 Bonus: Integrasi dengan Shell Hook (Auto-Switch)

Agar bvm bisa otomatis switch versi saat kamu cd ke folder proyek yang memiliki file .bvmrc, tambahkan hook berikut di konfigurasi shell kamu:

```bash
# Untuk ~/.zshrc atau ~/.bashrc
if command -v bvm &> /dev/null; then
  eval "$(bvm init -)"
fi
```

## Perbandingan Singkat: Native vs bvm

| Fitur                  | bun upgrade (Native)         | bvm (Version Manager)      |
| ---------------------- | ---------------------------- | -------------------------- |
| Install versi spesifik | ✅ `bun upgrade --bun x.y.z` | ✅ `bvm install x.y.z`     |
| Simpan banyak versi    | ❌ (hanya 1 aktif)           | ✅ (multi versi tersimpan) |
| Switch instan          | ❌ (harus download ulang)    | ✅ (langsung pakai)        |
| Auto-switch per folder | ❌                           | ✅ (via `.bvmrc`)          |
| Support versi canary   | ✅                           | ✅                         |
| Rekomendasi            | Pemula / 1 proyek            | Multi-proyek / Profesional |

### 🎯 Rekomendasi:

Gunakan bvm jika kamu bekerja di banyak proyek dengan requirement versi Bun berbeda. Gunakan bun upgrade jika kamu hanya butuh versi terbaru dan ingin setup yang lebih sederhana.
