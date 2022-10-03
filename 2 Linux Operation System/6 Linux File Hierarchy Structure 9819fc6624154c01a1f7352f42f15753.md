# 6. Linux File Hierarchy Structure

Created: June 23, 2022 2:38 PM

# **Apa itu struktur direktori?**

Pada sistem operasi Linux terdapat susunan direktori yang harus diketahui. Susunan direktori tersebut tentunya memiliki kegunaannya masing masing. Apa saja struktur direktori pada Linux?

Kita perlu mempelajari hal ini agar kita benar-benar tahu seperti apa isi dari sistem operasi GNU/Linux yang akan kita kelola saat menjadi DevOps nanti. Kita harus tahu folder A untuk apa, folder B untuk menyimpan file apa, folder C sebaiknya tidak boleh dihapus, dst.

Analoginya simple. Ibarat rumah, kita harus tau masing-masing ruangan di rumah tersebut fungsinya untuk apa. Agar kita tidak tersesat, agar kita tidak salah meletakkan barang, maupun agar kita tidak salah membuang barang yang ada didalamnya.

Sebagai pemilik rumah, kita wajib menguasai seluk beluk ruangan dari rumah kita sendiri. Sebagai DevOps kita wajib mengetahui seluk beluk struktur direktori dari server Linux kita sendiri.

## **Penjelasan Struktur Direktori**

Struktur direktori GNU/Linux sangat berbeda dengan struktur direktori windows/dos dimana dalam GNU/Linux tidak akan ditemukan drive a, drive c dan drive lainnya karena GNU/Linux menganut satu direktori utama yaitu direktori / (dibaca root). Dimana nantinya keseluruhan direktori dan file lainnya akan berada di dalam/dibawah direktori / ini.

