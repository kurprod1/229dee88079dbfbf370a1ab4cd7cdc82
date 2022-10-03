# 7. Routing

Created: August 15, 2022 11:48 AM

# **Apa itu Routing ?**

Sebelumnya kita sudah mempelajari bahwa beberapa Host/Komputer yang tidak tergabung kedalam satu jaringan/subnet yang sama, maka tidak akan bisa berkomunikasi kecuali adanya perangkat Router. Nah perangkat Router ini sebenarnya melakukan teknik Routing untuk bisa menghubungkan komputer/host yang berbeda jaringan tersebut.

Sehingga bisa dibilang bahwa Routing merupakan proses untuk memilih jalur yang harus dilalui oleh sebuah komputer/hosts untuk menuju jaringan/subnet lain.

![*Ilustrasi Routing*](https://lh3.googleusercontent.com/u7vj9oYuUOb05ON9SaCB0hqgpEy_3vbhvQneHBRR0FgnWGzVvGwZRzHgTSMDlCH0z6H6UPH9oOnM4SF5-n0ZbMYK2xoDv7iqz9hvNl0X64HNHHF0-yI-PWkKlZoby56Fhlcn0btfKS7pO2uhgRpnPQ)

*Ilustrasi Routing*

Ini seperti layaknya kita memilih jalur terbaik dari serangkaian jalur yang ada saat bepergian keluar kota. Misalnya kita ingin pergi ke Bandung, maka sebaiknya kita harus lewat Cikampek terlebih dahulu atau lewat mana terlebih dahulu.

# **Jenis Routing**

## ***Direct Routing***

Ini adalah jenis Routing dimana data dikirimkan dari satu perangkat ke perangkat lain secara langsung (host berada pada jaringan fisik yang sama). Sehingga tidak perlu melalui perantara perangkat lain atau gateway. Tips sederhananya adalah, jika kita melihat pada gambar dibawah, maka yang tergolong sebagai Direct Routing adalah jaringan/Subnet yang terhubung langsung dengan kaki-kaki perangkat tersebut. Misalnya pada gambar dibawah, yang tergolong sebagai Direct Routing bagi Router A adalah jaringan/Subnet 192.168.0.0/24 (terhubung dengan kaki ether0) dan 192.168.1.0/24 (terhubung dengan kaki ether1), sedangkan  192.168.2.0/24 tidak.

![*Ilustrasi Direct dan Indirect Routing*](https://lh6.googleusercontent.com/QEin518WcCBo1ZR9mWOOHtVxlRINGb3CEW2uq_WSMg2i6Gfn_p9sTHEs8SMEaz67Bif37EbPiiNLF221d92hvXRX687XYL1EmiwaD7DSEipnWDUjtogSqABcFHPMcs5z9kW9y7xR_M-7EkrfQIWPKg)

*Ilustrasi Direct dan Indirect Routing*

## ***Indirect Routing***

Sedangkan ini adalah jenis Routing dimana data dikirimkan dari suatu perangkat ke perangkat yang lain yang tidak terhubung langsung (berbeda jaringan/subnet) sehingga data akan melewati satu atau lebih gateway atau network yang lain sebelum sampai ke perangkat yang dituju. Kuncinya adalah ketika ada jaringan/subnet yang tidak terhubung langsung dengan kaki-kaki perangkat tersebut, maka tergolong sebagai Indirect Routing. Jika kita melihat lagi gambar pada bagian Direct Routing, maka bagi Router A jaringan/subnet 192.168.2.0/24 lah yang termasuk sebagai Indirect Routing.

# **Teknik/Metode Routing**

Terdapat teknik/metode routing yang terbagi kedalam tiga bagian, yaitu sebagai berikut :

## ***Static Routing***

Static Routing adalah teknik untuk melakukan Routing dimana kita sebagai Administrator jaringan yang secara manual menambahkan konfigurasi-konfigurasi routing pada setiap Router.

Routing statis memiliki kentungan-keuntungan berikut :

1. Pengunaan resource hardware yang lebih ringan. Sehingga Router tidak akan terbebani.
2. Lebih hemat bandwidth, karena antar Router tidak ada yang saling mengirimkan data traffic pertukaran informasi Routing satu sama lain.
3. Routing statis menambah keamanan, karena administrator dapat memilih untuk mengisikan akses routing ke jaringan tertentu saja.

Routing statis memiliki kerugian-kerugian berikut :

1. Administrator harus benar-benar memahami internet dan bagaimana setiap router dihubungkan untuk dapat mengonfigurasikan router dengan benar.
2. Routing statis tidak sesuai untuk network – network yang besar karena akan sangat kompleks dan serba manual. Tingkat kesalahan akan sangat tinggi.

## ***Dynamic Routing***

Dynamic Routing adalah teknik untuk melakukan Routing secara otomatis dan dinamis. Router akan saling mengupdate informasi Routing tanpa campur tangan Administrator jaringan.

![https://lh4.googleusercontent.com/Ix9jrOL-KX7aWZ1g3rcj02bmjdekAVB9eg8vqyh3rcQ5CjRJKIQPrncmpzqA6yF8zpOWxTpI2pvzyX1sk661_dJlUEjsb1w_SPuy7qnF9iC4fvJ7awMiWffuibQ9S7qYm6mA_JsUpYV8EIAttiso1A](https://lh4.googleusercontent.com/Ix9jrOL-KX7aWZ1g3rcj02bmjdekAVB9eg8vqyh3rcQ5CjRJKIQPrncmpzqA6yF8zpOWxTpI2pvzyX1sk661_dJlUEjsb1w_SPuy7qnF9iC4fvJ7awMiWffuibQ9S7qYm6mA_JsUpYV8EIAttiso1A)

*Ilustrasi Routing Dinamis*

Routing dinamis memiliki kentungan-keuntungan berikut :

1. Administrator jaringan menjadi tidak perlu ikut campur dalam melakukan konfigurasi-konfigurasi routing, sehingga lebih meringankan pekerjaan.
2. Sangat dinamis dan sangat cocok digunakan pada jaringan yang besar dan kompleks.

Routing Dinamis memiliki kerugian-kerugian berikut :

1. Penggunaan resource Router yang cukup besar. Sehingga biasanya diperlukan Router-router dengan spesifikasinya tinggi.
2. Lebih boros bandwidth, karena adanya traffic-traffic pertukaran informasi tabel routing yang berlalu lalang di jaringan.

Dalam menentukan pertukaran informasi Routing, maka Router memasukkan dan mengupdate informasi-informasi tersebut kedalam tabel bernama Tabel Routing. Isi dari Tabel Routing ini kira-kira berisi informasi “Kita mau kemana? Dan untuk menuju kesana, jalur mana yang terbaik untuk kita lewati?”. Kita akan lebih bahas lebih dalam terkait Tabel Routing ini pada bagian selanjutnya.

Routing dinamis memiliki beberapa protokol Routing diantaranya :

1. RIP : Routing protokol ini memilih jalur terbaik berdasarkan banyaknya jumlah lompatan gateway. Semakin sedikit lompatannya, maka dianggap makin baik.
2. OSPF : Routing protokol ini memilih jalur terbaik berdasarkan seberapa besarnya bandwidth jalur tersebut. Semakin besar bandwidthnya maka dianggap semakin baik. Bisa jadi OSPF memilih jalur yang lompatannya lebih banyak, jika dianggap jalur tersebut memiliki bandwidth yang lebih besar.
3. EIGRP, protokol ini menentukan jalur terbaik mirip seperti OSPF, namun bedanya EIGRP juga menentukan unsur delay pada penilaiannya. Jadi selain besar bandwidthnya, jalur tersebut apakah memiliki delay yang besar atau tidak. Sehingga bisa jadi EIGRP akan memilih jalur yang lebih jauh dan lebih kecil bandwidthnya jika dianggap jalur tersebut delaynya lebih kecil.

## ***Default Routing/Default Gateway***

Default Routing/Default Gateway adalah istilah untuk jalur menuju jaringan lain yang dijadikan 1 acuan terakhir jika jalur-jalur lain sudah habis. Misalnya komputer A jika ingin menuju komputer B bisa lewat Router A dan Router B, namun jika jalur Router A dan Router B ini down, maka satu-satunya jalur terakhir adalah melalui Router C. Nah jalur melalui Router C ini lah yang disebut sebagai Default Routing/Default Gateway.

Atau bisa jadi ketika memang tidak ada jalur lain, hanya ada satu-satunya jalur yang tersedia. Maka satu-satunya jalur tersebut juga disebut sebagai Default Routing/Default Gateway.

# **Mengenal Tabel Routing**

Dalam menentukan jalur rute-rute jaringan yang dituju, Router membaca informasi-informasi dan seluruh konfigurasi yang dituliskan pada Tabel Routing. Pada Routing Statis, Tabel Routing inilah yang harus diisi dan di update secara manual oleh Administrator. Sedangkan pada Routing Dinamis, informasi pada tabel routing ini yang dipertukarkan oleh antar Router di jaringan.

Tabel Routing pada umumnya berisi informasi tentang:

- Alamat-alamat Network Tujuan
- Interface Router/jalur gateway mana saja sebagai jalur untuk mencapai network tujuan.
- Metric, sebuah nilai parameter untuk menentukan jalur mana yang terbaik untuk mencapai network tujuan. Bisa dari kualitas kecepatan medianya (fiber optic atau bukan), bisa dari banyak atau tidak lompatan gatewaynya, dll tergantung dari protokol routing yang digunakan. Misalnya jika menggunakan protokol routing RIP, maka metric ini akan berisi nilai-nilai terkait lompatan gatewaynya.

Konsep pengisian tabel routing ini sebenarnya sangat sederhana. Pada masing-masing perangkat jaringan harus mengisi tabel routing mereka dengan informasi-informasi yang memiliki format : **MAU KEMANA** dan harus **LEWAT MANA**  selengkap mungkin. Kita coba lihat pada gambar dibawah :

![*Belajar tabel routing 1*](https://lh6.googleusercontent.com/Ben5NySotvV_GWpweDe1f6u_vjX58PHO_nfzSjB1IC9_wYAzPz0xpjCU90jO-wq-GImFohBmsuomWioZvgVCcseL82zCLsd6KeRmd_wTJ19kwAkLWXKo7ZWcaZS2ibOeuOG7KsUIUsINHK9zmIGBjg)

*Belajar tabel routing 1*

Mau Kemana ini merujuk pada alamat Network Address tujuan. Misalnya pada gambar diatas ada Network 192.168.0.0/24, 192.168.1.0/24, dan 192.168.2.0/24. Setiap perangkat harus menentukan untuk menuju Network ini harus lewat mana berdasarkan sudut pandang perangkat itu masing-masing.

Misalnya PC A kalau mau ke 192.168.0.0/24 harus lewat mana, sedangkan Router A kalau mau ke 192.168.0.0/24 lewat mana, Router B kalau mau ke 192.168.0.0/24 lewat mana, dst.

Sedangkan Lewat Mana, merujuk pada interface yang terhubung atau IP Address perangkat tetangga yang terdekat. Misalnya jika sudut pandang kita ada pada Router A, maka jika ingin menuju Network Address 192.168.0.0/24 harus lewat interface ether1, karena Network tersebut memang langsung terhubung dengan interface si Router A itu sendiri. Ini yang disebut Direct Routing yang sebelumnya sudah kita bahas, yaitu routing yang langsung terkoneksi dengan perangkat itu sendiri.

Beda lagi jika Router A ingin menuju Network Address 192.168.2.0/24 yang tidak terhubung langsung. Maka Router A harus lewat IP Address perangkat tetangga yang terdekat, yaitu IP Address ether1 dari Router B, 192.168.1.2. Ini yang disebut sebagai Indirect Routing, yaitu routing yang harus melewati perangkat lain terlebih dahulu.

Agar lebih paham, kita coba isi tabel routing dari masing-masing perangkat :

PC A

|Mau Ke Mana|Lewat Mana      |
|-----------|----------------|
|192.168.0.0/24|Lan-ethernet (Direct)|
|192.168.1.0/24|192.168.0.1 (Indirect)|
|192.168.2.0/24|192.168.0.1 (Indirect)|

Router A

|Mau Ke Mana|Lewat Mana      |
|-----------|----------------|
|192.168.0.0/24|ether1 (Direct) |
|192.168.1.0/24|ether2 (Direct) |
|192.168.2.0/24|192.168.1.2 (Indirect)|

Router B

|Mau Ke Mana|Lewat Mana      |
|-----------|----------------|
|192.168.0.0/24|192.168.1.1 (Indirect)|
|192.168.1.0/24|ether2 (Direct) |
|192.168.2.0/24|ether1 (Direct) |

PC B

|Mau Ke Mana|Lewat Mana      |
|-----------|----------------|
|192.168.0.0/24|192.168.2.1 (Indirect)|
|192.168.1.0/24|192.168.2.1 (Indirect)|
|192.168.2.0/24|Lan-ethernet (Direct)|

Tips agar mengerti routing ini adalah, benar-benar coba teliti dari gambar. Network yang menempel langsung dengan perangkat, maka itu sudah pasti Direct Routing, selain itu maka termasuk Indirect Routing. Untuk menentukan Lewat Mana dari Indirect routing ini, kita tinggal cari IP Address dari perangkat sebelah/tetangga yang terdekat.

# **Praktek Routing Dasar**

Disini kita akan coba lebih membiasakan kembali bagaimana cara memahami konsep dasar pengaplikasian routing dari sebuah gambar topologi. Hal ini agar ketika nantinya kita dihadapkan dengan  kasus nyata di lapangan, kita bisa mengetahui bagaimana alur dan cara menghubungkan antar perangkat jaringan menggunakan routing.

Contoh 1

![*Praktek Routing 1*](https://lh4.googleusercontent.com/GlWq0cK-Hy71gZRDSZcelmcsPMZO9lI3_xwb1lluYCvEDnM46xLjO6B4Kfs0xrI-jfcxEfXh19amcjWepsd_1COJgGSHimbYMSTzA3bMIEdky0M9nDGy1mVGSKDbmr32nG5bTlvoRxn5eZM5v52_Mw)

*Praktek Routing 1*

Bagaimanakah routing dari seluruh perangkat agar bisa saling terkoneksi?

Jawaban :

PC A

Mau Ke Mana,Lewat Mana
172.16.0.0/24,Lan-ethernet
0.0.0.0/0,172.16.0.1

PC B

|Mau Ke Mana|Lewat Mana      |
|-----------|----------------|
|172.16.1.0/24|Lan-ethernet    |
|0.0.0.0/0  |172.16.1.1      |

PC C

Mau Ke Mana,Lewat Mana
172.16.2.0/24,Lan-ethernet
0.0.0.0/0,172.16.2.1

Router A

Mau Ke Mana,Lewat Mana
172.16.0.0/24,ether1
172.16.1.0/24,"192.168.0.2,192.168.2.2"
172.16.2.0/24,"192.168.0.2,192.168.2.2"
192.168.0.0/24,ether2
192.168.1.0/24,"192.168.0.2,192.168.2.2"
192.168.2.0/24,ether3

Router B

Mau Ke Mana,Lewat Mana
172.16.0.0/24,"192.168.0.1,192.168.1.2"
172.16.1.0/24,ether1
172.16.2.0/24,"192.168.0.1,192.168.1.2"
192.168.0.0/24,ether2
192.168.1.0/24,ether3
192.168.2.0/24,"192.168.0.1,192.168.1.2"

Router C

Mau Ke Mana,Lewat Mana
172.16.0.0/24,"192.168.2.1,192.168.1.1"
172.16.1.0/24,"192.168.2.1,192.168.1.1"
172.16.2.0/24,ether1
192.168.0.0/24,"192.168.2.1,192.168.1.1"
192.168.1.0/24,ether3
192.168.2.0/24,ether2

Pada tabel routing diatas ada 2 hal yang unik :

1. Terdapat penggunaan Network 0.0.0.0/0 pada tabel routing PC A-C
2. Terdapat penggunaan dua IP Address Lewat Mana pada masing-masing Router

Nomor 1 itulah yang disebut sebagai default routing/default gateway. Jika dilihat-lihat, pada setiap PC, satu-satunya jalur keluar untuk menuju seluruh Network hanyalah 1 IP. Oleh karena itu kita tidak perlu memasukkan tabel routing seluruh Network satu persatu, melainkan kita cukup gunakan 1 Network tujuan yang mewakili seluruh network, yaitu 0.0.0.0/0.

Nomor 2 adalah contoh penggunaan bahwa untuk menuju suatu Network Address tidak selalu hanya 1 jalur saja. Melainkan bisa beberapa jalur. Nantinya beberapa jalur ini akan diperhitungkan oleh Router berdasarkan mana yang lebih baik. Parameter lebih baik ini bisa bermacam-macam tergantung protokol routing yang digunakan. Bisa lebih dekat, bisa lebih baik kualitas kecepatan linknya, dsb.