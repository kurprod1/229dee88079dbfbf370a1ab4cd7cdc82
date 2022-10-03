# 8. Text & File Manipulation

Created: June 24, 2022 8:21 AM

# **Apa itu manipulasi teks & file?**

Kunci utama skill DevOps yang lain adalah ilmu scripting. Yaitu ilmu untuk merangkai berbagai macam command-command di Linux untuk mencapai tujuan tertentu.

Ilmu scripting ini sangat mirip dengan programming, karena menggunakan alur dan pola berpikir yang sama. Namun bedanya scripting ini versinya jauh lebih kecil dibandingkan dengan programming. Pada bab berikutnya akan kita bahas lebih dalam terkait scripting ini.

Salah satu ilmu yang akan sangat menunjang skill scripting adalah ilmu manipulasi teks dan file. Dimana kita dapat memodifikasi dan memanipulasi isi dari suatu file yang acak, untuk di ekstrak informasi pentingnya saja untuk mencapai tujuan tertentu.

Misalnya kita adalah DevOps engineer di sebuah perusahaan. Kemudian bos kita ingin mengetahui berapa kali Web Server perusahaan tersebut down selama ini.

Nah untuk mencapai tujuan tersebut, kita bisa coba menggunakan salah satu informasi dari sebuah file log yang mencatat aktifitas web server perusahaan. Kira-kira isinya seperti ini :

```bash
[2018-06-05] Website has been accessed from IP 18.39.9.9
[2018-07-05] Website has been down
[2018-09-12] User has been blacklisted from accessing website with IP 9.29.29.100
[2018-03-30] Service restarted
[2018-11-18] Website has been down
[2018-12-17] Website has been down
```

Dari isi file tersebut idenya adalah bagaimana caranya kita menghitung berapa kali tulisan “Website has been down” muncul lalu kita tampilkan berupa angka misalnya : 5. Bagaimana caranya?

Misalnya pertama-tama kita eliminasi dulu semua baris yang tidak mengandung kata-kata Website has been down. Sehingga isi file yang baru menjadi seperti ini :

```bash
[2018-07-05] Website has been down
[2018-12-17] Website has been down
[2018-11-18] Website has been down
```

Kemudian berikutnya kita hilangkan seluruh bagian tanggalnya :

```bash
Website has been down
Website has been down
Website has been down
```

Kemudian kita hitung berapa kali line Website has been down muncul. Sehingga pada akhirnya isi file hanya menjadi seperti ini :

```bash
3
```

Semua step by step diatas menggunakan teknik manipulasi file dan teks yang akan kita pelajari di bab ini. Kita akan coba bahas lebih dalam terkait teknik-teknik manipulasi teks dan file yang sering digunakan.

# **Belajar redirection & Pipeline**

## ***Apa itu Redirection & Pipeline?***

Redirection dan Pipeline merupakan salah satu teknik yang dapat memperkaya kombinasi saat melakukan manipulasi teks/file. Dimana Redirection adalah teknik menghubungkan sebuah perintah command line dengan file, sedangkan pipeline adalah teknik untuk menghubungkan perintah command line dengan perintah command line lainnya.

Format dasar redirection dan piping :

```bash
command > file (format redirection)
command1 | command2 (format pipeline)
```

## ***Contoh Penggunaan Redirection***

Misalnya kita ingin memasukkan seluruh isi dari file test.txt ke dalam file baru bernama testcopy.txt.

```bash
cat test.txt > testcopy.txt
```

Cobalah lihat hasil dari file testcopy.txt, maka isinya akan sama persis dengan isi dari file test.txt.

Atau misalnya kita ingin melihat apa saja isi folder dari /, lalu kita masukkan hasilnya ke dalam file bernama direktory.txt.

```bash
ls / > direktory.txt
```

Coba lihat isi dari file direktory.txt, maka akan menampilkan keseluruhan isi folder /.

nb : Karena redirection sifatnya benar-benar menghapus seluruh isi file dengan yang baru, maka harus digunakan dengan sangat hati-hati. Salah-salah, isi file yang sangat penting bisa terhapus karena tidak sengaja kita redirection dengan isi command lain.

