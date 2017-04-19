---
title: Sistem Bilangan
date: 2017-04-17 19:56:24
tags:
  - komputer
categories:
  - Teknologi
  - Organisasi dan Arsitektur Komputer
---

# Macam-macam Sistem Bilangan
- Biner (basis 2)
  Simbol : 0,1
- Oktal (basis 8)
  Simbol : 0,1,2,3,4,5,6,7
- Desimal (basis 10)
  Simbol : 0,1,2,3,4,5,6,7,8.9
- Heksal (basis 16)
  Simbol : 0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15

# Konversi antar Sistem Bilangan
- Desimal ke Biner


  Contoh : Semisal kita akan mengubah 123(10) ke biner. Hal pertama yang harus kita lakukan adalah membagi angka tersebut dengan 2, kemudian hasil pembagian kita taruh dibagian bawah. Dan apabila angka habis dibagi 2 maka kita tulis 0 dan apabila bersisa kita tulis 1 di bagian samping. Lakukan langkah tersebut secara berulang-ulang sampai hasilnya tidak bisa dibagi 2 lagi. Contohnya adalah sebagai berikut :
  ```
  123
  --- =  1
  61
  --- = 1
  30
  --- = 0
  15
  --- = 1
  7
  --- = 1
  3
  --- = 1
  1
  ```
  Dari hasil diatas kita dapatkan hasil 1 1 1 1 0 1 1 (dibaca dari bawah). Jadi biner dari 123 adalah 1111011.

- Biner ke Desimal


  Contoh : Semisal kita akan mengubah 1111011(2) ke desimal. Hal pertama yang kita lakukan adalah mendefinisikan tiap digit dengan 2 pangkat nomer digit. Digit dihitung dari belakang. Contohnya adalah sebagai berikut :
  ```
  2^6   2^5   2^4   2^3   2^2   2^1   2^0
  64    32    16    8     4     2     1

  1     1     1     1     0     1     1
  ```
  Kemudian kita tambahkan tiap hasil dari 2 pangkat nomer digit yang bilangan binernya 1.
  64+32+16+8+4+2+1 = 123. Dari penjumlahan tersebut kita dapatkan hasil 123, jadi desimal dari 1111011 adalah 123.
