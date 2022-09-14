# 3. Pengenalan Server

Created: June 23, 2022 10:25 AM

# **Penjelasan Konsep**

Pada pembahasan bab sebelumnya, sering sekali disebut istilah Server dan Linux. Kedua hal ini kaitannya memang sangat erat dengan DevOps. Dan kedua hal ini adalah hal yang juga sangat berkaitan.

Pada bab ini kita akan fokus mempelajari terkait Linux. Apa itu Linux, kenapa harus Linux, untuk apa Linux, bagaimana pengaplikasiannya, dll. Akan tetapi, sebelum kita mempelajari apa itu Linux dan bagaimana penggunaannya pada dunia DevOps, kita harus mengenal dulu tentang Server.

Server sebenarnya hanyalah sebuah komputer sama seperti komputer pada umumnya. Namun bedanya, komputer server memiliki tujuan untuk memberikan suatu layanan yang bisa dinikmati oleh pengguna. Layanan ini bisa bermacam-macam bentuknya. Ada layanan web, layanan email, layanan database, layanan akses remote jarak jauh, dll. Misalnya kalau kita mau punya website seperti Bhinneka.com, maka itu perlu layanan web. Istilahnya adalah Web Server. Misalnya kalau mau punya aplikasi untuk kirim terima email seperti Gmail, maka itu perlu layanan email. Istilahnya adalah Mail Server. Begitu seterusnya.

[https://lh4.googleusercontent.com/TV0O6h3Fhua6LSiVXD5U_02rOSXeF4VPOOLtBiamiBcT494KEUtn6dwFWHfjAH2OGb9V2FJtW8FRZ8LQv1TkO58izryBV_Lq-7htKi_x2VhlUSQKuRmonp9ev5iA8Qa-MbrnHaDAQY0qcbcLCA](https://lh4.googleusercontent.com/TV0O6h3Fhua6LSiVXD5U_02rOSXeF4VPOOLtBiamiBcT494KEUtn6dwFWHfjAH2OGb9V2FJtW8FRZ8LQv1TkO58izryBV_Lq-7htKi_x2VhlUSQKuRmonp9ev5iA8Qa-MbrnHaDAQY0qcbcLCA)

Karena diperuntukkan untuk melayani pengguna, dan biasanya jumlah pengguna sangat besar (bisa bayangkan website Bukalapak.com itu diakses berapa juta pengguna perhari?), maka spesifikasi dari komputer untuk server ini biasanya sangat bagus. Prosesornya misalnya memiliki 32 Core, RAM nya 32GB, dan Harddisknya 4TB. Inilah yang menyebabkan seakan-akan komputer server dengan komputer biasa itu berbeda, padahal sebenarnya sama. Sama-sama komputer. Bedanya hanyalah di spesifikasinya saja.

[https://lh6.googleusercontent.com/ID3nDNPCQILbsuOtCI4rOJus4mZ4OSSmL-kCfmF3nOA2zw2o6SExgFgRP4Uanh6iFMRsoJpu15eAwWuxBbRzgmwSqSxOzT1P3m6lv8HlzKpBoKv1M-IiRU8bG_ui2uiYAoqdIQbGoX0gufpe1g](https://lh6.googleusercontent.com/ID3nDNPCQILbsuOtCI4rOJus4mZ4OSSmL-kCfmF3nOA2zw2o6SExgFgRP4Uanh6iFMRsoJpu15eAwWuxBbRzgmwSqSxOzT1P3m6lv8HlzKpBoKv1M-IiRU8bG_ui2uiYAoqdIQbGoX0gufpe1g)

Seluruh kegiatan DevOps nantinya pasti berkaitan dengan Server ini. Seluruh aplikasi maupun web di perusahaan tempat DevOps bekerja, itu pasti berjalan di server. Misalnya Tokopedia.com yang memiliki aplikasi berbentuk android dan web. Maka sebenarnya aplikasi-aplikasi itu adalah bentuk “layanan” yang disediakan oleh Server. Ada komputer-komputer Server yang berjalan dibalik itu semua. Dan itulah mengapa DevOps pasti selalu berkutat dengan Server.

Lalu apa hubungannya Server dengan Linux? Seperti yang sudah dijelaskan sebelumnya, pada dasarnya Server hanyalah sebuah komputer. Sebuah komputer ketika ingin bisa berjalan, maka perlu yang namanya Sistem Operasi. Nah, Sistem Operasi yang paling cocok untuk Server adalah Linux dibanding dengan Sistem Operasi yang lain seperti MacOS atau Windows. Kita akan bahas ini secara mendalam pada bagian berikutnya. Intinya disini kita cukup mengetahui bahwa seorang DevOps pasti berkutat selalu dengan yang namanya Server. Dan Sistem Operasi yang paling cocok untuk Server, adalah Linux.

[https://lh6.googleusercontent.com/Ng1z5CWlNLNA6MxStN0w4kvcim6eB0y0bSR2Uun06b-ghmTudnDaFqXwj-bHF43eJD8cXxzbWZMeIIrd1q6u3Y13LJMIJQ1qWijJNOAYPBCzdI7rUNJMS0NeAxdEST44klP2SsMQN2wjgP_pqA](https://lh6.googleusercontent.com/Ng1z5CWlNLNA6MxStN0w4kvcim6eB0y0bSR2Uun06b-ghmTudnDaFqXwj-bHF43eJD8cXxzbWZMeIIrd1q6u3Y13LJMIJQ1qWijJNOAYPBCzdI7rUNJMS0NeAxdEST44klP2SsMQN2wjgP_pqA)

Sebagai tambahan, Server tidak harus selalu berbentuk komputer fisik. Karena ada Server yang bentuknya virtual/cloud. Server virtual/cloud ini kita tidak pernah mengetahui bentuk fisiknya seperti apa, akan tetapi secara spesifikasi sudah sesuai dengan komputer server berbentuk fisik pada umumnya, yaitu memiliki RAM, CPU, dan harddisk tertentu.

# **Exercise**

1. Apa hubungan DevOps dengan Server?
2. Sebutkan Layanan-layanan server lainnya yang pernah Anda ketahui?