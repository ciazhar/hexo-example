---
title: Bagaimana Perangkat Elektronik Berjalan ?
date: 2017-04-15 16:56:24
tags:
  - komputer
categories:
  - Teknologi
  - Organisasi dan Arsitektur Komputer
---


Dalam kehidupan sehari-hari kita sering sekali menggunakan perangkat elektronik seperti komputer, laptop dan hp. Perangkat elektronik tersebut sudah didesain sedimikian rupa agar dapat nyaman berinteraksi dengan penggunanya, baik dari desain, perangkat input dll. Tetapi pernahkah anda berpikir bagaimana cara kerjanya alat-alat tersebut? Bagaimana data dari keyboard, mouse atau perangkat input lainya diproses ? Dan tentunya akan banyak sekali pertanyaan mengenai hal tersebut. Pada kesempatan ini saya akan sedikit menceritakan bagaimana proses data di perangkat elektronik tersebut.

## Proses Booting
Hal pertama yang dilakukan perangkat saat proses booting adalah melakukan booting Sistem Operasi. Kemudian perangkat akan melakukan inisialisasi, yaitu melakukan checklist terhadap hardware yang terhubung dengan perangkat kita.

## Transfer Data pada Komputer
Data yang kita inputkan melalui perangkat masukan sebenarnya adalah kumpulan pola arus listrik yang dikonversi menjadi kode biner. Secara teknis untuk tegangan 0 volt akan dikonversi menjadi kode biner 0 dan tegangan 5 volt akan dikonversi menjadi kode biner 1. Proses konversi dari arus listrik menjadi biner ini dilakukan oleh `Flip Flop` yang terdiri dari kumpulan gerbang logika. Data biner tersebut kemudian dibawa menuju `register` yang ada pada processor untuk disimpan. Setiap kode biner akan menghuni satu space register. Pengggambaran bagaimana data tersebut disimpan adalah seperti gambar di bawah ini :
```
_________________________________
|       |       |       |       |
|   1   |   2   |   3   |   4   | --> Register
|_______|_______|_______|_______|   
|       |       |       |       |
|   0   |   1   |   0   |   0   | --> Biner
|_______|_______|_______|_______|
```
Sedikit Info tentang Processor, dia memiliki bagian yang memiliki fungsi masing masing. Bagian tersebut diantaranya adalah :
- ALU
- Control Unit
- Register

Lanjut, data yang ada pada register kemudian diproses, apakah akan dioutputkan atau akan disimpan sesuai dengan yang kita inginkan. Apabila ingin dioutputkan data akan ditransfer menuju perangkat keluaran yang dikehendaki, semisal layar monitor. Dan apabila ingin disimpan sebelumnya akan dikonversi menuju kode heksal. Proses konversi dari kode biner dan heksal dan sebaliknya dilakukan oleh Sistem Operasi.

Data pada hardisk yang berupa kode heksal apabila ingin diproses maka harus dikonversi kembali menjadi kode desimal. Data tersebut kemudian diteruskan melalui RAM dan berakhir di Processor. Dalam tahap pemrosesan data, data tadi akan disimpan sementara pada cache memory yang ada pada processor.
