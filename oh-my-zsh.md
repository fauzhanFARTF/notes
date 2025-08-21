# Oh My Zsh

Oh My Zsh adalah framework untuk mempermudah pengaturan Zsh.

## LANGKAH 1: Menginstal dan mengintegrasikan Oh My Zsh

Menambahkan tema dan plugin seperti Powerlevel10k, syntax highlighting, dan autosuggestions

Jalankan perintah ini:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh )"
```

contoh :

```bash
fauzhan@Arroyan ~ % sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh )"
Cloning Oh My Zsh...
remote: Enumerating objects: 1456, done.
remote: Counting objects: 100% (1456/1456), done.
remote: Compressing objects: 100% (1388/1388), done.
remote: Total 1456 (delta 50), reused 1254 (delta 40), pack-reused 0 (from 0)
Receiving objects: 100% (1456/1456), 3.29 MiB | 7.51 MiB/s, done.
Resolving deltas: 100% (50/50), done.
From https://github.com/ohmyzsh/ohmyzsh
 * [new branch]      dependabot/pip/dot-github/workflows/dependencies/certifi-2025.7.9 -> origin/dependabot/pip/dot-github/workflows/dependencies/certifi-2025.7.9
 * [new branch]      master     -> origin/master
branch 'master' set up to track 'origin/master'.
Already on 'master'
/home/fauzhan

Looking for an existing zsh config...
Found /home/fauzhan/.zshrc. Backing up to /home/fauzhan/.zshrc.pre-oh-my-zsh
Using the Oh My Zsh template file and adding it to /home/fauzhan/.zshrc.

         __                                     __
  ____  / /_     ____ ___  __  __   ____  _____/ /_
 / __ \/ __ \   / __ `__ \/ / / /  /_  / / ___/ __ \
/ /_/ / / / /  / / / / / / /_/ /    / /_(__  ) / / /
\____/_/ /_/  /_/ /_/ /_/\__, /    /___/____/_/ /_/
                        /____/                       ....is now installed!


Before you scream Oh My Zsh! look over the `.zshrc` file to select plugins, themes, and options.

• Follow us on X: https://x.com/ohmyzsh
• Join our Discord community: https://discord.gg/ohmyzsh
• Get stickers, t-shirts, coffee mugs and more: https://shop.planetargon.com/collections/oh-my-zsh
➜  ~ 
```

## 🎨 LANGKAH 2: Tambahkan Tema (Contoh: Powerlevel10k)

### 1. Instal Powerlevel10k:

```bash
git clone https://github.com/romkatv/powerlevel10k.git  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
```

Contoh

```bash
➜  ~ git clone https://github.com/romkatv/powerlevel10k.git  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
Cloning into '/home/fauzhan/.oh-my-zsh/custom/themes/powerlevel10k'...
remote: Enumerating objects: 16804, done.
remote: Counting objects: 100% (76/76), done.
remote: Compressing objects: 100% (51/51), done.
remote: Total 16804 (delta 56), reused 25 (delta 25), pack-reused 16728 (from 2)
Receiving objects: 100% (16804/16804), 70.41 MiB | 7.59 MiB/s, done.
Resolving deltas: 100% (10973/10973), done.
➜  ~  
```

### 2. Edit file .zshrc:

```bash
nano ~/.zshrc
```

### 3. Ganti tema menjadi Powerlevel10k:

Cari baris:

```bash
ZSH_THEME="robbyrussell"
```

Ganti menjadi:

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

Contoh :

```bash
# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:$HOME/.local/bin:/usr/local/bin:$PATH

# Path to your Oh My Zsh installation.
export ZSH="$HOME/.oh-my-zsh"

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time Oh My Zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="powerlevel10k/powerlevel10k"

# Set list of themes to pick from when loading at random
# Setting this variable when ZSH_THEME=random will cause zsh to load
# a theme from this variable instead of looking in $ZSH/themes/
# If set to an empty array, this variable will have no effect.
# ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )

# Uncomment the following line to use case-sensitive completion.
# CASE_SENSITIVE="true"

# Uncomment the following line to use hyphen-insensitive completion.
# Case-sensitive completion must be off. _ and - will be interchangeable.
# HYPHEN_INSENSITIVE="true"
```

