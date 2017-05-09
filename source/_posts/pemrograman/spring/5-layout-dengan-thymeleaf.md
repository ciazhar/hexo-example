---
title: Thymeleaf
date: 2017-04-23 14:17:38
categories:
  - Pemrograman
  - Spring
---
![](/images/springboot.png)
# Layout dengan Thymeleaf
  Thymeleaf adalah template engine untuk JVM. Dia support HTMl, XML, TEXT, CSS, JS, dan RAW. Thymeleaf emmpunya kemampuan yang dikenal dengan Natural Template yaitu dimana kita dapat membuat 2 buah value yang sama. Hal ini mempermudah antara designer dan programer agar dapat bekerja bersama. Ketika value dari backed belum ada designer dapat menggunakan value html.
    ```html
      <input type="text" name="userName" value="James Carrot" th:value="${user.name}" />
    ```

# Menggunakan Thymeleaf
  Tambahkan xmlns dibawah ini pada tag html
  ```html
    <html xmlns:th="http://www.thymeleaf.org">
  ```
# Expression di Thymeleaf
  - Menampilkan pesan menggunakan `#{}`
    Contoh Menampilkan nama user yang sedang online
    ```html
      <p th:utext="#{home.welcome(${session.user.name})}">
    ```
  - Menampilkan variabel menggunakan `${}`
    contoh menggunakan th:each:
    ```html
      <tr th:each="pesertas : ${peserta}">
          <td th:text="${pesertas.nama}"></td>
          <td th:text="${pesertas.email}"></td>
          <td th:text="${pesertas.noHp}"></td>
          <td>
              <a th:href="${'/peserta/edit/'+pesertas.id}"><span class="glyphicon glyphicon-edit"></span></a>
              <a th:href="${'/peserta/hapus/'+pesertas.id}"><span class="glyphicon glyphicon-remove"></span></a>
          </td>
      </tr>
    ```
  - Menampilkan link url menggunakan `@{}`.
    Contoh url dapat berasal dari mapping controller :
    ```html
      <a th:href="@{/peserta}">Daftar Peserta</a>
    ```
    Contoh url dapat berasal dari default folder :
    ```html
      <link th:href="@{/css/bootstrap.min.css}" rel="stylesheet" />
    ```

## Template Inheritance ##
  Template Inheritance dapat menggunakan
  ```html
    <div layout:fragment="content">
  ```