## ***Contoh Pipeline***

Misalnya kita ingin melihat isi folder /home/rizal lalu mencari file bernama devops.png. Jika kita menggunakan perintah ls saja, maka hasilnya akan sangat semerawut seperti ini :

```bash
rizal@rizal-Inspiron-5468 ~ $ ls /home/rizal/ | grep png

aws training scheme for company white.png
aws training scheme for trainer.png
bandwidthkesedot1.png
bandwidthkesedot2.png
devops 1.png
devops 2.png
devops 3.png
hamster2.png
header-bg.png
jalankosong.png
okr1.png
pisahjalu1.png
pisahjalu2.png
profile1.png
profile2.png
proxmox 1.png
proxmox 2.png

```

Nah jika kita hubungkan perintah ls tersebut dengan perintah untuk memfilter kata kunci tertentu seperti grep, maka hasilnya menjadi seperti ini :

```bash
rizal@rizal-Inspiron-5468 ~ $ ls /home/rizal/ | grep devops
devops 1.png
devops 1.svg
devops 2.png
devops 2.svg
devops 3.png
devops 3.svg

```

Hasil diatas sudah lumayan betul, tetapi masih ada yang kurang tepat. Masih ada file dengan tipe svg disana. Oleh karena itu kita bisa lakukan piping yang lebih panjang seperti ini :

```bash
rizal@rizal-Inspiron-5468 ~ $ ls /home/rizal/ | grep devops | grep png
devops 1.png
devops 2.png
devops 3.png

```

# **Belajar grep**

## ***Apa itu Grep?***

Sebelumnya kita sudah sempat coba contoh penggunaan command grep pada saat belajar redirection dan piping. Disini kita akan bahas lebih banyak lagi contohnya. Grep ini pada intinya adalah command untuk memfilter teks/file sesuai kata kunci tertentu. Berikut adalah beberapa contoh-contoh penggunaannya.

1. ***Menampilkan Beberapa baris setelah atau sebelum pola yang dicari***

Misal berikut ada perintah untuk menampilkan informasi jaringan pada server kita :

```bash
enp3s0    Link encap:Ethernet  HWaddr a4:4c:c8:47:75:42
					UP BROADCAST MULTICAST  MTU:1500  Metric:1
					RX packets:0 errors:0 dropped:0 overruns:0 frame:0
					TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
					collisions:0 txqueuelen:1000
					RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
lo        Link encap:Local Loopback
					inet addr:127.0.0.1  Mask:255.0.0.0
					inet6 addr: ::1/128 Scope:Host
					UP LOOPBACK RUNNING  MTU:65536  Metric:1
					RX packets:1319 errors:0 dropped:0 overruns:0 frame:0
					TX packets:1319 errors:0 dropped:0 overruns:0 carrier:0
					collisions:0 txqueuelen:1000
					RX bytes:141519 (141.5 KB)  TX bytes:141519 (141.5 KB)

```

Nah kita ingin hanya menampilkan 4 baris setelah kata kunci lo maupun 4 baris sebelum kata kunci lo. Kita bisa gunakan opsi -A untuk 4 baris setelah, dan opsi -B untuk 4 baris sebelum.

```bash
rizal@rizal-Inspiron-5468 ~ $ ifconfig | grep -A 4 lo
lo        Link encap:Local Loopback
inet addr:127.0.0.1  Mask:255.0.0.0
inet6 addr: ::1/128 Scope:Host
UP LOOPBACK RUNNING  MTU:65536  Metric:1
RX packets:1325 errors:0 dropped:0 overruns:0 frame:0
rizal@rizal-Inspiron-5468 ~ $ ifconfig | grep -B 4 lo
TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
lo        Link encap:Local Loopback

```

1. ***Menampilkan teks dengan pola kata kunci tertentu***

