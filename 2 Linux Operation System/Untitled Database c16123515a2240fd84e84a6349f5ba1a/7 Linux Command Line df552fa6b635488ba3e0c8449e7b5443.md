# 7. Linux Command Line

Created: June 23, 2022 8:51 PM

# **Apa itu Command Line?**

Sebuah server dituntut agar beban kerjanya dapat se-ringan dan se-aman mungkin. Oleh karena itu biasanya hampir semua Server pasti tidak memiliki tampilan grafis untuk meringankan beban RAM dan CPU. Semua hal yang ingin dilakukan di server akan digantikan menggunakan perintah-perintah yang diketik, atau biasa disebut sebagai command line.

Aktivitas sesimpel membuat folder yang tinggal klik saja di komputer Windows, di Linux (dalam konteks server) harus dilakukan dengan mengetikkan sebuah command.

Seorang DevOps yang akan selalu mengelola server Linux wajib terbiasa dengan command line. Untuk konfigurasi dan setup server yang akan dikelola, maupun untuk membuat berbagai macam scripting untuk otomasi nantinya.

## **Remote Linux**

Pada bagian ini kita akan banyak menggunakan GNU/Linux, maka sebaiknya kalian menggunakan sistem operasi linux yang sudah terinstall di komputer.

Cara menggunakan linux yang sudah disediakan adalah dengan me-remote linux tersebut agar dapat langsung kita gunakan, untuk melakukan remote server pada linux tersebut kalian harus download terlebih dahulu aplikasi putty di link berikut.

