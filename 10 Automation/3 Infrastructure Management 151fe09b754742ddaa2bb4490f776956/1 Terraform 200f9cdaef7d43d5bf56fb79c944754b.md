# 1. Terraform

Created: July 25, 2022 3:06 PM

# **Pengenalan Terraform**

**Terraform** adalah **Infrastructure as Code** dan salah satu tool Automation pada AWS.  Infrastructure as Code adalah proses penyediaan IT infrastruktur dimana sistem dibangun dan dikelola melalui kode secara automasi (otomatis), bukan secara manual. Atau bisa disebut juga bahasa kerennya **Programmable Infrastructure**.

![*Logo Terraform*](https://lh4.googleusercontent.com/XUmkQwb7Mqhe7ItfEkG5MmSaY0dokrvSTlJuiLFaR1D5hGzJFTDPOZ33AmdCTowuVL49lFgJ06Bf9D0IfsSL47NiWZ6eg7jzEWJfCpqDgqY3yLDt8aXBzbpR4T1qpl-XCJNSc3JzJaOUXtgfDuwgnA)

*Logo Terraform*

Dengan menggunakan kode dan meng-automasi. Proses setting dan konfigurasi baremetal, virtual mesin, cloud computing baik itu instalasi baru atau perubahan konfigurasi dapat dilakukan secara cepat, mudah, dan berulang. Selain itu bermanfaat sebagai dokumentasi juga, jadi siapapun akan tahu konfigurasi server, kebutuhan aplikasi server dan sebagainya.

![*Ilustrasi alur kerja terraform*](https://lh6.googleusercontent.com/Nx1bYIvtBTk6beE2C4gIAGal_sMu3hy4OT9RHQhdM8Z5TdTkW3trKuj9HpzPv8CC3I1pVR1gkZ9Y2yvmMqrQHt2zWIKxfmWpAQfKn_fxOV3hRp8FsvN58raktZa_1F-YmJ_ECR55AbVTPHLGR04_Ww)

*Ilustrasi alur kerja terraform*

Gambar diatas merupakan salah satu ilustrasi dari sistem automasi terrafrom, disana ketika program yang sudah kita buat dijalankan, dia akan mencoba untuk mengecek identitas credential IAM yang kita masukan. Setelah tervalidasi, baru program akan mengekseskusi untuk membuat sebuah EC2 baru di AWS. Setelah proses pembuatan selesai, maka reportnya akan dikirimkan kembali kepada alamat awal si program, sehingga kita bisa tau proses tersebut error atau berhasil.

Selain AWS, ada juga beberapa provider yang support untuk menggunakan automasi dari terraform. Provider yang disupport Terraform adalah sebagai berikut :

- AWS, GCE, Azure, OpenStack, DigitalOcean, Docker, CloudStack, Heroku, vSphere, vCloud (Cloud Infrastructure)
- Chef, Rundeck (Configuration Management)
- CloudFlare, DNSMadeEasy, Dyn, DNSimple (DNS provider)
- Mailgun (Email)
- Atlas (Hashicorp workflow engine)
- Consul, PowerDNS (DNS and service registry)
- MySQL, PostgreSQL (Database)
- StatusCake (Monitoring)

# **Fungsi dan Kegunaan Terraform**

1. **Infrastruktur sebagai Kode**
    
    Infrastruktur dijelaskan menggunakan sintaks konfigurasi tingkat tinggi. Hal ini memungkinkan cetak biru pusat data kita akan diversi dan diperlakukan seperti yang kita lakukan pada kode lainnya. Selain itu, infrastruktur dapat dibagi dan digunakan kembali.
    
2. **Automation Plan**
    
    Terraform memiliki langkah "perencanaan" di mana ia menghasilkan rencana eksekusi. Rencana eksekusi menunjukkan apa yang akan dilakukan Terraform saat kita memanggil program. Ini memungkinkan kita menghindari kejutan ketika Terraform memanipulasi infrastruktur.
    
3. **Automation Change**
    
    Perubahan yang rumit dapat diterapkan pada infrastruktur kita dengan interaksi manusia yang sangat minim. Dengan rencana eksekusi dan grafik sumber daya yang disebutkan sebelumnya, kita akan tahu persis apa yang akan diubah dan menghindari banyak kemungkinan *human error.*