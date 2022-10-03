# 3. Pengertian CI/CD

Created: July 21, 2022 2:09 PM

CI/CD atau continuous integration/continuous delivery adalah sebuah metode untuk mendeploy atau mendeliver aplikasi ke client dengan otomatisasi ke dalam tahapan pengembangan aplikasi. CI/CD adalah solusi untuk masalah mengintegrasikan kode baru kedalam existing environment sekaligus building dan testing.

CI/CD adalah istilah penting dalam dunia DevOps. Dalam perjalanannya ada 3 istilah yang akan selalu kita gunakan.

![https://lh4.googleusercontent.com/EEkMOKRx3MBzfP8ggVJ01Cv4a-me__jzAuAUy7kosOMIkkYmvp2WJVkszJshgqZX0PjOdkvsdxCNVLBaELdwO6t4C68lWk27EAr8dCVrFoyw5cfFn1RcU9fqmeRZb3xAB3ZSx2J365zDLy8q0ZKVAw](https://lh4.googleusercontent.com/EEkMOKRx3MBzfP8ggVJ01Cv4a-me__jzAuAUy7kosOMIkkYmvp2WJVkszJshgqZX0PjOdkvsdxCNVLBaELdwO6t4C68lWk27EAr8dCVrFoyw5cfFn1RcU9fqmeRZb3xAB3ZSx2J365zDLy8q0ZKVAw)

1. ***Continuous Integration* (CI)**
    
    Pertimbangkan aplikasi yang kodenya disimpan dalam repositori Git di GitLab. *Developer* mendorong perubahan kode setiap hari, beberapa kali sehari. Untuk setiap *push* ke repositori, Kita dapat membuat satu set skrip untuk membuat dan menguji aplikasi secara otomatis, mengurangi kemungkinan memperkenalkan kesalahan pada aplikasi yang ada.
    
2. ***Continuous Delivery* (CD)**
    
    *Continuous Delivery* adalah langkah di luar Integrasi Berkelanjutan. Aplikasi tidak hanya dibangun dan diuji pada setiap perubahan kode yang di-*push* ke basis kode, tetapi, sebagai langkah tambahan, aplikasi ini juga digunakan secara terus menerus, meskipun penerapannya dipicu secara manual.Metode ini memastikan kode diperiksa secara otomatis tetapi membutuhkan campur tangan manusia untuk secara manual dan strategis memicu penyebaran perubahan.
    
3. ***Continuous Deployment* (CDP)**
    
    Continuous Deployment juga merupakan langkah lebih jauh dari *Continuous Integration*, mirip dengan *Continuous Delivery*. Perbedaannya adalah bahwa alih-alih menggunakan aplikasi secara manual, kita mengaturnya untuk digunakan secara otomatis. Sama sekali tidak memerlukan campur tangan manusia untuk memiliki aplikasi kita untuk di *deploy*.
    

Perbedaan Ketiganya dapat dilihat pada gambar berikut:

![https://lh6.googleusercontent.com/bcW6B1QNWVgdW043AMzTzS6Kel6VmZnoiOdEfC6ur0fe76_eVg2AJyJxsoWTUaKmINjx7Yfpm49TMTJEJ9ghbPDcv6Bv50IZ9K4m7Ut5v_kv7k8mF5AR9mK1F7CE5S9E4kZ0Jon7svv8jx_DAl53Nw](https://lh6.googleusercontent.com/bcW6B1QNWVgdW043AMzTzS6Kel6VmZnoiOdEfC6ur0fe76_eVg2AJyJxsoWTUaKmINjx7Yfpm49TMTJEJ9ghbPDcv6Bv50IZ9K4m7Ut5v_kv7k8mF5AR9mK1F7CE5S9E4kZ0Jon7svv8jx_DAl53Nw)

# **Pengembangan dan Hubungan dengan Git Flow**

Dalam kenyataannya di dunia kerja setidaknya ada 3 lingkungan pengembangan wajib. Dan beberapa lingkungan pendukung. Step-step ini bisa saja diimplementasikan berbeda, sesuai kebutuhan tiap-tiap perusahaan.

Berikut lingkungan tersebut dan beberapa penjelasannya:

- *Development*. Dalam fase ini, kode akan diuji coba oleh pembuat kode. Biasanya dalam repository menggunakan nama cabang *(branch) feature*/namafitur.
- *Staging*. Dalam fase ini, kode akan diuji coba oleh Tim QA (Quality Assurance). Biasanya dalam repository menggunakan nama branch staging.
- *Production*. Dalam fase ini, kode akan diuji coba oleh *User*. Biasanya menggunakan branch master.