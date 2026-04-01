# Panduan Multi-Version PostgreSQL di macOS (Homebrew)

Ya, Anda bisa menginstal dan mengelola beberapa versi PostgreSQL secara bersamaan di sistem yang sama, mirip seperti cara Anda menggunakan sphp untuk berpindah antar versi PHP di macOS.
Namun, PostgreSQL tidak menyediakan mekanisme switching global bawaan seperti PHP, karena:
PostgreSQL adalah server proses, bukan sekadar CLI tool.
Setiap versi biasanya berjalan di port berbeda dan memiliki data directory terpisah.
Switching "aktif" berarti mengatur service mana yang berjalan & port mana yang dipakai.

## ✅ Solusi Profesional: Multi-Version PostgreSQL dengan Homebrew

Karena Anda pengguna macOS + Homebrew, berikut adalah pendekatan terbaik untuk mengelola beberapa versi.

### 🔹 Langkah 1: Install Beberapa Versi PostgreSQL via Homebrew

Homebrew tidak menautkan (link) versi lama secara default untuk menghindari konflik. Jadi semua versi tetap terinstal tapi tidak aktif

```bash
# Contoh: Install versi 14 dan 15
brew install postgresql@14
brew install postgresql@15
brew install postgresql@16
```

### 🔹 Langkah 2: Buat Skrip spg (Switch PostgreSQL)

1. Buat skrip khusus untuk mempermudah switching, mirip seperti sphp pada PHP.
   Pastikan folder bin lokal ada:

   ```bash
   mkdir -p ~/.local/bin
   ```

2. Buat file ~/.local/bin/spg:

   ```bash
   nano ~/.local/bin/spg
   ```

3. Isi dengan skrip berikut:

   ```bash
   #!/bin/zsh

   if [ -z "$1" ]; then
   echo "Usage: spg <version>"
   echo "Example: spg 14"
   echo "Available versions: 14, 15, 16..."
   return 1
   fi

   VERSION=$1
   FORMULA="postgresql@$VERSION"
   DATA_DIR="/opt/homebrew/var/postgresql@$VERSION"
   LOG_FILE="/opt/homebrew/var/log/postgresql@$VERSION.log"
   PID_FILE="/opt/homebrew/var/postgresql@$VERSION/postmaster.pid"

   # Cek apakah versi terinstal

   if ! brew list | grep -q $FORMULA; then
   echo "❌ PostgreSQL $VERSION not installed!"
   echo "Install with: brew install $FORMULA"
   return 1
   fi

   echo "🛑 Force stopping ALL PostgreSQL services..."

   # Stop semua service postgres via brew

   for pg_ver in 14 15 16 17 18; do
   brew services stop postgresql@$pg_ver 2>/dev/null
   done
   brew services stop postgresql 2>/dev/null

   # Tunggu proses stop

   sleep 3

   # Force kill jika masih ada proses postgres

   echo "🔍 Checking for lingering postgres processes..."
   PG_PIDS=$(pgrep -f "postgres" 2>/dev/null)
   if [ ! -z "$PG_PIDS" ]; then
   echo "⚠️ Found lingering processes, force killing..."
   pkill -9 -f "postgres" 2>/dev/null
   sleep 2
   fi

   # Pastikan port 5432 bebas

   echo "🔍 Checking port 5432..."
   if lsof -i :5432 >/dev/null 2>&1; then
   echo "⚠️ Port 5432 still in use! Killing process..."
   lsof -ti :5432 | xargs kill -9 2>/dev/null
   sleep 2
   fi

   # Unlink semua versi

   echo "🔗 Unlinking all PostgreSQL versions..."
   for pg_ver in 14 15 16 17 18; do
   brew unlink postgresql@$pg_ver 2>/dev/null
   done
   brew unlink postgresql 2>/dev/null

   # Link versi yang dipilih

   echo "🔗 Linking PostgreSQL $VERSION..."
   brew link $FORMULA --force

   # Cek & init data directory jika belum ada

   if [ ! -d "$DATA_DIR" ] || [ ! -f "$DATA_DIR/PG_VERSION" ]; then
   echo "📁 Initializing data directory..."
   mkdir -p $DATA_DIR
   initdb $DATA_DIR
   fi

   # Fix permission

   chown -R $(whoami) $DATA_DIR 2>/dev/null

   # Start service

   echo "🚀 Starting PostgreSQL $VERSION..."
   brew services start $FORMULA

   # Wait for service to start

   sleep 5

   # Verify

   echo "🔍 Verifying..."
   if brew services list | grep -q "$FORMULA.\*started"; then
   echo ""
   echo "✅ Successfully switched to PostgreSQL $VERSION"
   echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"
   psql --version
   psql -c "SELECT version();" 2>/dev/null
   echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"
   else
   echo ""
   echo "❌ Failed to start PostgreSQL $VERSION"
   echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"
   echo "Debug info:"
   brew services info $FORMULA
   echo ""
   echo "Check logs: tail -n 50 $LOG_FILE"
   echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"
   return 1
   fi
   ```

