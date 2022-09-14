# 6. Menggambar dan Membaca Topologi

Created: August 15, 2022 11:45 AM

# **Kenapa harus bisa menggambar dan membaca Topologi?**

Pada sub-sub bab sebelumnya kita sudah mempelajari 3 komponen penting dalam ilmu jaringan, yaitu :

1. Topologi
2. Perangkat jaringan
3. IP Address

Ketiga komponen penting ini, pada prakteknya akan sangat sering dituangkan dalam bentuk gambar. Tujuannya agar lebih mudah dipahami oleh semua orang, baik oleh kita sendiri maupun oleh tim bahwa sebenarnya jaringan yang kita bangun ini seperti apa wujudnya. Ada berapa server yang digunakan, masing-masing server terhubung kemana, berapa ip masing-masing server, kalau ingin ke internet modemnya ada dimana, hingga berapa IP Address dari modem. Semua informasi ini harus bisa kita dapatkan dari gambar topologi ini.

Ibaratnya seperti seorang arsitek yang ingin membangun rumah, arsitek tersebut harus mempunyai sketsa denah rumahnya terlebih dahulu. Agar semua orang tahu bahwa berapa jumlah kamar di rumah tersebut, luas ruangannya, dll.

Gambar Topologi ini sebagai blue print yang harus bisa dipahami dan dibuat oleh setiap orang jaringan, termasuk DevOps Engineer.

# **Praktek menggambar topologi**

Agar lebih mudah, kita coba langsung praktekkan dalam bentuk contoh-contoh.

Contoh 1

[*Praktek menggambar topologi 1*](https://lh6.googleusercontent.com/Z9j89nDYGmyxAEiiCKg0j1SYS5imY2kTukcUQxyfjapxdQdCxUzZdL3crkTU8NFBIV7_7XJq7FMB6ZCsi5S8PnUS-6CO5sEGs8g9PTdVTUDyf8u-NgGfGQiqTrFgBV_BdIvzzCmC0XS5ly2jKM7UxQ)

*Praktek menggambar topologi 1*

Gambar tersebut menunjukkan bahwa ada 2 buah komputer yang saling terhubung, dimana PC A memiliki IP Address 192.168.1.1 dan PC B memiliki IP Address 192.168.1.2.

Contoh 2

[*Praktek menggambar topologi 2*](https://lh5.googleusercontent.com/hz71HSASOnRxoJgzfrhTGTLA5im5HyxHRn8KT7MSTf-tm7PvazX9OfJJDiG0txIi8sWeeux790_L7sFYBd8yuhkT1mm36139XkEJe0Z14mNOCsQoB8ksPJoO0HEvp5hLkPYsJVzHIKSZzDMunstuAQ)

*Praktek menggambar topologi 2*

Pada gambar diatas menunjukkan sebuah jaringan LAN sederhana yang terhubung ke internet melalui perangkat Modem.  Dimana PC A menggunakan IP Address 192.168.1.2, PC B menggunakan IP Address 192.168.1.3 dan modem mempunyai 2 buah interface yang masing-masing memiliki IP Private dan IP Publik. IP Private yang berada pada interface ether1 adalah 192.168.1.1 dan ip publik pada interface fo1 adalah 110.90.85.21.

Contoh 3

[*Praktek menggambar topologi 3*](https://lh4.googleusercontent.com/G7gDCfU0XGixyM1MrrRbqG10n7bbWrE3nJS4Y5nkB5SQll6Gp8UgltttYHHMTA4pTjFuRgSMz_wIZtmUSiCInh_bSA4fH5zm_xcglFhXF6iHAO7Qd3ezBsiBhTaYhH7kTCP18SDqKr3CTMnKsJkbfA)

*Praktek menggambar topologi 3*

Diatas adalah contoh topologi server-server yang dikelola oleh seorang DevOps di perusahaan A. Dimana masing-masing server memiliki IP Publik, yaitu Server Staging di ip 202.130.100.250, Server Production di 202.130.100.253, Server Test di 202.130.100.251, dan Server Dev di 202.130.100.252. Karena memiliki IP Publik maka Server-server ini bisa diakses melalui internet. Namun agar tetap aman, diantara Server dengan jaringan Internet tetap diberikan Router sebagai pengatur lalu lintas jaringan dan pengamanan. IP Router pada interface ether1 adalah 202.130.100.249, dan pada ether2 adalah 89.90.81.10.