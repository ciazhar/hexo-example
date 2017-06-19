---
title: Error Handling
date: 2017-06-19 09:37:35
tags:
  - ui-ux
categories:
  - Teknologi
  - Interaksi Manusia dan Komputer

---

![](http://bigdatadimension.com/wp-content/uploads/2017/03/Error-Handling-Testing.png)


# Apa Itu Error Handling :

Error Handling adalah suatu penanganan kesalahan ( eror ) pada berbagai keadaan dalam pemrograman. Setiap ada kesalahan, maka eksekusi program tidak akan dihentikan secara tiba - tiba, tetapi akan diteruskan ke baris program yang terdapat script penanganan kesalahan.
Contoh : Aplikasi Produk Jadi, misalkan Form pendaftaran media, konsumen telah mengisikan hampir seluruh datanya pada form pendaftaran tersebut, tetapi ditengah program terdapat suatu eror atau bug, jadi dengan penanganan yang baik, penanganan kesalahan akan dilakukan setelah baris program diisikan.

# Kelebihan dan Kekurangan Error Handling :

## Kelebihan :
- Membantu user dalam menangani kesalahan.
- Resiko kehilangan data dapat diminalisir.
- Mempermudah programmer dalam pendeteksian kesalahan.
- User tidak perlu melakukan restart program setelah terjadi kesalahan.

## Kekurangan :
- Memperumit Kode Program.
- Programmer harus benar - benar tahu kemungkinan kesalahan yang akan muncul.
- Satu fungsi pada program bisa memiliki berbagai kemungkinan kesalahan.

# Macam - Macam Jenis Error :
- Perceptual Error : adanya kesalahan yang disebabkan oleh ketidakjelasan keterangan dari petunjuk penggunaan yang menyebabkan kesalah tanggapan dari pihak pengguna atau user. Contoh : Icon yang ambigu dalam desain antarmuka.
- Cognitive Error : Kesalahan yang diakibatkan oleh kemampuan memecah oleh user atau karena banyak konteks dan informasi status.
- Motor Error : kesalahan yang disebabkan oleh ketidak sinkronan antara mata, tangan, dan kemampuan yang dimiliki oleh user. Contoh : typo / terlalu cepat mengetik, double klik pada mouse.


# Jenis - Jenis Kesalahan Dari User :
- Mistake : kesalahan yang terjadi ketika user berpikir bahwa sudah melakukan hal yang benar namun sebenarnya user melakukan kesalahan.
- Slip : kesalahan diluar keinginan user. Contoh : saat ingin menutup user ingin mengklik tombol close tetapi secara tidak sengaja user menekan tombol minimize.



# Jenis - Jenis Kesalahan Pada Program :
- Syntax Error : kesalahan dari penulisan syntax pada program sehingga syntax tersebut tidak dapat dieksekusi oleh program dan membuat program eror. Contoh : pada C++, baris kode harus selalu diakhiri dengan tanda (;) atau kesalahan penulisan pada standar penulisan program.
- Logical Error : kesalahan yang disebabkan oleh programmer karena kesalahan penulisan atau rumus yang diterapkan. Contoh : saat kita membuat program yang menghasilkan nilai luas, kita menuliskan 7 tetapi hasil yang ditampilkan program adalah 11 atau pada saat kita menulis variabel s adalah hasil tambah, tetapi yang didekrasikan pada awal adalah S besar.
- Runtime Error : kesalahan yang terjadi ketika sebuah program komputer dijalankan.



# Cara Membuat Error Handling yang Baik :

- Gunakan bahasa yang mudah dipahami oleh user.
- Hindari kata - kata seperti : bad, dummy, dll.
- Hindari kalimat perintah.
- FAQ ( Frequently Asked Questions ).
- Optimalisasikan dan pemanfaatan undo redo function dan cancel.
- Menyiapkan berbagai macam model respon.
- Validitas masukan / inteligent error checking dan recovery.
- Proteksi pengguna.
- Penampilan pesan.
- Optimasikan fungsi HELP ( quick access help ).
- Editing of Error Fields.
- Desain yang efektif dan effisien.
- Return cursor dan Highlight error.
- No Interupting Work Flow.
- Confirmation Commands.


# Tips sederhana untuk mencegah terjadinya error dalam program :
- Menulislah dengan teliti, coba ikuti aturan penulisan program dengan benar dan konsisten.
- Menulislah dengan rapi, coba ikuti aturan penulisan program yang baik atau mengikuti konvensi ( coding standar ).  Hal ini akan mempermudah dalam pencarian kesalahan program.
- Selalu konsisten dalam penamaan variabel dan sejenisnya juga membantu mencegah terjadinya error karena terkadang kesalahan terjadi karena perbedaan huruf besar dan kecil.
- Pastikan algoritma yang digunakan sudah teruji kebenarannya.
