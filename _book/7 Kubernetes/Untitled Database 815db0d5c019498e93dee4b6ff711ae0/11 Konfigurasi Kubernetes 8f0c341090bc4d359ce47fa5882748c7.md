# 11. Konfigurasi Kubernetes

Created: July 7, 2022 2:15 PM

# **File Yaml**

File yaml berguna untuk mengatur cluster pada kubernetes. dengan file yaml kita dapat melakukan pengaturan dengan mudah pada cluster kubernetes yang telah kita buat sebelum nya adapun kelebihan menggunakan file yaml adalah sebagai berikut.

1. Kemudahan, kita di berikan kemudahan dalam konfigurasi sistem dengan hanya membuat file dan menuliskan kode perubahan maka cluster kubernetes dapat berubah dengan cepat You’ll no longer have to add all of your parameters to the command line.
2. Maintenance, menggunakan file YAML dapat memaintenance cluster dengan mudah, jika ada perubahan pun akan mudah di cari, berdasarkan perubahan pada file yaml.
3. Flexibility, kita dapat membuat struktur dari kubernetes yang komplex hanya dengan menggunakan file yaml dan di jalankan dengan satu baris command line.

Sebagai contoh kita akan coba untuk membuat sebuah file YAML pada kubernetes, berikut merupakan scriptnya dan simpan dengan nama  pod.yaml.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: rss
  labels:
    app: web
