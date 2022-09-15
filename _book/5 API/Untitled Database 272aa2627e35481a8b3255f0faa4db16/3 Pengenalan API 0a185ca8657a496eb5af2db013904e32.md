# 3. Pengenalan API

Created: June 29, 2022 7:30 PM

# **Apa itu API ?**

API (*Application Programmable Interface*) adalah sebuah interface yang berupa kumpulan fungsi yang dapat di-'panggil' atau dijalankan oleh program lain. Kegunaan dari API adalah sebagai "jembatan" yang menghubungkan 2 program yang berbeda sehingga dapat memudahkan kegiatan yang akan dilakukan. Sebagai contoh, ketika kita ingin menggunakan fitur kamera di smartphone kita tidak perlu mengetikan kode untuk mengakses interface kamera, kita hanya perlu menggunakan API untuk mengaksesnya saja.

[*Ilustrasi Penggunaan API*](https://lh6.googleusercontent.com/fyNcaBKsnkzMcya8Kkb7Elr3haDn7o_lZjlAb2PP-wMRuViP-M7VgkJ2LY1U53HDM5KPkMRuYTpZxjqafvVeIUU5OFZftHJ8fY27q9wv3lT1OFQIj4rqv-pktgxuIl5tsfRBkw2C-fdzWkKb6w)

*Ilustrasi Penggunaan API*

Penggunaan API saat ini sudah sangat luas penerapannya, penerapannya dapat dilakukan di berbagai bahasa pemrograman, library dan framework, sistem operasi, dan web API atau web service. API dapat dihubungkan untuk menghubungkan 2 program yang berbeda misalnya :

- Menghubungkan bahasa pemrograman php dengan mysql menggunakan perintah/script mysqli dan pdo. Perintah mysqli dan pdo tersebut merupakan API yang digunakan untuk membuat koneksi antara php dan database mysql.
- Pada framework/library Codeigniter, ketika kita akan mengambil data dari sebuah tabel kita tidak perlu menggunakan syntax mysql yang cukup panjang, kita hanya perlu memanggil dengan API "***$this->db->get('nama_tabel');***". Ini merupakan API pada Codeigniter untuk mengambil seluruh data yang ada pada sebuah tabel.

# **REST API**

Rest (*REpresentational State Transfer*) API adalah sebuah gaya perancangan (*architectural style*). REST API memungkinkan terjadinya interaksi antar mesin, maksudnya ketika kita membuka sebuah web yang terjadi adalah interaksi antara manusia dengan mesin, sedangkan ketika menggunakan REST API maka yang terjadi adalah interaksi antara mesin dengan mesin. Salah satu contohnya misalnya aplikasi e-banking.

Aplikasi e-banking tidak mungkin memiliki akses langsung ke database milik bank, akan tetapi aplikasi tersebut dapat mengakses API yang dimiliki bank sehingga mereka dapat mendapatkan data-data dari berbagai bank tersebut.

[*Ilustrasi Alur Rest API*](https://lh3.googleusercontent.com/fGH_JDKJeuL8aK4nonKCWSnrCA03UL0OfVXDBonXJ6ttYvePGjU004GoSOLvYfe7qdCpobZLyDfbuS2sdHeIlBXVIGx-DlptLaMsEd83L3fmZmEDHHMEy56zwcgVKdwWu3SHw29sPSZchs_y_A)

*Ilustrasi Alur Rest API*

Kita dapat analogikan Rest API ini menjadi sebuah restoran. Disebuah restoran ada seorang pelanggan yang datang kemudian memesan makanan dari menu yang diberikan oleh pelayan, setelah selesai memilih pesanan maka pelayan akan menuliskan pesanan dari pelanggan kemudian memberikan pesanan tersebut pada koki di dapur. Setelah pesanan selesai maka pelayan akan mengantarkan makanan dari dapur menuju pelanggan.

[*Analogi Restoran Rest API*](https://lh6.googleusercontent.com/zX2gqMK0O18tb4ZorXQNjv7QOE185xi7l2mamfsb5sxkDy5w4BRhp1XSmHv0Ft4jF6l9PQRCZDN1ZCituBCAP7bCykreb8RXlbxC-CKmBwFdRC5K4bpZ7U-YkuIoWpBH-Phe2OnVcedUG3xIgg)

*Analogi Restoran Rest API*

**Pelanggan** adalah kita sebagai user yang memberikan request. **Pelayan** adalah API yang mencatat serta menyampaikan request dari user. **Menu** yang pelayan berikan adalah REST API karena fungsinya adalah sebagai aturan yang diberikan agar kita tidak memesan hal yang tidak ada dalam menu. Setelah makanan selesai dibuat dari dapur maka yang pelayan antarkan pada pelanggan adalah sebuah response.

# **Arsitektur API**

Hal pertama yang dibutuhkan pertama kali pada saat menggunakan REST API adalah REST Server, dimana bagian ini merupakan bagian yang akan menyediakan resource/data. Nantinya sebuah REST Client akan membuat HTTP Request ke server dan server akan merespon dengan mengirimkan sebuah HTTP Response sesuai request dari client.

[*Ilustrasi antara REST Client dan REST Server*](https://lh5.googleusercontent.com/VcII0Qk0CObUCetd5l2eRBUYBkT-uxDFklInwXIaSxTvHG2Ivc_t5AF4OdQb025CG-O75Mu24MoSIn6Ag1PL1eNUGvaPywDuxjcng7jyLBcwc0ZN2ry5AYiKBVc8fVyxNj9AAQ8aouUnNaJBTQ)

*Ilustrasi antara REST Client dan REST Server*

HTTP Request memiliki beberapa komponen yang diataranya adalah sebagai berikut :

- **HTTP method** : GET, POST, PUT, DELETE dan lain lain yang sesuai dengan penggunaanya
- **URI** (*Uniform Resource Identifier*) untuk mengetahui lokasi data di server
- **HTTP Version** : contohnya HTTP v1.1
- **Request Header** : yang isinya berupa seperti Authorization, tipe client dan lain lain
- **Request Body** : data yang diberikan ke server misalnya URI params

[*Ilustrasi HTTP Methode dari REST Client*](https://lh5.googleusercontent.com/lWOeycVHebIhQ65IIaiCacut7V5mTX-hvQX5iYkGXF-rFZeB8Q6I7ElYJeOlPvjyoA1rPnA3KzCQ_MSGZ47WQo4U70zKljrKwhvvjZmwVIE7FR6z97M2aCrLQyTzBbRrkxoHiJfa6-NW7nIU9g)

*Ilustrasi HTTP Methode dari REST Client*

Sedangkan untuk HTTP Response memiliki komponen sebagai berikut :

- **Response code** : Berupa status server terhadap request, ini dibutuhkan karena yang terjadi adalah interaksi antar mesin. Mesin dapat mengetahui hasilnya dengan embaca status code nya misalnya 200, 401, 404 dan lainnya.
- HTTP Version : contohnya HTTP v1.1
- **Response Header** : berisi metadata seperti contect type, cache tag dan lainnya
- **Response Body** : data resource yang diberikan oleh server baik berupa text, json atau xml

# **Kelebihan dan Kekurangan API**

Meskipun API memiliki beragam fungsi yang memudahkan, ada beberapa hal yang menjadi kekurangan dan juga kelebihan dari service API ini yang diantaranya sebagai berikut.

**Kelebihan API**:

1. Bisa digunakan oleh banyak bahasa pemrograman dan banyak platform.
2. Lebih simple dibandingkan dengan SOAP.
3. Mudah dipelajari.
4. Menggunakan protokol HTTP.

**Kekurangan API** :

1. Waktu akses yang biasanya lebih lama dibandingkan dengan native library.
2. Lebih rentan dengan serangan keamanan karena harus melewati protocol HTTP.