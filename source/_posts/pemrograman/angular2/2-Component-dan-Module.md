---
title: Component dan Module
date: 2017-04-28 10:01:37
categories:
  - Pemrograman
  - Angular
---
![](/images/angular.png)
## Komponen
Komponen ini dapat digunakan untuk membuat suatu layout atau menu. Contoh komponen yang digunakan sebagai layout yaitu seperti navbar, sidebar dan footer. Ada juga komponen yang digunakan sebagai menu seperti beranda, pengaturan, profil dan sebagainya.
Untuk membuat componen dapat menggunakan perintah sebagai berikut :
```
ng g component NAMA_COMPONENT
```
Sehingga Struktur foldernya akan menjadi seperti :
```
app/
├── app.component.css
├── app.component.html
├── app.component.spec.ts
├── app.component.ts
├── app.module.ts
├── NAMA_COMPONENT
|   ├── NAMA_COMPONENT.component.css
|   ├── NAMA_COMPONENT.component.html
|   ├── NAMA_COMPONENT.component.spec.ts
|   └── NAMA_COMPONENT.component.ts
```


## Membuat Module
Module ini seperti package atau folder. Dia berfungsi untuk menampung beberapa component yang memiliki fungsi yang sama. Analoginya seperti suatu transaksi memiliki aksi seperti jual, beli & rekap. Transaksi merupakan modulenya dan jual beli & rekap adalah componentnya.
Untuk membuat module dapat menggunakan perintah sebagai berikut :
```
ng g module NAMA_MODULE
```
Setelah itu struktur foldernya akan seperti berikut
```
app/
├── app.component.css
├── app.component.html
├── app.component.spec.ts
├── app.component.ts
├── app.module.ts
├── NAMA_COMPONENT
│   ├── NAMA_COMPONENT.component.css
│   ├── NAMA_COMPONENT.component.html
│   ├── NAMA_COMPONENT.component.spec.ts
│   └── NAMA_COMPONENT.component.ts
└── NAMA_MODULE
    └── NAMA_MODULE.module.ts
```
Kemudian kita buat beberapa component di dalamnya sehingga sebagai berikut
```
app/
├── app.component.css
├── app.component.html
├── app.component.spec.ts
├── app.component.ts
├── app.module.ts
├── NAMA_COMPONENT
│   ├── NAMA_COMPONENT.component.css
│   ├── NAMA_COMPONENT.component.html
│   ├── NAMA_COMPONENT.component.spec.ts
│   └── NAMA_COMPONENT.component.ts
└── NAMA_MODULE
    ├── NAMA_COMPONENT1
    │   ├── NAMA_COMPONENT1.component.css
    │   ├── NAMA_COMPONENT1.component.html
    │   ├── NAMA_COMPONENT1.component.spec.ts
    │   └── NAMA_COMPONENT1.component.ts
    ├── NAMA_COMPONENT2
    │   ├── NAMA_COMPONENT2.component.css
    │   ├── NAMA_COMPONENT2.component.html
    │   ├── NAMA_COMPONENT2.component.spec.ts
    │   └── NAMA_COMPONENT2.component.ts
    ├── NAMA_COMPONENT3
    │   ├── NAMA_COMPONENT3.component.css
    │   ├── NAMA_COMPONENT3.component.html
    │   ├── NAMA_COMPONENT3.component.spec.ts
    │   └── NAMA_COMPONENT3.component.ts
    └── NAMA_MODULE.module.ts
```
NAMA_COMPONENT1, NAMA_COMPONENT2 dan NAMA_COMPONENT3 merupakan component dari NAMA_MODULE. Sedangkan NAMA_COMPONENT dikenal sebagai top level component.
