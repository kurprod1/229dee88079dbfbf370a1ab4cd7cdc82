# 1. Introduction

Created: August 15, 2022 1:35 PM

Kalau kita bicara soal cloud, DevOps, dan teknologi, rasanya tidak akan luput dari yang namanya Linux. Dan yang perlu kita sadari bahwa cloud kebanyakan berisi Linux servers yang saling terhubung dengan network atau jaringan komputer.

Memiliki dasar linux, jaringan, dan scripting yang kuat merupakan salah satu “syarat penting” untuk memiliki karir di bidang DevOps. Pada section ini, kita akan membuat sebuah project yang akan mengkombinasikan 3 elemen diatas, untuk “pemanasan” sebelum kita memasuki topik-topik lainnya.

# Timeline

Kami menyarankan untuk mempelajari ketiga topik ini secara mendalam dengan menggunakan timeline sebagai berikut:

| No  | Topic            | Duration  |
| --- | ---------------- | --------- |
| 1   | Networking basic | < 1 pekan |
| 2   | Linux basic      | 1 pekan   |
| 3   | Bash scripting   | 1 pekan   |

Akan tetapi kami juga menyadari bahwa tempo belajar setiap orang akan berbeda-beda, maka dari itu, kamu bisa menyesuaikan pace belajarmu, namun dengan catatan jangan melebihi dari guideline waktu yang ditentukan, ya, karena masih banyak hal yang perlu kita pelajari kedepannya.

Untuk mempermudah kalian dalam menentukan objektif belajar, serta memastikan tidak ada yang terlewat, kami sediakan *mindmap* terkait apa saja yang semestinya kalian pelajari untuk memahami jaringan komputer yang nantinya akan digunakan di karir DevOps kalian.

![DO - Network.jpg](1%20Introduction/DO_-_Network.jpg)

# Why do We learn This? (An Overview)

Setelah kita mempelajari dasar mengenai jaringan hingga topologi, nantinya kita akan coba untuk melihat  topologi yang akan kita bangun pada proses pembelajaran di sekolah devops cilsy. Topologi yang akan kita bangun merupakan gambaran akhir dari tujuan pembangunan infrastruktur cloud, dimana infrastruktur tersebut terdiri dari komponen yang ada pada AWS, Git, dan juga bagian local.Perlu dipahami, pada saat awal perancangan infrastruktur baiknya kita sudah merencanakan apa saja yang akan kita bangun terlebih dahulu. Agar memudahkan kita dalam membangun environment yang layak dan optimal untuk kebutuhan aplikasi kita.Berikut merupakan topologi yang akan kita gunakan pada proses pembelajaran ini :

****

![topo.png](1%20Introduction/topo.png)

**Note**: Topologi diatas hanya berupa gambaran besarnya saja, Setiap orang berhak mengubah topologi tersebut berdasarkan tingkat pemahamannya, entah itu nantinya akan semakin besar, ataupun semakin simple, tergantung best practices yang dipahami.