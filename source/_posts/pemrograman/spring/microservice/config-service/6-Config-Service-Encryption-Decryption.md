---
title: Config Service Encryption Decryption
date: 2017-08-14 11:37:37
categories:
  - Pemrograman
  - Spring
---

![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)

Saat client mengambil konfigurasi dari config service secara default semua data tidak terenkripsi. Sehingga data data credential seperti password dan lain lain dapat langsung diketahui apabila telah mendapatkan file konfigurasinya. Untuk mengurangi bocornya data ada baiknya data credential tersebut kita enkripsi.

Spring Cloud Config Server mensupport enkripsi dan dekripsi. Untuk menggunakannya ikuti langkah langkah berikut :
- Download Java Criptography Enxtension (JCE)
- Replace fIle konfigurasi telah ada pada desktop kita dengan file JCE yang telah di download
- Konfigurasi encrypt key (resource/bootstrap.yml)

```yml
encrypt:
  key: abcdef
```
Encrypt key akan menentukan hasil dari enkripsi dan kunci untuk mendekrip.

- Konfig value yang terenkripsi agar tetap terenkripsi (resource/bootstrap.yml)

```yml
spring:
  cloud:
    config:
      server:
        encrypt:
          enabled: false
```
- Tambahkan encrypt key pada aplikasi client agar dapat mendekip value ()

```yml
encypt:
  key: abcdef
```

- Jalankan program

Untuk mengenkripsi, lakukan POST ke `localhost:8080/encrypt` dengan memasukkan data yang ingin di encrypt pada Body HTTP. Semisal kita ingin mengekripsi password dengan value ciazhar123. Maka masukkan password tersebut ke dalam Body HTTP, lalu POST. Dapat menggunakan curl untuk mempermudah :

```
curl localhost:8080/encrypt -d value
```
Selanjutnya kita akan mendapatkan response berupa hasil enkripsi yang dapat kita gunakan untuk mereplace data kita dengan hasil enkripsi tersebut. Hasil enkripsi tersebut dapat dipasang dengan cara seperti ini :

```yml
password : {cipher}1n1p455w0rd3nkr1ps1
```
- Untuk mendekripsi, lakukan POST ke `localhost:8080/decrypt` dengan memasukkan data yang ingin di decrypt pada Body HTTP.
Dapat menggunakan curl untuk mempermudah :

```
curl localhost:8080/decrypt -d value
```