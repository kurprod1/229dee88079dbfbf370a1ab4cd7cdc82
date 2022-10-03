# 6. My First CICD

Created: September 14, 2022 11:35 AM

Kita sudah mengenal tentang CICD dan salah satu tools CICD yaitu Jenkins. Kali ini kita akan membuat sebuah CICD menggunakan Jenkins pada aplikasi [https://github.com/sdcilsy/sosial-media](https://github.com/sdcilsy/sosial-media).

Aplikasi yang sudah disimpan di Github, akan kita build menjadi image Docker dan menyimpannya di Docker Hub. Setelah itu kita akan mendeploy image tersebut ke remote repository menggunakan Jenkins.

![https://lh4.googleusercontent.com/JDrV5O6VYAI5Vz32gxeGB-_SC0gBAifILfzSAadqOHDtYGiEeE5wRMqwKMeWzL7W56a-1Ge4USbGNpEOg72VZP2A7cyJSc2wC09Pq1cwNFDCwqrrdCMlyczgpA_IITGsFo-d-1u7ovMrZ7kRXPiD_8M3OWN7ykHLFdstjw7Er1BSGi8grEY0UiGPIA](https://lh4.googleusercontent.com/JDrV5O6VYAI5Vz32gxeGB-_SC0gBAifILfzSAadqOHDtYGiEeE5wRMqwKMeWzL7W56a-1Ge4USbGNpEOg72VZP2A7cyJSc2wC09Pq1cwNFDCwqrrdCMlyczgpA_IITGsFo-d-1u7ovMrZ7kRXPiD_8M3OWN7ykHLFdstjw7Er1BSGi8grEY0UiGPIA)

Tapi sebelum kita memulai, ada beberapa requirement:

1. Dua buah instance EC2 dengan 1 buah server Jenkins dan 1 buah server remote.
2. Akun docker hub ([https://hub.docker.com/signup](https://hub.docker.com/signup)).
3. Pada server Jenkins dan remote server, masing masing sudah terinstall Docker.

# **Setup Repository**

Seperti yang sudah disebutkan di awal, kita akan menggunakan aplikasi sosial media [https://github.com/sdcilsy/sosial-media](https://github.com/sdcilsy/sosial-media). Kita dapat melakukan **forking** untuk membuat repository baru pada akun github masing masing.

![https://lh3.googleusercontent.com/CEitqvTW_VUrk4T6soAYmBp3BUJTPOvFsC6RuMRIgPXjkGuI_MKrddXFUWNAItZSRugS0BGKQGAWGoYGKAoNgnkvbatfYlRFzZUQMToWzrD0Eg745-a2JT4aes97hhopHXrWuqJVCG1JJQDw2SgRbCdS6hCuIQA_6rWLhfsyGyI7BX0CAbIevFDxrg](https://lh3.googleusercontent.com/CEitqvTW_VUrk4T6soAYmBp3BUJTPOvFsC6RuMRIgPXjkGuI_MKrddXFUWNAItZSRugS0BGKQGAWGoYGKAoNgnkvbatfYlRFzZUQMToWzrD0Eg745-a2JT4aes97hhopHXrWuqJVCG1JJQDw2SgRbCdS6hCuIQA_6rWLhfsyGyI7BX0CAbIevFDxrg)

# **Setup User Jenkins**

Sesuai requirement, server Jenkins harus terinstall terlebih dahulu Docker. Setelah itu kita perlu memasukan user jenkins ke grup **docker** dan **root**.

Ini diperlukan karena building akan dilakukan oleh user **jenkins** dan jenkins memerlukan akses terhadap docker agar dapat menjalankan service docker**.**

Pada server Jenkins, kita eksekusi perintah berikut.

```bash
sudo usermod -aG docker jenkins
sudo usermod -aG root jenkins
```

![https://lh3.googleusercontent.com/h7R5cdrIZ0nKi5eIzioOsy0MOQ2E4MBgRmdwqH1546C6qV6iBzNoUtvL6SoduQsKr5KP23jmnQUvCDUYwnzkN0qp3Bned-O2G0bDSRsVpqZX_TcQKEkAsGwn2aSP93OCjRkloIUHnUJGs3drVuy4CnO-VgwLtFIS5yYpqp7_kNqOwmkZP2Z94_Ehnw](https://lh3.googleusercontent.com/h7R5cdrIZ0nKi5eIzioOsy0MOQ2E4MBgRmdwqH1546C6qV6iBzNoUtvL6SoduQsKr5KP23jmnQUvCDUYwnzkN0qp3Bned-O2G0bDSRsVpqZX_TcQKEkAsGwn2aSP93OCjRkloIUHnUJGs3drVuy4CnO-VgwLtFIS5yYpqp7_kNqOwmkZP2Z94_Ehnw)

Setelah itu kita akan menyimpan **kredensial** **docker hub** pada home directory jenkins agar jenkins dapat melakukan push ke docker hub. Kita akan mengeksekusi command sebagai user **jenkins** dengan command berikut. Isi menggunakan kredensial docker hub masing masing.

```bash
sudo su - jenkins
docker login
```

![https://lh3.googleusercontent.com/RIM2-BIH4d7_rdUjXw8mU3oNOJWmzGg-djK-UUSVDVko7wLDPJ0iu3ClZkOeJiqZmQZIFnrqdY71Ce5vPCH54jJzj5u05b3fyDPTrBPomMCPhswwmc6oUOB1s8SrnYoZi6L2AD0Ce0N60UEubkEO1piWvJ93VFFR9HOK9aSpjf0pW1e-8qqWZNLJUw](https://lh3.googleusercontent.com/RIM2-BIH4d7_rdUjXw8mU3oNOJWmzGg-djK-UUSVDVko7wLDPJ0iu3ClZkOeJiqZmQZIFnrqdY71Ce5vPCH54jJzj5u05b3fyDPTrBPomMCPhswwmc6oUOB1s8SrnYoZi6L2AD0Ce0N60UEubkEO1piWvJ93VFFR9HOK9aSpjf0pW1e-8qqWZNLJUw)

Lalu pada Remote Server, kita cukup memasukan user ubuntu ke group docker saja.

```bash
sudo usermod -aG docker ubuntu
```

![https://lh3.googleusercontent.com/7gBYlioiGvQiKsisDpcFVrlHU5wIx6PuTXJqobPlMzFIWRen1CmLxIX8c6F6LdsQKyQectrUrZskDzaqe-ve6ZhZUjCeIxhy7DlP_aCq6y8VcNS39e5memN53TjPNtJUdGFtYXbI7qdNf3GYtoNSG37VESvJHv-8nkrewp9V6WBWLaoM49zCk4RAKw](https://lh3.googleusercontent.com/7gBYlioiGvQiKsisDpcFVrlHU5wIx6PuTXJqobPlMzFIWRen1CmLxIX8c6F6LdsQKyQectrUrZskDzaqe-ve6ZhZUjCeIxhy7DlP_aCq6y8VcNS39e5memN53TjPNtJUdGFtYXbI7qdNf3GYtoNSG37VESvJHv-8nkrewp9V6WBWLaoM49zCk4RAKw)

# **Setup SSH ke Remote Server**

Karena langkah langkah build dilakukan oleh user Jenkins termasuk ssh, kita harus menyiapkan koneksi ssh untuk user Jenkins dengan cara membuat key pair dan menyimpan public key ke remote server.

Kita akan berubah menjadi user jenkins dengan perintah berikut.

```bash
sudo su - jenkins
```

Lalu kita akan membuat key pair untuk koneksi ke remote server menggunakan perintah berikut.

```bash
ssh-keygen -t ecdsa -b 521 -m PEM
```

Keypair sengaja dibuat dengan algoritma ECDSA, karena plugin Jenkins Publish Over SSH memiliki issue dalam membaca algoritma RSA.

![https://lh4.googleusercontent.com/BWhKVIDTu0qKYGdwJxzEULDhzDU5NwaEhsd1kHgtWfabXOfxrH2QOPfF0xgor_sRCT6Ie_3m1jhEc9zfLIrPPuDA2Bhtj7KpfpI3NpPKbHFe6CkHrvxTm2OgFx5Uz7GhYJ4MKpvrB-3Ua4HEdAC-tftsVWcgTiQKBLoX7GB7cHV3fg4tli1pWccKRQ](https://lh4.googleusercontent.com/BWhKVIDTu0qKYGdwJxzEULDhzDU5NwaEhsd1kHgtWfabXOfxrH2QOPfF0xgor_sRCT6Ie_3m1jhEc9zfLIrPPuDA2Bhtj7KpfpI3NpPKbHFe6CkHrvxTm2OgFx5Uz7GhYJ4MKpvrB-3Ua4HEdAC-tftsVWcgTiQKBLoX7GB7cHV3fg4tli1pWccKRQ)

Kita telah membuat private key dan public key di directory .ssh. Kita dapat menyimpan public key ke remote server agar jenkins dapat mengakses remote server.

Caranya dengan mencopy content dari file .**ssh/id_ecdsa.pub** lalu menyalinnya ke file **.ssh/authorized_keys** pada remote server.

![*Isi public key*](https://lh6.googleusercontent.com/ShDINQlhhFLFfgNHYSXrbz09jlAnyuCR9LnMg6uOuJB9ly4thegZHgz5WFOIPqsakEoLNlo_2cmSyj2m6NdILzIdlTOMVUmHBVUUq0K-sRb1oyqGpT-gu94CJ1N-GPJwLXJp8r38lNO3DGT13dgjO0IL0-buOO4HSrvcvmGYXeY64jpJRVys3IbmDg)

*Isi public key*

![*Salin ke authorized_keys*](https://lh6.googleusercontent.com/G-ViaVIOaHSi9fxBzZGDCLskPf2TikegqqWAhCBQAef514ci44b3bimy09ntxH4w3O9hgOeWlPYF26u5GoBfBarSmTrqKIwQgVKp1BZ6Hr3bPaTAdqPDG7r8iNlGNqJWiLw1XFJUGHTY1FlbbcMBw3wuxoQ6cdesJJoXfrofFkGNUQPhwo63AYM1rw)

*Salin ke authorized_keys*

Kita coba untuk melakukan ssh dari Jenkins menggunakan user jenkins ke Remote Server.

```bash
ssh ubuntu@ec2-3-85-128-26.compute-1.amazonaws.com -i .ssh/id_ecdsa
```

---

![https://lh4.googleusercontent.com/jNZlswqHncfLU6qnTSSKFJORfBrRf-OMrNLK8Umxx519_KFi2aTo7Kq68ovqfC_wR0wK93rGfjAdK-vZ2MEATbWuM3vXqIwGJ-PuRLAkY5a0DhtGwVSywx3YhI8jJCy7EC9jhVnNMHanMcZeBHhJFdwN-rAm76719QRgOQ41xqj3SHd1fn3cfDtakQ](https://lh4.googleusercontent.com/jNZlswqHncfLU6qnTSSKFJORfBrRf-OMrNLK8Umxx519_KFi2aTo7Kq68ovqfC_wR0wK93rGfjAdK-vZ2MEATbWuM3vXqIwGJ-PuRLAkY5a0DhtGwVSywx3YhI8jJCy7EC9jhVnNMHanMcZeBHhJFdwN-rAm76719QRgOQ41xqj3SHd1fn3cfDtakQ)

Lalu kita akan mengkonfigurasi remote server melalui plugin Publish Over SSH yang sudah kita install sebelumnya. Klik **Manage Jenkins** lalu **Configure System**.

Scroll sampai paling bawah dan temukan **Publish Over SSH**. Pertama, masukan **Path to key** dengan **.ssh/id_ecdsa**.

![https://lh5.googleusercontent.com/_VoSTSwFZ6k6X7vznYdpklt1SNubL2d8KG_Vil5pDXfdJmu1xOShMKK_VsoTgzBSa44w5fAcKYz1y911TszZoMfibjms7M-GFpT0d5dcU-aLLHJL8AmhtgWojWNGOGAeLpFel7JXS1gZKFUMkGg62CWQ3eixYobK8EF9ZSe1SC-akI5uNxKyT1m1aw](https://lh5.googleusercontent.com/_VoSTSwFZ6k6X7vznYdpklt1SNubL2d8KG_Vil5pDXfdJmu1xOShMKK_VsoTgzBSa44w5fAcKYz1y911TszZoMfibjms7M-GFpT0d5dcU-aLLHJL8AmhtgWojWNGOGAeLpFel7JXS1gZKFUMkGg62CWQ3eixYobK8EF9ZSe1SC-akI5uNxKyT1m1aw)

Kita tambah server dengan klik **Add server**. Lalu isikan **Name**, **Hostname**, dan **Username** sesuai alamat remote server. Ketika kita **test configuration**, jika benar, akan ada notification success. Klik **Save**.

![https://lh4.googleusercontent.com/hz9gG_fl2fpSb80vHOlMMYkfLn_t_81J0UV1bbiZDMKNr5PQMGj7CtJ5bwoDHKbB8mY4VfqRc1K2vFmQGnlm5lvGL-KJZKkq_KYi7a5pxXvtSVFATNaVcEjJ4WAAQcKNF5SIh0-dfRcoF1QYh1xNDwrDVpxbv4j_PqiuS_gWSBYFNclhMDWtv8h7vQ](https://lh4.googleusercontent.com/hz9gG_fl2fpSb80vHOlMMYkfLn_t_81J0UV1bbiZDMKNr5PQMGj7CtJ5bwoDHKbB8mY4VfqRc1K2vFmQGnlm5lvGL-KJZKkq_KYi7a5pxXvtSVFATNaVcEjJ4WAAQcKNF5SIh0-dfRcoF1QYh1xNDwrDVpxbv4j_PqiuS_gWSBYFNclhMDWtv8h7vQ)

# **Buat Dockerfile dan docker-compose**

Sekarang kita akan memodifikasi repository yang sudah kita fork dan clone yaitu menambahkan beberapa file untuk menjadikan aplikasi kita menjadi image docker.

Pertama yaitu membuat **Dockerfile.web** pada working directory. Ini digunakan untuk membuat image web PHP. Image ini akan mengekspose port 80 dan kita instalkan extension mysqli agar PHP dapat mengeksekusi perintah MySQL.

```bash
FROM php:7-apache

WORKDIR /var/www/html

COPY . /var/www/html

RUN docker-php-ext-install mysqli pdo pdo_mysql

EXPOSE 80
```

script dapat dilihat di [https://gist.github.com/sdcilsy/f33e14eee381cd3e6c19123c5ef9d35a#file-dockerfile-web](https://gist.github.com/sdcilsy/f33e14eee381cd3e6c19123c5ef9d35a#file-dockerfile-web)

Lalu kita membuat docker file kedua yaitu **Dockerfile.db** yang digunakan sebagai image database. Disini kita menambahkan beberapa environment variable yang sesuai dengan config database aplikasi. Lalu menambahkan file sql kedalam entry point.

```bash
FROM mysql:latest

ENV MYSQL_ROOT_PASSWORD=1234567890
ENV MYSQL_DATABASE=dbsosmed
ENV MYSQL_USER=devopscilsy
ENV MYSQL_PASSWORD=1234567890

COPY dump.sql /docker-entrypoint-initdb.d

EXPOSE 3306
```

script dapat dilihat di [https://gist.github.com/sdcilsy/f33e14eee381cd3e6c19123c5ef9d35a#file-dockerfile-db](https://gist.github.com/sdcilsy/f33e14eee381cd3e6c19123c5ef9d35a#file-dockerfile-db)

Lalu kita akan membuat file **docker-compose.yaml**. Docker compose ini bertugas untuk membuat service web dan db dari masing masing image yang akan kita build pada **Remote Server**. Tag sengaja kita buat menggunakan environment variable karena, tiap build menghasilkan string yang berbeda. Silahkan ubah image sesuai dengan registry docker hub masing masing.

```bash
version: "3.9"
services:
  web:
    container_name: web
    image: profesorgreen36/sosmed-web:${GIT_COMMIT_SHORT}
    ports:
      - "80:80"
    depends_on:
      - db
  db:
    container_name: db
    image: profesorgreen36/sosmed-db:${GIT_COMMIT_SHORT}
```

script dapat dilihat di [https://gist.github.com/sdcilsy/f33e14eee381cd3e6c19123c5ef9d35a#file-docker-compose-yaml](https://gist.github.com/sdcilsy/f33e14eee381cd3e6c19123c5ef9d35a#file-docker-compose-yaml)

Lalu terakhir, kita edit file **config.php** dan ubah **$db_host** menjadi **db**. Ini agar container web dapat berkomunikasi dengan db melalui service yang akan dibuat.

![https://lh3.googleusercontent.com/UJGn1cfY8dvUugvZ9-W6Xo8yHVO1dHHe9_eeqR8lBkH6wQXTN2VefajfvsAxt9f2D1-FHrE7SPfAp7orPzpd4nh1bgTomMRqYzr2tGFVuD9klA6b-fnogjTVPDi0U2PYh6352fSNZ-1qdRZPLx82qTnn0fgk4YP3PgG5e1AN-jIl8F6lmyv3HRPEqg](https://lh3.googleusercontent.com/UJGn1cfY8dvUugvZ9-W6Xo8yHVO1dHHe9_eeqR8lBkH6wQXTN2VefajfvsAxt9f2D1-FHrE7SPfAp7orPzpd4nh1bgTomMRqYzr2tGFVuD9klA6b-fnogjTVPDi0U2PYh6352fSNZ-1qdRZPLx82qTnn0fgk4YP3PgG5e1AN-jIl8F6lmyv3HRPEqg)

Jika sudah, kita dapat melakukan commit dan push ke repository masing masing.

```bash
git add .    
git commit -m "add Dockerfile"
git push
```

# **Create Job**

Setelah semua siap, saatnya kita membuat job di Jenkins. Kita beri nama **pesbuk**.

![https://lh6.googleusercontent.com/mXFpyKnOWtOwIbdRYT8f-pbe7uBEDfocYsEzUY7l5_MokrHMHM8ZeLmZimHF6PY33CDv1MrQf3I_IcfTFyvO1mkqxesI9SJOMi6o9u9-tk4NEUVg-H7bzzIrgbkXYFrO8GfDUZxAI-LRDhYKmPQ8_qxSDUCIfEqJraRb0xt94VYXygzpqCXBXAMsNQ](https://lh6.googleusercontent.com/mXFpyKnOWtOwIbdRYT8f-pbe7uBEDfocYsEzUY7l5_MokrHMHM8ZeLmZimHF6PY33CDv1MrQf3I_IcfTFyvO1mkqxesI9SJOMi6o9u9-tk4NEUVg-H7bzzIrgbkXYFrO8GfDUZxAI-LRDhYKmPQ8_qxSDUCIfEqJraRb0xt94VYXygzpqCXBXAMsNQ)

Pada section **Source Code Management**, kita isikan url git masing masing beserta credential github.

![https://lh6.googleusercontent.com/WZd6oS2rShSkV4YQJioJrqkqljNXIxex9ptPQnp0Wkn4NWEtx0mUORDRE3opDTXnfR1LysuJoOGmNKSZnWBHqIvHtwyhPHoDcPAkqaKtOrmLk06JlIWXFVTKceR7Gk6A0_jf1gHOQ3Iu1Eip6hV1DhzWeR6KTObQiWSajDOkXNdgz7OkP3Q6eaRjzw](https://lh6.googleusercontent.com/WZd6oS2rShSkV4YQJioJrqkqljNXIxex9ptPQnp0Wkn4NWEtx0mUORDRE3opDTXnfR1LysuJoOGmNKSZnWBHqIvHtwyhPHoDcPAkqaKtOrmLk06JlIWXFVTKceR7Gk6A0_jf1gHOQ3Iu1Eip6hV1DhzWeR6KTObQiWSajDOkXNdgz7OkP3Q6eaRjzw)

Pada section **Build Trigger** dan **Build Environmental**, kita kosongkan untuk saat ini.

Pada section **Build**, kita akan mengeksekusi beberapa command untuk membuat docker image.

```bash
export GIT_COMMIT_SHORT=$(echo $GIT_COMMIT | head -c 7)

docker build . -f Dockerfile.db -t sosmed-db:$GIT_COMMIT_SHORT
docker tag sosmed-db:$GIT_COMMIT_SHORT profesorgreen36/sosmed-db:$GIT_COMMIT_SHORT
docker push profesorgreen36/sosmed-db:$GIT_COMMIT_SHORT

docker build . -f Dockerfile.web -t sosmed-web:$GIT_COMMIT_SHORT
docker tag sosmed-web:$GIT_COMMIT_SHORT profesorgreen36/sosmed-web:$GIT_COMMIT_SHORT
docker push profesorgreen36/sosmed-web:$GIT_COMMIT_SHORT
```

---

Command command diatas, terdiri dari

- **export GIT_COMMIT_SHORT=$(echo $GIT_COMMIT | head -c 7)**

Membuat environment variable dengan 7 karakter pertama SHA commit.

- **docker build**

Membuat image docker di local dengan tag GIT_COMMIT_SHORT.

- **docker tag**

Memberi tag kredensial Dockerhub untuk setiap image.

- **docker push**

Melakukan push ke registry docker hub.

![https://lh6.googleusercontent.com/3v1ipV2BbGWK4WFzWxKf1iPmxIBelP2Ib14ee04C4OxN_-ScLuPPir7GkswWi-3pQpOdk3rxuBj3sXZ9w2_fqxtkEl_UlSwY0TuzhrTQSd3dFptb6bfVhxkbmp1eOInDab-7-sK52dtuSOSL6D0aZCX9ty8-fD4fYA9gjwqiEoNe9RVpom83JNsLsQ](https://lh6.googleusercontent.com/3v1ipV2BbGWK4WFzWxKf1iPmxIBelP2Ib14ee04C4OxN_-ScLuPPir7GkswWi-3pQpOdk3rxuBj3sXZ9w2_fqxtkEl_UlSwY0TuzhrTQSd3dFptb6bfVhxkbmp1eOInDab-7-sK52dtuSOSL6D0aZCX9ty8-fD4fYA9gjwqiEoNe9RVpom83JNsLsQ)

Setelah itu, tambahkan **Build Step** Send file or execute command over SSH. Kita akan mengirimkan file **docker-compose.yaml** ke Remote Sever untuk deployment. Oleh karena itu, isi Source file dengan **docker-compose.yaml.**

Lalu kita deploy dengan menjalankan command berikut.

```bash
export GIT_COMMIT_SHORT=$(echo $GIT_COMMIT | head -c 7)

echo "GIT_COMMIT_SHORT=$(echo $GIT_COMMIT_SHORT)" > .env

docker compose up -d
```

Command diatas akan membuat environment variable pada remote server dari environment variable jenkins. Lalu membuat file .env untuk **docker-compose.yaml**. Terakhir, kita menjalankan command docker compose untuk mendeploy aplikasi.

![https://lh5.googleusercontent.com/0OU0iza2ixoySDkwhzQ4kw4dPq48Yu8d4AxAZGn2Shm2oQ_cI5Eeg351jSU_NFbp2adGxJ-z8piDX02ZDHOOc3untgX1i8md6HaIuOxJIKeGOV6h-AEWANVSBBknwPpukOS3EFmVK1I84R3HUk7CQXoWD7kcj0y6gfjVOHPCxJDdzY7UwENtqwen8A](https://lh5.googleusercontent.com/0OU0iza2ixoySDkwhzQ4kw4dPq48Yu8d4AxAZGn2Shm2oQ_cI5Eeg351jSU_NFbp2adGxJ-z8piDX02ZDHOOc3untgX1i8md6HaIuOxJIKeGOV6h-AEWANVSBBknwPpukOS3EFmVK1I84R3HUk7CQXoWD7kcj0y6gfjVOHPCxJDdzY7UwENtqwen8A)

Tinggal kita save job yang sudah kita buat.

# **Testing**

Jalankan job yang sudah kita buat, dengam mengklik Build Now seperti di bawah.

![https://lh6.googleusercontent.com/lq73OIe2jvcrXzfYnlPseMursw8HVh6lMBhLDvWyZKaDRFqL8s5EdIwpo58Y6bLy03EZKUciXYnGHaaNS2RfnNI5rdbAmTalt26sPpCLLMZIO5LqykBfEBl7mejMX-zA9ZgO5tkQ3MRDZs9D1uFlhGbpJdyak-_VstT1TFxZii540ugrKdc4s9RV1A](https://lh6.googleusercontent.com/lq73OIe2jvcrXzfYnlPseMursw8HVh6lMBhLDvWyZKaDRFqL8s5EdIwpo58Y6bLy03EZKUciXYnGHaaNS2RfnNI5rdbAmTalt26sPpCLLMZIO5LqykBfEBl7mejMX-zA9ZgO5tkQ3MRDZs9D1uFlhGbpJdyak-_VstT1TFxZii540ugrKdc4s9RV1A)

Jenkins akan melakukan build mulai dari build docker image, tagging, push registry, hingga deployment ke remote server, sesuai instruksi yang sudah kita buat di dalam Job.

![https://lh6.googleusercontent.com/J7m5HFndGwmCcX8Scztk-S2sZ4RoESjRKR5o0GC1NhzDfjxybFOGA2KSLErYiGN68isITniS5cELhAnn0oeZSrMOp1plvhBa5kaf96mim3TAPqFCNEU_9uRlk35L5bepfLOYu1MOkOSS01l9E1jetuY-MPKYSXsdWFOaHYVyBzwTKlPZCOMy4_EKcQ](https://lh6.googleusercontent.com/J7m5HFndGwmCcX8Scztk-S2sZ4RoESjRKR5o0GC1NhzDfjxybFOGA2KSLErYiGN68isITniS5cELhAnn0oeZSrMOp1plvhBa5kaf96mim3TAPqFCNEU_9uRlk35L5bepfLOYu1MOkOSS01l9E1jetuY-MPKYSXsdWFOaHYVyBzwTKlPZCOMy4_EKcQ)

Lalu kita dapat melihat hasil deployment dengan mengakses ip/dns public dari remote server.

![https://lh5.googleusercontent.com/UJK9LD_7316w0XfHITWRqKQ0OGmOD07jEZ43uYR_r5rAoKGc1xNXyW2wljWjfuvotOZoe_1us0dv8UF7cfR4vLDaNARf8eIc4MdJpMvUXv1PGyP8n506s7Z_DryBeY6bnMKlMCznHvcIiJ1ec1niTOQWrA-p1ArWs1OZ68EWE0hvyKiGNJqkOEmsQg](https://lh5.googleusercontent.com/UJK9LD_7316w0XfHITWRqKQ0OGmOD07jEZ43uYR_r5rAoKGc1xNXyW2wljWjfuvotOZoe_1us0dv8UF7cfR4vLDaNARf8eIc4MdJpMvUXv1PGyP8n506s7Z_DryBeY6bnMKlMCznHvcIiJ1ec1niTOQWrA-p1ArWs1OZ68EWE0hvyKiGNJqkOEmsQg)