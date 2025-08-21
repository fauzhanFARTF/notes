# pyenv

## 🔹 Apa itu Pyenv?

pyenv adalah alat manajemen versi Python yang memungkinkan kamu menginstal dan beralih antar beberapa versi Python pada sistem yang sama, tanpa mengganggu instalasi Python sistem. Ini sangat berguna bagi pengembang yang bekerja pada proyek dengan kebutuhan versi Python yang berbeda-beda.

## 🔹 Fungsi Utama Pyenv

- Menginstal berbagai versi Python (misal: 3.8, 3.9, 3.10, 3.11, dll).
- Mengganti versi Python global (untuk seluruh sistem).
- Mengganti versi Python per proyek (dengan file .python-version).
- Menjalankan perintah dengan versi Python tertentu.
- Tidak mengganggu Python bawaan sistem (sangat aman digunakan).

## 🔹 Cara Menginstall Pyenv

### Di macOS (menggunakan Homebrew)

```bash
# 1. Install pyenv via Homebrew
    brew install pyenv

# 2. Set environment variable (tergantung shell yang digunakan)
    # Untuk Bash:
        echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
        echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
        echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
        # Reload shell
        source ~/.bash_profile

    # Untuk Bashrc:
        echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
        echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
        echo 'eval "$(pyenv init -)"' >> ~/.bashrc
        # Reload shell
        source ~/.bashrc 

    # Untuk Zsh:
        echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
        echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
        echo 'eval "$(pyenv init -)"' >> ~/.zshrc
        # Reload shell
        source ~/.zshrc  

```

### Di Linux atau WSL

```bash
# 1. Install dependensi
    sudo apt update
    sudo apt install -y make build-essential libssl-dev zlib1g-dev \
    libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
    libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev \
    libffi-dev liblzma-dev git

# 2. Clone pyenv dari GitHub atau install lewat curl
    git clone https://github.com/pyenv/pyenv.git ~/.pyenv
    # atau
    curl https://pyenv.run | bash

# 3. Set environment variable (tergantung shell yang digunakan)
    # Untuk Bash:
        echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
        echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
        echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
        # Reload shell
        source ~/.bash_profile

    # Untuk Bashrc:
        echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
        echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
        echo 'eval "$(pyenv init -)"' >> ~/.bashrc
        # Reload shell
        source ~/.bashrc 

    # Untuk Zsh:
        echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
        echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
        echo 'eval "$(pyenv init -)"' >> ~/.zshrc
        # Reload shell
        source ~/.zshrc  

```

## 🔹 Cheat Sheet Pyenv

```bash
# Cek versi Pyenv saat ini
pyenv --version

# Lihat semua versi Python yang sudah terinstal di pyenv
pyenv versions

# Lihat versi Python yang tersedia
pyenv install --list

# Instal versi tertentu
pyenv install 3.12.0

# Set versi global
pyenv global 3.12.0

# Instal versi tertentu
pyenv install 3.10.0

# Set versi local
pyenv local 3.10.0

# Cek versi Python saat ini
python --version
```
