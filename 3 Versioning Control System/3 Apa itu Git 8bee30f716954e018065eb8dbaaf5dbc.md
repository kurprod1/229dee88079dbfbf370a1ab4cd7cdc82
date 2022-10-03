# 3. Apa itu Git ?

Created: July 14, 2022 1:11 PM

Pernahkah terbayang temen temen bagaimana seorang designer yang tiap kali designnya gagal, ia akan membuang kertasnya dan memulai dari awal. Dan hal tersebut akan berulang sampai design sudah sesuai dengan keinginan. GIT hadir menyelesaikan problem tersebut. Bagaimana GIT menyelesaikannya dan apa sih sebenernya GIT itu?

Seperti yang kita tahu, perubahan atau changes itu berdampak pula pada hasil akhir sebuah produk. Apa jadinya jika perubahan tersebut tidak bisa di rollback, atau kembali lagi? Terpaksa harus ngulang dari awal ‘kan? Dengan menggunakan GIT, semua changes dapat ter track dan dapat kita rollback sesuai kebutuhan.

Kita ambil contoh seorang developer membuat aplikasi website. Nah pada saat developing, developer tersebut akan membuat chat. Namun setelah dipikir kembali, fitur tersebut sepertinya tidak akan berdampak baik bagi website. Akhirnya developer tersebut menghapus fitur dan sebagai kompensasinya, fitur yang ditambahkan adalah fitur text to speech misalnya. Nah sebelum developer menghapus fitur chat, developer tersebut terlebih dulu melakukan commit dan push ke repository agar dapat bisa rollback bilamana fitur chat kembali digunakan. Dengan begitu, developer tidak perlu membuat fitur chat lagi dari awal. Kira kira begitu contoh kecil kegunaan GIT.

Git merupakan salah satu *Version Control System (VCS)* atau sistem pengontrol versi pada proyek perangkat lunak yang bertugas mencatat setiap perubahan yang terjadi pada tim, maupun perseorangan.

![*Ilustrasi Distributed Revision Control*](https://lh5.googleusercontent.com/N2H4QWgqgy_Q2k2PlS44AnT0ZrLpjk8AEiB_7J-F_tMNyUJaB8o0uUuLihY1L6QnHcVifPiph7X3vqSsOwWPKVNa4t93LP4r4p6gbRwaubdqtAYVx6Gvesmlm1n5IsD7VrtC9ml2MiAEyZCMQA)

*Ilustrasi Distributed Revision Control*

Pada dasarnya GIT itu **menyimpan** perubahan yang terjadi pada project agar dapat mentrack apa saja yang diubah. Dan agar rekan se-tim atau developer lain dapat melihat perubahan yang terjadi. Misalnya ada dev A yang mengerjakan fitur A dan dev B yang mengerjakan fitur B. Diantara keduanya pasti akan ada bentrok karena dari masing masing developer ada fitur baru. Maka dari itu ada yang dinamakan merge yaitu proses menggabungkan beberapa perubahan dari tiap developer yang melakukan changes.

![*Ilustrasi Merge*](https://lh3.googleusercontent.com/nwtTqVTxlY7pDG0XXBVON-uK8XJ7TJ-ziFCMQk7NN-dfZfRU_lYXPKCVzwkhlWklADZCc8gBxWNEuB6zUKtpkRKsWg_Fnke0NFkfuReuHeqxP8VirJEY07p-626-oeVZYZSKBgiqwS9irm-zmg)

*Ilustrasi Merge*

Mungkin ilustrasi dibawah dapat menggambarkan mahasiswa semester akhir yang sedang menggeluti skripsi. Pasti temen temen juga pernah ngalamin hal ini. Ya  buat file baru saat ada perubahan. Tentunya hal ini tidak efektif dan bakal bikin bingung sendiri.

![*Ilustrasi Sebelum Menggunakan Git*](https://lh3.googleusercontent.com/nPBy-lRqa69l4MEkFj-KMpQpngddOabxWQK_KpAekTXeJ9HkZanjN8u0hCNgMCYy28Sx21PzIMnjJV7Pdcy7-iUzfq7G66tjVYO7C-_gmYhJS38Ji-LT8SMICXicceNIkvPEB-4HBvFYrCkaJw)

*Ilustrasi Sebelum Menggunakan Git*

Setelah mengetahui ada GIT, temen temen mungkin akan lebih ter track perubahan yang terjadi pada dokumen seperti ilustrasi dibawah.

![*Ilsutrasi setelah menggunakan Git*](https://lh6.googleusercontent.com/FVAW6lE919tfdGpASbderSsH83PhmVe3R5WBXkzTrTvTGJN_NCI98j7o5_y3cVlWm72fHV-6NVr8eOH1bJ9lMHHU8M6Xpbkb3pcmtlTlY4x3MyECnUrVbpX8Lz2uVf2U6uuYaOi-FUnD7o-aJg)

*Ilsutrasi setelah menggunakan Git*

Keren ‘kan Git? selain dari itu, Git juga ada beberapa manfaat setelah bisa menggunakan Git :

- Bisa menyimpan perubahan versi source code.
- Bisa paham cara kolaborasi dalam proyek.
- Bisa ikut berkontribusi ke proyek open-source.
- Lebih aman digunakan untuk kolaborasi, karena kita bisa tahu apa yang diubah dan siapa yang mengubahnya.
- Bisa memahami cara deploy aplikasi modern.
- dan sebagainya.