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
├── navbar
|   ├── navbar.component.css
|   ├── navbar.component.html
|   ├── navbar.component.spec.ts
|   └── navbar.component.ts
├── sidebar
|   ├── sidebar.component.css
|   ├── sidebar.component.html
|   ├── sidebar.component.spec.ts
|   └── sidebar.component.ts
├── footer
    ├── footer.component.css
    ├── footer.component.html
    ├── footer.component.spec.ts
    └── footer.component.ts
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
├── navbar
|   ├── navbar.component.css
|   ├── navbar.component.html
|   ├── navbar.component.spec.ts
|   └── navbar.component.ts
├── sidebar
|   ├── sidebar.component.css
|   ├── sidebar.component.html
|   ├── sidebar.component.spec.ts
|   └── sidebar.component.ts
├── footer
|    ├── footer.component.css
|    ├── footer.component.html
|    ├── footer.component.spec.ts
|    └── footer.component.ts
└── transaksi
    └── transaksi.module.ts
```
Kemudian kita buat beberapa component di dalamnya sehingga sebagai berikut
```
├── navbar
|   ├── navbar.component.css
|   ├── navbar.component.html
|   ├── navbar.component.spec.ts
|   └── navbar.component.ts
├── sidebar
|   ├── sidebar.component.css
|   ├── sidebar.component.html
|   ├── sidebar.component.spec.ts
|   └── sidebar.component.ts
├── footer
|    ├── footer.component.css
|    ├── footer.component.html
|    ├── footer.component.spec.ts
|    └── footer.component.ts
└── transaksi
    ├── jual
    │   ├── jual.component.css
    │   ├── beli.component.html
    │   ├── beli.component.spec.ts
    │   └── beli.component.ts
    ├── beli
    │   ├── beli.component.css
    │   ├── beli.component.html
    │   ├── beli.component.spec.ts
    │   └── beli.component.ts
    ├── rekap
    │   ├── rekap.component.css
    │   ├── rekap.component.html
    │   ├── rekap.component.spec.ts
    │   └── rekap.component.ts
    └── transaksi.module.ts
```
jual, beli dan rekap merupakan component dari module transaksi. Sedangkan navbar, sidebar dan footer dikenal sebagai layout component.
