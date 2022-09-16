# 9. Pengenalan Elastic Beanstalk

Created: July 18, 2022 1:26 PM

# **Apa itu Elastic Beanstalk ?**

**AWS Elastic Beanstalk** adalah sebuah *Platform As a Service* (PAaS) yang memberikan kemudahan dan manfaat bagi developer untuk mengembangkan dan mengatur aplikasi di AWS. Seorang Developer dapat menggunakan aplikasi mereka di AWS tanpa Elastic Beanstalk akan tetapi mereka akan menghabiskan waktu untuk memilih dan menyatukan layanan dari berbagai pilihan di dalam sistem lingkungan AWS tersebut.

![*Logo Elastic Beanstalk*](https://lh3.googleusercontent.com/djyzgzuuvDz5ZJe9ytiUmvOK7hQ4H1ggH7M0eiJXRSVGKZ4l_p6mAmH6bwe22D41FZnBEO0XmAZmBa3OGNuNfRbeIHa4ZXLXCiApsFCwV9SGuLNQgTKSbFBptbYvCI8zL34U0cDpb5pkwDItcA)

*Logo Elastic Beanstalk*

Dengan Elastic Beanstalk, memungkinkan mereka dengan cepat menyebarkan dan mengelola aplikasi di AWS dan mengabstraksi layer infrastruktur dari developer.  Meskipun begitu, developer sama sekali tidak dibatasi oleh Elastic Beanstalk. Mereka masih mendapatkan konfigurasi granular atas aplikasi mereka.

Jika kita analogikan, misalkan kita akan merakit sebuah komputer. Maka ada dua cara yang bisa kita lakukan untuk mencapainya, yakni :

![*Ilustrasi analogi memilih komputer*](https://lh6.googleusercontent.com/SXwE057s-qY6X11YVXKp519YK6b-5q_-muRl51MOS9IJrkE0srfc3g8OAtffTmzww0TI92ftrzPQiJnPHq3dPoadaqrEWTTv-j9bmvdc3KjJy2xOoxW382ivUYkqFQ7yX4Sa0Ffp9oWIshS5HA)

*Ilustrasi analogi memilih komputer*

## **Pergi ke Gudang Komputer**

Gudang komputer besar dan membingungkan dengan deretan demi deretan rak yang diletakkan di depan kalian. Kalian akan merasa kewalahan dengan banyaknya pilihan tetapi sangat perlu untuk memiliki semua bagian yang dibutuhkan untuk membangun komputer.

Kalian akan dengan hati-hati menavigasi di antara rak-rak untuk memilih CPU, SSD untuk penyimpanan, perangkat lunak sistem operasi dll. Lalu kalian mulai merakitnya bersama untuk mendapatkan produk akhir, yaitu komputer dambaan kalian.

Ini sama halnya dengan membangun aplikasi pada AWS tanpa Elastic Beanstalk. Kalian memilih seberapa kuat yang kalian inginkan untuk server EC2, jenis layanan penyimpanan apa dan seberapa besar ruang penyimpanannya, dll. Kemudian kalian mulai menyatukannya untuk membuat aplikasi aktif dan berjalan.

## **Pergi ke Toko Ritel Komputer**

Toko ritel komputer memiliki bagian depan toko yang lebih ramah konsumen. Ini jauh lebih bersih dan ber-AC. Di sepanjang gang, kita bisa menemukan salesman sedang tersenyum pada kita, siap untuk menjawab pertanyaan apa pun.

Kalian memberi tahu pramuniaga kebutuhan komputasi (misalkan komputer Game) dan kalian berjalan keluar dengan komputer yang dapat memenuhi kebutuhan itu. Sesederhana itu. Kalian tidak perlu mengambil manual dan berkeliling mencari di rak rak toko tersebut.

Dan jika kita tidak puas dengan spesifikasi yang diberikan, kita memiliki kebebasan untuk meningkatkan dan mengganti bagian tersebut. Seperti inilah kehidupan devops dengan Elastic Beanstalk.

# **Aplikasi yang didukung Elastic Beanstalk**

**Elastic Beanstalk** sangat ideal jika kita memiliki aplikasi web **PHP, Java, Python, Ruby, Node.js, .NET, Go, atau Docker**. Elastic Beanstalk menggunakan layanan AWS inti seperti *Amazon EC2, Amazon Elastic Container Service (Amazon ECS), Auto Scaling dan Elastic Load Balancer* untuk mendukung aplikasi yang perlu skala besar dalam melayani jutaan pengguna.

*Ilustrasi Aplikasi yang didukung Elastic Beanstalk*

![https://lh3.googleusercontent.com/BoIVv6bW85tUtQ6nsKDB0gFZoWd3i4WXLmKJiN1lNy-dM3SxfWbK5Yeb72g26WrnDkd-8HX-517mZ4yJeoCJRR0fKXm9Yk4YnM0CG959OxGVjyqiE0BFArkZOCl7czuj_VKr5v3UBlJC-5_5zQ](https://lh3.googleusercontent.com/BoIVv6bW85tUtQ6nsKDB0gFZoWd3i4WXLmKJiN1lNy-dM3SxfWbK5Yeb72g26WrnDkd-8HX-517mZ4yJeoCJRR0fKXm9Yk4YnM0CG959OxGVjyqiE0BFArkZOCl7czuj_VKr5v3UBlJC-5_5zQ)

Untuk menggunakan **Elastic Beanstalk**, pertama kita perlu membuat aplikasi dan mengunggah versi aplikasi tersebut dalam bentuk bundel aplikasi (misalkan zip) ke Elastic Beanstalk, kemudian memberikan beberapa informasi tentang aplikasi tersebut.

Elastic Beanstalk akan secara otomatis meluncurkan environment dan membuat konfigurasi dari resource AWS yang diperlukan untuk mejalankan aplikasi kita. Setelah environment berhasil diluncukan, selanjutnya kita dapat mengelola environment dan menyebarkan aplikasi dengan versi terbarunya. Berikut diagram ilustrasi dari alur kerja Elastic Beanstalk tersebut.

![*Diagram alur kerja amazon beanstalk*](https://lh3.googleusercontent.com/DNiBja6l7jnHQBWw95JVCvD3BKbuBD7XZGQSkZyP8nHpD4um--hVc-9u_5grt9B94m-wmwfZlTmFltbntUoF6XRHz4aOoGGP_Kcr-27iLhoCsBHD8sfKTtgka5KxZGJ6aWwvZanOr4NF_-z_yQ)

*Diagram alur kerja amazon beanstalk*

Setelah kita membuat dan menyebarkan aplikasi kita, semua informasi tentang aplikasi tersebut baik metrik, event, dan status environment akan bisa kita akses. Elastic Beanstalk sendiri memiliki dashboard yang nantinya akan memudahkan developer dan administrator untuk mengelola aplikasi mereka tanpa harus khawatir dengan infrastructure-nya.

# **Deploy Simple App**

Kali ini kita akan melakukan praktikum dengan **AWS Beanstalk** yaitu mendeploy aplikasi **[landing page cilsy](https://github.com/sdcilsy/landing-page)**. Nah kalau di modul awal kita mendeploy aplikasi pada AWS EC2, kali ini kita akan mendeploynya pada Beanstalk.

1. Pertama tama yang dilakukan adalah membuat zip dari aplikasi dari github.
    
    Dengan aplikasi yang terdapat di **[landing page cilsy](https://github.com/sdcilsy/landing-page)**, kita compress project tersebut sehingga hasilnya menjadi .zip. Kita bisa secara manual dengan memilih semua file dalam project lalu klik kanan compress atau dengan command line seperti berikut.
    
    ```bash
    git clone https://github.com/sdcilsy/landing-pagezip -r landing-page.zip landing-page
    ```
    
2. Setelah itu kita buat environment Beanstalknya dengan pilih service Beanstalk, lalu klik Create new environment.
    
    ![https://lh6.googleusercontent.com/dvt4oMd77C_W-txDc_18MEc1VdET_LvELfVSmd8UTpDmtDRV-F32IOWgW8HE17PdJIQHjeOym2nHaZdFea1mi7eklU_lvS7P1LcMqZnWoUXdMTYugI_qK0oNJx_aHpqwbqk04106EG2d9z30Uw](https://lh6.googleusercontent.com/dvt4oMd77C_W-txDc_18MEc1VdET_LvELfVSmd8UTpDmtDRV-F32IOWgW8HE17PdJIQHjeOym2nHaZdFea1mi7eklU_lvS7P1LcMqZnWoUXdMTYugI_qK0oNJx_aHpqwbqk04106EG2d9z30Uw)
    
3. Pilih tier. Pada kali ini kita akan mendeploy aplikasi, maka kita pilih **web server environment**.
    
    ![https://lh6.googleusercontent.com/JPVqj4mRFP0WVEEGJ8grjzMYOOStef81Hq80XcgVEqIYlVO8VUbrorQOxqC-QGos9yWVSUkag844a8HBdM42zBsRKFrE_hXU5pn5howp8tZWbfFTlyGxyFyuw4GjZ6F_gBc-wUbUl4KolPAL0g](https://lh6.googleusercontent.com/JPVqj4mRFP0WVEEGJ8grjzMYOOStef81Hq80XcgVEqIYlVO8VUbrorQOxqC-QGos9yWVSUkag844a8HBdM42zBsRKFrE_hXU5pn5howp8tZWbfFTlyGxyFyuw4GjZ6F_gBc-wUbUl4KolPAL0g)
    
4. Setelah itu, isi beberapa informasi seperti nama app, environment, platform, dan source code.
    
    Pertama kita isi nama app, atau jika ada, isi tag.
    
    ![https://lh5.googleusercontent.com/a6_s_tj0HjaNZR7maAjjnIXRT4rNCPWV2x4FaXwg2787kXO4vW13mFRnu_uXAD7A6YkfNzLLN0Jux-mmjJy5bFWymCPl54gfUXzagCToSwdonp3brLh7ZJww3hGhmOuiPXXIlB15qA_9VbmXYA](https://lh5.googleusercontent.com/a6_s_tj0HjaNZR7maAjjnIXRT4rNCPWV2x4FaXwg2787kXO4vW13mFRnu_uXAD7A6YkfNzLLN0Jux-mmjJy5bFWymCPl54gfUXzagCToSwdonp3brLh7ZJww3hGhmOuiPXXIlB15qA_9VbmXYA)
    
    Selanjutnya bagian environment, kita biarkan seperti default. Teman teman bisa mencantumkan domain custom yang sesuai.
    
    ![https://lh5.googleusercontent.com/dbRJxITsgeEkBOAKxf1rOHlMyH7sN8zUweFNn_XtIFG-OhObFdYcdMv8ZKUBpKTWBfYqk7ZZw-YWMp7gNYZ79yXnawjJaiibqwjAkajiItxHxxox3qq21ybak__IijBlewzk3QymFkpNx1G5lA](https://lh5.googleusercontent.com/dbRJxITsgeEkBOAKxf1rOHlMyH7sN8zUweFNn_XtIFG-OhObFdYcdMv8ZKUBpKTWBfYqk7ZZw-YWMp7gNYZ79yXnawjJaiibqwjAkajiItxHxxox3qq21ybak__IijBlewzk3QymFkpNx1G5lA)
    
    Selanjutnya adalah pemilihan platform. Aplikasi yang kita buat merupakan aplikasi yang dapat dirender dengan bahasa PHP, jadi kita kali ini menggunakan PHP sebagai platformnya.
    
    ![https://lh6.googleusercontent.com/d8e_se2SjTI2AljIx1BmWDdXAJ-qF7vkX_n5truVLvhay7vfsBjdwaMAH1tUD2wesaWPgp0WhrL4IzQa9elvIcMz-5HRAV3qf5hJ2mJMaAuV2EaqpwYHC1oG3Gfx1eD_AJHKSqxDUiy_QPZCDQ](https://lh6.googleusercontent.com/d8e_se2SjTI2AljIx1BmWDdXAJ-qF7vkX_n5truVLvhay7vfsBjdwaMAH1tUD2wesaWPgp0WhrL4IzQa9elvIcMz-5HRAV3qf5hJ2mJMaAuV2EaqpwYHC1oG3Gfx1eD_AJHKSqxDUiy_QPZCDQ)
    
    Selanjutnya pada bagian Application code, kita akan memilih source code untuk aplikasi yang akan di deploy. Masih ingat dengan **landing-page.zip** yang sudah disiapkan sebelumnya? Kita pilih itu untuk source codenya. Lalu klik **Create environment.**
    
    ![https://lh4.googleusercontent.com/-HIofh3hSk_zi7aZJ0tx3b5ahMob_XGUVwUrHn_vUTAHGltQqzQ6TIYgtT7epkB1Vq9QzVXXh3TQLY7fhN2YL8z0KmM4_xekqf7PFYOlV8XluS_QwsUa3mVbaRi2dHDAmbm2VVIZqvKst9cHrg](https://lh4.googleusercontent.com/-HIofh3hSk_zi7aZJ0tx3b5ahMob_XGUVwUrHn_vUTAHGltQqzQ6TIYgtT7epkB1Vq9QzVXXh3TQLY7fhN2YL8z0KmM4_xekqf7PFYOlV8XluS_QwsUa3mVbaRi2dHDAmbm2VVIZqvKst9cHrg)
    
5. Tunggu environment dibuat. Proses ini berlangsung sekitar 3-5 menit.
6. Akses aplikasi dengan link yang sudah disediakan.
    
    ![https://lh6.googleusercontent.com/jUeeROWRYAbhjRKT9jiWqUbwbIdEIQ5BFz_E8ufhNE3HJN56KqUic7sGhEmGNwz8_wPDU1rdyTOGVIzFG1KcowOeTR5bXaP9Iq6P19Fyb_b298jO9Pmpk60dsJy3HI6z-o6gu8i0O4n0SzqZeQ](https://lh6.googleusercontent.com/jUeeROWRYAbhjRKT9jiWqUbwbIdEIQ5BFz_E8ufhNE3HJN56KqUic7sGhEmGNwz8_wPDU1rdyTOGVIzFG1KcowOeTR5bXaP9Iq6P19Fyb_b298jO9Pmpk60dsJy3HI6z-o6gu8i0O4n0SzqZeQ)
    
    ![https://lh5.googleusercontent.com/zg_Fb2pq7oUFvU-WFiUvnf2uL36A2kMxzRL8aaoefB69xGFDH_HD3ZVeEt80rBAd0ir6fORHPPXRKU0SrKawOeDTbEC85lfjtwzN0E4jdec6hF_6QPAQXTBFDw3CCuoe8vUoLg7fzpFGny-Ywg](https://lh5.googleusercontent.com/zg_Fb2pq7oUFvU-WFiUvnf2uL36A2kMxzRL8aaoefB69xGFDH_HD3ZVeEt80rBAd0ir6fORHPPXRKU0SrKawOeDTbEC85lfjtwzN0E4jdec6hF_6QPAQXTBFDw3CCuoe8vUoLg7fzpFGny-Ywg)
    

# **Exercise**

1. Apa yang menjadi kelebihan dari elastic beanstalk dibanding dengan EC2 ?