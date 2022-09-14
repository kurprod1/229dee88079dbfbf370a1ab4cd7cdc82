# 15. Setup Webserver & Applications

Created: June 27, 2022 2:41 PM

# **Install Webserver dan Database Server**

Webserver merupakan sebuah layanan yang ada dalam sebuah server yang berfungsi untuk membaca program berbasis web yang diantaranya adalah html, css, js, php, dll. Banyak aplikasi webserver yang bisa kita gunakan salah satunya adalah apache dan NginX.

Pada bagian kali ini kita akan coba menginstallkan apache sebagai webservernya, serta menginstallkan php didalamnya menggunakan perintah berikut.

```bash
sudo apt-get install apache2 php php-mysql
```

Setelah webserver berhasil terinstall, maka selanjutnya kita install database mysql

```bash
sudo apt-get install mysql-server
```

Setelah selesai melakukan installasi webserver dan juga database mysql, sekarang kita ujicoba apakah webserver sudah berjalan atau belum. Kita dapat memanggil alamat server tersebut di browser untuk melihat hasil dari installasi webserver yang sudah kita lakukan.

[*Tampilan hasil webserver*](https://lh6.googleusercontent.com/Xgsy_QfYCzUa5804zI49viuwhwzIWqQ7wV40DfzH5zClkDT480B1Twg5pE1_ovt1Sb1q5c-3CmJ8RxcEjiK4Hfs8yks507PA2Zx3Ahh5w7SXXWIjqD5b2OIag0PDQXbotwi4kgKCIN8BBW5VJg)

*Tampilan hasil webserver*

Untuk mengecek keberhasilan dari database server, kita akan coba untuk masuk kedalam console mysql tersebut dengan menggunakan perintah berikut.

```bash
sudo mysql -u root -p
```

Masukan password mysql lalu tekan enter. Apabila belum membuat password, maka langsung enter saja dan akan muncul seperti berikut.

[*Tampilan console mysql*](https://lh4.googleusercontent.com/7qFUk0xmwyCPUh_vBrsHSezAPV2cOoSJe6oQThXdjSK55t1Na2L-aFjXAMNIMdD-DFymugSBOp4dfswLhb3P_0Zjc4DWefxNXlR_8A5fk-vTU8p2lVn5nyc9IUJmXa6Udn5D0QtjmaLAzQnZfw)

*Tampilan console mysql*

Dengan begini persiapan webserver dan database server sudah selesai kita setup, selanjutnya kita akan coba melakukan setup pada web aplikasi yang akan kita integrasikan degan webserver dan database server tersebut.

# **Setup Web Aplikasi Sosial Media**

Setelah melakukan installasi webserver dan database server, sekarang kita akan melakukan setup pada Web Aplikasi di server local tersebut. Pertama kita harus menyiapkan terlebih dahulu database yang akan kita gunakan, masuk ke console mysql dan tambahkan user.

```sql
sudo mysql -u root -p

mysql> create user ‘devopscilsy’@’localhost’ identified by ‘1234567890’;
```

Perintah diatas menerangkan bahwa nama user yang akan kita buat adalah devopscilsy dan password usernya adalah 1234567890. Jika berhasil maka akan muncul seperti dibawah ini.

[https://lh5.googleusercontent.com/o_Qwh3MKxgsvca8m2W08MxYUt2hI0CQVPetM1dh7VR9QhUrnu1rHCP0TWxKPxTQMbCSQW8y6ziRsHnjmH9IJJcHBunA-vmNMgiA_lLKRaAdGHChAFLspLHI4Qi4fr5EjPxh3owQyIA4_0wuRbQ](https://lh5.googleusercontent.com/o_Qwh3MKxgsvca8m2W08MxYUt2hI0CQVPetM1dh7VR9QhUrnu1rHCP0TWxKPxTQMbCSQW8y6ziRsHnjmH9IJJcHBunA-vmNMgiA_lLKRaAdGHChAFLspLHI4Qi4fr5EjPxh3owQyIA4_0wuRbQ)

Selanjutnya kita berikan hak akses pada user yang sudah kita buat tersebut.

```sql
mysql> grant all privileges on *.* to ‘devopscilsy’@’localhost’;
```

Setelah selesai memberikan hak akses pada user, kita dapat keluar dari console dengan menggunakan perintah ***\q**.* Lalu coba kembali masuk kedalam konsole mysql menggunakan user baru tersebut, dan buat database dengan nama dbsosmed didalamnya.

```sql
sudo mysql -u devopscilsy -p

mysql> create database dbsosmed;
```

Cek keberadaan database yang sudah kita buat dengan menggunakan perintah berikut.

show databases;

[https://lh4.googleusercontent.com/wDMbFvYwSm9dx_aUXFm3rgW_LfFTBkeVOh4zdoq5ZmluhAqUkaTmh6l3TcniZvqICd4eq5O9hvqypuzTmsmeqZeKl2Sp6AseMyjYQ18bE5JAwusJ690gzI1H4xdH-3sH2EVUZ1AxoGhXqcQWNA](https://lh4.googleusercontent.com/wDMbFvYwSm9dx_aUXFm3rgW_LfFTBkeVOh4zdoq5ZmluhAqUkaTmh6l3TcniZvqICd4eq5O9hvqypuzTmsmeqZeKl2Sp6AseMyjYQ18bE5JAwusJ690gzI1H4xdH-3sH2EVUZ1AxoGhXqcQWNA)

Selanjutnya keluar dari database dengan menggunakan perintah ***\q.***

Setelah kita melakukan persiapan database, maka selanjutnya kita download web aplikasi untuk dipasangkan pada server lokal kita. Pertama kita pindah direktori dulu ke direktori utama, lalu download aplikasi seperti berikut.

```bash
cd
wget [https://github.com/sdcilsy/sosial-media/archive/master.zip](https://github.com/sdcilsy/sosial-media/archive/master.zip)
```

Selanjutnya kita ekstrak file aplikasi tersebut, tetapi sebelumnya kita harus menginstallkan paket unzip terlebih dahulu.

```bash
sudo apt-get install unzip
unzip master.zip
```

Jika berhasil akan muncul seperti dibawah ini.

[https://lh3.googleusercontent.com/_3WLvzrfpdGItIBqPKfO8MHgzrYV7v2nMgkhKVfgvembWTh9WYIMvboy5b39BpX9pgtGvm73vgpkmbxc90vuiCfwRhk5aNNRmIjYN1mnN783oIyv-axbobF-IPRX6Rk0BHFgLX1KMXuKqr-7CQ](https://lh3.googleusercontent.com/_3WLvzrfpdGItIBqPKfO8MHgzrYV7v2nMgkhKVfgvembWTh9WYIMvboy5b39BpX9pgtGvm73vgpkmbxc90vuiCfwRhk5aNNRmIjYN1mnN783oIyv-axbobF-IPRX6Rk0BHFgLX1KMXuKqr-7CQ)

Selanjutnya kita akan pindahkan seluruh isi konten yang ada pada direktori *sosial-media-master* yang sudah kita ekstrak tadi ke */var/www/html/* agar konten aplikasi tersebut dapat kita akses. Sebelumnya hapus dulu file index.html yang ada pada direktori */var/www/html/*.

```bash
sudo rm /var/www/html/index.html
sudo mv sosial-media-master/* /var/www/html
```

Kita bisa check apakah semua konten sudah dipindahkan ke direktori */var/www/html/* dengan perintah ls seprti berikut.

[https://lh3.googleusercontent.com/Rb20OHzZdzbgz809IIaf6TGGDb_ohWg2C1A6VZRnuABLr9UVfE_ZniZwKTpvJxmu6IEHMsRCsDNlCLuXJmE_eLYAU-tbkN0j8eKx22WTrodoZnZVpZKRpdo7DP-I-nlyD3T54WhIyfDjPQSAuw](https://lh3.googleusercontent.com/Rb20OHzZdzbgz809IIaf6TGGDb_ohWg2C1A6VZRnuABLr9UVfE_ZniZwKTpvJxmu6IEHMsRCsDNlCLuXJmE_eLYAU-tbkN0j8eKx22WTrodoZnZVpZKRpdo7DP-I-nlyD3T54WhIyfDjPQSAuw)

Dalam seluruh isi konten bisa kita lihat ada file dump.sql, file tersebut merupakan data export dari database konten web sosmed ini. Sekarang kita akan coba import file tersebut ke database yang sudah kita buat sebelumnya yaitu dbsosmed.

```bash
cd /var/www/html/
sudo mysql -u devopscilsy -p dbsosmed < dump.sql
```

Setelah selesai, sekarang kita bisa ujicoba web aplikasi tersebut dengan memanggil kembali alamat server local yang kita miliki.

[*Halaman utama Aplikasi Web*](https://lh6.googleusercontent.com/6UoLJZgVSe9iaS8afG35rPCKNTiCZqc84kRtkoXQMjIT77CPC6K6Yl_TbdW4_3U2aAU3TEItH7SpGBRFHSnLf5IDZzk1F7__88s8HY3Um0sAKXMO9vqPY0up3Nc3hdea0rPvJ4LEC-APomnT4g)

*Halaman utama Aplikasi Web*

Kita ujicoba aplikasi tersebut dengan memilih tombol daftar untuk mendaftarkan akun baru pada aplikasi sosmed pesbuk.

[*Halaman Pendaftaran Akun*](https://lh5.googleusercontent.com/XnW9EH1c1MHxLtjsyA-qYa9EdygkedkEFC1b8uKfECqaXza392WjtX4lWGBmjAgutfKNVeQznkCcdwB5ZGSvH0SMSWQgNt6oVAPvoJMFIfSlDBBQ8NzJWBScrwkCxeZ_dLYksfkXfmgUs5a5eA)

*Halaman Pendaftaran Akun*

Setelah berhasil mendaftar, kalian akan diarahkan langsung ke form login aplikasi. Lakukan login dengan akun tersebut hingga kalian diarahkan pada halaman dashboard aplikiasi.

[*Halaman Login Akun*](https://lh6.googleusercontent.com/7bq7kOx2rKaPHh2KXVj_1PrzT2du96QdcdaW3ZeODGVl_qTiFSo32Mj6KMrdXJxHb33_QZLQ82JHuChfokwDyuZQCKJfvEYrkFN5yzfHv9JaOKue9A1r0sZo9pWD9zqQHJEc9NR1hkOovUvAkw)

*Halaman Login Akun*

[*Halaman Dashboard Aplikasi*](https://lh6.googleusercontent.com/A0GROhUOTbHYLdg6W2IQ1Y8WsoUS2mSOZdJbIFolbLhP046gSMLfMhxTa6cZAqXu_MK4ud5dVArYDDt-hnZ_dNMvNcEmFoOZPnrrp0qBy5ulsEHT8GqCy9wYPANNB-ktUv8hyZYR_7FpFbvo5g)

*Halaman Dashboard Aplikasi*

Selamat kamu sudah menyelesaikan sebuah infrastructure untuk sebuah web aplikasi sosial media pesbuk dengan menyertakan layanan webserver dan juga database server.