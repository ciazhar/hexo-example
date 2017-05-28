---
title: Melihat data User yang sedang Login menggunakan Spring Security
date: 2017-05-27 17:06:58
tags:
---

Untuk dapat melihar user yang sedang login dapat menggunakan `Authentication` yang nilainya akan diinjek oleh spring security. Berikut contoh kodenya :
```java
@RestController
@RequestMapping("api/user")
public class UserController {

    @RequestMapping("/current")
    public Authentication currentUser(Authentication authentication){
        return authentication;
    }
}
```
