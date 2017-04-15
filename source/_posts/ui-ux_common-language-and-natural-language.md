---
title: Bahasa Perintah dan Bahasa Alami
date: 2017-03-27 06:06:11
tags:  
  - ui
  - ux
categories:
  - Teknologi
  - Interaksi Manusia dan Komputer
---
![](/images/ui-ux/Ui-Ux.jpg)
## Pendahuluan
- Tujuan dasar bahasa
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
    Contoh: vim editor (Unix):
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
    ```bash
    COPY FILEA FILEB
    DEL FILEA
    ```
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
    Perangkat penuh perintah disusun menjadi struktur tree, seperti menu tree.
    Contoh:
    ```
    Action    Object     Destination
    CREATE    File       File
    DISPLAY   Process    Local printer
    REMOVE    Directory  Screen
    COPY                 Remote  printer
    MOVE
    ```
    Contoh di atas menghasilkan struktur berarti bagi
    5 × 3 × 4 = 60 tugas.

## Manfaat Struktur
    - Manfaat struktur:
      - Membantu proses belajar manusia, pemecahan masalah, dan ingatan.
      - Membantu task concepts, computer concepts, dan rincian sintaktik bahasa perintah.
    - Topik:
      - Urutan argumen yang konsisten
      - Simbol vs keyword
      - Struktur hierarkis dan kongruensi

### Urutan Argumen yang konsistensi
    Beberapa studi menunjukkan adanya manfaat urutan argumen yang konsisten.
    ```
    Inconsistent order              Consistent order

    SEARCH file no, message id      SEARCH message id, file no
    TRIM message id, segment size   TRIM message id, segment size
    REPLACE message id, code no     REPLACE message id, code no
    INVERT group size, message id   INVERT message id, group size
    ```
### Simbol Lawan Keyword
    Penggunaan keyword lebih mudah daripada simbol.
    Pemakai berpengalaman dapat mengembangkan keterampilan untuk menggunakan notasi aneh sehingga variasi sintaktik tidak banyak berpengaruh.
    ```
  	Symbol Editor                Keyword Editor

  	FIND:/TOOTH/-1               BACKWARD TO “TOOTH”
  	LIST;10                      LIST 10 LINES
  	RS:/KO/,/OK/;*               CHANGE ALL “KO” TO “OK”
    ```
### Struktur Hierarkis dan Kongruensi
    Kongruen: pasangan yang berlawanan secara selaras dan berarti (simetris).
    Struktur hierarkis dan kongruensi dapat membantu ingatan pemakai.
    ```
    Congruent
    Hierarchical           Nonhierarchical
    MOVE ROBOT FORWARD     ADVANCE
    MOVE ROBOT BACKWARD    RETREAT
    MOVE ARM FORWARD       PUSH
    MOVE ARM BACKWARD      PULL
    MOVE ARM RIGHT         SWING OUT
    MOVE ARM LEFT          SWING IN

    Noncongruent
    Hierarchical           Nonhierarchical
    MOVE ROBOT FORWARD     GO
    CHANGE ROBOT BACKWARD  BACK
    CHANGE ARM FORWARD     POKE
    MOVE ARM BACKWARD      PULL
    CHANGE ARM RIGHT       PIVOT
    MOVE ARM LEFT          SWEEP
    ```
### Ringkasan Manfaat Struktur
    Sumber struktur yang terbukti bermanfaat meliputi:
    - Konsistensi posisi
    - Konsistensi tatabahasa
    - Pasangan yang kongruen
    - Bentuk hierarkis

## Penamaan perintah
  Penamaan penting untuk proses belajar, pemecahan masalah, dan ingatan.
  Ketertentuan (specificity) vs keumuman (generality):
  - Istilah-istilah yang spesifik lebih deskriptif dan lebih mudah diingat.
  - Istilah-istilah yang umum lebih dikenal dan mudah diterima.
  Contoh pengujian untuk menambah dan menghapus teks (Black & Moran):
  ```
  Infrequent, discriminating words      insert    delete
  Frequent, discriminating words        add       remove
  Infrequent, nondiscriminating words   amble     perceive
  Frequent, nondiscriminating words     walk      view
  General words (frequent, nondiscr.)   alter     correct
  Nondiscriminating nonwords (nonsense) GAC       MIK
  Discriminating nonwords (icons)       abc-adbc  abc-ac
  ```
  Paling baik: “infrequent, discriminating”
  Paling buruk: general words.
  Nonsense cukup baik!
## Penyingkatan Perintah
  - Pemotongan sederhana.
    directory -> dir, delete -> del.
  - Buang huruf hidup dengan pemotongan sederhana.
    check disk -> chkdsk, move -> mv.
  - Huruf pertama dan terakhir.
    sort -> ST, block -> BK.
  - Huruf awal setiap kata dalam frase.
    change directory -> cd, switch user -> su.
  - Singkatan standar dari konteks lain.
    quantity -> QTY, transfer ->  XFER,
    backup -> BAK.
  - Fonik: fokus pada suara.
    execute -> XQT, I seek you -> ICQ,
    connection -> CNXN.

## Menu perintah
    Untuk mengatasi beban penghafalan perintah, beberapa perancang memberikan daftar perintah yang tersedia, dalam format yang disebut menu perintah.
    Contoh:
    ```
    Lynx
      H)elp O)ptions P)rint G)o M)ain screen Q)uit /=search [delete]=history list

    Pico
    	^G Get Help  ^O Writeout  ^R Read File
      ^X Exit      ^J Justify   ^W Where is

    WordStar
    	    --Cursor Movement--     | -Delete-
    ^S char left ^D char right    |^G char
    ^A word left ^F word right    |DEL chr lf
    ^E line up   ^X line down     | ^T word rt
          --Scrolling–-           |^Y line
    ^Z line down ^W line up       |
    ^C screen up ^R screen down   |
    ```
## Bahasa Alami di dalam komputer
  - Natural-language interaction
    Operasi komputer menggunakan bahasa alami manusia (mis. Inggris) untuk memberi instruksi dan menerima respons.
  - Natural-language queries
    Operasi pada database relasional.
    Masih lebih buruk daripada SQL.
    Contoh: INTELLECT, Symantec Q&A.
  - Text-database searching
    Untuk mencari database tekstual.
    Contoh: Ask Jeeves (ask.com).
  - Natural-language text generation
    Digunakan untuk laporan (mis. Prakiraan cuaca, laboratorium medis).
    Di sisi artistik dapat menghasilkan puisi dan novel.
  - Adventure and educational games
    Pemakai menyatakan gerakan dan perintah dengan bahasa alami.
    Menarik karena sistem tak dapat diramalkan dan perlu dijelajahi.

## Pedoman bahasa perintah
- Buat model objek dan aksi yang eksplisit.
- Pilih nama yang berarti, spesifik, dan dapat dibedakan.
- Coba mencapai struktur hierarkis.
- Gunakan struktur yang konsisten (hierarki, urutan argumen, aksi-objek).
- Dukung aturan penyingkatan yang konsisten.
- Berikan kemampuan membuat makro bagi frequent users.
- Pertimbangkan menu perintah pada tampilan berkecepatan tinggi.
- Batasi jumlah perintah dan cara melakukan tugas.
