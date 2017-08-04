---
title: Spring Config Service
date: 2017-07-22 13:25:51
categories:
  - Pemrograman
  - Spring
---

![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)


## Spring Config Service
Spring Config service adalah sebuah service yang digunakan untuk menyimpan, mengakses, dan mengatur konfigurasi dari setiap service. Spring Config Service juga dapat mensupport version control untuk setiap file file konfigurasinya.

### Spring Config Service Endpoint
- View/Fetch Configuration (json / yml)

```
http://localhost:8080/config/{name}/{profile}/{label}
```
- Encrypt Value

```
curl localhost:8080/encrypt -d value
```
- Decrypt Value

```
curl localhost:8080/decrypt -d value
```
- Refresh Client

```
curl -x POST localhost:8080/refresh
```
