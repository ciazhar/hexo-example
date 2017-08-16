---
title: Spring Cloud Netfix Eureka as Discovery Service
date: 2017-08-15 10:29:45
categories:
  - Pemrograman
  - Spring
---
![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)

Eureka adalah discovery service yang didevelop oleh netfix. Discovery service sendiri berfungsi untuk menampung data semua service yang ada di microservice.

# Server
- Tambahkan dependency `Eureka Server`
- Tambahkan anotasi `@EnableEurekaServer` pada main class
- baru (bootstrap.yml)
```yml
# config server port
server:
    port: 8761 


eureka:
    instance:
        # config hostname
        hostname: localhost
    client:
        # config tidak diperbolehkan aplikasi lain terintegrasi dengan eureka
        register-with-eureka: false
        # 
        feign-registry: false
```

# Client
- Tambahkan dependency `Eureka Client`
- Tambahkan anotasi `@EnableEurekaClient` pada main class
- Atur eureka server uri (bootstrap.yml)
```yml
eureka:
    client: 
        service-url:
            defaultZone: http://localhost:8761/eureka
```