Misalnya kita tidak tahu opsi apa saja yang bisa digunakan pada command grep. Sedangkan kita ingin menggunakan grep untuk memfilter kata kunci yang hanya match secara keseluruhan kata saja. Jika kita menggunakan fasilitas bantuan dari grep seperti ini, hasilnya terlalu banyak dan kita bingung mana yang harus digunakan :

```bash
rizal@rizal-Inspiron-5468 ~ $ grep --help
Usage: grep [OPTION]... PATTERN [FILE]...
Search for PATTERN in each FILE or standard input.
PATTERN is, by default, a basic regular expression (BRE).
Example: grep -i 'hello world' menu.h main.c
Regexp selection and interpretation:
-E, --extended-regexp     PATTERN is an extended regular expression (ERE)
-F, --fixed-strings       PATTERN is a set of newline-separated strings
-G, --basic-regexp        PATTERN is a basic regular expression (BRE)
-P, --perl-regexp         PATTERN is a Perl regular expression
-e, --regexp=PATTERN      use PATTERN for matching
-f, --file=FILE           obtain PATTERN from FILE
-i, --ignore-case         ignore case distinctions
-w, --word-regexp         force PATTERN to match only whole words

```

Nah kita bisa filter ini dengan grep misalnya kita cari yang hanya berkaitan dengan kata kunci “words” seperti ini :

```bash
rizal@rizal-Inspiron-5468 ~ $ grep --help | grep words
-w, --word-regexp         force PATTERN to match only whole words
```

Dari situ terfilter outputnya sesuai yang kita inginkan saja. Sehingga kita tahu bahwa dengan menggunakan opsi -w maka grep bisa melakukan matching secara keseluruhan kata.

1. ***Membalik Hasil yang muncul untuk memfilter***

Biasanya setiap file konfigurasi di Linux mengandung banyak komentar berawalan tanda pagar “#”. Contohnya seperti ini :

```bash
rizal@rizal-Inspiron-5468 ~ $ sudo cat /etc/hosts
# Localhost line
127.0.0.1	localhost
127.0.1.1	rizal-Inspiron-5468
# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

Nah bagaimana kalau kita ingin hanya menampilkan baris yang tidak ada tanda pagarnya saja? Maka kita bisa gunakan opsi -v. Opsi ini membuat yang ditampilkan justru yang tidak cocok dengan apa yang kita cari.

```bash
rizal@rizal-Inspiron-5468 ~ $ sudo grep -v "#" /etc/hosts
127.0.0.1	localhost
127.0.1.1	rizal-Inspiron-5468
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

## **Exercise**

**Teori**

1. Kenapa kita perlu mempelajari manipulasi teks dan file?

**Praktek**

Waktu pengerjaan : 10 menit

Masing-masing peserta praktekkan soal berikut ini di kolom terminal Linux masing-masing sambil melakukan sharing screen agar instruktur dapat melihat hasilnya.

1. Pertama-tama buatlah sebuah file bernama latihan1.txt yang berisi :
    
    ```bash
    cilsy.mp3
    cilsy.mp4
    devops cilsy.png
    devops.mp3
    sekolah devops cilsy.mp3
    #cilsy yahud.mp3
    cilsy keren.mp3
    #keren kok cilsy.mp3
    sekolah devops.cilsy.flv
    ```
    
2. Anda diminta untuk menyaring isi file tersebut dengan ketentuan sebagai berikut :
    - Hanya tampilkan baris yang mengandung kata “cilsy” dan berekstensi “.mp3” saja.
    - Tidak boleh ada baris yang mengandung “#” walaupun baris tersebut sudah betul mengandung kata “cilsy” dan berekstensi “.mp3”.
    - Hasil saringan file dimasukkan ke file baru bernama hasil1.txt.
    - Anda hanya boleh menggunakan teknik pipeline, grep, dan redirection untuk mencapai hal tersebut.

# **Belajar Regular Expression**

## ***Apa itu Regular Expression?***

Pada materi ini kita akan belajar untuk lebih memperkaya lagi kombinasi yang bisa kita lakukan dalam melakukan seleksi, manipulasi, dan modifikasi file dengan Regular Expression.

