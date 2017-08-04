---
title: Routing
date: 2017-04-28 10:01:38
categories:
  - Pemrograman
  - Angular
---
![](/images/angular.png)
Laman Web pada umumnya untuk berkomunikasi dengan menggunakan hyperlink. Sementara itu untuk berkomunikasi antar komponen, Angular menggunakan routing. Routing hampir seperti mapping di java. Untuk pergi ke komponen lain, jalurnya harus didefinisikan terlebih dahulu.
Routing sendiri berdasarkan letaknya dibedakan menjadi 2 yaitu routing Top Level Component dan routing Component pada Module.

## Routing Top Level Component
1. Sebelum melakukan routing kita akan buat terlebih dahulu membuat top level componentnya, sebagai contoh kita akan membuat 2 buah component yaitu home dan help. Struktur foldernya akan menjadi seperti ini
```
app/
├── app.component.css
├── app.component.html
├── app.component.spec.ts
├── app.component.ts
├── app.module.ts
├── home
│   ├── home.component.css
│   ├── home.component.html
│   ├── home.component.spec.ts
│   └── home.component.ts
├── help
    ├── help.component.css
    ├── help.component.html
    ├── help.component.spec.ts
    └── help.component.ts
```

2. Selanjunya import `RouterModule` dan `Routes`  (app.module.ts)
```ts
import { RouterModule, Routes } from '@angular/router';
```

3. Selanjutnya routing tiap module (app.module.ts)
```
const routingAplikasi : Routes = [
  { path: "help", component: HelpComponent },
  { path: "**", component: HomeComponent }
]
```
Keteranga :
Routes diatas melakukan routing untuk HelpComponent ke url `help` dan WelcomeComponent ke url lainya.

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
5. Mapping router ke html menggunakan `routerLink`
```html
<li><a routerLink="help">Help</a></li>

```
6. Menambahkan router outlet sebagai tempat keluarnya konten sehabis di routing.
(app.component.html)
```html
<router-outlet></router-outlet>
```


## Routing Component pada Module

- import RouterModule dan Routes (transaksi.module.ts)
```ts
import { RouterModule, Routes } from '@angular/router';
```

- buat Routes beserta path (transaksi.module.ts)
```ts
const routingTransaksi : Routes = [
  { path: "transaksi/beli", component: BeliComponent },
  { path: "transaksi/jual", component: JualComponent },
  { path: "transaksi/rekap", component: RekapComponent }
]
```

- Inisialisasi Routes (transaksi.module.ts)
```ts
@NgModule({
  ....
  imports: [
    RouterModule.forChild(routingTransaksi)
  ]
```

- import TransaksiComponent(app.module.ts)
```
import { TransaksiModule } from './transaksi/transaksi.module';
```

- tambah path untuk routing module(app.module.ts)
```ts
{ path: "transaksi", redirectTo: "/transaksi", pathMatch: "full"}
```

- Inisialisasi Routes (app.module.ts)
```ts
@NgModule({
  ....
  imports: [
    TransaksiModule,
  ]
```
