# 16. Kubernetes Secret

Created: July 11, 2022 2:25 PM

Kubernetes secret adalah objek yang berisi data data sensitif seperti password, token, atau key. Informasi tersebut mungkin dapat dimasukkan ke dalam spesifikasi Pod atau dalam image container. Menggunakan secret berarti tidak perlu menyertakan data sensitif dalam kode aplikasi secara eksplisit.

Secret mirip dengan ConfigMap tetapi secara penggunaan dikhususkan untuk menyimpan data rahasia.

# **Membuat Secret Menggunakan Kubectl**

Sebelum kita akan membuat Secret di *workspace* dengan menggunakan perintah berikut :

```bash
echo -n 'admin' > ./username.txtecho -n '1f2d1e2e67df' > ./password.txt
```

Selanjutnya inputkan password yang akan kita buat dengan perintah berikut :

```bash
kubectl create secret generic db-user-pass --from-file=./username.txt -from-file=./password.txt
```

Setelah memasukan perintah diatas output yang akan dihasilkan seperti berikut :

```bash
secret "db-user-pass" created
```

Selanjutnya masukan perintah berikut untuk memeriksa Secret yang sudah ada :

```bash
kubectl get secrets
```

*Output* yang dihasilkan seperti berikut :

```bash
NAME                  TYPE                                  DATA      AGE
db-user-pass          Opaque                                2         51s
```

bahkan kita bisa melihat detail secret yang sudah ada dengan menggunakan perintah berikut :

```bash
kubectl describe secrets/db-user-pass
```

Maka *output* yang dihasilkan dari perintah diatas sebagai berikut :

```bash
Name:            db-user-pass
Namespace:       default
Labels:          <none>
Annotations:     <none>

Type:            Opaque

Data
====
password.txt:    12 bytes
username.txt:    5 bytes
```

# **Membuat *Secret* secara *Manual***

kita akan membuat user pada workspace dengan menggunakan perintah beritkut:

```bash
echo -n 'admin' | base64
```

*Output* dari perintah diatas sebagai berikut :

```bash
YWRtaW4=
```

Setelah membuat *user* selanjutnya kita akan membuat *password* dengan mamasukan perintah berikut :

```bash
echo -n '1f2d1e2e67df' | base64
```

*Output* dari perintah diatas sebagai berikut :

```bash
MWYyZDFlMmU2N2Rm
```

Buat sebuah file dengan nama p-secret.yaml yang isinya sebagai berikut:

```bash
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  username: YWRtaW4=
  password: MWYyZDFlMmU2N2Rm
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/9c7ba0f35c23a656fb7563389c72fbae](https://gist.github.com/sdcilsy/9c7ba0f35c23a656fb7563389c72fbae)

Lakukan kubectl apply dengan menggunakan perintah berikut :

```bash
kubectl apply -f ./secret.yaml

secret/mysecret created
```

# **Menggunakan *Secret* pada *File***

Pada praktek ini, kita akan menggunakan repo facebook dengan kredensial **config.php** seperti username dan password, kita masukan kedalam Secret Kubernetes

Kita akan memasukan **username** dan **password** dari mysql kedalam bentuk **base64**. Nantinya, secara otomatis, kubernetes akan mendekripsi username dan password ini menjadi **plain text**.

```bash
echo -n 'devopscilsy' | base64ZGV2b3BzY2lsc3k=
echo -n '1234567890' | base64MTIzNDU2Nzg5MA==
```

Buat *file secret* p-fb-secret.yaml Isi *data* sesuai output pada langkah sebelumnya

```bash
apiVersion: v1
kind: Secret
metadata:
  name: p-secret-fb
  labels:
    app: pesbuk-secret
