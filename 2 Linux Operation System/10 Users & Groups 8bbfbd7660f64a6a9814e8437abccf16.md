# 10. Users & Groups

Created: June 27, 2022 1:17 PM

# **Belajar Manajemen User & Group**

## **Apa itu manajemen user & group?**

Kita sudah terbiasa menggunakan konsep 1 user dalam keseharian kita di laptop Windows. Dimana kita cukup login 1 buah user, dan user itulah yang kita pakai. Biasanya user yang kita pakai adalah user yang juga berfungsi sebagai user Administrator. Semuanya kita lakukan dengan menggunakan 1 user ini, apapun kegiatannya.

Jika dianalogikan, yang kita lakukan tersebut seperti ada sebuah rumah yang ditinggali hanya oleh 1 orang. 1 orang ini adalah satu-satunya yang kita perbolehkan untuk masuk ke seluruh ruangan di rumah tersebut termasuk menggunakan segala fasilitasnya seperti mencuci, memasak, tidur dll. Tanpa ada batasan apapun.

![*Ilustrasi Single User*](https://lh5.googleusercontent.com/cJHn9Kd0uBVaY7VXHwM_ie7OoEJNK19-gabG1NYlv0bwwutPHWvSKNswCUy510mf_UbKrKcE776nKwk8EoqQ-03lNGSHkohDwbbxeAbDroCQSQuD-iwWRl1o72c8gHLDKJBLnMT3Yk-PagF-QA)

*Ilustrasi Single User*

Ketika kita berbicara sebuah Server Linux, maka kita sudah berbicara konsep Multi User. Dimana dalam sebuah server itu terdapat banyak user yang memilki tugas dan wewenangnya masing-masing. Ada user yang khusus untuk menjalankan layanan web saja, ada user yang khusus untuk menjalankan layanan database, ada kelompok user yang berhak mengakses file-file departemen keuangan saja, hingga ada user yang khusus berfungsi sebagai Administrator. Kenapa perlu seperti ini? Karena inilah salah satu letak keamanan Linux. Dimana kita bisa mengatur hak akses segala macam layanan, folder, file, hingga command-command yang bisa dieksekusi berdasarkan user atau grup tertentu saja.

Ibarat analogi rumah tadi, jika konsep Multi User maka di rumah tersebut misalnya terdapat 4 orang bernama A,B,C,D. Si A hanya boleh masuk ke dapur untuk melakukan segala kegiatan di dapur tersebut, ke ruangan lain sama sekali tidak boleh masuk. Si B misalnya boleh masuk ke dapur, tapi hanya boleh memasak saja. Memblender, mencuci piring, dll tidak boleh. Lalu si C hanya boleh mengakses kamar mandi saja, tidak boleh ke ruangan lain. Sedangkan si D ini boleh mengakses seluruh ruangan dan menggunakan segala fasilitasnya. Semua sudah diatur sesuai wewenang dan hak aksesnya masing-masing agar lebih aman.

![*Ilustrasi Multi User*](https://lh3.googleusercontent.com/xmyH_yo9hpVpwN_vg6kS2AsOtW9yk7LvplpStZJP_73gTiGy1OtjgjSQ7379gitTRfkvIXbWnamI4hCHh5F6iMygSYINqskwXiY0yMUqpAbuUTPYD0EC-n8KUOf74IhfUbB_A-7n4M6qdF54vg)

*Ilustrasi Multi User*

Oleh karena itu disini kita akan mempelajari terlebih dahulu bagaimana cara melakukan manajemen user dan grup seperti membuat user, menghapus user, memasukkan user ke dalam sebuah grup, mengeluarkannya, dst. Untuk kemudian user dan grup yang sudah kita atur ini bisa kita konfigurasi lagi hak akses dan wewenangnya.

Dalam konsep Multiuser, manajemen user dan group sangat vital peranannya. Hal ini harus dikuasai dengan baik untuk menerapkan kebijakan-kebijakan seputar ownership permission di lingkungan GNU/Linux. Terkait ownership dan permission sendiri akan kita bahas lebih dalam di materi berikutnya.

# **Perintah-perintah manajemen User**

## ***Membuat User Baru***

Perintah untuk menambahkan user baru bernama limbad.

```bash
adduser limbad
```

## ***Memberi/mengganti password user***

Perintah untuk memberi password baru maupun mengganti password dari sebuah user.

```bash
passwd namauser
```

## ***Mengganti nama user***

Perintah untuk mengganti nama user ke nama yang baru.

```bash
usermod -l namabaru namauserlama
```

## ***Menghapus User***

Berikut adalah perintah untuk menghapus user beserta home direktorinya (seluruh data-datanya). Hilangkan opsi -r jika hanya ingin menghapus usernya saja tanpa menghapus data.

```bash
userdel -r limbad
```

## ***Disable/lock user***

Kita juga bisa hanya mengunci user dari pemakaian dibanding harus menghapusnya. Perintahnya adalah sebagai berikut untuk mendisable user root dan user cilsy :

```bash
passwd -l root
passwd -l cilsy
```

## ***Unlock user***

Jika suatu saat sudah ingin digunakan kembali, maka kita tinggal meng-enable kembali user yang sebelumnya kita kunci.

```bash
passwd -u cilsy
```

## ***Perintah-perintah manajemen user lainnya***

```bash
su	#berganti user
id	#mengecek user ID
w	#mengetahui siapa user yang sedang login
whoami	#siapa saya?
last	#melihat daftar login terakhir
```

# **Perintah-perintah manajemen Group**

## ***Membuat Group Baru***

Membuat group baru bernama staff

```bash
groupadd staff
```

## ***Merubah nama Group***

Perintah untuk merubah nama grup dari staff menjadi office.

```bash
groupmod -n office staff
```

## ***Menghapus Group***

Menghapus group office yang sudah kita buat sebelumnya :

```bash
groupdel office
```

## ***Menampilkan group suatu user***

Kita dapat mencari tahu suatu user itu tergabung kedalam grup apa saja dengan perintah berikut :

```bash
groups rizal
```

## ***Menambahkan user ke suatu grup***

User limbad yang telah dibuat sebelumnya akan dimasukkan ke dalam grup root. Perintahnya :

```bash
usermod -a -G root limbad
```

## ***Mengeluarkan user dari suatu grup***

User limbad yang telah dimasukkan ke grup root akan dikeluarkan lagi. Perintahnya adalah sebagai berikut :

```bash
gpasswd -d limbad root
```

# **Exercise**

**Praktek**

Waktu pengerjaan : 5 menit

Masing-masing peserta praktekkan soal berikut ini di kolom terminal Linux masing-masing sambil melakukan sharing screen agar instruktur dapat melihat hasilnya.

1. Buatlah user dan grup dengan skema sebagai berikut dan tunjukkan hasilnya :

|Grup|Anggota         |
|----|----------------|
|keuangan|cilsy, devops, jono|
|penjualan|tono, devops, jono|
|hrd |siska, ramon, jono|

**Teori**

1. Kenapa kita perlu mempelajari Manajemen User & Grup?
2. Pada kasus praktek diatas, apa efek ketika 1 user menjadi anggota 2 grup atau lebih (jono)?