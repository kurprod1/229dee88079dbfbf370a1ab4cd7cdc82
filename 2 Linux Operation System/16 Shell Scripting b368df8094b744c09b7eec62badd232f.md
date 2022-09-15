# 16. Shell Scripting

Created: June 27, 2022 2:52 PM

# **Apa itu Shell ?**

Shell adalah sebuah program tempat dimana pengguna dapat mengetikkan perintah-perintah yang diinginkan. Shell juga memungkinkan pengguna untuk menyusun sekumpulan perintah ini pada sebuah atau beberapa file untuk dieksekusi sebagai program.

![*Ilustrasi Shell*](https://lh5.googleusercontent.com/UPagTC-bHf_v56nh9WJEKP4vGOgNLf9fMdapaqgIZDMrUXtBN8bjd9xA0VtnaCBg-vNoNWay78WjODxtIZ1kyQcahrxmsExs8Wi78V00Gfg-JdXNeXza-FMyfqCu4UFOQAH5RAkZ6VKsI3Ef4g)

*Ilustrasi Shell*

Shell  memiliki berbagai macam jenis, yang diantaranya adalah Bourne shell(sh), C shell(csh), Korn shell(ksh), Bourne again shell(bash), Dsb.

Masing - masing shell mempunyai kelebihan dan kekurangan yang mungkin lebih didasarkan pada kebutuhan pemakai yang makin hari makin meningkat. Untuk modul yang digunakan di Sekolah DevOps Cilsy, shell yang digunakan adalah bash shell, yang merupakan pengembangan dari Bourne shell(sh) dan mengambil beberapa feature (keistimewaan) dari C shell serta Korn shell. Bash shell merupakan shell yang cukup banyak digunakan pemakai Linux karena kemudahan serta banyaknya fasilitas perintah yang disediakan.

# **Pemrograman Shell**

Pemrograman Shell itu sendiri adalah teknik untuk menyusun atau mengelompokkan beberapa perintah shell menjadi kumpulan perintah yang melakukan tugas tertentu sesuai tujuan kita sebagai penyusunnya. Kelebihan shell di Linux dibanding sistem operasi lain adalah bahwa shell di linux memungkinkan kita untuk menyusun serangkaian perintah ini seperti halnya bahasa pemrograman. Yaitu melakukan proses I/O, menyeleksi, logika-logika if, looping, membuat fungsi, dsb seperti proses - proses yang umumnya dilakukan oleh suatu bahasa pemrograman. Dengan kata lain Shell di Linux membuat kita dapat membuat sebuah program seperti halnya bahasa pemrograman. Untuk pemrograman shell ini sendiri kita sering menyebutnya sebagai Shell Scripting.

# **Perintah Dasar Shell**

Sebelum mempelajari pemrograman Shell Scripting di Linux sebaiknya kita telah mengetahui dan terbiasa menggunakan berbagai perintah-perintah dasar Shell di Linux. Pada dasarnya perintah dasar Shell yang sering digunakan adalah adalah seluruh command-command dan konsep yang sudah kita pelajari pada bagian sebelumnya. Sehingga jika kita sudah memahami dan terbiasa dengan command-command Linux tersebut, kita akan jauh lebih mudah dalam melakukan pemrograman Shell Scripting ini.

# **Bash Scripting Sederhana.**

Sekarang kita coba membuat script baru dengan mengetikan perintah dibawah ini pada prompt shell :

```bash
![ubuntu@linux$]echo "Script shell pertamaku di linux"
Script shell pertamaku di linux
```

String yang diapit tanda kutip ganda (double quoted) akan ditampilkan pada layar kita, echo adalah statement (perintah) built-in bash yang berfungsi menampilkan informasi ke standard output yang defaultnya adalah layar.

Jika kita ingin mengulangi perintah sebelumnya, kita tidak perlu mengerikan perintahnya kembali, cukup dengan fasilitas history dengan menggunakan tombol panah (atas bawah) kita sudah dapat mengulangi perintah tersebut.

Bagaimana jika perintah yang kita masukan berupa kumpulan perintah yang cukup banyak? tentunya jika kita harus mengetikkan satu-persatu secara terus menerus pada prompt shell akan sangat merepotkan. Untuk itulah sebaiknya perintah-perintah yang banyak tersebut kita simpan ke sebuah file. Dimana file ini dapat kita panggil/eksekusi kapanpun diinginkan.

Kita dapat melakukannya dengan membuat sebuah file misalnya bernama tes dengan perintah nano/vim, lalu didalam file tersebut isi dengan script berikut :

```bash
#!/bin/bash
echo "Hello, apa khabar"
```

Simpan file tersebut, lalu ubah permission file test tesebut agar memiliki hak akses untuk execute (x) menggunakan perintah chmod.

```bash
![ubuntu@linux$]chmod 755 tes
```

Selanjutnya adalah jalankan file tadi dengan perintah berikut :

```bash
![ubuntu@linux$]./tes
```

Tanda #! pada /bin/bash dalam script tes adalah perintah yang diterjemahkan ke kernel linux untuk mengeksekusi path yang disertakan dalam hal ini program bash pada direktory /bin, sebenarnya tanpa mengikutkan baris tersebut anda tetap dapat mengeksekusi script bash, dengan catatan bash adalah shell aktif. atau dengan mengetikkan bash pada prompt shell.

```bash
![ubuntu@linux$]bash tes
```

Selanjutnya kita coba membuat script shell yang menampilkan informasi berikut :

1. Waktu System
2. Info tentang komputer
3. Jumlah pemakai yang sedang login di system

Berikut merupakan contoh bash scriptnya :

```bash
#!/bin/bash
#myinfo
#membersihkan tampilan layar
clear
#menampilkan informasi
echo -n "Waktu system   :"; date
echo -n "Anda           :"; whoami
echo -n "Banyak pemakai :"; who | wc -l
```

Simpan file tersebut dengan nama “myinfo” selanjutnya jangan lupa untuk merubah permission file myinfo agar dapat diakses oleh kita :

```bash
![ubuntu@linux$]chmod 755 myinfo
![ubuntu@linux$]./myinfo
Waktu system   : Wed Jan 25  22:57:15 BORT 2022
Anda           : ubuntu
Banyak pemakai : 2
```

# **Pemakaian Variable**

Secara sederhana variabel adalah ibarat sebuah kotak penyimpanan yang dapat menyimpan suatu isi atau nilai. Isi atau nilai dapat berupa bermacam-macam. Bisa berupa angka, berupa huruf, kalimat, command, dll. Variable pada shell scripting sifatnya juga sama dengan variable pada bahasa pemrograman pada umumnya. Dalam dokumentasi ini kita membagi variabel menjadi 2 kategori, yaitu Positional Parameter Variable dan User Defined Variable. Sebenarnya masih ada 1 kategori variable lain, yaitu Environment Variable, namun variable ini belum terlalu perlu untuk dipahami di awal-awal pembelajaran Shell Scripting ini.

## ***Positional Parameter***

Positional Parameter merupakan variabel yang digunakan shell untuk menampung argumen yang diberikan pada saat shell dijalankan. Lebih jelasnya dapat kita lihat pada bagian script berikut.

```bash
#!/bin/bash
#argumen1
echo $1 adalah salah satu $2 populer di $3
```

Hasilnya adalah sebagai berikut.

```bash
![ubuntu@linux$]./argumen1 bash shell linux
bash adalah salah satu shell populer di linux
```

Ada 3 argumen yang disertakan pada script argumen1 yaitu bash, shell, dan linux, masing2 argumen akan disimpan pada variabel 1,2,3 sesuai posisinya.

## ***User Defined Variable***

User Defined Variable adalah variabel yang didefinisikan sendiri oleh pembuat script sesuai dengan kebutuhannya. Beberapa hal yang perlu diperhatikan dalam mendefenisikan User Defined Variable adalah sebagai berikut.

1. Dimulai dengan huruf atau underscore.
2. Hindari pemakaian spesial karakter seperti *,$,#,dll.
3. Bash bersifat case sensitive, yaitu antara huruf besar dan kecil dianggap berbeda, antara huruf a berbeda dengan A, nama berbeda dengan Nama, NaMa, dsb.

Untuk menentukan nilai variabel gunakan operator assignment (pemberi nilai) "=". Bisa menggunakan contoh script berikut ini :

```bash
myos="linux"        #double-quoted
nama='pinguin'      #single-quoted
hasil=`ls -l`;      #back-quoted
angka=12
```

Kalau kita perhatikan ada 3 tanda kutip yang kita gunakan untuk memberikan nilai string ke suatu variabel, masing-masing tanda kutip itu memiliki sedikit perbedaan.

Dengan kutip ganda (double-quoted), bash mengizinkan kita untuk menyisipkan variabel di dalamnya. Contohnya :

```bash
#!/bin/bash
nama="pinguin"
kata="Hi $nama, apa khabarmu" #menyisipkan variabel nama
echo $kata;
```

Hasilnya adalah sebagai berikut :

```bash
Hi pinguin, apa khabarmu
```

Kita dapat melihat bahwa di dalam variable kata, terdapat juga variable nama yang disisipkan.

Dengan kutip tunggal (single-quoted), akan ditampilkan apa adanya. Sehingga jika kita memasukkan variable didalamnya, tidak akan dianggap sebagai variable. Contohnya adalah sebagai berikut :

```bash
#!/bin/bash
nama="pinguin"
kata='Hi $nama, apa khabarmu' #menyisipkan variabel nama
echo $kata;
```

Hasilnya adalah sebagai berikut :

```bash
Hi $nama, apa khabarmu
```

Dengan kutip terbalik (double-quoted), bash menerjemahkan sebagai perintah/command yang akan dieksekusi, contohnya :

```bash
#!/bin/bash
hapus=`clear`;
isi=`ls -l`;  #hasil perintah ls -l disimpan di var isi
#hapus layar
echo $hapus
#ls -l
echo $isi
```

Hasilnya bisa kita lihat sendiri dengan mencoba perintah tersebut. Yaitu ketika kita memanggil variable $hapus, kita berarti memerintahkan agar shell mengeksekusi perintah/command clear. Begitupun dengan variable $isi.

Agar lebih jelas lagi perbedaannya, kita coba untuk menggabungkan beberapa penggunaan quote serta penggunaan Positional Parameter Variable menjadi satu :

```bash
#!/bin/bash
#varuse
nama="ubuntu"
OS='linux'
distro="macam-macam, bisa slackware, redhat, mandrake, debian, suse, dll"
pc=1
hasilnya=`ls -l $0`
clear
echo -e "Hi $nama,\\npake $OS\\nDistribusi, $distro\\nkomputernya, $pc buah"
echo "Hasil ls -l $0 adalah =$hasilnya"

```

Maka hasilnya akan menjadi seperti berikut ini.

```bash
![ubuntu@linux$]./varuse
Hi ubuntu,
pake linux Distribusi, macam-macam, bisa slackware,redhat,mandrake,debian,suse,dll
komputernya, 1 buah
Hasil ls -l ./varuse adalah -rwxr-xr-x 1 ubuntu users 299 Nov 21 06:24 ./varuse
```

Untuk operasi matematika ada 3 cara yang dapat kita  gunakan, dengan statement builtin *let* atau *expr* atau perintah subtitusi seperti contoh berikut :

```bash
#!/bin/bash
#mat1
a=10
b=5
#memakai let
let jumlah=$a+$b
let kurang=$a-$b
let kali=$a*$b
#memakai expr
bagi=`expr $a / $b`
#memakai perintah subtitusi $((ekspresi))
modul =$(($a%$b))  #sisa pembagian
echo "$a+$b=$jumlah"
echo "$a-$b=$kurang"
echo "$a*$b=$kali"
echo "$a/$b=$bagi"
echo "$a%$b=$mod"
```

Hasilnya adalah seperti berikut.

```bash
![ubuntu@linux$]./mat1
10+5=15
10-5=5
10*5=50
10/5=2
10%5=0
```

Fungsi *expr* begitu berguna baik untuk operasi matematika ataupun string contohnya :

```bash
![ubuntu@linux$]mystr="linux"
![ubuntu@linux$]expr length $mystr
5
```

Mungkin kalian bertanya-tanya, apakah bisa variabel yang akan digunakan dideklarasikan secara eksplisit dengan tipe data tertentu? mungkin seperti C atau pascal, untuk hal ini oleh Bash disediakan statement *declare* dengan opsi *-i* hanya untuk data integer (bilangan bulat). Contohnya sebagai berikut.

```bash
#!/bin/bash
declare -i angka
angka=100;
echo $angka;

```

# **Exercise**

1. Buatlah sebuah script yang dapat menampilkan status layanan dari masing-masing layanan berikut dengan menggunakan teknik Variable Position Parameter :
    1. sshd
    2. mariadb
    3. httpd

# **Belajar Logika Pemrograman pada Bash Script**

Materi ini mengajarkan agar kita lebih terbiasa dengan pola pikir logika seorang programmer. Kita dapat menggunakan berbagai logika ini untuk mencapai tujuan-tujuan tertentu bukan hanya saat membuat file-file script saja, namun untuk berbagai kasus selama menjadi seorang DevOps nantinya.

Disini kita akan mempelajari beberapa contoh kondisi logika seperti If Conditional dan Looping. Misalnya seperti : Jika kondisi A terpenuhi Maka lakukan command B, Ulangi kondisi A sebanyak X, Ulangi command A sampai kondisi B terpenuhi, dsb.

Contoh realnya misal kita dapat membuat script yang berisi kondisi : Jika Programmer sudah upload code mereka, Maka nyalakan server A. Atau Jika user yang akses Server sudah mencapai 1000 orang, maka aktifkan Server tambahan B.

Logika-logika ini akan cukup sering digunakan selama Anda menjadi DevOps. Karena seorang DevOps tidak hanya orang yang pandai jaringan, tapi juga memahami konsep-konsep programming.

## ***If Conditional***

Sederhananya If Conditional ini menggunakan pola berpikir : **Jika A Maka lakukan B.**

![*Flow chart If Condition*](https://lh5.googleusercontent.com/MxAfbqjO1aZV6-yFfC7s3YtmbWSy5t-egzhpmZkYcV18BQ9ttAAYHiyFSjshj01RUsGmoVOp8hua0qhrnChUcpYcLpTnrzREVtSaFgd_VMcz9DgcZ_1-FmQZevjm4RcFFYSpNMut-7IV60U_PQ)

*Flow chart If Condition*

Contohnya :

- jika kondisi A terpenuhi, Maka lakukan B.
- Jika 1+1 = 2 maka lakukan C
- Jika User A belum masuk group Admin, maka masukkan user A kedalam group Admin.

Berikut kita akan coba aplikasikan If Conditional pada bash script. Sintaks dasarnya adalah :

```bash
if ![ CONDITION ]; then
	COMMANDS;
else
	OTHER-COMMANDS;
fi
```

Dimana condition ini terdapat cukup banyak kombinasi yang bisa digunakan diantaranya :

|Operator|Description     |
|--------|----------------|
|! EXPRESSION|The EXPRESSION is false.|
|-n STRING|The length of STRING is greater than zero.|
|-z STRING|The lengh of STRING is zero (ie it is empty).|
|STRING1 = STRING2|STRING1 is equal to STRING2|
|STRING1 != STRING2|STRING1 is not equal to STRING2|
|INTEGER1 -eq INTEGER2|INTEGER1 is numerically equal to INTEGER2|
|INTEGER1 -ne INTEGER2|INTEGER1 is numerically not equal to INTEGER2|
|INTEGER1 -gt INTEGER2|INTEGER1 is numerically greater than INTEGER2|
|INTEGER1 -lt INTEGER2|INTEGER1 is numerically less than INTEGER2|
|-d FILE |FILE exists and is a directory.|
|-e FILE |FILE exists.    |
|-r FILE |FILE exists and the read permission is granted.|
|-s FILE |FILE exists and it's size is greater than zero (ie. it is not empty).|
|-w FILE |FILE exists and the write permission is granted.|
|-x FILE |FILE exists and the execute permission is granted.|

Misal kita ingin membuat script sebagai berikut :

```bash
#!/bin/bash
Y=1
if ![ $Y -eq 2 ]; then
	echo "Hebat"
else
	echo "Keren"
fi
```

Script itu artinya : Jika variabel Y sama dengan 2, maka tampilkan pesan Hebat. Jika selain 2 maka tampilkan Keren. Kita bisa coba ubah-ubah isi variable Y tersebut untuk memastikan apakah kondisi If sudah berjalan.

Kita bisa coba aplikasikan ilmu berbagai command, manipulasi teks dan penggunaan variable yang sudah kita pelajari sebelumnya dengan if conditional ini. Misal kita bisa buat script untuk mencari tau apakah seorang user bernama cilsy sudah masuk ke dalam grup sudo atau belum, jika belum maka masukkan user tersebut ke dalam grup sudo tersebut.

Nb : Pertama-tama buatlah terlebih dahulu user cilsy jika belum ada

Selanjutnya buatlah file bernama scriptbelajar2.sh yang berisi script berikut :

```bash
#!/bin/bash
grupsudo="sudo"
groups $1 | grep $grupsudo
 
if ![ $? -ne 0 ]; then
        echo "User $1 belum masuk grup sudo, kita masukkan terlebih dahulu.."
        sudo usermod -aG $grupsudo $1
        echo "Berhasil!"
else
        echo "User $1 sudah masuk grup sudo"
fi
```

Jangan lupa setelah itu kita berikan hak akses execute :

```bash
chmod 755 scriptbelajar2.sh
```

Selanjutnya coba jalankan script tersebut sambil kita cek perbedaannya antara sebelum masuk grup sudo dan sesudah :

```bash
rizal@rizal-Inspiron-5468 ~ $ groups cilsy
cilsy : cilsy
rizal@rizal-Inspiron-5468 ~ $ ./scriptbelajar2.sh cilsy
User cilsy belum masuk grup sudo, kita masukkan terlebih dahulu..
Berhasil!
rizal@rizal-Inspiron-5468 ~ $ groups cilsy
cilsy : cilsy sudo
rizal@rizal-Inspiron-5468 ~ $ ./scriptbelajar2.sh cilsy
cilsy : cilsy sudo
User cilsy sudah masuk grup sudo
```

Pada script tersebut kita menggunakan beberapa teknik yang sudah kita pelajari sebelumnya seperti User Defined Variable, dan Positional Parameter Variable. Kita juga menggunakan manipulasi teks menggunakan grep.

Yang perlu diperhatikan sedikit adalah pada bagian Condition disana kita menggunakan kondisi $?. $? ini adalah kondisi yang bisa menangkap status dari ada atau tidaknya output dari command yang sudah kita lakukan. Jika command tersebut ada outputnya dan berhasil, maka akan menampilkan angka 0. Jika tidak ada outputnya atau gagal, maka menampilkan angka 1. Sehingga pada kodisi diatas, bisa diartikan kita menangkap status dari command :

```bash
groups $1 | grep $grupsudo
```

Jika Command tersebut menampilkan output (bahwa user Cilsy ada di grup sudo), maka hasil $? menjadi 0. Jika tidak, maka menjadi 1.

Sehingga kesimpulan dari kondisi yang kita gunakan adalah : Jika status dari command “groups $1 | grep $grupsudo” TIDAK SAMA (-ne) dengan 0, maka …….

## ***While Looping***

Pola pikir While Looping adalah seperti ini : **Lakukan X terus menerus selama kondisi Y belum terpenuhi.**

![*Flow Chart While Looping*](https://lh3.googleusercontent.com/_HMsHppNmDFLrUSNvgpPg4Bn_UfuxDetRP6LgP1woYd5vYiBi5vhCXBmeJuWKxGcZ2JKEO7ggqsU-dEya3cNGHlL8b6iwlHcvlB5a2P8ilq1PgTCQIdEFK6pTYc8ifQSnumltXWuWDtAHIuqRA)

*Flow Chart While Looping*

Contohnya :

- Kurangi angka 100 selama hasilnya belum 1.
- Lakukan Command Y Selama command X belum dilaksanakan.
- Jangan restart server selama user yang akses belum 1000 orang.

Sintaks dasar dari While Looping adalah :

```bash
while ![ CONDITION ]
do
COMMAND
done
```

Berikut contoh sederhana dari penggunaan While Looping :

```bash
#!/bin/bash
# Basic while loop
counter=1
while ![ $counter -le 10 ]
do
	echo “Angka : $counter”
	((counter++))
done
echo All done
```

Script diatas Melakukan penambahan variable counter sebanyak 1 terus menerus hingga mencapai 10. Dan pada setiap perulangannya kita menampilkan pesan Angka : counter.

```bash
rizal@rizal-Inspiron-5468 ~ $ ./scriptbelajar4.sh 
Angka : 1
Angka : 2
Angka : 3
Angka : 4
Angka : 5
Angka : 6
Angka : 7
Angka : 8
Angka : 9
Angka : 10
All done
```

## ***For Looping***

Pola pikir For Looping agak sedikit berbeda dengan looping While. Dimana untuk For cara berpikirnya adalah seperti ini : **Untuk setiap X pada List yang diberikan, lakukan serangkaian Command Y. Dimana X nilainya akan sama dengan setiap List yang diberikan.**

![*Flow Chart For Looping*](https://lh6.googleusercontent.com/pl_KJTydCkRq1xC1OxFRg5w1krc509lHHW1pQUNoRrxhhctsh7fvEVRRusL4CYCdaW1YrhvifFBZDyeMFllYAeNeH5JV8xWfHkKTymMDjC-wVJmHqi3hsegKY8-gNQAEdt6DMJH4PiifJ70MQg)

*Flow Chart For Looping*

Contohnya :

- Masukkan user A kedalam setiap grup yang ada di server.
- Cari file bernama X sebanyak 1000 file yang ada di folder Z.
- Hapus angka 1 pada setiap nama file yang ada di folder Z.

Sintaks dasar dari For Looping adalah :

```bash
for VARIABLE in LISTS
do
COMMANDS
done
```

Berikut contoh sederhana dari penggunaan For Looping :

```bash
#!/bin/bash
# Basic range in for loop
for value in {1..5}
do
        touch /tmp/cilsy$value
done
echo All done
```

Pada script tersebut, kita membuat teks bernama cilsy+angka sebanyak 5x di folder /tmp. Sehingga terbuatlah file cilsy1, cilsy2, cilsy3 hingga cilsy5.

Contoh kedua misalnya kita akan membuat List dari masing-masing nama file yang ada di suatu folder kemudian melakukan sesuatu terhadap file tersebut pada setiap perulangannya.

Misal buatlah 3 buah file bernama seperti ini di folder /tmp/latihanscript :

```bash
mkdir /tmp/latihanscript
touch /tmp/latihanscript/forloop1.txt
touch /tmp/latihanscript/forloop2.txt
touch /tmp/latihanscript/forloop3.txt
```

Lalu buat file script bernama scriptbelajar6.sh dengan isi seperti ini :

```bash
#!/bin/bash
lihatdirektori=`ls /tmp/latihanscript`
counter=1
 
for value in $lihatdirektori
do
        mv /tmp/latihanscript/$value /tmp/latihanscript/hasilloop$counter.txt
        ((counter++))
done
echo All done
```

Cobalah eksekusi script tersebut dan lihat perbedaan antara sebelum dan sesudah :

```bash
rizal@rizal-Inspiron-5468 ~ $ chmod 755 scriptbelajar6.sh 
rizal@rizal-Inspiron-5468 ~ $ ls /tmp/latihanscript/
forloop1.txt  forloop2.txt  forloop3.txt
rizal@rizal-Inspiron-5468 ~ $ ./scriptbelajar6.sh 
All done
rizal@rizal-Inspiron-5468 ~ $ ls /tmp/latihanscript/
hasilloop1.txt  hasilloop2.txt  hasilloop3.txt
```

Script tersebut membuat variable value akan menangkap nama masing-masing nama file pada setiap perulangannya. Cara kerjanya kira-kira seperti ini :

```bash
mv /tmp/latihanscript/forloop1.txt /tmp/latihanscript/hasilloop1.txt
mv /tmp/latihanscript/forloop2.txt /tmp/latihanscript/hasilloop2.txt
mv /tmp/latihanscript/forloop3.txt /tmp/latihanscript/hasilloop3.txt
```

# **Exercise**

1. Buatlah sebuah script yang dapat menghitung pada baris keberapa kata “shadow” muncul pada file /etc/group. Jika nilai barisnya lebih dari 10 maka tampilkan pesan “Lebih dari 10”, jika dibawah 10 maka tampilkan pesan “kurang dari 10”.