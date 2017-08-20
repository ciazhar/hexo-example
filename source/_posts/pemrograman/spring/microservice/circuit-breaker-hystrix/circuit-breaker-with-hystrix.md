---
title: Membuat Circuit Breaker menggunakan Netflix Hystrix
date: 2017-08-18 16:45:52
categories:
  - Pemrograman
  - Spring
---
![](https://cdn-images-1.medium.com/max/264/0*gRZh5dHFWz-nFu7Z.png)

[Spring Cloud Netflix Hystrix](https://github.com/Netflix/Hystrix/blob/master/README.md) digunakan untuk memeberikan fallback apabila terjadi kegagalan saat request antar service dengan cara melakukan Load Balancing.

# Defending API from failure by bringing callback
[Sebelumnya](https://ciazhar.github.io/2017/08/15/pemrograman/spring/microservice/discovery-service-eureka/netflix-eureka-as-discovery-service/) kita telah membuat eureka server. Sekarang kita akan coba mendefend API kita yang tedapat pada aplikasi `other-eureka-client`. Berikut konfigurasi pada client kedua.

- Tambahkan dependency `spring-cloud-starter-hystrix`.
- Tambahkan anotasi `@EnableCircuitBreaker` pada main class.
- Tambahkan anotasi `@HystrixCommand` pada API yang ingin di fallback. Tambahkan parameter `fallbackMethod` di dalam command tersebut. Valuenya merujuk pada nama methode yang berisi string yang akan ditampilkan saat fallback.

```java
///Berikut contoh controller APInya
@RequestMapping("/api/halo")
@HystrixCommand(fallbackMethod = "fallback")
public String halo(){
    return restTemplate.getForObject("http://eureka-client/api/halo",String.class);
}

///Berikut contoh method yang akan menampilkan string fallback
public String fallback(Throwable hystrixCommand){
    return "Fallback Halo";
}   
```
- Set berapa milisecond lantency untuk metrigger fallback
```yml
hystrix:
  command:
    default:
      execution:
        isolation:
          thread:
            timeoutInMilliseconds: 10000
```

Apabila request dari `other-eureka-client` ke `eureka-client` sukses makan akan tampil String seperti "Halo ini dari Client Satu". Sedangkan apabila gagal maka akan tampil String seperti "Fallback Halo".