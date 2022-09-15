# 12. Mengeksplorasi Docker Hub

Created: July 5, 2022 10:01 AM

Jika kita berbicara terkait Image maka tidak lepas dari membicarakan Registry, atau tempat penyimpanan Image. Docker Hub merupakan Public Cloud Image Registry atau tempat penyimpanan image yang terdapat di internet. Kita dapat mengunduh berbagai macam image dari Docker Hub maupun menyimpan image kita sendiri ke dalamnya.

Pada bagian ini kita akan mempelajari apa-apa saja informasi yang bisa kita dapatkan di Docker Hub dan bagaimana cara memanfaatkan Docker Hub itu sendiri selama kita menggunakan Docker kedepannya.

# **Mendaftar Docker Hub**

Hal yang pertama harus kita lakukan adalah mendaftar di Docker Hub. Karena nantinya kita akan cukup banyak mengeksplorasi isi dari web Docker hub.

Cara mendaftar Docker Hub sangat mudah. Anda cukup buka halaman web [https://hub.docker.com](https://hub.docker.com/) dan lakukan pendaftaran seperti layaknya mendaftar web biasa.

[https://lh3.googleusercontent.com/cR4aE3PPux1GtH_G_34k1AuJ2cau8MlsQpvaS2tb3prmhurxSj2L8640jPAjGUYhjOBRHOhy5sf6hmwBJWZopnd1aQlFYTlasNT9Qy-H9Ou_5C7GgLtGBdRCuP5kxElXJH7yKQk6IPKqu8ASzQ](https://lh3.googleusercontent.com/cR4aE3PPux1GtH_G_34k1AuJ2cau8MlsQpvaS2tb3prmhurxSj2L8640jPAjGUYhjOBRHOhy5sf6hmwBJWZopnd1aQlFYTlasNT9Qy-H9Ou_5C7GgLtGBdRCuP5kxElXJH7yKQk6IPKqu8ASzQ)

Setelah berhasil mendaftar, simpanlah username dan password akun Docker Hub Anda karena kita akan membutuhkannya sewaktu-waktu.

# **Bagaimana Cara Melihat Image-Image yang Bagus**

Apabila kita mencari suatu image di Docker Hub, misalnya nginx. Maka kita akan mendapatkan 40 ribu lebih image repository terkait nginx.

[*Hasil pencarian image dockerhub*](https://lh4.googleusercontent.com/6WwIS3OHhDisMGuq_ETD82vBkSj9PC4kOju0znCOKePIERhD6BHLDt5TsIhTYRGe60FtrZZ1axT3x9ZadHomXcWsr30rURwTW3KM8DceY0_TxPyO7u8JWChy_j_PmgcO5axO-o3USm35zdvmnA)

*Hasil pencarian image dockerhub*

Lalu bagaimana kita menentukan mana image yang bagus?

# ***Image Official***

Sangat disarankan untuk menggunakan image official karena memang image ini yang benar-benar dikelola secara resmi oleh perusahaan pengembangnya masing-masing. Sehingga versi-versinya dijamin yang paling baru, memiliki dokumentasi yang sangat lengkap terkait bagaimana penggunaannya, hingga memiliki Dockerfile yang sesuai standar (terkait Dockerfile akan dibahas lebih lanjut pada materi berikutnya)

Ciri image official adalah :

1. Terdapat tulisan Official dibagian samping dari nama image repositorynya.
2. Tidak memiliki awalan nama user Docker hub pada nama imagenya. Jadi hanya murni bertuliskan nginx saja atau wordpress saja atau mysql saja. Bukan seperti kuasai/nginx atau bitnami/wordpress.

[*Image official dan non-official*](https://lh3.googleusercontent.com/moWbQBvjzUN3roJoLfUsOOo_D_UiVRUAysgn9ammccW-z4BT_7b8EjabIlVTCSTlFvZhTTUh_WBQ9CRePpg02v4PS8vDyG_ApXAl0j036-1O2_YGsBxKL6XO6WF4mHcq3IA2eLhp-kducMsPqQ)

*Image official dan non-official*

# ***Image non Official yang memiliki reputasi baik***

Terkadang ada image-image non official yang lebih cocok kebutuhannya untuk kita dibanding image official. Misalnya karena ada tambahan konfigurasi atau paket lainnya yang lebih cocok untuk kita.

Namun sebaiknya kita tetap melihat bahwa image non-official yang kita gunakan memiliki 3 ciri-ciri berikut :

1. Jumlah pull dan starsnya tinggi. Karena ini membuktikan bahwa banyak user yang mengunduh image ini dan memberikan rating baik.
2. Dokumentasinya lengkap. Cobalah untuk meng-klik salah satu image repository yang ada, disana nanti akan tampil dokumentasi penggunaan dari image tersebut. Jika lengkap dan mudah dimengerti, bisa diartikan bahwa user yang mengupload image ini “sangat niat” dan “bertanggung jawab”.
3. Pengembangnya masih aktif. Dapat Anda cek juga jika Anda meng-klik tab “Most Popular” lalu “Recently Update”. Jika cukup baru, maka dapat diartikan pengembang ini masih aktif mengelola image ini.

[*Jumlah Downloads & Stars Tinggi*](https://lh3.googleusercontent.com/OjVVaSUJRr5So32SbZ8tbpkxk4zVRmK9R4QhrOxEmkpS9Hc8oq_NZ8qIFl7-OgR3dmk1Z0w-viT_SCzqJ3FuXCi3vp-e5dcSLx463vyvT-lyIK_tC3KRr_Hhfs8iE4q-bNK_oL0N_WMW4TD-ZA)

*Jumlah Downloads & Stars Tinggi*

[*Dokumentasi Lengkap dan jelas*](https://lh3.googleusercontent.com/djpQ92IbZuPfHU9-c_IVxgGkJSgP2ek0q4QznQqbVOKUwY5gOyRpj4FaS6ErCkMzwrNdjuiyIZnQv4j1petZziwern5NvWTfDFkecz43tgXm16iO1-8JbEeE6hwYwc5ZfEeKMTDGJCS6tvARiQ)

*Dokumentasi Lengkap dan jelas*

[*Image yang cukup update*](https://lh4.googleusercontent.com/ZCe5S4WNnomNXMujJ1i6HdMTnMcm1U9S_KacdAKqkVta4g0Rqutvm35Wdr-EL2Bd2HEJz5CfRWvdqLM7LRyx_Ok7kn3yemxqyBNXL4HVUAuGO5pJxvJp52ag1Rd7h1IqYtV4gtTqJay9hh7Q3Q)

*Image yang cukup update*

# **Bagaimana Cara Mengunduh Berbagai Macam Image**

Di bagian ini kita akan sedikit mempraktekkan bagaiman cara untuk mengunduh berbagai image berdasarkan hasil pencarian kita di Docker Hub. Karena pada prakteknya nanti, kita akan sering melakukan pencarian di google maupun di Docker Hub untuk mengetahui informasi image yang akan kita gunakan. Nama imagenya, versinya, tagnya apa, sebaiknya gunakan image yang mana dll. Setelah sudah kita tentukan akan menggunakan yang mana, barulah kita aplikasikan ke dalam command-command Docker.

## ***Melihat List Image Yang Ada di Local***

Image-image yang kita sudah kita unduh/pull dari Docker Hub akan tersimpan di local Host kita. Kita dapat melihatnya dengan perintah berikut :

```bash
$ docker image ls
```

[https://lh3.googleusercontent.com/JqzJ99XAkd8jY9ldnlldFmNrB0iN6pHYlyMq9-t8oKjj7tv2s9aOBAZHB-kUW7G05wLsLWkajRASbilZZM1mQD0hqjXLxyCJInbFJUp5axwJahIbJZdnJ-oB3uZHqU0Ninz2cEU-Hr5UVq92Iw](https://lh3.googleusercontent.com/JqzJ99XAkd8jY9ldnlldFmNrB0iN6pHYlyMq9-t8oKjj7tv2s9aOBAZHB-kUW7G05wLsLWkajRASbilZZM1mQD0hqjXLxyCJInbFJUp5axwJahIbJZdnJ-oB3uZHqU0Ninz2cEU-Hr5UVq92Iw)

Informasi yang bisa kita dapatkan dari perintah ini diantaranya nama imagenya apa, tag nya apa, image ID nya, serta ukuran dari image ini berapa. Hal ini akan kita gali berikutnya. Sementara disini kita cukup mengetahui bahwa perintah diatas dapat menampilkan daftar image yang tersimpan di local Host kita.

# ***Image ID vs Tag***

Untuk memahami hal ini, kita coba praktekkan saja. Pertama-tama kita lihat beberapa tag yang dapat digunakan pada image nginx official (Anda dapat akses ini pada bagian Full Description pada Image di Docker Hub) :

Semua tag tersebut dapat digunakan dengan format berikut :

[https://lh3.googleusercontent.com/BHhtG-ruB0QikoUDdz27oGVkG65NMGEPZ4s1LtjhJmWxrlY7TjHAxgbxBoRisYBEqXa_xzRSQdzgmwk8NdpqvhbyZiOaFBpGaY_b5tv7MXbkrmDnj6-w9wAiaS-MO2VSSr4roW4SRhxokdKycw](https://lh3.googleusercontent.com/BHhtG-ruB0QikoUDdz27oGVkG65NMGEPZ4s1LtjhJmWxrlY7TjHAxgbxBoRisYBEqXa_xzRSQdzgmwk8NdpqvhbyZiOaFBpGaY_b5tv7MXbkrmDnj6-w9wAiaS-MO2VSSr4roW4SRhxokdKycw)

```bash
$ docker image pull nginx:<tag>
```

Contoh :

```bash
$ docker image pull nginx:1.15
$ docker image pull nginx:1.15.4
$ docker image pull nginx
```

Sekarang coba lihat lagi apa yang terjadi setelah kita mengunduh 3 image tersebut :

```bash
$ docker image ls
```

[https://lh6.googleusercontent.com/tAzHDcLCrZZk5XAR5HCdICovFf-Fal-zSCzGt867YRrLs7L_3Akqqd_OojxDg6Q9jZ0LHy4tc4E9be0WsVafm6pKDPu43atF27yEkm-9IDrn0ouWP449amvND7AB3K5Fiv4d2TXbzcRSGII_BA](https://lh6.googleusercontent.com/tAzHDcLCrZZk5XAR5HCdICovFf-Fal-zSCzGt867YRrLs7L_3Akqqd_OojxDg6Q9jZ0LHy4tc4E9be0WsVafm6pKDPu43atF27yEkm-9IDrn0ouWP449amvND7AB3K5Fiv4d2TXbzcRSGII_BA)

Kita bisa melihat bahwa image nginx memiliki 3 buah tag yang berbeda namun memiliki Image ID dan ukuran yang sama. Kenapa hal ini bisa terjadi?

Ini diakibatkan karena ketiga buah tag tersebut sebenarnya merujuk ke image yang sama, sehingga hanya memiliki 1 buah image ID saja. Sehingga bisa disimpulkan bahwa image ID merupakan identitas unik dari suatu image, sedangkan tag hanyalah rujukan kepada suatu image ID.

Tag dapat lebih memudahkan kita untuk menentukan tujuan penggunaan dari suatu versi image. Contohnya pada image nginx terdapat tag stable dan tag latest. Walaupun pada tag stable versi nginx lebih lama dibanding tag latest, namun dari sini kita bisa mengetahui bahwa kita jika kita ingin menggunakan versi nginx yang lebih stable maka kita menggunakan nginx versi 1.14, namun jika ingin versi nginx yang lebih baru maka kita akan mendapatkan nginx versi 1.15.

# ***Efisiensi Penyimpanan Image***

Kita coba lihat kembali gambar berikut :

[https://lh6.googleusercontent.com/tAzHDcLCrZZk5XAR5HCdICovFf-Fal-zSCzGt867YRrLs7L_3Akqqd_OojxDg6Q9jZ0LHy4tc4E9be0WsVafm6pKDPu43atF27yEkm-9IDrn0ouWP449amvND7AB3K5Fiv4d2TXbzcRSGII_BA](https://lh6.googleusercontent.com/tAzHDcLCrZZk5XAR5HCdICovFf-Fal-zSCzGt867YRrLs7L_3Akqqd_OojxDg6Q9jZ0LHy4tc4E9be0WsVafm6pKDPu43atF27yEkm-9IDrn0ouWP449amvND7AB3K5Fiv4d2TXbzcRSGII_BA)

Sekilas pada gambar tersebut terlihat bahwa kita seperti menyimpan 3 buah image dengan tag yang berbeda dengan masing-masing berukuran 109MB. Sehingga total yang tersimpan di local Host kita adalah 300MB.

Pada kenyatannya tidak. Berhubung ketiga buah image tersebut merujuk pada image ID yang sama, maka sebenarnya yang disimpan pada local hanyalah 1 file saja, yaitu sebesar 109MB.

Hal ini bisa terjadi karena prinsip layer pada image yang akan kita bahas lebih detail berikutnya.

# ***Latest Tidaklah Selalu “latest”***

Sebagai catatan bahwa Tag Latest itu tidak selalu menunjukkan versi terbaru dari suatu image. Melainkan lebih cocok menunjukkan versi “default” dari image tersebut. Versi default ketika kita tidak memberikan tag pada saat melakukan pull/push images.

Namun pada kebanyakan kasus, khususnya pada image-image yang dikelola secara rutin seperti image-image official, Latest memang merujuk pada versi terbaru pada image tersebut.