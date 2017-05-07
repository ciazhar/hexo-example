---
title: Component dan Module
date: 2017-04-28 10:01:37
categories:
  - Pemrograman
  - Angular
---
![](/images/angular.png)
## Membuat Komponen
Untuk membuat componen dapat menggunakan perintah sebagai berikut
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
│   ├── navbar.component.css
│   ├── navbar.component.html
│   ├── navbar.component.spec.ts
│   └── navbar.component.ts
└── sidebar
    ├── sidebar.component.css
    ├── sidebar.component.html
    ├── sidebar.component.spec.ts
    └── sidebar.component.ts
```
Navbar dan Sidebar merupakan contoh dari Top Level Component

## Membuat Module
Untuk membuat module dapat menggunakan
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
│   ├── navbar.component.css
│   ├── navbar.component.html
│   ├── navbar.component.spec.ts
│   └── navbar.component.ts
├── sidebar
│   ├── sidebar.component.css
│   ├── sidebar.component.html
│   ├── sidebar.component.spec.ts
│   └── sidebar.component.ts
└── transaksi
    └── transaksi.module.ts
```
Transaksi merupakan contoh module. Kemudian kita buat beberapa component di dalamnya sehingga sebagai berikut
```
app/
├── app.component.css
├── app.component.html
├── app.component.spec.ts
├── app.component.ts
├── app.module.ts
├── navbar
│   ├── navbar.component.css
│   ├── navbar.component.html
│   ├── navbar.component.spec.ts
│   └── navbar.component.ts
├── sidebar
│   ├── sidebar.component.css
│   ├── sidebar.component.html
│   ├── sidebar.component.spec.ts
│   └── sidebar.component.ts
└── transaksi
    ├── beli
    │   ├── beli.component.css
    │   ├── beli.component.html
    │   ├── beli.component.spec.ts
    │   └── beli.component.ts
    ├── jual
    │   ├── jual.component.css
    │   ├── jual.component.html
    │   ├── jual.component.spec.ts
    │   └── jual.component.ts
    ├── rekap
    │   ├── rekap.component.css
    │   ├── rekap.component.html
    │   ├── rekap.component.spec.ts
    │   └── rekap.component.ts
    └── transaksi.module.ts
```
Beli, jual dan rekap merupakan contoh component dari module transaksi
