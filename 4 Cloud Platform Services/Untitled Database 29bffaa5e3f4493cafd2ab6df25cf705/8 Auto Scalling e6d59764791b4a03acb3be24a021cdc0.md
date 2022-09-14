# 8. Auto Scalling

Created: July 18, 2022 1:09 PM

# **Apa itu Auto Scaling ?**

Auto Scaling merupakan salah satu layanan dari AWS yang bekerja memonitoring aplikasi kita dan secara otomatis menyesuaikan kapasitas untuk mempertahankan kinerja yang stabil. Dengan memanfaatkan informasi trafik yang masuk kedalam layanan instance kita, Auto Scaling dapat mengetahui kebutuhan yang dimiliki oleh pengguna sehingga dia dapat langsung melakukan scaling instance agar kebutuhan trafik terlayani dengan baik.

[*Logo AutoScalling*](https://lh3.googleusercontent.com/Zee8gpqIXcP49RNnF8_CP-8vjZOEUPViYknJ4drPX7rCWV_khDLEfl4Sj6WWHNFu2qcYQfUsrUV_yattaoY6Lcr2k2n4obJsgsSHAxssb7nvxBNxpMhAEtzBF2B6b6wVDPobJQbTj_45jcbDpw)

*Logo AutoScalling*

Auto Scaling memungkinkan layanan web kita bisa bisa menambah jumlah instance ketika load tinggi dan menguranginya ketika load rendah secara otomatis. Dengan Auto Scaling, kita tidak perlu lagi melakukan capacity guessing.

Untuk memaksimalkan layan ini, kita haus mengkombinasikan auto scaling dengan load balancing, sehingga semua server yang melakukan scale up dan scale down akan tetap bisa kita akses menggunakan alamat yang sama dari Load Balancer tersebut.

Sebelum membuat konfigurasi Auto Scaling, kita harus melakukan konfigurasi pada **Launch Configurasion.** Auto Scaling akan secara **otomatis me-launch dan men-delete instance** sesuai beban load dengan mengambil informasi dari template nya yaitu yang sudah dibauat pada launch configuration.

Pada dasarnya Launch Configuration adalah template EC2 yang akan digunakan oleh Auto Scaling, maka pembuatan Launch Configuration pun sangat mirip seperti ketika kita men-setup instance EC2.

1. **Exercise**
2. Cari tahu salah satu contoh pengaplikasian Load balancer pada dunia nyata !

# **Praktek AutoScalling**

## **Persiapan Instance**

Pada bagian ini kita akan coba melakukan praktek untuk membuat sebuah Auto Scalling dari Instance yang kita miliki. Kita akan membuat instance minimal yang aktif pada auto scalling ini adalah 2 dan maksimumnya adalah 6 instance, sehingga nantinya ketika CPU server nya naik maka server akan bertambah 1 persatu hingga mencapai 6 instance.

Pertama yang harus kita siapkan adalah sebuah instance yang akan kita setup untuk AutoScalling dengan rincian berikut :

- Operating System : **Ubuntu 18.04**
- Name Tag : **namapeserta AutoScalling**
- VPC : Gunakan yang sudah dibuat sebelumnya
- Instance Type : **t2.micro**
- Sisanya bisa default disesuaikan

Setelah instance selesai dibuat, selanjutnya kita akan lakukan setup webserver dan webaplikasi pada server instance tersebut. Kalian dapat menggunakan Script yang sudah dibuat sebelumnya untuk menginstall webserver dengan requirement tersebut :

- Apache 2
- Php dan php-mysql
- mysql-server

Setup web aplikasi, jangan lupa untuk membuat user database mysql dan import database dari web aplikasi tersebut.

## **Setup AutoDeployment**

Selanjutnya kita akan melakukan setup auto deployment pada instane yang sudah kita buat, karena nanti instance yang sudah kita buat sebelumnya akan dibuat menjadi sebuah image yang akan di load ketika server menggandakan diri. Maka konten yang ada pada server baru yang digandakan tersebut haruslah sama dengan konten terbaru yang kita miliki.

Sehingga kita buat sebuah automasi dimana ketika server hidup atau digandakan, dia akan otomatis melakukan deploy pada server dengan mengambil source dari github.

Pertama buat script berikut dengan nama **autodeploy.sh** di home server tersebut.

```bash
#!/bin/bash

echo "=============================>"

echo "Downloading Data"

echo "=============================>"

cd

rm -f master.zip

rm -R sosial-media-master

wget https://github.com/sdcilsy/sosial-media/archive/master.zip

echo "=============================>"

echo "Ekstrak File"

echo "=============================>"

sudo apt-get install -y unzip

unzip master.zip

echo "=============================>"

echo "Memindahkan data"

echo "=============================>"

sudo rm -R /var/www/html/*

sudo rm /var/www/html/*

sudo mv sosial-media-master/* /var/www/html/

echo "Setup selesai"

exit 0
```

Bagian hijau tersebut bisa diganti dengan repository yang kalian miliki sendiri. Setelah itu simpan dan beri hak akses pada file tersebut.

```bash
chmod +x autodeploy.sh
```

Selanjutnya kita akan buat script tersebut berjalan pada saat booting, pada ubuntu 18.04 ini kita akan menggunakan cronjob untuk konfigurasinya seperti berikut.

```bash
crontab -e
```

Akan muncul pilihan seperti dibawah ini, pilih editor sesuai yang kalain pahami. Tapi saya sarankan menggunakan nano.

[https://lh5.googleusercontent.com/R8IX4vdPJVVaQXqzjZXVflj8c-7ZK6z7rvyiOOFXzf_UuguuSYPrcQ1d0nxwH9S9Wb-_PlfatvPup4WmZSCyuctzl5qXq9Pe6_AUDxRonueerWyOh4EbuvpSkaFRpRcd9hkGYibpK_Zy1ZrouA](https://lh5.googleusercontent.com/R8IX4vdPJVVaQXqzjZXVflj8c-7ZK6z7rvyiOOFXzf_UuguuSYPrcQ1d0nxwH9S9Wb-_PlfatvPup4WmZSCyuctzl5qXq9Pe6_AUDxRonueerWyOh4EbuvpSkaFRpRcd9hkGYibpK_Zy1ZrouA)

Setelah masuk kedalam editor cronjob, kita pindah ke line paling akhir dan tambahkan script berikut dibawahnya.

```bash
@reboot sh /home/ubuntu/autodeploy.sh
```

Setelah itu simpan konfigurasi tesebut, dan kita bisa ujicoba keberhasilannya dengan melakukan reboot pada instance tersebut.

## **Setup AMI**

Pada bagian ini kita akan coba membuat image dari instance tadi, image ini disebut dengan AMI. Untuk membuat AMI, kita hanya perlu memilih instace lalu klik **Action > Image and templates > Create Image.**

[https://lh3.googleusercontent.com/kx91vbsUE96toxpp4ga_NDcr0_iIDhKrL5zDsKshuNiS1at3FvGnOj1prOisKCFzHoYhwivKWQ1H6rxghFXjoYq1MxpF9wgx9ByjxVeEjWYdpPl1rH-bCWWmDOoBELRuP2saM8J4SH9c83j-Pw](https://lh3.googleusercontent.com/kx91vbsUE96toxpp4ga_NDcr0_iIDhKrL5zDsKshuNiS1at3FvGnOj1prOisKCFzHoYhwivKWQ1H6rxghFXjoYq1MxpF9wgx9ByjxVeEjWYdpPl1rH-bCWWmDOoBELRuP2saM8J4SH9c83j-Pw)

Setelah itu akan masuk ke menu Create image, isikan deskripsi AMI yang akan kita buat dan setelah itu klik **Create Image.**

[https://lh4.googleusercontent.com/dLMy44y4knKK_DiZgmxCQeb2YRnCClMm7J73alNmno6yuDLCEXfbVAyvuAqhWHMgag9kyC3U8wnAv44lhSGJfuHS6HMT7O7Ic5WzFsXJGJ-K__KhEmpzdyMfwtDewFmK3AI4j3iEgcBZMvBd6w](https://lh4.googleusercontent.com/dLMy44y4knKK_DiZgmxCQeb2YRnCClMm7J73alNmno6yuDLCEXfbVAyvuAqhWHMgag9kyC3U8wnAv44lhSGJfuHS6HMT7O7Ic5WzFsXJGJ-K__KhEmpzdyMfwtDewFmK3AI4j3iEgcBZMvBd6w)

Untuk mengecek AMI yang sudah kita buat, kita bisa masuk kedalam menu AMI yang ada pada **dashboard EC2** seperti berikut. Tunggu proses pending pada AMI hingga selesai menjadi **available**.

[*Instance yang sudah menjadi AMI*](https://lh3.googleusercontent.com/pHXExwouRUAFtFcxyAoeZdf_2SUEQx1nDhveJ9HLCSR_Zsj1rUmJFv7CJScB3UWs_3TH5deLh_63GVEVts05yIDCWvkQdp7dfhnLN0LsjHCpOLGXG2DihHvrtvwr8xMB2IrXrRxETl3pjJXH8g)

*Instance yang sudah menjadi AMI*

## **Setup Launch Configuration**

Sekarang kita akan masuk kedalam setup autoscaling tahap awal, disini kita akan melakukan konfigurasi pada **launch configuration** dan mendaftarkan IAM yang sudah kita buat tadi. Pertama kit masuk ke dalam menu **Launch Configuration** lalu pilih tombol **Create launch configuration**.

[https://lh5.googleusercontent.com/RfxkrxI-0jtqTIL59l71PLBPoDMX9tumPexBAinimu_CpzlBu3jQhcdP6KsW6K22Zx6DXO4SoTTSfSiv4iU4TBUxTj8UaKoHqdarRzpizEkVh_H-ypqeoK-b9xbPVhbJ3ZKqMgLj0gqo_pVLWw](https://lh5.googleusercontent.com/RfxkrxI-0jtqTIL59l71PLBPoDMX9tumPexBAinimu_CpzlBu3jQhcdP6KsW6K22Zx6DXO4SoTTSfSiv4iU4TBUxTj8UaKoHqdarRzpizEkVh_H-ypqeoK-b9xbPVhbJ3ZKqMgLj0gqo_pVLWw)

Selanjutnya kita akan diarahkan pada launch configuration, pilih AMI yang sudah kita sediakan sebelumnya.

Setelah itu pilih instance type yang akan kita gunakan, disini saya memilih **t2.micro**.

Selanjutnya isikan detail konfigurasi launch instance yang akan kita gunakan, jangan lupa check monitoring cloudwatch agar kita bisa melihat traffic yang keluar dari server tersebut.

[https://lh5.googleusercontent.com/DYZ_RM5pxHiiQn58y-i93U0ZtV7OOpDKiA4hvb8qU4i1aVSjbqM4Qu_RWTpwU2JCklOSxxkpOnsA0-Sn7hvMHyBLz3yUS9UQz1vy33VZnM5b6QuywPlZhgYcO1U6zeZNtoLzS_Jl4fcbis1mlQ](https://lh5.googleusercontent.com/DYZ_RM5pxHiiQn58y-i93U0ZtV7OOpDKiA4hvb8qU4i1aVSjbqM4Qu_RWTpwU2JCklOSxxkpOnsA0-Sn7hvMHyBLz3yUS9UQz1vy33VZnM5b6QuywPlZhgYcO1U6zeZNtoLzS_Jl4fcbis1mlQ)

[https://lh5.googleusercontent.com/eMK-wju3oIdPuwnRJ4ATF8L81glRCUuSoocR662KRV5Pc9OlWe2GVkBLh8cmAA9VihEz-l-J5f8ObSLDu5l8jwujRJXunmFagtmMnitFqbH2Lzb_FNbY2vHzNkEk3r8G2ODaOTCTdLaV4IWWCw](https://lh5.googleusercontent.com/eMK-wju3oIdPuwnRJ4ATF8L81glRCUuSoocR662KRV5Pc9OlWe2GVkBLh8cmAA9VihEz-l-J5f8ObSLDu5l8jwujRJXunmFagtmMnitFqbH2Lzb_FNbY2vHzNkEk3r8G2ODaOTCTdLaV4IWWCw)

Selanjutnya sesuaikan storage yang akan digunakan pada server yang nanti akan kita gunakan**.**

[https://lh5.googleusercontent.com/auvfBjGY9Rd3OCAprV7jb6MsNtgoEsEHkBm1QdE5eEEBNZ1yr3WsOvu738DwKknxjp_JHq7n9zXaftnjRpwTDrsnY6Jcm4ViuvJC3aOEg16LInNt6EBDXKRK-tXkZvelD3VmNnaQIz4LywjjHg](https://lh5.googleusercontent.com/auvfBjGY9Rd3OCAprV7jb6MsNtgoEsEHkBm1QdE5eEEBNZ1yr3WsOvu738DwKknxjp_JHq7n9zXaftnjRpwTDrsnY6Jcm4ViuvJC3aOEg16LInNt6EBDXKRK-tXkZvelD3VmNnaQIz4LywjjHg)

Selanjutnya, buat **Security Group** baru dengan spesifikasi seperti dibawah ini, kalian juga dapat menggunakan security group yang sudah ada sebelumnya.

[https://lh6.googleusercontent.com/HMP6y6Z6wHGMW5Zk0R9rVcWT_DrSaGW7tjZEe1FU9aZga8AcQTrYB4wCtzaY2ZF_pPAtPBs4xJT0W8YmxZH2qvQ83Zv1azovVzUlrwc_G2cP5JXmX8JqkzxE8-xjn0JW1dQJhnex-DfuLqslAQ](https://lh6.googleusercontent.com/HMP6y6Z6wHGMW5Zk0R9rVcWT_DrSaGW7tjZEe1FU9aZga8AcQTrYB4wCtzaY2ZF_pPAtPBs4xJT0W8YmxZH2qvQ83Zv1azovVzUlrwc_G2cP5JXmX8JqkzxE8-xjn0JW1dQJhnex-DfuLqslAQ)

Kemudian kita lanjut ke bagian untuk memilih keypair. Gunakan yang sudah dibuat sebelumnya, disini kita memilih **cilsy** untuk keypairnya.

[https://lh4.googleusercontent.com/hrTXJzJis2J2PJml_pSQe99Mdq9syCgXQYUFHG6YymbxScimzfMqfo_mYubiBfo6eUXhDlcED_-NheNlL7rUZRhSaDjYjH9BKYTd4D6BrT4OUXO4NCY8H-UqFTDDpRtgfnW4k8ujuL70mmDfBA](https://lh4.googleusercontent.com/hrTXJzJis2J2PJml_pSQe99Mdq9syCgXQYUFHG6YymbxScimzfMqfo_mYubiBfo6eUXhDlcED_-NheNlL7rUZRhSaDjYjH9BKYTd4D6BrT4OUXO4NCY8H-UqFTDDpRtgfnW4k8ujuL70mmDfBA)

Selanjutnya, klik Create launch configuration

[https://lh4.googleusercontent.com/q3RVZJysEb5iAcUqCWFlLkW80m-i3DVMoWuRXG8TYEzO8XQLcq3X74kafAbdEb8XOtwRmn09a3j-_xEqzx1B45HvMUmo2eaXl_7ftY4tJE9afWEibN2ZfzR7mjdrB81lFDm6W2W7HTcjhN1d0w](https://lh4.googleusercontent.com/q3RVZJysEb5iAcUqCWFlLkW80m-i3DVMoWuRXG8TYEzO8XQLcq3X74kafAbdEb8XOtwRmn09a3j-_xEqzx1B45HvMUmo2eaXl_7ftY4tJE9afWEibN2ZfzR7mjdrB81lFDm6W2W7HTcjhN1d0w)

Maka setelah semua tahap konfigurasi dilakukan, kita telah berhasil membuat sebuah launch configuration yang akan kita gunakan pada autoscalling group nanti, hasilnya seperti berikut.

[*Hasil konfigurasi launch configuration*](https://lh4.googleusercontent.com/mx78FofVif-zPsklAnjfBEiHrXYKvMlVPr6SXOybUxSErpbkZeqm_NeUTjG3YXOwwcdCCCzqkMyYM_J5oLFuq-JZ4gYdUv6B_rXnO3o9b4GmRP9FHIqcl1zDOsKLsCKnYGXxWL1zR0Fe2mFJZg)

*Hasil konfigurasi launch configuration*

## **Konfigurasi Auto Scaling Group**

Setelah kita melakukan persiapan dengan membuat **Launch Configurations**, sekarang kita akan masuk kedalam konfigurasi Auto Saling Group. Untuk mulai membuatnya, kita harus masuk kedalam menu Auto Scaling Groups lalu tekan tombol **Create Auto Scaling Group.**

[https://lh3.googleusercontent.com/TjSbR3megOZymTvPA9d8jupC9eBujrW1TEgbkpgHwFenqxuI7l51YjwzADSjra2TQkbcKaMZLqZ3gxTtb_TS0OoxQszQWGmvmwjytiIGyU6Jn8e7XDcaFe2t1tL1Y-PJAFxmGUeYPbA3khkAMA](https://lh3.googleusercontent.com/TjSbR3megOZymTvPA9d8jupC9eBujrW1TEgbkpgHwFenqxuI7l51YjwzADSjra2TQkbcKaMZLqZ3gxTtb_TS0OoxQszQWGmvmwjytiIGyU6Jn8e7XDcaFe2t1tL1Y-PJAFxmGUeYPbA3khkAMA)

Setelah itu kita akan membuat **Auto Scaling Group**.

[https://lh6.googleusercontent.com/5F5763Qr84FBMKeqEnTKoriRJ2NzzZtis0JNp9aNa9PsSn2V4uU9guR8BfN9b2r2Fy-61EjdM3OEHi2HggTsHUT8SnbclzMvcQnLTmJWJK5v7R2Fh8BkcUlo9sxtjh96z437Qb88Qmi2g60dpQ](https://lh6.googleusercontent.com/5F5763Qr84FBMKeqEnTKoriRJ2NzzZtis0JNp9aNa9PsSn2V4uU9guR8BfN9b2r2Fy-61EjdM3OEHi2HggTsHUT8SnbclzMvcQnLTmJWJK5v7R2Fh8BkcUlo9sxtjh96z437Qb88Qmi2g60dpQ)

Pada awal menu kita akan diminta untuk mengisi nama Group dan memilih **launch configuration** yang kita miliki, disini pilih yang sudah kita buat sebelumnya**.**

[https://lh4.googleusercontent.com/n4EVQj0j4RA1svPFTu4x3ib5cUG6L5Nm8LHlD539tU7JhwsNnF70yqBaYptviNdbaGwuQijjt4KrrUDuUvrgoWbltayOsvkLtNKyq06d2wPQRArwlIAMpm0ePhFc49s2C9VGXxh8VBneOo4MYQ](https://lh4.googleusercontent.com/n4EVQj0j4RA1svPFTu4x3ib5cUG6L5Nm8LHlD539tU7JhwsNnF70yqBaYptviNdbaGwuQijjt4KrrUDuUvrgoWbltayOsvkLtNKyq06d2wPQRArwlIAMpm0ePhFc49s2C9VGXxh8VBneOo4MYQ)

[https://lh5.googleusercontent.com/12QMp0D8a1TqD6jRuhc3IxOMJvQp5Te4rG61qlnGWAglol5_bXhyGN40UgG4ifSDo4Trzk47-RxLCXbcdV0l9LZ9gx22n9wy-62_DiQrz8Ux7UVQU5xK587QBTxkI40Yh2HQZnOjZ1pCTz0cPw](https://lh5.googleusercontent.com/12QMp0D8a1TqD6jRuhc3IxOMJvQp5Te4rG61qlnGWAglol5_bXhyGN40UgG4ifSDo4Trzk47-RxLCXbcdV0l9LZ9gx22n9wy-62_DiQrz8Ux7UVQU5xK587QBTxkI40Yh2HQZnOjZ1pCTz0cPw)

Setelah itu, pilih VPC yang akan digunakan, dan juga subnetnya.

[https://lh3.googleusercontent.com/lsjBxSlB_4ixxV3rK0JlCcniUt7e-GvCTpBckpC0BbeR8tWcAVTM57k5j1FETXwy8CPEajcyEceZHw_KIyMUHQCyLa6xTVIPq8dHDxQu07n4sm9ajqYHJBZarfBoHxPL6Ibhw0gucKB29-eJvA](https://lh3.googleusercontent.com/lsjBxSlB_4ixxV3rK0JlCcniUt7e-GvCTpBckpC0BbeR8tWcAVTM57k5j1FETXwy8CPEajcyEceZHw_KIyMUHQCyLa6xTVIPq8dHDxQu07n4sm9ajqYHJBZarfBoHxPL6Ibhw0gucKB29-eJvA)

Jika kalian mempunyai ELB yang aktif, bisa memasukannya disini. Untuk praktikum kali ini, kita tidak akan menggunakan ELB.

[https://lh3.googleusercontent.com/k4eaJ42nVSguweXCOczvfO0EmOYq2cduPa-1LtXX1qiqkQ6gRvLA61SFB8wM7elT0P5Lqg7Met5UE8QjC5tiaRbeS3tIaw8xqwkBP0kB3lm1QxsUUZkXzTO_kSYTmGxXSygpAEG77oXimjvh4Q](https://lh3.googleusercontent.com/k4eaJ42nVSguweXCOczvfO0EmOYq2cduPa-1LtXX1qiqkQ6gRvLA61SFB8wM7elT0P5Lqg7Met5UE8QjC5tiaRbeS3tIaw8xqwkBP0kB3lm1QxsUUZkXzTO_kSYTmGxXSygpAEG77oXimjvh4Q)

Bagian selanjutnya pilih **Use Scaling Policies**. Setelah itu sesuaikan bagian **Group Size** untuk maximum dan minimum instance, disini saya menentukan **minimal 1 dan maximal 4** instance. Untuk bagian **Desired Capacity,** kita akan isi dengan 1. Sehingga apabila akan dilakukan scale up, jumlah instance yang akan ditambahkan adalah 1.

[https://lh3.googleusercontent.com/tvQRa8BSsd38zSwUwoJoQLdP3ogQr3PgpiOPNlzblfRmUkLVRLdLz25oyftel3WI2sctOzezutvU3_zpM488g8q4EUqKOe9M-CGiq_UOvQfUk56gy5Z5v_8VuZSBFldRQH6pMNquJKhsMQYBFw](https://lh3.googleusercontent.com/tvQRa8BSsd38zSwUwoJoQLdP3ogQr3PgpiOPNlzblfRmUkLVRLdLz25oyftel3WI2sctOzezutvU3_zpM488g8q4EUqKOe9M-CGiq_UOvQfUk56gy5Z5v_8VuZSBFldRQH6pMNquJKhsMQYBFw)

Selanjutnya kita set parameter **Scaling policies**, dimana nantinya ini akan jadi parameter ketika instance tersebut harus bertambah apabila CPU mengalami kenaikan. Pilih **Target tracking scaling policy**. Kemudian isikan informasi seperti dibawah ini, lalu isikan target value CPU menjadi **80**, setelah selesai klik **Next.**

[https://lh4.googleusercontent.com/thEBG-zGEnAKtaSKyG1SgTiwB8GsSX0-30NBrIOua9nD5lfRdpjRIzxmVG8BSUUaMvNdB1aSWDPdhWMGcuOYbCG8IQXjziBWt2i9doF2fi7M-sUHYmG-5RAmf9w5q7gLex8goiCUbJ8V_NPn_Q](https://lh4.googleusercontent.com/thEBG-zGEnAKtaSKyG1SgTiwB8GsSX0-30NBrIOua9nD5lfRdpjRIzxmVG8BSUUaMvNdB1aSWDPdhWMGcuOYbCG8IQXjziBWt2i9doF2fi7M-sUHYmG-5RAmf9w5q7gLex8goiCUbJ8V_NPn_Q)

Selanjutnya adalah bagian notifikasi, kalian dapat mensetting notifikasi untuk scalling ini. Akan tetapi pada bagian ini kita tidak akan melakukannya. Maka selanjutnya pilih **Next.**

[https://lh5.googleusercontent.com/ArrXNYMyW4UZT8VqY8k0d2NlLqUTgQ7oQ11TFgK3b4NrAO5YzuGPPfzxnACNH77VYOvLy66w_adwtxi0TK-Y9nqT7paXUiGWwRQQLeYB8pk18azD4Eyb6LjTzvvzCZxsx-QtUcajd1gJ5u2hcw](https://lh5.googleusercontent.com/ArrXNYMyW4UZT8VqY8k0d2NlLqUTgQ7oQ11TFgK3b4NrAO5YzuGPPfzxnACNH77VYOvLy66w_adwtxi0TK-Y9nqT7paXUiGWwRQQLeYB8pk18azD4Eyb6LjTzvvzCZxsx-QtUcajd1gJ5u2hcw)

Selanjutnya isikan **tag** pada instance yang akan di scale oleh auto scalling, disini kita akan berikan tag berupa nama, sehingga ketika ada penambahan instace baru maka akan memiliki nama sesuai tag yang kita buat. Setelah itu klik **Next.**

[https://lh4.googleusercontent.com/U77zEbRQuVwgMRvZLrJ_B-iIO4RtsCli1HfHuIg-PZqXfTHW_xqpQ6g8v6pGOcSm5UhmaFr-g06sx86O_-eqM_-IAYY3hE85uO00v4NSEArZx8_WfnTi5nbeQTQtVW-L7ldOqhURM0_WYK_wRw](https://lh4.googleusercontent.com/U77zEbRQuVwgMRvZLrJ_B-iIO4RtsCli1HfHuIg-PZqXfTHW_xqpQ6g8v6pGOcSm5UhmaFr-g06sx86O_-eqM_-IAYY3hE85uO00v4NSEArZx8_WfnTi5nbeQTQtVW-L7ldOqhURM0_WYK_wRw)

Berikutnya akan muncul bagian review, bagian ini hanya menampilkan sekilas review dari konfigurasi yang sudah kita buat tadi. Klik **Create Auto Scaling grup** untuk melanjutkan.

[https://lh5.googleusercontent.com/4MEXW0erLlXBlDut-z-0SS5MGD_P76PrG-a4Fzxmg_nd5ij_FjKap-rZZ2tYBDyAgqfJuxeMRLLiGTBRODnBdRy82q7LS-9XpJb6v9yXdb-5Fw4WTxfn4zHdlKtiMiDs6NEZOWpufL0YHSOg9Q](https://lh5.googleusercontent.com/4MEXW0erLlXBlDut-z-0SS5MGD_P76PrG-a4Fzxmg_nd5ij_FjKap-rZZ2tYBDyAgqfJuxeMRLLiGTBRODnBdRy82q7LS-9XpJb6v9yXdb-5Fw4WTxfn4zHdlKtiMiDs6NEZOWpufL0YHSOg9Q)

Maka hasil dari konfigurasi Auto Scaling Grup yang sudah dibuat tadi akan terlihat seperti dibawah ini.

[https://lh6.googleusercontent.com/JTFbwvtly5Qwo2_edRqP-jDlS93bh23PJ7B0UYjti1T2iWU6ZumLW8Mma5qlN02NEIZ2NFGslGQda1ygH9wK5l08hqfZyD_xK9JuNHTde9Hsr6hRXkhI8lK5ZC8Webd5dXGfFMFjdvF039FeqQ](https://lh6.googleusercontent.com/JTFbwvtly5Qwo2_edRqP-jDlS93bh23PJ7B0UYjti1T2iWU6ZumLW8Mma5qlN02NEIZ2NFGslGQda1ygH9wK5l08hqfZyD_xK9JuNHTde9Hsr6hRXkhI8lK5ZC8Webd5dXGfFMFjdvF039FeqQ)

Secara otomatis, autoscaling yang kita buat akan membuat 1 instance baru pada EC2. Ini karena **Minimal Capacity** yang kita set adalah 1 pada **Group Size**.

[https://lh4.googleusercontent.com/HHbVDL-rqlgdYfkQZjlAZYxiM4QRstsAuz0Fw0igOVmG5jx4TOpfcOh3l7kl01TmGvH_PFg8fuCzn65OnpmecXzfndKn4ZrlzlYBF1OJvOPTZdsafu3kS11fvinQztcrSpdnC9SCIbRMVPdGHQ](https://lh4.googleusercontent.com/HHbVDL-rqlgdYfkQZjlAZYxiM4QRstsAuz0Fw0igOVmG5jx4TOpfcOh3l7kl01TmGvH_PFg8fuCzn65OnpmecXzfndKn4ZrlzlYBF1OJvOPTZdsafu3kS11fvinQztcrSpdnC9SCIbRMVPdGHQ)

## **Pengujian AutoScaling**

Seperti yang sudah kita konfigurasi sebelumnya, jumlah instance akan bertambah jika CPU instance 80% atau lebih. Maka dari itu, untuk menguji apakah autoscaling yang sudah kita buat berjalan atau tidak, kita bisa membebani instance dengan load yang banyak pada cpu.

Ini bisa kita lakukan secara sengaja dengan menaruh load pada cpu dengan tool **stress**. Sesuai namanya, tool ini akan mengirim load ke system (cpu, disk, memory).

Kita bisa menginstalnya di instance **production-scale** dari **Auto Scaling Group** dengan command berikut.

```bash
sudo apt updatesudo apt install -y stress stress-ng
```

Karena instance yang dibuat adalah t2.micro yang memiliki 1 vcpu, maka kita akan melakukan stress pada 1 cpu. Load yang diberikan kepada cpu ini akan mengakibatkan load CPU menjadi 100%. Sehingga nantinya akan mentrigger untuk menambah **desired instance**. Untuk melakukan stress, kita bisa menggunakan command berikut.

```bash
sudo stress-ng --cpu 1 -v --timeout 600
```

Command diatas akan memberikan load pada 1 cpu (--cpu 1) selama 600 seconds/10 menit (--timeout 300) dan memperlihatkan hasil (-v)

Setelah beberapa lama, autoscaling akan menambah **desired instance** menjadi 2 karena CPU sudah melebih 80%.

[https://lh3.googleusercontent.com/Fwe49w8S8-rpjGS5nxC2fk_cjuSRd8kZzu_qpZYsFXcQhR0oL4Ah2-9THV2umtt0U-BhkV-RogLIjPe5xufJLohPya5UaEOoRci58jeseH624iMvZL6jnWdNT_ypiXe5r4D_wsRnlA856LphUA](https://lh3.googleusercontent.com/Fwe49w8S8-rpjGS5nxC2fk_cjuSRd8kZzu_qpZYsFXcQhR0oL4Ah2-9THV2umtt0U-BhkV-RogLIjPe5xufJLohPya5UaEOoRci58jeseH624iMvZL6jnWdNT_ypiXe5r4D_wsRnlA856LphUA)

# **Exercise**

1. Buat sebuh AMI server baru untuk digunakan Auto Scaling.
2. Buat sebuah Auto Scaling group baru dengan minimal instance 2 dan maximal 8
3. Atur penambahan instance ketika CPU naik 60% dan pengurangan instance ketika CPU turun menjadi 30%.

# **Integrasi Load balancing dan Auto Scaling**

Setelah kedua materi antara Load Balancing dan Auto Scaling telah kita pelajari, sekarang kita akan coba kombinasikan keduanya. Karena Auto Scaling tidak akan berjalan maksimal tanpa adanya load balancing. Maka kita perlu membuat load balancing dan memasangkannya pada auto scaling yang sudah kita buat tadi.

Pertama kita akan membuat load balancing terlebih dahulu, disini kita akan gunakan **classic load balancing**, tahap pembuatannya tidak akan berbeda dengan sebelumnya. Hanya ada beberapa yang diubah saja.

Masuk kedalam menu **Load balancing** dan pilih tombol **Create Load Balancer** untuk membuat ELB baru. 

[https://lh3.googleusercontent.com/9vFF0GzYEOLbGwRZcN4CGe4MmDS2AkYYQNfIjY3oGSr_vh07dEVFRqk6ILck5H3I3Q-Qidbb4E_rhT-0GVYIBs1lo_psPJGO5iL_ObMxrNCc-vn0Uwl3i3grJ0ZglfZcRI7sVmDysYoj1TowVw](https://lh3.googleusercontent.com/9vFF0GzYEOLbGwRZcN4CGe4MmDS2AkYYQNfIjY3oGSr_vh07dEVFRqk6ILck5H3I3Q-Qidbb4E_rhT-0GVYIBs1lo_psPJGO5iL_ObMxrNCc-vn0Uwl3i3grJ0ZglfZcRI7sVmDysYoj1TowVw)

Kita akan diberikan pilihan **model Load Balancer** mana yang akan kita buat, disini kita pilih **Classic Load Balancer,** lalu klik tombol **Create**.

[https://lh4.googleusercontent.com/pweTw4ZxCSRx8-hxN_gUi-StCyczaeYU-pzFrg-QIIO8MDdFvro7w958vZa_qwnFxdE7hArc6gxA6KNJfNI4EK2v5nOwFISXJVL9NxIc4KaRnbn03ECz_NcnMpzL4NBBT6d47fOoqhsMjhFF2w](https://lh4.googleusercontent.com/pweTw4ZxCSRx8-hxN_gUi-StCyczaeYU-pzFrg-QIIO8MDdFvro7w958vZa_qwnFxdE7hArc6gxA6KNJfNI4EK2v5nOwFISXJVL9NxIc4KaRnbn03ECz_NcnMpzL4NBBT6d47fOoqhsMjhFF2w)

Setelah itu kita akan diarahkan ke menu **Basic Configuration**.  Isikan Load Balancer Name : ELB1. Lalu tambahkan **protocol http** dengan port 80. Klik tombol **Next : Assign Security Group** untuk melanjutkan.

[https://lh5.googleusercontent.com/HI25g5NYrAh8S-nEUTObFsV8vamwPGdlkaZ8tbgS8l8sOg6k41Rfj6VdoSWDplkbu6_nD2LJ3WMXvSmHg-lVo0TL-xK8i8jdOgt7mVdyu4oaoIznLHiXVWr22-8M7Us648CGMoi-77Z_dVz8sw](https://lh5.googleusercontent.com/HI25g5NYrAh8S-nEUTObFsV8vamwPGdlkaZ8tbgS8l8sOg6k41Rfj6VdoSWDplkbu6_nD2LJ3WMXvSmHg-lVo0TL-xK8i8jdOgt7mVdyu4oaoIznLHiXVWr22-8M7Us648CGMoi-77Z_dVz8sw)

Selanjutnya kita masuk ke menu **security group**, pilih security group yang sudah kita buat sebelumnya kemudian klik **Next Configure Security Settings.**

[https://lh6.googleusercontent.com/0GYVwLUpAK__-QSh16MLhEmFJF9ekDSHpGmaC53rh0MOk0F0F9AGSvbex3AnVM8nIP1IvoJjV0usPVlc_uXP9wBm9MwWBykkS6KhllVAz2lpJBKBiAYYSLu172oiXXqwLYixpKGUcepNWKh3AA](https://lh6.googleusercontent.com/0GYVwLUpAK__-QSh16MLhEmFJF9ekDSHpGmaC53rh0MOk0F0F9AGSvbex3AnVM8nIP1IvoJjV0usPVlc_uXP9wBm9MwWBykkS6KhllVAz2lpJBKBiAYYSLu172oiXXqwLYixpKGUcepNWKh3AA)

Pada bagian selanjutnya langsung saja klik **Next Configure Health Check.**

[https://lh4.googleusercontent.com/GWecZ8DMuitetqbhB7Gt8OkP40TKYAygvSV_3lC535PUmrmQ2QPaEB0G8JPHAfPUroqP8f_7l-WWmkSGMxh8fwB_aDDl1PqjiKT9MCOI2W-DXDZJCS0FWQ0M7Rg0oIb-3Xb9qp5R3dkONNpqHw](https://lh4.googleusercontent.com/GWecZ8DMuitetqbhB7Gt8OkP40TKYAygvSV_3lC535PUmrmQ2QPaEB0G8JPHAfPUroqP8f_7l-WWmkSGMxh8fwB_aDDl1PqjiKT9MCOI2W-DXDZJCS0FWQ0M7Rg0oIb-3Xb9qp5R3dkONNpqHw)

Selanjutnya kita dapat mengatur **health check** dengan parameter ping protocol HTTP, ping port 80 dan ping path dengan “/”. Pada bagian Advanced setting kita dapat menyesuaikan seperti pengaturan dibawah ini.

[https://lh5.googleusercontent.com/iZUIkTzsxQA-VUVBmMyreOuHtZn2EJXlcei56riCH7JAxdoRnxPhWfsdgiRJGJMgMhjRLObgzZBQdXZKoDDL0bLBLKZcOCrni8x_5OXfUOk6PKue1qgESIyPiFqCg64gXOC0CNo_2fT7u6RTjw](https://lh5.googleusercontent.com/iZUIkTzsxQA-VUVBmMyreOuHtZn2EJXlcei56riCH7JAxdoRnxPhWfsdgiRJGJMgMhjRLObgzZBQdXZKoDDL0bLBLKZcOCrni8x_5OXfUOk6PKue1qgESIyPiFqCg64gXOC0CNo_2fT7u6RTjw)

Pada bagian ini sedikit berbeda, karena kita tidak perlu memilih dan me-register instance yang akan kita gunakan, langsung kita lewati saja dengan klik **Next Add Tags.**

[https://lh6.googleusercontent.com/ruIgv_qOumx13MlMAgvVmOBWePNZlTmtzuLiTY7NdeU4Vazu5ZXAzER8qRBtMvwmo4RtbRu1ASWrRjkJ7x-mJ4jnPuucYZLy0J61KO83e6PuirjX3HWBn-KvUHCKHCP56Vm214pz8vwE6KBIzA](https://lh6.googleusercontent.com/ruIgv_qOumx13MlMAgvVmOBWePNZlTmtzuLiTY7NdeU4Vazu5ZXAzER8qRBtMvwmo4RtbRu1ASWrRjkJ7x-mJ4jnPuucYZLy0J61KO83e6PuirjX3HWBn-KvUHCKHCP56Vm214pz8vwE6KBIzA)

Buat mebuah tag baru dengan menekan tombol **Create Tag** kemudian isi Key dengan **Name** dan Value dengan **ELB1**, tag ini berguna untuk memberikan nama pada ELB classic.

[https://lh5.googleusercontent.com/rffFBxjfNJWO_X4gDCkmx9Oyo_GJfIfIehBD0QpXy2xTPPWDGOHS6M9p5X_i5f2z33tuGud2fQqYyxTU3mQLTlVM5HZR1_SIhCePLLafRtzIgugeKgRzs07nlLS3bKDq_2XBtNDRgtt6cYmSvA](https://lh5.googleusercontent.com/rffFBxjfNJWO_X4gDCkmx9Oyo_GJfIfIehBD0QpXy2xTPPWDGOHS6M9p5X_i5f2z33tuGud2fQqYyxTU3mQLTlVM5HZR1_SIhCePLLafRtzIgugeKgRzs07nlLS3bKDq_2XBtNDRgtt6cYmSvA)

Setelah semua konfigurasi dan setting telah di lakukan, maka kita data melihat kembali rincian dari sudah kita konfigurasi tadi sebelumnya. Untuk melanjutkan klik **Create**.

[https://lh3.googleusercontent.com/pRP43-_e95P6btZauFecE6yP9NMAWE6fu_IHD2_iRqOmwZHd_2QWaDPabLyeOezJrM0aHmzWZzazkdJsvaTupSL_n8I7RWlhNcc2XAaoXfID_gjC7PqtOMxm7uLJSe2IHjcXNzCu7_AnZwpP7w](https://lh3.googleusercontent.com/pRP43-_e95P6btZauFecE6yP9NMAWE6fu_IHD2_iRqOmwZHd_2QWaDPabLyeOezJrM0aHmzWZzazkdJsvaTupSL_n8I7RWlhNcc2XAaoXfID_gjC7PqtOMxm7uLJSe2IHjcXNzCu7_AnZwpP7w)

Setelah selesai, kita akan diarahkan ke dalam menu **dashboard Elastic Load Balacer** dan kita dapat lihat konfigurasi yang sudah kita buat tadi. Untuk melihat DNS name url, kita dapat menklik tombol description yang ada di menu bawah ELB.

[https://lh6.googleusercontent.com/K8Ha5-XVl2APe9f6UcGuF534LNOi1meawrv1MWtGcQCRZtpfX0yUkONbYWUdtOKsKPkEaxAzu2MRYc97P1MeGrFVnKYbUKd1KtUFV1EDon2d41O7tLO3VwdaiIeceTSp58jHJSnLNUmDckSgTg](https://lh6.googleusercontent.com/K8Ha5-XVl2APe9f6UcGuF534LNOi1meawrv1MWtGcQCRZtpfX0yUkONbYWUdtOKsKPkEaxAzu2MRYc97P1MeGrFVnKYbUKd1KtUFV1EDon2d41O7tLO3VwdaiIeceTSp58jHJSnLNUmDckSgTg)

Selanjutnya pindah kedalam menu **Auto Scaling Group**, lalu pada bagian tab **Details** scroll ke bawah hingga menemukan menu **Load Balancing**, klik tombol **Edit**.

[https://lh6.googleusercontent.com/x_eCwKhGibGlNIgNNw9Dstyp2QnpY9vyRnnNuJkPXb9BKC8cJS_QoKECIWa6fdrJ9pEHYwxRC7uRwyvOw-2X7hIjyRQsrHq8PggXylYxkzlHcOKcgkHvoO_OuoJ8eSSqN6T8sQErJ01D8mpJ-A](https://lh6.googleusercontent.com/x_eCwKhGibGlNIgNNw9Dstyp2QnpY9vyRnnNuJkPXb9BKC8cJS_QoKECIWa6fdrJ9pEHYwxRC7uRwyvOw-2X7hIjyRQsrHq8PggXylYxkzlHcOKcgkHvoO_OuoJ8eSSqN6T8sQErJ01D8mpJ-A)

Akan muncul sebuah pop-out konfigurasi. Check pada **Classic Load Balancer** seperti pada gambar lalu pilih load balancer yang sudah kita buat tadi. Lalu klik **Update** untuk menyimpan.

[https://lh5.googleusercontent.com/LPL1Agcx_joQkz98ch2JFY3VMN1LDp4dmX0TJ0PFXO06vjr9dg-uh7D-rRotKGJ6SxwFqyJwY7D4t1V0nrIrNMswppcFczJPoVsvV1IuwVhC5I1BOGaCT958tOYoqwCGtA-DOz1T8w18krq5sQ](https://lh5.googleusercontent.com/LPL1Agcx_joQkz98ch2JFY3VMN1LDp4dmX0TJ0PFXO06vjr9dg-uh7D-rRotKGJ6SxwFqyJwY7D4t1V0nrIrNMswppcFczJPoVsvV1IuwVhC5I1BOGaCT958tOYoqwCGtA-DOz1T8w18krq5sQ)

Setelah selesai menyimpan, selanjutnya ujicoba load balance yang sudah kita buat dengan memanggil alamat load balancer tersebut. Harusnya akan muncul web aplikasi dari instance auto scaling yang kita buat load balancer.

![*Hasil Load Balancer dan AutoScaling*](8%20Auto%20Scalling%20e6d59764791b4a03acb3be24a021cdc0/Untitled.png)

*Hasil Load Balancer dan AutoScaling*