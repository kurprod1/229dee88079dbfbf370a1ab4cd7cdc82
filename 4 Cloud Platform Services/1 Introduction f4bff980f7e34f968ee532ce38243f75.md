# 1. Introduction

Created: July 18, 2022 10:20 AM

Cloud Computing dapat diibaratkan seperti menyewa sumberdaya IT. Bentuknya dapat berupa infrastuktur (virtual machine / network), storage, aplikasi, database, dll. Disediakan siap pakai oleh Cloud Provider, dapat kita akses dan gunakan secara fleksibel sesuai kebutuhan. Nantinya, kita akan dikenakan biaya oleh Cloud Provider hanya sebesar resource yang kita gunakan (*Pay-as-You-go*). Dengan Cloud Computing, kita tidak perlu memiliki server dan perangkat sendiri.

Ada 3 (tiga) model pengiriman dalam Cloud Computing :

1. Software as a Service (SaaS) merupakan layanan untuk menggunakan aplikasi yang telah disediakan penyedia layanan mengelola platform dan infrastruktur yang menjalankan aplikasi tersebut.
2. Platform as a Service (PaaS) merupakan layanan untuk menggunakan platform yang telah disediakan pengembang fokus pada aplikasi yang dibuat tanpa memikirkan tentang pemeliharaan platform. Jika kita analogikan seperti halnya kita menyewa hotel, kita tinggal tidur dikamar yang kita sewa tanpa peduli bagaimana perawaan dari kamar dan lingkungannya. Salah satu contoh layanan PaaS adalah AWS, Azure, Dll.
3. Infrastructure as a Service (IaaS) merupakan layanan untuk menggunakan infrastruktur yang telah disediakan. Jika kita analogikan seperti kita menyewa kamar kontrakan kosong yang bisa kita isi dalamnya sesuai dengan kebutuhan (sistem operasi). Sebagai contoh layanan IaaS adalah Amazon EC2, GCE, BizNetCloud, Dll.

![*Ilustrasi perbandingan model pengiriman cloud*](https://lh6.googleusercontent.com/x64TkbPZUw3YQMHw6MLcZN9Zbos592gc-6eAP4mRCHEGD20guHfwFZUDDmFLMrE-YnYKxaKnhZWRU8R89x9g05X-qNCShH9nAaJPheyxXjF_KfL9kB7Tbaid61Y2n5loaZarOzyG9N-HFyAUtA)

*Ilustrasi perbandingan model pengiriman cloud*

Berdasarkan model penyebaran (deployment) terdapat 4 model deployment dalam Cloud Computing yang diantaranya adalah :

1. Public Cloud merupakan layanan Cloud Computing yang disediakan untuk masyarakat umum. Kita sebagai user tinggal mendaftar ataupun bisa langsung memakai layanan yang ada. Banyak layanan Public Cloud yang gratis, dan ada juga yang perlu membayar untuk bisa menikmati layanan-nya.
2. Private Cloud merupakan layanan Cloud Computing, yang disediakan untuk memenuhi kebutuhan internal dari organisasi/perusahaan. Biasa-nya departemen IT akan berperan sebagai Service Provider (penyedia layanan) dan departemen lain menjadi user (pemakai).
3. Hybrid Cloud merupakan gabungan dari layanan Public Cloud dan Private Cloud yang diimplementasikan oleh suatu organisasi/perusahaan. Dalam Hybrid Cloud ini, kita bisa memilih proses bisnis mana yang bisa dipindahkan ke Public Cloud dan proses bisnis mana yang harus tetap berjalan di Private Cloud.
4. Community Cloud dapat digunakan bersama-sama oleh beberapa perusahaan yang memiliki kesamaan kepentingan

![*Ilustrasi model deployment cloud computing*](1%20Introduction%20f4bff980f7e34f968ee532ce38243f75/Untitled.png)

*Ilustrasi model deployment cloud computing*

Ada banyak cloud provider yang ada di dunia. Akan tetapi, yang paling populer digunakan ialah ***AWS (Amazon Web Services), GCP (Google Cloud Platform)*** dan ***Microsoft Azure*.**

Untuk mengetahui persaingan antar ketiga cloud provider tersebut, kita bisa melihat perbandingannya di halaman berikut.

[AWS vs Azure vs GCP: Comparing The Big 3 Cloud Platforms](https://www.bmc.com/blogs/aws-vs-azure-vs-google-cloud-platforms/)

Untuk mempermudah kalian mempelajari topik ini, berikut mindmap yang bisa kalian jadikan patokan.

![Mind Map AWS.jpg](1%20Introduction%20f4bff980f7e34f968ee532ce38243f75/Mind_Map_AWS.jpg)

Untuk gambaran besar apa saja yang akan kita bangun menggunakan AWS, kita bisa melihat topologi dibawah.

![Untitled](1%20Introduction%20f4bff980f7e34f968ee532ce38243f75/Untitled%201.png)