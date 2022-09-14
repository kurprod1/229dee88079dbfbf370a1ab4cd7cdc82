# 8. Remote Repository

Created: July 14, 2022 1:30 PM

Pada proyek pengembangan software yang melibatkan banyak orang (tim), kita tidak hanya akan menyimpan sendiri repository proyeknya. Semua tim yang terlibat dalam pengkodean (coding) akan menyimpan repository lokal di komputernya masing-masing. Setelah itu, akan dilakukan penggabungan ke repository inti atau remote. Biasanya akan ada repository pusat atau untuk menyimpan source code yang sudah digabungkan (merge) dari beberapa orang.

[*Ilustrasi remote repository*](https://lh6.googleusercontent.com/4o0fqExZs9RYO5aOHfzo5qvSmrI-38J1b8OkgN9gDxfjhRee7Ga76DYRfziAGcmFZwL6JssGGiZnMJUejxbrm3FPMIXmIQ4jlHA8H2yXSYqp-2aAuv0UnCLcuVHQTVR3ywgga-rSwbC6xzgD7w)

*Ilustrasi remote repository*

Di mana menyimpan repository remote-nya? Bisa di server kantor atau bisa juga menggunakan layanan seperti Github, Gitlab, Bitbucket, dll. Github adalah layanan yang paling populer untuk menyimpan (hosting) repository secara remote. Banyak proyek open source tersimpan di sana. Kita akan menggunakan Github pada tutorial ini, pastikan Anda sudah memiliki akun Github dengan cara mendaftar di **github.com.**

# **Membuat Repositori di GitHub**

Silahkan buka Github, kemudian buat sebuah repository dengan nama belajar-git seperti berikut ini.

[*Membuat repository 1*](https://lh4.googleusercontent.com/sbdVSqZzeKIeXjS9rJyrqwmpsoNiHPyznmCp104M1nuD8Czop4Pf1MJWRlHfuzwBmzcISk01u1c0SyZMFpg6BSGeKWiJgPLmP-dPXVoat-TpKmsx5qnGn-wNaGuo6yymG79JgyfcmKlc3l5ERg)

*Membuat repository 1*

Maka sekarang kita punya repository kosong bernama belajar-git di Github.

[*Membuat repository 2*](https://lh5.googleusercontent.com/QG97J3unfsEhOnEdh0pRn0W68c07Lu6m8eKyp-aEg2TJ0c1ZVJsucjUDK4qqKb4uR0ug7swpqLC164TDBJ1QlsWHP61xcTqcUbFTdtFIcoTltmhVqeYC2rz3ddybRGcVZIyWa78yUfrTHxU_OA)

*Membuat repository 2*

Silahkan buka kembali repository lokal yang pernah kita buat, yaitu **cilsy**. Berikutnya kita akan coba upload repository lokal ini ke repository remote Github.

# **Menambah Remote Repository**

Sebelum kita bisa upload semua revisi yang ada di repository lokal, kita harus menambahkan remote repository-nya terlebih dahulu. Remote repository dapat kita tambahkan dengan perintah seperti ini :

```bash
git remote add github [https://github.com/username/belajar-git.git](https://github.com/username/belajar-git.git)
git remote add github git@github.com:username/belajar-git.git
```

Perbedaan https dengan SSH adalah bentu autentikasinya. Untuk https, kita akan diminta user dan password setiap kali melakukan push, sedangkan SSH, kita hanya melakukan 1 kali autentikasi, yaitu dengan mendaftarkan public key kita ke repository.

# **Menggunakan SSH di GitHub**

SSH memungkinkan kita untuk melakukan push ke repository github tanpa login. Berbeda dengan cara yang biasa (melalui HTTPS), kita harus memasukkan username dan password setiap kali melakukan push. Tapi dengan SSH kita tidak akan melakukan itu lagi. Berikut adalah langkah-langkahnya.

## ***Membuat SSH Key.***

Pertama-tama kita akan membuat sebuah SSH Key. SSH Key ini adalah sebuah kombinasi 2 file terenkripsi (publik dan private) yang akan dicocokkan antara di server Remote repository dengan di lokal (pc/laptop). Ketika 2 file ini dinyatakan cocok, maka kita dianggap sebagai orang yang punya autentikasi tanpa perlu memasukkan password dan username lagi. Cara untuk membuat ssh key adalah masuk ke terminal dan ketikkan ssh-keygen lalu enter. Untuk passphrase dikosongkan saja.

[*Membuat SSH-Key*](https://lh6.googleusercontent.com/gU4GCngoUKdqf1zH4C6z3N1ntJswiOd4pdQmmisG4SYQbY0qrfPD-xJM8gPTvONR3EqnS9dSrjL4gRVjgzJq5c_X2XJcICx51vWsQ-M4Fwr6asZK9zV-cXEaFHyLwoWkZhCqXDGqMpw3rILLgg)

*Membuat SSH-Key*

Maka di dalam directory .ssh akan tercipta file baru yaitu id_rsa sebagai private key dan id_rsa.pub sebagai public key.

[*Public key dan private key*](https://lh5.googleusercontent.com/3tO5-nQfQxDeFK_jit4Ft2KJoJo1DP-sR2WlRjTJssCDhxOxvo9DdPoK3AlU4KjTl1Nq8FvmkhErAeQp6lAU7dpFJM8qVsEncJYTfBqpq1SHmf93enANXx2vFSFVgI6R3s-SziSrkTepbXsltg)

*Public key dan private key*

## ***Jalankan SSH Agent dan Load SSH Key***

Untuk memastikan apakah SSH Agent sudah berjalan atau tidak, gunakan perintah ini:

```bash
ps -e | grep [s]sh-agent
```

Kalau belum berjalan, gunakan perintah berikut ini untuk menjalankan SSH agent:

```bash
ssh-agent /bin/bash
```

Berikutnya kita Load SSH Key. Gunakan perintah:

```bash
ssh-add ~/.ssh/id_rsa
```

Kemudian untuk mengecek, gunakan perintah:

```bash
ssh-add -l
```

Tambahkan SSH Key ke Github. Sebelumnya ambil dulu publik key yang sudah anda buat, gunakan perintah cat.

```bash
cat ~/.ssh/id_rsa.pub
```

Copy isi teks yang ditampilkan. Lalu kembali ke Github, masuk ke menu **Settings> SSH and GPG Keys**, buat key baru dengan mengklik **New SSH Key**. Lalu masukkan key yang sudah dicopy.

[*Meng-input SSH Key di Github*](https://lh4.googleusercontent.com/0qf3CZdRWMXwyvQc3X2T5bLmtRgaOJatKoWe7OZAdbBLRwEzmrFRy_nvfwuLbqXl9ZvyNz-sAS1kV3Upv6Cx8_glQCnMA6M0TPxeDMe5v4BX7x-2aAXZjKvqbaqjit_KN8s6ryx60vwjx2XQPQ)

*Meng-input SSH Key di Github*

Sekarang seharusnya laptop Anda sudah terhubung dengan remote repository dengan metode SSH.

## ***Uji Konektivitas***

Ketik perintah berikut untuk menguji konektivitas SSH ke Github :

```bash
ssh -T git@github.com
```

Pastikan tidak ada pesan error yang muncul untuk memastikan bahwa konektifitas Github dengan SSH sudah berhasil.

# ***Mengubah dan Menghapus Remote Repository***

Silahkan ketik perintah *git remote -v* untuk melihat remote apa saja yang sudah ditambahkan.

[*Mengubah dan menghapus remote repository*](https://lh6.googleusercontent.com/0OzTxbw3w2sAwcF0vcdIXQyS84muPH0Stm85pzWZsd7QQ8sb5Rls1sXab3SHJ3jXB5DY8_Jc-Xg_uKhvLFTL9IwQYo5THDQ9vN0wYz3WLpzDB6d8lzmSkMBkR8UWXCbtb5kMF7nwcx2Yb0XYdQ)

*Mengubah dan menghapus remote repository*

Sekarang kita sudah menambahkan remote di dalam repository lokal. Selanjutnya kita bisa melakukan push atau mengirim revisi ke repository remote (Github). Nah untuk menghapus dan mengubah nama remote dapat dilakukan dengan perintah berikut.

Ubah nama remote:

```bash
git remote rename github kantor
```

*Keterangan : github adalah nama remote yang lama, kantor adalah nama remote yang baru.*

Hapus remote:

```bash
git remove github
```

# **Mengirim Revisi ke Remote Repository**

Perintah yang kita gunakan untuk mengirim revisi ke repository remote adalah git push.

```bash
git push github master
```

Keterangan: github adalah nama remote, master adalah nama branch tujuan.

Mari kita coba, pastikan repository lokal kita sudah memiliki remote.

[*Mengirim revisi*](https://lh3.googleusercontent.com/1XKFJiEUyIkbj-SdMj8rNJAljb9vpOVrd5cwsL7lvHbL9z1tvVscYcQ9NG6F33n0Da7-rUQoBkHcAGjnRF7eoLPMNWHBhPylRX9H4vsU-3hBlkZmDls7cgK5qv4IN9_9GB-JYuyMj0ijdkP0Jw)

*Mengirim revisi*

Setelah itu lakukan beberpa revisi atau commit.

```bash
git add .
git commit -m "menambahkan beberapa revisi"
```

Sebagai contoh, disini ada 5 catatan revisi.

[*Menampilkan catatan revisi*](https://lh4.googleusercontent.com/aUAKE-t0CmO6azSGbxfCQWfNt3phNNmjTSXJgTN6owTMYn4xxLmsfRkFZl5U0RlYZz44bgPaTlI2nCcabAtTJ415VDSY-h4L8xEJm7xjxreHryQQOZ8HWx2xSUfQDvk0Z9c11AZ148iHw0kRpg)

*Menampilkan catatan revisi*

Maka tinggal kita kirim saja dengan perintah git push github master. Jika muncul seperti ini, artinya push sukses dilakukan.

[*Melakukan push*](https://lh5.googleusercontent.com/feDUeeLtiS_5IPqJpyrzi_t-_mtQCh4EPjZ9FdhMz9ioDeM0W-d6zP_BjS6evuuNCkJBuvCQfxm38lA2hUX3ERtVqGrunpdR5lnbF_tBzUJi8Mgtqxn3UxJwYcdyNSh3dQ9D6xxDflXxik-n3w)

*Melakukan push*

Sekarang lihat ke Github, pasti semuanya sudah ter-upload ke sana.

[*Memeriksa hasil push*](https://lh4.googleusercontent.com/5cti9zBojQmqod0vPgJZYq8EOsp3QRsqr8P2GPJXuBn0rDzCIYmBKfbav2uOCYpAPCZnNHKge5n556vuss42UET9WctVY33-zvU_Y_BIPvA6ffJ8i5KGNRXTb5j163HzOEBqWxVYybEfJHp2DA)

*Memeriksa hasil push*

Coba buat revisi lagi di file index.html. Misalnya perubahannya seperti ini:

[*Melakukan perubahan file index.html*](https://lh4.googleusercontent.com/PFVOkhyQc5LUhn7-y4hs-aEOJEOJGsRYiJCsHTt9UlZofrNMaV2tR3rWYU_dcsvRFGTjXEaDA3bTagbGPaRrqUabEAte-RV7DEQTIKBKemthsY6ZJlmK9N6IoGQXcjIAXF_H7KcPtP6ym4FUOA)

*Melakukan perubahan file index.html*

Lalu lakukan commit dan push.

```bash
git add index.html
git commit -m "mengubah judul dan teks di body"
git push github master
```

Jika berhasil, maka akan tampil seperti ini:

[*Hasil push perubahan*](https://lh5.googleusercontent.com/DAPrtxezWQSkht1_SF50pefTCPkIGKEVwEcGzydaM2up4VOoU_ptOANY4DSvKUVfe6_NzrzEz2-wfv75_eYn5w15Y8eAHe-uiNQqbHTUFvWA1zro-8c6d1dPj5A-7t5opAYHGtPT3aGGYgNMZw)

*Hasil push perubahan*

Periksa kembali repository di Github dan perhatikanlah perubahannya.

[*Melihat hasil di Github*](https://lh3.googleusercontent.com/Pw1gHx3_TXYMDFrH6vl1aOx54ZOIc_PODVBXRHrQ4sbmalQ8DJGfDtRDwZ18nRqbzLt0O5Ds6qiVphb1Cn3cytlqzrWaJqQ-tVOBTj1a4WGcuFunnB7HfBAbOZrGK0noj6L2Uimb2aewDh3H6A)

*Melihat hasil di Github*

Jika kita klik commit terakhir, maka kita akan dibawa ke *git diff*-nya Github. Di sana kita bisa melihat perubahan apa kita yang dilakukan pada commit tersebut.

[*Melihat perbedaan di Github*](https://lh6.googleusercontent.com/R8-1HHM9fE3r0WMUU0GYBuFXUo9SadCsdfRnXe_5H2piR_mgM9rQAwBMa8eYfe8Jspx-HsTX-izFWANkqvlvZ7JmJuyp6DeasAWJu17FLYmu9ERoOw8enQK2kFim3ri3QgxiK5IuC4_zHvbF9A)

*Melihat perbedaan di Github*

# **Mengambil Revisi dan Remote Repository**

Saat kita bekerja dengan repository yang memiliki banyak kontributor, kita seharusnya mengambil dulu revisi terbaru dari repository inti agar tidak bentrok. Misalnya begini, pada repository remote ada kontributor lain yang sudah menambahkan dan merubah sesuatu di sana. Maka kita harus mengambil perubahan tersebut, agar repository lokal kita tetap ter-update atau sama persis seperti repository remote.

[*Mengambil revisi*](https://lh3.googleusercontent.com/c0IiqXL1i6i_K2dgxOm6jLGKB9XMo4eAqBzFqDB4PQ9-8QvKfwZfrXiJqJCf-PgGETFraB5ybJ1zAoGOjl---3qmkeAX8QZu1BK_zJzme9CWyIxGKA1xLC2KdJKqVMPG7k7-9hfhpolYCnh6HA)

*Mengambil revisi*

Ada dua perintah untuk mengambil revisi dari repository remote:

```bash
git fetch [nama remote] [nama cabang]
git pull [nama remote] [nama cabang]
```

Perbedaan pada keduanya adalah perintah git fetch hanya akan mengambil revisi (commit) saja dan tidak langsung melakukan penggabungan (merge) terhadap repository lokal. Sedangkan git pull akan mengambil revisi (commit) dan langsung melakukan penggabungan (merge) terhadap repository lokal.

Pemakaian salah satu keduanya tergantung dari situasi dan kondisi. Bila kita sudah membuat perubahan di repository lokal, maka sebaiknya menggunakan git fetch agar perubahan yang kita lakukan tidak hilang. Namun, bila kita tidak pernah melakukan perubahan apapun dan ingin mengambil versi terakhir dari repository remote, maka gunakanlah git pull.

# **Mengambil Revisi dengan Git Fetch**

Sekarang mari kita coba praktekkan. Silahkan buka github, dan tambahkan file README.md melalui Github. Klik tombol add README.

[*Mengambil revisi dengan git fetch*](https://lh4.googleusercontent.com/YrRzC_TYKDKa1wxkSIp1Ol3cCq9EXEVoT9cJFtp0evnOh5SUj9OSA4G5n99FpvUjfR9Lp2Qf-Q0Ghw8s7fHUlAo3TW4hGLt_pdH_ntTRdRdY_wH7cMVNOZ7HJu5KNTWcIUCvUVUQ5BYSVrh_kQ)

*Mengambil revisi dengan git fetch*

Setelah itu, isilah file README.md dengan apapun yang Anda inginkan. Setelah selesai, simpan perubahan dengan melakukan commit langsung dari Github.

[*Membuat file readme*](https://lh3.googleusercontent.com/_jX4E88RlAJe7icLm1oooBoH_RxzjxlKyCPPdi5DcmVFsEZ91wXWnAErfVblUNcWFhvM69yiO2gAdFTPxcA0W0MyFK3l0ZxoP_Gw50S6yCvSjtjCZPC52xfs-zmHHMKOH4YnBjXVuoAmnV-Vyg)

*Membuat file readme*

Pesan commit bersifat opsional, boleh di isi boleh tidak. Karena Github akan membuatkannya secara otomatis. Sekarang ada perubahan baru di repository remote dan kita akan mengambil perubahan tersebut. Mari kita lakukan dengan perintah *git fetch*.

[*Melakukan git fetch*](https://lh5.googleusercontent.com/5nbeU6yfRKflD7ZJK-oW_TjvnlhrEyjrVM7eSHSjvAbjNYhISxCwp5EqLc22YV6PuRUYkdCn_WxwvZGtOJKC6KFJe6z831bnGOpQZVv7ZW-FCSbFTJmAKHxTOKnLvskVqICG00c6tX-j95h99Q)

*Melakukan git fetch*

Revisi sudah diambil, tapi belum ada file README.md di dalam repository lokal. Kenapa bisa begitu? Ya, balik lagi dari pengertian *git fetch*. Dia hanya bertugas mengambil revisi saja dan tidak langsung menggabungkannya dengan repository lokal. Coba kita cek dengan git log.

[*Pengecekan dengan git log*](https://lh5.googleusercontent.com/ks-yD1WakCo7O37zR1CKdVKnclj-wKjbgXsnNavZLOd1pMMmSiPOG6hBM2YUM2mIhu32XV6tR8HCVc2koxAyST7A1vFARSXiLBG96QM5rXRRraJp9gR4qX0i2470NwyXIVmUJa4155UKd_eVHw)

*Pengecekan dengan git log*

Pada gambar di atas terlihat perbedaan log antara repository lokal dengan repository remote. Bila ingin mengecek apa saja perbedaannya, coba gunakan perintah git diff.

```bash
git diff master github/master
```

Keterangan: master adalah cabang master di repository lokal, github/master adalah cabang master di repository remote. Hasil outputnya kira-kira akan seperti ini:

```bash
diff --git a/README.md b/README.md
new file mode 100644
index 0000000..1174eb2
--- /dev/null
+++ b/README.md
@@ -0,0 +1,18 @@
+# belajar-git
+
+Repository ini adalah repository untuk belajar Git.
```

Lalu sekarang bagaimana cara kita menggabungkan commit dari repository remote dengan lokal? Gunakan perintah git merge.

```bash
git merge master github/master
```

Setelah itu coba ketik ls dan git log lagi, maka kita sudah berhasil menggabungkan revisi dari remote dan lokal.

[*Melihat hasil gabungan revisi remote dan lokal*](https://lh3.googleusercontent.com/2ZJWpWwNcG-i8BRktVXt_MI3HVoX0kTTGvrG2J9AirgOL-hu__lGXCpEdt7UxYHDFgLxqr-idgaZefBIJjBtDgq52GvCQpWtEjNYZvTKubeTLiEQUaBc9e-ze2ZdMsHzjzvVHB1YX2FLbeGgMA)

*Melihat hasil gabungan revisi remote dan lokal*

# **Mengambil Revisi dengan Git Pull**

Lakukan hal yang sama seperti tadi. Kali ini kita akan membuat file baru bernama register.html melalui Github.

[*Membuat file baru*](https://lh6.googleusercontent.com/ULnBzwYEkBP_O7gqZS8iIr6Dde28JKkT48pm0zSFdGfncsheFqQ3my2jGtUh7iEtMgr81hVyrkwhqZzxRXU0Ae8R228Eox8VKJlkL7-k25jKZQSkH54RhM3zgJYsUhccs3hj9QZMONa8mgaRfA)

*Membuat file baru*

Berikan nama file dengan register.html dan isi dengan apa saja.

[Mengisi file html](https://lh5.googleusercontent.com/zUlMPZsrf6YqbpGJVTaqIGIqmmqx2rG2k9cygjAbXFVeJhuRdqhLSCRcX7a8g-_f02rN3JVyZPUSDWkw3-ckF9b1jPRr2GU9MHtdcihAa8kOQVn3J2X9POy3TJtUuKWb_WTYF78roFCi1Z2vLQ)

Mengisi file html

Simpan revisi dan tambahkan commit seperti ini.

[*Melakukan commit file baru*](https://lh3.googleusercontent.com/aMO-0hg8Rgb8lOlTjyudk8oRt1to7eLB3pvf9vI1Emtpo-6RgdZ110lMr7ePEXGKsWbBfUrKSNPd0A_tzHH9ZHs2vWixFaBEhbqGml4w2OFVFguKNuTaBgt4cfNYfBsND9RBpFbGZH4io-q5Pg)

*Melakukan commit file baru*

Sekarang ada perubahan baru di repository remote dan kita akan mengambilnya dengan perintah git pull. Silahkan buka repository lokal dan ketik perintah berikut:

```bash
git pull github master
```

Maka semua revisi akan diambil dan langsung digabungkan (merge).

[*Pengecekan hasil git pull*](https://lh3.googleusercontent.com/Z5J1OaHPuVRayUUlcwj0_fWtVYq2AFiKaY8Lm1Ryc5bm8dHHYYHRQloE0usIMv46327EbO0TJStxcvil2g4S5xQxERPMZmyUWYE-x8aOloCMMNeChwOs0lkGHrmkgGTTivA2eLwY5iHk4dVeeA)

*Pengecekan hasil git pull*

# **Clone Remote Repository**

Clone repository bisa kita bilang seperti copy repository dari remote ke lokal. Perintah untuk melakukan clone adalah git clone.

```bash
git clone https://github.com/username/belajar-git.git [nama dir]
```

Keterangan: https://... adalah URL repository remote, kita juga bisa menggunakan SSH. [nama dir] (opsional) adalah nama direktory yang akan dibuat. Jika kita tidak berikan nama direktori, maka akan otomatis menggunakan nama repository. Mari kita coba. Sekarang kita akan pindah ke direktori Desktop.

```bash
cd ~/Desktop
```

Lalu clone remote repo:

```bash
git clone git@github.com:username/belajar-git.git
```

Maka akan ada direktori baru di sana.

FYI: Saat Anda clone sebuah repository dari Github, nama remote origin akan diberikan secara otomatis.

# **Exercise**

1. Buat sebuah akun GitHub.
2. Push repository local ke github
3. Buat clone dari repository yang sudah di push ke GitHub atau GitLab