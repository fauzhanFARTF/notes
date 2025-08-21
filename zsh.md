# 🧰 ZSH

## 🔤 Apa Itu Zsh?

Zsh (Z Shell) adalah shell (command interpreter) berbasis Unix yang sangat powerful dan fleksibel , dengan fitur tambahan yang tidak tersedia di shell standar seperti bash.

## 📌 Definisi Singkat

Zsh adalah shell komando Unix yang kompatibel dengan bash, tetapi memiliki fitur tambahan seperti autocomplete, tema, plugin, dan pengaturan yang lebih kaya.

### 🧩 Fitur Utama Zsh

- ✅ Autocomplete

    Bisa menebak perintah, opsi, nama file, dan lainnya saat kamu mengetik.
- 🎨 Tema & Prompt Keren

    Dapat dikustomisasi dengan tampilan prompt yang menarik (misalnya: Powerlevel10k).
- 🔌 Plugin & Framework

    Bisa menggunakan framework seperti (Oh My Zsh), untuk menambahkan plugin otomatis.
- 📁 Globbing Lanjutan

    Mendukung pencarian file dengan pola yang lebih kompleks.
- 🧠 Spelling Correction

    Otomatis memperbaiki kesalahan ketik perintah atau nama file.
- 🧰 Shared History

    Riwayat perintah bisa dibagikan di semua tab terminal.

### 🛠️ Contoh Penggunaan Zsh

```bash
# Navigasi cepat dengan autocomplete
$ cd ~/Documen<TAB>   # Otomatis jadi ~/Documents

# Menjalankan perintah
$ ls -la

# Menjalankan perintah sebelumnya
$ !! 

# Cari riwayat perintah
$ history | grep "sudo"
```

### 🧱 Zsh vs Bash – Apa Bedanya?

| Fitur              | Zsh                                   | Bash                           |
|--------------------|---------------------------------------|-------------------------------|
| Autocomplete       | Sangat lengkap dan bisa dikustomisasi | Terbatas                      |
| Prompt             | Bisa diubah jadi keren dengan tema    | Sederhana                     |
| Plugin/Theme       | Didukung lewat Oh My Zsh              | Tidak ada framework sekuat itu|
| Spelling Correction| Ada                                   | Tidak                         |
| Shared History     | Ada                                   | Tidak                         |


### 🌟 Oh My Zsh – Framework untuk Zsh

Oh My Zsh adalah framework open-source yang membuat penggunaan Zsh jadi jauh lebih menyenangkan dan produktif.

### 🔧 Fitur Oh My Zsh:

- Ratusan tema (misal: Powerlevel10k, Agnoster)
- Plugin untuk Git, Docker, Python, Node.js, dll.
- Auto-update
- Pengaturan yang mudah via file .zshrc

### 💡 Contoh Tema Oh My Zsh

- Powerlevel10k : Tema paling populer, kaya informasi dan cepat.
- Spaceship : Minimalis dan modern.
- Agnoster : Favorit banyak developer, terutama untuk WSL.

### 📦 Cara Instal Zsh

Di Linux (misalnya Ubuntu):

#### 1. Update apt dan install zsh

```bash
sudo apt update
sudo apt install zsh -y
```

atau 

```bash
sudo apt update && sudo apt install zsh -y
```

Contoh

