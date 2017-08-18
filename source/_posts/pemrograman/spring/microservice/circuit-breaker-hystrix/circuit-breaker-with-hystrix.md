---
title: Circuit Breaker With Hystrix
date: 2017-08-18 16:45:52
categories:
  - Pemrograman
  - Spring
---
![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)

# Defending API from failure by bringing callback
Sebagai contoh kita akan menggunakan project dari tutorial sebelumnya (netflix eureka). Konfigurasi berikut akan dilakukan pada client kedua (spring.application.name=client-dua).

- Tambahkan dependency `spring-cloud-starter-hystrix`.
- Tambahkan anotasi `@EnableCircuitBreaker` pada main class.
- Tambahkan anotasi `@HystrixCommand` pada API yang ingin di fallback. Tambahkan parameter `fallbackMethod` di dalam command tersebut. Isi dengan nama methode yang berisi string yang akan ditampilkan saat fallback.
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