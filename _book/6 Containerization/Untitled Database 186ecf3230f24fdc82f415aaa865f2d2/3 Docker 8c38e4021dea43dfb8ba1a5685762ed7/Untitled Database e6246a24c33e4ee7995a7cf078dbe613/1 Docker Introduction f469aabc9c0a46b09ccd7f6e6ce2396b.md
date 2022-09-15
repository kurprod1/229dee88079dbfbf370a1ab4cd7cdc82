# 1. Docker Introduction

Created: July 4, 2022 9:58 AM

# **Sejarah dan Konsep Docker**

Pada dasarnya sebelum ada Docker, teknologi yang sudah cukup sering dipakai adalah teknologi Virtualisasi. Yaitu teknologi untuk dapat memiliki banyak Server Virtual didalam sebuah server fisik. Sistem Virtualisasi ini sangat digandrungi, karena dapat memaksimalkan efisiensi secara budget dan pengelolaan. Bisa bayangkan kita cukup membeli 1 buah Server, tapi di dalamnya bisa kita bangun lagi 5 buah server virtual. Sangat cost-effective.

[*Arsitektur traditional vs Virtualisasi*](https://lh6.googleusercontent.com/BZfQe7DHwXo4l96G2cCfQNzXKM1c9N-T9qHbrpimJOVa1TCxa6WA8uTuRPBEhHrvEM_rgdbYs9XCUOuMJ9VWQjc4JXjzawl3bG8GF9MXl3smzIkwlas1rZwBAc7EJ96TiwcYeowd61sTRHi4jw)

*Arsitektur traditional vs Virtualisasi*

Sayangnya **Virtualisasi** memiliki 1 kekurangan besar, yaitu untuk menggunakan sebuah layanan/*service* kita tetap harus menginstall terlebih dahulu Sistem Operasi diatasnya, walaupun layanan/service tersebut sangat kecil kebutuhan resourcenya. Bisa kita lihat pada gambar diatas, untuk setiap App, tetap perlu OS dibawahnya.

Perlunya ada sistem operasi ini di masing-masing service ini juga menyebabkan pengelolaan menjadi kompleks dan lambat. Belum lagi beban yang semakin berat. Bisa bayangkan jika kita memiliki 5 server virtual, masing-masing memakan resource 2GB RAM, maka server kita sudah habis *resource* sebesar 10GB RAM.

Hal ini yang menyebabkan Virtualisasi menjadi kurang relevan di era serba cepat, era aplikasi seperti saat ini. Dibutuhkan sebuah teknologi mirip seperti Virtualisasi namun yang tidak memakan *resource* sebesar itu dan tidak selambat itu dalam pengelolaannya. Teknologi mirip Virtualisasi yang ringan dan cepat. Inilah yang disebut sebagai **Teknologi *Container*.**

Pada mulanya, teknologi *Container* ini muncul dari seseorang bernama Solomon Hykes yang memulai project Container bernama **Docker** di Prancis sebagai proyek internal di dotCloud, sebuah perusahaan *platform-as-a-service*. Docker dirilis sebagai proyek aplikasi *open source* pada bulan Maret 2013. Dengan sangat cepat Docker menjadi terkenal hingga pada tahun 2015 saja Docker sudah terdaftar memiliki lebih dari 6000 pengguna. Oleh karena itulah bermunculan standar – standar untuk teknologi Docker container, seperti OCI dan CNCF.

[*Logo Docker*](https://lh4.googleusercontent.com/rSUQSBQC64HpEmOSihtb4BGNFfrR5TBB_m9Qphsaso_v5wV-AUUwPRhqXtlN-9NMimWXdmx30Jp4_WR4B7Z12I0fGUph4eXjSRGZ2D0QE8SO0GHqOzU1yoF726Q2nY-_ELOGAU4D-Ybh_TSJ-Q)

*Logo Docker*

Docker dengan teknologi Containernya muncul dan membuat gebrakan di tengah-tengah pengguna Virtualisasi biasa. Kini Docker berhasil menjadi salah satu teknologi yang banyak dipakai di dalam industri startup. Alasannya mudah, karena dengan docker kita tidak perlu menginstall Sistem Operasi tertentu apabila kita hanya ingin menggunakan salah satu servicenya. Sebuah kelebihan yang tidak ada pada sistem Virtualisasi biasa.

Dengan demikian kita dapat menghemat sumber daya mesin kita untuk dapat melakukan job lainnya juga.

# **Perbedaan Docker dan Virtualisasi**

Baik **Teknologi Docker Container** dan **teknologi Virtualisasi** memiliki beberapa perbedaan dalam arsitekturnya, antara lain adalah sebagai berikut.

[*Ilustrasi perbedaan antara virtualisasi dengan container*](https://lh3.googleusercontent.com/G2YaTdTV2T626dwhSfYtJLys6IS8QqIn9RIaeAFyj_UBm36oXh-Nt4bC5EfQaWc8eNpfTRye2Jj1TSYeTsTqNFi6Z7ANisl6Spu8r0C6yvFxGTo3fN-Y8GIfihvbTvltiTNDMGvpO5_PzfS2PQ)

*Ilustrasi perbedaan antara virtualisasi dengan container*

Gambar diatas merupakan analogi struktur Virtualisasi (Kiri) dan Docker *Container* (Kanan). Nah dari gambar diatas dapat kita lihat perbedaannya.

## **Struktur Virtualisasi**

Pada struktur VM dibutuhkan Hypervisor (*Virtualization Software*) sebagai penghubung antara mesin kita (*Host OS*) dan OS Virtualisasi (*Guest OS*). Dengan Demikian kita dapat menginstall OS apapun dengan versi kernel berapapun di dalam *Guest* OS, karena *Guest* OS dan Host OS bisa dikatakan terpisah meskipun secara logical *Guest* OS terletak di dalam  Host OS. Misalnya saja kita dapat menginstall Windows 7 di dalam *Guest* OS meskipun *Host* OS kita menggunakan Ubuntu 16.04.

## ***Stuktur Docker***

Pada Struktur Docker dapat dilihat bahwa Container berjalan langsung diatas Mesin Kita (*Host OS*) tanpa adanya penghubung (*Hypervisor*) dengan demikian tidak dimungkinkan untuk menginstall OS maupun service di dalam Container dengan versi kernel yang berbeda. Jadi apabila kita menginstall OS atau service pada container pastilah OS atau *service* yang memiliki versi kernel dan *library* yang sama dengan *Host* OS.

Misalnya kita dapat menginstall Centos pada container meskipun *Host* OS kita adalah ubuntu dengan catatan Centos yang kita install menjalankan versi kernel yang sama dengan *Host* OS.

Masing-masing tentunya ada plus dan minusnya. Bila kita menggunakan hypervisor:

- Sistem operasi host dan guest tidak ada hubungan sama sekali. Jadi kita bisa menginstal sistem operasi apapun sebagai guest.
- *Overhead* lebih tinggi, karena adanya hardware virtual. Konsekuensinya, *performance* menjadi lebih terbatas. Penggunaan resource juga tidak bisa terlalu dioptimalkan, karena begitu sudah dibooking oleh salah satu guest tidak bisa digunakan *guest* lain, walaupun *guest* pertama sedang sibuk.
- Lebih mudah mengatur keamanan, karena hubungan antara *host* dan *guest* sangat sedikit.

Bila kita menggunakan *container*:

- Sistem operasi *guest* berbagi kernel dan aplikasi utama dengan *host*. Dengan demikian kita tidak bisa menginstal sistem operasi yang berbeda dengan *host*, seperti Windows di host Linux.
- Penggunaan *resource* *hardware* bisa lebih dioptimalkan. Karena *host* mengetahui secara detail kondisi masing-masing guest, maka dia bisa mengalokasikan *resource* yang tidak terpakai kepada *guest* yang sedang sibuk.
- Dengan Docker, kita bisa membuat macam-macam *environment* yang mendukung 1 aplikasi.

# **Komponen Docker**

Selain memiliki kelebihan, docker itu sendiri dapat berjalan karena beberapa komponen yang ada didalamnya, berikut merupakan beberapa komponen yang ada dalam docker.

[*Arsitektur komponen Docker*](https://lh6.googleusercontent.com/DGbbdvFFeLuj6a0Pnx-3CbzXF07f7cnxaFcNihiRKpZUmVqM5Ki4y5tU0SEtHSBLH51X_Vqe5FIsHfy2j1EDO6p8xpn_iLP_WbnG9yN7xqulTMitMSsg_X6_7QN5aMwV0e0hJ45EuExLjFflzw)

*Arsitektur komponen Docker*

Untuk memahami diagram arsitektur tersebut, kita perlu memahami beberapa istilah yang digunakan di dunia Docker.

- ***Docker Container*** : adalah virtual machine atau guest operating system. Aplikasi kita berjalan di dalam docker container dan merasa bahwa dia berjalan di dalam sistem operasi biasa. Docker container berjalan di atas docker engine.
- ***Docker Client*** : adalah seperangkat perintah c*ommand line* untuk mengoperasikan docker container, misalnya membuat *container, start/stop container*, menghapus (*destroy*), dan sebagainya. Docker *client* hanya bertugas mengirim perintah saja. Pekerjaan sesungguhnya dilakukan oleh docker daemon.
- ***Docker Daemon*** : adalah aplikasi yang berjalan di host machine. Docker server berjalan di *background* (sebagai *daemon*) dan menunggu perintah dari docker *client*. Begitu mendapatkan perintah, docker server bekerja membuat *container*, menjalankan/mematikan container, dan sebagainya.
- ***Docker Image*** : adalah template yang digunakan untuk membuat *container*. Contohnya, ada *image* Ubuntu, CentOS, dan sebagainya. Kita juga bisa membuat image baru dari image yang lama. Misalnya kita buat image Ubuntu yang sudah terinstal Java dan MySQL. Docker image memiliki komposisi dari beberapa layer. Tiap layer bisa mewakili *command* atau perubahan tertentu.

[*Ilustrasi Docker Image*](https://lh3.googleusercontent.com/-EyWLMSTcNJ0hCyzdTIZk0Ah575IA90TBXqDVn-CDelREcnoJH6JfxFizkCf_o2Ur_CDLgB2YtadOCixunvsB4Axhn3jrxZX8jci4ljHuNyd1e_TAuCD7Mbs1WNTPvOOBv0ZG5V6kPsFdMyFBQ)

*Ilustrasi Docker Image*

- ***Docker Registry*** : adalah tempat kumpulan *image-image (repository)* yang dapat digunakan dan diakses oleh semua orang karena tersimpan di *cloud*/di server yang sudah disediakan oleh pengembang Docker.

# **Masalah utama yang dipecahkan**

Masalah utama yang dipecahkan oleh Docker dengan teknologi Kontainernya adalah soal kompleksitas. Kita coba lihat matriks dibawah :

[*Gambar Matrix of Hell*](https://lh4.googleusercontent.com/KfyuHEaa3kq-ZgrqCsq81qlcvLPYP0QvufCQcuq5xeMbfvfW-PO5OBfiGYTbD47iro0ivywBRhqvvJTT5I3NxYRdfUND0BIuj2Ns1jA1bb9XZhzeK9IqUxQ3CoMXHuHp5RYuzV7FUsB3nyX-7w)

*Gambar Matrix of Hell*

Diatas disebut sebagai *Matrix of Hell*. Yaitu kondisi yang terjadi ketika setiap komponen aplikasi yang dibangun harus disesuaikan dengan masing-masing infrastruktur, environment, dan *device* agar dapat berjalan dengan lancar.

Jaman sekarang, untuk sebuah aplikasi sederhana saja itu biasanya pasti memiliki beberapa komponen yang dipisahkan. Misalnya seperti berikut :

1. *Frontend*
2. *Backend*
3. *Database*
4. *Queue*
5. dll

Masing-masing komponen tersebut tentunya agar bisa running harus memiliki konfigurasi OS tertentu, dependensi tertentu, topologi ip tertentu, dsb.

Bisa Anda bayangkan kompleksitas yang akan terjadi?

Di server datacenter kita harus konfigurasi sendiri VM nya, OS nya, konfigurasi tambahan dllnya. Lalu kalau mau migrasi ke Public Cloud Amazon Web Services juga harus di atur ulang VM, OS, dependensinya, ip nya dll. Dst. Lalu bagiamana juga agar aplikasi tersebut bisa jalan di komputer si Developer? Tentu harus setup ulang segala macamnya.

Docker mengatasi masalah kompleksitas ini dengan sangat baik. Docker memiliki konsep untuk “mempacking” seluruh kebutuhan OS, dependensi, konfigurasi dll nya. Ini menjadi sebuah bentuk Container untuk bisa “dibuka dan dijalankan” di manapun kita mau.

Baik itu di Windows, Mac, Linux, baik itu di Publik *Cloud*, di Datacenter, di Komputer, laptop, selama menjalankan Docker maka Container yang sudah “di-*packing*” tersebut bisa “dibuka dan dijalankan” dengan lancar.

[*Ilustrasi Container*](https://lh6.googleusercontent.com/y8OWL182s4qHiXUkjlCg2ZJeK-3Cycgp8OC33FopoBf-rONLnOfwcLqf4kzeuI3BJkrskqsAkbbGcVEK45qvNztwROBLDZRpqOgq0O16futhzRQmjlTjba2F_V8oCu-2Z66rR8XZEiSLh_fZTA)

*Ilustrasi Container*

Sebuah fakta menarik lainnya adalah, dari hasil penelitan ternyata kegiatan orang-orang infrastruktur (*sysops*) selama ini sebanyak 80%nya hanya dihabiskan untuk *maintenance*. Mulai dari melakukan *monitoring*, backup data, *troubleshooting*, migrasi, *setup* ini itu, monitoring lagi, troubleshooting lagi, dst. Seluruh kegiatan harian yang kompleks ini menyebabkan orang infrastruktur tidak memiliki waktu yang cukup untuk melakukan inovasi.

[*Data hasil penelitian tentang sysops*](https://lh5.googleusercontent.com/MRI5tGUKa32V6HzdwrudFoXtFNzxbhhIjncANVUnCY1EIYgyH1T79YtgF-4yeNjizSVSWyg4Y2A94DX3o4DXsR2TMPVwadVQE5XgLdCbJLjUcPrKpVYzxFri-3fgz4o6eyFwOKLYRmcx8inMlA)

*Data hasil penelitian tentang sysops*

Dengan Docker, seluruh kompleksitas pekerjaan harian maintenance tersebut juga bisa hilang secara signifikan. Bayangkan saja, jika kita tidak menggunakan teknologi *Container* dari Docker maka berapa lama waktu yang dibutuhkan untuk bisa melakukan *deployment* puluhan server di banyak infrastruktur? Bisa berhari-hari dengan berbagai kompleksitas dan kemungkinan *error* yang terjadi.

Harus *setup* VM, setup OS, konfigurasi ini itu, setup ini itu. Sedangkan apabila kita menggunakan *Container*, kita cukup lakukan deployment menggunakan beberapa *script*, maka dalam hitungan menit seluruh server sudah siap tersedia.

[*Moto Docker*](https://lh5.googleusercontent.com/7B9UDJoez-PYGdv7B1Uw7Fib_mS8iXC3v4-onjYncCWiOIVLOgj9JIhi99fs0uE5v0swRFpv1tUJYVG__BxQS16CVjDUsYogOr6FUVNWLBOqAgPdrN6GeK7Qqx6zUyl1KdP5X2HmwyB_NEnyew)

*Moto Docker*

Docker menghilangkan kompleksitas untuk mencapai kecepatan. Kecepatan dalam seluruh aspek pada development aplikasi yang menyebabkan bisnis bisa tumbuh dengan lebih cepat yang tentunya menaikkan profit bisnis itu sendiri.

# **Contoh Mesin Kontainerisasi Lainnya**

Perlu diketahui bahwa sesungguhnya mesin kontainerisasi yang digunakan di industri saat ini **tidak hanya Docker,** bahkan, ada yang performanya lebih baik dibandingkan docker. Namun, untuk belajar konsep dasar dari semua mesin kontainerisasi itu, kita dapat mempelajari Docker karena memang Docker merupakan *platform* yang umum digunakan. Berikut adalah beberapa contoh mesin kontainerisasi yang ada di Industri:

## ***PODMAN***

[https://lh3.googleusercontent.com/qVPMoOfftHG7M2ymJYPXx3fD1Vg30Dq39PP9WHKARF5raSds-VWpeIhXl17I95u41jvjYHriFXxOGmLgyuJDy7xCckJQ6UWvXMSOiWpslvxK1fEcEa8JHdBmzs4bDaRE1CwlCx_5NWKi03A9zA](https://lh3.googleusercontent.com/qVPMoOfftHG7M2ymJYPXx3fD1Vg30Dq39PP9WHKARF5raSds-VWpeIhXl17I95u41jvjYHriFXxOGmLgyuJDy7xCckJQ6UWvXMSOiWpslvxK1fEcEa8JHdBmzs4bDaRE1CwlCx_5NWKi03A9zA)

Podman merupakan engine container yang digunakan untuk mengelola container tanpa daemon atau daemonless. Podman juga memiliki command-line interface (CLI) yang kompatibel dengan docker serta pengintegrasian yang lebih baik dengan systemd. Podman memudahkan para developer untuk mencari, menjalankan, dan membagikan container.

[https://lh6.googleusercontent.com/-hAKbqWHng7u_DFxUzQBGtA4VCpk9et5dEtIuGVMMlv9b7txxlI9AOaDWyJ_Z39ZEW1z3TDxxrXp9cwVsdFkr-aqK6wPwc6CUUl1nHhvaYWn27AJ4c6_e-759wqZ9xovgw1LShEP7RfMCj3YQw](https://lh6.googleusercontent.com/-hAKbqWHng7u_DFxUzQBGtA4VCpk9et5dEtIuGVMMlv9b7txxlI9AOaDWyJ_Z39ZEW1z3TDxxrXp9cwVsdFkr-aqK6wPwc6CUUl1nHhvaYWn27AJ4c6_e-759wqZ9xovgw1LShEP7RfMCj3YQw)

[Podman](https://podman.io/)

## ***Buildah***

[https://lh6.googleusercontent.com/zFf0XvhnredMbI_kH03c84BmmmuC3SLJIJ7pi34qBci-854IpuIAd5a8LQnSYzB_XLBrRFAtK11Zn5yk6c_-nM4ZWQJkvfGxFIOojab4BeObWpfBlDFRmuJZr7N-_GdrBuDy0NEKXZlf07BNSg](https://lh6.googleusercontent.com/zFf0XvhnredMbI_kH03c84BmmmuC3SLJIJ7pi34qBci-854IpuIAd5a8LQnSYzB_XLBrRFAtK11Zn5yk6c_-nM4ZWQJkvfGxFIOojab4BeObWpfBlDFRmuJZr7N-_GdrBuDy0NEKXZlf07BNSg)

Buildah memungkinkan Anda untuk membangun dan memodifikasi container tanpa menggunakan *daemon* ataupun *docker*. Buildah akan tetap memakai *workflow* *dockerfile* yang sudah ada, tetapi memberikan para developer kontrol perihal *image*, *layers*, konten, dan *commits*. Buildah juga mengecilkan ukuran container image dengan menggunakan tools dari container host.

[https://lh5.googleusercontent.com/02zgcwsIM8axb7NO3Uih5KYWj0J_Yh7_6IXnuDIhLqBw7zf9Sat3u9W-4hlsugC75_x2EH9qtIIDvQsISJ0GkE0CQL9kNat2l8M7ml6Zy512AtcWnUDLRRzbQAhv8Qi_yfFSipOsEVyYlhFgrw](https://lh5.googleusercontent.com/02zgcwsIM8axb7NO3Uih5KYWj0J_Yh7_6IXnuDIhLqBw7zf9Sat3u9W-4hlsugC75_x2EH9qtIIDvQsISJ0GkE0CQL9kNat2l8M7ml6Zy512AtcWnUDLRRzbQAhv8Qi_yfFSipOsEVyYlhFgrw)

## ***Cri-O***

[https://lh4.googleusercontent.com/Pr5bRAVJYC0UGvPkILSuSg9PSG7mHeju2Duyps4bTfQLzaWYIr3E_Bc7sETaI3P8MiVOT-Zm1vtWEMO--5f9EU-Gvp38sdIAyum2QVRle6NUDY8r7x96mzkTZF9nf_pBemEBNYVjhoz5DuR5fg](https://lh4.googleusercontent.com/Pr5bRAVJYC0UGvPkILSuSg9PSG7mHeju2Duyps4bTfQLzaWYIr3E_Bc7sETaI3P8MiVOT-Zm1vtWEMO--5f9EU-Gvp38sdIAyum2QVRle6NUDY8r7x96mzkTZF9nf_pBemEBNYVjhoz5DuR5fg)

*Container Runtime Interface - Orchestrator* (CRI-O) adalah *runtime* yang ringan dan telah dioptimalkan untuk kluster Kubernetes. Dikembangkan oleh Red Hat dan kemudian diserahkan kepada subset dari *Special Interest Group* (SIG) yang diberi kewenangan perihal pengembangan Kubernetes.

CRI-O memberikan alternatif untuk *relying* pada *Docker runtime* yang kompatibel dengan *container images* dengan format *Open Container Initiative* (OCI).