4. Beri izin eksekusi:

   ```bash
      chmod +x ~/.local/bin/spg
   ```

   (Pastikan ~/.local/bin sudah ada di $PATH Anda)
   - Cara menambahkan ke path

   ```bash
   echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
   source ~/.zshrc
   ```

### 🔹 Langkah 3: Inisialisasi Data Directory

Setiap versi butuh data directory sendiri. Lakukan ini hanya sekali untuk setiap versi baru.

```bash
# Contoh untuk versi 15
initdb /opt/homebrew/var/postgresql@15
```

> **Catatan:**Lokasi ini sesuai dengan konfigurasi Homebrew. Cek lokasi pastinya dengan perintah: brew info postgresql@15.

### 🔹 Langkah 4: Jalankan Service Versi Tertentu

Gunakan skrip spg yang sudah dibuat, atau jalankan manual via brew services.

```bash
# Menggunakan skrip spg
spg 15

# Atau manual
brew services start postgresql@15
```

Hasil:
psql, pg_dump, createdb → otomatis pakai versi 15.
Server jalan di port default 5432.

#### 🔄 Menjalankan Dua Versi Sekaligus

Jika ingin menjalankan dua versi bersamaan, edit konfigurasi masing-masing agar pakai port berbeda.

1. Edit konfigurasi (misal versi 14):

   ```bash
   nano /opt/homebrew/var/postgresql@14/postgresql.conf
   ```

   Ubah baris port:

   ```conf
   port = 5433
   ```

2. Start manual:

   ```bash
   brew services start postgresql@14
   ```

   ### 🔹 Verifikasi Versi Aktif

   ```bash
   # Cek versi client
   psql --version


   # Cek versi server yang terhubung
   psql -c "SELECT version();"
   ```

   ### 📌 Catatan Penting

   | Aspek               | Penjelasan                                                                                                                                       |
   | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
   | Kompatibilitas Data | Data tidak kompatibel lintas versi mayor. Backup/restore wajib saat pindah versi (gunakan `pg_dump`).                                            |
   | Port Conflict       | Hanya satu versi boleh pakai port 5432. Versi lain harus ganti port (misal 5433, 5434).                                                          |
   | Extension (PostGIS) | Harus diinstal ulang di tiap versi. `brew install postgis` hanya untuk versi default. Untuk versi spesifik: jalankan `CREATE EXTENSION postgis`. |
   | Environment         | Tools seperti pgAdmin atau Python (`psycopg2`) akan terhubung ke **port**, bukan “versi”. Pastikan Anda tahu port yang digunakan.                |

   ### 💡 Alternatif: Gunakan Docker (Lebih Fleksibel)

   Jika Anda sering ganti-ganti versi atau butuh isolasi penuh, pertimbangkan Docker.

   ```bash
   # Contoh menjalankan PostgreSQL 15 di Docker
   docker run --name postgres-15 -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres:15
   ```

   Keuntungan:
   - Tidak campur aduk dengan sistem host.
   - Bisa jalankan banyak versi sekaligus (beda port container).
   - Termasuk PostGIS langsung (gunakan image postgis/postgis).

## 🔚 Kesimpulan

Ya, Anda bisa install & switch antar versi PostgreSQL, tapi caranya berbeda dari PHP karena sifatnya sebagai database server.
Rekomendasi untuk Anda:
Gunakan Homebrew + skrip spg jika ingin native, ringan, dan terintegrasi dengan sistem macOS.
Gunakan Docker jika butuh fleksibilitas maksimal & isolasi sempurna (terutama untuk proyek GIS dengan PostGIS).
Jika Anda membutuhkan bantuan lebih lanjut, saya bisa bantu:
Generate skrip spg lengkap dengan deteksi otomatis versi terinstal.
Setup Docker Compose untuk PostgreSQL + PostGIS multi-versi.
Migrasi data antar versi PostgreSQL.
