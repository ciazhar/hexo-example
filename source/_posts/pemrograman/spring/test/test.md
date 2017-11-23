---
title: Testing in Spring Framework
date: 2017-09-17 09:12:19
tags:
---

![](/images/spring-boot-banner.png)

- buat class test pada rest dari class controller
- tambahkan anotasi `@RunWith(SpringJUnit4ClassRunner::class)`
- `private val productController : ProductController ?= null`
- `private val mockMvc : MockMvc ?=null`. mock ini akan digunakan untuk menjalankan testing