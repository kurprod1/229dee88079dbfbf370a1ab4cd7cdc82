# 17. Membuat Automasi Setup Webserver dengan Bash

Created: June 27, 2022 3:25 PM

# **Automasi installasi webserver**

Pada beberapa bagian sebelumnya kita sudah mempelajari bagaimana kita melakukan installasi webserver dan juga setup web aplikasi, begitupun dengan pemrograman dasar menggunakan bahasa pemrograman bash yang ada pada linux.

Pada bagian ini kita akan menyatukan kedua hal yang sudah kita pelajari, jika sebelumnya kita sudah melakukan installasi webserver secara manual, sekarang kita akan coba lakukan installasi webserver secara otomatis menggunakan bash script.

Tujuan dari dibuatnya script automasi ini adalah untuk mempermudah kita pada saat membuat project baru yang menggunakan environment sistem yang masih sama. Kita tidak perlu lama mengetikan apa saja yang harus kita install, kita hanya perlu menjalankan satu script sehingga environment yang kita butuhkan sudah otomatis terbentuk.

```bash
#!/bin/bash
 
jawaban="Y"
 
read -p "Apakah kamu yakin akan menginstall webserver ? (Y/n) " pilih;
 
if [ $pilih == $jawaban ];
then
    echo "Menyiapkan Installasi Web server"
    sudo apt-get update
    echo "Melakukan Installasi Webserver"
    sudo apt-get install -y apache2 php php-mysql
    echo "Melakukan Installasi Database Server"
    sudo apt-get install -y mysql-server
    echo "Installasi Selesai"
    exit 0
else
    echo "Installasi dibatalkan"
    exit 1
fi
```

Script diatas akan memberikan pilihan kepada kita untuk menjalankan installasi atau tidak dengan memberikan perintah Y untuk ya dan n untuk tidak. Apabila kita memilih ya maka script tersebut akan menjalankan perintah untuk menginstall apache, php, dan mysql. Jika aplikasi sudah terinstall dikomputer kita, maka akan muncul seperti dibawah ini.

![*Proses installasi menggunakan script bash*](https://lh6.googleusercontent.com/p4qYjd252InlXWHrFImGLH9cbTzDGGYIQvN9nQ1C-G0-cUcj7l8u-ZrJj3P4CxiXsQqovAY5aVt1kJYqHtFYb2vtTF3odwiSwjT8d74II4Urfpkq-_sk6oTjR_00Rf9hdfrZCc-r5IvBRWA3AA)

*Proses installasi menggunakan script bash*

# **Automasi Setup Web Aplikasi**

Selain melakukan automasi untuk installasi webserver, kita juga dapat melakukan automasi untuk setup web aplikasi menggunakan bash script. Berikut merupakan salah satu contoh script automasinya.

```bash
#!/bin/bash
 
jawaban="Y"
 
read -p "Apakah kamu yakin akan melakukan setup Aplikasi Web ? (Y/n) " pilih;
 
if [ $pilih == $jawaban ];
then
    echo "=============================>"
    echo "Downloading Data"
    echo "=============================>"
    cd
    wget https://github.com/sdcilsy/sosial-media/archive/master.zip
    echo "=============================>"
    echo "Ekstrak File"
    echo "=============================>"
    unzip master.zip
    echo "=============================>"
    echo "Memindahkan data"
    echo "=============================>"
    sudo rm /var/www/html/*
    sudo rm -R /var/www/html/*
    sudo mv sosial-media-master/* /var/www/html
    echo "Setup selesai"
    exit 0
else
    echo "Setup dibatalkan"
    exit 1
fi
```

Dengan begini semua data yang ada pada direktori /var/www/html akan di replace oleh aplikasi baru yang sudah kita dowload. Kita juga dapat menambahkan beberapa setup untuk membuat database mysql didalamnya.

Apabila pada saat program diatas dijalankan mucul log seperti dibawah ini maka biarkan, karena memang direktory sudah terhapus.

*Hasil setup web aplikasi*

![https://lh4.googleusercontent.com/x0VtX-zm0AER155Mku3ZjceNnI6LJFJJ8DyM9K1tXsJFqhOXdVMTbYWMLTT802zWFZ40j7TAQ62aSNYaBtnBNdIJd9tv7SqfEWjikQBtyMcKW316Pl8LGGQsFFNLG2cXX2hKgFY_ZatqWYopgw](https://lh4.googleusercontent.com/x0VtX-zm0AER155Mku3ZjceNnI6LJFJJ8DyM9K1tXsJFqhOXdVMTbYWMLTT802zWFZ40j7TAQ62aSNYaBtnBNdIJd9tv7SqfEWjikQBtyMcKW316Pl8LGGQsFFNLG2cXX2hKgFY_ZatqWYopgw)

Dengan begini kita sudah bisa menyiapkan environment server local dengan mudah, hanya dengan menggunakan satu script yang sudah dibuat kita bisa menjalankan beberapa layanan yang akan kita gunakan. Selain itu kita juga tidak perlu susah untuk melakukan setup web aplikasi karena kita bisa melakukannnya secara otomatis.

# **Exercise**

1. Buatlah sebuah script bash yang bisa menghapus semua layanan webserver secara sekaligus seperti layanan apache, php, dan database mysql.