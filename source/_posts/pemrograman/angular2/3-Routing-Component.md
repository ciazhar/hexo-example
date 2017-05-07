---
title: Routing Component
date: 2017-04-28 10:01:38
categories:
  - Pemrograman
  - Angular
---
![](/images/angular2.png)
## Routing Top Level Component
1. Sebelum melakukan routing kita akan buat terlebih dahulu top level componentnya yaitu about dan welcome. Struktur foldernya akan menjadi seperti ini
```
src/app/
├── about
│   ├── about.component.css
│   ├── about.component.html
│   ├── about.component.spec.ts
│   └── about.component.ts
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
├── transaksi
│   ├── beli
│   │   ├── beli.component.css
│   │   ├── beli.component.html
│   │   ├── beli.component.spec.ts
│   │   └── beli.component.ts
│   ├── jual
│   │   ├── jual.component.css
│   │   ├── jual.component.html
│   │   ├── jual.component.spec.ts
│   │   └── jual.component.ts
│   ├── rekap
│   │   ├── rekap.component.css
│   │   ├── rekap.component.html
│   │   ├── rekap.component.spec.ts
│   │   └── rekap.component.ts
│   └── transaksi.module.ts
└── welcome
    ├── welcome.component.css
    ├── welcome.component.html
    ├── welcome.component.spec.ts
    └── welcome.component.ts
```

2. Selanjunya import router module (app.module.ts)
```ts
import { RouterModule, Routes } from '@angular/router';
```

3. Selanjutnya routing tiap module (app.module.ts)
```
const routingAplikasi: Routes = [
  { path: "about", component: AboutComponent },
  { path: "**", component: WelcomeComponent }
]
```
4. Inisialisasi router (app.module.ts)
```
@NgModule({
  ....
  imports: [
    ....
    RouterModule.forRoot(routingAplikasi)
  ],
  ...
})
```
5. mapping router ke html
(navbar.component.html)
```html
<li><a routerLink="about">Informasi</a></li>
```
(sidebar.component.html)
```html
<li class="active"><a routerLink="welcome">Dashboard <span class="sr-only">(current)</span></a></li>
```
6. Menambahkan router outlet yaitu tempat keluarnya konten sehabis di routing.
(app.component.html)
```html
<app-navbar></app-navbar>
<div class="container-fluid">
  <div class="row">
    <app-sidebar></app-sidebar>
    <div class="col-sm-9 col-sm-offset-3 col-md-10 col-md-offset-2 main">
      <router-outlet></router-outlet>
    </div>
  </div>
</div>
```


## Routing module

- import routing (transaksi.module.ts)
```ts
import { RouterModule, Routes } from '@angular/router';
```
- buat Routes beserta path
```ts
const routingTransaksi : Routes[
  { path: "/transaksi/beli", componen:  }
]
```
- import Routes

app module ts
- tambah path untuk routing module
