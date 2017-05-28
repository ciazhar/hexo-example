---
title: Otorisasi methode dengan Spring Security
date: 2017-05-27 16:56:05
tags:
---

Require :
- otorisasi login dengan spring security
- crud

```java
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class KonfigurasiSecurity extends WebSecurityConfigurerAdapter{

}
```

```java
@RestController
@RequestMapping("/api/harga")
public class HargaRestController {

    @Autowired private HargaDao hargaDao;

    @PreAuthorize("hasAuthority('HARGA_EDIT')")
    @GetMapping("/")
    public Page<Harga> daftarHarga(Pageable page){
        return hargaDao.findAll(page);
    }
}
```
