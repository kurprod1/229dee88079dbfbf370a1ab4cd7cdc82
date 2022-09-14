# 4. Mengenal Linux (GNU/Linux)

Created: June 23, 2022 10:27 AM

# **Mengenal Sistem Operasi**

Tahukah bahwa laptop yang temen temen gunakan itu sudah ada yang namanya sistem operasi. Misalnya Windows dan Linux Ubuntu. Tapi apakah itu sistem operasi?

Sistem operasi simplenya adalah sebuah paket software yang dapat menjadi perantara antara pengguna dengan perangkat keras. Sistem operasi ini sedemikian rupa didesain untuk memanage resource (RAM, CPU) dan menjalankan program program pada saat pengguna menjalankan/menggunakan komputer.

[https://lh4.googleusercontent.com/apHXnQG9ptXb84LcYddiS_3ruwzJnd2_j-jIkjbENRny5Qgxdoid3LcEkqs-ZZm8eRSNn7ibLBfTh9GTBB9bbLUZISkRX0Hlc5N3J57Z_6-sPsj-757Syu_efCmeAwnfxouijJ_lzY7qrZ-C2Q](https://lh4.googleusercontent.com/apHXnQG9ptXb84LcYddiS_3ruwzJnd2_j-jIkjbENRny5Qgxdoid3LcEkqs-ZZm8eRSNn7ibLBfTh9GTBB9bbLUZISkRX0Hlc5N3J57Z_6-sPsj-757Syu_efCmeAwnfxouijJ_lzY7qrZ-C2Q)

Dari beberapa sistem operasi yang ada, tentunya temen temen udah ga asing dengan Windows. Ya! Microsoft Windows merupakan salah satu sistem operasi yang paling populer karena desainnya yang intuitif bagi user sekalipun yang belum pernah memakai komputer.

Sistem operasi populer lainnya adalah Linux Ubuntu. Ya, sistem operasi ini populer dikalangan developer atau engineer karena peruntukannya yang cocok dengan daily usage.

Mengapa Linux Ubuntu cocok untuk developer atau engineer? Jawabannya simple yaitu karena Linux memiliki kelebihan pada bagian security dan speed. Dan lagi, Linux menyediakan berbagai macam paket  program untuk dijadikan sebagai penyedia layanan seperti mail, sharing file, DNS, hosting web dan lainnya. Linux kebanyakan menggunakan command line untuk menjalankan program yang dapat membuat proses layanan menjadi lebih cepat.

Berbeda dengan Windows atau MacOS yang lebih cocok untuk keperluan penggunaan kegiatan sehari-hari. Seperti bermain game, untuk ketik-ketik dokumen, untuk bekerja, dll. MacOS lebih untuk kegiatan terkait desain. Biasanya para desainer, pembuat film, pembuat musik lebih suka menggunakan Mac OS. Nah Linux, ini lebih cocok untuk dipakai di Server. Yaitu untuk memberikan layanan-layanan kepada pengguna.

# **Apa itu Linux?**

[https://lh3.googleusercontent.com/aJxFv74jjNIamNCyXDtmroOQDDzzTa1KeyxD4ilo4Ex4RPKc6MvekZqqL5CJUs2TfY7L6G2_Y1-gyE1Q2CxAoG_euu-0-hL_-4e71wmAXTh3EI2Ik9Jnww0lqnujno1158hE6ytczJ0iBtJGHg](https://lh3.googleusercontent.com/aJxFv74jjNIamNCyXDtmroOQDDzzTa1KeyxD4ilo4Ex4RPKc6MvekZqqL5CJUs2TfY7L6G2_Y1-gyE1Q2CxAoG_euu-0-hL_-4e71wmAXTh3EI2Ik9Jnww0lqnujno1158hE6ytczJ0iBtJGHg)

Lalu apa itu Linux? Linux lebih tepatnya hanyalah sebuah kernel, bukan sistem operasi itu sendiri. Kernel ini adalah inti atau mesin dari sistem operasi. Ibarat motor, kernel ini adalah mesin motor, bukan keseluruhan dari si motornya itu sendiri.

Untuk lebih detailnya, Linux disusun oleh beberapa komponen, diantaranya:

1. Bootloader – Software yang bertanggungjawab dalam proses awal saat mesin menyala yaitu booting. Bootloader akan memuat OS dan menjalankannya sampai bisa digunakan oleh user.
2. Kernel – Inti dari Linux yang bertanggungjawab menanage sistem dan resource pada mesin.
3. Init system – Subsystem yang berguna untuk mengatur daemon. Selain itu, init system juga meneruskan proses dari Bootloader seperti GRUB (GRand Unified Bootloader).
4. Daemons – Program yang berjalan pada background dimulai saat boot atau login.
5. Graphical server – Subsistem yang digunakan untuk menampilkan grafik monitor.
6. Desktop environment – Seperangkat tampilan UI yang digunakan untuk berinteraksi antara user dengan sistem. Singkatnya Desktop Environment ini seperti tema. Ada berbagai pilihan environment misalnya GNOME (Ubuntu default), KDE, Xfce, dan lain lain. Tiap environment memiliki paket layanan/program default yang berbeda seperti file manager, browser, dan lain lain.
7. Applications – Aplikasi yang dapat digunakan.

Linus Torvalds adalah pencipta Kernel Linux pada tahun 1991. Dan terus berkembang pesat sejak saat itu hingga sekarang karena seluruh source code dari Linux dapat diakses dan dimodifikasi secara bebas tanpa membayar sepeserpun atau open source.

Tool tool atau aplikasi yang ada pada Linux berasal dari GNU. GNU ini adalah sebuah proyek dari seorang bernama Richard Stallman berupa sekumpulan tools, software, aplikasi, dan komponen-komponen pelengkap sebuah Sistem Operasi.

[https://lh5.googleusercontent.com/JtFRB5cl9KdjicPcJomuHL7RnjLHXxkP2w73-BA7-GLjm2TNkR4GE3pf7ac5f7Ur--6WnIC-FyR7DyRLVb2jLX6WqbHkMOipSUg8c_fRg5HbdsbfOabSQLL4vm3MewTFoFdnPDnNdpXKJgI4ZA](https://lh5.googleusercontent.com/JtFRB5cl9KdjicPcJomuHL7RnjLHXxkP2w73-BA7-GLjm2TNkR4GE3pf7ac5f7Ur--6WnIC-FyR7DyRLVb2jLX6WqbHkMOipSUg8c_fRg5HbdsbfOabSQLL4vm3MewTFoFdnPDnNdpXKJgI4ZA)

# **Kenapa Linux bisa cocok untuk Server?**

Berikut kira-kira beberapa faktor mengapa Linux paling cocok digunakan untuk Server :

1. Lebih aman
2. Lebih stabil
3. Banyaknya tools dan aplikasi yang tersedia untuk kebutuhan Server
4. Mayoritas tools dan aplikasi yang tersedia di Linux itu Free.
5. Banyaknya dokumentasi yang tersebar di internet
6. Besarnya forum yang siap membantu menjawab dan mendokumentasikan segala hal tentang Linux.

Seluruh poin diatas hanya disebabkan oleh 1 hal. Karena kode sumber Linux yang bebas untuk diakses dan di modifikasi.

Hal inilah yang menyebabkan tumbuhnya basis pengembang aplikasi dan tools di Linux yang sangat besar di seluruh dunia. Mulai dari perorangan hingga perusahaan-perusahaan besar macam Intel, Oracle, Google, hingga Samsung juga turut berkontribusi. Mereka menyukai pembuatan aplikasi di Linux karena kebebasan modifikasinya. Mereka bisa turut berkontribusi bersama-sama untuk mengembangkan aplikasi, memperbaiki, hingga menggunakannya. Semuanya secara bebas.

[https://lh4.googleusercontent.com/9wzaqPZI-XCas5eryW4KJBN6Q0MgXV6hiZMD-9iDEa8_Z17vIxPzt3aB6GIDXtPFY3gmWuDvXkIHksD4PW54I3j75bCVgMjKEQ1c4p4Ou-9qWOq6oS6gB_93TrpNNCHzUhOXGWt8HCgLo10B6w](https://lh4.googleusercontent.com/9wzaqPZI-XCas5eryW4KJBN6Q0MgXV6hiZMD-9iDEa8_Z17vIxPzt3aB6GIDXtPFY3gmWuDvXkIHksD4PW54I3j75bCVgMjKEQ1c4p4Ou-9qWOq6oS6gB_93TrpNNCHzUhOXGWt8HCgLo10B6w)

Saking banyaknya orang dan perusahaan yang berkontribusi, akibatnya ketika ada sebuah virus maupun celah keamanan yang muncul di Linux akan sangat cepat diperbaiki. Ini yang menyebabkan Linux lebih aman, karena hampir tak ada kesempatan bagi hacker untuk menyerang Linux dengan sukses. Mereka sudah capek-capek membobol, tapi dalam waktu yang singkat berhasil diperbaiki. Membuat usaha mereka tidak sebanding dengan hasilnya. Untuk apa riset mencari celah berbulan-bulan tapi berhasil diperbaiki hanya dalam hitungan jam?

# **Distribusi/Distro Linux**

Distribusi Linux atau yang sering disebut sebagai distro Linux, merupakan sistem operasi GNU/Linux yang sudah di modifikasi untuk tujuan penggunaan tertentu.

Misalnya ada Distro Kali Linux yang cocok untuk tujuan hacking, atau ada distro Linux Mint yang cocok untuk tujuan kegiatan sehari-hari (printing, office, dll), atau ada distro Centos yang lebih cocok untuk digunakan sebagai Server, hingga Android yang merupakan distro untuk kebutuhan Smartphone.

[https://lh4.googleusercontent.com/R4BgAJY58lfN80_no3-lQ1_f42Uvfi5dB397OLVP9Fgmium6TsR-np8omKBt22p-8zvpAGRsau_tv16nF5Ym5IMZHCZfE4B5sA1mkNTU37uezT9PKxYosVPcY26SIX_QR8Ml96D_sCwqaXVWAA](https://lh4.googleusercontent.com/R4BgAJY58lfN80_no3-lQ1_f42Uvfi5dB397OLVP9Fgmium6TsR-np8omKBt22p-8zvpAGRsau_tv16nF5Ym5IMZHCZfE4B5sA1mkNTU37uezT9PKxYosVPcY26SIX_QR8Ml96D_sCwqaXVWAA)

Analogi Distro ini bisa diibaratkan  tipe sepeda motor. Misalnya Honda Beat, sepeda motor yang tujuannya untuk penggunaan sehari-hari keliling komplek saja. Atau ada Kawasaki Ninja, yaitu sepeda motor yang tujuannya untuk balapan. Sepeda Motornya itu sendiri adalah Sistem Operasi GNU/Linux, nah segala macam modifikasi aksesoris, stiker motornya, letak spionnya, model bodynya, sehingga terciptalah tipe motor Honda Beat, itulah Distro.

# **Distro Terkenal di Indonesia**

Beberapa distro yang populer di Indonesia adalah Debian, Ubuntu, Fedora, OpenSuse, Blankon, Linux Mint, hingga Android.

## **Parent Distro**

Distro Linux ini jumlahnya ada ribuan di seluruh dunia. Akan tetapi seluruh distro yang ada di dunia sejauh sebenarnya hanya merujuk pada 3 buah distro besar, yaitu :

1. Debian
2. RedHat
3. Slackware

Secara konsep, ketiga distro diatas dengan seluruh distro yang ada diseluruh dunia adalah sama. Sekalipun ada perbedaan, itu hanya beda nama dan teknik saja. Sehingga jika kita sudah menguasai salah satu distro, maka ketika pindah ke distro lain itu tidak akan ada masalah. Cukup melakukan beberapa penyesuaian saja.

Agar lebih fokus, distro yang digunakan selama pembelajaran Sekolah DevOps Cilsy menggunakan distro CentOS dan Ubuntu.

## **CentOS**

[https://lh3.googleusercontent.com/GYtNy1Zg7qmNTisRBSRHTsGcveiAl-1Ix8e7Ienp3UYtGLyOd9HW_ko0ZSlIh6zuqhs8-rMI5Wjq8_c1ys1Iw1sLTn_HfnBCC_7YfT_TlNYideCmmOV10G5TU01__9668fi-gCgF82IFkQZqjw](https://lh3.googleusercontent.com/GYtNy1Zg7qmNTisRBSRHTsGcveiAl-1Ix8e7Ienp3UYtGLyOd9HW_ko0ZSlIh6zuqhs8-rMI5Wjq8_c1ys1Iw1sLTn_HfnBCC_7YfT_TlNYideCmmOV10G5TU01__9668fi-gCgF82IFkQZqjw)

CentOS (Community ENTerprise Operating System) merupakan Distro Linux yang cocok dipergunakan dalam skala Server Enterprise selain itu juga gratis. CentOS dikembangkan oleh sebuah komunitas yang disebut CentOS Project, yang dibuat benar-benar persis dari kode sumber distro Red Hat Enterprise (RHEL). Distro RHEL ini sendiri adalah distro yang cukup disegani dan cukup banyak dipakai di perusahaan-perusahaan enterprise karena dikenal akan kestabilan dan kehandalannya serta didukung tim support yang mumpuni. Sayangnya RHEL ini adalah distro yang berbayar.

CentOS hadir sebagai solusi dimana orang yang ingin merasakan kualitas distro yang stabil dan handal persis seperti RHEL namun dengan harga yang gratis.

CentOS dirilis setiap versi RHEL juga dirilis. Biasanya selang 2-3 bulan setelah versi RHEL terbaru dirilis, CentOS juga akan ikut dirilis.

Paket aplikasi-aplikasi yang digunakan di CentOS menggunakan ekstensi .rpm.

## **Ubuntu**

[https://lh3.googleusercontent.com/ojd7Yx1vaBx51TA3fe86I3aTiryVzmrizmo7aHPelTMIZnzW5CLMh0pMb2mK8Ut7IRSg-gUmIR3A-BT259E0jl9rlW4xgEAa61db5lupyaVXfey3BptBY0kOleXlM0vB8Wi6Q3XVAK0puimTdg](https://lh3.googleusercontent.com/ojd7Yx1vaBx51TA3fe86I3aTiryVzmrizmo7aHPelTMIZnzW5CLMh0pMb2mK8Ut7IRSg-gUmIR3A-BT259E0jl9rlW4xgEAa61db5lupyaVXfey3BptBY0kOleXlM0vB8Wi6Q3XVAK0puimTdg)

Ubuntu merupakan salah satu distro Linux berbasis distro Debian dan didistribusikan sebagai distro  yang bebas dan gratis. Nama Ubuntu berasal dari filosofi dari Afrika Selatan yang berarti "kemanusiaan kepada sesama". Ubuntu dirancang untuk kepentingan penggunaan pribadi, namun versi server Ubuntu juga tersedia, dan juga telah dipakai secara luas.

Proyek Ubuntu resmi disponsori oleh Canonical Ltd. yang merupakan sebuah perusahaan yang dimiliki oleh pengusaha Afrika Selatan Mark Shuttleworth. Tujuan dari distribusi Linux Ubuntu adalah membawa semangat yang terkandung di dalam filosofi Ubuntu ke dalam dunia perangkat lunak. Ubuntu adalah sistem operasi lengkap berbasis Linux, tersedia secara bebas, dan mempunyai dukungan baik yang berasal dari komunitas maupun tenaga ahli profesional.

Ubuntu merupakan distro yang cukup populer di dunia karena dikenal akan kemudahan, ringan, handal, dan banyaknya support di internet.

Ubuntu memiliki dua buah versi rilis yang berbeda, yaitu versi LTS (Long Term Support) dan versi biasa. Letak perbedaan kedua versi ini adalah pada jangka waktu support yang disediakan oleh Cannonical. Versi LTS disupport selama 3 tahun untuk versi Desktop dan 5 tahun untuk versi Server. Namun semenjak versi Ubuntu 12.04 LTS, kedua versi sama-sama disupport selama 5 tahun. Versi biasa hanya disupport selama 18 bulan atau 1,5 tahun.

Versi LTS lebih ditujukan kepada pengguna Server, karena penggarapan versi LTS ini lebih diutamakan pada kestabilan dan kehandalan sistem. Versi LTS di rilis tiap 2 tahun sekali, sedangkan versi biasa dirilis tiap 6 bulan sekali.

[https://lh6.googleusercontent.com/zwqhnAOy-M8VmuYa2BuiFxlHidDlCooHwBa9vizUS6qgn24XKO7ZJOiIGWZ1bgc_fyom5xDv6TVRdWnXPMQx11J7OmwmiXC5uLRuR62qF1rsO9WE4jSTufX-AkQJ0y9OA4VIO1Gz-k-bTbMZMQ](https://lh6.googleusercontent.com/zwqhnAOy-M8VmuYa2BuiFxlHidDlCooHwBa9vizUS6qgn24XKO7ZJOiIGWZ1bgc_fyom5xDv6TVRdWnXPMQx11J7OmwmiXC5uLRuR62qF1rsO9WE4jSTufX-AkQJ0y9OA4VIO1Gz-k-bTbMZMQ)

# **Exercise**

1. Jelaskan kembali perbedaan Linux, GNU, Sistem Operasi, dan Distro?
2. Kenapa Linux lebih cocok untuk server dibanding sistem operasi lain?