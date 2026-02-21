# Install Maria db

## Permasalahan Utama

Karena MariaDB di Homebrew menggunakan plugin autentikasi unix_socket untuk user root@localhost.

Apa itu unix_socket?
Ini adalah metode autentikasi yang mengizinkan login sebagai root hanya jika Anda adalah user sistem dengan hak akses tinggi (UID 0).
Saat Anda jalankan sudo mariadb -u root, sistem:
Meminta password login macOS Anda (untuk otorisasi sudo)
Menjalankan perintah sebagai user root sistem
MariaDB melihat: "Oh, ini user root sistem → izinkan masuk sebagai root database"
✅ Jadi, password yang diminta bukan password database, tapi password login Mac Anda.

❌ Mengapa mariadb -u root -p Gagal Meski Sudah Set Password?
Karena plugin unix_socket masih aktif!

Meskipun Anda sudah jalankan:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'password_baru';
```

...MariaDB masih memaksa pakai unix_socket, jadi:

Ia tidak pernah mengecek password yang Anda berikan
Ia hanya cek: "Apakah kamu user root sistem?"
Karena Anda bukan (sudo tidak dipakai), maka ditolak
🚫 Jadi, mengganti password tidak cukup — Anda harus ganti metode autentikasinya.

## ✅ Solusi: Ubah Plugin Autentikasi dari unix_socket ke mysql_native_password

```bash
sudo mariadb -u root
```

Lanjutkan

```sql
-- Cek dulu plugin yang dipakai
SELECT User, Host, plugin FROM mysql.user WHERE User = 'root';

-- Ubah ke autentikasi berbasis password
ALTER USER 'root'@'localhost'
  IDENTIFIED VIA mysql_native_password
  USING PASSWORD('password_baru');

-- Contoh: password = "root"
-- ALTER USER 'root'@'localhost' IDENTIFIED VIA mysql_native_password USING PASSWORD('root');

FLUSH PRIVILEGES;
EXIT;
```

## Saran

### 🔐 Jawaban Singkat:

Mengubah plugin autentikasi dari unix_socket ke mysql_native_password itu boleh, tapi tidak disarankan untuk development lokal di macOS.

Lebih baik: gunakan user non-root (misal: 'fauzan'@'localhost') dengan password kosong atau sederhana.

### 📌 Mengapa unix_socket Digunakan oleh Homebrew MariaDB?

- Keamanan: Hanya user sistem dengan akses root yang bisa login sebagai root database.
- Tanpa password: Tidak perlu mengelola password untuk akun superuser.
- Default modern: MariaDB ≥ 10.4 dan MySQL 8+ menggunakan pendekatan serupa.

### ⚠️ Risiko Mengganti ke mysql_native_password

| **Risiko**                | **Penjelasan**                                                                                         |
| ------------------------- | ------------------------------------------------------------------------------------------------------ |
| Password bisa dilupakan   | Jika lupa, perlu reset manual yang prosesnya lebih ribet                                               |
| Tidak lebih aman di local | Di Mac pribadi tidak ada ancaman eksternal, sehingga password justru merepotkan                        |
| Bisa bentrok dengan tool  | Beberapa GUI seperti Navicat atau TablePlus bisa bermasalah jika `root` tiba-tiba menggunakan password |
| Tidak perlu               | Untuk development, kamu tidak perlu login sebagai `root`                                               |

### ✅ Solusi Lebih Baik: Gunakan User Non-Root

Anda tidak perlu memaksa root pakai password. Cukup:

```sql
CREATE USER 'fauzan'@'localhost' IDENTIFIED BY 'password baru';
GRANT ALL PRIVILEGES ON _._ TO 'fauzan'@'localhost';
```

#### Keuntungan:

- ✅ Bisa login tanpa sudo
- ✅ Tidak perlu password
- ✅ Tidak sentuh konfigurasi root
- ✅ Aman (karena hanya di localhost)
- ✅ Kompatibel dengan PHP, Navicat, CLI

💡 Akun root sebaiknya hanya dipakai untuk operasi admin jarang, seperti:

- Buat user baru
- Restore backup besar
- Ubah konfigurasi global

### 🛠️ Kapan Boleh Ganti ke mysql_native_password?

Hanya jika:

- Anda harus menggunakan root di aplikasi (tidak disarankan!)
- Anda deploy ke lingkungan yang tidak mendukung unix_socket (misal: shared hosting lama)
- Anda sedang testing kompatibilitas legacy
- Untuk 99% kasus development lokal di Mac, ini tidak perlu.

🔁 Perbandingan Langsung

| Pendekatan                         | Login CLI            | PHP / Navicat  | Keamanan           | Kemudahan       |
| ---------------------------------- | -------------------- | -------------- | ------------------ | --------------- |
| `unix_socket` + user `fauzan`      | `mariadb -u fauzan`  | Tanpa password | ✅ Tinggi          | ✅ Sangat mudah |
| `mysql_native_password` untuk root | `mariadb -u root -p` | Butuh password | ⚠️ Sama (di local) | ❌ Ribet        |
