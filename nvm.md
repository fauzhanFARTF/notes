# nvm

## 🔹 Apa itu nvm?

nvm (Node Version Manager) adalah alat baris perintah (command-line tool) untuk mengelola beberapa versi Node.js di sistem yang sama. Karena npm (Node Package Manager) dikirimkan bersama Node.js, maka dengan mengganti versi Node.js, kamu juga secara otomatis mengganti versi npm yang digunakan.

## 🔹 Fungsi Utama nvm

- Menginstal berbagai versi Node.js (dan otomatis membawa npm-nya).
- Beralih antar versi Node.js & npm per sesi shell.
- Menetapkan versi default atau global.
- Menjalankan perintah dengan versi Node.js tertentu.
- Tidak mengganggu instalasi Node.js sistem.

## 🔹 Cara Menginstall nvm

### Di macOS, Linux, WSL

```bash
# 1. Install 
    # via curl
        curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
    # Alternatif: gunakan wget
        wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# 2. Restart terminal atau jalankan:
    source ~/.bashrc  
    # atau 
    source ~/.zshrc
    # atau
    source ~/.bash_profile

# 3. Mengecek versi nvm
    nvm --version  
```

## 🔹 Cheat Sheet nvm

```bash
# Lihat semua versi Node JS yang sudah terinstal di nvm
nvm list

# Melihat versi node.js yang digunakan saat ini
nvm current
# atau
node -v

# Melihat versi npm yang digunakan saat ini
npm -v

# Lihat versi Node.js yang tersedia
nvm list-remote

# hanya tampilkan versi LTS (Long-Term Support)
nvm list-remote --lts

# Install node js versi tertentu
nvm install 18.17.0    
nvm install 20.10.0    
nvm install 16.20.2    
nvm install 10.8.0 
nvm install 23.2.0 

# Instal versi terbaru dari Node.js (latest)
nvm install node

# Gunakan Node Js versi tertentu
nvm use 18.17.0
nvm use 20.10.0

# Set versi default
nvm alias default 23.2.0

# Lihat semua alias yang tersedia
nvm alias
```
