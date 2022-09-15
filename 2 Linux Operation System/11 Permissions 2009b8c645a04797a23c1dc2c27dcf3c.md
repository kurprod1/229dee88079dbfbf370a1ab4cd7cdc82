# 11. Permissions

Created: June 27, 2022 1:37 PM

# **Belajar Permission**

## **Apa itu Permission?**

Permission ini sangat erat kaitannya dengan materi manajemen user dan grup sebelumnya. Dimana materi manajemen user & grup adalah materi untuk membuat dan mendesain skema user dan grup yang diinginkan, sedangkan pada materi Permission kita akan mengatur hak akses apa saja yang kita berikan kepada user-user dan grup tersebut.

## **Penjelasan Konsep Permission**

### ***Aturan Umum Permission***

Permission memiliki aturan-aturan umum sebagai konsep dasar

1. Setiap file pasti dimiliki oleh satu user pemilik dan satu group pemilik

Didalam sistem GNU/Linux setiap file, direktori ataupun proses pasti dimiliki oleh salah satu user dan group. Pada gambar dibawah ditunjukkan bahwa folder rizal dimiliki oleh user rizal dan dimiliki oleh grup rizal. Sedangkan folder lost+found dimiliki oleh user root dan grup root. Angka 1 menunjukkan user pemilik, dan angka 2 menunjukkan grup pemilik.