![*Struktur direktori di Linux*](https://lh3.googleusercontent.com/WDd-vAjLGHcXbGJ20NX8BwqPo0eHwBsN_sdCuCjN2jsvZw-0ZBITHOF5ODThmAGHDFZK3g7unKWX1FMk_pwvFgjdqX1TsUxq_EfqVk2SNuDhkg9QuHg5HABxMeUyqTL989XS2ZhyhYayNvS6EA)

*Struktur direktori di Linux*

Seluruh folder yang ada di bawah /, memiliki fungsi nya masing-masing sebagai berikut :

|/  |Dibaca root, merupakan direktori utama sistem Linux. Ibaratnya seperti C: pada windows.|
|---|---------------------------------------------------------------------------------------|
|/bin|Direktori yang berisi binary files yang dapat dieksekusi oleh users system. Direktori ini menghandle perintah-perintah standar GNU/Linux diantaranya ls, cp, mv dan beberapa lainnya.|
|/boot|Direktori yang berisikan file-file yang dibutuhkan saat proses booting termasuk didalamnya adalah kernel image GNU/Linux.|
|/dev|Direktori yang merepresentasikan/mewakili device hardware. Dalam GNU/Linux everything is files, dimana hard disk, cdrom, dll itu dianggap sebagai file. Semua device hardware komputer direpresentasikan sebagai file pada direktori ini.|
|/etc|Direktori yang berisi file-file konfigurasi system dan layanan. File-file konfigurasi ini dibutuhkan oleh paket-paket lain untuk menjaga perilaku system.|
|/home|Merupakan home direktori atau area kerja dari masing-masing user GNU/Linux kecuali user root(super user). User-user biasa menimpan data disini.|
|/lib|Merupakan direktori file-file library GNU/Linux yang mendukung binary files baik yang berada didirektori /bin maupun /sbin.|
|/mnt|Direktori yang disiapkan untuk mounting point device storage seperti flashdisk dan harddisk eksternal.|
|/media|Direktori memounting/mengaitkan media removable storages seperti harddisk eksternal, floppy disk, cdrom/dvdrom, flashdisk, digital kamera maupun media lainnya. Mirip seperti /mnt.|
|/opt|Direktori tempat instalasi paket yang diluar dari repository resmi.                    |
|/proc|Merupakan direktori yang unik yang dinamis karena direktori ini berisi virtual file system yang menyediakan akses informasi cpu, ram, kernel, suhu, dll secara realtime.|
|/root|Home direktori khusus super user (user root). Direktori ini sengaja dipisahkan dari direktori home user biasa di /home untuk menghandle jika partisi /home gagal di mounting maka system secara keseluruhan dapat diselamatkan oleh root. /root dibaca slash root.|
|/sbin|Direktori ini pada prinsipnya sama dengan direktori /bin yang berisi file-file binary. Namun direktori /sbin ini hanya dapat diakses oleh user root dalam kondisi sistem normal. Users biasa tidak memiliki akses untuk menjalankan binary files di direktori ini|
|/tmp|Direktori yang berisi temporary files artinya file-file yang sifatnya hanya dibutuhkan sementara dan akan hilang setiap komputer booting. Direktori ini dapat diakses oleh semua users sistem.|
|/usr|Bisa dikatakan sebagai direktori utama dibawah main direktori tempat diletakkannya file- file program aplikasi, dokumentasi, source kernel dan x-window system dari distribusi GNU/Linux yang digunakan. Mirip seperti Program Files pada Windows.|
|/var|Direktori yang diperuntukkan menyimpan file-file yang akan terus membesar ukurannya. Biasa digunakan untuk menyimpan file-file log system, file email, file-file web, file database.|

Sampai tahap ini, minimal kita sudah sekilas mengetahui fungsi-fungsi dari masing-masing folder yang ada di Linux

## **Penulisan Struktur Direktori**

Penulisan struktur direktori ini sangat penting dipahami untuk kepentingan penggunaan perintah-perintah command Line Linux nantinya. Karena salah satu huruf saja saat mengetikkan penulisan struktur direktori, maka dianggap oleh sistem Linux salah. Ketika dianggap salah, maka perintah-perintah yang ingin kita jalankan tidak akan bekerja.

Pada penulisan struktur direktori, terdapat 2 cara penulisan. Yaitu penulisan alamat folder secara lengkap, serta penulisan alamat folder berdasarkan posisi kita berada. Kita coba bahas satu persatu.

### ***Penulisan Alamat Lengkap***

Coba perhatikan gambar dibawah :

![*Alamat direktori 1*](https://lh3.googleusercontent.com/UdcnXY7Wn420QKSuViZEiZ4Eje9YlVJvmctZlWjoeYtU00EyEum3lbMOnKs_SedukUcTsIL7211VUl_2iilioSjCUfgBZOV8a7pQNanZubRcnx1WDn_jX5dy6ztfVAkkERJlHhGssNSEpluIhw)

*Alamat direktori 1*

Nama lain dari penulisan alamat lengkap adalah **absolute path**. Pada gambar tersebut terlihat ada folder bernama musik yang berada di dalam folder home dan folder home ada di dalam folder utama /. Nah jika kita ditanya bagaimanakah penulisan dari folder musik? Penulisan hirarki folder ditulis lengkap dari folder utama (/) hingga folder yang dituju dengan dipisahkan tanda / di masing-masing foldernya. Sehingga penulisannya menjadi seperti ini :

```bash
/home/musik
```

Contoh lain :

![*Alamat direktori 2*](https://lh4.googleusercontent.com/iFpL5f2ZYQHk_dcqzx5VIJhU0NIhCJccfuanyin5RWUu3xz-NTcekM0dJcUm67k4A6lc-a-BVMbfY1naqaOiPQiyKRgFZUUWS8GTvvk0NvPfB1rIIXBnaIvkv1Sn7ibIMo2MhvTVRFLjW1YC9Q)

*Alamat direktori 2*

Pada gambar tersebut ada dua hierarki yang terpisah. Maka jika ditanya bagaimana penulisan dari folder sosial dan keuangan? Maka penulisannya menjadi seperti ini :

`Hierarki 1 : /media/flashdisk/cilsy/sosial`

`Hierarki 2 : /tmp/kasus/keuangan`

Lalu jika ditanya lagi, bagaimanakah penulisan dari folder media dan kasus? Maka menjadi seperti ini :

`Hierarki 1 : /media`

`Hierarki 2 : /tmp/kasus`

Sebenarnya kita cukup membayangkan hierarki folder dan penulisan ini seperti layaknya kita melakukan klik folder, lalu di dalam folder tersebut ada folder lain lagi, di klik lagi ada folder lagi, dst.

Keuntungan dari teknik alamat lengkap ini adalah minim kesalahan. Selama kita menulis alamat lengkapnya secara benar, maka kita tidak perlu khawatir salah melakukan perintah command line tertentu nantinya.

Kekurangan dari teknik ini adalah kita akan cukup panjang saat mengetik alamat foldernya. Apalagi jika letak foldernya sangat dalam dan jauh. Misalnya saja :

```bash
/var/www/html/bhinneka/admin/panel/configuration/beta1/access
```

Akan sangat melelahkan bukan jika harus terus mengetik sepanjang itu?

### ***Penulisan Alamat berdasarkan posisi kita berada***

Untuk mengatasi penulisan alamat yang terlalu panjang, kita bisa menggunakan teknik yang satu ini. Teknik ini memperdulikan posisi kita berada saat melakukan penulisan alamat. Sehingga file atau folder yang ada didalam posisi kita saat ini berada tidak perlu di tulis dengan tanda / dan folder-folder diatas posisi kita berada tidak perlu di tulis kembali. Nama lain dari penulisan alamat berdasarkan posisi adalah **relative path**.

Misalnya masih pada kasus yang sama dengan folder musik, namun disini dianggap kita berada di dalam folder home.

![*Alamat direktori 3*](https://lh6.googleusercontent.com/ghIQab6rwbDdFg5qiw_Yt3La5dIMEa4LJAsVBhpr645jvDm5oOwX78GTxtwIoVZ-_hYb41zixwkQeRhIbw2J94XfGcQAyRpk9QgfP-632P9O8pxzgUaokj1n2f-A8F3w7pTEu2WMhTlkY0tlig)

*Alamat direktori 3*

Maka ketika kita diminta seperti apakah penulisan folder musik, jawabannya seperti ini :

```bash
musik
```

Jadi sama sekali tidak ada penulisan lengkap mulai dari /home/musik. Melainkan cukup musik saja.

Kita ambil lagi contoh yang ini :

![*Alamat direktori 4*](https://lh4.googleusercontent.com/mEUL9_3XwzRqy5RrdIvfrv-jjaoLuWIQhPXe3tweX6KQE6zRGgmih9sjYdCQpWPsL1tm0g2kV7HoxJ7lzIcjUMtrdMYACB3_OEw7MZoQcRToWrwR0_u6WfVJptzMVCyNnlu38XE-xqCFdl4_1g)

*Alamat direktori 4*

Pada gambar diatas kita diposisikan berada di dalam folder flashdisk. Sehingga jika ditanya penulisan dari folder sosial, adalah seperti ini :

```bash
cilsy/sosial
```

Didepan folder cilsy, sama sekali tidak ada tanda /. Karena folder cilsy berada didalam posisi kita berada sekarang.

Lalu bagaimana dengan folder keuangan? Bisakah kita menuliskannya cukup dengan begini ? :

```bash
kasus/keuangan
```

atau :

```bash
keuangan
```

Jawabannya adalah tidak bisa. Karena kita tidak berada didalam folder tmp maupun folder kasus. Sehingga jika posisi kita berada masih di folder flashdisk tapi diminta untuk menuliskan letak folder keuangan, kita tetap harus menuliskannya lengkap seperti ini :

```bash
/tmp/kasus/keuangan
```

Namun ketika kita sudah pindah ke folder kasus seperti gambar berikut :

![*Alamat direktori 5*](https://lh3.googleusercontent.com/ik7xolebdZt0FJ2ioJKQJKLGLVdvqLdmYOvW5mTuHXMJL3976l_Tp42TJ8pzVosO-pAzPC7AM1xL32zO2CvgoDcHZU9_tI_Qb1IQpamDQ98hCw9ppXgD14vcW054wx4Qaokv1sC1KM1zQy4pSg)

*Alamat direktori 5*

Barulah kita bisa menuliskan keuangan seperti ini :

```bash
keuangan
```

Kalau kita ada di folder tmp, bagaimana kah penulisan alamat folder keuangan?

```bash
kasus/keuangan
```

Kalau kita ada di folder /, bagaimana kah penulisan alamat folder keuangan?

```bash
tmp/kasus/keuangan
```

Kesimpulannya teknik ini dapat lebih mempersingkat penulisan, namun memang sangat rawan kesalahan. Teknik ini biasa digunakan ketika banyak command yang harus dilakukan didalam folder yang sangat dalam posisinya. Kalau belum terlalu paham betul dengan konsep ini, sebaiknya selalu gunakan teknik yang penulisan alamat lengkap.

# **Exercise**

**Teori**

1. Kenapa kita perlu belajar Struktur direktori Linux?

**Praktek**

Waktu pengerjaan : 7 menit.

Masing-masing peserta selesaikan soal dibawah ini dengan cara mengkopi jawabannya ke kolom chat saat pembelajaran.

![*Struktur direktori di Linux*](https://lh6.googleusercontent.com/13dAQ7oWkQgJw11kI60cOwL2_hQxzt-tmpNnXxeJKSFnNahtveeugisp0KDbNnx-MNuYe2bFf4yjOFhwUjgCGuc-6Dv9liRs5BBKfwCSAFxn25ijQWb9FLfnAhRR65vDp0NP3PZy4zTrR8L2Ig)

*Struktur direktori di Linux*

1. Tuliskan alamat dari folder **Mail** yang berada didalam folder **yxz** (abaikan posisi).
2. Tuliskan alamat folder **howto** yang berada didalam **doc** jika posisi kita sedang berada di dalam folder **share**.
3. Tuliskan alamat folder **packages** yang berada didalam **doc** jika posisi kita sedang berada di dalam folder **X11R6**