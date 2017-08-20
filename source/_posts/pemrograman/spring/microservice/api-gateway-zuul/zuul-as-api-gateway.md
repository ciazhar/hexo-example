---
title: Membuat API Gatewat Menggunakan Netflix Zuul
date: 2017-08-18 22:00:46
categories:
  - Pemrograman
  - Spring
---
![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)

[Spring Cloud Netflix Zuul](https://github.com/Netflix/zuul) merupakan gerbang utama yang akan dilewati oleh request dari apps atau website yang menuju backend. Zuul dapat berfungsi sebagai API Gateway, security, dll.

# Membuat API Gateway
[Sebelumnya](https://ciazhar.github.io/2017/08/18/pemrograman/spring/microservice/circuit-breaker-hystrix/circuit-breaker-with-hystrix/) kita telah membuat eureka server dan eureka client yang terintegrasi dengan Hystrix. 
Sekarang kita akan mencoba membuat api gatewat dan mengintegrasikanya.

- Buat project baru menggunakan Spring Initializr
- Tambahkan dependency `spring-cloud-starter-zuul`.
- Tambahkan anotasi `@EnableZuulProxy` pada main class
- Tambahkan konfigurasi zuul
```yml
spring:
  application:
    name: api-gateway
zuul:
  prefix: /api
  routes:
    eureka-client:
      path: /pertama/**
      serviceId: EUREKA-CLIENT
    other-eureka-client:
      path: /kedua/**
      serviceId: OTHER-EUREKA-CLIENT
server:
  port: 8004
```
Dengan adanya API Gateway untuk memanggil API dari masing masing backend tidak harus memanggilnya secara manual dengan menyebutkan portnya, tetapi hanya perlu memanggilnya via API Gateway sesuai pathnya. Nantinya service yang bernama eureka-client akan diinisialisasi menggunakan path /pertama. Sedangkan service yang bernama eureka-client akan diinisialisasi menggunakan path /kedua. 

Apabila dulu jika ingin mengakses API di service eureka-client menggunakan http://localhost:8002/api/halo sekarang dapat diganti dengan http://localhost:8004/api/pertama/api/halo. Sedangkan apabila dulu jika ingin mengakses API di service other-eureka-client menggunakan http://localhost:8003/api/halo sekarang dapat diganti dengan http://localhost:8004/api/kedua/api/halo.

Hal ini akan meringankan beban dalam development aplikasi karena tidak perlu menghafal port untuk setiap servicenya, tetapi hanya perlu mengetahui nama servinya.

- Konfigurasi tambahan
```yml
# Konfigurasi Config Service
spring:
  cloud:
    config:
      uri: http://localhost:10003

# Konfigurasi Discovery Service
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8001/eureka

# Konfigurasi Circuit Breaker
hystrix:
  command:
    default:
      execution:
        isolation:
          thread:
            timeoutInMilliseconds: 10000
```