```bash
fauzhan@Arroyan:~$ sudo apt update && sudo apt install zsh -y
[sudo] password for fauzhan:
Get:1 http://security.ubuntu.com/ubuntu noble-security InRelease [126 kB]
Hit:2 http://archive.ubuntu.com/ubuntu noble InRelease
Get:3 http://archive.ubuntu.com/ubuntu noble-updates InRelease [126 kB]
Get:4 http://security.ubuntu.com/ubuntu noble-security/main amd64 Packages [1009 kB]
Get:5 http://archive.ubuntu.com/ubuntu noble-backports InRelease [126 kB]
Get:6 http://security.ubuntu.com/ubuntu noble-security/main Translation-en [178 kB]
Get:7 http://security.ubuntu.com/ubuntu noble-security/main amd64 Components [21.5 kB]
Get:8 http://security.ubuntu.com/ubuntu noble-security/main amd64 c-n-f Metadata [7068 B]
Get:9 http://security.ubuntu.com/ubuntu noble-security/universe amd64 Packages [873 kB]
Get:10 http://security.ubuntu.com/ubuntu noble-security/universe Translation-en [192 kB]
Get:11 http://security.ubuntu.com/ubuntu noble-security/universe amd64 Components [52.3 kB]
Get:12 http://security.ubuntu.com/ubuntu noble-security/universe amd64 c-n-f Metadata [17.0 kB]
Get:13 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 Packages [1436 kB]
Get:14 http://archive.ubuntu.com/ubuntu noble/universe amd64 Packages [15.0 MB]
Get:15 http://security.ubuntu.com/ubuntu noble-security/restricted Translation-en [311 kB]
Get:16 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 Components [212 B]
Get:17 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 c-n-f Metadata [468 B]
Get:18 http://security.ubuntu.com/ubuntu noble-security/multiverse amd64 Packages [18.5 kB]
Get:19 http://security.ubuntu.com/ubuntu noble-security/multiverse Translation-en [4288 B]
Get:20 http://security.ubuntu.com/ubuntu noble-security/multiverse amd64 Components [212 B]
Get:21 http://security.ubuntu.com/ubuntu noble-security/multiverse amd64 c-n-f Metadata [380 B]
Get:22 http://archive.ubuntu.com/ubuntu noble/universe Translation-en [5982 kB]
Get:23 http://archive.ubuntu.com/ubuntu noble/universe amd64 Components [3871 kB]
Get:24 http://archive.ubuntu.com/ubuntu noble/universe amd64 c-n-f Metadata [301 kB]
Get:25 http://archive.ubuntu.com/ubuntu noble/multiverse amd64 Packages [269 kB]
Get:26 http://archive.ubuntu.com/ubuntu noble/multiverse Translation-en [118 kB]
Get:27 http://archive.ubuntu.com/ubuntu noble/multiverse amd64 Components [35.0 kB]
Get:28 http://archive.ubuntu.com/ubuntu noble/multiverse amd64 c-n-f Metadata [8328 B]
Get:29 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 Packages [1269 kB]
Get:30 http://archive.ubuntu.com/ubuntu noble-updates/main Translation-en [258 kB]
Get:31 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 Components [163 kB]
Get:32 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 c-n-f Metadata [13.5 kB]
Get:33 http://archive.ubuntu.com/ubuntu noble-updates/universe amd64 Packages [1111 kB]
Get:34 http://archive.ubuntu.com/ubuntu noble-updates/universe Translation-en [284 kB]
Get:35 http://archive.ubuntu.com/ubuntu noble-updates/universe amd64 Components [376 kB]
Get:36 http://archive.ubuntu.com/ubuntu noble-updates/universe amd64 c-n-f Metadata [26.0 kB]
Get:37 http://archive.ubuntu.com/ubuntu noble-updates/restricted amd64 Packages [1533 kB]
Get:38 http://archive.ubuntu.com/ubuntu noble-updates/restricted Translation-en [330 kB]
Get:39 http://archive.ubuntu.com/ubuntu noble-updates/restricted amd64 Components [212 B]
Get:40 http://archive.ubuntu.com/ubuntu noble-updates/restricted amd64 c-n-f Metadata [492 B]
Get:41 http://archive.ubuntu.com/ubuntu noble-updates/multiverse amd64 Packages [33.2 kB]
Get:42 http://archive.ubuntu.com/ubuntu noble-updates/multiverse Translation-en [6772 B]
Get:43 http://archive.ubuntu.com/ubuntu noble-updates/multiverse amd64 Components [940 B]
Get:44 http://archive.ubuntu.com/ubuntu noble-updates/multiverse amd64 c-n-f Metadata [592 B]
Get:45 http://archive.ubuntu.com/ubuntu noble-backports/main amd64 Packages [39.9 kB]
Get:46 http://archive.ubuntu.com/ubuntu noble-backports/main Translation-en [9152 B]
Get:47 http://archive.ubuntu.com/ubuntu noble-backports/main amd64 Components [7060 B]
Get:48 http://archive.ubuntu.com/ubuntu noble-backports/main amd64 c-n-f Metadata [272 B]
Get:49 http://archive.ubuntu.com/ubuntu noble-backports/universe amd64 Packages [28.0 kB]
Get:50 http://archive.ubuntu.com/ubuntu noble-backports/universe Translation-en [17.1 kB]
Get:51 http://archive.ubuntu.com/ubuntu noble-backports/universe amd64 Components [28.4 kB]
Get:52 http://archive.ubuntu.com/ubuntu noble-backports/universe amd64 c-n-f Metadata [1304 B]
Get:53 http://archive.ubuntu.com/ubuntu noble-backports/restricted amd64 Components [216 B]
Get:54 http://archive.ubuntu.com/ubuntu noble-backports/restricted amd64 c-n-f Metadata [116 B]
Get:55 http://archive.ubuntu.com/ubuntu noble-backports/multiverse amd64 Components [212 B]
Get:56 http://archive.ubuntu.com/ubuntu noble-backports/multiverse amd64 c-n-f Metadata [116 B]
Fetched 35.7 MB in 8s (4415 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
138 packages can be upgraded. Run 'apt list --upgradable' to see them.
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  zsh-common
Suggested packages:
  zsh-doc
The following NEW packages will be installed:
  zsh zsh-common
0 upgraded, 2 newly installed, 0 to remove and 138 not upgraded.
Need to get 4985 kB of archives.
After this operation, 19.1 MB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu noble/main amd64 zsh-common all 5.9-6ubuntu2 [4173 kB]
Get:2 http://archive.ubuntu.com/ubuntu noble/main amd64 zsh amd64 5.9-6ubuntu2 [812 kB]
Fetched 4985 kB in 3s (1709 kB/s)
Selecting previously unselected package zsh-common.
(Reading database ... 40768 files and directories currently installed.)
Preparing to unpack .../zsh-common_5.9-6ubuntu2_all.deb ...
Unpacking zsh-common (5.9-6ubuntu2) ...
Selecting previously unselected package zsh.
Preparing to unpack .../zsh_5.9-6ubuntu2_amd64.deb ...
Unpacking zsh (5.9-6ubuntu2) ...
Setting up zsh-common (5.9-6ubuntu2) ...
Setting up zsh (5.9-6ubuntu2) ...
Processing triggers for debianutils (5.17build1) ...
Processing triggers for man-db (2.12.0-4build2) ...
```