[https://www.putty.org/](https://www.putty.org/)

Install aplikasi tersebut sampai selesai, setelah itu buka aplikasi Putty untuk melakukan akses ke ubuntu tersebut, setelah itu isikan username dan ip public dari ubuntu yang akan kita remote. Username dan IP Public sudah diberikan sebelumnya melalui chat slack

[https://lh6.googleusercontent.com/3DWz1t_9JjCbO1wv5cDx5eDDDLsP7cSzbv9Mg1IUnGQJwa0mAb_S5h5BrkRoKJ0KnwY-e9Q1WkWIgyht9OL8dPo02bA4Ok-G0d9JKoPEUHG_lL3pTOb76aejhCFdhMq7oXI5H1QmbeWZUd1XVA](https://lh6.googleusercontent.com/3DWz1t_9JjCbO1wv5cDx5eDDDLsP7cSzbv9Mg1IUnGQJwa0mAb_S5h5BrkRoKJ0KnwY-e9Q1WkWIgyht9OL8dPo02bA4Ok-G0d9JKoPEUHG_lL3pTOb76aejhCFdhMq7oXI5H1QmbeWZUd1XVA)

Sebelum klik open, pilih terlebih dahulu menu Auth yang ada di categori menu connection > SSH > Auth. Klik tombol browse dan cari file keypair.ppk yang sudah diberikan sebelumnya.

[https://lh5.googleusercontent.com/9XXUr87Dy3mRAoGba4LnaLBxY4BX19rdLnoEuSDw3P2Pj-2p1n2rxfj5C5n1Bdp_k24dDNJIIXiNf0h9m7jp7eqUT_7uwUvUj4JdYurRpn6juXKCxADKkpQi9OyWjPTGmCBqIizBFV28eW0hAw](https://lh5.googleusercontent.com/9XXUr87Dy3mRAoGba4LnaLBxY4BX19rdLnoEuSDw3P2Pj-2p1n2rxfj5C5n1Bdp_k24dDNJIIXiNf0h9m7jp7eqUT_7uwUvUj4JdYurRpn6juXKCxADKkpQi9OyWjPTGmCBqIizBFV28eW0hAw)

Klik open lalu kita akan diarahkan ke pop out security alert, pilih yes untuk melanjutkan.

[https://lh5.googleusercontent.com/IlnSgQoS6YVtgL-PkeP_0TaYlWNA9fQTv4reQC6SPNuSmJBSXRAIX5-Vaq27IKSfTlO15VMkjEfwKkCvJPfU3xwwZctp9ZnDUObFLz_O4yUWSPXuhT8CfoGmcbXekchwJt8lI4W81L1CU_VAeA](https://lh5.googleusercontent.com/IlnSgQoS6YVtgL-PkeP_0TaYlWNA9fQTv4reQC6SPNuSmJBSXRAIX5-Vaq27IKSfTlO15VMkjEfwKkCvJPfU3xwwZctp9ZnDUObFLz_O4yUWSPXuhT8CfoGmcbXekchwJt8lI4W81L1CU_VAeA)

Dengan begitu kita sudah selesai remote login ke ubuntu yang akan kita gunakan, dan hasilnya adalah sebagai berikut ini.

[https://lh3.googleusercontent.com/vTNBEjmQJMb2fs5NBWJVVUus4P34G2zod1Lcw8xl873Ym1Y3UKEd0ddo-WllOk8k9xMFBUm3QTXxrrSwyeOTCRkjO_OzwVTlE4HaSwor00z8fM_zapZzF5f3k9xsrQJh9Hzn0Q6O_t-PZAdAzg](https://lh3.googleusercontent.com/vTNBEjmQJMb2fs5NBWJVVUus4P34G2zod1Lcw8xl873Ym1Y3UKEd0ddo-WllOk8k9xMFBUm3QTXxrrSwyeOTCRkjO_OzwVTlE4HaSwor00z8fM_zapZzF5f3k9xsrQJh9Hzn0Q6O_t-PZAdAzg)

## **Belajar Login Logout**

Saat kita berhasil masuk ke sistem Linux, maka pertama kali yang kita lihat adalah layar hitam dengan tulisan :

```bash
cilsy login:
Password:
```

Itu adalah tampilan prompt login default dari Linux. Kita tidak akan bisa melakukan apapun di Linux sebelum kita berhasil login. Sehingga yang pertama harus dilakukan adalah login sesuai user masing-masing yang sudah didapatkan saat instalasi maupun saat kita membuat server di AWS. Misalnya disini user yang digunakan adalah rizal :

```bash
cilsy login: rizal
Password:
rizal@cilsy:~$
```

Perhatikan tanda **$**, tanda tersebut mewakili jenis user yang digunakan login, yaitu user biasa. Bukan user root (administrator).

Sekarang coba ketikkan perintah berikut :

```bash
rizal@cilsy:~$ sudo -i
root@cilsy :~#
```

Sudo -i adalah perintah untuk masuk ke mode root atau mode administrator. Setelah masuk mode root, tanda **$** berubah menjadi **#**. Landing direktori kedua user diatas juga berbeda berdasarkan home direktorinya masing-masing.

`User biasa berada di : /home/rizal`

`User root berada di : /root`

Perintah sudo sendiri membuat kitaa dapat bebas melakukan apapun di sistem kita. Hampir semua konfigurasi dan command-command yang terkait administrasi server mewajibkan kita untuk masuk mode root terlebih dahulu menggunakan perintah sudo.

Lalu bagaimana jika kita ingin keluar dari sistem Linux kita? Gunakan perintah logout atau exit. Bisa juga dengan menekan kombinasi tombol ctrll+d.

```bash
rizal@cilsy:~$ logout
rizal@cilsy:~$ exit
```

# **Perintah Navigasi**

Perintah navigasi digunakan untuk menjelajahi direktori-direktori yang ada di Linux. Sama seperti ketika kita melakukan pindah-pindah folder dengan mengklik-klik di komputer Windows.

Berikut merupakan beberapa perintah navigasi pada GNU/Linux.

**pwd** 	: print working directory, untuk melihat alamat direktori kita berada saat ini

**cd** 	: change direktory, untuk berpindah folder

**ls** 	: list, melihat daftar isi direktori saat ini

Contoh dari penggunaan perintah navigasi bisa dilakukan dengan cara berikut.

**pwd** 	: untuk melihat posisi kita berada sekarang

- **pwd**

**cd** 	: untuk berpindah direktori

- **cd /home/devops** (jika /home/devops berada diluar direktori sekarang)
- **cd home/devops** (jika home berada didalam direktori sekarang)
- **cd ..** (kembali satu tingkat ke direktori sebelumnya)
- **cd –** (kembali ke direktori yang dimasuki sebelumnya)
- **cd** (kembali ke home direktori)

**ls**	: untuk melihat isi folder

- **ls** (jika ingin melihat isi direktori tempat berada sekarang)
- **ls /home/devops** (Melihat isi dari direktori devops)

# **Perintah pengelolaan Direktori & File**

Perintah ini digunakan untuk aktifitas dasar dalam pengelolaan file dan folder di Linux. Yaitu untuk membuat file, membuat folder, mengkopi, cut-paste, menghapus, hingga merubah nama.

Berikut merupakan beberapa perintah pengelolaan direktori pada GNU/Linux.

**cp**		: copy, intuk menyalin berkas atau folder (seperti copy paste)

**mv** 		: move, untuk memindahkan atau mengganti nama (seperti cut-paste)

**rm** 		: remove, untuk menghapus file atau folder

**mkdir**		: make directory, untuk membuat folder

**touch**		: untuk membuat file

Contoh dari penggunaan perintah Direktori bisa dilakukan dengan cara berikut.

**mkdir** : make directory, membuat folder

- **mkdir folderbaru** (folder yang dibuat ingin didalam direktori sekarang)
- **mkdir /tmp/folderbaru** (folder yang dibuat ingin diluar direktori sekarang)

**touch** : membuat file

- **touch filebaru** (file yang dibuat ingin didalam direktori sekarang)
- **touch /tmp/filebaru** (file yang dibuat ingin diluar direktori sekarang)

**cp**	: copy, menyalin berkas atau folder

- **cp test1.txt test2.txt** (menyalin file dalam direktori ke dalam direktori)
- **cp test1.txt /tmp/test2.txt** (menyalin file dalam direktori ke luar direktori)
- **cp /tmp/test2.txt test3.txt** (menyalin file luar direktori ke dalam direktori)
- **cp /tmp/test2.txt /tmp/test3.txt** (menyalin file luar ke luar direktori)
- **cp -R /tmp/namafolder /home/namafolder** (untuk menyalin direktori yang ada isinya)

**mv**	: move, memindahkan atau mengganti nama (seperti cut-paste)

- **mv test1.txt test2.txt	(mengganti nama test1 menjadi test2)**
- **mv /tmp/test2.txt /home/rizal/test3.txt (memindahkan file test2 lalu merubah namanya menjadi test3)**

**rm**	: remove, menghapus berkas atau folder

- **rm namabenar.txt (menghapus file namabenar.txt)**
- **rm -R namafolder (untuk menghapus direktori)**

# **Perintah Editing File**

Perintah ini sama seperti kegiatan kita dalam mengedit dan membuat file teks di Windows menggunakan notepad. Perintah ini akan sangat sering kita gunakan, karena hampir seluruh file konfigurasi di Linux nantinya akan kita edit-edit, kita baca, kita modifikasi dengan perintah ini.

Berikut merupakan beberapa perintah file editing pada GNU/Linux.

**nano**	: GNU nano, text editor berbasis konsol yang mudah dioperasikan

**vim** 	: vim, text editor berbasis konsol yang mudah dioperasikan

Contoh penggunaannya :

**nano/vim** = text editor berbasis konsol yang mudah dioperasikan

- **vim /home/rizal/test1.txt (mengedit file diluar direktori)**
- **nano rizal/test1.txt (mengedit file di direktori kita berada sekarang)**
- **nano test1.txt (mengedit file didalam direktori kita berada)**

Kita perlu mengingat beberapa kombinasi dasar saat pengoperasian text editor ini. Yaitu pada nano ada kombinasi Ctrl+X untuk menutup program (exit) dan Ctrl+O untuk menyimpan (save). Sedangkan untuk vim, sebelum menulis kita perlu mengetik karakter i (insert) lalu untuk menyimpan kita gunakan kombinasi Esc+:wq (write and quit). Adapun sudo diperlukan setiap pengguna menyunting berkas pada area sistem seperti pada /etc.

# **Perintah Bantuan Manual Guide**

Pada dasarnya, di Linux kita sama sekali tidak perlu menghafal seluruh perintah yang ada. Ketika kita membutuhkan informasi detail terhadap suatu command, opsi-opsi yang digunakan apa saja, kita dapat memanfaatkan manual guide yang sudah disediakan pada setiap perintah.

Berikut merupakan beberapa perintah untuk membaca bantuan manual guide pada GNU/Linux :

**man**			: manual, perintah untuk membuka manual guide lengkap dari suatu command

- **-help**	: opsi untuk melihat manual singkat dari suatu command

Contoh penggunaan :

- **cp --help	(melihat manual guide singkat dari perintah cp)**
- **man cp	(melihat manual guide lengkap dari perintah cp)**
- **nano --help (melihat manual guide singkat dari perintah nano)**
- **man nano (melihat manual guide lengkap dari perintah nano)**

Informasi yang disediakan oleh manual guide tersebut biasanya sudah sangat mewakili dan sangat bisa dipraktekkan. Namun jika masih mengalami kesulitan, jangan lupakan bahwa kita selalu bisa mencarinya di google. Cukup mengetikkan “cp command practice” atau “nano command linux practice” biasanya akan muncul banyak artikel yang membahasnya.

# **Exercise**

**Teori**

1. Kenapa kita perlu mempelajari perintah dasar command line?

**Praktek**

Waktu pengerjaan : 15 menit

Masing-masing peserta praktekkan soal berikut ini di kolom terminal Linux masing-masing sambil melakukan sharing screen agar instruktur dapat melihat hasilnya.

1. Pertama-tama login sebagai user masing-masing.
2. Pindahlah ke direktori /tmp.
3. Buatlah 1 buah file bernama test1.txt yang berisi “Sekolah DevOps Cilsy” didalam folder anda berada sekarang.
4. Buatlah 1 folder bernama latihan didalam folder Anda berada sekarang.
5. Kopikan file test1.txt tersebut ke dalam folder latihan yang barusan anda buat dengan nama test2.txt.
6. Masih dalam posisi Anda sekarang berada (jangan pindah folder), lakukan cut-paste file test2.txt yang ada didalam folder latihan ke folder /home/ dengan nama baru test3.txt.
7. Sekarang pindahlah ke home direktori anda lagi.
8. Hapuslah file test1.txt yang ada di /tmp tanpa anda pindah folder ke /tmp terlebih dahulu.
9. Hapuslah folder latihan yang ada di /tmp tanpa anda pindah folder ke /tmp terlebih dahulu.
10. Kumpulkan hasilnya ke instruktur.