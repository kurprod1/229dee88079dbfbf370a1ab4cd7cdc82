# 18. Docker Compose

Created: July 5, 2022 10:53 AM

# **Apa itu docker-compose ?**

Compose adalah tool untuk mendefinisikan dan menjalankan aplikasi multi container. Dengan Compose, kita menggunakan file YAML untuk mengonfigurasi service aplikasi. Kemudian, dengan satu perintah, Anda membuat dan memulai semua layanan dari konfigurasi Anda.

Singkatnya, Compose menghandle applikasi yang menjalankan beberapa container sekaligus. Misalnya kita memiliki aplikasi **Wordpress**. Aplikasi ini berjalan dengan **MySQL**. Dengan menggunakan compose, kita bisa mendefinisikan kedua container ini bersamaan di file YAML yang sama.

Compose bisa digunakan di skala development, staging, production, testing, dan juga CI workflow.

Sebetulnya, penggunaan Compose ini dirangkum dengan 3 step berikut :

- Tentukan **Dockerfile** sebagai **environment** applikasi yang akan dibuat sehingga dapat direproduksi di mana saja.
- Tentukan layanan yang membentuk aplikasi di **docker-compose.yml**.
- Jalankan perintah **docker-compose up** untuk menjalankan aplikasi.

# **Installation**

Docker-compose secara default tidak terinstal bersama docker. Oleh karena itu kita harus menginstal secara manual docker-compose ini.

