# Menginstal WSL (Windows Subsystem for Linux)

## 🛠️ LANGKAH 1: Instal WSL (Windows Subsystem for Linux)

### 1. Buka PowerShell sebagai Administrator

- Klik tombol Start , ketik PowerShell
- Klik kanan → Run as administrator

### 2. Aktifkan Virtual Machine Platform

- Di Powershell ketikkan

    ```powershell
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    ```

    Contoh

    ```powershell
    PS C:\Windows\system32>dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

    Deployment Image Servicing and Management tool
    Version: 10.0.26100.1150

    Image Version: 10.0.26100.4652

    Enabling feature(s)
    [==========================100.0%==========================]
    The operation completed successfully.

    ```

- Jika Anda belum mengaktifkan WSL sebelumnya, jalankan juga:

    ```powershell
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    ```

    contoh

    ```powershell
    PS C:\Windows\system32>dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

    Deployment Image Servicing and Management tool
    Version: 10.0.26100.1150

    Image Version: 10.0.26100.4652

    Enabling feature(s)
    [==========================100.0%==========================]
    The operation completed successfully.

    ```

- Jalankan perintah berikut:

    powershell

    ```powershell
    wsl --install
    ```

    Ini akan mengaktifkan fitur WSL dan menginstal distribusi Linux default (biasanya Ubuntu).

    nanti kamu akan diminta

    1. Membuat username

    2. Membuat password

    Output

    ```powershell
    PS C:\Windows\system32> wsl --install
    Downloading: Ubuntu
    Installing: Ubuntu
    Distribution successfully installed. It can be launched via 'wsl.exe -d Ubuntu'
    Launching Ubuntu...
    Provisioning the new WSL instance Ubuntu
    This might take a while...
    Create a default Unix user account: fauzhan
    New password:
    Retype new password:
    passwd: password updated successfully
    To run a command as administrator (user "root"), use "sudo <command>".
    See "man sudo_root" for details.

    fauzhan@Arroyan:/mnt/c/Windows/system32$
    ```

- Restart komputer

- Cara Mengecek Versi WSL

    ```powershell
    wsl --version
    ```

    contoh:

    ```powershell
    # Mengecek Versi WSL
    PS C:\Windows\system32> wsl --version
    WSL version: 2.5.9.0
    Kernel version: 6.6.87.2-1
    WSLg version: 1.0.66
    MSRDC version: 1.2.6074
    Direct3D version: 1.611.1-81528511
    DXCore version: 10.0.26100.1-240331-1435.ge-release
    Windows version: 10.0.26100.4652
    ```

- Mengecek distribusi yang telah terinstall  

    ```powershell
    wsl --list
    ```

    contoh

    ```powershell
    PS C:\Windows\system32> wsl --list
    Windows Subsystem for Linux Distributions:
    Ubuntu (Default)
    ```

- Keluar dari wsl

    ```powershell
    exit
    ```

    contoh :

    ```powershell
    fauzhan@Arroyan:/mnt/c/Windows/system32$ exit
    exit
    ```

- di start menu buka aplikasi ubuntu (WSL yang telah terinstall)

## 🐧 LANGKAH 2: Instal Distribusi Linux (jika belum)
Jika kamu ingin menggunakan distribusi lain selain Ubuntu, kamu bisa tambahkan dengan di powershell

``` powershell
wsl --install -d <NamaDistribusi>
```

Contoh:

```powershell
wsl --install -d Debian
```

Mengecek Daftar distribusi yang tersedia:

```powershell
wsl --list --online
```

Hasil Output

```powershell
PS C:\Windows\system32> wsl --list --online
The following is a list of valid distributions that can be installed.
Install using 'wsl.exe --install <Distro>'.

NAME                            FRIENDLY NAME
AlmaLinux-8                     AlmaLinux OS 8
AlmaLinux-9                     AlmaLinux OS 9
AlmaLinux-Kitten-10             AlmaLinux OS Kitten 10
AlmaLinux-10                    AlmaLinux OS 10
Debian                          Debian GNU/Linux
FedoraLinux-42                  Fedora Linux 42
SUSE-Linux-Enterprise-15-SP6    SUSE Linux Enterprise 15 SP6
SUSE-Linux-Enterprise-15-SP7    SUSE Linux Enterprise 15 SP7
Ubuntu                          Ubuntu
Ubuntu-24.04                    Ubuntu 24.04 LTS
archlinux                       Arch Linux
kali-linux                      Kali Linux Rolling
openSUSE-Tumbleweed             openSUSE Tumbleweed
openSUSE-Leap-15.6              openSUSE Leap 15.6
Ubuntu-18.04                    Ubuntu 18.04 LTS
Ubuntu-20.04                    Ubuntu 20.04 LTS
Ubuntu-22.04                    Ubuntu 22.04 LTS
OracleLinux_7_9                 Oracle Linux 7.9
OracleLinux_8_10                Oracle Linux 8.10
OracleLinux_9_5                 Oracle Linux 9.5
PS C:\Windows\system32>
```

## Jika Error waktu instalasi

> The operation could not be started because a required feature is not installed.
Error code: Wsl/InstallDistro/Service/RegisterDistro/CreateVm/HCS/HCS_E_SERVICE_NOT_AVAILABLE

### Aktifkan Hyper-V secara manual

  1. Buka PowerShell sebagai Administrator dan jalankan:

      ```powershell
      Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
      ```

  2. Setelah selesai, restart komputer .

  3. Setelah restart, cek apakah layanan Hyper-V sudah ada:

      ```powershell
      Get-Service -Name "vmcompute"
      ```

      Contoh

      ```powershell
      PS C:\Windows\system32> Get-Service -Name "vmcompute"
      Status   Name               DisplayName
      ------   ----               -----------
      Running  vmcompute          Hyper-V Host Compute Service
      ```

  4. Dan cek juga apakah Hyper-V sudah muncul:

      ```powershell
      Get-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V
      ```

      Harus menunjukkan State: Enabled .

      Contoh 
      PS C:\Windows\system32> Get-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V"

      ```powershell
      FeatureName      : Microsoft-Hyper-V
      DisplayName      : Hyper-V Platform
      Description      : Provides the services that you can use to create and manage virtual machines and their resources.
      RestartRequired  : Possible
      State            : Enabled
      CustomProperties :
      ```

  5. Kembali ke langkah instalasi awal

## Ringkasan

  ```powershell
  # Cek versi Windows
  Get-WinVersion

  # Cek status fitur WSL
  Get-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

  # Cek status Virtual Machine Platform
  Get-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform

  # Cek status Hyper-V
  Get-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V

  # Cek status layanan vmcompute
  Get-Service -Name "vmcompute" -ErrorAction SilentlyContinue

  ```
