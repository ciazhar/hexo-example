---
title: Setup Project Angular2
date: 2017-04-28 10:01:36
categories:
  - Pemrograman
  - Angular2
---
![](/images/angular2.png)
## Menginstall Node dan NPM
Untuk menginstall node saya menyarankan menggunakan tutorial dari [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04) dengan menggunakan nvm.


## Menginstall Angular CLI
Angular ini adalah salah satu tools untuk membuat aplikasi angular2. Untuk menggunakanya cukup ketikkan kode berikut apda terminal.
```
  npm install -g @angular/cli
```

## Membuat Project Angular2
```
  ng new NAMA_PROJECT
```
Setelah itu akan dibuat struktur folder sebagai berikut :
```
angular2-spring-boot-pegadaian/
├── .git
│   ├── branches
│   ├── COMMIT_EDITMSG
│   ├── config
│   ├── description
│   ├── HEAD
│   ├── hooks
│   │   ├── applypatch-msg.sample
│   │   ├── commit-msg.sample
│   │   ├── post-update.sample
│   │   ├── pre-applypatch.sample
│   │   ├── pre-commit.sample
│   │   ├── prepare-commit-msg.sample
│   │   ├── pre-push.sample
│   │   ├── pre-rebase.sample
│   │   └── update.sample
│   ├── index
│   ├── info
│   │   └── exclude
│   ├── logs
│   │   ├── HEAD
│   │   └── refs
│   │       └── heads
│   │           └── master
│   ├── objects
│   │   ├── 82
│   │   │   └── e3a754b6a0fcb238b03c0e47d05219fbf9cf89
│   │   ├── e6
│   │   │   └── 9de29bb2d1d6434b8b29ae775ad8c2e48c5391
│   │   ├── f1
│   │   │   └── 65300d6c67d5599ceb9b0ed355c2a8cbe336bf
│   │   ├── info
│   │   └── pack
│   └── refs
│       ├── heads
│       │   └── master
│       └── tags
├── .gitignore
└── NAMA_PROJECT
    ├── .angular-cli.json
    ├── e2e
    │   ├── app.e2e-spec.ts
    │   ├── app.po.ts
    │   └── tsconfig.e2e.json
    ├── .editorconfig
    ├── .gitignore
    ├── karma.conf.js
    ├── package.json
    ├── protractor.conf.js
    ├── README.md
    ├── src
    │   ├── app
    │   │   ├── app.component.css
    │   │   ├── app.component.html
    │   │   ├── app.component.spec.ts
    │   │   ├── app.component.ts
    │   │   └── app.module.ts
    │   ├── assets
    │   │   └── .gitkeep
    │   ├── environments
    │   │   ├── environment.prod.ts
    │   │   └── environment.ts
    │   ├── favicon.ico
    │   ├── index.html
    │   ├── main.ts
    │   ├── polyfills.ts
    │   ├── styles.css
    │   ├── test.ts
    │   ├── tsconfig.app.json
    │   ├── tsconfig.spec.json
    │   └── typings.d.ts
    ├── tsconfig.json
    └── tslint.json
```
Pada Project tersebut terdapat beberapa file yaitu :
- angular-cli.json. File ini berisi konfigurasi dari tools angular cli.
- package.json. File ini digenerate untuk setiap project yang menggunakan npm. Berisi konfigurasi dependency/library.
- tsconfig.json. File ini berisi konfigurasi untuk typscript compiler. Terdapat `emitDecoratorMetadata` yang digunakan memproses decorator dimana fungsinya sama dengan anotation pada spring framework. Decorator berfungsi untuk mengkonversi Typescript ke Javascript. Terdapat juga `module` yang berisi module systemnya. Terdapat juga `target` untuk outputnya nanti menjadi apa. Terdapat juga `moduleResolution` untuk system modulnya. Terdapat juga `outDir` untuk compilenya kemana. Terdapat juga `sourceMap` untuk mapping hasil compile ke sourcecode aslinya.
- node_module. Folder ini merupakan repository local yang berisi dependency yang telah didownload.
- index.html. File ini merupaka html indexnya. Angular2 ini menggenerate Single Page Aplication. Jadi file html cuma 1 dan yang lainya JS.
- main.ts. File ini merupaka main class nya.
- style.css. File css untuk global.
- app. Folder yang berisi sourcecode. Di folder ini terdapat beberapa file yaitu `.css` untuk cssnya, `.html` untuk templatenya, `.spec.ts` untuk testing, `.ts` untuk konfigurasi template dan ts, `module.ts` untuk modulenya (kalo di java seperti package).

## Running Project
Untuk running project dapat gunakan code berikut pada terminal
```
cd NAMA_PROJECT
ng serve
```
Hasilnya dapat anda lihat di browser pada `localhost:4200`.


## Build Project
Untuk running project dapat gunakan code berikut pada terminal
```
cd NAMA_PROJECT
ng serve
```
Hasilnya dapat anda lihat pada folder dist


## Flow Angular2
1. main.ts akan dijalankan pertama kali. Di main.ts sendiri dia mengimport app.module.ts melalui koding `import { AppModule } from './app/app.module';`. Selain itu main.ts juga membootrap app.module.ts melalui koding `platformBrowserDynamic().bootstrapModule(AppModule);`
2. Selanjutnya app.module.ts. Di app.module.ts dia terdapat `declaration` yang berisi kelas-kelas apa saja yang ada di modul ini. Selanjutnya ada `import` yang berisi kelas-kelas apa saja yang diimport. Selanjutnya ada `bootstrap` yang digunakan untuk menjalankan file (yaitu AppComponent).
3. Selanjutnya app.component.ts. Di app.component.ts terdapat `selector` yang digunakan untuk tag pada html. Jadi dia akan mencari tag di html (yaitu app-root), apabila ada maka dia akan menginjectkan templatenya ke dalam tag tersebut. Templatenya sendiri berasa dari `templateUrl`.
4. Selanjutnya app.component.html. Di app.component.html apabila ada variabel maka dia akan mengambilnya dari app.component.ts bagian export.


## Install Bootstrap
Step ini optional karena untuk css bisa pake framework yang lain atau menginputkan sendiri cssnya. Step ini hanya untuk mempermudah saja.
Untuk menginstallnya dapat menggunakan kode
```
npm install ng2-bootstrap bootstrap --save
```
Setelah itu includekan bootstrapnya ke file angular-cli.json.
```json
"styles": [
  "styles.css",
  "../node_modules/bootstrap/dist/css/bootstrap.min.css"
],
```

## Arsitektur Aplikasi Angular2
Arsitekturnya kurang lebih seperti berikut
```
  Aplikasi
  ├── Top Level Component
  │   ├── Module
  │   │   ├── Component
  |   |   |   |── Typescript
  |   |   |   |── HTML
```
Penjelasanya adalah setiap aplikasi terdiri dari satu atau lebih Component. Components ini menyusun Kelompok dari Module tertentu. Begitu juga dengan Module yang tersusun dari satu atau lebih Component. Component sendiri dibuat berdasarkan file Typescript dan HTML. Berikut contoh sederhananya:
```
  Aplikasi Tabungan Emas
  ├── Sidebar Component
  │   ├── Informasi Rekening
  │   ├── Transaksi Emas
  │   │   ├── Form
  │   │   ├── Rekap
  ├── Navbar Component
  │   ├── Settings
  │   ├── Profile
  │   ├── Help
```