Kita bisa menemukan dokumentasi untuk instalasi docker-compose ini [disini](https://docs.docker.com/compose/install/#install-compose).

Berikut cara menginstal compose pada linux.

Pada kali ini, versi stable dari compose adalah **1.29.2**.

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-
```

setelah itu tambahkan permission agar compose bisa executable

```bash
sudo chmod +x /usr/local/bin/docker-compose
```

apabila docker-compose tidak muncul, atau tidak bisa dieksekusi, kita bisa buat symlink ke salah satu directory PATH.

```bash
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

kita jalankan perintah **docker-compose version** untuk melihat compose sudah terinstal.

[https://lh5.googleusercontent.com/We16RLqHxby83VPs5aBJJ4AsZaKM3UlYqy0AEPQraSbIe7DpSI4oP4xG4qxvFxWSXVJ8Gjka9jeGvET7RmjBH5YgUGOUzJ_aA8OwJ1UEnwoH9T_tv3Lp0DQQeVRvodvqtNzlPyf7MSrJ7-ZB-Q](https://lh5.googleusercontent.com/We16RLqHxby83VPs5aBJJ4AsZaKM3UlYqy0AEPQraSbIe7DpSI4oP4xG4qxvFxWSXVJ8Gjka9jeGvET7RmjBH5YgUGOUzJ_aA8OwJ1UEnwoH9T_tv3Lp0DQQeVRvodvqtNzlPyf7MSrJ7-ZB-Q)

# **Docker-compose.yaml**

Compose menggunakan file **docker-compose.yaml** untuk membuat aplikasi.

Coba perhatikan contoh berikut.

```bash
version: "3.9"
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
      - logvolume01:/var/log
    links:
      - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```

docker-compose.yaml tersebut berisi konfigurasi seperti berikut.

- Menggunakan compose file versi 3.9. Versi ini menentukan format untuk membuat resource di docker. Dokumentasinya ada [di sini](https://docs.docker.com/compose/compose-file/compose-versioning/).
- Membuat 2 service yaitu **web** dan **redis**.
- Pada service **web** akan membuat image dari **Dockerfile** yang ada di directory yang sama. Mengekspose port **5000**. Binding volume ke **/code** dan **/var/log**. Lalu membuat link ke service **redis**.
- Pada service redis akan menggunakan image **redis**.
- dan terakhir akan membuat volume **logvolume01**.

Seperti yang disebutkan diawal, kita bisa menggunakan Dockerfile untuk dijadikan sebagai service yang akan digunakan. Docker-compose secara otomatis akan membuat image dari Dockerfile.

Bisa kita lihat ada 2 service yang dibuat yaitu **web** dan **redis**. Nantinya service service ini akan dibuatkan network khusus agar kedua service dapat berkomunikasi satu sama lain.

Secara default, kita tidak membutuhkan **links** karena service yang dibuat menggunakan compose dapat berkomunikasi satu sama lain. Dalam kasus ini service web dan redis.

Setelah itu, kita bisa menjalankan aplikasi kita tadi, menggunakan perintah berikut.

```bash
docker-compose up -d
```

# **Environment Variable in Compose**

Ketika membangun suatu applikasi, kadang kalanya ktia membutuhkan environment variable entah itu untuk memasukan variable ke container yang akan dibuat atau agar mudah memaintain applikasi yang dibuat.

Banyak kegunaan dari environment variable contohnya adalah untuk menentukan versi image yang digunakan applikasi.

```bash
web:
  image: "webapp:${TAG}"
```

contoh diatas merupakan salah satunya. Service web akan menggunakan image webapp dengan versi yang ditentukan oleh variable **TAG**.

Ada beberapa cara untuk menampung environment variable pada docker.

- Membuat file **.env**
- membuat variable didalam container

# ***.env file***

Docker menyediakan sebuah file khusus untuk menampung environment variable yaitu **.env**. File ini bisa kita simpan di directory yang sama dengan **docker-compose.yaml** atau di directory lain.

Misalnya kita buat sebuah file **.env** dengan isi berikut.

```bash
TAG=1.5
```

nah setelah itu, ketika menjalankan aplikasi dengan perintah **docker-compose up**, dia akan membaca variable dari file .env tersebut dengan catatan file tersebut berada di directory yang sama dengan file **docker-compose.yaml**.

Namun apa jadinya jika kita mempunyai file .env di directory yang berbeda ?

Kita masih bisa menggunakannya namun dengan option **--env-file [directory]**.

Misalnya seperti berikut

```bash
docker-compose --env-file ./config/.env.dev up
```

# **Simple App with Compose**

Setelah memahami pengenalan tentang docker-compose, mari kita buat sebuah aplikasi sederhana menggunakan compose.

Kita akan membuat aplikasi web berbasis Python yang akan menampilkan berapa kali kita melihat laman. Aplikasi web ini dibangun dengan 2 service yaitu **web** dan **redis**.

## ***Setup***

Pertama, kita buat sebuah direktori untuk bekerja.

```bash
mkdir composetest
cd composetest
```

setelah itu kita buat sebuah file **app.py** dengan isi sebagai berikut.

```python
import time
 
import redis
from flask import Flask
 
app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)
 
def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)
 
@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/af74f4740e8fe0096b8c3f21ed1b2e7f#file-app-py](https://gist.github.com/sdcilsy/af74f4740e8fe0096b8c3f21ed1b2e7f#file-app-py)

setelah itu, kita buat file **requirements.txt** dengan isi sebagai berikut.

```python
flask
redis
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/af74f4740e8fe0096b8c3f21ed1b2e7f#file-requirements-txt](https://gist.github.com/sdcilsy/af74f4740e8fe0096b8c3f21ed1b2e7f#file-requirements-txt)

## ***Create a Dockerfile***

Kali ini kita akan membuat Dockerfile yang digunakan untuk membuat image untuk service web yang akan dibangun.

Buat file dengan nama Dockerfile dengan isi berikut.

```docker
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run"]
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/af74f4740e8fe0096b8c3f21ed1b2e7f#file-dockerfile](https://gist.github.com/sdcilsy/af74f4740e8fe0096b8c3f21ed1b2e7f#file-dockerfile)

Dockerfile ini akan membuat :

- Buat image yang dimulai dengan image Python 3.7.
- Set direktori ke /code.
- Tetapkan variabel lingkungan yang digunakan oleh perintah flask.
- Instal gcc dan dependensi lainnya
- Salin requirements.txt dan instal dependensi Python.
- Membuka port 5000
- Salin direktori saat ini. dalam proyek ke workdir . dalam image.
- Setel perintah default untuk container agar flask dijalankan.

## ***Define services in a Compose file***

Setelah membuat Dockerfile, kita akan buat service service di **docker-compose.yaml**

buat file bernama docker-compose.yaml lalu isikan seperti berikut.

```bash
version: "3.9"
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/af74f4740e8fe0096b8c3f21ed1b2e7f#file-docker-compose-yaml](https://gist.github.com/sdcilsy/af74f4740e8fe0096b8c3f21ed1b2e7f#file-docker-compose-yaml)

Sehingga direktori kita akan seperti ini.

[https://lh5.googleusercontent.com/eFavH04TXqrunprywubBo6AFfKxXZgRlVfTRaxeFKjLH9tf2kLagN5QTakJk9KOwyfs2u21a3XtKd_qfim2SoD6stTwgLthbMPidSV_qj1mr-3xXr6Qd73XcqvA1y6zi-SnHqOiw8paUz4JXAA](https://lh5.googleusercontent.com/eFavH04TXqrunprywubBo6AFfKxXZgRlVfTRaxeFKjLH9tf2kLagN5QTakJk9KOwyfs2u21a3XtKd_qfim2SoD6stTwgLthbMPidSV_qj1mr-3xXr6Qd73XcqvA1y6zi-SnHqOiw8paUz4JXAA)

## ***Build and run Apps***

Jalankan aplikasi menggunakan perintah berikut

```bash
docker-compose up -d
```

[https://lh3.googleusercontent.com/59z2VhFVnaOkcbewm81X806UQazRssA9qGKwEsZaaKX7t7xcBDU008amiKV7HvNSbKcGpZFqX3aOxKl04jb7we_J5Ve3HEUdbWfdIzr9WDUu8DtxmcBZpe8b-Cho9xzkJkVHeC0t-g4pEbO7FQ](https://lh3.googleusercontent.com/59z2VhFVnaOkcbewm81X806UQazRssA9qGKwEsZaaKX7t7xcBDU008amiKV7HvNSbKcGpZFqX3aOxKl04jb7we_J5Ve3HEUdbWfdIzr9WDUu8DtxmcBZpe8b-Cho9xzkJkVHeC0t-g4pEbO7FQ)

## ***Testing***

Untuk melakukan testing, kita bisa membuka browser untuk mengakses [http://localhost:5000](http://localhost:5000/)

[https://lh5.googleusercontent.com/DFfKT5H_GCXb5Z2qsAjiN4wtCYJi0xSgvb47wPuS0yqKLzBNhp9HI0dKBnoK-PvpPopJx0h-FRM9sW7dtdK4wlVH25eI6wNb7WWIJ0iVruSafvfkc010KjsC6ap3KuJYtcEYvF3kCJei0GrZVA](https://lh5.googleusercontent.com/DFfKT5H_GCXb5Z2qsAjiN4wtCYJi0xSgvb47wPuS0yqKLzBNhp9HI0dKBnoK-PvpPopJx0h-FRM9sW7dtdK4wlVH25eI6wNb7WWIJ0iVruSafvfkc010KjsC6ap3KuJYtcEYvF3kCJei0GrZVA)

Jika kita refresh halaman tersebut, maka akan berubah seperti berikut.

[https://lh3.googleusercontent.com/6BGLN7dx_Z2u54WUcdUlhBZumUYApB416M_n8ezBaHk4kwKmtRqgMkpE9HE6Hgd3D0aIDHAt-PoQiNTu_07LvbfFMcLdQZ03iMjShdi8c5vS0FAsc9m4dHBMeQtvXEon1zblzpTCpO94r_fBsg](https://lh3.googleusercontent.com/6BGLN7dx_Z2u54WUcdUlhBZumUYApB416M_n8ezBaHk4kwKmtRqgMkpE9HE6Hgd3D0aIDHAt-PoQiNTu_07LvbfFMcLdQZ03iMjShdi8c5vS0FAsc9m4dHBMeQtvXEon1zblzpTCpO94r_fBsg)

## ***Cleanup***

Untuk memberhentikan aplikasi, kita bisa menggunakan perintah berikut.

docker-compose down

[https://lh3.googleusercontent.com/eAC0V9QXbhJIXXy7pXPKauFBG6GDRipp6CQnzTgFzCZn2gQ91RLHu7pMIu4D7fvJ9W59gjeOh6XnNS-1xtvo9qLA4F_Zi5BzSuycUYkfX3nEMmlnk7hjPgxWa7cxk1fPTjAD8tYpR_i9XYKlZA](https://lh3.googleusercontent.com/eAC0V9QXbhJIXXy7pXPKauFBG6GDRipp6CQnzTgFzCZn2gQ91RLHu7pMIu4D7fvJ9W59gjeOh6XnNS-1xtvo9qLA4F_Zi5BzSuycUYkfX3nEMmlnk7hjPgxWa7cxk1fPTjAD8tYpR_i9XYKlZA)