Regular Expression ini adalah simbol yang merepresentasikan pola karakter. Gunanya adalah untuk lebih mempermudah kita dalam melakukan filtering output dari sebuah command, teks, maupun file.

Regular Expression terdiri dari :

- ( . ) → untuk menandai minimal ada 1 karakter apapun,
- ( * ) → untuk menandai minimal ada 0 atau lebih karakter.
- ( + ) → untuk menandai minimal ada 1 atau lebih karakter .
- ( ? ) → untuk menandai minimal ada 0 atau 1 karakter.
- [ character ] → untuk mencocokkan karakter yang ditentukan didalam tanda [ ], bisa juga menggunakan tanda hubung seperti [–] untuk menandai range dari karakter : [a-z], [1-9]
- ^ → untuk mencocokkan awal dari sebuah baris pada file.
- $ → untuk mencocokkan akhir dari sebuah baris pada file.
- \ → karakter escape untuk menghindari sebuah karakter biasa dianggap menjadi karakter meta.
- | → sebagai fungsi OR (atau).

Kita akan coba bahas konsep dari Regular Expression ini dengan menggunakan sebuah file bernama filetest.txt dengan isi seperti ini :

```bash
rizal@rizal-Inspiron-5468 ~ $ cat filetest.txt
rizal
Rizal
RIZAL
manrah
rahman
rahmaN
1rizal
2rizal
3rizal
4rizal
5rizal
6Rizal
```

Isi file tersebut akan kita coba ubah dan manipulasi menggunakan pola-pola regular expression.

### ***Penggunaan ( . )***

Contoh jika kita mengetikkan command berikut :

```bash
grep -E ‘.r’
```

Artinya “Cari baris yang memiliki 1 karakter apapun sebelum huruf r”. Maka akan muncul seperti ini :

```bash
rizal@rizal-Inspiron-5468 ~ $ grep -E '.r' filetest.txt
manrah
1rizal
2rizal
3rizal
4rizal
5rizal
```

Baris manrah masuk kriteria, karena sebelum huruf r ada 1 huruf, yaitu n. Begitupun dengan baris 1rizal, 2rizal, 3rizal, dst, karena sebelum huruf r ada angka 1,2,3,dll. Sedangkan untuk baris rizal saja, itu tidak termasuk karena sebelum huruf r tidak ada 1 huruf apapun.

Contoh lain penggunaan ( . ) misalnya :

```bash
grep -E ‘1.i’
```

Artinya “Cari baris yang memiliki minimal 1 karakter apapun diantara angkat 1 dan huruf i”. Maka hasilnya sebagai berikut :

```bash
rizal@rizal-Inspiron-5468 ~ $ grep -E '1.i' filetest.txt
1rizal
```

Yang memenuhi syarat hanyalah baris 1rizal. Karena memiliki 1 karakter r diantara angka 1 dan huruf i.

### ***Penggunaan ( * )***

Contoh jika kita mengetikkan perintah ini :

```bash
grep -E 'riz*' filetest.txt
```

Maka artinya “Cari baris yang memiliki “riz” lalu boleh diikuti dengan karakter apapun dan dengan jumlah berapapun (termasuk 0)”. Maka hasilnya :

```bash
rizal@rizal-Inspiron-5468 ~ $ grep -E 'riz*' filetest.txt
rizal
1rizal
2rizal
3rizal
4rizal
5rizal
```

Semua baris tersebut kebetulan memiliki karakter yang sama, yaitu setelah riz terdapat karakter al. Namun sebenarnya jika terdapat karakter seperti rizaaaaaaaal maupun riz saja, itu tetap akan masuk kriteria, karena tetap memenuhi syarat bahwa setelah kata riz minimal ada 0 karakter atau lebih.

### ***Penggunaan +***

Untuk mencari baris yang memiliki minimal 1 huruf r sebelum huruf z.

```bash
rizal@rizal-Inspiron-5468 ~ $ grep -E 'r+z' filetest.txt
```

