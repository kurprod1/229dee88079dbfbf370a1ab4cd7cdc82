# 3. Kubernetes Introduction

Created: July 7, 2022 1:15 PM

# **Apa itu Kubernetes ?**

Kubernetes adalah sebuah cluster management open source yang digunakan untuk mengelola container. Aplikasi ini berasal dari aplikasi internal yang digunakan Google untuk mengelola cluster. Secara bisnis, Kubernetes adalah senjata andalan Google untuk mendongkrak peringkatnya di pasar cloud hosting atau google cloud platform.

[*Ilustasi Kubernetes*](https://lh5.googleusercontent.com/A44I-IzE6BAhk2bBIoErjbCnaSOs69l1kqqf5M6fdCrs_YjelIo4SATqGEzAyCpYs8Ef2C4H9RIqevFBTBTj4z-jJMgC353o7g0KLqiboV5gq92c8ujj7ZhqN6tnCKhyxjzygARY1y9z6gDbOA)

*Ilustasi Kubernetes*

Kubernetes berfungsi sebagai mesin untuk scheduling dan controlling container pada server physical atau virtual server. Kubernetes memberikan infrastruktur kontainer-sentris maksudnya semua aplikasi berjalan dalam kontainer atau docker.

# **Arsitektur Kubernetes**

[*Arsitektur Kubernetes*](https://lh4.googleusercontent.com/nCrI-GK2kuuYF7NFq1WDhF6BQX_VaFWAmJL6ZaGJv7cgWFQCbC71DBmVwSWJWCCJO58FQqU2ZuM-dTvYk3oQnJWm7IDy-qB2ujcHhwGyenvsaWkarHpv1OrMbzhbK8R2wqvCwwv7cSnsvetRgg)

*Arsitektur Kubernetes*

Pada gambar diatas kita bisa lihat diagram arsitektur kubernetes yang memiliki beberapa komponen yang berbeda dan saling terintegrasi satu sama lain diantaranya adalah

1. **Kubelet**
2. **Kubernetes controller manager**
3. **Kubernetes API server**
4. **Fitur Kubernetes**
5. **Automatic Binpacking**

Otomatis mengelola kontainer berdasarkan resource yang dibutuhkan dan tidak mengorbankan ketersedian resource..

1. **Horizontal Scaling**
    
    Melakukan scale up dan down aplikasi menggunakan perintah sederhana, dengan UI, atau dengan otomatis berdasarkan penggunaan cpu.
    
2. **Self-healing**
    
    Merestart container yang gagal, menggantikan dan menjadwalkan ulang container saat node worker mati. mematikan container yang tidak merespon pemeriksaan kesehatan yang dibuat oleh pengguna, dan tidak mengadvertise container ke klien hingga siap untuk digunakan.
    
3. **Service discovery and load balancing**
    
    Tidak perlu modifikasi aplikasi untuk menggunakan mekanisme service discovery yang tidak dikenal. kubernetes memberikan alamat ip pada container dan memberikan single DNS untuk sekumpulan container dan dapat load balance diantara container.
    
4. **Secret and configuration management**
    
    Deploy dan update secret dan konfigurasi aplikasi tanpa rebuild image anda tanpa memberitahukan secret dalam stack konfigurasi.
    
5. **Storage orchestration**
    
    Secara otomatis akan mounting ke sistem penyimpanan yang sudah dipilih, baik penyimpanan local, public cloud storage seperti GCP atau AWS dan network storage seperti NFS, iSCSI, Gluster, Ceph, Cinder atau Flocker.
    

# **Istilah – Istilah pada kubernetes**

Pada aplikasi kubernetes sendiri terdapat beberapa istilah yang mungkin akan sering kita dapatkan, berikut merupakan beberapa istilah beserta arti dari istilah tersebut.

1. **Deployment**
    
    Deployment menyediakan update deklaratif untuk Pod dan ReplicaSet. Kita bisa mengatur bagaimana pod dibangun, berapa banyak replika dari pod dan sebagainya.
    
2. **Replicasets**
    
    Replika dari pod yang didefinisikan pada Deployment
    
3. **Pod**
    
    Pod merupakan grup container instance. Kita bisa menjalankan beberapa container (misalnya aplikasi web + Database) dalam satu pod. Di antara container dalam satu pod bisa saling mengakses dengan menggunakan alamat localhost, bisa di katakan pod seperti laptop yang kita pakai coding.
    
4. **Node**
    
    Node adalah penyebutan dari mesin-mesin yang di gunakan. Mesin ini bisa saja mesin virtual (seperti VPS atau Instance) atau mesin fisik.
    
5. **Service**
    
    Service merupakan mekanisme untuk mengekspos pod kita ke dunia luar. Aplikasi kita yang berjalan dalam pod tidak memiliki alamat IP yang tetap. Agar bisa diakses oleh aplikasi lain atau oleh user, kita perlu alamat IP yang tetap. Service menyediakan alamat IP yang tetap, yang nantinya akan kita arahkan ke pod kita dengan menggunakan selector.
    
6. **Label**
    
    Label adalah seperangkat informasi metadata untuk mencari pod tertentu.
    
7. **App-Test**
    
    Kita buat label app yang isinya adalah nama aplikasi. Semua container, pod, dan service yang menjadi bagian dari aplikasi test kita beri label app=test.
    
8. **Stage-production**
    
    Label stage bisa kita gunakan untuk menentukan berbagai konfigurasi environment deployment aplikasi kita, misalnya development, testing, performancetest, securitytest, dan production.
    
9. **Jenis-frontend**
    
    kita bisa membuat label jenis aplikasi, misalnya frontend, cache, database, fileserver, dan sebagainya.
    
10. **Selector**
    
    Selector adalah filtering menggunakan label. Misalnya kita ingin mencari semua instance database untuk aplikasi test  yang berjalan di production.
    

# **Fungsi dan Kegunaan kubernetes**

Kubernetes dapat menjadwalkan dan menjalankan kontainer aplikasi pada kelompok mesin fisik atau virtual. Kubernetes  memberikan keuntungan dan manfaat penuh terhadap  Container. Kubernetes menyediakan infrastruktur untuk membangun lingkungan pengembangan yang benar-benar kontainer-sentris.

1. **Exercise**
2. **Jelaskan menurut kalian perbedaan antara kubernetes dengan Docker !**
3. **Jelaskan peran aplikasi Kubernetes dalam dunia devops !**