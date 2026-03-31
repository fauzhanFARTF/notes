# Panduan Multi-Version PostgreSQL di macOS (Homebrew)

Ya, Anda bisa menginstal dan mengelola beberapa versi PostgreSQL secara bersamaan di sistem yang sama, mirip seperti cara Anda menggunakan sphp untuk berpindah antar versi PHP di macOS.
Namun, PostgreSQL tidak menyediakan mekanisme switching global bawaan seperti PHP, karena:
PostgreSQL adalah server proses, bukan sekadar CLI tool.
Setiap versi biasanya berjalan di port berbeda dan memiliki data directory terpisah.
Switching "aktif" berarti mengatur service mana yang berjalan & port mana yang dipakai.

## ✅ Solusi Profesional: Multi-Version PostgreSQL dengan Homebrew

Karena Anda pengguna macOS + Homebrew, berikut adalah pendekatan terbaik untuk mengelola beberapa versi.

### 🔹 Langkah 1: Install Beberapa Versi PostgreSQL via Homebrew

Homebrew tidak menautkan (link) versi lama secara default untuk menghindari konflik. Jadi semua versi tetap terinstal tapi tidak aktif di $PATH.
bash
123

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
   echo "Example: spg 15"
   echo "Available versions: 14, 15, 16..."
   return 1
   fi

   VERSION=$1
    FORMULA="postgresql@$VERSION"

   # Stop semua service postgresql yang berjalan

   brew services stop postgresql
   brew services stop $FORMULA

   # Unlink versi sebelumnya

   brew unlink postgresql 2>/dev/null

   # Link versi yang dipilih

   echo "Switching to PostgreSQL $VERSION..."
   brew link $FORMULA --force

   # Start service versi yang dipilih

   brew services start $FORMULA

   echo "✅ Successfully switched to PostgreSQL $VERSION"
   psql --version

   ```

4. Beri izin eksekusi:

   ```bash
       chmod +x ~/.local/bin/spg
   ```

   (Pastikan ~/.local/bin sudah ada di $PATH Anda)

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