![https://lh5.googleusercontent.com/cofSWG8hGPiYvdAfpKz9DAsyemk_XvUF43S8qXZV-pRe_sMrD8Is0rzwboj_oTUJujGAAlMQ7QcIyLN2-gWtN_0g8SrXqBGjf1qy_oKWjQkML_12Kh2hRTrfEBLXr9F4RtHxLeZArvEgs3qauA](https://lh5.googleusercontent.com/cofSWG8hGPiYvdAfpKz9DAsyemk_XvUF43S8qXZV-pRe_sMrD8Is0rzwboj_oTUJujGAAlMQ7QcIyLN2-gWtN_0g8SrXqBGjf1qy_oKWjQkML_12Kh2hRTrfEBLXr9F4RtHxLeZArvEgs3qauA)

Selain yang tertera sebagai user pemilik dan grup pemilik disebut other.

2. Setiap file hak aksesnya dimiliki oleh user pemilik, group pemilik dan other. Dan setiap user pemilik, group pemilik, dan other memiliki hak akses nya sendiri-sendiri.

![https://lh5.googleusercontent.com/dslNR3v_YzNsTFjYPtyGdP83FzsmI1Ff_EvmcAkHFOHRRjJuqTXc1W8Fn34M3VAEMjNoQl5rQYPgxoFRnX0pSJGZT9p46wCYbWHELVC3FjGpUq_IU8NNCpVBT4LnyAyJbOZsndCVBuvwaLo06Q](https://lh5.googleusercontent.com/dslNR3v_YzNsTFjYPtyGdP83FzsmI1Ff_EvmcAkHFOHRRjJuqTXc1W8Fn34M3VAEMjNoQl5rQYPgxoFRnX0pSJGZT9p46wCYbWHELVC3FjGpUq_IU8NNCpVBT4LnyAyJbOZsndCVBuvwaLo06Q)

Pada gambar diatas tertulis kombinasi huruf-huruf seperti rwxr-xr-x dan rwx------. Itu disebut sebagai permission atau hak akses. Dimana r berarti hak akses untuk read (membaca, membuka), w berarti hak akses untuk write (menghapus, mengedit, membuat), x berarti hak akses untuk execute (menjalankan script, membuka folder), dan – berarti hak akses none (tidak punya akses apa-apa).

Perhatikan pola dibawah. Secara keseluruhan permission memiliki 9 kombinasi r,w,x,- yang dibagi menjadi 3 blok (masing-masing 3 kombinasi per bloknya). Yaitu blok permission untuk masing-masing user, group, dan others yang sudah ditandai dengan warna merah, hijau dan biru. Masing-masing user, group, dan others memiliki kombinasi permissionnya masing-masing.

![][1]

Jika kita sambungkan lagi dengan screenshot gambar diatas, maka artinya folder rizal memiliki permission rwxr-xr-x. Dimana user rizal sebagai user pemilik memiliki hak akses untuk rwx (full akses) , grup rizal memiliki hak akses untuk r-x (tidak bisa write, hanya baca dan exekusi saja), dan others memiliki hak akses untuk r-x (tidak bisa write, hanya baca dan exekusi saja).

![*Ilustrasi Permission*](https://lh4.googleusercontent.com/-8NuFTJv7ZZiSqeHTAhpT0AORRWXOorXb6SKMZ47rbNuOmKuQJSbm6tGNZMGlMK3khE6CqVKVcH5w9BBIrIlpju8QH9nbi8PFZbWdtkriqFvg1f43Xvm1_RqtFHCBWnFetVW4A9eWhsvRXZX4w)

*Ilustrasi Permission*

1. Group mewakili user-user anggotanya.

Misalnya ada sebuah grup bernama keuangan. Anggota grup tersebut adalah cilsy, egi, adi. Jika ada sebuah file yang dimiliki oleh grup keuangan, maka user cilsy, irfan, dan adi akan mewakili hak akses grup tersebut. Misalnya grup keuangan memiliki hak akses rwx pada folder invoice, maka user cilsy, irfan dan adi bisa melakukan apapun didalam folder tersebut seperti membuat file, mengedit file, membuat folder baru, dll.

4. Other adalah user/grup selain user pemilik maupun group pemilik

Misalnya ada sebuah file yang dimiliki oleh user egi dan grup marketing. Grup marketing beranggotakan tresna dan saputra. Maka jika ada user/grup lain bernama gudang atau jono itu dianggap sebagai other, karena gudang jono bukanlah user egi maupun anggota grup marketing.

5. User pemilik file memiliki hak mengatur permission file bersangkutan

Pada kasus sebelumnya terlihat bahwa folder rizal dimiliki oleh user rizal dan grup rizal serta memiliki permission rwxr-xr-x. Nah yang berhak untuk merubah permission rwxr-xr-x menjadi misalnya rwx------ , itu hanyalah user rizal sebagai user pemilik. Jika ada user lain misalnya cilsy, maka itu tidak bisa mengubahnya. Selain user pemiliki ada 1 user yang juga bisa mengubah pemission, yaitu user root (administrator).

## ***Cara Menghitung Nilai Oktal Permission***

Perhatikan kembali pola berikut :

![][1]

Pada materi ini, kita akan belajar untuk bisa mengubah seluruh 9 kombinasi rwx pada permission diatas menjadi bentuk angka. Kenapa? Karena saat kita melakukan pengaturan permission, kita akan memasukkan sintaks commandnya dalam bentuk angka. Misalnya 777 untuk mewakili kombinasi rwxrwxrwx, 755 untuk mewakili kombinasi rwxr-xr-x, 600 untuk mewakili kombinasi rw-------, dst.

Lalu bagaimana cara menghitungnya? Pertama-tama kita perlu tahu dulu berapa nilai satuan dari masing-masing rwx-. Yaitu sebagai berikut :

`r = 4		w = 2		x = 1		- = 0`

Setelah mengetahui nilai satuannya, kita coba gabungkan kombinasi tersebut kedalam 1 blok terlebih dahulu. Caranya adalah dengan menjumlahkan nilainya. Misalnya begini :

```
rwx = (r) 4 + (w) 2 + (x) 1 = 7
r-x = (r) 4 + (-) 0 + (x) 1 = 5
r-- = (r) 4 + (-) 0 + (-) 0 = 4
```

Mudah bukan? Nah berikut adalah contoh kombinasi-kombinasi lainnya.

```
rwx	= 7		r--	= 4		--x     = 1
rw-	= 6		-wx	= 3		---     = 0
r-x	= 5		-w-	= 2
```

Setelah sudah memahami bagaimana menghitung nilainya dalam 1 blok, maka berikutnya kita tinggal menghitungnya secara keseluruhan blok. Tekniknya kita tinggal menghitungnya secara per blok, baru dijajarkan secara keseluruhan. Contohnya begini :

```
rwxrwxrwx = [4+2+1] [4+2+1] [4+2+1] = 777
rwxr--r-x = [4+2+1] [4+0+0] [4+0+1] = 745
```

Ingat kuncinya adalah dihitung dulu perblok, lalu di jajarkan (tidak dijumlah lagi).

Berikut adalah contoh-contoh dari kombinasi permission secara keseluruhan :

```
rwxrwxrwx	= 777
rwxr-xr-x	= 755
rwx------	= 700	
-wx--xrw- 	= 316
```

## **Praktek Permission**

Memperbaiki Ownership pada suatu file saja tidak cukup. Terkadang kepemilikan file sudah diberikan pada user dan grup yang tepat, tetapi nyatanya user tersebut misalnya tidak bisa mengedit atau membuat file baru. Nah disinilah peran Permission. Yaitu untuk mengatur hak akses yang tepat kepada folder/file sesuai dengan Ownership yang sudah diberikan.

Format untuk mengubah permission adalah sebagai berikut :

```bash
chmod [opsi] nilai_oktal namafilenya
```

Misalnya kita mempunyai folder dengan nama latihan dengan permission sebagai berikut :

```bash
ls -l

drwxr-xr-x 2 rizal   rizal     4096 Jul 26 17:38 latihan
```

Kemudian kita ingin mengubah hak akses user pemilik menjadi read dan write saja (tanpa execute), sedangkan group dan other tidak punya hak akses apa-apa. Secara perhitungan, kebutuhan diatas nilainya akan menjadi seperti ini :

```
user = rw- = 6
grup = --- = 0
others = --- = 0
```

Sehingga sintaks yang bisa kita lakukan adalah :

```bash
chmod 600 latihan
ls -l
drw------- 2 rizal   rizal     4096 Jul 26 17:38 latihan
```

Contoh lain misal kita ingin mengubah direktori latihan dengan hak akses user pemilik full akses, untuk hak akses group diberikan read dan write saja tanpa execute, serta untuk others hanya read saja.

Secara perhitungan seharusnya menjadi seperti ini :

```
user = rwx = 7
grup = rw- = 6
others = r-- = 4
```

Sehingga sintaksnya menjadi seperti ini :

```bash
chmod 764 latihan
ls -l
drwxrw-r-- 2 rizal   rizal     4096 Jul 26 17:38 latihan
```

Gunakan opsi -R untuk merubah hak akses ownership keseluruhan dari isi direktori

```bash
chmod -R 775 latihan
# ls -l
drwxrwxr-x 2 rizal   rizal     4096 Jul 26 17:38 latihan
```

[1]:11%20Permissions%202009b8c645a04797a23c1dc2c27dcf3c/image1.png