---
title: Spring Cloud Netfix Eureka as Discovery Service
date: 2017-08-15 10:29:45
categories:
  - Pemrograman
  - Spring
---
![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)

Eureka adalah discovery service yang didevelop oleh netfix. Discovery service sendiri berfungsi untuk menampung data semua service yang ada di microservice. Discovery service juga dapat mempermudah komunikasi antar service yang berdiri di atasnya.

# Implement Eureka Server
- Tambahkan dependency `spring-cloud-eureka-server`
- Tambahkan anotasi `@EnableEurekaServer` pada main class
- Tambahkan konfigurasi eureka service (application.yml)
```yml
spring:
  application:
    name: eureka-service

server:
  port: 8761

eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
    server:
      waitTimeInMsWhenSyncEmpty: 0
```

# Implement Eureka Client
- Tambahkan dependency `spring-cloud-starter-eureka`
- Tambahkan anotasi `@EnableDiscoveryClient` pada main class
- Tambahkan konfigurasi eureka server (bootstrap.yml)
```yml
spring:
  application:
    name: eureka-client
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka
server:
  port: 8002
```

# Komunikasi Data antar Eureka Client
Kita misalkan terdapat 2 eureka client, client pertama(spring.application.name=eureka-client) berjalan di port 8002, sendangkan client kedua(spring.application.name=other-eureka-client) berjalan di port 8003. Client kedua ingin mengambil API dari client pertama menggunakan eureka server. 
Berikut contoh kode untuk komunikasi antar client. 
- Controller pada client pertama

```java
@RestController
public class SimpleController {

    @RequestMapping("/api/halo")
    public String halo (){
        return "Halo ini dari Client Satu";
    }
}
```
- Konfigurasi RestTemplate pada client kedua

```java
@Configuration
public class SimpleConfig {

    @Bean
    @LoadBalanced
    RestTemplate restTemplate(){
        return new RestTemplate();
    }
}
```
- Controller pada client kedua

```java
@RestController
public class SImpleController {
    @Autowired private RestTemplate restTemplate;

    @RequestMapping("/api/halo")
    public String halo(){
        return restTemplate.getForObject("http://eureka-client/api/halo",String.class);
    }
}
```
Bisa dilihat pada controller client kedua mengambil API dari client pertama menggunakan RestTemplate dengan tidak mengghardcode url APInya, tetapi hanya mencantumkan `spring.application.name` dari client pertama. Dan data dari API tersebut kemudian disimpan dan dikembalikan dalam tipe data String.