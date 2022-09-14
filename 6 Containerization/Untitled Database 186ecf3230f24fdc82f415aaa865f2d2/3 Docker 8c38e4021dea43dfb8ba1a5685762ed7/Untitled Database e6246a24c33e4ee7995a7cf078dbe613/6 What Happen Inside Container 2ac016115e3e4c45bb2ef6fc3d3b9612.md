# 6. What Happen Inside Container?

Created: July 4, 2022 1:42 PM

Pada materi sebelumnya kita sudah sempat menyinggung terkait apa sebenarnya yang terjadi ketika perintah Docker run dijalankan. Disini kita akan coba ulas sedikit lebih dalam terkait hal tersebut.

Saat perintah Docker run di eksekusi, sebenarnya cukup banyak hal yang terjadi di balik layar. Bukan hanya semata-mata jalankan Container, lalu selesai.

Contohnya kita coba jalankan sebuah container dengan perintah berikut :

```bash
$ docker container run -d -p 80:80 --name httpdhost httpd
```

Maka yang terjadi adalah :

1. Pertama-tama Docker akan mencari image bernama httpd di *registry* local terlebih dahulu.
2. Karena image httpd belum ada di lokal, maka Docker akan mengambil *image* httpd dari *registry* publik yaitu Docker Hub. Jika kita tidak menentukan versi spesifik dari image yang ingin kita ambil, maka secara *default* Docker akan mengambil *image* dengan tag “*latest*”. Kita dapat tentukan versi tertentu misalnya httpd:1.11.1.
3. Sebuah *container* baru bernama httpdhost akan dijalankan menggunakan *image* httpd tersebut.
4. *Virtual* IP dan *private* *network* akan dipasang pada *Container* tersebut.
5. Perintah -p (*publish*) membuat *port* 8080 pada *host* akan di buka.
6. Seluruh *traffic* menuju *port* 8080 dari host akan diarahkan ke port 80 pada *container* httpdhost.
7. Container akan dijalankan menggunakan *command* utama yang sudah di tentukan pada Dockerfile (ini akan kita bahas pada materi berikutnya)

Dari banyaknya proses ini, kita dapat memodifikasi perintah docker *run* berdasarkan kebutuhan :

```bash
$ docker container run -d -p 8080:80 --name httpdhost httpd:2.4.35 httpd -e debug
```

Misalnya pada perintah diatas kita mengubah port host yang awalnya 80 menjadi 8080, mengubah versi *image* httpd menjadi 2.4.35 dan menggunakan *Command* *custom* berupa “httpd -e debug” dimana command ini merupakan command untuk menjalankan webserver httpd dengan *mode* *log* *debug*.

Berikut adalah hasilnya, dimana *log* dari *container* ini yang biasanya hanya sedikit, menjadi sangat lengkap karena kita menjalankannya dengan *mode* *debug* :

Kita juga bisa melakukan berbagai variasi dan perubahan lain selama masih memenuhi standard struktur *command* dari docker *container* *run* yaitu :

```bash
$ docker container run [OPTIONS] IMAGE [COMMAND] [ARG…]
```

Misal kita bisa menghubungkan container kita dengan *private* network bernama net-kuasai, atau menentukan agar IP dari container ini adalah 172.16.0.100, dll. Itu semua bisa dilakukan.

Disini mungkin Anda masih cukup bingung, namun yang pasti semua proses diatas akan kita kupas satu persatu selama berjalannya kelas. Sehingga di akhir, semuanya baru menjadi masuk akal bagi Anda.