#### 2. Cek versi

```bash
zsh --version
```

Contoh

```bash
fauzhan@Arroyan:~$ zsh --version
zsh 5.9 (x86_64-ubuntu-linux-gnu)
```

#### 3. Set Zsh sebagai shell default

```bash
chsh -s $(which zsh)
```

Contoh

```bash
fauzhan@Arroyan:~$ chsh -s $(which zsh)
Password:
fauzhan@Arroyan:~$
```

#### 4. Lalu Keluar dari terminal dan masuk lagi ke ubuntu.

#### 5. Nanti akan muncul

```bash
This is the Z Shell configuration function for new users,
zsh-newuser-install.
You are seeing this message because you have no zsh startup files
(the files .zshenv, .zprofile, .zshrc, .zlogin in the directory
~).  This function can help you with a few settings that should
make your use of the shell easier.

You can:

(q)  Quit and do nothing.  The function will be run again next time.

(0)  Exit, creating the file ~/.zshrc containing just a comment.
     That will prevent this function being run again.

(1)  Continue to the main menu.

(2)  Populate your ~/.zshrc with the configuration recommended
     by the system administrator and exit (you will need to edit
     the file by hand, if so desired).

--- Type one of the keys in parentheses ---

```

Pilih no 2 : ➡️ Ini akan membuat file .zshrc dengan konfigurasi dasar, dan Anda bisa langsung mulai menggunakan Zsh tanpa gangguan lagi.

Contoh :

```bash
This is the Z Shell configuration function for new users,
zsh-newuser-install.
You are seeing this message because you have no zsh startup files
(the files .zshenv, .zprofile, .zshrc, .zlogin in the directory
~).  This function can help you with a few settings that should
make your use of the shell easier.

You can:

(q)  Quit and do nothing.  The function will be run again next time.

(0)  Exit, creating the file ~/.zshrc containing just a comment.
     That will prevent this function being run again.

(1)  Continue to the main menu.

(2)  Populate your ~/.zshrc with the configuration recommended
     by the system administrator and exit (you will need to edit
     the file by hand, if so desired).

--- Type one of the keys in parentheses --- 2
/home/fauzhan/.zshrc:15: scalar parameter HISTFILE created globally in function zsh-newuser-install
(eval):1: scalar parameter LS_COLORS created globally in function zsh-newuser-install
fauzhan@Arroyan ~ %   
```

## 📌 Kesimpulan

| Komponen     | Penjelasan                                                               |
|--------------|---------------------------------------------------------------------------|
| Zsh          | Shell komando yang lebih canggih dari Bash                               |
| Fitur        | Autocomplete, tema, plugin, correction, dll.                              |
| Oh My Zsh    | Framework untuk mempermudah pengaturan Zsh                                |
| Penggunaan   | Sangat populer di developer, sistem administrator, dan power user         |

---