Simpan:

- Tekan Ctrl + O → Enter → Ctrl + X

### 4. Install Font MesloLGS NF

- link download

    https://raw.githubusercontent.com/romkatv/powerlevel10k-media/master/MesloLGS%20NF%20Regular.ttf

- install font tersebut

### 5. Muat ulang konfigurasi:

```bash
source ~/.zshrc
```

Saat pertama kali menggunakan Powerlevel10k, kamu akan diminta menjalani konfigurasi awal (pilih gaya prompt, dll). Ikuti saja langkah-langkahnya.

contoh

```bash
➜  ~ source ~/.zshrc
```

Lalu akan muncul kustomisasi tema powerlevel10 k, ikuti step-stepnya

#### 1.  Choice [ynq]: y

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20074423.png?raw=true)

#### 2.  Choice [ynrq]: y

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20074442.png?raw=true)

#### 3.  Choice [ynrq]: y

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20074423.png?raw=true)

#### 4. Choice [123rq]:2

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20074522.png?raw=true)

#### 5. Choice [ynrq]: y

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20074758.png?raw=true)

#### 6. Choice [ynrq]: y

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20074816.png?raw=true)

#### 7. Choice [1234rq]: 3

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20074840.png?raw=true)

#### 8. Choice [1234rq]: 1

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20074953.png?raw=true)

#### 9. Choice [1234rq]: 2

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20075037.png?raw=true)

#### 10. Choice [1234rq]: 1

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20074953.png?raw=true)

#### 11. Choice [12345rq]: 3

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20075146.png?raw=true)

#### 12. Choice [12345rq]: 2

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20075217.png?raw=true)

#### 13. Choice [12rq]: 1

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20075302.png?raw=true)

#### 14. Choice [12rq]: 1

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20075319.png?raw=true)

#### 15. Choice [12rq]: 2

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20075354.png?raw=true)

#### 16. Choice [12rq]: 2

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20075413.png?raw=true)

#### 17. Choice [ynrq]: n

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20075437.png?raw=true)

#### 18. Choice [123rq]: 1

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20075624.png?raw=true)

#### 19. Choice [ynrq]: y

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20075637.png?raw=true)

#### 20. Selesai

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20075731.png?raw=true)


## 6. Jika ingin merubah kustomisasi tema powerlevel 10k bisa mengetikan

```bash
p10k configure
```

## 🔍 LANGKAH 3: Instal Plugin Tambahan

### 1. Instal Syntax Highlighting

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20080220.png?raw=true)

### 2. Instal Autosuggestions

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20080308.png?raw=true)

### 3. Aktifkan plugin di .zshrc

```bash
nano ~/.zshrc
```

Cari baris:

```bash
plugins=(git)
```

Ganti menjadi:

```bash
plugins=(git zsh-syntax-highlighting zsh-autosuggestions)
```

contoh:

```bash
# or set a custom format using the strftime function format specifications,
# see 'man strftime' for details.
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

# Which plugins would you like to load?
# Standard plugins can be found in $ZSH/plugins/
# Custom plugins may be added to $ZSH_CUSTOM/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
# plugins=(git)
plugins=(git zsh-syntax-highlighting zsh-autosuggestions)

source $ZSH/oh-my-zsh.sh

# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
```

Simpan:

Tekan Ctrl + O → Enter → Ctrl + X

muat ulang:

```bash
source ~/.zshrc
```

## 🖥️ LANGKAH 4: Tampilan Lebih Keren (Opsional)

### 1. Instal Nerd Font (misal: FiraCode Nerd Font)

- Download: https://www.nerdfonts.com/font-downloads

- Instal font dengan klik dua kali dan pilih Install

### 2. Buka WSH Terminal

- Klik kanan pada judul terminal dan pilih Settings atau tekan Ctrl + ,.

- Anda juga bisa membuka file konfigurasi secara langsung:

    ![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20081217.png?raw=true)

### 3. Buka file settings.json

Pilih opsi "Open JSON file" .

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-20%20082824.png?raw=true)

### 4. Tambahkan konfigurasi font

