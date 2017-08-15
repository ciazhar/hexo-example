---
title: Spring Config Service Security
date: 2017-08-15 10:08:41
categories:
  - Pemrograman
  - Spring
---

![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)

# Konfigurasi Config Server
- Tambahkan dependency `Spring Security`
- Tambahkan username dan password
```yml
security:
    user:
        name: username
        password: pass
```

# Konfigurasi Config Client
- Tambahkan username dan password
```yml
spring:
    cloud:
        config: 
            username: username
            password: pass
```