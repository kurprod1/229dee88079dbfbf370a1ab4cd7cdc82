# 2. Project For This Section

Created: August 3, 2022 1:40 PM

# Project ID : DO-CLO-P4

Untuk Mengguide teman teman peserta dalam meraih goals yang sudah di set, kami akan memberikan tugas pada awal pembelajaran sebagai acuan dan pembanding antara goals yang sudah diset dan pemahaman materi secara pararel.

# Requirement

1. Buat sebuah **VPC** dengan 3 subnet (2 subnet private, 1 subnet public). 
    1. Setting Konfigurasi Subnet, Gateway, dan NAT pada VPC yang sudah dibuat!
2. Buat sebuah **EC2** dengan spesifikasi:
    1. type : t2.micro
    2. VPC : VPC yang dibuat dipoin 1
    3. disk : 8 GB
    4. Webserver NGINX terinstall
    5. Konten website adalah [https://github.com/sdcilsy/landing-page](https://github.com/sdcilsy/landing-page)
3. Jalankan autoscaling ketika CPU usage diatas 70%
4. Buat domain di **Route53** lalu pasangkan subdomain **web** ke aplikasi pada poin 2.e