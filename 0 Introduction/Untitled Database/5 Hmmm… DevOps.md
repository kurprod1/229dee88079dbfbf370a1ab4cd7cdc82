# 5. Hmmm… DevOps?

Created: August 16, 2022 1:25 PM

# ****Why DevOps?****

Kalau menyimak video diatas, kita hanya tahu beberapa hal yang sifatnya general saja. Nah sekarang saatnya kita untuk mengenal hal-hal yang lebih spesifik lagi, terutama mengenai DevOps. 

Berikut adalah poin-poin yang perlu kalian ketahui, untuk memahami kenapa sih industri tech membutuhkan DevOps dalam mendukung kinerja perusahaan.

# **Understand SDLC**

Dalam menghasilkan/menciptakan Aplikasi yang bagus, maka perusahaan pasti menerapkan suatu sistem dalam pembuatan aplikasi tersebut, atau bisa disebut Development Cycle. 

Intinya Development Cycle merupakan serangkaian proses dan metode bagaimana pembuatan aplikasi (atau suatu fitur di aplikasi) dari awal sampai jadi. Mulai dari ide nya seperti apa, perancangannya, bentuk desainnya, hingga implementasi dan menghasilkan suatu output.*Ilustrasi Development Cycle*

Misalnya ketika situs web Bhinneka.com ingin mengeluarkan fitur “Rating” pada kolom produk, nah proses dari awal desainnya, posisi tombolnya dimana, lalu proses pembuatan fiturnya itu sendiri, testing apakah berhasil jalan sesuai harapan atau tidak, proses analisa & revisi, sampai akhirnya fitur itu live dan bisa dinikmati oleh pengunjung situs web Bhinneka.com, itulah yang disebut sebagai Development Cycle.Sebagai pengetahuan, metode Development Cycle yang paling terkenal ada 2. Yaitu metode Waterfall dan metode Agile. 

Pengetahuan terkait metode Development Cycle ini perlu dipahami oleh kita, agar nantinya lebih mudah dalam memahami bagaimana DevOps bekerja.

[Agile Vs Waterfall: Know the Difference Between Methodologies](https://www.guru99.com/waterfall-vs-agile.html)

# **The Problems: Too Slow!**

Pada prakteknya, walaupun di environment (laptop/pc) para Developer fitur/aplikasi yang dibuat sudah sesuai yang diharapkan, ketika kode itu di deploy oleh tim Operation ke Server seringkali banyak errornya.  

Misalnya tadinya tombol A sudah bisa diklik, ternyata di server tombol tersebut tidak bisa diklik.Akibatnya, antara kedua tim ini sering saling menyalahkan apakah errornya gara-gara coding atau gara-gara server. 

Istilah-istilah seperti “It’s not my code, it’s your server!” dan “It’s not my server, it’s your code!” sudah merupakan hal yang lumrah terjadi.Developer dan Operation juga memiliki pandangan yang sangat berbeda. Developer menginginkan perubahan atau pengembangan berkala pada software mereka, sedangkan Operation menginginkan stabilitas pada server – server mereka. 

Antara tim Developer dan tim Operation menjadi seperti memiliki “bunker” masing – masing. Merasa departemen mereka benar-benar terpisah, cenderung “malas” untuk saling membantu.Akibat seluruh perbedaan ini, sekarang kita coba lihat bagaimana contoh alur yang terjadi ketika misalnya terjadi error dalam sebuah aplikasi :

1. Tim Operation meminta tim Developer mengecek.
2. Ternyata tim Developer tidak mau mengecek karena mereka merasa kesalahan bukan di sisi mereka.
3. Akhirnya tim Developer meminta ulang tim Operation yang mengecek.
4. Tim Operation “malas” mengecek karena mereka merasa sudah mensetup server mereka dengan benar.
5. Begitu terus seterusnya.

![Ilustrasi Alur Developer dan Operation yang Lambat](5%20Hmmm%E2%80%A6%20DevOps/Untitled.png)

Ilustrasi Alur Developer dan Operation yang Lambat

Bisa kita bayangkan akan berapa lama proses delay yang terjadi akibat saling lempar kesalahan tersebut. Lebih parah lagi kalau pada akhirnya tidak ada yang mau bertanggung jawab mencari solusi. Ujung-ujungnya proses delivery sebuat fitur/aplikasi baru menjadi lambat.

Delivery yang lambat ini sangat berpengaruh terhadap masa depan perusahaan. Selain cost operasional meningkat dan revenue perusahaan menurun, juga berpengaruh terhadap posisi perusahaan di industri. Masih ingat saat Snapchat masih terkenal di Indonesia sebelum ada Instagram Story? Andai saja Instagram begitu lambat dalam merilis fitur Instagram Story, maka tidak mungkin Instagram bisa mengalahkan Snapchat seperti saat ini.

# **DevOps as Solution**

DevOps sebenarnya bukanlah suatu jabatan melainkan lebih tepat menyebutnya sebagai sebuah kultur. Sebuah kultur dimana tim Developer dan tim Operation bekerja sama dalam proses development aplikasi agar lebih cepat dan efisien.

Tim Developer dan Tim Operation tidak lagi bekerja sendiri-sendiri melainkan benar-benar berkolaborasi menjadi satu persis seperti yang tergambarkan pada gambar dibawah :

![Ilustrasi Penggabungan Developer dengan Operation](5%20Hmmm%E2%80%A6%20DevOps/Untitled%201.png)

Ilustrasi Penggabungan Developer dengan Operation

Harapannya dengan penerapan DevOps, terciptalah kultur sistem development yang Iteratif, Kolaboratif, Komunikatif, Kontinyu, Sistematis, dan Ter-otomatisasi.

Dalam kultur DevOps, Tugas Operation dari yang tadinya sebagai tukang mengkonfigurasi server dan tukang deploy code ke server secara manual, berubah menjadi tukang otomasi dan pencipta sistem baru yang kontinyu serta terintegrasi. Tim Operation akan membuat sistem agar tugas Developer menjadi lebih ringan. Developer cukup ngoding saja, tidak perlu lagi pusing-pusing memikirkan masalah Deploy dan segala macamnya. Seluruh proses dari bagaimana mengintegrasikan code-code yang dibuat oleh antar sesama developer, bagaimana testingnya, hingga code itu di deploy ke server sampai live bisa dinikmati pengguna, hampir semua akan berjalan serba otomatis.

Ilustrasi setelah penerapan DevOpsProduktivitas kedua tim ini pasti akan meningkat. Karena pekerjaan yang awalnya serba manual dan juga serba delay menjadi hilang sehingga kedua tim dapat lebih fokus mengerjakan hal-hal yang lebih penting, Seperti pengerjaan aplikasi-aplikasi berikutnya maupun melakukan riset dan pengembangan teknologi baru.Transisi tugas tim Operation yang dulunya serba manual menjadi serba otomatis.

![Ilustrasi setelah penerapan DevOps](5%20Hmmm%E2%80%A6%20DevOps/Untitled%202.png)

Ilustrasi setelah penerapan DevOps

Produktivitas kedua tim ini pasti akan meningkat. Karena pekerjaan yang awalnya serba manual dan juga serba delay menjadi hilang sehingga kedua tim dapat lebih fokus mengerjakan hal-hal yang lebih penting, Seperti pengerjaan aplikasi-aplikasi berikutnya maupun melakukan riset dan pengembangan teknologi baru.

Transisi tugas tim Operation yang dulunya serba manual menjadi serba otomatis.