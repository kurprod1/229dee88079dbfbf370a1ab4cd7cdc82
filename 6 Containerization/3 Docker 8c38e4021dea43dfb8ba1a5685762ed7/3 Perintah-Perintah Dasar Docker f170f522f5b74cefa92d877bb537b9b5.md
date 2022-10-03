# 3. Perintah-Perintah Dasar Docker

Created: July 4, 2022 1:25 PM

Pada bagian ini kita akan mempelajari beberapa perintah-perintah paling dasar dari Docker sebagai prinsip dasar agar kita menggunakan berbagai command Docker kedepannya.

# **Docker *Version***

Docker *version* merupakan perintah untuk mengecek versi dari Docker yang sudah terinstall. Selain itu juga untuk mengecek apakah Docker *Client* sudah dapat berkomunikasi dengan Docker Server.

Perintahnya :

```bash
docker version
```

![https://lh6.googleusercontent.com/lb2j2zef9rErQP7LX0FSsCZG5ca9ajSNErJGdIvgb0_NVeF46DAm0W_hfH5PFYULE9jfxffMW8vKlHU22TPj4f6F7eIMlTwOnkCt2rJ1Y7pt0lJ2PQyiZC3CBwQBBsZJS2meqQv9PQxIkJqNRQ](https://lh6.googleusercontent.com/lb2j2zef9rErQP7LX0FSsCZG5ca9ajSNErJGdIvgb0_NVeF46DAm0W_hfH5PFYULE9jfxffMW8vKlHU22TPj4f6F7eIMlTwOnkCt2rJ1Y7pt0lJ2PQyiZC3CBwQBBsZJS2meqQv9PQxIkJqNRQ)

# **Docker Info**

Docker info merupakan command untuk mendapatkan informasi sistem Docker secara keseluruhan. Kita bisa mendapatkan info-info seperti :

1. Ada berapa *container* yang berjalan, yang di *pause*, yang dihentikan
2. Ada berapa *image*
3. Versi server
4. *Plugin, Driver*, IP
5. dll
    
    ![https://lh5.googleusercontent.com/md_GJJgyIzXVgkrfcwnCa0us_HLZv0wk1cRl9qSGRetKi4Q86fkBhbQiq2UPW_mADzi3UX8Chcl1CYiNXv_u98i85X4XMq-HqV3rPRCWVxYWH4x3DlSxTY-yY2Zll-jIiX4fEvJ6UeisBM7v9Q](https://lh5.googleusercontent.com/md_GJJgyIzXVgkrfcwnCa0us_HLZv0wk1cRl9qSGRetKi4Q86fkBhbQiq2UPW_mADzi3UX8Chcl1CYiNXv_u98i85X4XMq-HqV3rPRCWVxYWH4x3DlSxTY-yY2Zll-jIiX4fEvJ6UeisBM7v9Q)
    

Biasanya kita menggunakan command ini ketika ingin secara sekilas melihat sistem Docker yang sedang berjalan di Server.

# **Docker *Help***

Kita tidak perlu menghapal seluruh command yang ada pada Docker karena Docker sudah menyediakan seluruh petunjuk dan bantuan pada setiap commandnya. Kita cukup membaca penjelasan dari setiap command tersebut untuk mengerti seperti apa penggunaan dan formatnya.

Perintah untuk mendapatkan bantuan dari perintah-perintah Docker adalah :

```bash
docker --help
```

atau :

```bash
docker <command> --help
```

Disana akan tampil seluruh command beserta masing-masing penjelasannya.

Selain itu jangan lupakan peran dari website Docker Docs. Seluruh penjelasan, petunjuk, konsep, dan contoh-contoh penggunaan command sudah dituliskan dengan sangat rapi oleh para pengembang Docker disana. Saat kita melakukan googling pun biasanya ujung-ujungnya diarahkan ke website tersebut. Jadi jika kita butuh bantuan, sering-sering kunjungi website ini.

# ***Docker Command Structure***

Penulisan format *command* Docker ini merupakan acuan setiap kita ingin melakukan *command* apapun kedepannya. Struktur ini berlaku universal sehingga walaupun *command*-nya berbeda-beda, biasanya strukturnya sama.

Ada 2 buah struktur command pada Docker yaitu :

**Struktur Lama**

```bash
docker <command> (options)
```

Contoh :

```bash
docker run -p 80:80 mysql
docker rm containerA
docker inspect
```

**Struktur Baru**

```bash
docker <command> <sub-command> (options)
```

Contoh :

```bash
docker container run -p 80:80 mysql
docker container rm containerA
docker container inspect
```

Pada struktur baru, setiap *command* menjadi lebih spesifik dan rapi secara tujuannya. Misal diatas kita jadi lebih tahu bahwa sesuatu yang di “run” adalah *container*. Berbeda dengan yang format penulisan lama bahwa hanya ada command “run” tapi tidak cukup jelas bahwa yang di run itu apa (bagi orang awam).

Contoh lain misal kita dapat menggunakan perintah berikut :

```bash
docker container rm testing
docker image rm testing
```

2 *command* diatas juga menunjukkan secara jelas bahwa yang ingin kita hapus adalah sebuah container dan sebuah image masing-masing bernama *testing*. Bandingkan dengan perintah hapus pada format lama seperti berikut :

```bash
docker rm testing
```

Secara kasat mata kita akan bingung bahwa “*testing*” yang dihapus diatas adalah container atau image.

Walaupun struktur penulisan yang lama masih dapat digunakan, sebaiknya kita tetap  lebih mengutamakan menggunakan penggunaan struktur command yang baru.