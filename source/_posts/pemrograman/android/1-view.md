---
title: Android
date: 2017-04-23 14:17:29
categories:
  - Pemrograman
  - Android
---
![](https://mediarealm.com.au/wp-content/uploads/2013/02/Android-Banner1.jpg)
# Android for Beginner
## Layouting
### View
#### Pengertian View
View pada dasarnya adalah sebuah kotak yang berisi berbagai macam konten. Konten tersebut dapat berupa kalimat gambar, tulisan tombol dan sebagainya.

####	Macam - macam view berdasar kontenya
- Text View
- Image View
- Button

Dalam menuliskan pemrograman, kita diharuskan untuk menulis kode program sebagai instruksi yang spesifik dan detail.

IDE (Integrated Development Environment) merupakan suatu ruang kerja berupa perangkat lunak yang digunakan untuk menulis kode program. IDE yang biasa digunakan untuk menulis kode program android adalah Android Studio.

Bahasa yang digunakan untuk membuat view pada Android berupa XML.

Untuk menulis kode xml anda dapat menggunakan https://udacity.github.io/android-layout.

Kode XML digambarkan sebagai berikut :
	<!--gambar video ke 10-->
	```xml
	<TextView
		android:text="Ini Text"
		android:textColor="@android:color/white"
		android:background="@android:color/black"
		android:layout_width="200dp"
		android:layout_height="300dp"
	/>
	```
Kode tersebut memiliki ketentuan yaitu :
- Kode program ditulis di dalam tag. Tag didefinisikan dengan `<>` (kurung siku).
- Terdapat 2 tag yaitu tag pembuka dan tag penutup. Perbedaan antara tag pembuka dan tag penutup terdapat tanda `/`(garis miring).
```xml
<TextView
  .....
/>
```
Tag juga bisa didefinisikan seperti berikut :
```xml
<TextView>
  ....
</TextView>
```
- Terdapat nama tag yang mewakili view yang ingin dipakai. Dalam contoh diatas nama tag adalah TextView.
- Terdapat atribut(-atribut) yang digunakan untuk mengcustom view tersebut. Semisal untuk konten, warna tinggi dll.
- Setiap atribut memiliki nilai. Nilai mewakili apa yang akan dicustom pada setiap atribut. Nilai tersebut dipisahkan dari atributnya oleh tanda  `=` (samadengan) dan ditulis di dalam `""` (tanda petik dua).

#### Text View
Macam macam atribut untuk text view :
- Menulis text

```xml
<TextView
  android:text="tulis text anda di sini"
/>
```

- Mengatur tinggi dan lebar layout

```xml
<TextView
  android:height_layout="300dp"
  android:width_layout="300dp"
/>
```
Satuan panjang (untuk panjang, tinggi dll) biasanya didefinisikan dengan satuan `dp`.
Atau untuk membuatnya menyesuaikan lebar dan tinggi text, anda dapat menggunakan mengisi nilainya dengan `wrap_content`.
```xml
<TextView
  android:height_layout="wrap_content"
  android:width_layout="wrap_content"
/>
```

- Mengganti warna text

```xml
<TextView
  android:textColor="@android:color/white"
  atau
  android:textColor="#Kode_hexa_desimal"
/>
```

- Mengganti ukuran font

```xml
<TextView
  android:textSize="30sp"
/>
```
Satuan ukuran font didefinisikan dengan `sp`. Ukuran font dapat juga didefinisikan sebagai berikut :

```xml
<TextView
  android:textAppearance="?android:textAppearanceLarge"
  android:textAppearance="?android:textAppearanceMedium"
  android:textAppearance="?android:textAppearanceSmall"
/>
```

- Referensi untuk design dapat dilihat di [Material Design Spec](https://www.google.com/design/spec/material-design/introduction.html) atau [google+ #AndroidDev #Protip](https://plus.google.com/+AndroidDevelopers)


#### Image view
Macam-macam atribut untuk Image View :
- Memilih gambar dari resource/assets:

```xml
<ImageView
  android:src="@drawable/ocean"
/>
```

- Mengatur tinggi dan lebar layout

```xml
<TextView
  android:height_layout="300dp"
  android:width_layout="300dp"
/>
```

- Mengatur posisi dan skala gambar

```xml
<ImageView
  android:scaleType="centerCrop"
  atau
  android:scaleType="center"
/>
```

### Memposisikan View
#### View Group
View group ini digunakan untuk mengelompokkan berbagai macam view. Jadi dia seperti `div` pada html. View group ini juga dapat didefinisikan sebagai parent sedangkan view didefinisikan sebagai child.
Kode XML dari view grup digambarkan sebagai berikut :
```xml
<LinearLayout
  android:orientation="vertical"
  android:layout_width="wrap_content"
  android:layout_height="wrap_content">
  <TextView
    android:text="Guest List"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    />
  <TextView
    android:text="Kunai"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    />
</LinearLayout>
```

Note :
Perlu diketahui setiap XML yang kita buat harus kita tambahkan `xmlns:android="http://schemas.android.com/apk/res/android"`. Kode tersebut biasa disebut `XML namespace declaration`. Ini digunkan untuk mendefinisikan bahwa XML kita digunakan untuk android.  

Macam-macam view grup :
1.  Linear Layout
    View disusun secara berderet baik horizontal ataupun vertikal pada view grup. Untuk menggunakan Linear Layout cukup menggunakan tag `LinearLayout`.
    - Vertical row, yaitu view yang disusun secara vertical atas-bawah. Untuk menggunakan vertical row cukup tambahkan atribut `android:orientation="vertical"`.
    - Horizontal column, yaitu view yang disusun secara horizontal kanan-kiri. Untuk menggunakan horizontal column cukup tambahkan atribut `android:orientation="horizontal"`.

Untuk mengatur panjang dan tinggi view dengan menyesuaikan parentnya dapat menggunakan sintaks sebagai berikut :
```xml
<LinearLayout
  xmlns:android="http://schemas.android.com/apk/res/android"
  android:orientation="vertical"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  >
  <TextView
    android:text="Guest List"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    />
  <TextView
    android:text="Kunai"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    />
</LinearLayout>
```
Pada kode diatas LinearLayout menggunakan match parent yang mengakibatkanya memiliki tinggi dan lebar sebesar resolusi layar. Begitu juga dengan text view yang menyesuaikan LinearLayout memiliki lebar sebesar layar.

Untuk mengatur proporsi pajang dan lebar antar view kita dapat menggunakan `android:layout_weight="1"` dan setiap panjang dan lebar diatur ke 0dp. Berikut contohnya :
```xml
<LinearLayout
  xmlns:android="http://schemas.android.com/apk/res/android"
  android:orientation="vertical"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  >
  <TextView
    android:text="Guest List"
    android:layout_width="0dp"
    android:layout_height="0dp"
    android:layout_weight="1"
    />
  <TextView
    android:text="Kunai"
    android:layout_width="0dp"
    android:layout_height="0dp"
    android:layout_weight="1"
    />
</LinearLayout>
```

2.  Relative Layout
    View disusun secara sembarang. Posisi view dapat dibagi menjadi yaitu bagian atas, kanan, kiri dan bawah.
    - Relative to parent, yaitu view yang disusun relatif berdasarkan pada parent.

    Untuk mengatur konten posisi konten berdasar parentnya dapat menggunakan atribut
    ```xml
    <RelativeView>
      ....
      <TextView
        android:layout_alignParentTop="true/false"
        android:layout_alignParentButton="true/false"
        android:layout_alignParentLeft="true/false"
        android:layout_alignParentRight="true/false">
    <RelativeView>
    ```

    Untuk mengatur perataan konten dapat menggunakan
    ```xml
    <RelativeView>
      ....
      <TextView
        android:layout_centerHorizontal="true/false"
        android:layout_centerVertical="true/false">
    </RelativeView>
    ```

    Posisi tersebut dapat dicustom sesuka hati dan dapat di mix and match. Semisal untuk pojok kiri atas maka yang top dan left diberi nilai true dan seterusnya.

    - Relative to other child, yaitu view yang disusun relatif berdasarkan pada child lainya.

    Untuk mengatur konten posisi konten berdasar parentnya dapat menggunakan atribut
    ```xml
    <RelativeView>
      ....
      <TextView
        android:layout_alignParentTop="true/false"
        android:layout_alignParentButton="true/false"
        android:layout_alignParentLeft="true/false"
        android:layout_alignParentRight="true/false">
    <RelativeView>
    ```

https://icons8.com/android-icons/
