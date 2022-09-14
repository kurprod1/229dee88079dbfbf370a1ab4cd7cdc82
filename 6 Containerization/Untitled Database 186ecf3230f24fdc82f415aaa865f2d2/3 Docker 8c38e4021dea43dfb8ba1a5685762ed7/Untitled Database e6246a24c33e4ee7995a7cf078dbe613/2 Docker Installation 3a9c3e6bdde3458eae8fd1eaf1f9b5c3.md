# 2. Docker Installation

Created: July 4, 2022 10:21 AM

# ***Docker Edition***

## **CE vs EE**

Docker memiliki 2 bersi yaitu *Community Edition* (CE) dan *Enterprise* *Edition* (EE). Versi CE ini adalah versi gratisan dan versi EE adalah versi berbayar. Dimana tentunya pada versi EE memiliki beberapa fitur-fitur unggulan dan support tim ahli yang tidak ada di versi CE.

Versi EE lebih cocok digunakan di perusahaan-perusahaan yang memang sudah memiliki dana dan benar-benar digunakan dalam skala Production yang besar. Sedangkan versi CE lebih cocok digunakan untuk riset atau digunakan skala production oleh perusahaan-perusahaan yang masih belum mempunyai cukup dana.  Secara overall dalam versi CE Anda tetap bisa menggunakan Docker tanpa kurang suatu apapun. Namun tentunya Anda yang harus melakukannya semua sendiri.

Berikut adalah sedikit tabel perbandingan dari CE dan EE :

[Untitled](2%20Docker%20Installation%203a9c3e6bdde3458eae8fd1eaf1f9b5c3/Untitled%20Database%20c0e15f36f6e64e458cde2f7fa9c391eb.csv)

## ***Edge vs Stable***

Docker juga dalam setiap rilisnya dibagi menjadi 2 tipe. Yaitu *Edge* dan *Stable*. Dimana versi *Edge* dikhususkan untuk versi “coba-coba” sedangkan *Stable* adalah versi siap pakai untuk real implementasi.

Secara umum karakteristik kedua versi ini adalah :

**Versi *Edge***

1. Rilis tiap bulan
2. Disupport selama 1 bulan
3. Selalu dapat fitur terbaru
4. Cenderung banyak bug.

**Versi *Stable***

1. Rilis setiap 4 bulan sekali.
2. Di support selama 4 bulan
3. Tidak dapat semua fitur-fitur terbaru.
4. Cenderung lebih stabil

[https://lh4.googleusercontent.com/WxUxZz5lOacR_ic0ry8m1abeYnNpdQFnbsA67RPKnPLxM8b9sIdI66dDSYurgFeTgFrq7V2lVNjqRPOVF9UnfukEAV1sfclCd766fPmLJytGnkCoai9eCIxUd99fPngfg2og1gDDgBQgovBV9g](https://lh4.googleusercontent.com/WxUxZz5lOacR_ic0ry8m1abeYnNpdQFnbsA67RPKnPLxM8b9sIdI66dDSYurgFeTgFrq7V2lVNjqRPOVF9UnfukEAV1sfclCd766fPmLJytGnkCoai9eCIxUd99fPngfg2og1gDDgBQgovBV9g)

*Data version stable dan Edge*

# **Penulisan Versi**

Mulai tahun 2017, penulisan versi dari Docker menggunakan format YY.MM (tahun.bulan) mengikuti penulisan versi mirip salah satu distro Linux yaitu Ubuntu. Jadi misalnya ada Docker versi 18.04 maka artinya Docker tersebut dirilis tahun 2018 bulan 4.

Namun jika Anda pernah melihat versi seperti 1.12 maupun 1.13 itu adalah versi terdahulu sebelum tahun 2017.

# **Langkah instalasi Docker**

1. ***Linux***

Untuk instalasi di Linux paling mudah menggunakan script berikut yang bisa dapat dari [https://get.docker.com](https://get.docker.com/) :

```bash
curl -fsSL get.docker.com -o get-docker.sh
```

Setelah itu jalankan scriptnya dan proses instalasi Docker akan berlangsung secara otomatis :

```bash
chmod +x get-docker.sh
sh get-docker.sh
```

Baik Linux distro berbasis RHEL (Centos, Fedora) maupun Debian (Ubuntu, Linux Mint), dapat menggunakan perintah tersebut.

Ada sedikit perbedaan instalasi Docker di Linux, yaitu di Linux kita belum terinstall komponen Docker secara lengkap. Yang belum terinstall adalah Docker *Compose* dan Docker *Machine*.

Instalasi Docker Compose dapat dilakukan dengan mengeksekusi script berikut :

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version

```

Sedangkan untuk Docker Machine bisa eksekusi perintah berikut :

```bash
base=[https://github.com/docker/machine/releases/download/v0.16.2](https://github.com/docker/machine/releases/download/v0.14.0)
curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine
sudo install /tmp/docker-machine /usr/local/bin/docker-machine
```

# **Pengecekan hasil instalasi**

Untuk mengecek seluruh hasil instalasi dapat mengetikkan perintah berikut di terminal/cmd :

```bash
docker version
docker-compose --version
docker-machine --version
```

# **Exercise**

**Teori**

1. Kenapa perlu mempelajari Docker?
2. Ceritakan apa yang akan Anda coba terapkan dengan Docker untuk kebutuhan Anda?