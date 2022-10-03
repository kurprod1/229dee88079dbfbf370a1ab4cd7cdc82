# 15. Kubernetes ConfigMap

Created: July 11, 2022 2:22 PM

Banyak aplikasi memerlukan konfigurasi melalui beberapa kombinasi file config, argumen baris perintah, dan environment variable. Artefak konfigurasi ini harus dipisahkan dari konten image agar aplikasi yang dipaketkan tetap portabel. API ConfigMap menyediakan mekanisme untuk memasukan data konfigurasi ke kontainer sambil tetap menyimpan agnostik container di kubernetes. ConfigMap dapat digunakan untuk menyimpan informasi seperti properti individu atau informasi seluruh file konfigurasi atau JSON.

API ConfigMap menyimpan pasangan key-value yang dapat digunakan dalam pod atau digunakan untuk menyimpan data konfigurasi untuk komponen sistem seperti pengontrol. ConfigMap mirip dengan Secret, tetapi dirancang untuk lebih mendukung kerja dengan string yang tidak mengandung informasi sensitif.

Catatan: ConfigMap tidak dimaksudkan untuk bertindak sebagai pengganti file properti. ConfigMap dimaksudkan untuk bertindak sebagai referensi ke beberapa file properti. Bahasa lainnya dapat dianggap sebagai cara untuk merepresentasikan sesuatu yang mirip dengan direktori / etc, dan file-file di dalamnya, pada komputer Linux. Salah satu contoh model ini adalah membuat Volume Kubernetes dari ConfigMap, di mana setiap item data dalam ConfigMap menjadi file baru.

# **Persiapan Umum**

