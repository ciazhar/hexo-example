---
title: Service
date: 2017-05-09 20:24:21
categories:
  - Pemrograman
  - Angular
---
![](/images/angular.png)
Service ini pada dasarnya digunakan untuk membuat suatu layanan.
- Untuk membuat service dapat menggunakan perintah sebagai berikut :
```
ng g service NAMA_SERVICE;
```
Sebagai contoh kita akan membuat service di dalam transaksi.
- Struktur foldernya akan seperti berikut
```
transaksi
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
├── transaksi.module.ts
├── transaksi.service.spec.ts
└── transaksi.service.ts
```
- Pada file service.ts terdapat anotasi `@Injectable`. Anotasi ini berfungsi untuk menandai koding javascript agar langsung injek ketika proses compilasi berlangsung.

- Buat methode sederhana untuk service(transaksi.service.ts)
```
getDaftarTransaksi(){
  let dataTransaksi = [
    {tanggal : "tanggal", keterangan : "Saldo awal",nilai : 0, saldo : 0},
    {tanggal : "tanggal", keterangan : "Tambah",nilai : 10, saldo : 10},
    {tanggal : "tanggal", keterangan : "Kurang",nilai : 5, saldo : 5},
    {tanggal : "tanggal", keterangan : "Tambah",nilai : 20, saldo : 25}
  ];
}
```

- Buat promise untuk menjembatani apabila service mengalami kegagalan dalam http request.(transaksi.service.ts)
```ts
getDaftarTransaksi(){
  let dataTransaksi = [
    {tanggal : "tanggal", keterangan : "Saldo awal",nilai : 0, saldo : 0},
    {tanggal : "tanggal", keterangan : "Tambah",nilai : 10, saldo : 10},
    {tanggal : "tanggal", keterangan : "Kurang",nilai : 5, saldo : 5},
    {tanggal : "tanggal", keterangan : "Tambah",nilai : 20, saldo : 25}
  ];
  return Promise.resolve(dataTransaksi);
}
```

- Import service (transaksi.module.ts)
```
import { TransaksiService } from './transaksi.service'
```
- Definisikan pada ngModule sebagai provider (transaksi.module.ts)
```
@NgModule({
  provider:[
    TransaksiService
  ]  
})
```
- Service telah siap digunakan. Kemudian kita akan menggunakanya di component rekap(rekap.component.ts)
```
export class RekapComponent implements OnIt {

  dataTransaksi = [];

  constructor(private transaksiService : TransaksiService){}

  ngOnIt(){
    this.transaksiService.getDaftarTransaksi().then(hasil => this.dataTransaksi = hasil)
  }
}
```
- Tampilkan hasilnya di UI(rekap.component.html)
```
<table class="table table-hover table-condensed table-striped">
  <thead>
    <tr>
      <th>Tanggal</th>
      <th>Keterangan</th>
      <th>Beli</th>
      <th>Jual</th>
      <th>Saldo</th>
    </tr>
  </thead>
  <tbody>
    <tr *ngFor="let transaksi of dataTransaksi">
      <th>{{transaksi.tanggal}}</th>
      <th>{{transaksi.keterangan}}</th>
      <th>{{transaksi.nilai}}</th>
      <th>{{transaksi.nilai}}</th>
      <th>{{transaksi.saldo}}</th>
    </tr>
  </tbody>
</table>
```
