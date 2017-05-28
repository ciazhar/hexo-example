---
title: Setup Project Untuk CRUD dengan Spring Data JPA dan MySQL
date: 2017-04-23 14:17:31
categories:
  - Pemrograman
  - Spring
---
![](/images/springboot.png)

# Setup Project untuk CRUD
Pada tutorial kali ini kita akan melakukan Create Read Update Delete (CRUD) menggunakan Spring Data JPA. Kita akan menggunakan mysql untuk databasenya, jadi anda harus menginstallnya terlebih dahulu.
Berikut ini merupakan langkah-langkahnya :

## Pertama-tama kita akan tambahkan dependendcy spring data jpa (pom.xml)

```xml
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
  </dependency>
  <dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>6.0.6</version>
  </dependency>
```
Untuk mencari dependency dapat dilihat di [Maven Repostory](https://mvnrepository.com)

## Setting Database (main/resources/application.properties)

```yml
  spring.datasource.url=jdbc:mysql://localhost:3306/pelatihan
  spring.datasource.username=pelatihanuser
  spring.datasource.password=pelatihanpasswd
```
Keterangan :
1. `spring.datasource.url` merupakan url untuk database. Dalam pengisianya harap disesuaikan dengan jenis database, port pada perangkat, dan nama database yang telah dibuat. Pada contoh tersebut menggunakan jenis database (mysql), port pada perangkat (3306), dan nama database(pelatihan)
2. `spring.datasource.username` merupakan username database.
3. `spring.datasource.password` merupakan password database.


## Membuat Schema (CLI).
Untuk schema tetap harus dibuat manual. Berikut langkah-langkahnya untuk mysql.
- Login ke mysql. Jika sudah login dapat diabaikan langkah ini.

```
  mysql -u root -p
```
- Memasang otentifikasi database

```
grant all on pelatihan.* to pelatihanuser@localhost identified by 'pelatihanpasswd'
```
- Membuat database

```
create database pelatihan;
```

## Meggunakan MySQL (CLI)
Berikut adalah sintaks yang akan sering digunakan dalam mysql.
- Menggunakan database

```
  use pelatihan;
```
- Melihat list tabel dalam database

```
  show tables;
```
- Melihat atribut pada tabel secara detail

```		
  show create table nama_tabel \G
```
- Melihat data pada tabel

```
  select * from nama_tabel
```
- Menghapus data pada tabel

```
  drop table peserta;
```