Kita akan tetap menggunakan [repo social media](https://github.com/sdcilsy/sosial-media). Namun bedanya, kita tidak mengubah file config.php tapi akan mengganti isi config.php dengan configmap.

Untuk persiapan pod, kita sudah menyiapkan image php-sosmed dan mysql-sosmed yang nantinya akan digunakan pada langkah selanjutnya.

Pada kali ini teman teman memerlukan kubernetes cluster yang dapat dibuat menggunakan kops atau kubeadm pada AWS. Cara membuat cluster kubernetes sudah di jelaskan pada sebelumnya**.** Silahkan teman teman baca kembali. Jika sudah, teman teman bisa melanjutkan ke langkah selanjutnya.

# **Membuat ConfigMap**

Buat sebuah configmap dengan nama **p-fb-configmap.yaml** lalu masukan konfigurasi berikut

```bash
apiVersion: v1
kind: ConfigMap
metadata:
  name: p-fb-configmap
  labels:
    app: pesbuk
data:
  config.php: |
    <?php
    $db_host = "php-pesbuk";
    $db_user = "devopscilsy";
    $db_pass = "1234567890";
    $db_name = "dbsosmed";
    try {    
      //create PDO connection
      $db = new PDO("mysql:host=$db_host;dbname=$db_name", $db_user, $db_pass);
    } catch(PDOException $e) {
      //show error
      die("Terjadi masalah: " . $e->getMessage());
    }
    ?>
```

script dapat dilihat di [https://gist.github.com/sdcilsy/b02bf1e03645212e4bc7a75377398207](https://gist.github.com/sdcilsy/b02bf1e03645212e4bc7a75377398207)

Kita bisa mengeksekusi perintah berikut untuk membuat **configmap**

```bash
kubectl apply -f p-fb-configmap.yaml

configmap/p-fb-configmap created
```

# ***Mengatur YAML Pod Pesbuk***

Lakukan konfigurasi pada bagian env pada p-fb-pod.yml dengan isi konfigurasi sebagai berikut

```bash
apiVersion: v1
kind: Pod
metadata:
  name: php-pesbuk
  labels:
    app: pesbuk
spec:
  volumes:
    - name: config-fb
      configMap:
        name: p-fb-configmap
    
  containers:
  - name: php-sosmed
    image: sekolahdevopscilsy/php-sosmed
    ports:
    - containerPort: 80
    volumeMounts:
    - name: config-fb
      mountPath: "/var/www/html/config.php"
      subPath: "config.php"
  
  - name: mysql-sosmed
    image: sekolahdevopscilsy/mysql-sosmed
    ports:
    - containerPort: 3306
    env:
      - name: MYSQL_ROOT_PASSWORD 
        value: "1234567890"
```

script dapat dilihat di [https://gist.github.com/sdcilsy/bbb6472895f9c49fe40f87fe36928dcf](https://gist.github.com/sdcilsy/bbb6472895f9c49fe40f87fe36928dcf)

Kita bisa mengeksekusi perintah berikut untuk membuat **pod**

```bash
kubectl apply -f p-fb-pod.yaml

pod/php-pesbuk created
```

Setelah itu kita akan membuat service agar pod php-pesbuk dapat diakses dari luar cluster menggunakan NodePort.

Kita dapat membuat service dengan file **p-fb-service.yaml** berikut.

```bash
apiVersion: v1
kind: Service
metadata:
  name: pesbuk-service
spec:
  selector:
    app: pesbuk
  type: NodePort
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 80
```

Script dapat dilihat di :

[https://gist.github.com/sdcilsy/5a81c2cd5677522edbf63c9b05220cc6](https://gist.github.com/sdcilsy/5a81c2cd5677522edbf63c9b05220cc6)

```bash
kubectl -f p-fb-service.yaml

service/pesbuk-service created
```

Service tersebut akan mengekspos pod yang listen pada port 80 dan mengarahkannya pada port 8080. Kita dapat lihat service yang dibuat dengan perintah berikut.

```bash
kubectl get svc
```

![https://lh3.googleusercontent.com/WJ7vV8bxFsGPTysivpTmoY5Ir-3MyaC5YoOHujoVapSrQqsCQ6rFprvt14yD4blIybAF911STu7udhUWHSAVZq9aAd3Z-nDxrO9nn2rUbgqifr83j_xDDH7bTZlJHv8ruvneuD8GTsUaDwoR3g](https://lh3.googleusercontent.com/WJ7vV8bxFsGPTysivpTmoY5Ir-3MyaC5YoOHujoVapSrQqsCQ6rFprvt14yD4blIybAF911STu7udhUWHSAVZq9aAd3Z-nDxrO9nn2rUbgqifr83j_xDDH7bTZlJHv8ruvneuD8GTsUaDwoR3g)

Bisa kita lihat, sekarang service **pesbuk-service** sudah memiliki port nat (**32171**) yang dapat kita akses. Namun service tersebut belum dapat kita akses karena policy inbound pada AWS belum mengizinkan port tersebut. Oleh karena itu kita akan membuat rule tambahan pada AWS.

Pertama kita masuk ke menu **Security Group**. Lalu pilih security group dengan nama **master.<nama cluster>** setelah itu klik **Edit inbound rules**.

[https://lh4.googleusercontent.com/oiQqrVF8WfqOEjvNAmzYELyzZ4Gq6crZ4-uIJNxBKWMSvIZbrJfKAwiVttgyh9EH5TkIoqngL2jDgBaPwjDWI410KeTpK2NzEd1yLIyU8uvMCQ3TqD9BIawkwv8On1eJpcis0QflAzvd91sn_g](https://lh4.googleusercontent.com/oiQqrVF8WfqOEjvNAmzYELyzZ4Gq6crZ4-uIJNxBKWMSvIZbrJfKAwiVttgyh9EH5TkIoqngL2jDgBaPwjDWI410KeTpK2NzEd1yLIyU8uvMCQ3TqD9BIawkwv8On1eJpcis0QflAzvd91sn_g)

Setelah itu kita buka port range **30000-32767** dengan type **Custom** **TCP** yang merupakan [default port nat kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#type-nodeport). Kita akan izinkan sourcenya dari **anywhere.**

![https://lh4.googleusercontent.com/TyHTKB9wPPzXT9Y82DWyI45RHn3RInw7ryzGq03yHNK1QMjmA_vmZHAcUlzSdTCNtEtad3GupPTLv8YjbSiayKmr9iKADb6mm59bl8HGxTgGwO-ReCfrY6WVHaHyoeHxoweyN4lGtdI-gRqo6A](https://lh4.googleusercontent.com/TyHTKB9wPPzXT9Y82DWyI45RHn3RInw7ryzGq03yHNK1QMjmA_vmZHAcUlzSdTCNtEtad3GupPTLv8YjbSiayKmr9iKADb6mm59bl8HGxTgGwO-ReCfrY6WVHaHyoeHxoweyN4lGtdI-gRqo6A)

Untuk pengujian, kita bisa akses IP/DNS instance **master** dengan port nat pada service (**32171**) pada browser.

![https://lh3.googleusercontent.com/tVUGMcd1l09JO1uFhCS8Bb5-pYmI-IKStQ74Vl0Acr-L-8gRK8kHdc2BT-hWFVL5oG-fm_N_Qpv0hdpKltvdMO4BkviwvIigVpZPQpQZG1vWQtZr6q7bc60-pPtaeLjEjfSx3YP_CKTafo4y4g](https://lh3.googleusercontent.com/tVUGMcd1l09JO1uFhCS8Bb5-pYmI-IKStQ74Vl0Acr-L-8gRK8kHdc2BT-hWFVL5oG-fm_N_Qpv0hdpKltvdMO4BkviwvIigVpZPQpQZG1vWQtZr6q7bc60-pPtaeLjEjfSx3YP_CKTafo4y4g)

Cobalah untuk **daftar** untuk melihat apakah koneksi ke mysql dapat berjalan ?