---
title: Debugging Spring Security
date: 2017-05-27 17:03:50
categories:
  - Pemrograman
  - Spring
---
![](https://ordina-jworks.github.io/img/spring-security-logo.png)

Spring security memberikan fasilitas untuk mendebug. Untuk menggunakannya cukup dengan menambahkan anotasi `@EnableWebSecurity(debug = true)` pada file KonfigurasiSecurity.

```java
@EnableWebSecurity(debug = true)
public class KonfigurasiSecurity extends WebSecurityConfigurerAdapter{
}
```

Debug ini hanya disarankan pada tahap development saja.
