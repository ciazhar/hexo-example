---
title: Config Service Refresh Scope and Health Check
date: 2017-08-14 23:20:36
categories:
  - Pemrograman
  - Spring
---

![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)

# Refresh Scope
Refresh Scope memungkinkan kita untuk mengupdate API yang berisi data konfigurasi pada konfig service tanpa redeploy aplikasi client dan server. Sehingga data yang di dapatkan aplikasi client akan selalu up to date. Konfigurasi dilakukan di config client.

- Tambahkan anotasi `@RefreshScope` pada class yang membutuhkan data dari file konfigurasi
- Tambahkan dependency `Spring Actuator`
- Disable Security default (bootstrap.yml)
```yml
management:
    security:
        enabled: false
```
- Enable username & password to secure client app(bootstrap.yml)
Sebelumnya anda harus menambahkan dependency `Spring Security`.
```yml
security:
  user:
    name: usernameusr
    password: passwordusr
```
- Untuk merefresh kofigurasi gunakan endpoint `http://localhost:PORT/refresh`

# Health Check

- Untuk melihat keadaan config service gunakan endpoint `localhost:PORT/health`
