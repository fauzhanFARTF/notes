# macos-sequoia-apache-multiple-php-versions

## Bagian 1: Lingkungan Pengembangan Web di macOS 15.0 Sequoia

Mengembangkan aplikasi web di macOS merupakan pengalaman yang sangat menyenangkan. Terdapat banyak pilihan untuk menyiapkan lingkungan pengembangan Anda, termasuk MAMP Pro yang populer karena menyediakan antarmuka grafis (UI) di atas Apache, PHP, dan MySQL. Namun, terkadang MAMP Pro mengalami perlambatan, menggunakan versi perangkat lunak yang sudah usang, atau berperilaku tidak stabil akibat sistem templat konfigurasinya yang kaku serta build-nya yang tidak mengikuti standar resmi.

Pada situasi seperti inilah banyak pengembang mulai mencari pendekatan alternatif—dan untungnya, solusi tersebut tersedia serta relatif mudah untuk diatur.

Dalam artikel blog ini, kami akan memandu Anda langkah demi langkah dalam menyiapkan dan mengonfigurasi Apache 2.4 bersama beberapa versi PHP sekaligus. Pada artikel kedua dari seri dua bagian ini, kami akan membahas instalasi MySQL, virtual host Apache, caching APC, serta instalasi Xdebug.

Jika sebelumnya Anda pernah mengikuti panduan serupa yang menggunakan tap homebrew/php dan kini ingin beralih ke pendekatan baru berbasis homebrew/core, maka Anda sebaiknya membersihkan instalasi lama terlebih dahulu dengan mengikuti petunjuk dalam panduan terbaru kami berjudul Upgrading Homebrew.

Panduan ini ditujukan bagi pengembang web berpengalaman. Jika Anda masih pemula, Anda akan lebih nyaman menggunakan MAMP atau MAMP Pro.

## Xcode Command Line Tools

Jika Anda belum menginstal Xcode, disarankan untuk terlebih dahulu menginstal Command Line Tools-nya, karena alat ini akan digunakan oleh Homebrew:

```bash
xcode-select --install
```

## Instalasi Homebrew

Proses ini sangat bergantung pada package manager macOS bernama Homebrew. Dengan perintah brew, Anda dapat dengan mudah menambahkan berbagai fitur canggih ke Mac Anda—namun pertama-tama, Anda harus menginstal Homebrew terlebih dahulu. Proses instalasinya cukup sederhana: buka aplikasi Terminal Anda (/Applications/Utilities/Terminal), lalu jalankan perintah berikut:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Ikuti petunjuk yang muncul di terminal dan masukkan kata sandi Anda saat diminta. Proses ini mungkin memakan waktu beberapa menit.

Jika ini merupakan instalasi baru dan PATH sistem Anda belum dikonfigurasi dengan benar, Anda bisa mengikuti instruksi "Next steps" yang ditampilkan setelah instalasi—yang sudah disesuaikan secara otomatis—atau secara manual menambahkan baris berikut ke file .bashrc atau .zshrc Anda:

