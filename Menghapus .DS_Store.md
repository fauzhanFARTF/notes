# Menghapus File `.DS_Store` di macOS

File `.DS_Store` adalah file metadata yang dibuat otomatis oleh macOS (Finder) untuk menyimpan pengaturan tampilan folder seperti posisi ikon, mode tampilan, dan lainnya.

File ini aman untuk dihapus dan biasanya tidak diperlukan dalam project development.

---

## 📌 Hapus Satu File `.DS_Store`

```bash
rm .DS_Store
```

Jika berada di folder lain:

```bash
rm /path/folder/.DS_Store
```

---

## 📌 Hapus Semua `.DS_Store` dalam Folder (Rekursif)

Perintah ini akan mencari dan menghapus semua file `.DS_Store` di folder saat ini beserta subfoldernya:

```bash
find . -name ".DS_Store" -type f -delete
```

---

## 📌 Hapus Semua `.DS_Store` di Seluruh Sistem (Opsional)

Gunakan jika ingin membersihkan seluruh Mac:

```bash
sudo find / -name ".DS_Store" -type f -delete
```

> ⚠️ Perintah ini membutuhkan akses administrator dan biasanya tidak diperlukan.

---

## 📌 Mencegah `.DS_Store` Masuk ke Git Repository

Tambahkan ke file `.gitignore`:

```bash
.DS_Store
```

Jika file sudah terlanjur ter-commit:

```bash
git rm --cached .DS_Store
git commit -m "Remove .DS_Store"
```

---

## 📌 Mencegah macOS Membuat `.DS_Store` di Network Drive

```bash
defaults write com.apple.desktopservices DSDontWriteNetworkStores true
```

Untuk mengembalikan ke pengaturan semula:

```bash
defaults write com.apple.desktopservices DSDontWriteNetworkStores false
```

---

## ✅ Rekomendasi untuk Developer

Biasakan menjalankan perintah berikut sebelum commit:

```bash
find . -name ".DS_Store" -type f -delete
```

Atau tambahkan `.DS_Store` ke `.gitignore` agar tidak mengganggu repository.

---

## 📄 Lisensi

Bebas digunakan untuk kebutuhan pribadi maupun project.
