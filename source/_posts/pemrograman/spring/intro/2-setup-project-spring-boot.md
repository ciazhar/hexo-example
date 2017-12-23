---
title: Setup Project Spring Boot
date: 2017-04-23 14:17:29
categories:
  - Pemrograman
  - Spring
---
![](/images/springboot.png)

# 1. Install Development Environment

Untuk menggunakan Spring Boot anda perlu menginstall beberapa Development Environment. Diantaranya adalah :

- Java Development Kit (JDK atau openJDK).
- Build Tools (Apache Maven atau Gradle).
- IDE atau Text Editor (IntellijIDEA / VSCode).

# Setup Project Mengunakan Spring Initializer

- Buka browser lalu masukkan url `http://start.spring.io/`
- Maka akan tampil antarmuka seperti ini.

![](http://img.blog.csdn.net/20161203083002608)

- Selanjutnya anda akan diminta untuk mengisi beberapa data yaitu :
  - Tipe Project. Project dapat berupa `maven` atau `gradle`. Isi dengan Build tools yang sudah anda install di komputer anda.
  - Versi Spring. Pilih versi terbaru yang bukan SNAPSHOOT.
  - Project Metadata. Format pengisianya adalah sebagai berikut :
    Group : com.nama.domain.anda (dipisah dengan titik)
    Artifact : nama-aplikasi-anda (tidak boleh diberi spasi)
  - Dependencies. Isi dengan library yang anda butuhkan.
- Generate Project.
- Add project ke text editor/IDE.

# Struktur Folder Aplikasi Spring Boot

Struktur foldernya akan seperti berikut :

```struct
demo
├── mvnw
├── mvnw.cmd
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   │   └── com
    │   │       └── example
    │   │           └── DemoApplication.java
    │   └── resources
    │       ├── application.properties
    │       ├── static
    │       └── templates
    └── test
        └── java
            └── com
                └── example
                    └── DemoApplicationTests.java
```

Sebagai catatan struktur folder tersebut dapat berubah sesuai data yang anda masukkan saat membuat project.
Pada Project tersebut terdapat beberapa file yaitu :

- `pom.xml`. File ini merupakan konfigurasi dari Maven. Jika anda menggunakan Gradle maka yang dibuat adalah file `.gradle`.
- Di dalam folder `src/main/java/com/example` terdapat file DemoApplication.java. File ini merupakan main file dari aplikasi spring boot anda.
- Folder `src/main/java/` sendiri digunakan untuk menampung file-file java.
- Di dalam folder `src/main/resources` terdapat file application.properties. File ini digunakan untuk mengkonfigurasi aplikasi spring.
- Folder `src/main/resources/static` digunakan untuk menampung file static (hmtl, css dan js)
- Folder `src/main/resources/templates` digunakan untuk menampung file html yang menggunakan template engine.
- Folder `src/test/java/com/example` digunakan untuk menampung file-file testing.

# Menjalankan aplikasi

Untuk menjalankan project dapat menggunakan perintah berikut pada CLI

```bash
mvn clean spring-boot:run
```

Maka secara default aplikasi anda akan berjalan di port 8080.