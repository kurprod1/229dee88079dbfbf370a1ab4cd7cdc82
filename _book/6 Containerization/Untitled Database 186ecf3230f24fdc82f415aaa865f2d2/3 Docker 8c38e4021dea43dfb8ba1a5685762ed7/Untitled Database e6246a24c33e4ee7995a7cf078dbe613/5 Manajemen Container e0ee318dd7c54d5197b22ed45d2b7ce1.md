# 5. Manajemen Container

Created: July 4, 2022 1:39 PM

Container merupakan komponen utama dari Docker. Kita tidak dapat mengotak-atik berbagai komponen lainnya seperti Image dan Registry selama kita belum paham terkait Container. Sehingga di bagian ini kita akan coba memahami cara kerja *Container* dengan langsung coba mempraktekkan beberapa command-commandnya.

# **Menjalankan *Container* Baru**

Untuk menjalankan sebuah container baru kita dapat menggunakan format command berikut :

```bash
$ docker container run <options> image
```

Contoh kita akan membuat sebuah Container yang berisi webserver Nginx. Maka kita bisa coba eksekusi command berikut :

```bash
$ docker container run -p 80:80 --name nginxhost nginx
```

[https://lh5.googleusercontent.com/gwQydwR9qu_TnzkTtvOoHDph8slkqY6uJ8Dvcugl_7eUqoeBXcCav747O5LCdJ73AS-Cd9SQh4039iMQ1DvnB6yhCYNyjgu5_bRSWSS7CdPcMbp-7Uty-AWXc-Lv5LYK-RYmVP_UnjXLv4FTzg](https://lh5.googleusercontent.com/gwQydwR9qu_TnzkTtvOoHDph8slkqY6uJ8Dvcugl_7eUqoeBXcCav747O5LCdJ73AS-Cd9SQh4039iMQ1DvnB6yhCYNyjgu5_bRSWSS7CdPcMbp-7Uty-AWXc-Lv5LYK-RYmVP_UnjXLv4FTzg)

Sekarang coba buka browser dan arahkan ke alamat server yang kita miliki.

[https://lh3.googleusercontent.com/WkSTY1A6AQSgPcNXkUpzc1Zv7ceYEG3DRBtqq4DZnUevGqc85j33qlu3bkq7QO0TYWCtbEJVMdqsQFnFL7hDVRO9jQf8VJc5AQdkbF5Te4uIlNvi-oBUF9Mct5zTkCnvlPGoTGUm2yElVY4Uug](https://lh3.googleusercontent.com/WkSTY1A6AQSgPcNXkUpzc1Zv7ceYEG3DRBtqq4DZnUevGqc85j33qlu3bkq7QO0TYWCtbEJVMdqsQFnFL7hDVRO9jQf8VJc5AQdkbF5Te4uIlNvi-oBUF9Mct5zTkCnvlPGoTGUm2yElVY4Uug)

Webserver NGINX sudah dapat kita akses. Artinya Container sudah berhasil berjalan dengan baik.

Sebenarnya apa proses yang terjadi ketika kita menjalankan perintah tersebut? Berikut kira-kira penjelasannya :

1. Pertama-tama Docker akan mencari image bernama nginx di *registry* local terlebih dahulu.
2. Karena *image* nginx belum ada dilokal, maka Docker akan mengambil *image* nginx dari *registry* publik yaitu Docker Hub. *Image* ini kemudian akan disimpan di lokal.
3. Sebuah *container* baru bernama nginxhost akan dijalankan menggunakan image nginx tersebut.
4. Perintah -p (*publish*) membuat *port* 80 pada *host* (komputer/mesin yang menjalankan Docker) akan di buka.
5. Seluruh traffic menuju *port* 80 dari *host* akan diarahkan ke *port* 80 pada container nginxhost.

Sebagai catatan tidak boleh ada 2 container atau lebih yang menjalankan *port* yang sama. Jadi misalnya kita menjalankan 2 buah container berisi image NGINX, maka kita bisa jalankan di 2 port yang berbeda misalnya di 8080 dan 8081.  Lalu bagaimana kalau kita ingin tetap membutuhkan menjalankan banyak container dengan port yang sama? Solusinya adalah *load* balancer.

Kita juga biasanya tidak menginginkan *Container* berjalan dalam terminal yang aktif. Karena jika kita jalankan Container dalam terminal aktif, ketika layar terminal ini kita tutup atau kita tekan CTRL + C maka container tersebut akan berhenti. Oleh karena itu kita bisa jalankan Container dengan opsi -d (detach mode) :

```bash
$ docker container run -d -p 80:80 --name nginxhost nginx
```

Lalu bagaimana kita bisa melihat container-container yang sedang berjalan dalam mode detach? Kita akan bahas pada bagian selanjutnya.

# **Melihat *Container* yang Berjalan dan Menghentikannya**

Perintah untuk melihat container yang sedang berjalan adalah :

```bash
$ docker container ls
```

Disana akan terlihat *container-container* yang saat ini sedang berjalan di host tersebut. Lalu bagaimana kita menghentikan *container* yang sedang berjalan? Kita bisa gunakan perintah berikut:

```bash
$ docker container stop <container name>
```

Contoh :

```bash
$ docker container stop nginxhost
```

[https://lh4.googleusercontent.com/MVDOz_bRawX8iDbDP0c7tzyqNMY_hw5xWKyWMiiNn-YWJ_7C6mg58Vbi5WgpLRkYwn4DTZT9PfxwvLf3Yibnp41MbK0i0WXMRpWbO5WQJKuLEIMVXeYQyXQ1f0vfJDX72mOZABNupogtBC_a9w](https://lh4.googleusercontent.com/MVDOz_bRawX8iDbDP0c7tzyqNMY_hw5xWKyWMiiNn-YWJ_7C6mg58Vbi5WgpLRkYwn4DTZT9PfxwvLf3Yibnp41MbK0i0WXMRpWbO5WQJKuLEIMVXeYQyXQ1f0vfJDX72mOZABNupogtBC_a9w)

Coba kita lihat kembali daftar *container* yang sedang berjalan menggunakan perintah :

```bash
$ docker container ls
```

Disana kita tidak akan dapat melihat *container-containe*r yang sudah pernah dihentikan. Terkadang kita tetap butuh informasi *container* yang sudah dihentikan itu apa saja agar dapat kita jalankan kembali di kemudian hari. Maka untuk melihat daftar *container* yang sudah berhenti kita bisa gunakan opsi -a seperti berikut :

```bash
$ docker container ls -a
```

# **Menjalankan *Container* yang sudah dihentikan**

Kita dapat menjalankan kembali *Container* yang sudah berhenti menggunakan perintah :

```bash
$ docker container start <container name>
```

Contoh :

```bash
$ docker container start nginxhost
```

[https://lh4.googleusercontent.com/up3PPU1S0Ie_4dmH9T0Iw83h7sOrqAlsGkymmCQNxdqrlYS43seC9sqgTQMfdxAkPCELfNm_O0HTQ8M3cFqVQ-Ukvg2wkfD8kWOZFHo3Y_Va0eTP8Q5n8BMWo1QrxVN3aSzXEOhCATvG28Sy9w](https://lh4.googleusercontent.com/up3PPU1S0Ie_4dmH9T0Iw83h7sOrqAlsGkymmCQNxdqrlYS43seC9sqgTQMfdxAkPCELfNm_O0HTQ8M3cFqVQ-Ukvg2wkfD8kWOZFHo3Y_Va0eTP8Q5n8BMWo1QrxVN3aSzXEOhCATvG28Sy9w)

Perbedaan utama dari *command* docker *container* run dengan docker *container* *start* adalah, *command* docker container run selalu membuat container baru. Sedangkan docker container *start* hanya menjalankan container yang sudah ada, namun sedang berhenti.

# **Docker *Logs* dan *Top***

Jika Anda terbiasa memantau informasi-informasi penting Server dari lognya, maka Anda dapat gunakan perintah berikut :

```bash
$ docker container logs <container name>
```

Contoh :

```bash
$ docker container logs nginxhost
```

Disana akan tampil informasi-informasi log standar tergantung layanan yang digunakan. Misalnya layanan nginx biasanya yang ditampilkan adalah log dari /var/nginx/access.log dan /var/nginx/error.log.

[https://lh3.googleusercontent.com/TSAbfM8LNFZKI-K5p3L_FBTlcYMF2M2eBYN62EPN2TEJb0H231YdiDxEG5XRpq3NDdd695BYPhEpW9dzFQdGa2h-7BsxvKD-q2eQ2FvfGjQHzFF8kHi9km6oIgMwWv9En6JmExvHBLcfTBLPKg](https://lh3.googleusercontent.com/TSAbfM8LNFZKI-K5p3L_FBTlcYMF2M2eBYN62EPN2TEJb0H231YdiDxEG5XRpq3NDdd695BYPhEpW9dzFQdGa2h-7BsxvKD-q2eQ2FvfGjQHzFF8kHi9km6oIgMwWv9En6JmExvHBLcfTBLPKg)

Kita juga dapat meliha proses apa saja yang dijalankan oleh suatu *Container* menggunakan perintah “*top*”. Ini biasa kita gunakan untuk menganalisa container mana yang misalnya memakan RAM paling besar karena terlalu banyak menjalankan proses. Perintah *top* ini sangat mirip dengan perintah top Linux pada umumnya :

```bash
$ docker container top <container name>
```

[https://lh3.googleusercontent.com/bYEfm9SdD8rpHlI7CIpUi7Og9L-Wo7ViMmSGtG2MVMS5kzc5oxc8JWnTs3JFpZM6qxO6VSd_i6scxB7QcE6rlb0j-ajRxBZfE2RnFN5tXCP2bmHXXafY7a5u-0-g7B0S5sdeZnrhoyTvcQ4vwQ](https://lh3.googleusercontent.com/bYEfm9SdD8rpHlI7CIpUi7Og9L-Wo7ViMmSGtG2MVMS5kzc5oxc8JWnTs3JFpZM6qxO6VSd_i6scxB7QcE6rlb0j-ajRxBZfE2RnFN5tXCP2bmHXXafY7a5u-0-g7B0S5sdeZnrhoyTvcQ4vwQ)

# **Menghapus *Container***

Untuk menghapus *container* kita dapat menggunakan perintah berikut :

$ docker container rm <container name>

Contoh :

$ docker container rm nginxhost

Namun perintah hapus ini tidak akan bisa digunakan pada *Container* yang sedang dalam keadaan berjalan. Kita dapat menggunakan opsi -f untuk memaksa menghapus *container* yang sedang berjalan :

$ docker container rm -f <container name>

Contoh :

$ docker container rm -f nginxhost

[https://lh6.googleusercontent.com/cEo97FKpi_htyk1lTj_Sg7gLDnDZRGtLhhv3F8dGaf6ezIczwTKPdqsKG_4hNHdOo1TJF2VZufF3I0JaCHoCsI2kamEIDdaHI9bPWrxsyqpkYDlN-evjhJkU2KXUqhD_3yMnbBXAdICl1Z0xkg](https://lh6.googleusercontent.com/cEo97FKpi_htyk1lTj_Sg7gLDnDZRGtLhhv3F8dGaf6ezIczwTKPdqsKG_4hNHdOo1TJF2VZufF3I0JaCHoCsI2kamEIDdaHI9bPWrxsyqpkYDlN-evjhJkU2KXUqhD_3yMnbBXAdICl1Z0xkg)

# ***Exercise***

**Teori**

1. Menurut Anda seperti apa proses yang terjadi jika kita menjalankan *Container* menggunakan *images* yang sudah ada di local ?

**Praktek**

1. Coba jalankan 3 buah *Container* menggunakan image yang sama yaitu : **mysql.** Tapi coba jalankan tanpa menggunakan opsi --*name*.
2. Tampilkan semua container yang sedang berjalan tersebut. Apa keanehan yang Anda temukan? Apa kesimpulan Anda?