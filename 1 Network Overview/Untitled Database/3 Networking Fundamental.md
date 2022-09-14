# 3. Networking Fundamental

Created: August 15, 2022 11:16 AM

Materi ini bertujuan untuk memberikan wawasan dan pengetahuan dasar terkait dunia jaringan komputer.

# **Apa itu Jaringan Komputer ?**

Jaringan komputer adalah istilah untuk ketika ada sekelompok perangkat komputer yang bisa saling berkomunikasi satu sama lain.

![*Ilustrasi bermain game menggunakan jaringan komputer*](3%20Networking%20Fundamental/image1.png)

*Ilustrasi bermain game menggunakan jaringan komputer*

Sebagai salah satu contoh pengaplikasiannya, apabila kita bermain game PC seperti Dota 2 ataupun Counter Strike berdua dengan teman dengan menggunakan Wifi itu sudah bisa dikatakan sebuah jaringan, karena pada saat kita bermain game tersebut terjadi sebuah komunikasi dari satu PC ke PC lainnya melalui sebuah media jaringan, yaitu Wifi.

[Network](https://idcloudhost.com/kamus-hosting/network/)

# **Macam-macam Jaringan**

Jaringan komputer sendiri dikelompokan menjadi berbagai macam tergantung dengan skala jarak dan besarnya pengguna pada jaringan tersebut. Jaringan yang ada pada sebuah warnet  dengan hanya ada beberapa user saja akan berbeda dengan jaringan kampus yang memiliki banyak user, begitupun satu negara yang menampung berjuta user, atau seluruh dunia yang menampung milyaran user. Berikut merupakan macam-macam jaringan berdasarkan skala jarak dan penggunanya.

## ***Local Area Network / Intranet***

Local Area Network (LAN) merupakan jaringan komputer yang memiliki area yang sangat dekat/kecil. Biasanya jaringan ini digunakan oleh pribadi, organisasi, maupun kelompok didalam sebuah area dalam gedung atau bangunan.

![*Ilustrasi LAN dalam sebuah kantor*](3%20Networking%20Fundamental/image2.png)

*Ilustrasi LAN dalam sebuah kantor*

Pada ilustrasi diatas digambarkan sekumpulan komputer yang saling terhubung membentuk sebuah jaringan LAN yang berada pada sebuah ruangan kantor. Salah satu contoh jaringan LAN adalah sebuah ruangan warnet yang diisikan oleh beberapa komputer, sebuah ruangan didalam kantor dan beberapa komputer dirumah yang terhubung ke internet.

Jaringan LAN ini juga biasa disebut sebagai jaringan intranet, yaitu sebuah jaringan private  sendiri yang tidak bisa diakses oleh publik melalui internet. Walaupun ada sedikit perbedaan istilah antara LAN dengan Intranet, namun agar tidak membingungkan dan terlalu banyak istilah disini konsep keduanya ini kita anggap sama.

## ***Metropolitan Area Network***

Metropolitan Area Network atau MAN ini memiliki cakupan lebih dari LAN atau dalam kata lain, gabungan dari beberapa LAN. Biasanya MAN ini menghubungkan komputer antar gedung atau antar kota seperti halnya ISP.

![*MAN*](3%20Networking%20Fundamental/image3.png)

## ***Wide Area Network / Internet***

Wide Area Network (WAN) dan Internet juga sebenarnya memiliki beberapa perbedaan pengertian. Namun agar tidak terlalu banyak pemahaman yang perlu dicerna, disini kita anggap bahwa WAN dan Internet ini sebagai satu konsep yang sama. Yaitu sebagai jaringan publik yang bisa diakses oleh siapapun, yang mencakup area yang sangat besar di seluruh dunia.

![*Ilustrasi Jaringan internet yang sangat luas*](3%20Networking%20Fundamental/image4.png)

*Ilustrasi Jaringan internet yang sangat luas*

Jaringan WAN/Internet ini adalah jaringan yang biasanya kita gunakan sehari hari dimana kita bisa terhubung dan mengakses jaringan dengan orang-orang dan server yang jauh disana. Salah satu contohnya bisa mengakses server AWS yang ada di singapura.

[![](https://img.youtube.com/vi/YQ2IN7jEhV0/0.jpg)](https://www.youtube.com/watch?v=YQ2IN7jEhV0)

# **Topologi Jaringan**

Selain dari jenis jaringan berdasarkan skala luasnya, jaringan juga dibagi berdasarkan bentuk hubungan antar perangkat jaringan didalamnya yaitu Topologi.

## ***Topologi BUS***

Topologi ini adalah topologi dimana masing-masing komputer akan terhubung ke satu buah jalur utama berupa kabel panjang dengan beberapa terminal.

![*Ilustrasi Topologi BUS*](3%20Networking%20Fundamental/image5.png)

*Ilustrasi Topologi BUS*

Topologi ini sudah sangat jarang digunakan didalam membangun jaringan komputer biasa karena memiliki beberapa kekurangan diantaranya besarnya kemungkinan tabrakan aliran data, serta jika salah satu perangkat putus atau terjadi kerusakan pada satu bagian komputer maka jaringan langsung tidak akan berfungsi karena hanya menggunakan 1 buah jalur utama.

## ***Topologi Star***

Seperti namanya susunan pada topologi Star sama seperti lambang bintang, yaitu kumpulan perangkat-perangkat komputer yang terhubung ke 1 titik terpusat. Titik pusatnya ini biasa menggunakan perangkat jaringan seperti Hub/Switch.

![*Ilustrasi topologi Star*](3%20Networking%20Fundamental/image6.png)

*Ilustrasi topologi Star*

## ***Topologi Tree***

Topologi jaringan komputer Tree merupakan gabungan dari beberapa topologi Star yang dihubungkan dengan topologi Bus, jadi setiap topologi star akan terhubung ke topologi Star lainnya menggunakan topologi Bus, biasanya dalam topologi ini terdapat beberapa tingkatan jaringan, dan jaringan yang berada pada tingkat yang lebih tinggi dapat mengontrol jaringan yang berada pada tingkat yang lebih rendah.

![*Ilustrasi topologi tree*](3%20Networking%20Fundamental/image7.png)

*Ilustrasi topologi tree*

## ***Topologi lainnya***

Selain dari seluruh topologi diatas, masih ada beberapa topologi-topologi lainnya yang sering digunakan di masa kini seperti topologi Mesh dan Hybrid. Cobalah untuk mengesplor kembali terkait topologi-topologi lainnya ini.

[√ Pengertian dan Macam-macam Topologi Jaringan Komputer](https://www.it-jurnal.com/pengertian-dan-macam-macam-topologi-jaringan-komputer/)

# **Macam-macam Perangkat Jaringan**

## ***Network Interface Card***

![*Ilustrasi Network Interface Card Wired*](3%20Networking%20Fundamental/image8.png)

*Ilustrasi Network Interface Card Wired*

Network Interface Card (NIC) ini merupakan sebuah board/bagian fisik yang berfungsi sebagai jembatan yang menghubungkan perangkat komputer ke sebuah jaringan. Komponen ini biasanya sudah terpasang secara onboard di masing-masing komputer. Dimana NIC ini nantinya biasanya sebagai board/bagian yang akan dicolok kabel untuk dihubungkan ke perangkat jaringan lainnya.

Namun pada dasarnya terdapat 2 macam NIC yaitu Wired dan Wireless. Dimana Wired adalah NIC yang dapat terhubung menggunakan media kabel, sedangkan Wireless adalah NIC yang dapat terhubung menggunakan media Wireless.

![*Ilustrasi Network Interface Card Wireless*](3%20Networking%20Fundamental/image9.png)

*Ilustrasi Network Interface Card Wireless*

## ***Kabel dan Konektor***

Perangkat jaringan tidak lepas kaitannya dengan kabel dan konektor. Kabel dan konektor ini digunakan untuk menghubungkan antar perangkat komputer/jaringan dengan cara di pasang/di colok ke NIC. Kabel dan konektor inilah sebagai penghantar informasi-informasi (berupa sinyal-sinyal listrik atau cahaya) antar perangkat di jaringan

Ada beberapa kabel jaringan yang dapat sering ditemukan temukan yaitu :

1. STP (Shield Twisted Pair) dan UTP (Unsheald Twisted Pair). Menggunakan konektor RJ45. Ini adalah kabel dan konektor yang paling umum digunakan.
2. Kabel Coaxial. Kabel ini menggunakan konektor BNC/T. Jenis kabel ini sudah jarang sekali digunakan karena berbagai kekurangannya.
3. Kabel Fiber Optic. Kabel ini menggunakan konektor ST. Kabel ini terbuat dari serat kaca dengan metode menghantarkan informasi menggunakan cahaya. Karena menggunakan cahaya, maka untuk saat ini teknologi Fiber Optic merupakan teknologi kabel yang paling cepat dalam menghantarkan informasi/data, Kecepatannya diperkirakan bisa mencapai 43 Terabyte/Second.

![*Ilustrasi Kabel UTP, STP, dan Konektor RJ45*](3%20Networking%20Fundamental/image10.png)

*Ilustrasi Kabel UTP, STP, dan Konektor RJ45*

![https://lh4.googleusercontent.com/gt_TOBZQ8iEu-UfeijQaLAwI1EvtHg4ZmlDGUwr_Jdtx4G5h3Y9a5NsugCd9lzAz0i04mfycI5obD3OrJJVTyz1217uGxLtxvSzYE_O-hZIvs8ZFS7q9jajE-ccXBYF-cN_tHpvWoA3njJbp2cLGtA](3%20Networking%20Fundamental/image11.png)

![*Ilustrasi Kabel Coaxial dan Konektor*](3%20Networking%20Fundamental/image12.png)

*Ilustrasi Kabel Coaxial dan Konektor*

![*Ilustrasi Kabel Fiber Optic dan Konektor*](3%20Networking%20Fundamental/image13.png)

*Ilustrasi Kabel Fiber Optic dan Konektor*

## ***Hub / Switch***

Hub/Switch merupakan komponen jaringan komputer untuk menghubungkan banyak komputer/perangkat jaringan lainnya dalam 1 buah jaringan yang sama. Perangkat ini ibaratnya seperti terminal listrik  yang dapat memperluas jangkauan listrik dari yang tadinya hanya 1 colokan, menjadi banyak colokan.

Hub/Switch ini jumlah portnya cukup banyak dan variatif, mulai dari 8, 16, 24, sampai 32 port.

![*Ilustrasi Perangkat Hub*](3%20Networking%20Fundamental/image14.png)

*Ilustrasi Perangkat Hub*

![*Ilustrasi Perangkat Switch Managable*](3%20Networking%20Fundamental/image15.png)

*Ilustrasi Perangkat Switch Managable*

Switch sendiri pada prinsipnya sama dengan hub, bedanya switch lebih pintar daripada hub. Switch mampu menganalisa paket data yang dilewatkan padanya sebelum dikirim ke tujuan. Selain itu terdapat juga Switch Manageable yang dapat diatur berbagai konfigurasi-konfigurasi tambahan lainnya.

## ***Router***

Router secara fungsi dasarnya merupakan perangkat yang mirip seperti Polisi Lalu Lintas. Yaitu perangkat yang bertanggung jawab mengatur lalu lintas di jaringan. Seperti memperbolehkan komputer mana saja yang boleh mengakses jaringan, menghubungkan antar jaringan, dll. Salah satu fungsi utamanya adalah untuk menghubungkan perangkat  pada dua buah jaringan yang berbeda agar saling bisa berkomunikasi. Beberapa router terkenal diantaranya adalah mikrotik, fortigate, juniper, cisco, dll.

![*Ilustrasi Router Mikrotik*](3%20Networking%20Fundamental/image16.png)

*Ilustrasi Router Mikrotik*

## ***Server***

Server sudah kita bahas di Bab sebelumnya secara lengkap. Pada intinya Server adalah sebuah komputer yang bertugas untuk memberikan layanan pada pengguna. Layanan-layanan yang dapat disediakan oleh server diantaranya : Web Server, Mail Server, Database Server, dll.

![*Ilustrasi Komputer Server*](3%20Networking%20Fundamental/image17.png)

*Ilustrasi Komputer Server*

## ***Modem***

![*Ilustrasi Perangkat Modem*](3%20Networking%20Fundamental/image18.png)

*Ilustrasi Perangkat Modem*

Modem merupakan perangkat yang digunakan sebagai penghubung jaringan LAN dengan Internet. Ini adalah perangkat yang wajib ada di jaringan yang membutuhkan akses ke internet.