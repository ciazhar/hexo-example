---
title: Membuat Launcher di Linux
date: 2017-10-15 20:36:13
tags:
- linux
categories:
  - Linux
---

![](/images/linux.jpg)

# Membuat Launcher di Linux

Apakah anda pernah menginstall apikasi di linux ? Sebenearnya di linux terdapat banyak cara dalam menginstall aplikasi tergantung dari jenis filenya, diantaranya :

- Menggunakan Software Center.
- Menggunakan perintah `sudo apt install {nama_package}` pada terminal
- Menggunakan executable file dengan ektensi seperti `.deb`, `.rpm` atau `.sh`
- Menggunakan binary file yang di kompres dalam `.tar.gz`.

Untuk aplikasi yang di kompress dalam `.tar.gz`, terkadang setelah menginstallnya, sistem tidak otomatis membuat Launcher untuk aplikasi tersebut. Sehingga kita harus membuat Launcher secara manual.
Launcher sendiri bisa dibilang cara GUI/Shortcut untuk menjalankan aplikasi tersebut. Biasanya terletak di `whisker` (star menu kalo di w*nd*ws).

Oleh karena itu kita akan coba membuat Launcher untuk aplikasi kita. Saya akan memberi contoh untuk membuat launcher aplikasi `Robomongo`.

## 1. Pindah direktori ke `/usr/share/applications/` menggunakan terminal

```bash
cd /usr/share/appications/
```

## 2. Buat file berekesensi `.dekstop`. Nama file dapat diesusaikan dengan nama apikasi

```bash
touch robomongo.desktop
```

## 3. Buka file tersebut menggunakan teks editor kesayangan anda. Disini saya akan menggunakan gedit

```bash
sudo gedit robomongo.desktop
```

## 4. Isi file tersebut dengan format seperti di bawah ini

```desktop
[Desktop Entry]
Version=
Type=
Name=
Comment=
Exec=
Icon=
Path=
Terminal=
StartupNotify=
```

Keterangan :

- Version       : versi aplikasi
- Type          : tipe aplikasi
- Name          : nama aplikasi
- Comment       : comment aplikasi
- Exec          : cara mengeksekusi aplikasi tsb
- Icon          : direktori untuk icon aplikasi tersebut
- Path          : direktori aplikasi tersebut
- Terminal      : apakah aplikasi khusus untuk berjalan di terminal
- StartupNotify : apakah akan ada notifikasi waktu aplikasi berjalan

Berikut contohnya untuk aplikasi Robomongo saya :

```desktop
[Desktop Entry]
Version=1.0
Type=Application
Name=Robomongo
Comment=Robomongo
Exec=/home/ciazhar/Application/robomongo-1.0.0/bin/robomongo
Icon=/home/ciazhar/Application/robomongo-1.0.0/CWNda0_WwAAWE-F.png
Path=/home/ciazhar/Application/robomongo-1.0.0
Terminal=false
StartupNotify=false
```

Finally Laucher telah dapat digunakan dan sudah tersedia di whisker.