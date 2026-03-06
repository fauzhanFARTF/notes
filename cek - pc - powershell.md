# 🖥️ Pengecekan Spesifikasi PC Menggunakan PowerShell

## Pendahuluan

Dokumentasi ini menjelaskan cara mengecek spesifikasi hardware komputer Windows menggunakan **PowerShell** dengan memanfaatkan **WMI / CIM Classes**.

Metode ini berguna untuk:

- Inventaris perangkat IT
- Audit hardware komputer
- Dokumentasi perangkat
- Troubleshooting

---

## 📋 Daftar Isi

1. [Mengecek Motherboard](#1-mengecek-motherboard)
2. [Mengecek Storage](#2-mengecek-storage)
3. [Mengecek RAM](#3-mengecek-ram)
4. [Mengecek GPU](#4-mengecek-gpu)
5. [Mengecek System Product](#5-mengecek-system-product)
6. [Pengecekan Tambahan](#6-pengecekan-tambahan)
7. [Contoh Ringkasan Spesifikasi](#7-contoh-ringkasan-spesifikasi)

---

## 1️⃣ Mengecek Motherboard

Perintah:

```powershell
Get-CimInstance Win32_BaseBoard |
Select Manufacturer, Product, SerialNumber, Version
```

Penjelasan:

| Field        | Keterangan             |
| ------------ | ---------------------- |
| Manufacturer | Produsen motherboard   |
| Product      | Model motherboard      |
| SerialNumber | Nomor seri motherboard |
| Version      | Versi motherboard      |

Contoh hasil:

| Manufacturer | Product           | SerialNumber    | Version        |
| ------------ | ----------------- | --------------- | -------------- |
| ASRock       | X870 Riptide WiFi | M80-HB014800678 | Default string |

---

## 2️⃣ Mengecek Storage

Perintah:

```powershell
Get-CimInstance Win32_DiskDrive |
Select Model, SerialNumber, InterfaceType
```

Penjelasan:

| Field         | Keterangan                           |
| ------------- | ------------------------------------ |
| Model         | Model storage                        |
| SerialNumber  | Serial number storage                |
| InterfaceType | Jenis interface (SATA / NVMe / SCSI) |

Catatan:

NVMe sering muncul sebagai **SCSI** di Windows.

Contoh hasil:

| Model                | SerialNumber                            | InterfaceType |
| -------------------- | --------------------------------------- | ------------- |
| XPG GAMMIX S70 BLADE | 0000_0000_0000_0000_707C_18B3_E3C5_B1AA | SCSI          |

---

## 3️⃣ Mengecek RAM

Perintah:

```powershell
Get-CimInstance Win32_PhysicalMemory |
Select DeviceLocator, Manufacturer, PartNumber, SerialNumber
```

Penjelasan:

| Field         | Keterangan     |
| ------------- | -------------- |
| DeviceLocator | Slot RAM       |
| Manufacturer  | Produsen RAM   |
| PartNumber    | Tipe RAM       |
| SerialNumber  | Nomor seri RAM |

Contoh hasil:

| Slot   | Manufacturer      | PartNumber             |
| ------ | ----------------- | ---------------------- |
| DIMM 1 | A-DATA Technology | AX5U6400C3232G-DCLARBK |
| DIMM 2 | A-DATA Technology | AX5U6400C3232G-DCLARBK |

---

## 4️⃣ Mengecek GPU

Perintah:

```powershell
Get-CimInstance Win32_VideoController |
Select Name, PNPDeviceID
```

Penjelasan:

| Field       | Keterangan         |
| ----------- | ------------------ |
| Name        | Nama GPU           |
| PNPDeviceID | Device ID hardware |

Contoh hasil:

| GPU                     |
| ----------------------- |
| AMD Radeon Graphics     |
| NVIDIA GeForce RTX 4060 |

Artinya komputer memiliki:

- iGPU AMD
- GPU Dedicated NVIDIA RTX 4060

---

## 5️⃣ Mengecek System Product

Perintah:

```powershell
Get-CimInstance Win32_ComputerSystemProduct |
Select Name, IdentifyingNumber
```

Penjelasan:

| Field             | Keterangan         |
| ----------------- | ------------------ |
| Name              | Nama produk sistem |
| IdentifyingNumber | Nomor identifikasi |

Contoh hasil:

| Name              | IdentifyingNumber |
| ----------------- | ----------------- |
| X870 Riptide WiFi | Default string    |

---

## 6️⃣ Pengecekan Tambahan

### CPU

```powershell
Get-CimInstance Win32_Processor |
Select Name, NumberOfCores, NumberOfLogicalProcessors
```

---

### Total RAM

```powershell
Get-CimInstance Win32_ComputerSystem |
Select TotalPhysicalMemory
```

---

### BIOS

```powershell
Get-CimInstance Win32_BIOS |
Select Manufacturer, SMBIOSBIOSVersion
```

---

## 7️⃣ Contoh Ringkasan Spesifikasi

Contoh hasil pengecekan perangkat:

| Komponen    | Spesifikasi                           |
| ----------- | ------------------------------------- |
| Motherboard | ASRock X870 Riptide WiFi              |
| Storage     | XPG GAMMIX S70 Blade NVMe             |
| RAM         | A-DATA DDR5 AX5U6400C3232G            |
| GPU         | AMD Radeon Graphics + NVIDIA RTX 4060 |

---

# 📌 Kesimpulan

PowerShell dapat digunakan untuk mengecek spesifikasi hardware secara cepat tanpa aplikasi tambahan dengan memanfaatkan **CIM / WMI Classes** seperti:

- `Win32_BaseBoard`
- `Win32_DiskDrive`
- `Win32_PhysicalMemory`
- `Win32_VideoController`
- `Win32_Processor`

Metode ini sangat cocok untuk:

- Dokumentasi inventaris IT
- Audit perangkat komputer
- Troubleshooting hardware
