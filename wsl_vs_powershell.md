# CUSTOM TERMINAL Windows (WSL - Oh My ZSH)

## 🧩 1. WSL (Windows Subsystem for Linux)

### 🔍 Definisi:

WSL (Windows Subsystem for Linux) adalah fitur di Windows yang memungkinkan pengguna menjalankan lingkungan Linux (seperti Bash shell dan berbagai perintah serta aplikasi Linux) secara langsung di Windows , tanpa perlu dual-boot atau virtual machine.

### 💡 Fungsi Utama:

Menjalankan aplikasi Linux native (seperti grep, sed, awk, vim, python, docker, dll.)
Mengembangkan aplikasi Linux di lingkungan Windows
Mengakses sistem file Windows dari Linux dan sebaliknya
Menjalankan server Linux seperti Apache, MySQL, dll.

### 🧱 Versi WSL:

#### WSL 1

Menjalankan biner Linux dengan kompatibilitas penuh, tetapi tidak menggunakan kernel Linux asli.

#### WSL 2

Menggunakan kernel Linux asli (dengan teknologi virtualisasi ringan), lebih cepat dan kompatibel untuk pengembangan.

#### 🧪 Contoh Penggunaan

```bash
# Di terminal WSL
$ ls -la
$ python3 app.py
$ sudo apt update
```

## 🖥️ 2. PowerShell

### 🔍 Definisi

PowerShell adalah shell command-line dan scripting language yang dikembangkan oleh Microsoft. Ini adalah alat yang sangat kuat untuk otomatisasi tugas administratif dan manajemen sistem di Windows, Linux (dengan WSL), dan macOS.

### 💡 Fungsi Utama

- Menjalankan perintah sistem (mirip dengan CMD, tapi jauh lebih canggih)
- Mengotomatisasi tugas administratif lewat script
- Mengelola sistem Windows dan jaringan
- Bekerja dengan objek, bukan hanya teks (berbeda dengan CMD)

#### ⚙️ Contoh Penggunaan

```bash
# Di PowerShell
PS C:\> Get-Process
PS C:\> wsl --install
PS C:\> Get-Service | Where-Object {$_.Status -eq "Running"}
```

#### 🌐 PowerShell Core / PowerShell 7+

- Versi lintas platform (Windows, Linux, macOS)
- Pengganti CMD dan PowerShell lama
- Buka source dan dikembangkan oleh Microsoft

## 🆚 3.  Perbedaan WSL dan PowerShell

| Fitur           | WSL                                       | PowerShell                                |
|-----------------|-------------------------------------------|-------------------------------------------|
| Tujuan          | Menjalankan Linux di Windows              | Mengelola sistem Windows dan otomatisasi  |
| Sistem Operasi  | Linux (Ubuntu, Debian, dll.)              | Windows (dan juga bisa di Linux/macOS)    |
| Perintah        | Bash/Linux commands                       | PowerShell commands (dan CMD)             |
| Kernel          | Linux (khususnya WSL2)                    | Tidak menggunakan kernel Linux            |
| Integrasi       | Dengan Windows file system, app, dll.     | Dengan sistem Windows, registry, services |

## 🔄4.  Integrasi WSL dan PowerShell

Kamu bisa menggunakan PowerShell untuk mengelola WSL , seperti:

```bash
#di powershell
wsl --list --online      # Lihat distribusi Linux tersedia
wsl --install -d Ubuntu  # Instal Ubuntu
wsl --shutdown           # Matikan WSL
wsl -l -v                # Lihat versi WSL (1 atau 2)
```

## 📌 Kesimpulan

| Komponen   | Deskripsi                                                         |
|------------|-------------------------------------------------------------------|
| WSL        | Menjalankan Linux di Windows                                      |
| PowerShell | Shell dan alat otomatisasi sistem di Windows                      |
| Gabungan   | PowerShell digunakan untuk menginstal dan mengelola WSL di Windows |

---
