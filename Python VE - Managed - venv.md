# Membuat Virtual Environment Menggunakan Venv

Untuk Membuat Virtual Environtmentnya kita dapat mengetikkan perintah di terminal

```zsh
python -m venv venv
```

💡 Perintah di atas akan membuat virtual environment di dalam folder bernama venv (Anda bisa mengganti nama folder sesuai kebutuhan, misalnya env atau myenv atau venv).

Setelah perintah dijalankan, sebuah direktori venv akan terbentuk dengan struktur folder yang berisi salinan interpreter Python, skrip aktivasi, serta direktori untuk paket-paket yang akan diinstal.

## 📁 Struktur Direktori

Berikut adalah struktur direktori yang dihasilkan dari perintah diatas :

### A. MacOS / Linux / Windows (WSL)

```bash
API-NOTES/
└── venv/
    ├── bin/
    │   ├── activate                    # Skrip aktivasi (bash, zsh)
    │   ├── activate.csh
    │   ├── activate.fish
    │   ├── Activate.ps1
    │   ├── pip
    │   ├── pip3
    │   ├── pip3.12
    │   ├── python
    │   ├── python3
    │   └── python3.12
    ├── include/python3.12/
    └── lib/python3.12/site-packages/
        ├── pip/
        ├── pip-23.2.1.dist-info/
        └── pyvenv.cfg
```

### B. Windows (cmd / powershell / gitbash)

```bash
API-NOTES/
└── venv/
    ├── Scripts/
    │   ├── activate.bat          # Skrip aktivasi (Command Prompt)
    │   ├── activate.ps1          # Skrip aktivasi (PowerShell)
    │   ├── deactivate.bat        # Nonaktifkan environment
    │   ├── pip.exe               # Eksekusi pip
    │   ├── pip3.exe
    │   ├── pip3.12.exe
    │   ├── python.exe            # Salinan interpreter Python
    │   ├── pythonw.exe           # Python tanpa console (untuk GUI)
    │   ├── python3.exe
    │   └── python3.12.exe
    ├── Include/                  # Header C untuk ekstensi Python
    ├── Lib/
    │   └── site-packages/        # Tempat paket Python diinstal
    │       ├── pip/
    │       ├── pip-24.0.dist-info/
    │       ├── setuptools/
    │       ├── setuptools-69.5.1.dist-info/
    │       └── ...
    └── pyvenv.cfg                # File konfigurasi virtual environment
```

Gambar tersebut menunjukkan struktur direktori dari sebuah lingkungan virtual Python (venv) yang dibuat untuk sebuah proyek bernama API-NOTES. Berikut penjelasannya:

1. ✅ venv (Lingkungan Virtual)

    Ini adalah lingkungan virtual Python, digunakan untuk mengisolasi ketergantungan (dependencies) proyek dari instalasi Python global.

2. 📂 bin/ (Pada Unix/Linux/macOS) , Scripts/ (Pada Windows)

    Berisi skrip eksekusi:

    - activate: Mengaktifkan lingkungan virtual di bash.
    - activate.csh, activate.fish: Untuk shell csh dan fish.
    - Activate.ps1: Untuk PowerShell (Windows).
    - pip, pip3, pip3.12: Alat baris perintah untuk menginstal paket.
    - python, python3, python3.12: Menunjuk ke interpreter Python di dalam lingkungan virtual.

    ⚠️ Catatan: Pada Windows, folder ini disebut Scripts/ bukan bin/ Jika dijalankan melalui cmd / git bash

3. 📂 include/python3.12/

    Berisi file header yang dibutuhkan saat mengompilasi ekstensi C (misalnya saat membangun paket seperti NumPy).

4. 📂 lib/python3.12/site-packages/

    Tempat semua paket Python yang terinstal disimpan.

    - pip/: Paket pip itu sendiri (manajer paket).
    - pip-23.2.1.dist-info/: Metadata tentang versi pip yang terinstal.
    - pyvenv.cfg: File konfigurasi yang memberi tahu Python bahwa ini adalah lingkungan virtual dan menentukan jalur Python dasar.

5. pyvenv.cfg
File konfigurasi utama dari virtual environment. Bisa dibuka dengan editor teks.

    Contoh :

    ```bash
    home = C:\Python312
    include-system-site-packages = false
    version = 3.12.3
    ```

    Penjelasan:

    - home : Lokasi instalasi Python utama (base interpreter) yang digunakan untuk membuat environment ini.
    include-system-site-packages :
    - false → Environment tidak bisa mengakses paket dari sistem global (rekomendasi, agar benar-benar terisolasi).
    - true → Bisa mengakses paket global (tidak disarankan kecuali ada alasan khusus).
    - version : Versi Python yang digunakan saat environment dibuat.

        🔁 File ini dibaca oleh Python saat kamu menjalankan python di dalam venv untuk menentukan konfigurasi lingkungan.

## Mengaktifkan Virtual Environment

✅ Cara Mengaktifkan di MacOS / Linux / Windows (WSL)

```bash
source venv/bin/activate
```

✅ Cara Mengaktifkan di Windows

1. Git Bash:

    ```bash
    source venv/Scripts/activate
    ```

2. Command Prompt (CMD):

    ```cmd
    venv\Scripts\activate
    ```

3. PowerShell:

    ```powershell
    venv\Scripts\Activate.ps1
    ```

    ⚠️ Jika muncul error kebijakan eksekusi (execution policy), jalankan dulu:

    ``` powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```

    🧼 Tips untuk Windows
    - Pastikan Anda menjalankan terminal sebagai user biasa, bukan admin, kecuali benar-benar diperlukan.
    - Tambahkan venv/ ke file .gitignore agar tidak terunggah ke GitHub:

        ```gitignore
        venv/
        ```

    - Gunakan PowerShell atau Windows Terminal untuk pengalaman lebih baik dibanding CMD.

## Untuk Melihat VE sedang digunakan atau tidak

### 1. Menggunakan Perintah "Where Python"

```bash
where python                                                                                                   
```

Hasil

✅ MacOS / Linux / Windows (WSL)

```bash
# Tidak Digunakan (MacOS - zsh)
python: aliased to python3
/Users/fauzannurrachman/.pyenv/shims/python

# Tidak Digunakan (Windows - WSL)
/home/fauzhan/.pyenv/shims/python
```

Ketika Virtual Environment Aktif / Sedang Digunakan

```bash
# Digunakan / aktif (MacOS - zsh)
python: aliased to python3
/Users/fauzannurrachman/Sites/Learn/project/cuy-notes/api-notes/venv/bin/python
/Users/fauzannurrachman/.pyenv/shims/python

# Digunakan / Aktif (Windows - WSL)
/mnt/c/sites/learn/project/cuy-notes/api-notes/venv/bin/python
/home/fauzhan/.pyenv/shims/python
```

### 2. Menggunakan Perintah "echo $VIRTUAL_ENV"

```bash
echo $VIRTUAL_ENV 
```

- Kalau hasilnya kosong berarti ve belum digunakan / diaktifkan
- Jika Ada hasilnya, itu menandakan lokasi instalasi virtual environmentnya

```bash
# MacOS - zsh
/Users/fauzannurrachman/Sites/Learn/project/cuy-notes/api-notes/venv
# Windows - wsl
/mnt/c/sites/learn/project/cuy-notes/api-notes/venv/
```
