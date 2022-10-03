# 2. Setup dan Installasi Terrafom

Created: July 25, 2022 3:07 PM

# **Instalasi Terraform**

Terraform tersedia pada berbagai platform mulai dari Windows, Linux dan Mac. Setiap platform juga memiliki caranya sendiri untuk menginstalkan Terraform. Untungnya, semua sudah ada dokumentasinya yang bisa di lihat [di sini](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started).

Pada saat modul ini dibuat, Terraform memiliki versi stable di versi 1.1.7. Berikut beberapa cara untuk menginstalkan Terraform pada mesin kita.

## ***Linux***

Untuk menginstal Terraform pada Linux, kita cukup menambahkan repository Terraform dan menginstalkannya menggunakan package manager pada distro yang dipakai.

```bash
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl

curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -

sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"

sudo apt-get update && sudo apt-get install terraform
```

## ***Windows***

[Chocolatey](https://chocolatey.org/) adalah sistem package management open source dan gratis untuk Windows. Instal paket Terraform dari baris perintah.

```bash
choco install terraform
```

## ***Mac***

Homebrew adalah sistem package management open source dan gratis untuk Mac OS X. Instal formula resmi Terraform dari terminal.

Pertama, instal tap HashiCorp, tempat penyimpanan semua paket Homebrew kami.

```bash
brew tap hashicorp/tap
```

Sekarang, instal Terraform dengan hashicorp/tap/terraform.

```bash
brew install hashicorp/tap/terraform
```

# **Verify Installation**

Ketikan **terraform** **version** di terminal, maka akan muncul seperi dibawah ini.

![*Hasil Installasi Terraform*](https://lh6.googleusercontent.com/WKA31A71AzzdVVm77ttvbhjTtzzfaPXEbuYbGQDOFaXBEeCG-77ecY5G_pcPQ1tOZl2Qlb8QmqcuraFzIoysCkvh9gAeyt_V6Ji7X6xlN-CfajFP3e04XOWig4bYfK_3i9MTi51yNWUWOrNmKAj2IQ)

*Hasil Installasi Terraform*

# **Download Konfigurasi Terraform**

Ada beberapa konfigurasi terraform yang sudah didesain secara best practice dan akan dibahas dibagian selanjutnya, maka dari itu kita harus mendownloadnya terlebih dahulu. Berikut merupakan link nya.

```bash
git clone https://github.com/sdcilsy/terraform-aws.git
```

# **Setup Credential AWS**

Pada bagian ini kita akan mencoba untuk mengakses AWS menggunakan terraform , hal yang harus di siapkan adalah credential yang berguna untuk autentikasi ke AWS. Untuk membuat credential sudah kita bahas pada bab sebelumnya, harusnya kalian sudah dapat membuat sebuah credential yang siap untuk digunakan.

![https://lh4.googleusercontent.com/E6XIi1LngSWX_67yt29uWgcupZvq3F_bR9ClCcjG0SrRlkYbMivPxwHntk3z2j1pLmSSVZUR6SJSoUwLg0sPPBMJ3znZLnc2C0qtvrDtMeIZyyNcfVjDNRPAm2axksfsoud0BUCT-hc8VL1a4ISXIQ](https://lh4.googleusercontent.com/E6XIi1LngSWX_67yt29uWgcupZvq3F_bR9ClCcjG0SrRlkYbMivPxwHntk3z2j1pLmSSVZUR6SJSoUwLg0sPPBMJ3znZLnc2C0qtvrDtMeIZyyNcfVjDNRPAm2axksfsoud0BUCT-hc8VL1a4ISXIQ)

Berikut adalah **Access key ID** dan **Secret access key** seperti gambar di atas, selanjutnya kita simpan atau catat key tersebut yang nantinya akan kita gunakan pada terraform untuk mengakses akun AWS.

Kita juga bisa menggunakan **AWS CLI** sebagai pengganti input access_key dan secret_key pada block **provider aws**, jadi kita tidak menggunakan variable **aws_access_key** pada variable.tf begitu juga dengan private key.

![https://lh4.googleusercontent.com/QCTGtx8YnnXhAvtPvSvqfk9DQ6wmzLoQgoQyaBJ46y5TZE55zoQjEXH9h7tzqo-ZQcHaksbH0kd9MdOqGMGUvaK9OROHqn93Vsl_sdolk7u-W7uBExZxfJhBDqA2uE4Xdo7ASm8ghsamKAo3N20o-g](https://lh4.googleusercontent.com/QCTGtx8YnnXhAvtPvSvqfk9DQ6wmzLoQgoQyaBJ46y5TZE55zoQjEXH9h7tzqo-ZQcHaksbH0kd9MdOqGMGUvaK9OROHqn93Vsl_sdolk7u-W7uBExZxfJhBDqA2uE4Xdo7ASm8ghsamKAo3N20o-g)

# **Membuat Key Pair**

Kita membutuhkan key pair untuk mengakses instance yang akan dibuat. Jika kita tidak mendeklarasikan **key_name** pada **resource aws intance**, kita tidak akan dibuatkan key pair oleh Terraform.

Maka dari itu, kita bisa membuat private key terlebih dahulu secara manual atau dengan resource [aws_key_pair](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/key_pair).

Pada praktikum ini, saya menggunakan key-pair dengan nama **taufik_kurikulum_kp** yang sudah disimpan di local machine.

# **Membuat Security Group (optional)**

Pada kasus tertentu, kita membutuhkan instance kita untuk dapat menerima traffic custom. Oleh karena itu, kita bisa saja membuat Security Group untuk instance kita.

Jika kita tidak membuat Security Group, maka terraform akan menggunakan default security group yang ada pada vpc.

Pada praktikum ini, saya menggunakan Security Group dengan id **sg-0d1878abf7b359496** dengan rule sebagai berikut.

![https://lh3.googleusercontent.com/iJkQcgADkg-k1_Pw2DieRqmFDRRMyYnPzJGPk8GCPIs-RTF360gwZYMe6JR15LqREuScy94A32XD_Muxfj2A1wlgvqK45CuQ_R1ujXlZ5lUA3l9Ob9BrHsTzcs8usud_2HrlXXMlut-9OzyjlIL1Qg](https://lh3.googleusercontent.com/iJkQcgADkg-k1_Pw2DieRqmFDRRMyYnPzJGPk8GCPIs-RTF360gwZYMe6JR15LqREuScy94A32XD_Muxfj2A1wlgvqK45CuQ_R1ujXlZ5lUA3l9Ob9BrHsTzcs8usud_2HrlXXMlut-9OzyjlIL1Qg)