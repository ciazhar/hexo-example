---
title: Melakukan Tracing antar Microservice menggunakan Netflix Sleuth
date: 2017-08-20 08:42:20
categories:
  - Pemrograman
  - Spring
---
![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)

Spring Cloud Netflix Sleuth digunakan untuk membuat log tracing antar service. Sleuth dalam melakukan tracing, dia menggunakan Trace ID dan Span ID. Trace ID merupakan id yang digunakan untuk mentracing lintas service. Sedangkan Span ID merupakan ID yang digunakan untuk mentracing internal service.

# Implement Sleuth
- Tambahkan dependency `spring-cloud-starter-sleuth` dan `spring-boot-starter-web`

# Komunikasi Data antar Sleuth Client

- Controller pada client pertama (jalan di port 8080)

```java
@RestController
public class SimpleController {

    org.slf4j.Logger LOGGER = org.slf4j.LoggerFactory.getLogger(this);

    @RequestMapping("/api/halo")
    public String halo (){
        LOGGER.info("Sampai ke Server")
        return "Halo ini dari Client Satu";
    }
}
```

- Konfigurasi RestTemplate pada client kedua (jalan di port 8081)
```java
@Configuration
public class SimpleConfig {

    @Bean
    RestTemplate restTemplate(){
        return new RestTemplate();
    }
}
```

Sletuh akan terinjek kedalam restTemplate lewat Bean di atas.


- Controller pada client kedua
```java
@RestController
public class SimpleController {
    @Autowired private RestTemplate restTemplate;
    org.slf4j.Logger LOGGER = org.slf4j.LoggerFactory.getLogger(this);
    @RequestMapping("/api/halo")
    public String halo(){
        LOGGER.info("Sebelum sampai ke server");
        return restTemplate.getForObject("http://localhost:8080/api/halo",String.class);
        LOGGER.info("Setelah sampai ke server);
    }
}
```