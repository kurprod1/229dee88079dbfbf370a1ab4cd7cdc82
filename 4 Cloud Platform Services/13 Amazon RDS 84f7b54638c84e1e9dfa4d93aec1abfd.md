# 13. Amazon RDS (Relational Database Service)

Created: July 18, 2022 10:17 PM

# **Apa itu Amazon RDS ?**

**Amazon Relational Database Service (Amazon RDS)** adalah layanan server basis data (*database*) dimana data dan server akan berada di cloud yang akan menjamin kualitas koneksi, kecepatan, keamanan dan kehandalan. Kita dapat memiliki aplikasi server yang kita mau seperti MySQL, Oracle, PostgreSQL dan SQL Server.

![*Amazon RDS Logo*](https://lh4.googleusercontent.com/LrjFyA41d_TA8v7DyQQrP6iUJAegx-cahqBobMrjkPbfRaGan2BneTymFAyT6ycWIkCHdnrGJTolkIhwl_dedzubvHe19xbwl7RQx0Gmz7CbwugRjiZ_Q4MCyiHWCIT7KrU00Vwz6wI4qPDW7Q)

*Amazon RDS Logo*

Dengan menggunakan amazon RDS, server dari database yang kita miliki bisa dimuat secara terpisah dari server tersebut. Kita bisa sesuaikan kapasitas dari server database ini seperti halnya menyeseuaikan sebuah instance pada umumnya.

Salah satu kelebihan utama yang dimiliki layanan ini adalah replica database, layanan ini memungkinkan kita untuk melakukan replica atau mirroring database. Sehingga database yang kita miliki akan aman apabila terjadi kesalahan yang fatal. Inilah yang membedakan database RDS dengan database yang biasanya kita gunakan.

# **Fungsi dan kegunaan Amazon RDS**

Selain berfungsi sebagai layanan server database, Amazon RDS sendiri memiliki beberapa fungsi lain dan keunggulannya. Berikut keuntungan  menggunakan Amazon RDS:

- Tidak membutuhkan Maintenance atau perawatan. Apalagi bila tidak memiliki database administrator yang bertugas merawat, mengoptimasi, memantau, termasuk urusan update dan perbaikan software. Beda halnya jika kita menggunakan database pada Amazon EC2, kita harus melakukan sendiri proses instalasi, konfigurasi, optimasi, hingga menangani masalah ketika menggunakan database.
- Mudah melakukan pengaturan, mulai dari meningkatkan kapasitas storage, CPU, memori, hingga duplikasi read-replica melalui halaman AWS Management Console.
- Backup otomatis. Amazon RDS akan melakukan backup rutin pada waktu yang telah kita tentukan. Jika ingin menambah waktu backup, ada tambahan biaya lagi. Backup berupa snapshot (kondisi mesin) sehingga bisa dengan mudah di-restore jika terjadi masalah. Beda halnya dengan menggunakan Amazon EC2, kita harus membuat script untuk melakukan backup. Script melakukan dumping ke format SQL kemudian mengompresi dan menyimpan ke Amazon S3 yang dilakukan lewat cron.
- Tersedia halaman monitoring. Untuk mengetahui penggunaan CPU dan jumlah koneksi yang terjadi. Akan tetapi kita tidak bisa mengetahui penggunaan storage.

Selain daripada kelebihan yang dapat kita nikmati, adapula beberapa kekurangan yang menjadi nilai minus dari Amazon RDS. Berikut merupakan kekurangan Amazon RDS :

- Tidak ada akses langsung ke file konfigurasi. Jika pada MySQL kita bisa melakukan konfigurasi spesifik melalui file my.cnf atau my.ini, Amazon RDS menggunakan API yang bisa diakses menggunakan Amazon RDS Command Line Tools.
- Amazon RDS dibatasi oleh jumlah koneksi maksimal. Tidak ada cara lain untuk menaikkan jumlah koneksi maksimal kecuali menaikkan spesifikasi instance.

![*Gambaran Amazon RDS*](https://lh6.googleusercontent.com/byjEO6_y4VqRzMLcQhtU2WiCpdaEOAgwL0f4TTiXSYr4JBLJb5wpfYVbfZ5jQQgSbZMGqTUkk9R9FDStPmndO28IuFlUMBZbbdSzboHLBxJDMvQuPwtb5V9CfgwiLgvj2HxHQNIWlL_AwlsVKg)

*Gambaran Amazon RDS*

# **Setup Amazon RDS**

## **Launch DB Instance**

Pada bagian ini kita akan melakukan **setup pada Amazon RDS**, Hal pertama yang harus kita lakukan adalah masuk kedalam menu **Service** lalu cari **RDS** atau Search pada kolom text dengan pencarian RDS seperti berikut.

Selanjutnya kita akan diarahkan pada dashboard Amazon RDS. Untuk membuat DB Instance baru kita harus masuk ke menu **Database** lalu klik tombol **Create database** yang ditunjuk seperti gambar dibawah ini.

![https://lh4.googleusercontent.com/miDgYdgk7Rpn2wQcN01NkeEIGo0SV3TyMbkcPS-ELYRllZmllL-8Y3-lyJ4BZ2VTzi-qNXQKdrLVaMZ4-Lx6KfEi4CYfqn0Ptj2VGCL31oHgWiEXbiCuXSpeSy9JTOX4mvu-DK0lwaYBfP0Bdw](https://lh4.googleusercontent.com/miDgYdgk7Rpn2wQcN01NkeEIGo0SV3TyMbkcPS-ELYRllZmllL-8Y3-lyJ4BZ2VTzi-qNXQKdrLVaMZ4-Lx6KfEi4CYfqn0Ptj2VGCL31oHgWiEXbiCuXSpeSy9JTOX4mvu-DK0lwaYBfP0Bdw)

![https://lh6.googleusercontent.com/jj_ZOEO9EdQWpRXYU5DcyFv6IYq5zN7tDTlmWNtFFsdcljOMaaPdoHk1Zlv4kl2lZI4lyAjmFBYXDu7j6wgBg4W9Lg0WrcOKQK9qp8M-wiNTuvLHsWkfTG21EQ2AbgnpzXCvHrRJi7WxcrsuHQ](https://lh6.googleusercontent.com/jj_ZOEO9EdQWpRXYU5DcyFv6IYq5zN7tDTlmWNtFFsdcljOMaaPdoHk1Zlv4kl2lZI4lyAjmFBYXDu7j6wgBg4W9Lg0WrcOKQK9qp8M-wiNTuvLHsWkfTG21EQ2AbgnpzXCvHrRJi7WxcrsuHQ)

Kemudian pilih **Engine database** yang akan kita gunakan, disini kita akan menggunakan **MySQL**. Selain MySQL, Amazon RDS juga menyediakan database lain seperti Amazon Aurora, MariaDB, PostgreSQL, Oracle dan Microsoft SQL Server. Setelah memilih selanjutnya klik **Next**.

![https://lh5.googleusercontent.com/j_OXyTNOzmTH9wuF3sYBrU-CWtIaRNJ3Lf-YHsLxubO9Mp3ZdH0GjTsx1eKi3G8SPhFX4HMUP2d1MwkbXT0XzdQk7gcdPkZzFvhLu5TwBWihpMyrdI8KrsLlYgoMyAfgrChbMcytGNmbYRnBVg](https://lh5.googleusercontent.com/j_OXyTNOzmTH9wuF3sYBrU-CWtIaRNJ3Lf-YHsLxubO9Mp3ZdH0GjTsx1eKi3G8SPhFX4HMUP2d1MwkbXT0XzdQk7gcdPkZzFvhLu5TwBWihpMyrdI8KrsLlYgoMyAfgrChbMcytGNmbYRnBVg)

Pada bagian **Use Case** kita pilih **Dev/Test** lalu klik **Next** untuk melanjutkan konfigurasi.

![https://lh4.googleusercontent.com/zr55fAzqmoUcsk-FY8w0DKhbwX_jHP4_YG1NZ_hZRTOzNlACkv0i2seO8Q-vKS4-zjwZE5SRnoeEMhkTReaxd9QNZgF93UAG7RlYF6kaN70LiPSoLxZ3x7z8FdW0GU9H_ShkcV4X668DhEeNQQ](https://lh4.googleusercontent.com/zr55fAzqmoUcsk-FY8w0DKhbwX_jHP4_YG1NZ_hZRTOzNlACkv0i2seO8Q-vKS4-zjwZE5SRnoeEMhkTReaxd9QNZgF93UAG7RlYF6kaN70LiPSoLxZ3x7z8FdW0GU9H_ShkcV4X668DhEeNQQ)

Pada bagian **Specift DB details** , kita akan memilih versi mysql yang akan kita gunakan. Disini kita akan coba gunakan **versi 5.6.40.** 

![https://lh4.googleusercontent.com/zJ61UEnX-k_XpnLkc5t11w9zQKKCW39rNKCkQQGrbjD1ah_HJTgSjbdYHhb-K0uaO45aRkHCcG0-lQDSAEg4oYK4AfbA1BTko5ruAHJTqtz4Sh9NyU4em998jlmzuvgARy6pj8bvi15gmF7dwA](https://lh4.googleusercontent.com/zJ61UEnX-k_XpnLkc5t11w9zQKKCW39rNKCkQQGrbjD1ah_HJTgSjbdYHhb-K0uaO45aRkHCcG0-lQDSAEg4oYK4AfbA1BTko5ruAHJTqtz4Sh9NyU4em998jlmzuvgARy6pj8bvi15gmF7dwA)

Kita dapat membuat **replikasi** ke region atau zona lain pada Amazon RDS dengan memilih **Create replica in different zone**. Default size Strorage  20GB, dan type storage dengan SSD.

![https://lh5.googleusercontent.com/zMBDHVR5TenZzvc4k3yUkuaKx44576fJ1yK1c2GkKQnjOH_NBYrZCxRfnhSs2y5-QAB7a5DKQchcV-PA2XG8pc5H0L2Qauhr-qYRsGV2mjt7Pww4zPCQnqDG8a7E_KU_6Po1f8z_PIsP1qXQ4g](https://lh5.googleusercontent.com/zMBDHVR5TenZzvc4k3yUkuaKx44576fJ1yK1c2GkKQnjOH_NBYrZCxRfnhSs2y5-QAB7a5DKQchcV-PA2XG8pc5H0L2Qauhr-qYRsGV2mjt7Pww4zPCQnqDG8a7E_KU_6Po1f8z_PIsP1qXQ4g)

Tahap selanjutnya kita setting **DB Instance Identifier** dengan nama **db-test** dan user **root** lalu master password untuk database yang akan kita buat dengan amazon RDS.

![https://lh6.googleusercontent.com/FzzGYNAaxb2fWvlguNsEQUBxUVWJ3LIl1FOrk8WyGm_CZQounByL1wMhiQViJ_y3RPcokeELyX11WsnbiuorDSYA4jJVl5Pq6obPmpbskqFOl7KJA5G5Eiace93cw2IX96r7dyq4UYW5DjBr6w](https://lh6.googleusercontent.com/FzzGYNAaxb2fWvlguNsEQUBxUVWJ3LIl1FOrk8WyGm_CZQounByL1wMhiQViJ_y3RPcokeELyX11WsnbiuorDSYA4jJVl5Pq6obPmpbskqFOl7KJA5G5Eiace93cw2IX96r7dyq4UYW5DjBr6w)

Pada bagian **Network dan Security Group**, kita pilih **Default VPC** atau VPC yang sudah pernah kita buat. Pada **Public accessibility** pilih yes agar kita dapat membuka database melalui SQL client yang kita miliki.

![https://lh5.googleusercontent.com/5sFcL1V1KvOuemA9brtmGGAmafpmDYOTnzCnxkdabr8dP6VQL-jZ-FtCSqytda2AlwsR8cTjPmNyadCQk4yllvqjYR_sOnXgXqaCZcikG5u_dlbpIdeZdEPnQMha5raHvzpyVRRylL94CVRztg](https://lh5.googleusercontent.com/5sFcL1V1KvOuemA9brtmGGAmafpmDYOTnzCnxkdabr8dP6VQL-jZ-FtCSqytda2AlwsR8cTjPmNyadCQk4yllvqjYR_sOnXgXqaCZcikG5u_dlbpIdeZdEPnQMha5raHvzpyVRRylL94CVRztg)

Selanjutnya kita buat nama database dengan nama **db-test** dan port **default** pada database dengan menggunakan port 3306.

![https://lh3.googleusercontent.com/x8QyD5NydCN-IkLU-_JbfPrKn7zpT91nW9LySRUrDNh8SQY-y7rOU84r-BUbaC9nqwT-UeChtKewa2nOkMd6EVLdVMAUCgUgE8npyjL0aA82HmyZ0VOZg6L01QkNxKS_P9i2eV4UVhriwxQ0rw](https://lh3.googleusercontent.com/x8QyD5NydCN-IkLU-_JbfPrKn7zpT91nW9LySRUrDNh8SQY-y7rOU84r-BUbaC9nqwT-UeChtKewa2nOkMd6EVLdVMAUCgUgE8npyjL0aA82HmyZ0VOZg6L01QkNxKS_P9i2eV4UVhriwxQ0rw)

Coba Scroll lagi ke bagian bawah, kita akan mendapatkan pengaturan monitoring. Disini kita pilih

**Enable Enhanced Monitoring**, dengan **Granularity 60s.**

![https://lh6.googleusercontent.com/OpiGeOFKPLhRYcIXaXYQnDOvZhK2WZf-EloV_agnjnBBll6Qka1KIJcGoq4QL7rCUrJQaT69W9VR7U8fN2lF0kxuBlwxXkghv0iVJpDz5_lAmgOx9gezYGd_H8eZI1N1Cpi0nPXBoMLXY6TUew](https://lh6.googleusercontent.com/OpiGeOFKPLhRYcIXaXYQnDOvZhK2WZf-EloV_agnjnBBll6Qka1KIJcGoq4QL7rCUrJQaT69W9VR7U8fN2lF0kxuBlwxXkghv0iVJpDz5_lAmgOx9gezYGd_H8eZI1N1Cpi0nPXBoMLXY6TUew)

Selanjutnya untuk menyimpan konfiguras yang sudah kita buat, dan mulai menjalankan database, kita klik tombol **Create database.**

![https://lh5.googleusercontent.com/Um2a6AYDoBiNWXM7E9LSSxUMUuMFeAk-Pvil-SiqTq1qzidyx1oyVpDTXgsN4jJZdV7rc4bATfzJdtemqQR38mMKpX01eWQKYTEaCckDe42LPK0GacAa0TCegPK27v4Ff_jjMDa_WaoSgTRR4g](https://lh5.googleusercontent.com/Um2a6AYDoBiNWXM7E9LSSxUMUuMFeAk-Pvil-SiqTq1qzidyx1oyVpDTXgsN4jJZdV7rc4bATfzJdtemqQR38mMKpX01eWQKYTEaCckDe42LPK0GacAa0TCegPK27v4Ff_jjMDa_WaoSgTRR4g)

Setelah proses konfigurasi berhasil dilakukan,  kita dapat melihat detail database dengan menekan tombol **View DB instance detail**.

![https://lh3.googleusercontent.com/Ihb9yml3LpAaT5No5fHjsc0JlG0YeMGkRoYWp4AkV6_K4lQ3AnNVgllkZkMMRsDGTI4CSOggvg5iNPpPWbgt-Tiv5IjKoksgCxQdtUT3nTbLwInRAtSoDmmLbwu_bESS0-N0kh40yWFbXDIzMQ](https://lh3.googleusercontent.com/Ihb9yml3LpAaT5No5fHjsc0JlG0YeMGkRoYWp4AkV6_K4lQ3AnNVgllkZkMMRsDGTI4CSOggvg5iNPpPWbgt-Tiv5IjKoksgCxQdtUT3nTbLwInRAtSoDmmLbwu_bESS0-N0kh40yWFbXDIzMQ)

Berikut merupakan tampilan dashboard dari database yang sudah kita buat. Kita dapat memonitoring penggunakan CPU yang kita gunakan, DB Connetion, dan storage kosong.

![https://lh5.googleusercontent.com/4lEOtP0Krw4MS2tkg_DFpKoA1D1EYwqE5VbEUaRym6rdWszB2buglbpS9dyUsVVDhvWYhoNWbHilZ2sb5UO4CCajcUJ_gBUm9c4CeKPnF2b559pgSF8gwaGNNzwBaj6KSr5ewudPXIjnNyH4jA](https://lh5.googleusercontent.com/4lEOtP0Krw4MS2tkg_DFpKoA1D1EYwqE5VbEUaRym6rdWszB2buglbpS9dyUsVVDhvWYhoNWbHilZ2sb5UO4CCajcUJ_gBUm9c4CeKPnF2b559pgSF8gwaGNNzwBaj6KSr5ewudPXIjnNyH4jA)

Selain itu kita dapat melihat memori yang tidak di gunakan, melihat proses IOPS write dan IOPS read. IOPS densiri mempengaruhi kecepatan dalam mengakses menulis atau membaca database.

![https://lh6.googleusercontent.com/xATifYApSPJ7mnjeAvMcTGxera7NkFq-J8bWyT7YOhW17AIaDXWihdN8tvMhkpe82VPuyg4GtlNxuoOaMSirZG9ZmzI6TcpSnt7wXdhCbCmLUSAKGXmBoryxNGNLK0drBnHghcrOESh6hV2dtA](https://lh6.googleusercontent.com/xATifYApSPJ7mnjeAvMcTGxera7NkFq-J8bWyT7YOhW17AIaDXWihdN8tvMhkpe82VPuyg4GtlNxuoOaMSirZG9ZmzI6TcpSnt7wXdhCbCmLUSAKGXmBoryxNGNLK0drBnHghcrOESh6hV2dtA)

Kita juga dapat melihat detail data mengenai database, seperti versi MySQl, username database, hingga endpoint. Endpoint ini berguna untuk mengakses database MySQL dari SQL Client maupun phpmyadmin yang nanti akan kita setting.

Selain data-data di atas, kita juga dapat melihat **snapshot** (*backup database*) dan juga **CloudWatch** alarm atau notifikasi yang di berikan oleh database MySQL.

![https://lh6.googleusercontent.com/W-Lblo1TD5UmNeJyyiFrpt4Grl_9jfYZShSxk7n4fjaHmKI3-VyytQ3LLzvbguY6W4cwbI2GfXDM3NYqCTP0qdQZ5nEuWzlEUGTuVul8zWgcXfem3dwi4Y_A2tE7yr3iF8lQR2hisrS3MTorkA](https://lh6.googleusercontent.com/W-Lblo1TD5UmNeJyyiFrpt4Grl_9jfYZShSxk7n4fjaHmKI3-VyytQ3LLzvbguY6W4cwbI2GfXDM3NYqCTP0qdQZ5nEuWzlEUGTuVul8zWgcXfem3dwi4Y_A2tE7yr3iF8lQR2hisrS3MTorkA)

Dengan begini, kita sudah memiliki sebuah database yang siap kita isi dengan data-data yang kita miliki, kita bisa mengkombinasikan database ini dengan aplikasi yang kita miliki didalam Server AWS tersebut.

![https://lh5.googleusercontent.com/X9hG8V2qpBHa3NtlQL1mTavou89RI5KgssFKo8CGiVWZ7udhiNKlH0IWoDToFpuJzjsOSEbKUxML7nYE3QsMCB2pxoYsAmL-uLpRyvRKQnph2ZQQ9m_8S-PRnJdt2XJQJ4YuZhFcgbl9BJI_LA](https://lh5.googleusercontent.com/X9hG8V2qpBHa3NtlQL1mTavou89RI5KgssFKo8CGiVWZ7udhiNKlH0IWoDToFpuJzjsOSEbKUxML7nYE3QsMCB2pxoYsAmL-uLpRyvRKQnph2ZQQ9m_8S-PRnJdt2XJQJ4YuZhFcgbl9BJI_LA)

# **Replikasi Amazon RDS**

Apabila pada bagian pembuatan database Amazon RDS tadi kita tidak mengaktifkan **replikasi**, maka kita bisa melakukan replikasi secara manual yang akan kita bahas dibagian ini. Tujuan dari replikasi ini adalah untuk menduplikat database yang sudah kita buat dengan menggunakan sistem mirroring sehingga isi dari duplikasi database yang baru akan sama dengan database pertama yang sudah kita buat sebelumnya.

Pertama kita harus memilih **Database RDS** yang akan kita replikasi. Klik pada tombol **Instance Action**, kemudian klik **Create Read Replica** seperti berikut.

![https://lh6.googleusercontent.com/aVFgsVbpg9_2rOuZYvbrqtafcrTPgR0ysRaCmu97nxRlvpGPNPKTPntw1OQBGZJ5x57-OCFJ7FQlP1wzzuGAVPp6BFcGWQel9INzcHlZ5eaIrX-gpu9YNG2f-3h3JOTwAAVCMBKQFN2FO1nlMA](https://lh6.googleusercontent.com/aVFgsVbpg9_2rOuZYvbrqtafcrTPgR0ysRaCmu97nxRlvpGPNPKTPntw1OQBGZJ5x57-OCFJ7FQlP1wzzuGAVPp6BFcGWQel9INzcHlZ5eaIrX-gpu9YNG2f-3h3JOTwAAVCMBKQFN2FO1nlMA)

Kemudian pada bagian konfigurasi **Network & Security**. Pilih **Destination region** (sebaiknya pilih region yang berbeda) kemudian atur ***Publicly Accessible***, jika kita ingin membuka akses untuk jaringan public maka pilih *yes*. Jika hanya untuk jaringan private maka pilih *no*.

- *Note:  Pilihan *No* pada *Publicly Accessible* digunakan untuk meningkatkan security dan keamanan pada database kita.

![https://lh6.googleusercontent.com/2Ovo78yZp4EyNnV3a-xnzo6O_Jm-6xXF1rr7Uhf0n_eTQdyeUd7bcS3f6BWf0orvP3RjEq5w2nj-VhyQ84UqpwOrXExfbRl-bsZEUwT3es6nZpyPbJVVvBI1mQhx-rVtuObPYUkzpKrEprYSlA](https://lh6.googleusercontent.com/2Ovo78yZp4EyNnV3a-xnzo6O_Jm-6xXF1rr7Uhf0n_eTQdyeUd7bcS3f6BWf0orvP3RjEq5w2nj-VhyQ84UqpwOrXExfbRl-bsZEUwT3es6nZpyPbJVVvBI1mQhx-rVtuObPYUkzpKrEprYSlA)

Kemudian kita masuk ke **Instance specifications**, sesuaikan **DB Instance Class** sama seperti dengan type EC2. Secara default typenya adalah db.t2.micro (1 vCPU, 1 GiB RAM).

![https://lh4.googleusercontent.com/56eqEVjTnSze2Z9OItWhwh3bClZuJfkOJ_12VSXS9SjSd1-2VuMW7E8agExtKC_VML_ggAo6CrLT07VQrUikipi6Y98SGCX3Ir8R3hhy0Y27SJ85J7hEFVQoZzQ4_xW0FkKPEfVzGObkPOkNDQ](https://lh4.googleusercontent.com/56eqEVjTnSze2Z9OItWhwh3bClZuJfkOJ_12VSXS9SjSd1-2VuMW7E8agExtKC_VML_ggAo6CrLT07VQrUikipi6Y98SGCX3Ir8R3hhy0Y27SJ85J7hEFVQoZzQ4_xW0FkKPEfVzGObkPOkNDQ)

Kemudian pada menu **Settings** kita akan memilih **source replika database** yang ingin kita buat, kemudian kita buat nama replikasi (**DB instance identifier**) dengan nama **rdsreplikasi**. Pada Database Options masukan port  dengan **3306,** dan pilih **disable** untuk IAM DB authentification.

![https://lh3.googleusercontent.com/ydXYvKU3ZT5we7CqOyL-UBtgSXFXrYjgGFpPg5-MQHScGqqjYYbIOZ0v03ri14s_ogoQv9pIcBwDFW2Psf_MXOYe2W6MXWSZX541hmURStA_GLS_RHuBGOTDAbKYFAzzShuBh6aE9Dw6gwUSdA](https://lh3.googleusercontent.com/ydXYvKU3ZT5we7CqOyL-UBtgSXFXrYjgGFpPg5-MQHScGqqjYYbIOZ0v03ri14s_ogoQv9pIcBwDFW2Psf_MXOYe2W6MXWSZX541hmURStA_GLS_RHuBGOTDAbKYFAzzShuBh6aE9Dw6gwUSdA)

Kemudian nyalakan pengaturan untuk monitorin dengan klik **enable enhanced monitoring** seperti gambar berikut.

![https://lh3.googleusercontent.com/tzMgBqWTDpqLUxWn4nJNSP0sGlVe9yA6fa1gXjmsmOWV3hJbLaRjC-h3qBQAECi5411tAIpLsmNI0caYXSf5bL07NBpl5evOL-zqUlPM-MXSJeebAPMMsJeNE6uzwg3rSh1yFDpdbjDAYqEc4g](https://lh3.googleusercontent.com/tzMgBqWTDpqLUxWn4nJNSP0sGlVe9yA6fa1gXjmsmOWV3hJbLaRjC-h3qBQAECi5411tAIpLsmNI0caYXSf5bL07NBpl5evOL-zqUlPM-MXSJeebAPMMsJeNE6uzwg3rSh1yFDpdbjDAYqEc4g)

Selanjutnya di bawah pengaturan monitoring akan muncul **Maintenance** dan pilih **Yes** untuk auto maintannce. Setelah semuanya selesai maka kita dapat meng klik **Create read replica.**

![https://lh4.googleusercontent.com/xIbURI4573cQ7YGpJJ2lvQtwMUqm2WIYZuMMxm_6HHOh4xkiYsCMDvDBB3nfg1mSTEBENl4jHbojt45omtNsP8JUIKBPASZZTNfRS2GucBWv4ruhrR6hJGPSlrJvKR_KSw9fKDLUaW7GDlYjUw](https://lh4.googleusercontent.com/xIbURI4573cQ7YGpJJ2lvQtwMUqm2WIYZuMMxm_6HHOh4xkiYsCMDvDBB3nfg1mSTEBENl4jHbojt45omtNsP8JUIKBPASZZTNfRS2GucBWv4ruhrR6hJGPSlrJvKR_KSw9fKDLUaW7GDlYjUw)

Tunggu proses pembuatan replikasi sampai dengan selesai.

Setelah selesai kita akan masuk kedalam halaman **dashboard**, kita dapat melihat informasi untuk koneksi ke amazon RDS , melalui aplikasi yang kita miliki.

Kita juga dapat melihat status Replication pada halaman dashboard

![https://lh3.googleusercontent.com/ELQwdQvdxUJejWFuq0xKFEHJ8ZsVz__AjwjaSojsGaAdoNoHUYkdxeHFghWs6m_NRhZzzr18cq_3zBb6-kEvjkGV1BqqoaabhwsGbn36Y4tDRLUAYskwYHDynRNAii362mJNMrQ80MwFJK315w](https://lh3.googleusercontent.com/ELQwdQvdxUJejWFuq0xKFEHJ8ZsVz__AjwjaSojsGaAdoNoHUYkdxeHFghWs6m_NRhZzzr18cq_3zBb6-kEvjkGV1BqqoaabhwsGbn36Y4tDRLUAYskwYHDynRNAii362mJNMrQ80MwFJK315w)

Dengan begini kita sudah menyelesaikan untuk membuat sebuah replikasi database dari amazon RDS. Apabila kita lupa membuat replikasi, kita bisa membuatnya secara manual seperti ini. Dan database kita akan aman karena datanya sudah di replikasi.

![https://lh3.googleusercontent.com/BfPn5mt-J_ucsJIBuHUfBTQDTnaw29LFdZ8o9Cz4FICx9dw4qP58glJ1ZCEupUtYnwcP4ms76F_BHg4Y_O7PWtZg63A30FYh1Rzf49oz66ggUR0wVLyUMtMreySBmlNdYfr3RVPtdgpTTIuNWw](https://lh3.googleusercontent.com/BfPn5mt-J_ucsJIBuHUfBTQDTnaw29LFdZ8o9Cz4FICx9dw4qP58glJ1ZCEupUtYnwcP4ms76F_BHg4Y_O7PWtZg63A30FYh1Rzf49oz66ggUR0wVLyUMtMreySBmlNdYfr3RVPtdgpTTIuNWw)

# **Setup Web Aplikasi dengan RDS**

## **Migration Database**

Agar aplikasi yang kita miliki dapat menggunakan database dari RDS, pertama kita harus melakukan migrasi database terlebih dahulu agar semua data yang kita miliki bisa langsung digunakan pada database RDS tersebut.

Disini saya asumsikan kita sudah memiliki sebuah server yang sudah ada aplikasi didalamnya, misalkan aplikasi pesbuk yang bisa kita gunakan. Apabila kita sudah memiliki banyak data pada databasenya, kita bisa melakukan export terlebih dahulu dengan menggunakan perintah berikut.

```bash
sudo mysql -u devopscilsy -p dbsosmed > dbsosmed.sql
```

Tunggu sampai proses export selesai dilakukan, selanjutnya kita masuk kembali ke Amazon RDS pada database yang kita buat. Cek alamat endpoint yang ada pada database tersebut.

![https://lh4.googleusercontent.com/s3IjCLs1FjwaC9ea_-clRXETIma4UdQVQ-qdLCzJ6KDsJzorD-uruE0JNOCVupbQVzR5PYqb01dcpRiHd3BublV7mCyxicgtBOJB9BYB4U9XLHkspxaANrP5hKjxAMJO8oNHoFqKZ0VhU5RiHA](https://lh4.googleusercontent.com/s3IjCLs1FjwaC9ea_-clRXETIma4UdQVQ-qdLCzJ6KDsJzorD-uruE0JNOCVupbQVzR5PYqb01dcpRiHd3BublV7mCyxicgtBOJB9BYB4U9XLHkspxaANrP5hKjxAMJO8oNHoFqKZ0VhU5RiHA)

Alamat ini adalah alamat yang akan kita gunakan untuk mengakses database Amazon RDS tersebut, setelah kita mengetahui alamatnya sekarang kita coba melakukan akses pada database yang sudah kita buat di Amazon RDS dengan menggunakan perintah berikut.

```bash
sudo mysql -h **db-test.cqomfrrvzdvl.us-east-2.rds.amazonaws.com** -u root -p
```

***Note** : yang diberi bold adalah endpoint dari database Amazon RDS.

Masukan password sesuai dengan yang sudah kita buat tadi, kita juga bisa cek database yang ada didalamnya menggunakan perintah ***show databases;*** seperti biasa

![https://lh6.googleusercontent.com/KBpCNn6YxU1NSrec7oeNFY7pNnqDhxQHwjruDBTdDGg9k4a0YsydvmFdqcwGKpH87b7oxh_Dd3ZI6KTs7GcBEABXdPYcFnrVkqTsEuHPOka5j8Hb-hLclaxLm-pdSdWYlaanD_71Ye2gd3MxrA](https://lh6.googleusercontent.com/KBpCNn6YxU1NSrec7oeNFY7pNnqDhxQHwjruDBTdDGg9k4a0YsydvmFdqcwGKpH87b7oxh_Dd3ZI6KTs7GcBEABXdPYcFnrVkqTsEuHPOka5j8Hb-hLclaxLm-pdSdWYlaanD_71Ye2gd3MxrA)

Setelah itu coba keluar dari console database tersebut dengan perintah \q lalu kita coba import database yang kita miliki dengan menggunakan perintah berikut.

```bash
sudo mysql -h **db-test.cqomfrrvzdvl.us-east-2.rds.amazonaws.com** -u root -p db_test < dbsosmed.sql
```

*** Note** : yang bold adalah database kita di amazon RDS

Dengan ini proses import database dari local ke database Amazon RDS sudah selesai, sekarang kita masuk kedalam tahap konfigurasi dan perubahan pada konten web aplikasi yang kita miliki.

# **Konfigurasi Web Aplikasi**

Setelah kita melakukan import data dari local ke server database RDS, sekarang kita akan melakukan konfigurasi pada webapps yang kita miliki. Kita akan coba mengubah alamat tujuan, user dan password dari koneksi database webapps ke database RDS.

Untuk itu kita perlu melakukan konfigurasi pada file **config.php** pada web aplikasi **pesbuk**. Perlu diperhatikan bahwa “***file yang kita konfig mungkin tidak akan sama dengan dilapangan, karena file konfig ini nanti menyesuaikan dengan file yang dibuat oleh programmer”***.

Coba masuk kedalam direktory /var/www/html lalu masukan perintah

```bash
sudo nano config.php
```

Didalam konfigurasi tersebut akan terdapat script seperti dibawah ini.

```bash
$db_host = "localhost";

$db_user = "devopscilsy";

$db_pass = "1234567890";

$db_name = "dbsosmed";
```

Coba sesuaikan konfigurasi dengan database RDS yang sudah dibuat tadi seperti dibawah ini.

```bash
$db_host = "db-test.cqomfrrvzdvl.us-east-2.rds.amazonaws.com";

$db_user = "root";

$db_pass = "1234567890";

$db_name = "db_test";
```

Setelah itu simpan konfigurasi pada file tersebut dan coba akses kembali web aplikasi yang kalian miliki. Buat sebuah user baru dan login dengan user baru tersebut.

Apabila berhasil maka proses migrasi database bisa dikatakan berhasil dan selesai.

![*Hasil dari import database*](13%20Amazon%20RDS%20(Relational%20Database%20Service)%2084f7b54638c84e1e9dfa4d93aec1abfd/Untitled.png)

*Hasil dari import database*