Tidak ada hasil yang muncul, karena tidak ada satu baris pun yang memiliki 1 huruf r sebelum huruf z. Misalnya ada baris seperti 1rzl atau rzal atau rzaaaaal, itu baru akan muncul.

### ***Penggunaan (?)***

Untuk mencari baris yang memiliki minimal 0 (tidak ada) maupun 1 huruf r sebelum huruf z.

```bash
rizal@rizal-Inspiron-5468 ~ $ grep -E 'r?z' filetest.txt
rizal
Rizal
1rizal
2rizal
3rizal
4rizal
5rizal
6Rizal
```

Walaupun tidak ada satupun baris yang memiliki huruf r sebelum huruf z, tapi semua baris diatas tetap muncul karena masih dianggap memenuhi syarat. Yaitu boleh tidak muncul karakter r sama sekali sebelum huruf z.

### ***Penggunaan ^ dan |***

Untuk mencari baris yang berawalan r ATAU berawalan 1.

```bash
rizal@rizal-Inspiron-5468 ~ $ grep -E '^r|^1' filetest.txt
rizal
rahman
rahmaN
1rizal
```

Baris yang tidak berawalan r atau 1 tidak akan muncul seperti baris 2rizal, 3rizal, maupun manrah.

### ***Penggunaan $ dan [ karakter ]***

Untuk mencari baris yang berakhiran l maupun berakhiran n atau N.

```bash
rizal@rizal-Inspiron-5468 ~ $ grep -E 'l$|[nN]$' filetest.txt
rizal
Rizal
rahman
rahmaN
1rizal
2rizal
3rizal
4rizal
5rizal
6Rizal
```

Untuk mencari baris yang berawalan angka 1-9

```bash
rizal@rizal-Inspiron-5468 ~ $ grep -E '^[1-9]' filetest.txt
1rizal
2rizal
3rizal
4rizal
5rizal
6Rizal
```

Untuk mencari baris yang berawalan 1-9 DAN memiliki 1 huruf R kapital.

```bash
rizal@rizal-Inspiron-5468 ~ $ grep -E '^[1-9]' filetest.txt | grep -E 'R'
6Rizal
```

# **Exercise**

**Teori**

1. Kenapa kita perlu mempelajari manipulasi teks dan file?

**Praktek**

Waktu pengerjaan : 15 menit

Masing-masing peserta praktekkan soal berikut ini di kolom terminal Linux masing-masing sambil melakukan sharing screen agar instruktur dapat melihat hasilnya.

1. Pertama-tama buatlah sebuah file bernama latihan2.txt yang berisi :
    
    ```
    1cilsy@
    aDVOPScilsy
    Acilsy
    bcilsy#
    Bcilsy
    99cilsy
    100cilsy
    08cilsy
    76cilsy
    zZcilsy
    %cilsy
    @cilsy
    #
    ##cilsy
    #devopscilsy
    #sekolahcilsy
    .cilsy
    .cilsy@
    .cilsy1
    2sekolahdevopscilsy
    3cilsy@
    7cilsy
    9cilsy
    ```
    
2. Anda diminta untuk menyaring isi file tersebut dengan ketentuan sebagai berikut :
- Tampilkan baris yang harus berawalan angka apapun 1 digit (tidak boleh lebih) kemudian diikuti oleh tulisan cilsy. Masukkan hasilnya ke file baru bernama hasil2-1.txt.
- Tampilkan baris yang harus berawalan angka apapun 1 digit atau lebih yang diikuti oleh tulisan cilsy. Masukkan hasilnya ke file baru bernama hasil2-2.txt.
- Tampilkan baris yang harus berawalan angka apapun 1 digit (tidakboleh lebih) yang diikuti oleh tulisan cilsy dan harus diakhiri oleh tanda “@”. Masukkan hasilnya ke file baru bernama hasil2-3.txt.
- Anda hanya boleh menggunakan teknik regular expression, grep, dan redirection untuk mencapai hal tersebut.

# **Belajar sed**

## ***Apa itu Sed?***

