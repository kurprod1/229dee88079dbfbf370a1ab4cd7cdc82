# 6. Membuat Repositori dan Revisi

Created: July 14, 2022 1:16 PM

# **Membuat Repositori**

Bayangkan sebuah rak yang digunakan untuk menyimpan buku buku dipajang. Di dalam rak ini terdapat banyak buku. Ada 1 buku dengan banyak cetakan, yaitu cetakan ke-1, ke-2, sampai ke-4. Nah repository juga seperti rak tersebut yang berguna untuk menyimpan asset atau dalam konteks pembelajaran kita, source code.

Membuat repository bisa digunakan dengan command git init yang secara langsung membuat repository local untuk temen temen.

Pembuatan repositori dapat dilakukan dengan perintah : **git init nama-direktori**

```bash
git init cilsy
```

Perintah tersebut akan membuat direktori bernama cilsy. Kalau direktorinya sudah ada, maka Git akan melakukan inisialisasi di dalam direktori tersebut. Perintah git init akan membuat sebuah direktori bernama .git di dalam proyek kita. Direktori ini digunakan Git sebagai database untuk menyimpan perubahan yang kita lakukan.

**Hati-hati apabila kita menghapus direktori ini, maka semua rekaman atau catatan yang dilakukan oleh Git akan hilang.**

Contoh lainnya perintah berikut ini akan membuat repositori pada direktori saat ini (working directory).

```bash
git init .
```

Tanda titik (.) artinya kita akan membuat repository pada direktori tempat kita berada saat ini. Perintah berikut ini akan membuat repositori pada direktori /var/www/html/proyekweb/.

```bash
git init /var/www/html/proyekweb
```

## ***Gitignore***

Gitignore ( *.gitignore* ) merupakan sebuah file yang berisi daftar nama-nama file dan direktori yang akan diabaikan oleh Git. Perubahan apapun yang kita lakukan terhadap file dan direktori yang sudah masuk ke dalam daftar .gitignore tidak akan dicatat oleh Git.

Untuk dapat mengunakan .gitignore, buat saja sebuah file bernama .gitignore dalam root direktori **proyek/repo**. Misalnya kita isi filenya seperti berikut :

```bash
/vendor/
/upload/
/cache
test.php
```

Pada contoh file .gitignore di atas, kita memasukan direktori vendor, upload, cache dan file test.php. File dan direktori tersebut akan diabaikan oleh Git. Pembuatan file .gitignore sebaiknya dilakukan di awal pembuatan repositori.

# **Revisi**

Sebelumnya kita sudah membuat repositori kosong. Sekarang kita coba tambahkan sebuah file baru. Sebagai contoh, kita akan menambahkan tiga file HTML kosong.

