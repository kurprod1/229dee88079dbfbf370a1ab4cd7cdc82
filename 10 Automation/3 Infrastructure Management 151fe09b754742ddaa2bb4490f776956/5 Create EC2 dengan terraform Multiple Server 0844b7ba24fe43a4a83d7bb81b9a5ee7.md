# 5. Create EC2 dengan terraform (Multiple Server)

Created: July 25, 2022 3:26 PM

Pada bagian ini kita akan mencoba untuk membuat beberapa server sekaligus dengan menggunakan terraform seperti di bawah ini. Tahap pertama yang harus kita lakukan adalah membuka file variables.tf pada **ec2/**.

```bash
variable "instance_count" {
    default = 1
}
```

Lalu ubah menjadi seperti dibawah ini dengan menambahkan instance_count dan nilainya.

```bash
variable "instance_count" {
    default = 3
}
```

Instance count, berguna untuk mengatur jumlah server yang ingin kita deploy pada AWS. Untuk menjalankan program tersebut maka jalankan perintah berikut.

```bash
terraform plan
```

Hasil perintah di atas akan menghasilkan seperti gambar dibawah ini.

![https://lh3.googleusercontent.com/IbR8_9eq4kvClnJRSPfx7ZF3sMt1SDe90ryyydva9WTjwm310hxGAX1n5fvf8ZqO-ri1AJI1hy9bvrJ-GcR3nzgJ-4sSeAQEaAy8jOqqvNmXPAyXokJaKs-JTktwc_NDIXBB9dWLkwq5uCZXUhohJg](https://lh3.googleusercontent.com/IbR8_9eq4kvClnJRSPfx7ZF3sMt1SDe90ryyydva9WTjwm310hxGAX1n5fvf8ZqO-ri1AJI1hy9bvrJ-GcR3nzgJ-4sSeAQEaAy8jOqqvNmXPAyXokJaKs-JTktwc_NDIXBB9dWLkwq5uCZXUhohJg)

Selanjutnya apply terraform yang sudah kita setting tadi.

```bash
terraform apply
```

![https://lh3.googleusercontent.com/w9-6BiR2IT9pdWTFo3BD_R-D818swEGsmFe09xijkQpj2ZXjHUsISqDeoI1ZCk--GwlMumSEaHqp9XYHS5Sl5g3MnR1F_1iWVAJrHU-wvP-_4iWZcmdcfINMPe9csn4pygDDmOnz2cR5YxGDCO5OCA](https://lh3.googleusercontent.com/w9-6BiR2IT9pdWTFo3BD_R-D818swEGsmFe09xijkQpj2ZXjHUsISqDeoI1ZCk--GwlMumSEaHqp9XYHS5Sl5g3MnR1F_1iWVAJrHU-wvP-_4iWZcmdcfINMPe9csn4pygDDmOnz2cR5YxGDCO5OCA)

![https://lh3.googleusercontent.com/ntIf8-Fp_759uSZ7UeYFWN9RLBhS4NQki96TRxGJbN6mndfz9ypmXA6EBWMvcW5QonHWpbSdSzajdkU7aDUqF_8V9F2-Re5yFNN6uwAWTbg1qsniJxwwnN47vRFHQaEg2dwVc_RJQqGZPZB0DcOAOA](https://lh3.googleusercontent.com/ntIf8-Fp_759uSZ7UeYFWN9RLBhS4NQki96TRxGJbN6mndfz9ypmXA6EBWMvcW5QonHWpbSdSzajdkU7aDUqF_8V9F2-Re5yFNN6uwAWTbg1qsniJxwwnN47vRFHQaEg2dwVc_RJQqGZPZB0DcOAOA)

Jika muncul gambar seperti di atas maka proses berjalan dengan baik, kita dapat melihat dashboard EC2 maka akan muncul 3 instance yang telah kita buat.

![*Hasil Multiple Server*](https://lh6.googleusercontent.com/ksL4MZgq52x9Lk5skzxk2SXZy-rLBwaFnOMX5SnVjkXaS30bgeKoBi2ts0UEfaGCtsCwH25RHHO3Gbo966lAG6NdQMGMeAImpzejBrCwjc7f6t03DXyY6Eas7F9koJXHrcY368SLMVkKcxB2OGwOAQ)

*Hasil Multiple Server*

# **Exercise**

Soal Praktek :

1. Build 3 buah instance baru menggunakan Sistem Operasi Ubuntu Server 18.04.
2. Pastikan ketiga instance tersebut sudah terinstallkan webserver dan database server yang dapat diakses.
3. Semua tesebut dibuild menggunakan terrafrom.