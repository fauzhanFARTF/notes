# Virtual Environment

## 📘 Apa Itu Virtual Environment di Python?

Virtual environment (lingkungan virtual) adalah sebuah direktori terisolasi yang berisi salinan interpreter Python beserta paket-paket (libraries) yang diinstal secara lokal. Dengan kata lain, ini adalah "dunia kecil" Python yang terpisah dari instalasi Python utama di sistem Anda.

🔍 Analoginya: Bayangkan kamu punya beberapa proyek Python. Proyek A butuh Django 3.2, sementara Proyek B butuh Django 4.2. Jika kamu instal keduanya di sistem global, akan terjadi konflik. Maka dari itu, kamu buat virtual environment masing-masing agar tidak saling mengganggu. 

## 🧩 Fungsi Utama Virtual Environment

1. Isolasi Dependensi (Dependency Isolation)
    - Setiap proyek bisa memiliki versi paket yang berbeda tanpa bentrok.
    - Contoh: Proyek X pakai requests==2.25.1, Proyek Y pakai requests==2.31.0.
2. Mencegah Konflik Global
    - Menghindari "polusi" pada instalasi Python global.
    - Tidak perlu izin admin (sudo) untuk instal paket.
3. Portabilitas dan Reproduksibilitas
    - Bisa ekspor daftar paket (requirements.txt atau environment.yml) agar orang lain bisa membuat environment yang sama.
4. Testing dan Development
    - Memudahkan pengujian dengan versi Python atau library berbeda.
5. Clean Project Management
    - Setiap proyek punya "ruang kerja" sendiri → lebih rapi dan terorganisasi.

## 🛠️ Cara Kerja Virtual Environment

Saat kamu membuat virtual environment:

1. Dibuat folder baru (misal: venv/ atau myenv/).
2. Di dalamnya terdapat:
    - Salinan dari python executable.
    - Folder Scripts/ (Windows) atau bin/ (macOS/Linux) yang berisi pip, python, dan script aktivasi.
    - Folder Lib/ atau site-packages/ untuk menyimpan paket yang diinstal.
3. Ketika environment diaktifkan, perintah python dan pip akan merujuk ke lingkungan tersebut, bukan ke sistem global.

## ✅ Kenapa Harus Pakai Virtual Environment?

| Topik                     | Tanpa Virtual Environment                                             | Dengan Virtual Environment                                           |
| ------------------------- | --------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Manajemen paket           | Semua paket diinstal di sistem global → mudah konflik, sulit dikelola | Setiap proyek mandiri → aman, rapi, dan bisa direproduksi            |
| Keamanan & isolasi proyek | ❌ Tidak ada isolasi                                                   | ✅ Ada isolasi                                                        |
| Reproduksibilitas proyek  | ❌ Sulit reproduksi                                                    | ✅ Mudah reproduksi                                                   |
| Best Practice             | ❌ Tidak disarankan                                                    | ✅ Selalu gunakan untuk setiap proyek Python, kecuali skrip sederhana |

## 🔧 Tools untuk Membuat Virtual Environment

| Tool           | Keterangan                                                                                      |
| -------------- | ----------------------------------------------------------------------------------------------- |
| **venv**       | Bawaan Python 3.3+, ringan, cukup untuk kebanyakan proyek                                       |
| **virtualenv** | Lebih fleksibel, bisa digunakan di Python versi lama, fitur lebih lengkap                       |
| **conda**      | Manajer environment & paket lintas bahasa, populer di data science, bisa atur versi Python juga |

### Perbandingan Dari ketiga tools 🔧 Tersebut  

| Fitur                        | Bawaan Python (venv)      | Pipenv / Virtualenv | Conda / Anaconda / Miniconda |
| ---------------------------- | ------------------- | ------------------- | ---------------------------- |
| Instalasi                    | ✅ Ya                | ❌ (harus instal)    | ❌ (butuh Anaconda/Miniconda) |
| Hanya untuk Python           | ✅ Ya                | ✅ Ya                | ❌ Bisa untuk multi-bahasa    |
| Manajemen versi Python       | ❌ Tidak             | ❌ Tidak             | ✅ Bisa                       |
| Package manager terintegrasi | ❌ (harus pakai pip) | ❌ (pakai pip)       | ✅ Ya                         |
| Resolusi dependensi          | ❌ Lemah             | ❌ Lemah             | ✅ Sangat baik                |
| Ukuran & kecepatan           | Ringan              | Cepat               | Lebih berat tapi powerful    |
| Cocok untuk pemula           | ✅                   | ✅                   | ✅ (terutama data science)    |

Catatan penting:

venv dan virtualenv mirip, bedanya virtualenv bisa dipakai di Python versi lebih lama dan sedikit lebih fleksibel untuk virtual environment cross-version, tapi tetap tidak bisa upgrade versi Python di environment yang sama.

Conda lebih “powerful” karena bisa mengubah versi Python sekaligus menjaga kompatibilitas paket.

### Contoh 

Kalau kamu sudah punya virtual environment (misal venv) dan ingin ganti versi Python tapi tetap pakai environment yang sama, itu tidak langsung bisa. Alasannya:

1. Virtual environment venv terikat dengan versi Python yang dibuatnya.

2. Mengganti versi Python di dalam environment yang sama akan merusak struktur venv karena interpreter, library, dan binari terkait versi lama.

Solusi umum:

1. Buat environment baru dengan versi Python yang diinginkan.

    ```bash
    pyenv install 3.12.0
    pyenv global 3.12.0
    python -m venv myenv_new
    ```

    Lalu install ulang paket yang diperlukan (biasanya bisa pakai requirements.txt dari environment lama).

2. Dengan Conda, sedikit lebih fleksibel:

    Conda memungkinkan mengubah versi Python di environment yang sama, misal:

    ```bash
    conda activate myenv
    conda install python=3.12
    ```

    Conda akan mencoba menyesuaikan paket yang ada agar kompatibel dengan versi Python baru.

Jadi ringkasnya:

- venv → harus buat environment baru untuk ganti versi Python.
- conda → bisa upgrade Python langsung di environment lama, dengan manajemen dependensi otomatis.