Cari bagian profiles.list atau defaults dan tambahkan atau ubah baris berikut:

```json
{
  "face": "FiraCode Nerd Font",
  "size": 12
}
```

Contoh lengkap:

```json
{
    "profiles": 
    {
        "defaults": 
        {
            "font": 
            {
                "face": "FiraCode Nerd Font",
                "size": 12
            }
        },
        "list": 
        [
            {
                "commandline": "%SystemRoot%\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "hidden": false,
                "name": "Windows PowerShell"
            },
            {
                "commandline": "%SystemRoot%\\System32\\cmd.exe",
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "hidden": false,
                "name": "Command Prompt"
            },
            {
                "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
                "hidden": false,
                "name": "Azure Cloud Shell",
                "source": "Windows.Terminal.Azure"
            },
            {
                "guid": "{59d2bd70-f9a6-5353-baf7-81a6b2ad87d7}",
                "hidden": false,
                "name": "Python Command Prompt",
                "source": "ArcGIS"
            },
            {
                "guid": "{2ece5bfe-50ed-5f3a-ab87-5cd4baafed2b}",
                "hidden": false,
                "name": "Git Bash",
                "source": "Git"
            },
            {
                "guid": "{f2c8c022-3f4c-5b1c-98ca-5189c7ed80ef}",
                "hidden": false,
                "name": "Ubuntu",
                "source": "Microsoft.WSL"
            },
            {
                "guid": "{db8e8d9c-54f3-5b08-84b2-2d49b6b1f34e}",
                "hidden": false,
                "name": "Ubuntu",
                "source": "Microsoft.WSL"
            },
            {
                "guid": "{6e2bc259-e838-5293-9588-271eaece0c66}",
                "hidden": false,
                "name": "Ubuntu",
                "source": "Microsoft.WSL"
            },
            {
                "guid": "{9380c5c7-037e-5947-a523-34a8ed04211b}",
                "hidden": false,
                "name": "Debian",
                "source": "Microsoft.WSL"
            }
        ]
    },
}
```

Simpan dan restart terminal

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-22%20180736.png?raw=true)

### 5. Untuk VS Code

Tambahkan ke settings.json dengan cara tekan ctrl + shift + p lalu akan muncul

![Logo Aplikasi](https://github.com/fauzhanFARTF/notes/blob/main/img-oh-my-zsh/Screenshot%202025-07-23%20083550.png?raw=true)

ketik setting -> pilih preferences Open user Setting (JSON)

Lalu tambahkan di json tersebut

```json
"terminal.integrated.fontFamily": "FiraCode Nerd Font"
```

contoh :

```json
{
  // "terminal.integrated.fontFamily": "MesloLGS NF",
  "terminal.integrated.fontFamily": "FiraCode Nerd Font",
  "workbench.colorCustomizations": {
    "terminal.background": "#000000",
    "terminal.foreground": "#D0D0D0",
    "terminalCursor.background": "#111b74",
    "terminalCursor.foreground": "#D0D0D0",
    "terminal.ansiBlack": "#000000",
    "terminal.ansiBlue": "#013788",
    "terminal.ansiBrightBlack": "#808080",
    "terminal.ansiBrightBlue": "#0066FF",
    "terminal.ansiBrightCyan": "#00FFFF",
    "terminal.ansiBrightGreen": "#78f800",
    "terminal.ansiBrightMagenta": "#CC00FF",
    "terminal.ansiBrightRed": "#f72f2f",
    "terminal.ansiBrightWhite": "#ffffff",
    "terminal.ansiBrightYellow": "#FF0099",
    "terminal.ansiCyan": "#00FFFF",
    "terminal.ansiGreen": "#33FF00",
    "terminal.ansiMagenta": "#CC00FF",
    "terminal.ansiRed": "#f70606",
    "terminal.ansiWhite": "#d0d0d0",
    "terminal.ansiYellow": "#0af50a"
  },
```

## ✅ LANGKAH 5: Verifikasi Instalasi

Jalankan perintah berikut untuk memastikan semua berjalan lancar:

```bash
echo $SHELL
```

Harus menunjukkan:

```bash
/usr/bin/zsh
```
