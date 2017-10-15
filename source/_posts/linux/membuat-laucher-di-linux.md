---
title: Membuat Launcher di Linux
date: 2017-10-15 20:36:13
tags:
- linux
categories:
  - Linux
---

# Membuat Launcher di Linux

Terdapat banyak cara dalam menginstall aplikasi di linux tergantung dari jenis filenya, diantaranya :
- Menggunakan `apt install` pada terminal
- Menggunakan executable file dengan ektensi seperti `.deb`, `.rpm` / `.sh`
- Menggunakan binary file yang di kompres dalam `.tar.gz`.

Untuk aplikasi yang di kompress dalam `.tar.gz` karena untuk menggunakanya hanya dicopy kedalam direktori kita dan tidak diinstall, atau aplikasi yang diinstall terkadang tidak otomatis membuat Launcher. Launcher bisa dibilang cara menjalankan aplikasi tersebut melalui GUI. Biasanya terletak di `whisker`. 
Oleh karena itu kita akan coba membuat Launcher untuk aplikasi kita.
Untuk kalo ini saya akan memberi contoh menggunakan aplikasi `Robomongo`. 
Caranya cukup mudah, pertama buat file dengan ekstensi `.desktop` dengan nama sesuai nama aplikasi kita. Kemudian isi file tersebut dengan format seperti :
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
```
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

Kemudian simpan file tersebut di direktori `/usr/share/applications/`. Hati hati dengan dalam menyimpan file karena membutuhkan Permission.

Finally Laucher telah dapat digunakan dan sudah tersedia di whisker.