Tools lain yang juga sering digunakan untuk manipulasi file dan teks adalah Sed. Sed biasa digunakan untuk mengganti karakter-karakter dari input yang diberikan. Misalnya merubah semua kalimat yang berawalan saya menjadi kamu. Merubah semua yang huruf kecil menjadi huruf kapital, dll.

## ***Contoh penggunaan Sed***

Sintaks dasar :

```bash
sed ‘s/yangingindiubah/diubahmenjadiapa/flag’
```

Flag yang umum digunakan adalah g (untuk mengubah) dan d (untuk menghapus).

Misalnya kita ingin merubah semua kata rizal menjadi cilsy pada filetest.txt :

```
rizal@rizal-Inspiron-5468 ~ $ sed 's/rizal/cilsy/g' filetest.txt
cilsy
Rizal
RIZAL
manrah
rahman
rahmaN
1cilsy
2cilsy
3cilsy
4cilsy
5cilsy
6Rizal
```

Disana terlihat masih ada kata rizal yang tidak terganti akibat huruf kapital yang digunakan. Kita bisa coba gabungkan ilmu Regular Expression disini.

```bash
rizal@rizal-Inspiron-5468 ~ $ sed 's/[rR][iI][zZ][aA][lL]/cilsy/g' filetest.txt
cilsy
cilsy
cilsy
manrah
rahman
rahmaN
1cilsy
2cilsy
3cilsy
4cilsy
5cilsy
6cilsy
```

Terlihat sekarang semua karakter rizal sudah berubah menjadi cilsy baik itu yang kapital maupun tidak.

Contoh lain misal kita ingin menghapus baris yang berawalan angka :

```bash
rizal@rizal-Inspiron-5468 ~ $ sed '/^[1-9]/d' filetest.txt
rizal
Rizal
RIZAL
manrah
rahman
rahmaN
```

Semua baris 1rizal,2rizal,3rizal sampai 6Rizal sudah terhapus karena masuk kriteria baris yang memiliki awalan angka 1-9.

# **Belajar cut**

## ***Apa itu Cut?***

Cut adalah command yang dapat memotong bagian-bagian tertentu dari sebuah file/teks. Cocok juga untuk melakukan manipulasi dan filtering.

## ***Contoh penggunaan Cut***

Misalnya kita bisa memotong karakter ke 1-3 saja dari isi filetest.txt

```bash
rizal@rizal-Inspiron-5468 ~ $ cut -b 1-3 filetest.txt
riz
Riz
RIZ
man
rah
rah
1ri
2ri
3ri
4ri
5ri
6Ri
```

Terlihat bahwa selain 3 karakter awal, semua karakter yang lain menjadi hilang.

Contoh lain misal kita bisa memotong karakter berdasarkan batas tertentu. Misalnya kita punya file bernama file2.txt dengan isi seperti ini :

```bash
rizal@rizal-Inspiron-5468 ~ $ cat file2.txt
Sekolah,Smith,34,London
Cilsy,Evans,21,Newport
Devops,Jones,32,Truro
```

Disana kita dapat ambil bagian sebagian teks berdasarkan batas tanda koma menggunakan opsi -d (delimiter)

```
rizal@rizal-Inspiron-5468 ~ $ cut -d\\, -f1 file2.txt
Sekolah
Cilsy
Devops
rizal@rizal-Inspiron-5468 ~ $ cut -d\\, -f2 file2.txt
Smith
Evans
Jones
rizal@rizal-Inspiron-5468 ~ $ cut -d\\, -f3 file2.txt
34
21
32

```

- f disana berarti kita ingin ambil potongan yang bagian mana. Bagian 1 artinya bagian paling kiri dari koma pertama, bagian f2 artinya sebelah kanan dari koma pertama, dst. Sedangkan -d untuk menentukan batasnya, yaitu tanda koma (disana juga digunakan tanda escape \ agar tanda koma tetap dianggap karakter biasa *baca kembali bagian Regular Expression).

# **Belajar Sort & Uniq**

## ***Apa itu Sort & Uniq?***

