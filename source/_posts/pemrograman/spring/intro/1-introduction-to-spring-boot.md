---
title: Introduction to Spring
date: 2017-04-23 14:17:28
categories:
  - Pemrograman
  - Spring
sticky: true
---

![](/images/spring.png)

# Sekilas tentang Spring Framework

>[Spring Framework](http://spring.io) adalah Fullstack Web Framework yang dikembangkan oleh Pivotal menggunakan bahasa bahasa JVM (seperti Java, Kotlin dan Groovy).

Spring sendiri telah mengalami evolusi sampai beberapa kali, diantara lain :

- __Spring MVC__. Aplikasi spring edisi ini untuk masih dikonfigurasi secara manual, sehingga dalam development masih lambat. Web Server juga masih terpisah sehingga harus di deploy secara manual.
- __Spring MVC yang di wrap dengan Spring Boot__. Dengan adanya Spring Boot, setup project menjadi lebih cepat dan mudah. Web server juga sudah di embed sehingga tidak perlu di deploy secara manual. Secara default menggunakan Tomcat Web Server.
- __Spring Webflux yang di wrap dengan Spring Boot__. Spring Webflux menawarkan Reactive Programming yang Non Blocking. Web Server default diganti dengan netty yang lebih leightweight. Sehingga performa dari aplikasi spring dapat meningkat.

Sejauh ini secara pribadi spring merupakan framework paling lengkap yang pernah saya temui. Spring dapat mengatasi permasalahan  mulai dari masalah REST API sampai Microservice.

Framework ini merupakan __compiled framework__ karena dalam menjalankannya harus di compile terlebih dahulu. Oleh karena itu Spring memiliki performa yang lumayan bagus. Saya pernah melakukan benchmark menggunakan __wrk__ untuk melakukan hit API mendapatkan hasil sekitar 30.000an request per detik. Lebih detailnya dapat di cek di [Laman Berikut]().

Walaupun memiliki performa yang lumayan, framework ini memiliki waktu startup yang relatif lama, sekitar 10 detik lebih. Sehingga apabila anda memiliki RAM lebih saya menyarankan menggunakan build tool __Gradle__ daripada Maven untuk mempercepat proses kompilasi.

## Roadmap Belajar Spring

Berikut sekilas peta jalan yang dapat anda pelajari untuk dapat membuat aplikasi spring. Happy Coding :D.

### [1. Setup Project Spring Boot](https://ciazhar.github.io/2017/04/23/pemrograman/spring/intro/2-setup-project-spring-boot/)

### [2. Membuat Web pada Spring Boot menggunakan Template Engine](https://ciazhar.github.io/2017/04/23/pemrograman/spring/web/membuat-web-sederhana-dengan-spring-boot-starter-web-dan-thymeleaf/)
##### [2.1. Berkenalan dengan Template Engine Thymeleaf]()
##### [2.1. Membuat Aplikasi CRUD menggunakan Spring Boot, Spring Data dan Thymeleaf]()

### [3. Membuat REST API pada Spring Boot]()
##### [3.1. Membuat REST API Sederhana]()
##### [3.2. Membuat REST API dengan Spring Boot dan Spring Data JPA]()
##### [3.3. Membuat REST API  dengan Spring Boot dan Spring Data MongoDB]()


### [4. Mengamankan Aplikasi Spring Boot]() 
##### [4.1. Basic Auth In Memory]()
##### [4.2. Basic Auth Database]()
##### [4.3. OAuth2]()
##### [4.4. JWT]()

### [5. [Reactive] Membuat REST API pada Spring Boot]()
##### [5.1. Membuat REST API Sederhana]()
##### [5.2. Membuat REST API dengan Spring Boot dan Spring Data JPA]()
##### [5.3. Membuat REST API  dengan Spring Boot dan Spring Data MongoDB]()


### [6. [Reactive] Mengamankan Aplikasi Spring Boot]()
##### [6.1. Basic Auth In Memory]()
##### [6.2. Basic Auth Database]()

### [7. Membuat Mail Server]()

### [8. Membuat Report menggunakan Jasper Report]()

### [9. Database Migration menggunakan FlywayDB]()

### [9. API documentation menggunakan Swagger2]()

### [7. Membuat Microservice dengan Spring Cloud]()


<!-- ## Create Read Update Delete
- [Setup Project Untuk CRUD dengan Spring Data JPA dan MySQL](https://ciazhar.github.io/2017/04/23/pemrograman/spring/jpa/1-setup-project-crud-jpa-mysql/)
- [CRUD dengan Spring Data JPA + Thymeleaf (Server Side Rendering)](https://ciazhar.github.io/2017/04/23/pemrograman/spring/jpa/2.1-crud-jpa-thymeleaf/)
- [CRUD dengan Spring Data JPA + AngularJS (Client Side Rendering / RESTfull API)](https://ciazhar.github.io/2017/04/23/pemrograman/spring/jpa/2.3-generate-content-dari-client-side-dengan-AngularJS/) -->
<!-- - [Spring Boot REST API Design Pattern](https://ciazhar.github.io/2017/05/27/pemrograman/spring/jpa/2.2-crud-jpa-thymeleaf(extended)/) -->
<!-- - [Kardinalitas pada Spring Data JPA](https://ciazhar.github.io/2017/04/23/pemrograman/spring/jpa/3-kardinalitas/)  -->
<!-- - [Debug Spring Data JPA](https://ciazhar.github.io/2017/05/28/pemrograman/spring/jpa/4-Debug-Spring-Data-JPA/)  

## Security
- [Otoriasai login dengan Spring Security](https://ciazhar.github.io/2017/04/23/pemrograman/spring/security/1-otorisasi-login-dengan-spring-security/)
- [Otorisasi controller dengan Spring Security](https://ciazhar.github.io/2017/05/27/pemrograman/spring/security/2-otorisasi-method-dengan-spring-security/) 
- [Debug Spring Security](https://ciazhar.github.io/2017/05/27/pemrograman/spring/security/3-debug-spring-security/) 
- [Melihat Data User Login dengan Spring Security](https://ciazhar.github.io/2017/05/27/pemrograman/spring/security/4-melihat-data-user-login-dengan-spring-security-md/)   
- [Securing Spring Boot App with Spring OAuth2 + JSON Web Token (JWT)](https://ciazhar.github.io/2017/05/27/pemrograman/spring/security/5-oauth2-spring/)
- [Single Signed On dengan Spring Security](https://ciazhar.github.io/2017/05/27/pemrograman/spring/security/6-SSO-dengan-Spring-Security/)

## Report
- [Membuat Report dengan Jasper Report](https://ciazhar.github.io/2017/04/23/pemrograman/spring/report/jasper-report/)

## Mail
- [Membuat Register dengan Verifikasi Email](https://ciazhar.github.io/2017/08/17/pemrograman/spring/mail/sending-mail/)

## Database Migration
- [Migrasi Database dengan FlywayDB](https://ciazhar.github.io/2017/05/28/pemrograman/spring/database-migration/Database-Mirgation-dengan-FlywayDB/)

## Microservice
- [Microservice dengan Spring Cloud](https://ciazhar.github.io/2017/05/28/pemrograman/spring/microservice/Microservice-dengan-Spring-Cloud/)
- [Spring Cloud Discovery Service (Eureka)](https://ciazhar.github.io/2017/08/15/pemrograman/spring/microservice/discovery-service-eureka/netflix-eureka-as-discovery-service/)
- [Spring Cloud Circuit Breaker (Hystrix)](https://ciazhar.github.io/2017/08/18/pemrograman/spring/microservice/circuit-breaker-hystrix/circuit-breaker-with-hystrix/)
- [Spring Cloud API Gateway (Zuul)](https://ciazhar.github.io/2017/08/18/pemrograman/spring/microservice/api-gateway-zuul/zuul-as-api-gateway/)
- [Spring Cloud Config Service : Intro](https://ciazhar.github.io/2017/07/22/pemrograman/spring/microservice/config-service/1.GS-Config-Service/)
- [Spring Cloud Config Service : File System](https://ciazhar.github.io/2017/07/28/pemrograman/spring/microservice/config-service/2.Config-Service-File-System/)
- [Spring Cloud Config Service : Vault Server](https://ciazhar.github.io/2017/07/28/pemrograman/spring/microservice/config-service/3.Config-Service-Vault-Server/)
- [Spring Cloud Config Service : Git Repositoty](https://ciazhar.github.io/2017/08/05/pemrograman/spring/microservice/config-service/4.Config-Service-Git-Repository/)
- [Spring Cloud Config Service : Config Client](https://ciazhar.github.io/2017/08/14/pemrograman/spring/microservice/config-service/5-Config-Service-Cient/) 
- [Spring Cloud Config Service : Encryption & Decryption](https://ciazhar.github.io/2017/08/14/pemrograman/spring/microservice/config-service/5-Config-Service-Encryption-Decryption/) 
- [Spring Cloud Config Service : Refresh Scope & Health](https://ciazhar.github.io/2017/08/14/pemrograman/spring/microservice/config-service/7-Config-Service-Refresh-Scope-and-Health-Check/) 
- [Spring Cloud Config Service : Security](https://ciazhar.github.io/2017/08/15/pemrograman/spring/microservice/config-service/8-Spring-Config-Service-Security/)  -->