[*Pembuatan file html*](https://lh4.googleusercontent.com/KRvsrx15O_xC4HnFdMmhyOjWovwpfO9FoAUAMW7m5RrLoEbvzp4s57GVSutpram6xCm1fi4r0PaVNppnm40u4iwPyw0bW4WogvE7MRKZBbasBHQPuUcLIO5XUovf85nc0yi8Ji7WmZLrSxdWxw)

*Pembuatan file html*

Setelah ditambahkan, coba ketikan perintah git status untuk melihat status repositorinya.

[*Melihat status Git*](https://lh6.googleusercontent.com/gsoEa-cMNx3GbVEr1KMcqjqzYcHfo77i0MFp6rz0swVdD7il8Y9M6RCx4KYrYU7L1TNyk6aPDNn0cj7ksDwrrARIYrliONhpYA7UTeIFI3qT8n2fqLiXmoamPxZB9zIv8_ppPOvIF749wTuAig)

*Melihat status Git*

Berdasarkan keterangan di atas, saat ini kita berada cabang (branch) master dan ada tiga file yang belum ditambahkan ke Git.

Ada Tiga Kelompok Kondisi File dalam Git yang diantaranya sebagai berikut.

1. **Modified**
    
    Modified adalah kondisi dimana revisi atau perubahan sudah dilakukan, tetapi belum ditandai dan belum disimpan di version control. Contohnya pada gambar di atas, ada tiga file HTML yang dalam kondisi modified.
    
2. **Staged**
    
    Staged adalah kondisi dimana revisi sudah ditandai, tetapi belum disimpan di version control. Untuk mengubah kondisi file dari modified ke staged gunakan perintah *git add nama_file*. Contoh:
    
    ```bash
    git add index.html
    ```
    
3. **Commited**
    
    Commited adalah kondisi dimana revisi sudah disimpan di version control. perintah untuk mengubah kondisi file dari staged ke commited adalah *git commit*.
    

Sekarang kita sudah tahu kondisi-kondisi file dalam Git. Selanjutnya, silahkan ubah kondisi tiga file HTML tadi menjadi staged dengan perintah *git add*.

```bash
git add index.html
git add about.html
git add contact.html
```

Kita dapat melakukan seperti dibawah ini untuk menandai banyak.

```bash
git add index.html about.html contect.html
```

Atau seperti ini untuk add extention yang dipilih.

```bash
git add *.html
```

Jika ingin add semuanya, gunakan perintah ini(semua file dan direktori di current directory).

```bash
git add .
```

Setelah itu cobalah ketik perintah *git status* lagi. Kondisi filenya sekarang akan menjadi *staged*.

[*Melihat status Staged*](https://lh5.googleusercontent.com/-ESZSTQppdcLC4ZPEshUZ7dcmwOpbwT4jB2Dz-TGYbvJJzm9cfZC-nOVPnbwQePJgBr62PbPIErrplZQ1vLQYKWeXvq1CRpVVyXJdmGEGv7xJp0csTqjgVBojGIuO-yXL5HoG2Fxj5VxAURr7g)

*Melihat status Staged*

Setelah itu, ubah kondisi file tersebut ke commited agar semua perubahan disimpan oleh Git.

```bash
git commit -m ‘Commit Pertama’
```

[*Melihat status Commit*](https://lh5.googleusercontent.com/puKkbTTfAohnrNIBr-nv3ZBapiau9rVK-0mtUnCh-Q390XM5mZ46sAez7GaV99bOOdjTCRVQjdX88hUHaM-zPsuCxDWEsG8J70bLinIp3j37Ki-JuIscrV5buc1mtZ5IgJspnmKEz0J2Ly6dxQ)

*Melihat status Commit*

Sekarang kita akan mencoba untuk membuat Revisi kedua. Misalkan skenarionya adalah  ada perubahan yang akan kita lakukan pada file index.html. Silahkan modifikasi isi file index.html. Sebagai contoh kita mengisinya seperti ini.

```bash
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Belajar Git - Project 01</title>
    </head>
    <body>
        <p>Hello Semua, kita sedang belajar Git</p>
    </body>
</html>
```

Setelah itu ketik lagi perintah *git status*.

[*Melihat git status*](https://lh3.googleusercontent.com/pBsPJX8KvVCEh-9S-lsaGyOMse-T5h2djIfh5v3uyjJucjCBeQtxFPl7qDq09Wi-1fzc9y4hH2hpZ8_23xBjkjMX8qi6DNUG3YI1aIK_Cw3ytyk4sbo5TJRJTQySCyGTBW6TfteTPYimxYzeEA)

*Melihat git status*

Terlihat di sana, file index.html sudah dimodifikasi. Kondisinya sekarang berada dalam modified. Lakukan commit lagi seperti revisi pertama.

[*Melihat status commit*](https://lh6.googleusercontent.com/hIexhrfJdl1yTdUyk8OKxN4L7FSULZwXFJhrPAUaaoXMdLZF8Ab386M9iSl4fPh1XA_D7NiDVe6dN2-ZIrn-MV40t0-TSnQVlO8DtiGhR9cGv-mnF0zJvpu0qUGtUTMyiEAt4bmxg1rfEjnOug)

*Melihat status commit*

Dengan demikian, revisi kedua sudah disipan oleh Git. Mungkin anda belum tahu maksud dari argumen -m, argumen tersebut untuk menambahkan pesan setiap menyimpan revisi.

[*Ilustrasi revisi*](https://lh6.googleusercontent.com/FK9rY1hrq7DFmF2XwswUvt9AUB6Fm7Kw-k6XyRW2XtJkxPgyaYiCN8N5fEv5Kl2lxU930Aej_py1dFxUWcSudS-mD0mbGqpG471haurFw2igHKv4oanVIXWTr7Aq9gzQ8QTn7Yxr613GDDSnpw)

*Ilustrasi revisi*

Sekarang Git sudah mencatat dua revisi yang sudah kita lakukan. Kita bisa ibaratkan revisi-revisi ini sebagai checkpoint pada Game. Apabila nanti ada kesalahan, kita bisa kembali ke checkpoint ini.

## ***Melihat Log Revisi***

Pada skenario sebelumnya, kita sudah membuat dua revisi pada repositori project-01. Sekarang bagaimana caranya kita melihat catatan log dari revisi-reivisi tersebut? Git sudah menyediakan perintah git log untuk melihat catatan log perubahan pada respositori. Contoh penggunaannya:

```bash
git log
```

[*Melihat log revisi*](https://lh3.googleusercontent.com/BbHpJn8gQLARxy6aqptj7vDWFRorUSpD0XnrNbKQpPCYGAgY3EA0QehNVjyYl_DsOWEEFuZnskE-Hykg-y1gPnjCI6oT8GNo4tUM9vJ36cDL4AJRRO9ITvEOh6pMZuRqFJwn6SJoPFr1Q8CMMg)

*Melihat log revisi*

Pada gambar di atas, terdapat dua revisi perubahan yang telah dilakukan. Untuk menampilkan log yang lebih pendek, kita bisa menambahkan argumen --oneline.

```bash
git log --oneline
```

[*Melihat log lebih pendek*](https://lh3.googleusercontent.com/aI46GMslr_HJF6VW_kcTMcZzyavsDUy-jeH2E7QjnNFnKHVzbKdlGN-Hor6oLpv0Jp3iiJ3BumXM8Ti5P84eN7Af21ENdHc4TqeGgNCyOXbBc6rxqrZi7Xmi6mqSP3xDUaaePzGkF8bE00Bcsg)

*Melihat log lebih pendek*

## ***Log pada Nomor Revisi/Commit***

Untuk melihat log pada revisi tertentu, kita bisa memasukan nomer revisi/commit.

```bash
git log 331f6058c6ed132af24d5ca1f17a306d5683f9f1
```

[*Melihat revisi nomor commit*](https://lh4.googleusercontent.com/6Z1GDRN3qmv5CsOukW9o7i1zEu_OHORn8NiKtWQEsjy45NmCnRi7guqnl6hy7_GUgVhY5HvMBOmxLUF_jiKEGaCUec3GzW7AhHmEQsV5Btd0eYtmvo_N_xAChdU1j0zcYFWN9cC7EJ0MlVle7w)

*Melihat revisi nomor commit*

## ***Log pada File Tertentu.***

Untuk melihat revisi pada file tertentu, kita dapat memasukan nama filenya.

```bash
git log index.html
```

[*Melihat log pada file tertentu*](https://lh5.googleusercontent.com/YHsHOajwcaftQkI0220SPmJi55QKVZXIcaz0KnjjcUyj0_G3gjRlp3FfIw5Gv26lA-t9BFvGP_h2vNzFk3VCWlSHdkX5cYVmMZhKiom_SyiLrnrp8h5V_CXgp7OuT3B9LpjvQ0Sm0dbuYXBP3Q)

*Melihat log pada file tertentu*

[*Melihat log author tertentu*](https://lh6.googleusercontent.com/flW3bX-XxF4FceqaRfZoZNbsqcMKWdkubR6EkeAHQkhEFTO39fP3xC1TP1mg0idz5ZCqlo3hHoPZejGlvBK_thODoyyJalheTy3A9yAFddXYAZuACxZC4uV-uJ8460-E4kdzA4rfWr-Mmtzgfw)

*Melihat log author tertentu*

# ***Melihat Perbandingan Perubahan yang Dilakukan pada Revisi***

Gunakan perintah berikut ini untuk melihat perubahan apa saja yang dilakukan pada revisi tertentu.

```bash
git diff commit_number
```

[*Melihat perbedaan*](https://lh4.googleusercontent.com/zWK3E2JkyakcdBwEAIEzEnUf3fHpfGiPG2xjeO4Z2Ayh_e3R-RY1AmqZt6pQSB2G1rUqmjYi69_f41z1qAJY3zctijXEzXJzG29-j3hRlFH214MJB95JCjKqCtADauUrinHBTiCtr52NJZ1n5Q)

*Melihat perbedaan*

Lihatlah hasil di atas, simbol plus (+) artinya kode yang ditambahkan. Sedangkan kalau ada kode yang dihapus simbolnya akan menggunakan minus (-).

Sekarang kita akan mencoba merubah isi dari index.html untuk melihat perbedaannya. Kita coba cek lagi bahwa berikut adalah kode original sebelum diubah:

```bash
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Belajar Git - Project 01</title>
    </head>
    <body>
        <p>Hello Semua, kita sedang belajar Git</p>
    </body>
</html>
```

Berikut adalah kode setelah diubah :

```bash
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Belajar Git - Project 01</title>
    </head>
    <body>
        <p>Hello Dunia!, kita sedang belajar Git</p>
    </body>
</html>
```

Setelah itu lakukan jalankan perintah git diff lagi.

[*Melihat hasil akhir perbedaan*](https://lh4.googleusercontent.com/wNrYkj9o2toFi44RVe4QgQ6DvyQwndGQjoiKFgJS2jF6Ri_IUDhnnnrNd_yvPqnY-kciOZHkO4iJVBDb1ulBJWkg6Cu6DVoN2mckQP_DXz2m5GXZvs5hcySeeCO9k7RDigtoU_5z5QTzRBlRQA)

*Melihat hasil akhir perbedaan*

Perintah git diff akan membandingkan perubahan yang baru saja dilakukan dengan revisi/commit terakhir.

# ***Melihat Perbandingan pada File***

Apabila kita melakukan banyak perubahan, maka akan banyak sekali tampil output. Karena itu, kita mungkin hanya perlu melihat perubahan untuk file tertentu saja. Untuk melihat perbandingan perubahan pada file tertentu, gunakan perintah berikut.

```bash
git diff index.html
```

Perintah di atas akan melihat pebedaan perubahan pada file index.html saja.

# ***Melihat Perbandingan antar Revisi/Commit***

Perintah untuk membandingkan perubahan pada revisi dengan revisi yang lain dapat menggunakan perinta dibawah ini.

git diff <nomer commit> <nomer commit>

# ***Perbandingan Antar Cabang (Branch)***

Kita memang belum masuk ke materi percabangan di Git. Tapi tidak ada salahnya megetahui cara melihat perbandingan perubahan antar cabang.

```bash
git diff <nama cabang> <nama cabang>
```

Kita sudah pelajari fungsi dari perintah git diff. Perintah ini untuk melihat perbandingan perubahan apa saja yang telah dilakukan pada repositori.

# **Exercise**

1. Buat sebuah repository Git baru dengan nama Anda !
2. Buat file gitignore pada repository tersebut !
3. Buat beberapa file dan lakukan revisi sebanyak tiga kali !