type: Opaque
data:
  DB_USER: ZGV2b3BzY2lsc3k=
  DB_PASS: MTIzNDU2Nzg5MA==
  MYSQL_ROOT_PASSWORD: MTIzNDU2Nzg5MA==
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/8adc7917ab18916a7f4da2b844200d17](https://gist.github.com/sdcilsy/8adc7917ab18916a7f4da2b844200d17)

Lalu kita bisa mengeksekusi perintah berikut untuk membuat **Secret**

```bash
kubectl apply -f secret.yaml

secret/p-secret-fb created
```

Selanjutnya kita membuat **configmap** file config.php bernama **p-fb-configmap.yaml**. Ubah beberapa variabel seperti **host**, **username**, **password**, dan kita arahkan untuk mengambil ke **variabel environment**.

```bash
apiVersion: v1
kind: ConfigMap
metadata:
  name: p-fb-configmap-secret
  labels:
    app: pesbuk-secret
data:
  config.php: |
    <?php
    $db_host = getenv("DB_HOST");
    $db_user = getenv("DB_USER");
    $db_pass = getenv("DB_PASS");
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

script dapat dilihat di

[https://gist.github.com/sdcilsy/beb8123fb9a8098342dc3f07d36abef3](https://gist.github.com/sdcilsy/beb8123fb9a8098342dc3f07d36abef3)

# ***Mengatur YML Pod Facebook***

Kita akan melakukan pengaturan pada bagian env dibagian p-fb-secret-pod.yml

```bash
apiVersion: v1
kind: Pod
metadata:
  name: php-pesbuk-secret
  labels:
    app: pesbuk-secret
spec:
  volumes:
    - name: config-secret
      configMap:
        name: p-fb-configmap-secret

  containers:
  - name: php-sosmed
    image: sekolahdevopscilsy/php-sosmed
    ports:
    - containerPort: 80
    volumeMounts:
    - name: config-secret
      mountPath: "/var/www/html/config.php"
      subPath: "config.php"
    env:
    - name: DB_HOST
      value: "php-pesbuk-secret"
    - name: DB_USER
      valueFrom:
        secretKeyRef:
          name: p-secret-fb
          key: DB_USER
    - name: DB_PASS
      valueFrom:
        secretKeyRef:
          name: p-secret-fb
          key: DB_PASS

  - name: mysql-sosmed
    image: sekolahdevopscilsy/mysql-sosmed
    ports:
    - containerPort: 3306
    env:
    - name: MYSQL_ROOT_PASSWORD
      valueFrom:
        secretKeyRef:
          name: p-secret-fb
          key: MYSQL_ROOT_PASSWORD
```

script dapat dilihat di [https://gist.github.com/sdcilsy/99dfd1c2c98fa3a36e4275f03552a633](https://gist.github.com/sdcilsy/99dfd1c2c98fa3a36e4275f03552a633)

Lakukan deployment pada  p-fb-pod.yaml dengan menggunakan perintah berikut :

```bash
kubectl apply -f p-fb-pod.yaml

pod/php-pesbuk-secret created
```

Dengan cara yang sama kita akan membuat service agar pod **php-pesbuk-secret** dapat diakses dari luar cluster.

buat file bernama p-fb-secret-service.yaml dengan konfigurasi berikut.

```bash
apiVersion: v1
kind: Service
metadata:
  name: pesbuk-secret-service
spec:
  selector:
    app: pesbuk-secret
  type: NodePort
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 80
```

script dapat dilihat di:

[https://gist.github.com/sdcilsy/e55a0b09487bba3ed7d5edd18b382e5b](https://gist.github.com/sdcilsy/e55a0b09487bba3ed7d5edd18b382e5b)

Kita akan mendapat port seperti service sebelumnya namun berbeda numbernya (**31182**).

```bash
kubectl get svc
```

[https://lh6.googleusercontent.com/ZaN1xiyHGnEZCneSvBFcd-r3wEtGXcHJ0DyHmLa5WmmvLk8wBwEXngWhnrIHGvNTzoeAkokYdLz0MHpC7VjJAoz7M_d25lfgv7LaPHaLa-1jPlutOUDCPoT7ji5vZrqTdqPu-48ZOT-V-G4Puw](https://lh6.googleusercontent.com/ZaN1xiyHGnEZCneSvBFcd-r3wEtGXcHJ0DyHmLa5WmmvLk8wBwEXngWhnrIHGvNTzoeAkokYdLz0MHpC7VjJAoz7M_d25lfgv7LaPHaLa-1jPlutOUDCPoT7ji5vZrqTdqPu-48ZOT-V-G4Puw)

Karena inbound rule untuk instance master sudah diupdate pada langkah sebelumnya, jadi kita tidak perlu lagi mengkonfigurasinya.

Untuk pengujian, kita bisa akses IP/DNS instance **master** dengan port nat pada service (**31182**) pada browser.

[https://lh4.googleusercontent.com/RhaXjWFsDVJp9Cpskan1koHKki1Nif_Vs90uis2wA33KD_PAL3jP5x9knCiBrKG7N9phte-UBGlA6rFJb8400FDuhfHM22fmGy9xhGt8cHATB5_V9dln3PyaYKepMJEnMBsBPhciesheXIqqQg](https://lh4.googleusercontent.com/RhaXjWFsDVJp9Cpskan1koHKki1Nif_Vs90uis2wA33KD_PAL3jP5x9knCiBrKG7N9phte-UBGlA6rFJb8400FDuhfHM22fmGy9xhGt8cHATB5_V9dln3PyaYKepMJEnMBsBPhciesheXIqqQg)