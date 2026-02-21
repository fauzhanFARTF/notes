# Install PHP

Tentu, Fauzan! Berikut script one-time setup lengkap yang akan:

- ✅ Menginstal versi PHP yang umum dipakai (7.4, 8.0, 8.1, 8.2, 8.3) via shivammathur/php
- ✅ Menginstal dan mengonfigurasi php-version untuk auto-switch
- ✅ Menambahkan fungsi ke .zshrc agar otomatis switch saat masuk folder proyek
- ✅ (Opsional) Membuat file .php-version otomatis di semua folder proyek berdasarkan deteksi framework atau preferensi

## 📜 Nama File: setup-php-multi-version.sh

```bash
mkdir -p ~/Documents/scripts
mv ~/setup-php-multi-version.sh ~/Documents/scripts/
```

Simpan lalu jalankan sekali.

```bash
#!/bin/zsh

# =============================================================================
# One-Time Setup: Multi-Version PHP + Auto-Switch per Project
# Untuk Developer PHP Native (macOS + Homebrew)
# Oleh: Assistant (untuk Fauzan Nurrachman)
# =============================================================================

echo "🚀 Memulai setup multi-versi PHP..."

# --- LANGKAH 1: Pastikan Homebrew terinstal ---
if ! command -v brew &> /dev/null; then
    echo "❌ Homebrew belum terinstal. Menginstal sekarang..."
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"
fi

# --- LANGKAH 2: Tambahkan tap PHP ---
echo "🔧 Menambahkan tap shivammathur/php..."
brew tap shivammathur/php

# --- LANGKAH 3: Instal versi PHP yang dibutuhkan ---
PHP_VERSIONS=("7.4" "8.0" "8.1" "8.2" "8.3")

echo "📥 Menginstal versi PHP: ${PHP_VERSIONS[*]} ..."
for ver in "${PHP_VERSIONS[@]}"; do
    if brew list | grep -q "php@$ver"; then
        echo "✅ PHP $ver sudah terinstal. Melewati."
    else
        echo "📦 Menginstal PHP $ver..."
        brew install shivammathur/php/php@$ver
    fi
done

# --- LANGKAH 4: Instal php-version ---
echo "🔄 Menginstal php-version untuk switching..."
if ! command -v php-version &> /dev/null; then
    brew install php-version
else
    echo "✅ php-version sudah terinstal."
fi

# --- LANGKAH 5: Konfigurasi .zshrc ---
ZSHRC="$HOME/.zshrc"

# Tambahkan source php-version jika belum ada
if ! grep -q "php-version.sh" "$ZSHRC"; then
    echo 'source $(brew --prefix php-version)/php-version.sh' >> "$ZSHRC"
    echo "✅ Menambahkan php-version ke .zshrc"
fi

# Buat file auto-switch jika belum ada
AUTO_SWITCH_FILE="$HOME/.auto-php-version.sh"
if [ ! -f "$AUTO_SWITCH_FILE" ]; then
    cat > "$AUTO_SWITCH_FILE" << 'EOF'
# Auto-switch PHP version based on .php-version file
autoload -U add-zsh-hook
load-local-php-version() {
  if [[ -f .php-version ]]; then
    local version=$(cat .php-version | tr -d '[:space:]')
    if [[ -n "$version" ]]; then
      php-version use "$version" >/dev/null 2>&1
    fi
  fi
}
add-zsh-hook chpwd load-local-php-version
load-local-php-version
EOF
    echo "✅ Membuat file auto-switch: $AUTO_SWITCH_FILE"
fi

# Tambahkan source auto-switch ke .zshrc jika belum ada
if ! grep -q ".auto-php-version.sh" "$ZSHRC"; then
    echo 'source ~/.auto-php-version.sh' >> "$ZSHRC"
    echo "✅ Mengaktifkan auto-switch di .zshrc"
fi

# --- LANGKAH 6: (Opsional) Buat .php-version otomatis di proyek ---
read -p "📁 Masukkan path utama proyek Anda (misal: ~/Projects): " PROJECTS_DIR
PROJECTS_DIR="${PROJECTS_DIR/#\~/$HOME}"

if [ -d "$PROJECTS_DIR" ]; then
    echo "🔍 Mencari folder proyek di: $PROJECTS_DIR"

    # Cari semua folder yang mengandung file PHP
    find "$PROJECTS_DIR" -maxdepth 2 -type f \( -name "*.php" -o -name "composer.json" \) | \
    while read -r file; do
        dir=$(dirname "$file")

        # Lewati jika sudah ada .php-version
        if [ -f "$dir/.php-version" ]; then
            continue
        fi

        # Deteksi versi berdasarkan isi file (opsional)
        version="8.2"  # default

        # Contoh: jika ada Laravel < 9 → PHP 8.0, dll.
        if [ -f "$dir/composer.json" ]; then
            if grep -q '"laravel/framework":.*"8\.' "$dir/composer.json"; then
                version="8.0"
            elif grep -q '"laravel/framework":.*"9\.' "$dir/composer.json"; then
                version="8.1"
            elif grep -q '"php":.*"7\.4"' "$dir/composer.json"; then
                version="7.4"
            fi
        fi

        # Jika proyekmu adalah db_sekretariat → pakai 8.2
        if [[ "$dir" == *"db-sekretariat"* ]]; then
            version="8.2"
        fi

        echo "$version" > "$dir/.php-version"
        echo "📝 Membuat .php-version ($version) di: $dir"
    done
else
    echo "⚠️ Direktori proyek tidak ditemukan. Lewati pembuatan .php-version otomatis."
fi

# --- SELESAI ---
echo ""
echo "✅ SETUP SELESAI!"
echo ""
echo "Perintah cepat:"
echo "  php-version          → lihat daftar versi"
echo "  php-version 8.2      → switch manual ke PHP 8.2"
echo ""
echo "Mulai sekarang, setiap kali Anda 'cd' ke folder proyek yang memiliki .php-version,"
echo "versi PHP akan otomatis disesuaikan!"
echo ""
echo "🔁 Jangan lupa restart terminal atau jalankan: source ~/.zshrc"
```

## ▶️ Cara Menggunakan Script Ini

### Langkah 1: Simpan dan Beri Izin Eksekusi

```bash
cd ~
nano setup-php-multi-version.sh
# (paste isi script di atas)
chmod +x setup-php-multi-version.sh
```

### Langkah 2: Jalankan

```bash
./setup-php-multi-version.sh
```

### Langkah 3: Restart Terminal

```bash
source ~/.zshrc
# atau buka terminal baru
```

### 🧪 Contoh Hasil

Setelah selesai:

- Di ~/Projects/db-sekretariat/ → ada file .php-version berisi 8.2
- Di ~/Projects/legacy-app/ → .php-version berisi 7.4
- Saat kamu

```bash
cd ~/Projects/db-sekretariat
php -v
```

Output

```bash
PHP 8.2.12 (cli) ...
```
