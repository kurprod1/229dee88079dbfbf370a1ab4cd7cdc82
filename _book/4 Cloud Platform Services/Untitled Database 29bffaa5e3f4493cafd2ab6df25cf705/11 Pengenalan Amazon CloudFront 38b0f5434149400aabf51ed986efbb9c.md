# 11. Pengenalan Amazon CloudFront

Created: July 18, 2022 4:59 PM

# **Apa itu CDN ?**

**CDN (Content Delivery Network)** adalah kumpulan dari server global yang terletak di beberapa data center dan tersebar di berbagai negara. Jaringan ini berfungsi untuk mengirimkan konten dari server ke suatu website. CDN meningkatkan kecepatan pengiriman data melalui jaringan server kepada visitor dari lokasi terdekat yang paling memungkinkan.

[*Ilustrasi tanpa menggunakan CDN*](https://lh3.googleusercontent.com/NoXl-hOqxGyTapzEUnF03MGjObKXU0tsQUCT92487GPbRgvlcKIJuvz5bOkDR1i2w59EaM8sqAnj7JbU7NrR6-NBRcBMlrag-Si1JlGCUfeJfB6ooGd5-FPMVE4pKOJi_4o8XqE1p8RiqDF0CQ)

*Ilustrasi tanpa menggunakan CDN*

Katakanlah lokasi visitor berada di indonesia, sedangkan server dari website kita berada di US. Karena jarak antara lokasi visitor dan server, pengiriman konten memerlukan proses waktu yang lama. Tapi, dengan adanya server CDN yang berada di beberapa tempat seperti indonesia, india, US, proses pengiriman konten dapat menjadi lebih cepat.

Jika visitor kita berasal dari indoneisa, CDN akan mengirimkan file dari lokasi terdekat yang paling memungkinkan. Dalam kasus ini, file bisa jadi dikirimkan dari server yang juga terletak di indonesia.

*Ilustrasi menggunakan CDN*

[https://lh4.googleusercontent.com/yVzq_w7cTmwVtAMymTuUOqPQ7qMfepptCZa1UpdAfRk96WwRubdDf6JwlSAWZhuGJGopc7GPw3UvJ4o4qaO7n4UDdPaTejwik7EXf74ypNKEo6hWI3beETbOb4_YpgY7j_yEg0gyUSYxVa-RXA](https://lh4.googleusercontent.com/yVzq_w7cTmwVtAMymTuUOqPQ7qMfepptCZa1UpdAfRk96WwRubdDf6JwlSAWZhuGJGopc7GPw3UvJ4o4qaO7n4UDdPaTejwik7EXf74ypNKEo6hWI3beETbOb4_YpgY7j_yEg0gyUSYxVa-RXA)

CDN mempercepat loading website. Fungsinya, memastikan pengiriman konten statis seperti gambar, CSS, JavaScript, video, dan lain-lain dari lokasi server terdekat ke pengguna yang mengakses website kita. Hal tersebut dapat meningkatkan kecepatan respon suatu website ketika diakses.

# **Macam-macam CDN**

Karena kecanggihan dari laynan CDN ini, banyak sekali platfrom yang menediakan fasilitas CDN yang dapat kita gunakan. Mulai dari yang gratis sampai dengan yang berbayar, berikut merupakan beberapa macam CDN yang tersedia sampai saat ini.

1. **Cloudflare**
2. **Amazon CloudFront**
3. **Incapsula**
4. **MaxCDN**
5. **RackSpace**
6. **Dll**

Di AWS sendiri kita memiliki layanan yang memiliki fungsi sebagai Content Delivery Network, yaitu adalah Cloudfront. Kita akan membahas mengenai layanan AWS ini.

# **Apa itu Amazon CloudFront ?**

**Amazon CloudFront** adalah layanan **Content Delivery Network** (CDN) yang secara aman mengirimkan data, video, aplikasi, dan API kepada pengguna dengan *low latency* (Jeda waktu yang rendah) dan kecepatan transfer yang tinggi.

**CloudFront** terintegrasi dengan AWS, termasuk lokasi fisik yang terhubung langsung ke infrastruktur global AWS seperti *AWS Shield* untuk mitigasi *DDoS, Amazon S3, Elastis Load Balancing* atau *Amazon EC2* yang bekerja secara lancar.

*Logo AWS CloudFront*

[https://lh5.googleusercontent.com/9t-Htvkzi_5qHtUCuUsoDJnyJnJH-YaLnWUFHl27u4BGDK12iQBk4ysF2zeY1IfVH9a-tnAIQKu_1Li1Njm9ITpqybN7cWVEuX4gVmWqlXU6xkGgOFPKeyPE6tNmNo3njSCsA8AsDOdxHGSY5Q](https://lh5.googleusercontent.com/9t-Htvkzi_5qHtUCuUsoDJnyJnJH-YaLnWUFHl27u4BGDK12iQBk4ysF2zeY1IfVH9a-tnAIQKu_1Li1Njm9ITpqybN7cWVEuX4gVmWqlXU6xkGgOFPKeyPE6tNmNo3njSCsA8AsDOdxHGSY5Q)

Amazon CloudFront mempercepat distribusi konten web statis dan dinamis seperti html, css, js, dan file gambar kepada pengguna. CloudFront memberikan konten melalui jaringan pusat data di seluruh dunia yang disebut ***edge location.***

Ketika seorang pengguna melakukan request konten melalui layanan cloudfront, maka pengguna akan diarahkan ke lokasi yang menyediakan *low latency* sehingga konten tersebut akan dikirimkan dengan kinerja sebaik mungkin.

1. Jika konten sudah berada di *edge location* dengan *low latency*, CloudFront akan segera mengirimkannya.
2. Akan tetapi jika konten tidak berada di *edge location* tersebut, CloudFront akan mengambilnya dari asal yang telah kita tetapkan (misalkan webserver) yang di identifikasi sebagai sumber untuk versi definitif konten.

# **Praktek Amazon CloudFront**

## **Setup S3 Bucket**

Sebelum melakukan setup pada **cloudfront**, pertama kita harus menyiapkan terlebih dahulu **sebuah bucket di Amazon S3**. Karena cloudfront sendiri menggunakan S3 bucket untuk penggunaannya.

Disini kita anggap kalian sudah mengerti paham bagaimana cara membuat sebuah bucket S3 baru, apabila kalian masih kebingungan, kalian bisa membaca kembali tahap sebelumnya mengenai Amazon S3. Berikut adalah requirement untuk S3 bucket yang akan digunakan.

- Sebuah Bucket S3 dengan nama kalian (contoh ***tresna-devops-S3***)
- Buat bucket di region manapun
- Jangan dulu mengisi apapun pada S3 tersebut.

## **Setup Amazon CloudFront dengan S3**

Setelah kita menyiapkan S3 Bucket, selanjutnya kita lakukan setup pada cloudfront. Untuk masuk kedalam dashboard kita hanya perlu memilih menu **Services > Cloudfront** seperti dibawah ini.

[https://lh6.googleusercontent.com/vX6ZLp2eJoX-lLMKRFBrgQx_Ct193leGq5mYL5F9u6PDcjHv4QyS_vLQI6p052buAvmLvISVjwv6cw7SGwkz2Dgl4C7gA7lzq98UL8Ly1Wh5AVMyU3n2R-8YLQoOf5ME2YBh-ZcBoVL7upqHnQ](https://lh6.googleusercontent.com/vX6ZLp2eJoX-lLMKRFBrgQx_Ct193leGq5mYL5F9u6PDcjHv4QyS_vLQI6p052buAvmLvISVjwv6cw7SGwkz2Dgl4C7gA7lzq98UL8Ly1Wh5AVMyU3n2R-8YLQoOf5ME2YBh-ZcBoVL7upqHnQ)

Setelah masuk kedalam **dashboard** milik cloudfont, selanjutnya pilih menu **Create Distribution** untuk membuat sebuah CDN baru.

[https://lh3.googleusercontent.com/Wx2wxwLyH0LFDKq1cEnmKanFHH824LF7WqCYARNq4gATWOIBWbQCqO72my_hGJ8f7K0UdiOeg4sqA4jvWpZJ5tCVarVgJwxdnbo2pz3tixA7UGlQs4vJ1xeoOcwu-oQW9GY5K0f85MpezuNfsA](https://lh3.googleusercontent.com/Wx2wxwLyH0LFDKq1cEnmKanFHH824LF7WqCYARNq4gATWOIBWbQCqO72my_hGJ8f7K0UdiOeg4sqA4jvWpZJ5tCVarVgJwxdnbo2pz3tixA7UGlQs4vJ1xeoOcwu-oQW9GY5K0f85MpezuNfsA)

Kita akan diarahkan untuk membuat Distribution dengan mengeklik Get Started.

[https://lh5.googleusercontent.com/hq165Qui-1o0n6xO4saB-oVo2mBf5iWQP7eilKYegj1d-wKtH5bXq9CiQlbgdXTs_o3x3HKonppq_P1NI0hcQvzQkJQfIZeYLMQUnG3-sGpjbh6ZXZC7yx2YrqRsVpQuTQvC1B99a4lSP2TEfg](https://lh5.googleusercontent.com/hq165Qui-1o0n6xO4saB-oVo2mBf5iWQP7eilKYegj1d-wKtH5bXq9CiQlbgdXTs_o3x3HKonppq_P1NI0hcQvzQkJQfIZeYLMQUnG3-sGpjbh6ZXZC7yx2YrqRsVpQuTQvC1B99a4lSP2TEfg)

Isikan **Origin Domain Name** dengan **bucket S3** yang kita sudah buat tadi, lalu ubah beberapa option menjadi seperti berikut.

- **Restrict Bucket Access =** Yes
- **Origin Access Identity =** Create a New Identity
- **Grant Read Permissions on Bucket =** Yes, Update Bucket Policy

Setelah itu scroll ke bagian bawah, karena tidak banyak yang akan kita konfigurasi disini. Sampai pada bagian dibawah ini, ubah **Default Root Object** menjadi **index.html**. Sesuaikan nanti dengan konten yang ada di dalam bucket tersebut.

[https://lh4.googleusercontent.com/b9OaQqPlDd0Qh2KyKhH84jnNbAwsKYrWdO8Q12aJULivIvK0jWIVJPRI-Ybf4YIwiZVztCdFBE7oqb_oc8fZ2HGqDtaeglXYAeiIpWGXDd4fHcVKMc91M-81VK7edRgmLujowwY96PLzVGTrVw](https://lh4.googleusercontent.com/b9OaQqPlDd0Qh2KyKhH84jnNbAwsKYrWdO8Q12aJULivIvK0jWIVJPRI-Ybf4YIwiZVztCdFBE7oqb_oc8fZ2HGqDtaeglXYAeiIpWGXDd4fHcVKMc91M-81VK7edRgmLujowwY96PLzVGTrVw)

Lalu untuk menyelesaikan konfigurasi, klik **Create Distribution**.

[https://lh3.googleusercontent.com/Lpc4QRpdhR8K3Mc78QTBdQGa8S-ZG1SrUZi3Htxw0yJzWHVqWyy70lh3U0TaznulRNtGwe8rc8m8TI4fPwqnLKJxKiYcbgVYPdvd7edZR9qK4Fwz0jRqXyWV8CfqiePTM0U4IYtEhmSbZ4sQ1w](https://lh3.googleusercontent.com/Lpc4QRpdhR8K3Mc78QTBdQGa8S-ZG1SrUZi3Htxw0yJzWHVqWyy70lh3U0TaznulRNtGwe8rc8m8TI4fPwqnLKJxKiYcbgVYPdvd7edZR9qK4Fwz0jRqXyWV8CfqiePTM0U4IYtEhmSbZ4sQ1w)

Maka hasilnya akan terlihat seperti dibawah ini, proses pembuatan masih berlangsung. Kita bisa lihat pada bagian **Status** yang masih **in progress**. Kita bisa lihat domain cloudfront kita dengan memilih menu **Distribution Settings**.

[https://lh6.googleusercontent.com/hcrmccqcvjuuhIpTI2bUCWvyESrvona38b_CO_1wb7yWt2G6QxPN7er-hcodBodN0wcUoRU2NJVhQmkc56yTTOKpCtKlpnyV6-Q2fBJV0Pb4u5wtqMOVUFqjuMuhQt-m_Q-K94AV4dW9Z57m8g](https://lh6.googleusercontent.com/hcrmccqcvjuuhIpTI2bUCWvyESrvona38b_CO_1wb7yWt2G6QxPN7er-hcodBodN0wcUoRU2NJVhQmkc56yTTOKpCtKlpnyV6-Q2fBJV0Pb4u5wtqMOVUFqjuMuhQt-m_Q-K94AV4dW9Z57m8g)

Setelah masuk setting, kita bisa melihat bagian alamat domain pada cloudfront tersebut. Kita bisa coba akses alamatnya, apabila alamat masih belum bisa diakses maka kita hanya perlu menunggu 3-5 menit.

[https://lh3.googleusercontent.com/2tiLjt4Ng-iyF233TtFalwAv9A8c46dzipEBvb03eCD0pMKCQlDpN9OO5DpW_Efpc97kJUopHlffSJ_TsoOAypksTCnTli1dxL4rJf_ReoNohpQp45k0VszpFo3iJfxZzbiUuPXDvOQksX_HIg](https://lh3.googleusercontent.com/2tiLjt4Ng-iyF233TtFalwAv9A8c46dzipEBvb03eCD0pMKCQlDpN9OO5DpW_Efpc97kJUopHlffSJ_TsoOAypksTCnTli1dxL4rJf_ReoNohpQp45k0VszpFo3iJfxZzbiUuPXDvOQksX_HIg)

Berikut merupakan hasil dari cloudfront yang sudah kita buat, hasilnya akan terlihat seperti dibawah ini.

[https://lh6.googleusercontent.com/oaL9cP0cGYn5yaWWveEu4NwmAxgRif0OkfStOliPU2JfhtU05GWkHa8uZrTsxdOs7oSta--Byo4BIRvmO8g8820lb69FNQ-sMQC0wdnqO8Q1DmfRvH6ktFpOiK2YdZh5kOkSZ8yvwYTYTxvfTA](https://lh6.googleusercontent.com/oaL9cP0cGYn5yaWWveEu4NwmAxgRif0OkfStOliPU2JfhtU05GWkHa8uZrTsxdOs7oSta--Byo4BIRvmO8g8820lb69FNQ-sMQC0wdnqO8Q1DmfRvH6ktFpOiK2YdZh5kOkSZ8yvwYTYTxvfTA)

# **Setup Amazon CloudFront dengan Load Balancer**

Selain menggunakan S3 Bucket, CloudFront ini dapat menggunakan **Load Balancer** dan Elastic Beanstalk untuk **Content Delivery Network.** Hanya terdapat sedikit perbedaan konfigurasi di awal untuk dapat menggunakan Load Balancer pada CDN ini.

Langkah pertama yang harus kita lakukan adalah menyiapkan server yang sudah kita load balance, saya asumsikan disini kalian sudah membuat load balancer tersebut. Setelah iku kita buat sebuah cloudfront baru dengan cara yang sama seperti sebelumnya.

Pilih menu **Create Distribution** untuk membuat sebuah CDN baru.

[https://lh3.googleusercontent.com/Wx2wxwLyH0LFDKq1cEnmKanFHH824LF7WqCYARNq4gATWOIBWbQCqO72my_hGJ8f7K0UdiOeg4sqA4jvWpZJ5tCVarVgJwxdnbo2pz3tixA7UGlQs4vJ1xeoOcwu-oQW9GY5K0f85MpezuNfsA](https://lh3.googleusercontent.com/Wx2wxwLyH0LFDKq1cEnmKanFHH824LF7WqCYARNq4gATWOIBWbQCqO72my_hGJ8f7K0UdiOeg4sqA4jvWpZJ5tCVarVgJwxdnbo2pz3tixA7UGlQs4vJ1xeoOcwu-oQW9GY5K0f85MpezuNfsA)

Isikan **Origin Domain Name** dengan **Load Balancer** yang kita sudah buat tadi, lalu ubah beberapa option menjadi seperti berikut.

- **Origin Protocol Policy = Match viewer**

[https://lh4.googleusercontent.com/mMW9j6p_k8rR5qzuSqNt7hQpsAnPafc1AZf4CqxObEDzD5b5HTdg8PKQbD6ekOezrw6gwBfsjL9OKaOA3uTsCDNiA3FL7tzVv99c_nGDiqFMtRYhY4GdDvLEHxlCik7Shfsd9PRC-jmSX1btZg](https://lh4.googleusercontent.com/mMW9j6p_k8rR5qzuSqNt7hQpsAnPafc1AZf4CqxObEDzD5b5HTdg8PKQbD6ekOezrw6gwBfsjL9OKaOA3uTsCDNiA3FL7tzVv99c_nGDiqFMtRYhY4GdDvLEHxlCik7Shfsd9PRC-jmSX1btZg)

Setelah itu scroll ke bagian bawah, karena tidak banyak yang akan kita konfigurasi disini. Sampai pada bagian dibawah ini, ubah **Default Root Object** menjadi **index.html**. Sesuaikan nanti dengan konten yang ada di dalam bucket tersebut.

Lalu untuk menyelesaikan konfigurasi, klik **Create Distribution**.

[https://lh4.googleusercontent.com/3OKkR6WjElqtGmLQxkGesdNJH5ae0Ckkq3QZ8sNF3brk0_g0BlJZlQeiwqERH3u0aa9B1EvtvUmBpiUcZ-ILniiucx_jQkxrTPM6QciM9ZyCveqCDHyc9l0EhGW0U4J5XYVb5WcYfQIQDx_9Kg](https://lh4.googleusercontent.com/3OKkR6WjElqtGmLQxkGesdNJH5ae0Ckkq3QZ8sNF3brk0_g0BlJZlQeiwqERH3u0aa9B1EvtvUmBpiUcZ-ILniiucx_jQkxrTPM6QciM9ZyCveqCDHyc9l0EhGW0U4J5XYVb5WcYfQIQDx_9Kg)

Setelahnya akan muncul seperti dibawah ini, klik menu **Distribution** untuk melihat hasil yang sudah kita buat.

[https://lh4.googleusercontent.com/YyGUvrIgF-xAGalR9h2Kt8dlh4vDwUFaHMS5g-pUYWXBUJSxcDrnfY8iJ3I-8-BClm1n-pvFv4-sPkDOACBPSzzE4oj4gnCl-8VEYSvKCk1Vi-8dODjxwolgYW5K0hhmrkyakvQTk-wV2JGPZA](https://lh4.googleusercontent.com/YyGUvrIgF-xAGalR9h2Kt8dlh4vDwUFaHMS5g-pUYWXBUJSxcDrnfY8iJ3I-8-BClm1n-pvFv4-sPkDOACBPSzzE4oj4gnCl-8VEYSvKCk1Vi-8dODjxwolgYW5K0hhmrkyakvQTk-wV2JGPZA)

Maka hasilnya akan terlihat seperti dibawah ini, proses pembuatan masih berlangsung. Kita bisa lihat pada bagian **Status** yang masih **in progress**. Kita bisa lihat domain cloudfront kita dengan memilih menu **Distribution Settings**.

[https://lh3.googleusercontent.com/aXeY1pvrkfNLQumEs6LQL9FEUxpmlwyffXIBFDS413MCiHloPaLUiqVkHl25-LjVS9XTf1jDAo5icUamu6bz31wjlvw2SzKkc98hgSYokX1Vqafkxp7L5AqUnW5mjd9Jjp4Ez649Bat-Fdz0sA](https://lh3.googleusercontent.com/aXeY1pvrkfNLQumEs6LQL9FEUxpmlwyffXIBFDS413MCiHloPaLUiqVkHl25-LjVS9XTf1jDAo5icUamu6bz31wjlvw2SzKkc98hgSYokX1Vqafkxp7L5AqUnW5mjd9Jjp4Ez649Bat-Fdz0sA)

Setelah masuk setting, kita bisa melihat bagian alamat domain pada cloudfront tersebut. Kita bisa coba akses alamatnya, apabila alamat masih belum bisa diakses maka kita hanya perlu menunggu 3-5 menit.

[*Alamat CloudFront yang sudah berhasil dibuat*](https://lh3.googleusercontent.com/PaO1mZJ3JLZGqbK_rp1ARjtXlfA5Bbfdrwa7XlA2t7FWiG8hS1OdrPfbTjHx9bHrIc1itYslu8qM8E5e9WY0Zm22Hx2ec9t_7-W3ytXvM1kJM7rDIndrnw7qt_tpy0otnN2pCtxcNTvbL78x-g)

*Alamat CloudFront yang sudah berhasil dibuat*