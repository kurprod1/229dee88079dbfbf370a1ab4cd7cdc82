# 8. Setup Webhooks Jenkins

Created: July 21, 2022 2:36 PM

Kali ini kita akan membuat integrasi CI/CD menggunakan Github dan Jenkins menggunakan webhook. Secara konsep, kita sudah mengenal bagaimana CICD berjalan menggunakan Jenkins pada praktikum modul sebelumnya. Namun kali ini kita akan mengintegrasikan Github dan Jenkins menggunakan webhook. Ketika ada **commit** dari repository, Jenkins akan segera melakukan **building** secara otomatis. App yang akan kita build kali ini adalah [https://github.com/sdcilsy/cilist](https://github.com/sdcilsy/cilist).

Sebetulnya kita melanjutkan dari praktikum sebelumnya dimana sebelumnya kita build aplikasi **sosial media**, kali ini [https://github.com/sdcilsy/cilist](https://github.com/sdcilsy/cilist) dengan integrasi menggunakan **webhook**.

[https://lh3.googleusercontent.com/jDJvveEfpsd8pwOFQNiUWc0mHAHcv6nr3IiJI45rino40txJFj5rwZwvywhh89F1cvjYqR38HuuAvnBl4mQFmiSxtOZfLIKmaBGVwJjHlD9A1ukI2-_sS01vNotfk_YIrXCOueHWXe7ctmdq1x60VsLBi0JFrKhjFIXDzEECk-zJVWaFUPMNEPbdIQ](https://lh3.googleusercontent.com/jDJvveEfpsd8pwOFQNiUWc0mHAHcv6nr3IiJI45rino40txJFj5rwZwvywhh89F1cvjYqR38HuuAvnBl4mQFmiSxtOZfLIKmaBGVwJjHlD9A1ukI2-_sS01vNotfk_YIrXCOueHWXe7ctmdq1x60VsLBi0JFrKhjFIXDzEECk-zJVWaFUPMNEPbdIQ)

Dari requirement tidak jauh berbeda dengan praktikum sebelumnya. Karena kita melanjutkan dari praktikum Jenkins pada modul sebelumnya, kita dapat melakukan clone job sebelumnya dan memodifikasi beberapa instruksi build serta file.

# ***Setup* Github Repository**

Aplikasi yang akan kita coba deploy adalah aplikasi **cilist** ([https://github.com/sdcilsy/cilist](https://github.com/sdcilsy/cilist)). Silakan untuk fork repository app cilist.

[https://lh3.googleusercontent.com/M5QdEfZgCmAYYRMXUAB1aWq9-QXziGw0Mds-w2Ser8gdQ-QrJkTpLDO8hzWrkfGkqvJFmpxQf96H-AlkYjowrWhy7OMZWAFyonDH6GpXzEKKbvwiULPNGPS2GnvYjfiDS0WmfwPVAQ1Y-OW9DwE-nLhTHQ7imyn1MXw7Mk2_CspUWrhQUdRh6mCe6g](https://lh3.googleusercontent.com/M5QdEfZgCmAYYRMXUAB1aWq9-QXziGw0Mds-w2Ser8gdQ-QrJkTpLDO8hzWrkfGkqvJFmpxQf96H-AlkYjowrWhy7OMZWAFyonDH6GpXzEKKbvwiULPNGPS2GnvYjfiDS0WmfwPVAQ1Y-OW9DwE-nLhTHQ7imyn1MXw7Mk2_CspUWrhQUdRh6mCe6g)

# ***Setup* Github Webhooks**

Pada bagian ini kita akan coba melakukan ***setup* webhooks** pada **github** yang akan kita hubungkan pada *server* Jenkins yang kita miliki. Kita akan coba melakukan *trigger*, dimana ketika kita melakukan push pada Github maka pada saat itu Jenkins tersebut akan otomatis melakukan *build*.

Pertama buka Repository kita yang ada di github. Kemudian setelah itu klik tombol **Setting** yang ada disamping atas selanjutnya masuk kedalam menu **Webhooks** yang ada disamping kiri menu. Lalu klik **Add webhook**.

[https://lh6.googleusercontent.com/5ZSTRMbxoERqzV3PCMgiYxXfQwiaVhBZ-lsUWzix_SIq63jDAcJoMXzmZpar9TIlUX_MC66JFwJKXN89DJX2uLmFq3G3MGUI39MMAuaqhCdJ4riZTV5IDJT78V5KRekFazrpk1xqEjpA3DQ7cJYFHIaxorQY_QL9IEL7zwhkdd6Rym6KG3jwM60p8Q](https://lh6.googleusercontent.com/5ZSTRMbxoERqzV3PCMgiYxXfQwiaVhBZ-lsUWzix_SIq63jDAcJoMXzmZpar9TIlUX_MC66JFwJKXN89DJX2uLmFq3G3MGUI39MMAuaqhCdJ4riZTV5IDJT78V5KRekFazrpk1xqEjpA3DQ7cJYFHIaxorQY_QL9IEL7zwhkdd6Rym6KG3jwM60p8Q)

Kemudian tambahkan alamat URL dari jenkins yang kita miliki dengan menambahkan ***/github-webhook/*** diujung alamatnya seperti dibawah ini. Biarkan bagian **content type** dan **event trigger** secara *defaults*. Setelah itu simpan.

[*Url webhooks github*](https://lh4.googleusercontent.com/j84KUXpeUfuYe-FwSxgJMtcnAsvcSKoRDfLtiXZQLRW-vZNOCaBZQYEbjRBY-LG8nEdy_IjDl5LdB_XdR-VsdC08Rgu8ppcWODcZjSLd4dr73-a6n9hOBISA-TJ7aAyh0gBXMUPn_H79gRACK0Xg0jezYyDRNmgo2fGdxTo3_plRcw1LnZc0yuDvHg)

*Url webhooks github*

# **Buat Dockerfile dan docker-compose.yaml**

Sekarang kita akan memodifikasi repository yang sudah kita fork dan clone yaitu menambahkan beberapa file untuk menjadikan aplikasi kita menjadi image docker.

Pertama yaitu membuat **Dockerfile** pada directory **database**. Ini digunakan untuk membuat image database. Image ini akan mengekspose port 3306  dan menambahkan beberapa environment variable yang sesuai file .env **backend**. Lalu menambahkan file sql kedalam entry point.

```bash
FROM mysql:latest

ENV MYSQL_ROOT_PASSWORD=s3k0l4hd3v0p5
ENV MYSQL_DATABASE=people
ENV MYSQL_USER=people
ENV MYSQL_PASSWORD=people

ADD crud_db.sql /docker-entrypoint-initdb.d

EXPOSE 3306
```

Selanjutnya yaitu membuat **Dockerfile** pada directory **backend**. Ini digunakan untuk membuat image backend. Image ini akan mengekspose port 5000.

```bash
FROM node:lts-gallium

WORKDIR /app

COPY . /app

RUN apt update && apt install nano -y

RUN npm install

EXPOSE 5000

CMD [ "npm", "start" ]
```

Selanjutnya yaitu membuat **Dockerfile** pada directory **frontend**. Ini digunakan untuk membuat image frontend. Image ini akan mengekspose port 3000.

```bash
FROM node:lts-gallium

ENV NODE_ENV=development

WORKDIR /app

COPY . /app

RUN apt update && apt install nano -y

RUN npm install

EXPOSE 3000

CMD [ "npm", "start" ]
```

Lalu kita akan membuat file **docker-compose.yaml** yang akan kita simpan di **working directory**. Docker compose ini bertugas untuk membuat service db, backend, dan frontend dari masing masing image yang akan kita build pada **Remote Server**. Pada service backend dan frontend dibutuhkan environment variable. Silakan ubah sesuai dengan variable yang sesuai.

Tag sengaja kita buat menggunakan environment variable karena, tiap build menghasilkan string yang berbeda. Silahkan ubah image sesuai dengan registry docker hub masing masing.

```bash
version: '3.8'

services:
  database:
    container_name: cilist-db
    image: profesorgreen36/cilist-db:${GIT_COMMIT_SHORT}
  
  backend:
    image: profesorgreen36/cilist-be:${GIT_COMMIT_SHORT}
    ports:
      - "5000:5000"
    depends_on:
      - database
    environment:
      - BASE_URL_PORT=5000
      - MYSQL_ROOT_PASSWORD=s3k0l4hd3v0p5
      - DATABASE_USERNAME=people
      - DATABASE_PASSWORD=people
      - DATABASE_DATABASE=people
      - DATABASE_HOST=database
      - DATABASE_PORT=3306
  
  frontend:
    image: profesorgreen36/cilist-fe:${GIT_COMMIT_SHORT}
    ports:
      - "3000:3000"
    environment:
      - REACT_APP_BACKEND_URL=http://localhost:5000
5000
```

Pada environment variable **REACT_APP_BACKEND_URL** kita masukan public dns dari **remote server** seperti dibawah.

[https://lh5.googleusercontent.com/I3ktGRu61fcDUzmiPAl-OLQh5cG1RtiTKv78RY6QgHTQpIzTL5XNE1Nn0Kax2u2sISw8Wm8wYIYS69qy2MFjytMsJh8cKBfMS4I9A4_o9W0_l2tOfcbMiHxUC2sEUAYlTBtMRFWAjW0UDcQzbR2oXuRwOtoyvhbHo3paJohz2lzz4VW29ebT4qINmg](https://lh5.googleusercontent.com/I3ktGRu61fcDUzmiPAl-OLQh5cG1RtiTKv78RY6QgHTQpIzTL5XNE1Nn0Kax2u2sISw8Wm8wYIYS69qy2MFjytMsJh8cKBfMS4I9A4_o9W0_l2tOfcbMiHxUC2sEUAYlTBtMRFWAjW0UDcQzbR2oXuRwOtoyvhbHo3paJohz2lzz4VW29ebT4qINmg)

Nantinya repository local kita akan menjadi seperti ini.

[https://lh3.googleusercontent.com/8x5_9URIfNu-n78RXm2_RATmuxtPwTTKsLrjxh0AS9qrxE1POUrm0Dut1g7vubzBLPZrY3eRC9xN-kefpVtLReK3mjAJlY8dryS7Rl7aJul3Pxhb6dyCTcSzGTzDOYeACQHT9A7-JyJY0sEd9dov0WK9yzWUNhOXhcpgq6iBFyK9xBpJaUAXsKkxfg](https://lh3.googleusercontent.com/8x5_9URIfNu-n78RXm2_RATmuxtPwTTKsLrjxh0AS9qrxE1POUrm0Dut1g7vubzBLPZrY3eRC9xN-kefpVtLReK3mjAJlY8dryS7Rl7aJul3Pxhb6dyCTcSzGTzDOYeACQHT9A7-JyJY0sEd9dov0WK9yzWUNhOXhcpgq6iBFyK9xBpJaUAXsKkxfg)

Setelah itu, teman teman bisa commit ke registry.

```bash
git add .    
git commit -m "add Dockerfile"
git push
```

# **Clone Job**

Agar tidak ribet setup job lagi, kita akan melakukan clone job dari praktikum sebelumnya dengan catatan sudah mengerjakan praktikum di modul sebelumnya.

Pertama kita akan membuat **New Item** dan masukan nama **cilist**. Namun kita akan copy dari Job yang sudah ada. Dengan memasukan opsi paling bawah **Copy from**, masukan nama job yang sudah ada. Pada kasus ini, **pesbuk**. Lalu klik OK.

[https://lh3.googleusercontent.com/hpPShAKcQWXEeF_PoRoA75WTIMuPJBxg7mCgSqsbQtnVYUo7p-rkXKosxCki6og6tlAtuZkMPMO0PGZ3gLd4QRGoPV9MRzwrIRwvlXbi-12Ut7d1HSulnk9f0wzGltscjc_Qn0lGELD-tdpn1AI2CVI-F8zOFladPQLmhJOChbQakJvqGYlum-Riug](https://lh3.googleusercontent.com/hpPShAKcQWXEeF_PoRoA75WTIMuPJBxg7mCgSqsbQtnVYUo7p-rkXKosxCki6og6tlAtuZkMPMO0PGZ3gLd4QRGoPV9MRzwrIRwvlXbi-12Ut7d1HSulnk9f0wzGltscjc_Qn0lGELD-tdpn1AI2CVI-F8zOFladPQLmhJOChbQakJvqGYlum-Riug)

Setelah itu, kita dapat memodifikasi Job baru ini.

Ubah repository menjadi repository yang sudah di fork.

[https://lh6.googleusercontent.com/ru9WOrKPi1MlBHhVj9PeOr2XL-fJ_tkGIT6vpNX1GPUUkvV-6DvhzNR-wJboXieBM21o3KMPr96o8W_xVd3-_ojK8a8yq4-UyN7qhoRos1A5jhRhUYw9b-jFUkLyPh1nndhUBYAP8hFV6JElM0dG6LiMECA0C66g3zx5WB537lN9OWUN3ENmc4bDVw](https://lh6.googleusercontent.com/ru9WOrKPi1MlBHhVj9PeOr2XL-fJ_tkGIT6vpNX1GPUUkvV-6DvhzNR-wJboXieBM21o3KMPr96o8W_xVd3-_ojK8a8yq4-UyN7qhoRos1A5jhRhUYw9b-jFUkLyPh1nndhUBYAP8hFV6JElM0dG6LiMECA0C66g3zx5WB537lN9OWUN3ENmc4bDVw)

Pada section **Build Trigger**, pilih **GitHub hook trigger for GITScm polling**. Ini lah yang akan menjadikan build dilakukan secara otomatis jika ada perubahan pada repository karena integrasi menggunakan webhook.

[https://lh6.googleusercontent.com/taZBYKrGWVNeS5VfXJ-58ty6KczM0iVloYr_j61c0-ev7lkf07plOdVCnRN5c5U7PRprv8mQ65G0BF63MAGHl8TjaokJparvXteVCIuvaj10N2VTpzfHzcVubgiLQzwUnc1A6kuz0f_Kbg9Cuw57H8LDOrFh8oISZy4TpLFbl_Nlu8IkQLgsUXk8dA](https://lh6.googleusercontent.com/taZBYKrGWVNeS5VfXJ-58ty6KczM0iVloYr_j61c0-ev7lkf07plOdVCnRN5c5U7PRprv8mQ65G0BF63MAGHl8TjaokJparvXteVCIuvaj10N2VTpzfHzcVubgiLQzwUnc1A6kuz0f_Kbg9Cuw57H8LDOrFh8oISZy4TpLFbl_Nlu8IkQLgsUXk8dA)

Pada section **Build**, kita modifikasi command yang sudah ada, menjadi seperti berikut.

Command tersebut akan membuat masing masing image sesuai context (database, backend, dan frontend), tagging, serta push ke docker hub.

```bash
export GIT_COMMIT_SHORT=$(echo $GIT_COMMIT | head -c 7)

docker build database -f database/Dockerfile -t cilist-db:$GIT_COMMIT_SHORT
docker tag cilist-db:$GIT_COMMIT_SHORT profesorgreen36/cilist-db:$GIT_COMMIT_SHORT
docker push profesorgreen36/cilist-db:$GIT_COMMIT_SHORT

docker build backend -f backend/Dockerfile -t cilist-be:$GIT_COMMIT_SHORT
docker tag cilist-be:$GIT_COMMIT_SHORT profesorgreen36/cilist-be:$GIT_COMMIT_SHORT
docker push profesorgreen36/cilist-be:$GIT_COMMIT_SHORT

docker build frontend -f frontend/Dockerfile -t cilist-fe:$GIT_COMMIT_SHORT
docker tag cilist-fe:$GIT_COMMIT_SHORT profesorgreen36/cilist-fe:$GIT_COMMIT_SHORT
docker push profesorgreen36/cilist-fe:$GIT_COMMIT_SHORT
```

---

Untuk bagian **Send file or execute command over SSH** kita tambahkan command dibawah untuk memberikan waktu service **backend** untuk konek ke **database** selama 40 detik.

```bash
sleep 40

docker compose restart backend
```

---

[https://lh5.googleusercontent.com/DSZu5Wvm6EFXmHBvruvG2SBskxKn6LTxUHQ9aq62gp8u-TugCPrdpRxy2PiodSVS00BsBsfwCkysVxUUvjDPey5rPewDW5AWJBMCZP4YxFKB4VWSbMLiRKr1-uYtSCgQ3SQpAQlMy8UeiVlGa2vxj5O3h0iUjkdPp8wG29Npc_3F2dUlzXt2W1m0cg](https://lh5.googleusercontent.com/DSZu5Wvm6EFXmHBvruvG2SBskxKn6LTxUHQ9aq62gp8u-TugCPrdpRxy2PiodSVS00BsBsfwCkysVxUUvjDPey5rPewDW5AWJBMCZP4YxFKB4VWSbMLiRKr1-uYtSCgQ3SQpAQlMy8UeiVlGa2vxj5O3h0iUjkdPp8wG29Npc_3F2dUlzXt2W1m0cg)

Lalu kita bisa save Job.

# **Testing**

Jika pada praktikum sebelumnya kita melakukan build secara manual dengan mengklik **Build Now** pada Job, sekarang karena sudah kita pasangkan webhook, testing dilakukan dengan memodifikasi file yang ada pada directory, lalu lalukan push.

Misalnya edit **README.md** sehingga ada perubahan pada repository local. Lalu lakukan push ke remote repository.

```bash
git add .
git commit -m "edit readme"
git push
```

---

Maka secara otomatis, rangkaian build Jenkins akan dimulai.

[https://lh6.googleusercontent.com/tjs_C5g6VRsqXFukjSxfCBbV7XmdU3F1aVr1jFUMbWoicNIVU54BqYQLVxs31NdMsQh1LaGWuQnTlnwCzZ0vi6qF-fHk5CHZZh9wBFWuUXStr_buGxcMo4AXL1FyVuxGjtXamtkv05825KmNEneDi7JgOhnDsQRBzsgiqNTlcdnh5UrsLfqXGRuVdw](https://lh6.googleusercontent.com/tjs_C5g6VRsqXFukjSxfCBbV7XmdU3F1aVr1jFUMbWoicNIVU54BqYQLVxs31NdMsQh1LaGWuQnTlnwCzZ0vi6qF-fHk5CHZZh9wBFWuUXStr_buGxcMo4AXL1FyVuxGjtXamtkv05825KmNEneDi7JgOhnDsQRBzsgiqNTlcdnh5UrsLfqXGRuVdw)

Kita dapat mengakses aplikasi dengan mengakses address **remote server** dengan port 3000.

[https://lh6.googleusercontent.com/evrhVyNzWGsMjyQnTWWgvgbQc741_pEFnrFLEKiVl3r_oKKrD_BaU-rkzH0MLvXSRgpRoxMypY6MF42Um2XZC9iBVFNNTbcvVHjEhACYFwExMgEqJHnHdsmKC6tnEYv7dQPCVhVIVlWqgI4szhjHM20_MuP1Y8noDBXYesNL0hskMxb1I1yk-ZW0-Q](https://lh6.googleusercontent.com/evrhVyNzWGsMjyQnTWWgvgbQc741_pEFnrFLEKiVl3r_oKKrD_BaU-rkzH0MLvXSRgpRoxMypY6MF42Um2XZC9iBVFNNTbcvVHjEhACYFwExMgEqJHnHdsmKC6tnEYv7dQPCVhVIVlWqgI4szhjHM20_MuP1Y8noDBXYesNL0hskMxb1I1yk-ZW0-Q)