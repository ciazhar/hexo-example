---
title: two-activity
date: 2017-09-19 13:53:18
tags:
---

### Modal
- Relative View
- Text View
- Button
- Edit Text

### Learn
- Parent Activity
- Intent

### Target
Kita akan membuat 2 acivity yang saling berinteraksi. Dua activity tersebut adalah `MainActivity` yang difungsikan sebagai activity utama/parent dan `SecondActivity` yang difungsikan sebagai activity child. Nantinya MainActivity akan mengakses ke SecondActivity menggunakan Button. Pada SecondActovity akan terdapat tombol kembali atau `<-` yang menuju ke MainActivity.

### Step
- Membuat MainActivity
    - Relative View(activity_second.xml)
    - Button(activity_second.xml)
- Membuat SecondActivity
    - Relative View(activity_second.xml)
    - Text View(activity_second.xml)
    - Konfigurasi Parent Activity (manifest.xml)
        ```
        <activity
            android:name=".SecondActivity"
            android:label="@string/SecondActivity"
            android:parentActivityName=".MainActivity"
            >
            <meta-data
                android:name="android.support.PARENT_ACTIVITY"
                android:value=".MainActivity"
                />
        </activity>
        ```
- Membuat intent untuk menghubungkan MainActivity ke SecondActivity
```
fun launchSecondActivity(view: View) {
    Log.d(LOG_TAG, "Button Clicked")
    val intent = Intent(this, SecondActivity::class.java)
    startActivity(intent)
}
```
- Menambahkan edit text untuk input