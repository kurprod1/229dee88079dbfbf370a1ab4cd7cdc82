# 12. Pengenalan Route53

Created: July 18, 2022 10:04 PM

# **Apa itu Route53 ?**

**Amazon Route 53** merupakan *domain name system (DNS)*. Pada dasarnya sebuah DNS menerjemahkan alamat IP Public menjadi sebuah nama domain yang dapat kita baca dan ingat dengan sangat mudah, amazon route 53 memiliki fungsi sebagai domain manager dimana layanan ini menghubungkan DNS pada layanan yang ada di AWS mencakup instance, load balancer, S3 bucket, Dan layanan lainnya.

[*Amazon Route53 Logo*](https://lh4.googleusercontent.com/oVnHvLIT0eFjzNVb6Kb4anxEh4squKizQoN7lBcq8lJsFzB7XlcvuaFUvtoI1y5CfoYW2KbdVn9yUoeUJYYoJ1xetO7l7Q4dsH1KaAwAGW7M0QUfWAQ5tilL6FEJca5MKiGcAySI9wVD1mJvag)

*Amazon Route53 Logo*

Pada layanan ini kita dapat menggunakan domain yang dapat kita beli melalui layanan Route53 ataupun menggunakan domain yang sudah kita beli pada platform lain. Kita hanya perlu mengarahkan Name Server pada Route53 pada domain yang kita beli di platform lain, sehingga domain tersebut dapat kita gunakan.

[*Ilustrasi cara kerja Route53*](https://lh4.googleusercontent.com/NKt8XQ8qRzw5ZYLJTRvQfSQ6HfXN-AX6AdllhR2uU5HkPoiU-VMcXHSkpokKMYqZYz6tx3dIXLdrDRoZycgiqXZ5qs2TuwH19qzK7VcNCargm2dEvhkfqPJEom16Op0FLfsjWbhsheBAoKfFmg)

*Ilustrasi cara kerja Route53*

Dengan begini setiap instance dan load balance yang kita buat, tidak perlu kita akses menggunakan alamat IP Public maupun DNS dynamic dari AWS. Kita hanya perlu mengarahkan layanan tersebut pada domain yang sudah kita daftarkan pada route53.

# **Praktek Route53**

## **Persiapan Domain**

Sebelum kita melakukan konfigurasi pada layanan Route53, kita harus sudah memiliki domain terlebih dahulu. Pada bagian ini kita akan coba menggunakan domain yang sudah dibeli dari provider lain dan bukan membeli dari AWS itu sendiri.

Mungkin kami akan memberikan beberapa platform yang menyediakan yang menjual domain yang diantaranya adalah berikut :

1. IDCloudhost
2. Qwords
3. Dewa Web
4. ID Hostinger
5. Pandi
6. Dll

Disini kami sendiri akan menggunakan provider IDCloudhost untuk domain yang akan kita gunakan. Kami akan memberikan sebuah akun yang dapat kalian gunakan untuk mengakses domain tersebut.

## **Konfigurasi Domain di Route53**

Pada bagian ini kita akan coba untuk melakukan konfigurasi pada Route53, disini kita akan memasukan domain yang akan kita gunakan pada layanan ini. Disini kita akan mencontohkan dengan menggunakan domain ***sdcilsy-alpha.web.id***.

Kalian dapat menyesuaikan kembali nanti dengan domain yang kalian miliki. Pertama yang harus kita lakukan adalah masuk kedalam **dashboard Route53**. Caranya adalah masuk kedalam **Services** lalu cari **Route53**.

[https://lh3.googleusercontent.com/8DhCAL1-oBTNdsiGEn70yQyid5JRMvvhHDDS8i8G4gH_nXvYoT0KxBt9PgDM6nfJJv9E-2hQWvJIq-7L01cHpgitZUNFHl8H_ny4sYc-8sLTmCop0qiVnRsyUSJ-UQP0L97uagzHBb1gNSNHvw](https://lh3.googleusercontent.com/8DhCAL1-oBTNdsiGEn70yQyid5JRMvvhHDDS8i8G4gH_nXvYoT0KxBt9PgDM6nfJJv9E-2hQWvJIq-7L01cHpgitZUNFHl8H_ny4sYc-8sLTmCop0qiVnRsyUSJ-UQP0L97uagzHBb1gNSNHvw)

Setelah masuk kedalam dashboard DNS Manager di Route53, selanjutnya kita buat sebuah **Hosted Zone** baru dengan menklik tombol **Create Hosted Zone**.

[https://lh5.googleusercontent.com/9Kpc9By5Ksf73fj7j3Ij6GM-FsvWEGVzbBRQAUiMKIR03k_DHeP3FsCR7pZQljyTJA2veNt1yscnCxfgneySWQmH2zPxqAJb7UwKUbmMOgPKTH-BxBFd4Hxp7NkXoNgtjwMbgarEwa50tDdP-g](https://lh5.googleusercontent.com/9Kpc9By5Ksf73fj7j3Ij6GM-FsvWEGVzbBRQAUiMKIR03k_DHeP3FsCR7pZQljyTJA2veNt1yscnCxfgneySWQmH2zPxqAJb7UwKUbmMOgPKTH-BxBFd4Hxp7NkXoNgtjwMbgarEwa50tDdP-g)

Setelah itu akan muncul pop-out dari samping, masukan alamat domain yang akan kita daftarkan pada route53. Disini kita akan masukan domain ***sdcilsy-alpha.web.id***. Setelah itu klik **Create** untuk menyimpan.

[https://lh4.googleusercontent.com/Jd2QpwOX-HJzW_86zuKtl1uof5DIvlYL9QOQuQQWsNFrrgJsI8vWEEenYjsCbrep4RA5zxL24Mc81P3xqD7FCcBl3WvRh37QGXrmcnuaDZMmC6csVoTYWY2Wzi8yVh4MqmTxYZHIZxbasSuwGA](https://lh4.googleusercontent.com/Jd2QpwOX-HJzW_86zuKtl1uof5DIvlYL9QOQuQQWsNFrrgJsI8vWEEenYjsCbrep4RA5zxL24Mc81P3xqD7FCcBl3WvRh37QGXrmcnuaDZMmC6csVoTYWY2Wzi8yVh4MqmTxYZHIZxbasSuwGA)

Setelah itu kita akan diarahkan kedalam hasi setting dari domain yang kita masukan barusan, disana kita akan melihat Name Server (NS) dan juga SOA dari domain tersebut.

[https://lh5.googleusercontent.com/cRmNPTaVhAWoJQbDQttgyZaSYny6MD8hdvbTGE6es-rYoOxu4egPzMHRqrYT1iVn_5IT-_lU2Fd2BaXbe8YqAA-CXyI-huHVKxixOu-BgLq15AfVRwqDXq0oaXIVY3jMW9GFhGKseJl0IbXdwA](https://lh5.googleusercontent.com/cRmNPTaVhAWoJQbDQttgyZaSYny6MD8hdvbTGE6es-rYoOxu4egPzMHRqrYT1iVn_5IT-_lU2Fd2BaXbe8YqAA-CXyI-huHVKxixOu-BgLq15AfVRwqDXq0oaXIVY3jMW9GFhGKseJl0IbXdwA)

NS ini yang nanti akan kita masukan kedalam domain yang kita miliki, agar nantinya route53 bisa mengarahkan server yang ada di AWS ke domain yang sudah kita miliki.

## **Konfigurasi Domain Provider**

Setelah kita melakukan konfigurasi pada route53, sekarang kita coba konfigurasi Name Server pada domain yang sudah kita siapkan. Disini kita menggunakan domian dari IDCloudHost untuk providernya.

Untuk masuk kedalam dashboard, pertama kita harus mengakses alamat resminya di [https://idcloudhost.com/](https://idcloudhost.com/). Setelah itu masuk kedalam webnya klik tombol **Login**.

[https://lh5.googleusercontent.com/Xnudv_bxpM7sJ1oCNq6PZVX2fDXK9TNgRYPgy7VnJ-Rmy74A8jXDr2n9d2hKi8reAriPMsFIdCefhOuBcJjgLhd9DLVr-t0TFFV2hCejcZNOjgtPv0CMFK4oRYQsLnR1L12wvBRkEF-RAEuzBQ](https://lh5.googleusercontent.com/Xnudv_bxpM7sJ1oCNq6PZVX2fDXK9TNgRYPgy7VnJ-Rmy74A8jXDr2n9d2hKi8reAriPMsFIdCefhOuBcJjgLhd9DLVr-t0TFFV2hCejcZNOjgtPv0CMFK4oRYQsLnR1L12wvBRkEF-RAEuzBQ)

Setelah itu coba login dengan menggunakan user dan password yang sudah diberikan sebelumnya. Lalu klik Login.

[https://lh4.googleusercontent.com/CzK_mg_2vWTuijP4B8jK6XIOMzQXbZP5fAaYuMy1jSiTjOpBDcKGQLelPjPpVMNGCKytOiueIwIivQXYziv5CrqIS1tgn9iCUvpd8YzaSuQXymJlS8fQ1nt06XqzNJdpr3B2JWSFk3-wUS2xBg](https://lh4.googleusercontent.com/CzK_mg_2vWTuijP4B8jK6XIOMzQXbZP5fAaYuMy1jSiTjOpBDcKGQLelPjPpVMNGCKytOiueIwIivQXYziv5CrqIS1tgn9iCUvpd8YzaSuQXymJlS8fQ1nt06XqzNJdpr3B2JWSFk3-wUS2xBg)

Kita akan diarahkan ke dashboard dari IDCloudHost tersebut, pilih menu domain agar kita masuk kedalam list domain yang kita miliki.

Setelah itu pilih domain yang akan kita set dan sudah kita masukan kedalam route53 tadi, klik tombol setting yang ada disampingnya.

[https://lh5.googleusercontent.com/e6v4_oIHBUPolivQK0Iw9RTpts-gnZLIkJuc5ffFwRCWzKo5ptvB18IQOC0q5l1lm0jyAQNEwEGT1kBJtgIrL75LOc_-K2o1t3U3VAAdI4c6eTA5vmsqJbNOvhrs1H7oS_1hRLK0bzWo5nRCYA](https://lh5.googleusercontent.com/e6v4_oIHBUPolivQK0Iw9RTpts-gnZLIkJuc5ffFwRCWzKo5ptvB18IQOC0q5l1lm0jyAQNEwEGT1kBJtgIrL75LOc_-K2o1t3U3VAAdI4c6eTA5vmsqJbNOvhrs1H7oS_1hRLK0bzWo5nRCYA)

Kita akan masuk kedalam menu setting, pilih tab NameServers, pilih use custom nameserver dan isikan NS yang sebelumnya kita dapatkan di route53 seperti dibawah ini.

[https://lh6.googleusercontent.com/DCWiTIoYPz_KsbE7mO-0Q4jdv-Pi8zYmfzDQbWKl3FhgEJoiOxQC9FN-P62VyUOcvhn5FpooTQRn-OAqp2iySW6do42tu6cOeQhYdQsVS9n794rEAPZUf-29kujNhuA-tOoLNxCtqg2ZC4mzUA](https://lh6.googleusercontent.com/DCWiTIoYPz_KsbE7mO-0Q4jdv-Pi8zYmfzDQbWKl3FhgEJoiOxQC9FN-P62VyUOcvhn5FpooTQRn-OAqp2iySW6do42tu6cOeQhYdQsVS9n794rEAPZUf-29kujNhuA-tOoLNxCtqg2ZC4mzUA)

Setelah selesai klik **save** untuk menyimpan perubahan yang telah dilakukan. Selanjutnya kita akan coba hubungkan instance yang sudah kita siapkan untuk web server agar dapat diakses oleh domain tersebut.

[https://lh5.googleusercontent.com/xKXE54BPIvHjE8Q4kAFZ6tK3BkI4XnaEjT7Uo8LppaocOa_UjryJN8wLIxSnpUxytu0MQ6OXnDD-WuUKvhxsDQa6v62bGIPAefKyTAU2aBYB9OpDnj3uXVWAgG_vn7YEzRsNipM15cNn-6gReA](https://lh5.googleusercontent.com/xKXE54BPIvHjE8Q4kAFZ6tK3BkI4XnaEjT7Uo8LppaocOa_UjryJN8wLIxSnpUxytu0MQ6OXnDD-WuUKvhxsDQa6v62bGIPAefKyTAU2aBYB9OpDnj3uXVWAgG_vn7YEzRsNipM15cNn-6gReA)

# **Integrasi Instance ke Route53**

Pada bagian ini kita akan coba untuk mengarahkan instace pada domain yang sudah kita setting tadi. Hal pertama yang harus kita lakukan adalah menyiapkan **webserver** yang sudah berjalan. Kalian dapat membuat sebuah server baru atau juga mengunakan server yang sudah ada.

Disini saya sudah menyimpkan satu buah webserver yang sudah berjalan, pilih webserver tersebut lalu salin **IP Public** yang dia miliki.

[https://lh6.googleusercontent.com/tXDom2iPNswcM1yEoB0l89baKMIiJKJBA36tO_5SSZM7OX0Li2dqYz0bFq_syi2lFKZwuAIF6W4ZCaqJ8ZsJv4Id6eZQBUKN0Jly8XlhCSNK9yYSQNGk5ERIWIC8ruQ1u1Q5xT62lwViSRxnIQ](https://lh6.googleusercontent.com/tXDom2iPNswcM1yEoB0l89baKMIiJKJBA36tO_5SSZM7OX0Li2dqYz0bFq_syi2lFKZwuAIF6W4ZCaqJ8ZsJv4Id6eZQBUKN0Jly8XlhCSNK9yYSQNGk5ERIWIC8ruQ1u1Q5xT62lwViSRxnIQ)

Setelah kita salin IP Public tersebut, selanjutnya kita masuk kembali ke dashboard Route53 yang ada di AWS. Masuk kedalam Zone domain yang sudah kita buat, klik **Create Record**.

[https://lh5.googleusercontent.com/cRmNPTaVhAWoJQbDQttgyZaSYny6MD8hdvbTGE6es-rYoOxu4egPzMHRqrYT1iVn_5IT-_lU2Fd2BaXbe8YqAA-CXyI-huHVKxixOu-BgLq15AfVRwqDXq0oaXIVY3jMW9GFhGKseJl0IbXdwA](https://lh5.googleusercontent.com/cRmNPTaVhAWoJQbDQttgyZaSYny6MD8hdvbTGE6es-rYoOxu4egPzMHRqrYT1iVn_5IT-_lU2Fd2BaXbe8YqAA-CXyI-huHVKxixOu-BgLq15AfVRwqDXq0oaXIVY3jMW9GFhGKseJl0IbXdwA)

Lalu akan kita akan diarahkan untuk mengisikan alamat **IP Public** tadi dibagian value. Setelah itu klik Tombol **Create Record** untuk menyimpan.

[https://lh3.googleusercontent.com/TwRz_xfJInCehP98l3u0aJ0r0bgxkH3JQIdaBwM95_-hbKqQMpJ21p-iuEobW1vG6zI1tlu2KByvN_RiS69-YBrfs1myZ3WhTdx2ZUmeuwvCeB24b01ePPV-3p32RGlEF0fZFV0by8wWFf56Qg](https://lh3.googleusercontent.com/TwRz_xfJInCehP98l3u0aJ0r0bgxkH3JQIdaBwM95_-hbKqQMpJ21p-iuEobW1vG6zI1tlu2KByvN_RiS69-YBrfs1myZ3WhTdx2ZUmeuwvCeB24b01ePPV-3p32RGlEF0fZFV0by8wWFf56Qg)

Setelah itu kita bisa melihat hasil yang sudah kita buat seperti dibawah ini.

[https://lh3.googleusercontent.com/E7AoQwvm6EDV408jGWFvP1CM4inGD7-D4JWVWN05mxxEJEYnQ6Ta6gr5tGRuXDUZLvr2AnovKSpXxPmss_TldC_bgJnwBGwNnI6W2uynN54vpsKYp4IlteBCQkNl07RS7ufbBqyddyfFWhqHMQ](https://lh3.googleusercontent.com/E7AoQwvm6EDV408jGWFvP1CM4inGD7-D4JWVWN05mxxEJEYnQ6Ta6gr5tGRuXDUZLvr2AnovKSpXxPmss_TldC_bgJnwBGwNnI6W2uynN54vpsKYp4IlteBCQkNl07RS7ufbBqyddyfFWhqHMQ)

Biasanya proses penerapan domain ini akan memakan waktu maksimal 24 jam, dalam waktu sekitar 1-3 menit biasanya sudah bisa langsung kita akses doamin tersebut. Tapi terkadang kita juga harus menunggu sampai 24 penuh untuk bisa mengakses alamat domainnya.

Berikut merupakan hasil domain yang sudah berhasil mengakses server aws.

[*Hasil domain Route53*](https://lh4.googleusercontent.com/-Hq6jYSyjXFBps7WcAtGFhNZCgQVrQ0F3bEJDHVggppDyzzuxdAiwQ9OELv3APgyrMIyMZkol8N3HX2PVPq5ZM--8yc4bUMJkOR7Bn_ukThnCtU0YAY1rOIhPdGBPDTnbkqC2tDA2LG5We57iQ)

*Hasil domain Route53*

# **Setup Subdomain dan Layanan AWS Lainnya**

Setelah kita berhasil membuat domain dapat diakses dan mengarahkan alamat instance, sekarang kita akan coba membuat sebuah subdomain sekaligus mengarahkannya ke salah satu load balance yang ada.

Prosesnya masih sama seperti pada saat akan membuat record pertama kali.

[https://lh6.googleusercontent.com/XYMctnKqPG_ZlSv64E4mlHdpyd7LCWxGexN48m2ZQa-thOvEMU-0pPNZlwEOaUGEPhxre_Gm5n81WmXN8pzjj568S63W4NnETpjAvrV7a2oLiahP-p0qwn_Mf-ejZwVv87OGQL1LZk1_BhHBIw](https://lh6.googleusercontent.com/XYMctnKqPG_ZlSv64E4mlHdpyd7LCWxGexN48m2ZQa-thOvEMU-0pPNZlwEOaUGEPhxre_Gm5n81WmXN8pzjj568S63W4NnETpjAvrV7a2oLiahP-p0qwn_Mf-ejZwVv87OGQL1LZk1_BhHBIw)

Pada bagian **Name** diisikan dengan subdomain yang kita inginkan. Pada bagain **Alias** pilih Yes dan pada **Alias Target** pilih Load Balance, Elastic Beanstalk, ataupun Amazon S3 yang akan kita arahkan ke subdomain agar mudah dipanggil nantinya.

[https://lh6.googleusercontent.com/YRlLe1GvfJDr-Ca2cJlTOWFc16Wr8ZhHXJm1EG44rG-Op-cPl-twjCsLOhR6rNo9mb0y9fw8xjPIS0O-au2K6acYV-5KglHaI7ypSkuUT-R0wcSEDmhDJu2dPITd0-LbGts_FJn60gBPU35n7w](https://lh6.googleusercontent.com/YRlLe1GvfJDr-Ca2cJlTOWFc16Wr8ZhHXJm1EG44rG-Op-cPl-twjCsLOhR6rNo9mb0y9fw8xjPIS0O-au2K6acYV-5KglHaI7ypSkuUT-R0wcSEDmhDJu2dPITd0-LbGts_FJn60gBPU35n7w)

Setelah kita simpan, hasilnya konfigurasinya akan terlihat seperti dibawah ini.

[https://lh4.googleusercontent.com/X_cP2aeku5n2xmIlKnnKCP_Ev9I_GgpOaqdoUjD5dKJdi33c11e6kr4sItIiP1qA3FOmwQxO0cHbkngvJdaknjGfXxZ9ecxFdsqFv9NfEdz_XbQ_lIdmSy7TbP7u1d4UzQHiCbRIUcX4ubjFQQ](https://lh4.googleusercontent.com/X_cP2aeku5n2xmIlKnnKCP_Ev9I_GgpOaqdoUjD5dKJdi33c11e6kr4sItIiP1qA3FOmwQxO0cHbkngvJdaknjGfXxZ9ecxFdsqFv9NfEdz_XbQ_lIdmSy7TbP7u1d4UzQHiCbRIUcX4ubjFQQ)

Jika kita coba akses alamat subdomain tersebut, maka akan otomatis mengarahkan pada instance yang kita miliki seperti dibawah ini.

![Untitled](12%20Pengenalan%20Route53%20a5ab919683cb4f57bc320d5e6b8b452c/Untitled.png)

Dengan begini kita sudah bisa mengarahkan server yang sudah kita siapkan sehingga bisa diakses oleh user melalui domain.