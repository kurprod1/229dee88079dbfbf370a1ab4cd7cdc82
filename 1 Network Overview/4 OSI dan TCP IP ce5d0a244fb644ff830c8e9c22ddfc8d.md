# 4. OSI dan TCP/IP

Created: August 15, 2022 11:23 AM

Pada bagian ini kita akan mempelajari bahwa jaringan komputer dapat bekerja karena didalamnya sudah dibuat suatu aturan-aturan yang sudah distandarisasi. Aturan-aturan ini yang menentukan cara kerja bagaimana ketika kita mengetikkan google.com di browser kita, dalam beberapa detik menjadi muncul halaman website Google. Bagaimana cara kerja ini tetap memastikan bahwa apa yang kita dapat, sesuai dengan apa yang kita minta. Bagaimana agar ketika kita akses google.com, tidak tampil situs-situs yang lain atau gambarnya berubah, atau fontnya berubah, dll. Bagaimana ketika kita telepon menggunakan Skype, suara dan video kita dapat tampil secara realtime, dll. Bagaimana agar berbagai merk dan software perangkat jaringan yang berbeda-beda seperti TP-Link, Linksys, Apple, Windows tetap bisa mendapatkan informasi yang sama, dll.

Aturan-aturan jaringan yang sudah terstandarisasi ini ada 2, yaitu model TCP/IP dan OSI.

Namun karena materi ini terlalu teoritis dan tidak pernah digunakan dalam praktek nyatanya (kecuali kita terjun ke bidang akademis untuk penelitian S2/S3 terkait jaringan), maka kita tidak perlu membahasnya terlalu dalam. Kita cukup memahami bahwa jaringan komputer itu dapat bekerja karena merujuk pada aturan yang terstandarisasi, yaitu model TCP/IP dan OSI.

# **Apa itu Model OSI ?**

*Open System Interconnection* atau biasa disingkat OSI merupakan sebuah model referensi ideal yang menjelaskan bagaimana proses komunikasi dalam jaringan komputer terjadi. Tujuan dibuatnya model referensi OSI ini agar menjadi rujukan untuk para vendor dan developer sehingga produk atau software yang mereka buat dapat bersifat *universal*, yang berarti dapat bekerja secara normal walaupun berbeda-beda vendor dan merk perangkat jaringan.

OSI memiliki 7 layer yang saling berhubungan satu sama lain, layer ini akan menjadi standar alur proses dimana sebuah data dikirimkan dari satu komputer ke komputer lainnya :

