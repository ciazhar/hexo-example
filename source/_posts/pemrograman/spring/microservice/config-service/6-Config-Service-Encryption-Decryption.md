---
title: Config Service Encryption Decryption
date: 2017-08-14 11:37:37
categories:
  - Pemrograman
  - Spring
---

![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)

Saat client mengambil konfigurasi dari config service secara default semua data tidak terenkripsi. Sehingga data data credential seperti password dan lain lain dapat langsung diketahui apabila telah mendapatkan file konfigurasinya. Untuk mengurangi bocornya data ada baiknya data credential tersebut kita enkripsi.
Spring Cloud Config Server mensupport enkripsi dan dekripsi. Untuk menggunakannya ikuti langkah langkah berikut

- Download Java Criptography Enxtension (JCE)
- Replace fIle konfigurasi telah ada dengan file JCE yang telah di download
- Konfigurasi encrypt key (resource/bootstrap.yml)
```yml
encrypt:
  key: abcdef
```
- Run
- Untuk mengenkripsi, lakukan POST ke `localhost:8080/encrypt` dengan memasukkan data yang ingin di encrypt pada Body HTTP. Semisal kita ingin mengekripsi password dengan value ciazhar123. Maka masukkan password tersebut ke dalam Body HTTP, lalu POST. Kita akan mendapatkan response berupa hasil enkripsi yang dapat kita gunakan untuk mereplace data kita dengan hasil enkripsi tersebut. Hasil enkripsi tersebut dapat dipasang dengan cara seperti ini :
```yml
password : {cipher}1n1p455w0rd3nkr1ps1
```
- Untuk mendekripsi, lakukan POST ke `localhost:8080/decrypt` dengan memasukkan data yang ingin di decrypt pada Body HTTP.
- Konfig value yang terenkripsi agar tetap terenkripsi (resource/bootstrap.yml)
```yml
spring:
  cloud:
    config:
      server:
        encrypt:
          enabled: false
```
- Tambahkan encrypt ket pada aplikasi client agar dapat mendekip value ()
```yml
encypt:
  key: abcdef
```