Sort dan Uniq adalah command yang biasanya selalu digunakan berpasangan. Sort adalah command untuk mengurutkan teks, sedangkan Uniq untuk mengeliminasi baris-baris yang sama. Sangat cocok digunakan untuk menghitung jumlah baris-baris yang sama.

## ***Contoh penggunaan Sort dan Uniq***

Misalnya kita punya 1 buah file bernama file3.txt yang berisi :

```bash
rizal@rizal-Inspiron-5468 ~ $ cat file3.txt
website down
website aktif
website aktif
website down
website aktif
website down
website aktif
website aktif
website down
```

Kemudian kita ingin mengetahui ada berapa kali baris website down muncul dan berapa kali website aktif muncul dengan perintah sort dan uniq :

```bash
rizal@rizal-Inspiron-5468 ~ $ sort file3.txt | uniq -c
5 website aktif
4 website down
```

Perintah sort pertama akan mengurutkan seluruh baris berdasarkan alphabet, kemudian perintah uniq -c menampilkan berapa kali baris yang sama muncul.

Materi sort dan uniq ini adalah materi terakhir untuk manipulasi teks dan file.  Sebenarnya masih sangat banyak kombinas-kombinasi manipulasi teks yang bisa dilakukan. Juga masih ada ada tools-tools yang lain seperti tr dan awk yang bisa kita eksplor lebih jauh. Kunci agar bisa menguasai teknik ini hanyalah sering-sering berlatih

# **Exercise**

**Praktek**

Waktu pengerjaan : 10 menit

Masing-masing peserta praktekkan soal berikut ini di kolom terminal Linux masing-masing sambil melakukan sharing screen agar instruktur dapat melihat hasilnya.

1. Pertama-tama buatlah sebuah file bernama latihan3.txt yang berisi :
    
    ```
    lo        Link encap:Local Loopback
    					inet addr:127.0.0.1  Mask:255.0.0.0
    					inet6 addr: ::1/128 Scope:Host
    					UP LOOPBACK RUNNING  MTU:65536  Metric:1
    					RX packets:4654 errors:0 dropped:0 overruns:0 frame:0
    					TX packets:4654 errors:0 dropped:0 overruns:0 carrier:0
    					collisions:0 txqueuelen:1000
    					RX bytes:519016 (519.0 KB)  TX bytes:519016 (519.0 KB)
    wlp2s0    Link encap:Ethernet  HWaddr d4:6a:6a:9a:56:c5
    					inet addr:192.168.88.254  Bcast:192.168.88.255  Mask:255.255.255.0
    					inet6 addr: fe80::3d7d:f7c8:d7c7:7661/64 Scope:Link
    					UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
    					RX packets:805339 errors:0 dropped:0 overruns:0 frame:0
    					TX packets:312298 errors:0 dropped:0 overruns:0 carrier:0
    					collisions:0 txqueuelen:1000
    					RX bytes:997268528 (997.2 MB)  TX bytes:52292659 (52.2 MB)
    eth0      Link encap:Ethernet  HWaddr d4:6a:6a:9a:56:c5
    					inet addr:11.10.100.29  Bcast: 11.10.100.255  Mask:255.255.255.0
    					inet6 addr: fe80::3d7d:f7c8:d7c7:7661/64 Scope:Link
    					UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
    					RX packets:805339 errors:0 dropped:0 overruns:0 frame:0
    					TX packets:312298 errors:0 dropped:0 overruns:0 carrier:0
    					collisions:0 txqueuelen:1000
    					RX bytes:997268528 (997.2 MB)  TX bytes:52292659 (52.2 MB)
    ```
    
2. Anda diminta untuk menyaring isi file sehingga hasil akhirnya menjadi seperti ini :
    
    ```
    11-10-100-29
    127-0-0-1
    192-168-88-254
    ```
    
    Hasil akhir tidak perlu dimasukkan ke suatu file. Cukup tampilkan di command line saja. Anda bebas menggunakan seluruh teknik yang sudah dipelajari di materi manipulasi teks dan file ini.