```bash
(echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Setelah itu, Anda dapat menguji apakah instalasi Homebrew berhasil dengan menjalankan:

```bash
brew --version
```

Output yang diharapkan (versi mungkin berbeda):

```bash
Homebrew 4.3.23
```

Sebaiknya Anda juga menjalankan perintah berikut untuk memastikan semuanya dikonfigurasi dengan benar:

```bash
brew doctor
```

Perintah ini akan memberi tahu Anda jika ada hal yang perlu diperbaiki.

## Pustaka yang Diperlukan di Sequoia

Saat melakukan instalasi baru di macOS Sequoia, saya menemukan beberapa pustaka (library) yang tidak tersedia secara bawaan saat menjalankan langkah-langkah berikut. Agar proses berjalan lebih lancar, silakan jalankan perintah berikut sekarang:

```bash
brew install openssl
```

## Instalasi Apache

macOS 15.0 Sequoia (sebelumnya disebut sebagai macOS 13.0 dalam draf awal—catatan: versi resmi macOS 15 adalah Sequoia) sebenarnya sudah menyertakan Apache 2.4 secara bawaan. Namun, mulai rilis ini, Apple telah menghapus beberapa skrip yang diperlukan, sehingga versi Apache bawaan sistem tidak lagi mudah digunakan bersama Homebrew.

Solusinya adalah menginstal Apache 2.4 melalui Homebrew, lalu mengonfigurasinya agar berjalan pada port standar (80 untuk HTTP dan 443 untuk HTTPS).

Jika Anda sebelumnya sudah menjalankan Apache bawaan macOS, Anda perlu menghentikannya terlebih dahulu dan menonaktifkan skrip peluncuran otomatisnya. Tidak ada salahnya menjalankan semua perintah berikut secara berurutan—bahkan jika ini instalasi baru:

```bash
sudo apachectl -k stop
sudo launchctl unload -w /System/Library/LaunchDaemons/org.apache.httpd.plist 2>/dev/null
```

Setelah itu, instal versi Apache dari Homebrew:

```bash
brew install httpd
```

Tanpa opsi tambahan, httpd akan diinstal langsung dari binary yang telah dikompilasi, sehingga prosesnya cepat. Setelah selesai, Anda akan melihat pesan seperti:

```console
🍺  /opt/homebrew/Cellar/httpd/2.4.62: 1,664 files, 32.2MB
```

🍺 /opt/homebrew/Cellar/httpd/2.4.62: 1,664 files, 32.2MB
Langkah terakhir adalah mengatur agar Apache dari Homebrew otomatis berjalan saat sistem dinyalakan:

```bash
brew services start httpd
```

Kini Anda telah berhasil menginstal Apache versi Homebrew dan mengonfigurasinya untuk otomatis berjalan dengan hak akses yang sesuai. Layanan Apache tersebut seharusnya sudah aktif. Untuk memverifikasi, buka browser dan kunjungi:

```apache
http://localhost:8080
```

Anda akan melihat halaman sederhana dengan tulisan "It works!" — tanda bahwa server Apache berjalan dengan baik.

## Tips Pemecahan Masalah

Jika browser menampilkan pesan bahwa tidak dapat terhubung ke server, langkah pertama yang perlu Anda lakukan adalah memastikan bahwa server Apache benar-benar sedang berjalan.

Periksa proses Apache dengan menjalankan perintah berikut di Terminal:

```bash
ps -aef | grep httpd
```

Jika Apache aktif dan berjalan dengan baik, Anda akan melihat beberapa baris yang menampilkan proses httpd.

Jika tidak muncul atau Anda mencurigai adanya masalah, coba mulai ulang layanan Apache:

```bash
brew services restart httpd
```

Untuk memantau log kesalahan secara real-time—terutama saat memulai ulang atau mengakses server—buka tab atau jendela Terminal baru dan jalankan:

```bash
tail -f /opt/homebrew/var/log/httpd/error_log
```

Log ini sangat berguna untuk mengidentifikasi konfigurasi yang salah, izin file, modul yang gagal dimuat, atau masalah lainnya.

Karena Apache dikelola melalui brew services, berikut beberapa perintah yang sering digunakan:

```bash
brew services stop httpd      # Menghentikan Apache
brew services start httpd     # Menjalankan Apache
brew services restart httpd   # Memulai ulang Apache
```

## Visual Studio Code

Pada panduan sebelumnya, saya biasa memberikan instruksi untuk mengedit file menggunakan aplikasi TextEdit bawaan macOS. Namun, jujur saja—TextEdit bukan pilihan ideal untuk pengembangan web. Saat menguji panduan ini di Sequoia, saya terus mengalami masalah terkait enkoding karakter, ketidakmampuan menampilkan nomor baris, serta kurangnya dukungan sintaksis.

Solusi terbaik adalah beralih ke editor teks modern yang gratis, ringan, namun sangat tangguh: Visual Studio Code (VS Code). VS Code tersedia untuk macOS, Windows, dan Linux—namun saat ini kita hanya fokus pada versi macOS.

Anda dapat menginstal VS Code beserta perintah baris perintah (code)-nya dalam satu langkah menggunakan Homebrew:

```bash
brew install --cask visual-studio-code
```

Jika Anda sudah menginstal VS Code sebelumnya (misalnya dari situs resminya), Anda tetap bisa mengaktifkan perintah code di Terminal dengan membuat symlink:

```bash
ln -s "/Applications/Visual Studio Code.app/Contents/Resources/app/bin/code" /opt/homebrew/bin/code
```

💡 Pastikan direktori /opt/homebrew/bin ada di PATH Anda (biasanya sudah otomatis jika Anda mengikuti langkah instalasi Homebrew sebelumnya).

Setelah itu, Anda bisa membuka file apa pun langsung dari Terminal dengan:

```bash
code <nama_file>
```

## Konfigurasi Apache

Sekarang Anda memiliki server web yang berjalan. Langkah selanjutnya adalah menyesuaikan konfigurasinya agar lebih cocok sebagai lingkungan pengembangan lokal.

Di versi terbaru Homebrew, Apache secara default berjalan di port 8080, bukan port standar HTTP (80). Untuk mengubahnya, Anda perlu mengedit file konfigurasi utama Apache:

```bash
/opt/homebrew/etc/httpd/httpd.conf
```

Jika Anda telah menginstal VS Code dan mengaktifkan perintah code, buka file tersebut dengan:

```bash
code /opt/homebrew/etc/httpd/httpd.conf
```

(Alternatif: Jika Anda tetap ingin menggunakan TextEdit, gunakan open -e /opt/homebrew/etc/httpd/httpd.conf, meskipun ini tidak disarankan untuk pekerjaan pengembangan.)

Di dalam file httpd.conf, cari baris berikut:

```apache
Listen 8080
```

Ubah menjadi:

```apache
Listen 80
```

⚠️ Catatan: Port 80 adalah port sistem yang biasanya memerlukan hak akses root. Namun, karena Homebrew menjalankan httpd melalui mekanisme brew services yang aman, Apache tetap dapat menggunakan port 80 tanpa harus dijalankan sebagai root—selama tidak ada layanan web lain (seperti Apache bawaan macOS) yang masih aktif.

Setelah menyimpan perubahan, mulai ulang Apache agar perubahan berlaku:

```bash
brew services restart httpd
```

Kini, Anda seharusnya bisa mengakses server lokal Anda cukup dengan:

```bash
http://localhost
```

(bukan lagi http://localhost:8080).

Berikut adalah terjemahan dan penjelasan langkah-langkah konfigurasi Apache dalam bahasa Indonesia yang jelas dan terstruktur:

## Ubah Port Dengarkan (Listen Port)

Cari baris berikut di file httpd.conf:

```apache
Listen 8080
```

Ubah menjadi:

```apache
Listen 80
```

## Ubah Document Root

Document root adalah direktori tempat Apache mencari file untuk ditampilkan. Secara bawaan, nilainya adalah /opt/homebrew/var/www. Karena ini mesin pengembangan, kita akan mengarahkannya ke folder di direktori pengguna Anda.

Cari baris berikut:

```apache
DocumentRoot "/opt/homebrew/var/www"
```

Ganti dengan path ke folder Sites di direktori home Anda (ganti your_user dengan nama pengguna macOS Anda—misalnya
fauzannurrachman):

```apache
DocumentRoot "/Users/your_user/Sites"
```

## Perbarui Blok \<Directory>

Tepat di bawah baris DocumentRoot, Anda akan menemukan blok \<Directory>. Ubah juga path-nya agar sesuai:

```apache
<Directory "/Users/your_user/Sites">
```

Di dalam blok ini, cari pengaturan AllowOverride. Ubah nilainya menjadi All agar file .htaccess dapat digunakan (penting untuk framework seperti Laravel atau routing berbasis mod_rewrite):

```apache
AllowOverride All
```

## Aktifkan mod_rewrite

Fitur mod_rewrite (digunakan untuk URL rewriting) dinonaktifkan secara default. Cari baris berikut:

```apache
#LoadModule rewrite_module lib/httpd/modules/mod_rewrite.so
```

Hapus tanda # di awal baris untuk mengaktifkannya. Di VS Code, Anda bisa menempatkan kursor di baris tersebut dan menekan ⌘ + / untuk mengomentari/menghapus komentar:

```apache
#LoadModule rewrite_module lib/httpd/modules/mod_rewrite.so
```

## Atur User dan Group

Secara default, Apache berjalan sebagai pengguna \_www dan grup \_www. Ini akan menyebabkan masalah izin saat mengakses file di direktori pribadi Anda.

Cari dua baris berikut (sekitar sepertiga bagian bawah file httpd.conf):

```apache
User _www
Group _www
```

Ganti dengan nama pengguna Anda dan grup staff (grup standar di macOS untuk pengguna biasa):

```apache
User your_user
Group staff
```

⚠️ Ganti your_user dengan nama pengguna macOS Anda. Misalnya, jika Terminal Anda menunjukkan fauzannurrachman@MacBook, maka gunakan:

```apache
User fauzannurrachman
Group staff
```

## Atur ServerName

Apache merekomendasikan adanya ServerName. Cari baris berikut:

```apache
#ServerName www.example.com:8080
```

Ganti dengan:

```apache
ServerName localhost
```

Pastikan tidak ada port (:8080) di akhir, karena kita sudah menggunakan port 80.

## Buat Folder Sites

Buat folder Sites di direktori home Anda, lalu tambahkan file index.html sederhana:

```bash
mkdir ~/Sites
echo "<h1>My User Web Root</h1>" > ~/Sites/index.html
```

## Mulai Ulang Apache

Terapkan semua perubahan dengan memulai ulang Apache:

```bash
brew services restart httpd
```

💡 Jika muncul error saat restart, coba hapus tanda kutip (") di sekitar path pada DocumentRoot dan \<Directory>, sehingga menjadi:

```apache
DocumentRoot /Users/your_user/Sites
<Directory /Users/your_user/Sites>
```

(Meskipun secara resmi Apache mendukung kutip, terkadang versi tertentu sensitif terhadapnya.)

## Uji di Browser

Buka browser dan kunjungi:

```apache
http://localhost
```

Anda seharusnya melihat tulisan: "My User Web Root".

🔁 Jika masih menampilkan halaman lama, lakukan Shift + Reload (atau Cmd + Shift + R) untuk membersihkan cache browser dan memuat konten terbaru.

Jika semuanya berfungsi, selamat! Lingkungan dasar Apache Anda siap untuk pengembangan web lokal.
