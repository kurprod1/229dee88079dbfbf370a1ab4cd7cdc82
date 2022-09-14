# 3. Your Big Project

Created: August 16, 2022 1:22 PM

# Project ID : DO-BP-P0

Pada bagian ini, akan dijelaskan mengenai Big Project yang akan kalian kerjakan selama di Sekolah Devops batch 18.

Mengapa kami menampilkan Big Project ini di awal? Karena disini kami berharap para siswa bisa paham apa tujuan dari proses belajar yang dijalani. Dengan kita tahu target akhir dari pembelajaran kita, pastinya kita akan lebih memaknai setiap detail dari proses belajar kita ke depannya

# Penjelasan Project

## **Kondisi Environment Sekarang**

Saat ini, Cilsy sedang melakukan development produk baru yang bernama Cilist (Cilsy List). Cilist ini merupakan aplikasi to-do list yang berbasis web. Aplikasi ini dibangun menggunakan MERN Stack (MongoDB, ExpressJS, ReactJS, dan NodeJS). Saat ini, frontend, backend, dan database baru disimpan di 1 vm yang sama, sehingga apabila terjadi error di vm tersebut, maka aplikasi tidak bisa digunakan sama sekali. Seluruh sistem di  Cilist belum ada sistem DevOps, CI/CD sama sekali.

## **Goal**

Membuat sebuah infrastruktur dengan konsep CI/CD DevOps yang tepat dan lengkap untuk aplikasi web menggunakan Amazon Web Service. Apabila kalian dapat menyelesaikan project ini sesuai requirementnya, maka kalian bisa dinyatakan memiliki kemampuan untuk merancang infrastruktur devops yang cocok digunakan pada apikasi web yang menggunakan layanan Cloud AWS.

## **Requirement**

Pada requirement ini kalian bebas untuk menggunakan tools yang menurut kalian handal dan cocok untuk diterapkan pada Environment yang dibutuhkan.

1. Memberikan desain topologi, sistem dan flow seperti apa yang sebaiknya dibangun. Kelebihan dan kekurangannya apa.
2. Local development (laptop programmer masing-masing),
3. Environment Staging untuk memastikan bahwa benar-benar sudah siap dan tanpa cacat sebelum masuk ke production,
4. Dan environment Production environment yang tampil ke user.
5. Pihak Cilist menginginkan adanya pemisahan antara layanan frontend, backend, serta database.
6. Seluruh sistem harus berbasis Container dan saling berkesinambungan proses development dan deploynya dari sisi programmer. mulai dari development di lokal, masuk ke environment staging, hingga production.
7. Terdapat fitur autoscaling yang dapat mencegah server lambat saat trafik tinggi.
8. Diterapkannya sistem CI/CD (Jenkins atau semacamnya)
9. Terdapat sistem sentral monitoring untuk seluruh container dan server (TIG atau semacamnya)
10. Terdapat sistem sentral logging untuk seluruh container dan server (ELK atau semacamnya)
11. Code-code terkait environment (docker, dll) yang dibuat harus scalable dan bisa digunakan ulang secara bersama-sama oleh tim lain dengan mudah. Misalnya ada programmer baru yang masuk, maka programmer itu tinggal pull seluruh code dari github tanpa ubah apapun, dia sudah bisa langsung start kerja.
12. Biaya environment seefisien mungkin, dan dibuat perhitungan budget yang diberikan untuk 6 bulan pemakaian.
13. Sistem harus High availability 24x7x365.
14. Source code aplikasi: [https://github.com/sdcilsy/cilist](https://github.com/sdcilsy/cilist)

# Syarat keberhasilan/kelulusan

1. Mengerjakan project seusai requirement
2. Harus bisa mempresentasikan & menjelaskan ke instruktur dengan baik pada saat presentasi Final Project.