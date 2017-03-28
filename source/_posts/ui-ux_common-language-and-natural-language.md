---
title: Bahasa Perintah dan Bahasa Alami
date: 2017-03-27 06:06:11
tags:  
  - ui
  - ux
categories: Kuliah
type: imk
---
## Pendahuluan
- Tujuan dasar Bahasa
  - presisi
  - kekompakan
  - kemudahan dalam penulisan dan pembacaan
  - mudah dipelajari
  - sederhana dan mengurangi kesalahan
  - mudah diingat

- Tujuan tingkat lebih tinggi
  - Hubungan yang dekat antara realitas dan notasi.
  - Kemudahan dalam melaksanakan manipulasi yang relevan dengan tugas.
  - Kompatibilitas dengan notasi yang telah ada.
  - Fleksibilitas untuk mengakomodasi pemakai pemula dan ahli.
  - Ekspresif, mendukung kreativitas.
  - Daya tarik visual.

- Kendala-kendala penggunaan Bahasa
  - kapasitas manusia mengingat notasi
  - kecocokan antara ingatan dan media penampil
  - kemudahan berbicara(mengucapkan)

- Bahasa komputer yang efektif
  Bahasa komputer yang efektif harus tidak hanya merepresentasikan tugas pemakai dan memenuhi kebutuhan manusia untuk berkomunikasi, tetapi juga harus selaras dengan mekanisme perekaman, manipulasi, dan penampilannya di komputer.
  Beberapa contoh bahasa yang efektif
  - Bahasa pemrograman:
    - Pemakaian noninteraktif: Fortran, COBOL, ALGOL, PL/I, Pascal.
    - Inkremental: BASIC, LISP, APL, PROLOG.
    - Kompilasi dan eksekusi cepat: C.
    - Pemrograman tim, sharing, reusability: ADA, C++.
    - Jaringan, cross-platform: Java.
    - Scripting World Wide Web: PHP, JavaScript, VBScript.
  - Alamat World Wide Web.
  - Bahasa database query: SQL.
  - Bahasa perintah command line: perintah Unix, MS-DOS.

## Strategi Organisasi perintah
  - Simple command set
    Setiap perintah dipilih untuk melaksanakan tugas (task) tunggal, jumlah perintah sama dengan jumlah tugas.
    Contoh: vi editor (Unix):
    0		: go to start of line
    $		: go to end of line
    (space)	: go right one space
    H		: go left one space
    W		: forward one word
    b		: backward one word
    )		: forward one sentence
    (		: backward one sentence
  - Command plus arguments
    Perintah diikuti argumen yang menunjukkan objek yang dimanipulasi.
    Contoh:
    COPY FILEA FILEB
    DEL FILEA
    Label keyword dapat membantu untuk meningkatkan keterbacaan dan meniadakan urutan.
    ```html
    <img src="gbr.gif" width="40" height="5" alt="Gambar">
    ```
  - Command plus options and arguments
    Perintah dapat berisi options untuk menunjukkan kondisi khusus.
    Jumlah argumen dan option yang banyak dapat meningkatkan tingkat kesalahan.
    Contoh:
    ```bash
    DIR C:\WINDOWS\*.EXE /S/W/P/O-N
    ls -alF /home/agus
    ```
  - Hierarchical command structure

## Manfaat Struktur
## Penamaan perintah
## Penyingkatan Perintah
## Menu perintah
## Bahasa Alami di dalam komputer
## Pedoman bahasa perintah
