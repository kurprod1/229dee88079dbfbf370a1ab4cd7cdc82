# 17. Push ke Docker Hub

Created: July 5, 2022 10:51 AM

Untuk melakukan push ke Docker Hub, seperti biasa kita harus mengubah tagging image ini menjadi format :

`<nama user di Docker hub>/<nama image>:<tag>`

Berikut adalah contohnya (disini kita menggunakan tag latest saja) :

```bash
$ docker image tag nginx-custom:latest cilsy/nginx-custom:latest
```

Setelah sudah diubah tagnya, langsung lakukan push dengan perintah berikut :

```bash
$ docker image push cilsy/nginx-custom
```

![https://lh6.googleusercontent.com/2PTAUSK9JFooJXm7ZYA_SkEF1LBVFL9t9Umi-cYFDy35YYKxSvtUij8ehdnITUcxMJP78TkTLPzUOfmqRMUAbN9kAA0a4CfJogLuxVn3-jt2k4ysORskPc48rz2gfYjWgI-qTdmAbfLWe6VHjw](https://lh6.googleusercontent.com/2PTAUSK9JFooJXm7ZYA_SkEF1LBVFL9t9Umi-cYFDy35YYKxSvtUij8ehdnITUcxMJP78TkTLPzUOfmqRMUAbN9kAA0a4CfJogLuxVn3-jt2k4ysORskPc48rz2gfYjWgI-qTdmAbfLWe6VHjw)

Sampai tahap ini seharusnya image anda sudah masuk ke Docker Hub. Sebagai testing, kita akan coba menghapus image nginx-custom dari local untuk nantinya kita akan coba mengambil ulang image ini dari Docker Hub.

Pertama-tama kita coba hapus terlebih dahulu image nginx-custom dari local :

```bash
$ docker image rm cilsy/nginx-custom
$ docker image rm nginx-custom
```

Setelah itu kita coba jalankan container menggunakan image ini, tapi dengan langsung pull ulang image ini dari Docker Hub :

```bash
$ docker container run -p 80:80 --rm cilsy/nginx-custom
```

![https://lh4.googleusercontent.com/wtg08UsM9uNX7nxC3jsXeLGJhvamUBeJGGl9seTdPx8-RVlznhP6zGJ0xBhII0oegvKErFYy9HT_V7MNWdOa1dpgGDlUKEbHzy3OgXxjXVfyvypEtDS5MVtE8i2sFfVNZBdUrnlhGQN8lH-2Bg](https://lh4.googleusercontent.com/wtg08UsM9uNX7nxC3jsXeLGJhvamUBeJGGl9seTdPx8-RVlznhP6zGJ0xBhII0oegvKErFYy9HT_V7MNWdOa1dpgGDlUKEbHzy3OgXxjXVfyvypEtDS5MVtE8i2sFfVNZBdUrnlhGQN8lH-2Bg)

Anda bisa coba lihat bagian yang ditandai merah, bahwa image cilsy/nginx-custom sudah tidak dapat ditemukan di local dan Docker akan mengambilnya dari Docker Hub.  Setelah running, pastikan ketika Anda test di browser, container ini tetap membuka halaman custom nginx seperti sebelumnya.