![*Ilustrasi OSI Layer*](https://lh4.googleusercontent.com/-FTUdm9NzArZ0yGJdKmKhNDs-iefddn1wI-U6sdxhrYEi_m08FlH3vUYgqAPuKCw2Tqw3k_Ls_OfYq2vzQqMGtXkVNpU8GBzp8hSm2PSMyGDXN3LCIb2FxwYVVY8qJ3jfyDcNFHowJgelN0YBVXg-A)

*Ilustrasi OSI Layer*

Contoh misalnya ketika kita membuka halaman website Google.com di sebuah komputer, maka sebenarnya secara garis besar akan terjadi alur sebagai berikut :

1. Komputer kita menghubungi Server google untuk meminta halaman web dari link yang diminta.
2. Google mengirimkan data-data halaman web kepada komputer kita.
3. Halaman web google tampil di komputer kita.

Namun dibalik 3 alur diatas, terjadi alur yang lebih panjang melalui masing-masing layer OSI pada masing-masing komputer. Pada komputer kita terjadi alur seperti ini :

1. Di layer 7, Komputer kita menjadikan permintaan halaman google.com yang diketik kedalam bentuk protokol aplikasi web, yaitu HTTP.
2. Di layer 6, Dari protokol HTTP ini dikonversi kedalam bentuk data yang lebih kecil dan terpecah, yaitu permintaan dokumen-dokumen web seperti HTML, JPG, dll.
3. Di layer 5, Disini terjadi proses untuk memastikan koneksi antara komputer kita dengan Server Google.com tidak putus.
4. Di layer 4, Disini seluruh data diubah menjadi bentuk yang lebih kecil lagi berupa segment-segment.
5. Di layer 3, Disini seluruh segment diubah menjadi bentuk yang lebih kecil lagi menjadi bentuk paket-paket.
6. Di layer 2, Disini seluruh paket diubah menjadi bentuk frame-frame yang lebih kecil lagi.
7. Di layer 1, Seluruh data berbentuk frame diubah kedalam bentuk bit-bit biner (01010101) yang nantinya dikirim dalam bentuk sinyal-sinyal listrik/cahaya untuk melalui media jaringan (kabel/wireless). Nantinya sinyal-sinyal informasi ini akan sampai ke Server penerima. Disini yang berperan adalah perangkat kabel dan konektor.

Pada komputer server Google.com juga berlaku hal yang sama, namun bedanya mereka akan mulai dari layer 1 terlebih dahulu. Data-data berupa sinyal listrik yang sudah dikirim dari komputer kita, akan diterjemahkan ulang melalui masing-masing layer hingga menjadi data yang sama saat pertama kali dikirim oleh komputer kita pada layer 7.

![*Ilustrasi Cara Kerja OSI Layer*](https://lh3.googleusercontent.com/v3E0_S8yLlCk7wwxDupXs0TZJWWoLfWIkSCNT_7_eMN6fwrXADULI93eXcKS6WY-piWoEVvGx2_KNc684Txg2536UN8Kbn-r-oXJwxGUDuMBEmkvpOVHKBW0XbuQU5LlQoYFDuQl028mXZJFIqEuUA)

*Ilustrasi Cara Kerja OSI Layer*

Sekilas akan sulit untuk membayangkan konsep dari model OSI ini. Namun memang kita tidak perlu memahami terlalu dalam konsep OSI ini. Karena pada kenyataannya Model OSI hanyalah konsep ideal yang dicetuskan oleh sekelompok ilmuwan, yang bahkan tidak pernah digunakan sama sekali di dunia jaringan komputer. Justru model yang diimplementasikan oleh seluruh jaringan komputer saat ini adalah model TCP/IP.

[![https://www.youtube.com/watch?v=Ilk7UXzV_Qc](https://img.youtube.com/vi/Ilk7UXzV_Qc/0.jpg)](https://www.youtube.com/watch?v=Ilk7UXzV_Qc)

# **Apa itu Model TCP/IP ?**

TCP/IP ini  sebenarnya versi model referensi aturan yang lebih sederhana dibandingkan dengan OSI. Dari keseluruhan 7 layer OSI, pada TCP/IP digabung menjadi hanya 4 layer saja. Namun karena TCP/IP muncul terlebih dahulu dibanding model OSI, membuat TCP/IP terlanjur terlebih dahulu lebih banyak diimplementasikan di dunia pada jaman dulu. Sehingga model OSI yang sebenarnya lebih bagus, menjadi tidak laku.

Secara cara kerja dan konsep, model TCP/IP mirip seperti pada model OSI. Dimana ketika ada sebuah komunikasi di jaringan terjadi, maka kedua komputer tersebut akan melalui serangkaian proses pada masing-masing layer. Di masing-masing layer setiap data akan disesuaikan dengan fungsinya masing-masing.

Berikut adalah layer-layer pada model TCP/IP :

![*Ilustrasi TCP/IP Layer*](https://lh3.googleusercontent.com/D49dnTj1jpP3oiZ9HDJ7m4XRrHP5-36rtiaD8iTqS6OuAlm-v9CLX_0HvewwFQAZ6uu0S1cigGfdpx4QnWTX67SCCSzAfChBBSC1Vr1JHrr89_UMgyFSJsE7v-lrvZ9ENXpwOON7Dzaphc5PlkL0OQ)

*Ilustrasi TCP/IP Layer*

[![https://www.youtube.com/watch?v=OTwp3xtd4dg](https://img.youtube.com/vi/OTwp3xtd4dg/0.jpg)](https://www.youtube.com/watch?v=OTwp3xtd4dg)