spec:
  containers:
    - name: front-end
      image: nginx
      ports:
      - containerPort: 80
    - name: rss-reader
      image: nginx:latest
      ports:
      - containerPort: 88
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/60a3ab47925a46053040afb9a5d6dc76](https://gist.github.com/sdcilsy/60a3ab47925a46053040afb9a5d6dc76)

Setelah file disimpan, kita bisa menjalankannya dengan perintah berikut.

```yaml
kubectl create -f pod.yaml
```

# **Setting Deployment dengan YAML**

Untuk menjalankan aplikasi maka kita harus mendeploy aplikasi tersebut ke dalam cluster kubernetes, untuk mendeploy kita dapat menggunakan file yaml.

Untuk melakukan deployment kita bisa membuat sebuah file Yaml yang kurang lebih seperti script di bawah ini. Script tersebut digunakan untuk mendeploy nginx ke dalam cluster kubernetes. Simpan dengan nama **deployment.yaml.**

```yaml
apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2        # tells deployment to run 2 pods matching the template
  template:          # create pods using pod definition in this template
    metadata:
# unlike pod-nginx.yaml, the name is not included in the meta data as a unique name is
# generated from the deployment name
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

script dapat dilihat di [https://gist.github.com/sdcilsy/eed87e5f30dac05f151fd96acd8bbedf](https://gist.github.com/sdcilsy/eed87e5f30dac05f151fd96acd8bbedf)

Setelah itu simpan, lalu jalankan script yang sudah kita buat barusan.

```yaml
kubectl create -f deployment.yaml
```

Jika kita ingin melakukan perubahan misal images docker kita ubah dari nginx:1.7.9 menjadi nginx:latest, kita bisa buat file YAML menggunakan script dibawah ini.

```yaml
apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2        # tells deployment to run 2 pods matching the template
  template:          # create pods using pod definition in this template
    metadata:
# unlike pod-nginx.yaml, the name is not included in the meta data as a unique name is
# generated from the deployment name
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/d78df0ab2de4df1e79db77fa19a6923e](https://gist.github.com/sdcilsy/d78df0ab2de4df1e79db77fa19a6923e)

Setelah disimpan, jalankan konfigurasi berikut.

```yaml
kubectl apply -f deployment.yaml
```

Baiklah kita telah berhasil mendeploy nginx kedalam cluster kubernetes, namun nginx belum dapat kita akses karena kita belum membuat service pada kubernetes untuk nginx. Maka dari itu kita harus melakukan konfigurasi service agar nginx bisa diakses.

# **Setting Service**

Pada tahap ini kita akan melakukan konfigurasi service pada kubernetes dengan file yaml, berikut merupakan script file YAML yang dapat kita buat. Simpan file dengan nama **service.yaml.**

```yaml
apiVersion: apps/v1beta2
kind: Service
apiVersion: v1
metadata:
  name: nginx
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```

script dapat dilihat di [https://gist.github.com/sdcilsy/854a1d803cdbf632dbcdd686bddaeced](https://gist.github.com/sdcilsy/854a1d803cdbf632dbcdd686bddaeced)

Setelah selesai kita simpan, lalu jalankan script berikut.

```yaml
kubectl create -f service.yaml
```

Jika ingin mengupdate script maka kita dapat menggunakan perintah berikut.

```yaml
kubectl apply -f service.yaml
```

Setelah semua kita konfigurasi, sekarang kita dapat masuk ke halaman menu service pada dashboard akan muncul nginx seperti di bawah ini.

[https://lh6.googleusercontent.com/z-tpwEg1RzGaDxT4500sXR-LoNNSRsLsck4f-LBgGP939-L9rSjG30HZ-STYYBaRR4bPdXSZ0R05lW05j4yGUjVp3r604K5tMtCEK4Qe1eEM18M68G7JJKhqD62UjmJh5ycCgW1LR6J6sEj2eA](https://lh6.googleusercontent.com/z-tpwEg1RzGaDxT4500sXR-LoNNSRsLsck4f-LBgGP939-L9rSjG30HZ-STYYBaRR4bPdXSZ0R05lW05j4yGUjVp3r604K5tMtCEK4Qe1eEM18M68G7JJKhqD62UjmJh5ycCgW1LR6J6sEj2eA)

Pada menus service kita dapat mengakses dengan eksternal endpoint. Jika kita akses maka akan muncul seperti di bawah ini

[*Hasil Deployment nginx*](https://lh6.googleusercontent.com/Wi_c5A4MDXA2gRBf2TjjeTM9JfreU4GRDx2L4NDke4pcb6n4oPIf0yBbltJ6XYgzQLf3cHUP1G2NYUCfXb6ZtsvV3K6rcNo465yO80eRSzIkWVJ3OpBb1yMbp0c4uWjG3jb8vOtNLXUD0NG_5g)

*Hasil Deployment nginx*

# **Deployment Wordpress**

Pada bagian ini kita akan coba melakukan deployment wordpress pada kubernetes, database yang digunakan pada wordpress tersebut akan menggunakan database dari amazon RDS. Maka dari itu pertama kita siapkan sebuah databse mysql di Amazon RDS.

Setelah itu buat sebuah file **wordpress.yaml** dengan script berikut.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  ports:
    - port: 80
  selector:
    app: wordpress
    tier: frontend
  type: LoadBalancer
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: wp-pv-claim
  labels:
    app: wordpress
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 20Gi
---
apiVersion: apps/v1beta2 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  selector:
    matchLabels:
      app: wordpress
      tier: frontend
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: wordpress
        tier: frontend
    spec:
      containers:
      - image: wordpress:4.8-apache
        name: wordpress
        ports:
        - containerPort: 80
          name: wordpress
```

script dapat dilihat di [https://gist.github.com/sdcilsy/df9f67f843491367e8c7e1ce58d2dc9b](https://gist.github.com/sdcilsy/df9f67f843491367e8c7e1ce58d2dc9b)

Setelah itu deploy dengan menggunakan perintah berikut.

```yaml
kubectl create -f wordpress.yaml
```

Jika berhasil, maka hasilnya dapat kita lihat pada dashboard console kubernetes bagian deployment seperti berikut.

Masuk pada bagian service dan kalian dapat melihat bagian endpoint pada wordpress yang sudah kalian deploykan.

[https://lh5.googleusercontent.com/E-aKqL35-u1WQ9k6VVC2Yiv32GGSDaGO3bG5NYWYVABcpkGLaiqj0KARgJfivNI3i9D55xcnO0-VyvMDOvPgUW6Sh6VewWBA6VOw74YBggDVBk7g5AN4JfidKdpxJ3eqlaunTBJodxsu6zdz_A](https://lh5.googleusercontent.com/E-aKqL35-u1WQ9k6VVC2Yiv32GGSDaGO3bG5NYWYVABcpkGLaiqj0KARgJfivNI3i9D55xcnO0-VyvMDOvPgUW6Sh6VewWBA6VOw74YBggDVBk7g5AN4JfidKdpxJ3eqlaunTBJodxsu6zdz_A)

Klik alamat endpoint tersebut, lalu lakukan setup pada wordpress dengan mengarahkan database pada amazon RDS yang kalian sudah buat sebelumnya. Kalian seharusnya sudah dapat melakukan setup RDS seperti yang sudah dipelajari sebelumnya.

[*Wordpress pada kubernetes*](https://lh4.googleusercontent.com/iHYSeF5eXa_mUJZvY_wOnaK-sU0FqmvUuf01eBNXywnC28adpROoGuGcPv0U4DvAeHiGwPYqH0a--Uc4zD6Dpuw9mF46gGIz_Fkl-0H2eWn5omoPo8SF_be6ZWKItKv4KZbLIu18Kzl2OvnzkQ)

*Wordpress pada kubernetes*

# **Excercise**

Soal Praktek :

1. Lakukan Deployment Drupal menggunakan database Amazon RDS.
2. Jalankan hingga dapat kalian akses melalui endpoint public.
3. Cari referensi yang dapat kalian gunakan untuk menginstall drupal pada kubernetes.