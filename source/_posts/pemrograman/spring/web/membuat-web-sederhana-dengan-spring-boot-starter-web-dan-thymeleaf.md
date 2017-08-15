---
title: Membuat Web Menggunakan Spring Boot dan Thymeleaf
date: 2017-04-23 14:17:30
categories:
  - Pemrograman
  - Spring
---
![](/images/springboot.png)
[Pada tutorial sebelumnya](https://ciazhar.github.io/2017/04/23/pemrograman/spring/1-setup-project/) kita sudah melakukan setup project spring pada perangkat anda. Sekarang kita akan coba melihat bagaimana aplikasi spring dibuat.
Untuk pertama kali kita akan coba membuat laman web sederhana. Langkah-langkahnya adalah sebagai berikut :

- Membuat controller sederhana (main/java/domain/Controllers/HaloController.java)
```java
  @Controller
  public class HaloController{
    @RequestMapping("/")
    public String halo(){
      return "index";
    }
  }
```
Keterangan :
1. `@Controller` digunakan untuk menandai bahwa class `HaloController` adalah class controller
2. `@RequestMapping` digunakan untuk melakukan mapping url pada metode bernama halo ke `/`. Kemudian controller itu akan di tampilkan pada view bernama `index`.


- Membuat file HTML (main/resources/templates/index.html)
```html
  <html xmlns:th="http://www.thymeleaf.org">
    <head>
      <title>Aplikasi Spring Boot</title>
      <link rel="stylesheet" th:href="@{/css/bootstrap.min.css}"  media="screen"/>
      <link rel="stylesheet" th:href="@{/css/signin.css}" media="screen"/>
    </head>

    <body>
      <nav class="navbar navbar-inverse navbar-fixed-top">
        <div class="container">
          <div class="navbar-header">
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
              <span class="sr-only">Toggle navigation</span>
              <span class="icon-bar"></span>
              <span class="icon-bar"></span>
              <span class="icon-bar"></span>
            </button>
            <a class="navbar-brand" th:href="@{/}">ciazhar</a>
          </div>
        </div>
      </nav>

      <div class="container">
        <h1>Aplikasi Spring Boot Dengan Thymeleaf</h1>
      </div>

      <script th:src="@{/js/jquery.min.js}"></script>
      <script th:src="@{/js/bootstrap.min.js}"></script>
    </body>
  </html>
```
Keterangan :
1. `<html xmlns:th="http://www.thymeleaf.org">` menandai bahwa html itu menggunakan template engine thymeleaf
2. `th:href` (jika di html bernama `href`) digunakan untuk menginjek css. css tersebut dapat di simpan di `src/main/resources/static/css`. Tetapi karena `src/main/resources/static` merupakan classpath maka untuk menginjeknya hanya perlu dari folder css saja. contoh : `<link rel="stylesheet" th:href="@{/css/bootstrap.min.css}"  media="screen"/>`
Selain itu kita juga dapat menggunakanya untuk melakukan link sesuai mapping di controller. contoh : `<a class="navbar-brand" th:href="@{/}">ciazhar</a>`
3. `th:src`(jika di html bernama `src`) digunakan untuk menginjek js. js tersebut dapat di simpan di `src/main/resources/static/js`. contoh : `<script th:src="@{/js/jquery.min.js}"></script>`



- Memasang Library (/src/main/resources)
Jika kita lihat pada html diatas kita memerlukan beberapa library yaitu bootstrap dan jquery. Library tersebut dapat anda download di official masing-masing library tersebut. Kemudian masukkan ke /src/main/resources/css untuk file CSS dan /src/main/resources/js untuk file JS. Jika anda asset diinjek menggunakan CDN anda dapat melewati langkah berikut.
