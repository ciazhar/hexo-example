---
title: Integrating Backend to Config Service
date: 2017-08-14 22:40:19
categories:
  - Pemrograman
  - Spring
---

![](https://stocklogos-pd.s3.amazonaws.com/styles/logo-medium-alt/logos/image/1398937767-b70129ba6592929d32c0337c3eea2880.png?itok=NBZRaOhz)

- Tambahkan Dependency `Spring Cloud Starter Config` pada pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
- Konfigurasi config server uri pada src/main/resource/bootstrap.yml
```yml
spring:
    cloud:
        config:
            uri: http://localhost:10003
```