# 11. Whats inside Docker Image?

Created: July 5, 2022 10:00 AM

Image seperti yang sudah dibahas pada materi sebelumnya adalah aplikasi yang ingin kita jalankan. Tapi sebenarnya terbuat dari apa image ini?

Apa saja yang ada di dalam Image :

1. Binary dan dependensi aplikasi. Seperti file-file konfigurasi .conf, file executable .sh dari aplikasi.
2. Metadata terkait bagaimana image tersebut akan dijalankan.

Image bukanlah template OS seperti file ISO sehingga Image tidak memiliki :

1. Kernel OS
2. Driver Module
3. Dan modul-modul lainnya yang terkait hardware.

Akibatnya Image dapat berukuran super kecil berupa sebuah library saja, maupun super besar (bergiga-giga) berupa distro lengkap dengan aplikasi-aplikasi didalamnya seperti Ubuntu + Wordpress + Mysql.

Berikutnya kita akan banyak membahas lebih detail tentang hal-hal yang berkaitan dengan image, bagaimana konsep image bekerja, dan manajemen-manajemen yang bisa kita lakukan seputar image.