# 4. Arsitektur Docker

Created: July 4, 2022 1:37 PM

Pada bagian ini kita akan mempelajari secara ringkas komponen apa saja yang terdapat didalam Docker dan seperti apa alur proses dari komponen-komponen tersebut. Setiap komputer/server yang sudah kita *install* Docker, maka pasti memiliki komponen-komponen ini dan juga memiliki alur proses yang sama.

Berikut adalah gambar dari arsitektur Docker yang akan kita bahas masing-masing berikutnya :

![*Arsitektur Docker*](https://lh3.googleusercontent.com/hI37H79AvzUnJYuHMhxB3SUEseYcUWQT1McvibSJYN7QrafM1NQ7rQrj_0xs5oLF-wMiMf59WZov0gIHfpwNNdbBF2G1NK4Dk7OPZxOe766qSRx9E4hjS1PEEF-PjXAJcOcJ7CjkieIN3xI-7w)

*Arsitektur Docker*

# ***Client***

**Docker *Client*** adalah seluruh *Command* Docker yang kita jalankan di layar terminal. Command ini nantinya akan masuk ke Docker *Host* untuk kemudian dieksekusi sesuai fungsinya.

# ***Host* dan *Daemon***

**Docker *Host*** merupakan mesin (komputer,server) yang terinstall Docker didalamnya. Didalam Docker Host terdapat Docker *Daemon* yang merupakan otak utama untuk memproses setiap permintaan (command) dari Docker *Client*. **Docker *Daemon*** yang akan mengatur bahwa misalnya *command* “docker *image* *push*” akan melakukan upload sebuah image ke *Registry*, atau *command* “docker *container* ls” akan menampilkan seluruh daftar container yang sedang berjalan di sistem.

Docker Host dan Docker Client sudah terinstall di mesin kita masing-masing saat kita melakukan instalasi Docker sebelumnya.

# ***Image***

***Image*** adalah aplikasi yang ingin kita jalankan. Image berisi *binary, library* dan s*ource code* dari aplikasi yang ingin kita jalankan tersebut. Pada prakteknya Image ini akan sering kita isi komponen berikut :

1. Layanan (nginx,mysql)
2. Layanan + Aplikasi (nodejs + web apps berbasis nodejs)
3. OS (ubuntu,centos,alpine)
4. OS + Layanan (ubuntu+nginx, ubuntu+nodejs)
5. OS + Layanan + Aplikasi + Konfigurasi tambahan (ubuntu + nginx + wordpress + file website perusahaan + konfigurasi php.ini yang sudah dimodifikasi sesuai keinginan)

Semua tergantung dari kebutuhan dan kasus kita masing-masing. Namun konsep utamanya adalah sebisa mungkin kita membuat image yang sekecil dan seefisien mungkin. Misalnya kita tidak perlu mengisi image kita dengan OS Ubuntu apabila kita hanya ingin menjalankan aplikasi webserver berbasis XAMPP, cukup gunakan image berisi layanan XAMPP saja.

Image ini akan disimpan di Registry, baik itu Registry lokal maupun Registry publik seperti Docker Hub.

# ***Container***

***Container*** adalah instance yang menjalankan image dalam bentuk sebuah proses. Kuncinya adalah ini. Container hanya akan menjadi sebuah proses, bukan sebuah server *Virtual Machine* tersendiri. Sehingga sifatnya seperti menjalankan aplikasi biasa. Seperti layaknya menjalankan Firefox di OS Windows.

Kita dapat menjalankan banyak *Container* untuk 1 buah image yang sama.

# ***Registry***

**Registry** merupakan tempat penyimpanan *Image* yang dapat berupa penyimpanan Publik maupun lokal. Siapapun bisa membuat Registry ini termasuk kita sendiri. Namun biasanya sudah sangat cukup menggunakan Re*g*istry publik seperti Docker Hub untuk memenuhi kebutuhan kita dalam menggunakan Docker sehari-hari.

Untuk pembelajaran kedepan, kalian wajib untuk mendaftar di Registry publik Docker Hub terlebih dahulu. Daftar melalui link berikut : ![https://hub.docker.com](https://hub.docker.com/)

# **Alur penggunaan Docker secara umum**

Secara umum berikut adalah alur cara kerja Docker :

1. Kita sebagai administrator mengeksekusi sebuah Command, dimana command ini akan disampaikan ke Docker *Host*.
2. Permintaan Docker *Client* (*command*) akan diperoses oleh Docker *Host* sesuai fungsinya masing-masing (melalui jasa Docker *Daemon*).
3. Kita dapat mengambil *image* dari *Registry* maupun menyimpannya kembali ke *Registry*.
4. Setiap Container akan menjalankan image yang sudah diambil tadi.
5. *User* (atau *Container* lainnya) dapat menikmati layanan dari *Container* yang dijalankan tsb. Misalnya *container* yang berisi Wordpress maka dapat benar-benar kita akses web wordpressnya, atau container yang berisi Database maka benar-benar bisa kita isi *database* di dalamnya, dll.

# **Komponen lainnya**

Sebenarnya ada komponen-komponen lainnya dari Docker seperti Docker *Machine*, Docker*Swarm*, namun itu akan kita pelajari di materi-materi berikutnya agar tidak terlalu banyak informasi yang perlu dicerna.