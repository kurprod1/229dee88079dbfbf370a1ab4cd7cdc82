# 9. Commands Execution Container

Created: July 4, 2022 1:46 PM

Jika anda sudah terbiasa mengelola server, maka anda pasti sering menggunakan fasilitas *remote* *server* seperti SSH untuk bisa masuk ke dalam server. Dengan *Container*, anda bahkan tidak perlu melakukan itu. Kita bisa masuk langsung ke dalam *Shell* *Container* memanfaatkan mode interaktif.

# **Menjalankan Container dengan mode Interaktif**

Perintahnya adalah sebagai berikut :

```bash
$ docker container run -it nginx bash
```

Diatas adalah contohnya kita menjalankan container menggunakan image nginx secara mode interaktif dengan *shell Bash.* Hasilnya Anda akan mendapatkan shell seperti berikut :

```bash
root@3642bcc47543:/$
```

Jika sudah didalam *shell* *container* seperti ini, maka semua command yang kita lakukan akan terjadi di dalam *container* tersebut, bukan pada Host.

Contohnya disini kita bisa mengeksekusi perintah **cat /etc/nginx/nginx.conf** untuk melihat isi dari konfigurasi NGINX kita :

```bash
root@3642bcc47543:/$ cat /etc/nginx/nginx.conf
```

Bahkan kita dapat melakukan instalasi paket tambahan seperti nano :

[https://lh6.googleusercontent.com/tFa-6rG-2WrGkXs3wmP3WRNAFCwTERUo_KMfOAQuxHVOaQIgJUCbSKMv73CXOdftM4ms7NtFUDICsEvKlTIehv-l7OgwbiLpGLoLuHSmCvMMq3WpAcDhfHV5_CHXgT1Y-B1hRNc_7914-2yK2g](https://lh6.googleusercontent.com/tFa-6rG-2WrGkXs3wmP3WRNAFCwTERUo_KMfOAQuxHVOaQIgJUCbSKMv73CXOdftM4ms7NtFUDICsEvKlTIehv-l7OgwbiLpGLoLuHSmCvMMq3WpAcDhfHV5_CHXgT1Y-B1hRNc_7914-2yK2g)

```bash
root@3642bcc47543:/$ apt-get update && apt-get install nano
root@3642bcc47543:/$ nano /etc/nginx/nginx.conf
```

Jika sudah selesai, Anda dapat mengetikkan exit untuk keluar dari *Shell*. Sayangnya jika kita sudah keluar dari *Shell* seperti ini, maka *container* otomatis akan dihentikan.

# **Docker Exec**

Lalu bagaimana agar *Container* tetap berjalan dan kita tetap bisa masuk ke dalam Shell ? Pertama-tama kita perlu untuk menjalankan *Container* seperti biasa dengan mode detach.

```bash
$ docker container run -d -p 80:80 --name nginx nginx
```

Container nginx ini sama sekali tidak memiliki mode interaktif bukan? Namun kita tetap bisa masuk ke dalamnya menggunakan command Exec. Berikut adalah contohnya :

```bash
$ docker container exec -it nginx bash
```

Maka kita akan masuk ke dalam *shell* *mode* interaktif, sama seperti yang kita bahas sebelumnya. Saat kita exit dari shell pun *container* tetap akan berjalan, karena Docker Exec ini sifatnya hanya sebagai proses tambahan bukan proses utama dari Containernya itu sendiri.