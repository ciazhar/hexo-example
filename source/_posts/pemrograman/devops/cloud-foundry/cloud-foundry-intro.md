---
title: Cloud Foundry
date: 2017-08-21 17:22:41
tags:
---

![](https://upload.wikimedia.org/wikipedia/en/thumb/b/bb/CloudFoundryCorp_vertical.svg/1280px-CloudFoundryCorp_vertical.svg.png)

# Definisi Cloud Foundry

Cloud Foundry adalah suatu Paas(Platform as a Service) berbasis open source yang disediakan dikembangkan Pivotal. Platform as a service sendiri adalah service yang digunakan untuk mendeploy aplikasi kita ke cloud. 

Perbedaan Traditional IT, Infrastructure as a Service (IaaS), Platform as a Service (PaaS) dan Software as a Service (SaaS).

# Deploy aplikasi ke Pivotal Cloud Foundry
##1. Install Cloud Foundry CLI
Kunjungi [tautan berikut](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html) untuk totorial bagaimana menginstall Cloud Foundry CLI.

##2. Login ke pivotal API
- Gunakan command `cf login -a api.run.pivotal.io` pada command line untuk login.
- Kemudian anda akan diminta memasukkan email dan password
- Kemudian pilih space mana yang akan anda gunakan

##3. Buat file konfgurasi
Buat file bernama manifest.yml dan simpan di bagian terluar project anda. Berikut isi dari file tersebut :
```yml
---
applications:
- name: spring-boot-cloud-foundry
  path: target/spring-boot.jar
  domain: cfapps.io
  memory: 512m
  instance: 1
```
Keterangan :
- name : nama aplikasi
- path : letak file hasil kompilasi berada
- domain : domain aplikasi
- memory : memory aplikasi
- instance : jumlah instance/replikasi aplikasi

##4. Push ke Cloud Foundry
Gunakan perintah `cf push` pada terminal untuk melakukan push aplikasi ke cloud foundry.

Kemudian akan terlihat log. Tunggu beberapa saat sampai aplikasi anda terdeploy.

##5. Mengubah Konfigurasi Service
Gunakn perintah `cf update-service nama-service -c 'konfigurasinya'`
Contoh : 
`cf update-service config-server -c '{"git": { "uri": "http://example.com/config" } }'`


## Login ke servic mysql
mysql -u b42da3b446621e -pd66fa990 -h us-cdbr-iron-east-05.cleardb.net ad_a2227b61d61fce9
