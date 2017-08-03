---
title: Config Service 2
date: 2017-07-28 09:08:13
categories:
  - Pemrograman
  - Spring
---

![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)


# Membuat Config Service yang berisi lebih dari konfigurasi 1 service

Setelah kita membuat config service dengan 1 konfigurasi service, kita akan coba menambahkan beberapa konfigurasi aplikasi pada config service kita. Karena pada dasarnya config service ini yang akan menghandle file file konfigurasi dari bebagai microservice.

- Buat File konfigurasi
Contoh Konfigurasi aplikasi 1 Default(resource/app1/myapp.properties)
```
foo=bar
bar=bam
```
Contoh Konfigurasi aplikasi 1 untuk Developer Stage(resource/app1/myapp-dev.properties)
```
foo=bardev
bar=bam
```
Contoh Konfigurasi aplikasi 2 Default (resource/app2/myapp.properties)
```
foo=bar
bar=bam
```

- Tambahkan konfigurasi untuk multiple aplikasi menggunakan `spring.cloud.config.server.native.search-locations:`


Berikut adalah contohnya :
```
spring.cloud.config.server.native.search-locations:classpath:/config, classpath:/app1, classpath:/app2
```
> Nama folder konfigurasi ditulis setelah classpath:/ . Dalam konteks ini classpath berada di direktori src/main/resource.


Untuk dapat melihat hasilnya anda dapat mengakses beberapa url berikut :
```
http://localhost:8080/myapp/default
http://localhost:8080/myapp/dev
http://localhost:8080/myapp-default.json
http://localhost:8080/myapp-dev.json
```

# Override value konfigurasi
Kita dapat mengoverride konfgurasi yang identik, semisal untuk file `resource/app1/myapp.properties` dan `resource/app2/myapp.properties`. Kedua file konfigurasi tersebut sama-sama memiliki parameter bernama `foo`. Apabila anda ingin mengoverride value dari foo tersebut, dapat dilakukan dengan beberapa langkah berikut.

- Tambahkan konfigurasi untuk override konfigurasi
```
spring.cloud.config.server.overrides.<nama-parameter>=<value>
```
> Pada script diatas ada 2 nilai yang harus diisi yaitu nama-parameter yang akan di override  dan value dari parameter tersebut

Untuk dapat melihat hasilnya anda dapat mengakses beberapa url berikut :
```
http://localhost:8080/myapp/default
http://localhost:8080/myapp-default.json
http://localhost:8080/myapp-default.yml
```
