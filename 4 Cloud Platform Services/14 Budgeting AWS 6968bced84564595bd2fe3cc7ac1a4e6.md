# 14. Budgeting AWS

Created: July 19, 2022 10:13 AM

Berbicara tentang uang adalah merupakan hal yang cukup menarik kerena hal ini memang cukup sering melekat kepada kita di kehidupan sehari hari, setiap manusia pastinya membutuhkan uang untuk melakukan pembelian barang dan kebutuhan. Akan tetapi tidak semua orang bisa mengatur anggaran keuangannya sehingga bisa memenuhi kebutuhannya sesuai dengan kondisi keuangan yang ada.

Hal ini menjadi bagian yang sangat cukup penting, bayangkan saja apabila kita memiliki uang yang hanya cukup untuk keperluan pokok selama sebulan, akan tetapi kita tidak dapat mengaturnya sehingga sebelum masuk di akhir bulan kita sudah tidak memiliki uang. Cukup mengerikan bukan ?

[*Pusing dengan anggaran keuangan*](https://lh5.googleusercontent.com/__2QVxcfYHsqwDsy7RIu1l9tK5AqRT1iGhfsvVkvNeQ1U9BX333FocnpqqnoDkoz8lh1cMJMSuIDlYoqiFAlj-qIgvtcDzN58LDKJwU3Fl7MNKMiwrUV9gPJbbn9xLP-mD4Us80YQipvEIq1KZ__YQ)

*Pusing dengan anggaran keuangan*

Materi ini cukup berhubungan dengan pembahasan mengenai profesi kita sebagai devops engineer. Menjalankan aplikasi dan teknologi canggih yang bisa membuat pekerjaan kita menjadi lebih mudah tidaklah cukup, semua akan menjadi percuma apabila perusahaan tidak dapat membayar semua teknologi canggih yang sudah kita rancang sedemikian rupa.

Alhasil pengeluaran dari teknologi yang kita rancang akan membludak tapi belum bisa membuahkan hasil yang maksimal karena anggaran keuangan sudah habis duluan untuk membayar tagihan, masih untung apabila perusahaan kita mendapat suntikan dana dari investor, kalau tidak ? Cukup bisa membuat kepala ini pusing semalaman.

Maka dari itu kita akan coba belajar mengenai budgeting. Materi ini akan kita lebih fokuskan  pada budgeting akun AWS yang kita miliki, karena nantinya semua aktifitas pembelajaran yang kita jalankan akan menggunakan AWS Cloud tentunya.

Mungkin akan ada beberapa layanan yang sering dan tidak sering kita gunakan, maka kita bisa lebih memprioritaskan alokasi dana yang kita miliki untuk layanan yang sering digunakan dan bahkan mungkin layanan yang tidak kita gunakan dapat kita matikan agar tidak memakan cost dengan percuma.

# **Tujuan**

Di section ini, peserta diharapkan sadar terhadap penggunaan setiap layanan, akan berimbas pada pengeluaran rutin AWS. Dan siswa diharapkan mampu menghitung biaya pengeluaran rutin ketika merancang solusi cloud. Hitungan biaya yang timbul dalam suatu solusi cloud merupakan salah satu pertimbangan apakah sebuah rencana solusi bisa diterima semua pihak.

# **Type Pembayaran**

Untuk dapat melakukan management billing, kita harus mengetahui terlebih dahulu apa saja type pemayaran yang dapat kita gunakan pada saat menggunakan AWS yang diantaranya adalah sebagai berikut.

## **Pay-As-You-Go / On-Demand Pricing**

Metode ini merupakan tipe pembayaran paling populer karena paling mudah dengan biling perjam. Biasanya metod ini dianjurkan untun mesin/service yang masih dalam mode riset sehingga membutuhkan perubahan masa pakai maupun tipe mesin sesering mungkin.

## **Reserved Instance**

Metod ini merupakan metod pembayaran langganan. Satuan billing dihitung dalam pembulatan perbulan. Metod ini dianjurkan untuk mesin/service yang sudah ditemukan spek stabil jangka panjangnya. Sehingga kecil kemungkinan ada perubahan spek lagi. Dalam penerapannya, metod ini menghasilkan harga per service lebih murah untuk pemakaian dalam jangka panjang, misal kontrak setahun. Selisih dengan method pay-as-you-go bisa mencapai 75% lebih murah.

# **Point-point yang Menjadi Hitungan Billing AWS**

Didalam seluruh pembelajaran yang akan kita tekuni di sekolah devops ini, ada beberapa service yang akan sering kita jumpai dan kita gunakan. Service ini akan menjadi point-point penting karena akan cukup memakan biaya dari billing AWS yang kita gunakan.

Beberapa servicenya adalah sebagai berikut.

- EC2
- Storage, SSD, HDD, Snapshot, Backup
- RDS
- Elastic IP
- ELB
- S3
- Route53
- Network

Selanjutnya kita akan coba menjelaskan beberapa rincian biaya dari layanan tersebut, untuk detailnya dapat kalian akses pada halaman berikut 

[Pricing](https://aws.amazon.com/pricing/)

Pada penjelasan selanjutnya harga yang tertera adalah untuk region asia pasifik singapore (ap-southeast-1) saja. Harga diregion lain akan berbeda, mungkin bisa lebih murah atau lebih mahal.

## **EC2**

Harga EC2 yang kita bayar hanya menghitung jumlah core dan ram yang digunakan. Oleh sebab itu untuk mempermudah pengguna, AWS telah menyediakan templet tipe server sesuai kebutuhan user. Harga yang tertera biasanya merupakan tarif perjam untuk pembayaran pay-as-you-go. Sedangkan untuk hitungan perbulan dihitung sebagai 1bulan = 720jam. Harga ini juga akan berbeda untuk tiap region, jenis generasi processor dan type peruntukan.

Type yang akan kita gunakan lebih sering adalah tipe

- T2.(xxx)
- T3.(xxx) Kami menyarankan menggunakan tipe t3, sebagai templet tipe server yang menggunakan generasi processor lebih baru.

Detailnya dapat kita lihat pada halaman : 

[EC2 On-Demand Instance Pricing - Amazon Web Services](https://aws.amazon.com/ec2/pricing/on-demand/)

Berikut terlampir harga type EC2 untuk region AP-2 (Singapore) dengan OS Ubuntu Linux.

[*Harga EC2 Linux AWS*](https://lh3.googleusercontent.com/CsVgk1_Mcipe12qF29KIxmKmG7e3Tq2Vbq1KEU_LaoafmSm_fY60xjMZHVpewzc2ohvFtq61VJKoj_iyIUEkdLk7vd6CUvbt1ydZ6ssDoMKVv0KWKGvac5g6oEXnbYPgw-cLqvrlKnSY9-NQoLpFnQ)

*Harga EC2 Linux AWS*

## **Storage**

Storage yang digunakan disini adalah EBS (Elastic Block Storage). EBS menyediakan beberapa tipe penyimpanan, diantaranya:

- General SSD (GP2). Ini merupakan tipe penyimpanan yang akan kita pakai secara bawaan.
- EBS Snapshots, Ini adalah tipe penyimpanan yang biasa kita gunakan untuk backup snapshot.

Untuk harga adalah sebagai berikut:

- GP2: $0.12 per GB-month of provisioned storage
- EBS Snapshots: $0.05 per GB-month of data stored

Detailnya dapat kita lihat pada halaman :  

[High-Performance Block Storage- Amazon EBS Pricing - Amazon Web Services](https://aws.amazon.com/ebs/pricing/)

## **RDS**

Untuk database yang kita gunakan disini masih keluarga MySQL dan Postgresql, harga yang dibayar berasal dari jumlah Core dan Ram yang digunakan. Namun komposisi core dan RAM sudah menjadi kesatuan template.

Setelah itu harga RDS ditambah dengan penggunaan storage untuk data, backup dan snapshot. Ini karena untuk mode RDS terdapat mekanisme auto backup snapshot dalam tenggat waktu tertentu.

### ***Harga Resource Compute***

Berikut tipe RDS Mariadb yang biasa dipakai beserta harganya untuk on-demand/pay-as-you-go: [https://aws.amazon.com/rds/mariadb/pricing/?pg=pr&loc=4](https://aws.amazon.com/rds/mariadb/pricing/?pg=pr&loc=4)

[*Harga RDS*](https://lh5.googleusercontent.com/7DWJNgOVzMhbgXrgl9g3JlH8Pr6r7aKlhpdGZWqrExKYOrLCJsdnd3bEklS-K2fXRqYiB6zJNR6voRtm-OWkiUVZL-eKiTOJ7Vqy9mOWGq58eZxa1Hb8t5mpkIw5nXIHqm0uoR6UjQLZoQkD_EeY2w)

*Harga RDS*

### **Harga Storage**

- General Purpose (SSD) Storage $0.138 per GB-month
1. ***Data Transport***
    
    Ini adalah harga yang dibayar untuk bandwith. Harganya memang tidak terlalu mahal. Namun sebagai pos pengeluaran rutin, wajib kita ketahui.
    
2. **Data Transfer IN To Amazon RDS From Internet**
    - All data transfer in $0.00 per GB
3. **Data Transfer OUT From Amazon RDS To Internet**
    - Up to 1 GB / Month $0.00 per GB
    - Next 9.999 TB / Month $0.12 per GB

Detailnya dapat kita lihat pada halaman :

[Managed Relational Database - Amazon RDS Pricing - Amazon Web Services](https://aws.amazon.com/rds/pricing/)

## **Elastic IP**

Elastic IP adalah alamat IP yang kita sewa sehingga IP ini secara teknis hanya untuk kita dan tidak bisa digunakan orang lain. Sehingga jika tidak digunakana kan dikenakan biaya rutin sebagai berikut:

- $0.005 per additional IP address associated with a running instance per hour on a pro rata basis
- $0.005 per Elastic IP address not associated with a running instance per hour on a pro rata basis

## **S3**

S3 adalah layanan penyimpanan object. bentuk penyimpanan berupa bucket. Berikut harga layanan ini:

1. **S3 Standard - General purpose storage for any type of data, typically used for frequently accessed data**
    - First 50 TB / Month $0.025 per GB
    - Next 450 TB / Month $0.024 per GB
    
    Detailnya dapat kita lihat pada halaman : 
    
    [Amazon S3 Simple Storage Service Pricing - Amazon Web Services](https://aws.amazon.com/s3/pricing/)
    

# **Route53**

Route53 merupakan layanan pengelola DNS. Materi ini sudah kita bahas pada pembahasan sebelumnya. Berikut tarifnya.

1. **Hosted Zones and Records**
    - $0.50 per hosted zone / month for the first 25 hosted zones
    - $0.10 per hosted zone / month for additional hosted zones

## **ELB**

Harga ELB diitung dari banyaknya ELB yang dibuat, tipe ELB dan Banwith yang dihabiskan. Berikut harga perkiraan ELB:

- $0.028 per Classic Load Balancer-hour (or partial hour)
- $0.008 per GB of data processed by a Classic Load Balancer

Detailnya pada halaman berikut :

[Network Traffic Distribution-Elastic Load Balancing Pricing -Amazon Web Services](https://aws.amazon.com/elasticloadbalancing/pricing/)

# **AWS Calculator Billing**

AWS menyedikan simulasi berapa harga yang harus dibayar untuk satu bulan jika menggunakan layanannya. Kalkulator dapat diakses pada tautan berikut: 

[Amazon Web Services Simple Monthly Calculator](https://calculator.s3.amazonaws.com/index.html)

[*Kalkulator AWS*](https://lh5.googleusercontent.com/_8QLF-J3c61DpGl2RCC2cs_peWGUG5VhWpBXrlpjEox_OVbMSyLisWs71WLMJy8OAxobKIdmPqCajydbwSNt7ZqBS-R38aBZBZJ8Ou8mMwO1kouqbQcPyManoep0hnVPzefLKRWZ8uhweCSvV9PQYg)

*Kalkulator AWS*

Cara menggunakannya tidak begitu sulit, kita hanya perlu memasukan layanan apa saja yang kita gunakan beserta dengan spesifikasi dari layanan tersebut. Maka kalkulator akan melakukan akumulasi dari semua layanan yang akan kita gunakan dalam jangka waktu satu bulan.

Dengan begini kita dapat memperkirakan pengeluaran yang akan kita lakukan dalam rentan satu bulan ini, sehingga kita dapat mempersiapkan dengan matang pengeluaran yang akan kita bebankan diakhir bulan.

[*Contoh hasil kalkulasi AWS*](https://lh5.googleusercontent.com/dLh3ZKqYNFT-5i09i3KYu9aTz60D-HHr5v6zXEIH01I1_9mBPu7RFqL0HIsb2qRthpAImN35xttfkCEBPKSh6U1AnWIehSmHNQq8GfHW1v4jrPDf2HazJGQLNCu14fG_-F6plUaDGHaZcMkoxAcN1g)

*Contoh hasil kalkulasi AWS*

# **Mengakses Menu Billing AWS**

Menu ini memungkinkan kita memantau berapa budget yang sudah terpakai di bulan berjalan. Menu dapat diakses dari menu kanan atas. **Nama Account >My Billng Dashboard.** Atau pada tautan [https://console.aws.amazon.com/billing/home?region=ap-southeast-1#/](https://console.aws.amazon.com/billing/home?region=ap-southeast-1#/)

Menu ini dapat dilihat untuk user root atau user IAM lainnya yang sudah mendapat akses billing. Billing bulanan akan dihitung pertanggal 1 tiap bulannya. Setelah itu sistem akan mengirimkan tagihan pemakaian ke alamat root account untuk segera dibayarkan sebelum jatuh tempo.

Pembayaran bisa menggunakan auto debet (CC) atau penagihan manual. Keterlambatan pembayaran tagihan dari masa tenggang pembayaran bisa mengakibatkan akun aws diblok, layanan server non aktie. Sehingga mengundang resiko kehilangan data di server. Berikut tampilan biling dashboard:

[*AWS Billing Console*](https://lh6.googleusercontent.com/Qujh10zNjK1uLn7MqgpwlbOiRw-9fxgCJIsukVJojWZP50GM4PODgTx_PIBdfZBsyvET0DC4BNkCpOEVxFx6yaIVFVZypJc30tHCNIcKAxB-WH3NeQbVvAYtp4PHHLjEdWJGII33_bLpuozakAwFqQ)

*AWS Billing Console*

Pada bagian tersebut kita dapat melihat berapa kalkulasi penggunaan dari billing yang sudah kita gunakan, untuk melihat secara detail apa saja layanan yang sudah kita gunakan, kita dapat memilih menu **Bills** yang ada disamping. Maka munculah detail dari penggunaan layanan seperti berikut.

[*Details Bills AWS*](https://lh4.googleusercontent.com/e0Sz61sCXa1Kkn8QaRUTwoxoHtJzJOK61AbB7R0pObm7WTOH_RWWyUuCaieelAau-I1is1QzwikxF_7IO3bTrKxy6vXCs4D2fX1Hu6UZoWg0v4JNbSmEgzya5AtVonFo5VXkFxT75X7s34U24600-A)

*Details Bills AWS*

# **Membuat Perencanaan dengan AWS Budgets**

Setelah kita bahas panjang lebar mengenai pentingnya merencanakan budgeting untuk kebutuhan layanan, membahas mengenai harga setiap layanan yang ada pada AWS. Sekarang kita akan coba membuat perencanaan budget.

Dengan membuat perencanaan di AWS Budget kita akan diberikan peringatan apabila cost dari layanan kita sudah hampir melebihi dari anggaran yang kita buat sebelumnya.

Untuk membuat perencanaan baru, masih dalam billing page kita masuk kedalam menu budgets, lalu klik **Create a budget.**

[*Billing Menu*](https://lh6.googleusercontent.com/7ZjkDjuxtwdV7tMG9jA0G4-bMB2JPhm_gwiHDhWMIp6iND8DdaSg5SUOUUrnxJSOYicx1W6uIFOcKG4jNsgsWwgjCK3nNP2NU1dhPIxEbW2q5ki7TDzKoxZPMxhKDWfeFd4-w0h198pl9zoU-Itj3Q)

*Billing Menu*

Selanjutnya masuk kedalam menu budget, lalu pilih type yang akan kita manage. Di pembahasan ini kita akan coba manage cost budget, klik **Set your budget** untuk melanjutkan.

[https://lh3.googleusercontent.com/piw0ZFLVt4OuoqEEJkSbh82UfPca3C1GUMv3KDCkVhZ20w3_g-RJumX-BKuYtyHegiJkUD5lYJCdkijanl1wxQqTiVehkEo_O9vvzmVTsJHK5uTP-6GEevDzc5_P75jM93x57Ol6xAY9Qx9DLww8Sg](https://lh3.googleusercontent.com/piw0ZFLVt4OuoqEEJkSbh82UfPca3C1GUMv3KDCkVhZ20w3_g-RJumX-BKuYtyHegiJkUD5lYJCdkijanl1wxQqTiVehkEo_O9vvzmVTsJHK5uTP-6GEevDzc5_P75jM93x57Ol6xAY9Qx9DLww8Sg)

Isikan name budget lalu pilih periode budget yang akan dipantau serta mulainya program budgeting tersebut.

[https://lh6.googleusercontent.com/0V4MM3bF8HwoqLP2NI-TLWqaU8g-Fmwa8d1XmlHey0HS3t3Z1MIN9opB6FKmKzCKDzyKLXb2JsjpfltLQ4AXnuGRAk3Z0QA8nLmfK2vkZLMIxlSsATLNDG8zZRqDskLuN1pK9xWVOGSCH7il2fuHkQ](https://lh6.googleusercontent.com/0V4MM3bF8HwoqLP2NI-TLWqaU8g-Fmwa8d1XmlHey0HS3t3Z1MIN9opB6FKmKzCKDzyKLXb2JsjpfltLQ4AXnuGRAk3Z0QA8nLmfK2vkZLMIxlSsATLNDG8zZRqDskLuN1pK9xWVOGSCH7il2fuHkQ)

Isikan informasi total budget yang akan kita setting, kita juga dapat membuat budget yang berbeda di setiap bulannya dengan memilih mounthly budget planning. Klik Configure allerts untuk melanjutkan.

[https://lh5.googleusercontent.com/vLYC18-xGV2NN-DHSRfRPIYPH9hFJRfm8Xwfr_fKU1fVlQsPZLnN-GIoX6b0lrdtVf89gv3LKtXn6j1n0l4rnTIoZuwTAHFypjDtOGrbD7jsrG4OcPntWHTsWzVEJp0rrmu9Kady5x-yaDHxFbqZgA](https://lh5.googleusercontent.com/vLYC18-xGV2NN-DHSRfRPIYPH9hFJRfm8Xwfr_fKU1fVlQsPZLnN-GIoX6b0lrdtVf89gv3LKtXn6j1n0l4rnTIoZuwTAHFypjDtOGrbD7jsrG4OcPntWHTsWzVEJp0rrmu9Kady5x-yaDHxFbqZgA)

Lalu klik **Configure Tresholds**

[https://lh6.googleusercontent.com/moEu4M5O__SUlWKuVV77M7wPK5B0ni-MhaYAut7nh3nX1EhDnLeXaGNQkMr2gTh2VZtTGnsF5LRVMiovyBqIQkr7sEuZo0EVBM3QOcEM8qbru4mzSZNf8ayaVUna2V3uVHE3eOr90u99uVhXUL4WDA](https://lh6.googleusercontent.com/moEu4M5O__SUlWKuVV77M7wPK5B0ni-MhaYAut7nh3nX1EhDnLeXaGNQkMr2gTh2VZtTGnsF5LRVMiovyBqIQkr7sEuZo0EVBM3QOcEM8qbru4mzSZNf8ayaVUna2V3uVHE3eOr90u99uVhXUL4WDA)

Selanjutnya setup persentase usage untuk alarm nantinya, lalu email untuk mengirimkan alert bila sudah mencapai batasnya.

[https://lh5.googleusercontent.com/Hik-V_jz3bpJ4BqIJauZzu5RSEnXZttTUjqlMhBujFRz1t1wOVQyNjnmXdZOf1-EYl4dPidzK6DWQuHzsUH1sbAgoqmTNSF7pRewzYGK2w4LHMA6KCIwWamv_aCza09E29Ih_Ph_jwb0iNkjADfYyw](https://lh5.googleusercontent.com/Hik-V_jz3bpJ4BqIJauZzu5RSEnXZttTUjqlMhBujFRz1t1wOVQyNjnmXdZOf1-EYl4dPidzK6DWQuHzsUH1sbAgoqmTNSF7pRewzYGK2w4LHMA6KCIwWamv_aCza09E29Ih_Ph_jwb0iNkjADfYyw)

[https://lh6.googleusercontent.com/_t0ZcIqxQM8ITizxWsZHSNrUUnEBWdu9ydhJCBYn7I1VdOTt453kvxJRnb-Gp_CWINZ9mV6iZGayroruu7q-Xs3FB7ljEp_6UcwEVP8nK7O99EWfEmF0CztKmCEZa3im3iDpKrCdp_7ZY4l4AU4ZtA](https://lh6.googleusercontent.com/_t0ZcIqxQM8ITizxWsZHSNrUUnEBWdu9ydhJCBYn7I1VdOTt453kvxJRnb-Gp_CWINZ9mV6iZGayroruu7q-Xs3FB7ljEp_6UcwEVP8nK7O99EWfEmF0CztKmCEZa3im3iDpKrCdp_7ZY4l4AU4ZtA)

Selanjutnya kita akan melihat preview dari hasil setup yang telah kita lakukan, klik create untuk melanjutkan.

[https://lh6.googleusercontent.com/fTN0WizYA_MpE_87CAMB0odzt5Dgrp8WOZXKoDoLe7C-XatfpIgR0Cro_esCzNNq7aJxnGFTn8PYoWFCMI_vsLCUC2b_t6o9088qm7sMOR6m1zYvD_swo-2kfmUGg9cpwXwyfhy3sp3bE0GR7ING7w](https://lh6.googleusercontent.com/fTN0WizYA_MpE_87CAMB0odzt5Dgrp8WOZXKoDoLe7C-XatfpIgR0Cro_esCzNNq7aJxnGFTn8PYoWFCMI_vsLCUC2b_t6o9088qm7sMOR6m1zYvD_swo-2kfmUGg9cpwXwyfhy3sp3bE0GR7ING7w)

Yeay ! Dengan begini kita telah berhasil melakukan setup budget AWS, jadi nanti apabila usage cost yang kita miliki sudah 80% mendekati planing awal. Maka kita akan mendapatkan email bahwa cost sudah melebihi batas dan kita dapat menyesuaikan kebutuhan kita.

![Untitled](14%20Budgeting%20AWS%206968bced84564595bd2fe3cc7ac1a4e6/Untitled.png)