# 15. Building Image : Basic Dockerfile

Created: July 5, 2022 10:21 AM

# **Apa itu Dockerfile ? Untuk apa Dockerfile?**

Dockerfile merupakan resep untuk membangun sebuah image. Semua image pasti memiliki sebuah Dockerfile didalamnya. Anda bisa coba lihat-lihat contoh Dockerfile dari image-image yang ada di Docker Hub, seperti contohnya Dockerfile pada salah satu image Postgres berikut :

[*Docker file pada image postgress*](https://lh4.googleusercontent.com/cvkIEkIhIVW1Yqulslxz-eONYa8TIoGsRL-L15K8sp2MkwjuwNX5rsC3mwKRgW_BvAm-S8XK6MxHKWwdmQ4STqXYlC1TJFRdUE_5M1WvRVX50qknP98eVQeVzrj4Fxw5uidQOPgpiPIvaEGA-w)

*Docker file pada image postgress*

[*Isi dari Dockerfile*](https://lh4.googleusercontent.com/Bh3ePlVOY0fXdeOtt8XtSivE4SPT62iyDKBbqBnSz4kV7UwJewD4N_rStPtQL0rK8bMN55JNS3gDoiM3WpTBymp1Gdn_d-d9xlMG4nt-DXDUml2R-Zvuf91x4g3LwBKko5k7ulYq22mkCUqRhQ)

*Isi dari Dockerfile*

Dockerfile benar-benar bahasa yang khusus hanya untuk docker, bukanlah :

1. Shell Script
2. Bahasa programming

Perlu dipahami juga bahwa setiap command yang dijalankan di Dockerfile (yang berwarna merah pada screenshot diatas) dibaca dari atas kebawah, dan masing-masing command tersebut mewakili 1 buah layer image.

Apa maksud dari masing-masing command tersebut serta bagaimana cara membacanya? Kita akan coba jelaskan langsung dari file contoh di materi berikut.

## **Memahami Dockerfile dari contoh**

Kita coba buka Dockerfile dari folder dockerfile-contoh-1 yang merupakan Dockerfile dari official image nginx :

```bash
# NOTE: this example is taken from the default Dockerfile for the official nginx Docker Hub Repo
# https://hub.docker.com/_/nginx/
 
FROM debian:stretch-slim
# all images must have a FROM
# usually from a minimal Linux distribution like debian or (even better) alpine
# if you truly want to start with an empty container, use FROM scratch
 
ENV NGINX_VERSION 1.13.6-1~stretch
ENV NJS_VERSION   1.13.6.0.1.14-1~stretch
# optional environment variable that's used in later lines and set as envvar when container is running
 
RUN apt-get update \
	&& apt-get install --no-install-recommends --no-install-suggests -y gnupg1 \
	&& \
	NGINX_GPGKEY=573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62; \
	found=''; \
	for server in \
		ha.pool.sks-keyservers.net \
		hkp://keyserver.ubuntu.com:80 \
		hkp://p80.pool.sks-keyservers.net:80 \
		pgp.mit.edu \
	; do \
		echo "Fetching GPG key $NGINX_GPGKEY from $server"; \
		apt-key adv --keyserver "$server" --keyserver-options timeout=10 --recv-keys "$NGINX_GPGKEY" && found=yes && break; \
	done; \
	test -z "$found" && echo >&2 "error: failed to fetch GPG key $NGINX_GPGKEY" && exit 1; \
	apt-get remove --purge -y gnupg1 && apt-get -y --purge autoremove && rm -rf /var/lib/apt/lists/* \
	&& echo "deb http://nginx.org/packages/mainline/debian/ stretch nginx" >> /etc/apt/sources.list \
	&& apt-get update \
	&& apt-get install --no-install-recommends --no-install-suggests -y \
						nginx=${NGINX_VERSION} \
						nginx-module-xslt=${NGINX_VERSION} \
						nginx-module-geoip=${NGINX_VERSION} \
						nginx-module-image-filter=${NGINX_VERSION} \
						nginx-module-njs=${NJS_VERSION} \
						gettext-base \
	&& rm -rf /var/lib/apt/lists/*
# optional commands to run at shell inside container at build time
# this one adds package repo for nginx from nginx.org and installs it
 
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log
# forward request and error logs to docker log collector
 
EXPOSE 80 443
# expose these ports on the docker virtual network
# you still need to use -p or -P to open/forward these ports on host
 
CMD ["nginx", "-g", "daemon off;"]
# required: run this command when container is launched
# only one CMD allowed, so if there are multiple, last one wins
```

**Penjelasan :**

- FROM merupakan command untuk menentukan basis image ini menggunakan image apa. Contohnya untuk image nginx ini berbasis image salah satu distro Linux yaitu Debian Jessie. Setiap Dockerfile harus memiliki FROM, dan biasanya FROM ini merujuk pada distro Linux yang super kecil seperti alpine.
- ENV untuk menentukan variable tertentu yang dapat terus dijalankan baik saat mem-build image ini maupun saat sudah menjalankan container. Seperti disini sudah ditentukan variable NGINX_VERSION adalah 1.13.6-1~stretch. Sehingga setiap ada kebutuhan untuk menyebutkan versi NGINX, dibanding untuk menulis 1.13.6-1~stretch, kita bisa langsung tulis NGINX_VERSION saja. Contohnya di Dockerfile ini ada tertulis :
    - apt-get install --no-install-recommends --no-install-suggests -y **nginx=${NGINX_VERSION}** \
    
    Artinya perintah itu sama saja dengan :
    
    - apt-get install --no-install-recommends --no-install-suggests -y **nginx=1.13.6-1~stretch** \
- RUN merupakan command-command tambahan yang akan dieksekusi saat mem-build image ini. Command-command ini biasanya merupakan command-command Linux pada umumnya.
- EXPOSE ini untuk membuka suatu port di image ini. Tapi tetap harus menggunakan opsi -p pada saat menjalankan container.
- CMD merupakan command default yang akan dijalankan oleh container jika menggunakan image ini. Biasanya berisi command untuk menjalankan layanan/aplikasi tersebut. Contohnya disini command yang dijalankan : nginx -g daemon off

Secara garis besar konsep urutan isi Dockerfile ini mirip seperti urutan langkah-langkah instalasi dan konfigurasi suatu layanan/program di Linux pada umumnya, yaitu :

1. Instalasi dependensi-dependensi aplikasi yang dibutuhkan
2. Instalasi aplikasi/layanannya itu sendiri
3. Lakukan konfigurasi-konfigurasi tambahan agar aplikasi/layanan itu dapat berjalan
4. Jalankan aplikasi/layanan tersebut.

Jika Anda sebelumnya sudah sering berkutat dengan dunia server dan Linux pasti sudah tidak asing dengan pola seperti ini. Dockerfile official image nginx diatas pun jika diperhatikan memiliki pola yang mirip-mirip :

1. Gunakan distro Debian Jessie (FROM)
2. Tentukan versi nginx yang ingin diinstall (ENV)
3. Install dependensi-dependensi dari nginx dan install nginxnya (RUN apt-get update, apt-get install)
4. Lakukan konfigurasi tambahan (expose port, RUN ln -sf)
5. Jalankan nginx nya (CMD ["nginx", "-g", "daemon off;"])

Masih sangat banyak contoh-contoh penggunaan Dockerfile yang lain yang tidak akan mungkin di hafal dan cepat dipahami. Kuncinya adalah sering-sering dicoba dan sering-sering berlatih. Anda bisa coba akses link berikut untuk referensi best practice dan petunjuk penggunaan Dockerfile :

1. [https://docs.docker.com/engine/reference/builder/](https://docs.docker.com/engine/reference/builder/)
2. [https://docs.docker.com/develop/develop-images/dockerfile_best-practices/](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

# **Building image : Running Docker Builds**

Perintah untuk build image formatnya adalah sebagai berikut :

```bash
$ docker image build -t <nama image yang diinginkan>:<tag> .
```

Nb : perintah diatas hanya bisa dilakukan jika kita berada di dalam folder yang sudah terdapat Dockerfile dan nama Dockerfilenya benar-benar bernama “Dockerfile”.

**Contoh :**

```bash
$ docker image build -t nginxbebas .
```

Apabila nama Dockerfilenya selain dari defaultnya, maka bisa gunakan perintah ini :

```bash
$ docker image build -f <nama Dockerfile> -t <nama image yang diinginkan>:<tag> .
```

Contoh :

```bash
$ docker image build -f dockerfile-nginx -t nginxbebas .
```

Misalnya kita coba build image nginx tersebut :

```bash
$ docker image build -t nginxbebas .
```

Maka kita bisa lihat bahwa akan terjadi banyak proses yang dijalankan sesuai command-command yang sudah ditentukan di dalam Dockerfile, seperti perintah RUN, perintah EXPOSE, perintah CMD.

[*Hasil menjalankan docker build*](https://lh6.googleusercontent.com/q74d7-T5xPZVLVyALGOBRRrkg91dyMe6rPWZOtSV0kXXm08A1oTVSTSyWcWoIFwMhKgr5g71SNdOLF9Gn27rEWruHasaSUPG76il9oNlSXdNz3ZQvNtUN1i9Dq2zPn5P_cmtbbEdg_-x6jXM6w)

*Hasil menjalankan docker build*

[*Hasil menjalankan docker build*](https://lh4.googleusercontent.com/arnSjICZ5uC968xWAIdz3lrkWudcS2DdwOKmBkesost4ze2VF9ZSmkTNpMbMs5VxljNQbIV9y4hDlRtBUkCnv0f3QXCoZ6XaTdTlOco1LX4eLoQPrm90J9McsKTrLKEyiYAHWVLgXMQnskCfbw)

*Hasil menjalankan docker build*

Setelah proses build selesai, cobalah ulangi perintah build yang sama dan perhatikan apa yang terjadi :

```bash
$ docker image build -t nginxbebas .
```

Proses yang tadinya cukup lama, sekarang hanya berjalan tidak sampai 1 detik. Kenapa hal ini bisa terjadi?

Sekarang coba perhatikan gambar dibawah ini :

[https://lh6.googleusercontent.com/3Z4GgN-9lImx9YiMOqHQ_Zu1l-7qgV2JP70XNw8e6L3UyIqnnzS2iz6PDwHyX_qEnLM4hxpoW5dJQ8kTzQ8tVabbpKDGlYv9Cvzh5gs0F_VpA87gmA5vCGkHuhYxgls_QD4_O96ktdK5-sCj6A](https://lh6.googleusercontent.com/3Z4GgN-9lImx9YiMOqHQ_Zu1l-7qgV2JP70XNw8e6L3UyIqnnzS2iz6PDwHyX_qEnLM4hxpoW5dJQ8kTzQ8tVabbpKDGlYv9Cvzh5gs0F_VpA87gmA5vCGkHuhYxgls_QD4_O96ktdK5-sCj6A)

Terlihat bahwa pada setiap command diatas muncul tulisan “Using Cache”. Ini artinya command tersebut masih merupakan layer image yang sama dengan yang tersimpan di local sehingga tidak perlu dieksekusi kembali.

Sebuah image layer dinyatakan sama ketika :

1. Isi commandnya persis sama
2. Urutan commandnya sama

Misalnya saja kita coba ubah isi dari Dockerfile yang bagian EXPOSE menjadi 80 443 8080.

Maka ketika kita coba lakukan build ulang imagenya, bagian command tersebut tidak akan menggunakan cache lagi. Tapi benar-benar di eksekusi ulang. Terlihat dari tidak adanya tanda “Using Cache” disana.

[https://lh4.googleusercontent.com/VqzlcOSkErePe7pTSOKbOuIt6eavsYR_2PwGgVP2ICkPM2g-mqgnKSZtnJ0J1AB0FkN5Gjw2LCIuKeFwS0exnJqnpphfwLZ8RzEAm0QeNqLOQCIb1KUqUKeXk2ooYlFaTX4poENeNL8fU6F4Bg](https://lh4.googleusercontent.com/VqzlcOSkErePe7pTSOKbOuIt6eavsYR_2PwGgVP2ICkPM2g-mqgnKSZtnJ0J1AB0FkN5Gjw2LCIuKeFwS0exnJqnpphfwLZ8RzEAm0QeNqLOQCIb1KUqUKeXk2ooYlFaTX4poENeNL8fU6F4Bg)

[*Hasil build setelah diubah expose*](https://lh6.googleusercontent.com/dVnsDxW7dMzxpKXBpU7WbagbcgAx5hwfwZHqCrF1-_VNnK9DVNUOHY9XLHt5NmoTd-TucrQDC55DcAY4XsKL6WY-QYIw9WivqpSoSdvJ8Qy0wARFqkBqk0ORdrO7CjhGDFAFxUSop8rjNN10Zw)

*Hasil build setelah diubah expose*

Uniknya lagi, ketika kita mengubah sebuah command, maka command yang berada dibawahnya semuanya akan dieksekusi ulang walaupun kita tidak merubahnya. Bisa kita lihat bahwa command CMD juga sudah tidak menggunakan Cache lagi.

Hal ini merupakan mekanisme keamanan default dari Docker untuk memastikan bahwa command yang baru saja diubah tidak mempengaruhi command-command dibawahnya.

Kesimpulannya sebaiknya pastikan command-command yang bagian teratas dari Dockerfile merupakan command-command yang paling sedikit diubah, dan yang bagian bawah merupakan command-command yang paling sering berubah. Hal ini perlu dipahami dengan baik agar proses build image dapat tetap dijalankan dengan cepat dan tidak memakan resource data yang tidak perlu.

[*Command Dockerfile*](https://lh4.googleusercontent.com/Hn-E0aWp7_8H8WzRCBH1dEhTvKop6k1ZcaRwYsgaFtmiPUPq0xfrFcojeM3yfSnVc_90XXyDsbuovDWTiZtBElvlcpXwYKQon3vYh7Zm9m_bDgHhueWON57YrJUZlYukED8jt4GorCXwzzDZNg)

*Command Dockerfile*

# **Building Image : Extending Official Image**

Sering kali official image pada akhirnya tidak bisa memenuhi kebutuhan kita. Misalnya kita selain membutuhkan webserver nginx, tapi kita juga membutuhkan nginx ini ditambahkan dengan file html dari web perusahaan kita. Atau misalnya image mysql perlu ditambah dengan database dari aplikasi kita.

Oleh karena itu biasanya kita menggunakan Official Image sebagai basis dari image custom yang akan kita buat sendiri.

# **Build Official Image yang sudah dimodifikasi**

Disini kita akan coba untuk menggunakan official image dari nginx kemudian menambah sebuah file index.html kedalamnya. Hal ini sebagai simulasi dasar ketika kita ingin membangun sebuah webserver + file-file web didalamnya.

Bukalah folder **dockerfile-contoh-2**, disana tersedia 2 buah file yaitu Dockerfile dan **index.html**. Kita tidak perlu tahu isi dari file html tersebut, kita juga tidak perlu tahu bahasa html, tugas kita sebagai orang infrastruktur/devops adalah mengotak-atik Dockerfile nya.

Ini lumrah terjadi karena nanti biasanya para Developer hanya akan memberikan Anda folder semacam ini. Tugas kita adalah memastikan folder aplikasi ini bisa dijadikan image dan dijalankan kedalam container dengan baik.

Sekarang kita coba lihat isi dari Dockerfilenya :

```docker
# this shows how we can extend/change an existing official image from Docker Hub
FROM nginx:latest

# highly recommend you always pin versions for anything beyond dev/learn

WORKDIR /usr/share/nginx/html

# change working directory to root of nginx webhost

# using WORKDIR is prefered to using 'RUN cd /some/path'

COPY index.html index.html

# replace file index.html original with index.html custom
```

**Penjelasan :**

Pada bagian FROM kita menggunakan official image nginx:latest. Sehingga kita sudah tidak perlu mengurusi bagian instalasi dependensi nginx, expose port, dan lain-lainnya seperti yang sudah ada pada Dockerfile official image nginx.

Seperti yang sudah dijelaskan pada bagian komentar (#) diatas, bagian WORKDIR seperti menjalankan perintah pindah direktori “cd”. Kenapa pindah ke direktori /usr/share/nginx/html ? Karena itu adalah folder default tempat meletakkan file-file web untuk nginx.

Setelah kita masuk ke direktori /usr/share/nginx/html, maka kita kopikan file index.html custom yang kita miliki ke dalam folder tersebut.

Jika sudah cukup mengerti, keluarlah dari file Dockerfile tersebut. Sekarang sebelum kita mencoba untuk mem-build image ini dan menjalankannya, kita coba jalankan ulang sebuah container nginx yang default untuk nanti melihat perbedaannya :

```bash
docker container run -p 80:80 --rm nginx
```

Lihat hasilnya di browser :

[*Hasil nginx*](https://lh6.googleusercontent.com/Gmdz3Qu0AnF-vtuvC2f3HjQeMy8pcUOA2pOO6SrYesrRr5RkJiXSL4ePixs1VZvM8HuA6ZHJbVO5V-MUZtJXfkbC4BR6xUvMtkWEDUttkHdKPv7vlJUT54HWG0s9o4RzIMtLdZaBiJLZqsEyeA)

*Hasil nginx*

Tekan CTRL + C untuk menghentikan container tersebut. Baru berikutnya kita coba untuk build image yang baru dengan nama nginx-custom :

```bash
docker image build -t nginx-custom .
```

Nb : pastikan saat melakukan build, Anda sudah berada didalam folder **dockerfile-contoh-2**

Coba lihat, pada proses build image nginx-custom ini, tidak ada lagi proses download dan instalasi yang panjang seperti sebelumnya. Karena kita sudah memiliki image nginx:latest di local dengan image layer yang sama, dan disini yagn terjadi adalah hanya proses mengkopi file index.htmlnya saja.

[https://lh3.googleusercontent.com/-5NGpL6G6AzYvFXnQDtdPaIPVvQXPSQV2gmgNXVGWcWS3s6Pe3DDmddVSf7jx-sVXW1LclDkUIIK1QticPVzccr3OHJZPZ-qNm6tVnVLmXhK2yyxXoDIbnFXTx2nf6avlKxfN9nlGmfY8F0Wzw](https://lh3.googleusercontent.com/-5NGpL6G6AzYvFXnQDtdPaIPVvQXPSQV2gmgNXVGWcWS3s6Pe3DDmddVSf7jx-sVXW1LclDkUIIK1QticPVzccr3OHJZPZ-qNm6tVnVLmXhK2yyxXoDIbnFXTx2nf6avlKxfN9nlGmfY8F0Wzw)

Jika sudah berhasil di build, kita coba untuk menjalankan container ini :

```bash
# docker container run -p 80:80 --rm nginx-custom
```

Lalu lihat hasilnya di browser :

[*Hasil custom dockerfile nginx*](https://lh6.googleusercontent.com/d6OWvGr42L_OVA-GXImbxP4dY2Sij8rfcE1dBJ7y9-7PoFekfVpw8wConw-uBE61iocqT9x6HwJZiRu0gIg69d8vq44cAKyw1NjA-RTsBuoOm9xJm30gVBQM5KxRWocwQvPRtc77KXZqbeWDww)

*Hasil custom dockerfile nginx*