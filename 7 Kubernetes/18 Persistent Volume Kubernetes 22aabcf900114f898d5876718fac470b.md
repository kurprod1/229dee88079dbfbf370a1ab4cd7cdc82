# 18. Persistent Volume Kubernetes

Created: July 12, 2022 12:01 PM

Salah satu fitur yang disediakan oleh Kubernetes adalah adanya **Persistent Volume (PV)**. Ini berguna untuk menyediakan resource volume pada kluster yang dapat digunakan sesuai kebutuhan. **Persistent Volume** adalah volume yang disediakan oleh administrator dengan file sistem tertentu, ukuran, dan pengenal seperti ID dan nama dari volume tersebut.

Namun, persistent volume tidak dapat langsung digunakan untuk pod. Oleh karena itu, ada fitur lain yang Kubernetes berikan, yaitu adalah **Persistent** **Volume** **Claim** **(PVC)**.  **Persistent Volume Claim** adalah sebuah permintaan penggunaan Persistent Volume dari pengguna. Claim ini ditujukan ke sebuah pod yang mengkonsumsi resource dari **Persistent Volume** sesuai dengan permintaan dari **Persistent Volume Claim**. Dalam persistent volume claim, kita bisa menyebutkan spesifikasi volume yang diperlukan untuk pod misalnya adalah ukuran dari volume yang dibutuhkan.

Tipe Storage

- gcePersistentDisk
- awsElasticBlockStore
- Cinder
- (lebih lengkapnya baca dokumentasi [disini](https://kubernetes.io/docs/concepts/storage/volumes/#volume-types))

Untuk praktikum selanjutnya, kita akan mencoba membuat **Persistent Volume**, **Persistent Volume Claim** dan menggunakannya pada pod.

Dalam praktik ini, kita bisa menggunakan **cluster K8S** pada **AWS** sebagai bahan percobaan. Tujuannya adalah agar aplikasi pada pod dapat menggunakan volume yang ada pada host node. Jika belum memiliki cluster kubernetes, coba baca kembali **section sebelumnya** untuk membuat cluster menggunakan **kops** atau **kubeadm**.

# **Membuat Persistent Volume**

Ada banyak sekali [tipe persistent volume](https://kubernetes.io/docs/concepts/storage/volumes/#volume-types) pada kubernetes. Tiap tipe memiliki karakteristik masing masing sesuai kebutuhan. Ada yang binding ke local disk atau sesuai provisioner (cloud provider). Pada praktikum kali ini kita akan membuat **persistent volume** menggunakan tipe [volume local](https://kubernetes.io/docs/concepts/storage/volumes/#local) yang binding volume ke directory local (node).

Untuk membuat persistent volume, kita buat file konfigurasi persistent volume ini dengan nama **vp-devops.yaml**.

```bash
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-devops
  labels:
    type: node-local
spec:
  capacity:
    storage: 10Gi
  volumeMode: Filesystem
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Delete
  storageClassName: local-storage
  local:
    path: /home/ubuntu/data
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values
          - #hostname node/worker
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/e4d13017f7d839c0a0e4c58307999986](https://gist.github.com/sdcilsy/e4d13017f7d839c0a0e4c58307999986)

File konfigurasi tersebut akan membuat persistent volume dengan nama **pv-devops,** kapasitas **10Gb**, access mode **Read Write Once**, storageClassName dengan nama **local-storage** dan mounting pada */home/ubuntu/data* dengan volume type **local**.

Ada yang menarik dari konfigurasi diatas yaitu **nodeAffinity**. Yaitu node yang dipilih yang bertanggungjawab atas persistent volume yang dibuat. Baca dokumentasi [ini](https://kubernetes.io/docs/concepts/storage/volumes/#local) lebih lanjut. Node yang dipilih adalah node worker berdasarkan **hostnamenya**. ****Pada case ini, hostname dari node worker penulis adalah **ip-172-20-33-189.ec2.internal**. Maka directory **/home/ubuntu/data** yang kita set tadi akan diambil dari instance ini.

![https://lh3.googleusercontent.com/oE3n1igqnYDRXU160PI9ve3mxy7fAPRA9rx_K1RAMBYLHH1DyOsxeGGZ-SPI0r-h-aVpPm8dP81B6OtPqS4Gvun6Z5exnYVBdVc3_Cigls6lCGR-TVCokmwHlCPziWMz50pn0tMcrwE3AwS2PA](https://lh3.googleusercontent.com/oE3n1igqnYDRXU160PI9ve3mxy7fAPRA9rx_K1RAMBYLHH1DyOsxeGGZ-SPI0r-h-aVpPm8dP81B6OtPqS4Gvun6Z5exnYVBdVc3_Cigls6lCGR-TVCokmwHlCPziWMz50pn0tMcrwE3AwS2PA)

Selanjutnya kita eksekusi perintah **kubectl apply -f pv-devops.yaml** untuk membuat **persistent volume**.

```bash
kubectl apply -f pv-devops.yaml

persistentvolume/pv-devops created
```

kita bisa melihat **persistent volume** dengan perintah **kubectl get pv.**

![https://lh4.googleusercontent.com/LZeKzva8pBsJKbnn3ebbGI4uCoKwv5ODLfUUMPF9nUyO0mIEyeY01pZa4wFvswmy0SWWs3Cx0lOoTbQ64PVBppwQnGihygULPQJ1m8ZRpRsVRXy3Na726KMH49GoTnJozu0XedgXupJ4PXPohQ](https://lh4.googleusercontent.com/LZeKzva8pBsJKbnn3ebbGI4uCoKwv5ODLfUUMPF9nUyO0mIEyeY01pZa4wFvswmy0SWWs3Cx0lOoTbQ64PVBppwQnGihygULPQJ1m8ZRpRsVRXy3Na726KMH49GoTnJozu0XedgXupJ4PXPohQ)

Langkah selanjutnya yang dilakukan adalah untuk menyiapkan data yang akan dijadikan **Persistent** **Volume**. Yaitu dengan membuat direktori */**home/ubuntu/data*** pada instance node seperti yang dijelaskan diatas dengan file **index.html** seperti berikut.

```bash
ssh ubuntu@<IP/DNS instance node> -i ~/.ssh/id_rsa

sudo mkdir /mnt/data

sudo sh -c "echo 'Hello from Kubernetes storage' > /home/ubuntu/data/index.html"

cat /home/ubuntu/data/index.html 
Hello from Kubernetes storage
```

# **Membuat Persistent Volume Claim**

Langkah selanjutnya adalah untuk membuat **Persistent Volume Claim** untuk kebutuhan pod yang akan dibuat nanti. Caranya hampir sama dengan membuat **persistent** **volume**, namun kita perlu mendefinisikan **storageClassName** yang sama dengan **Persistent Volume** dan **alokasi ukuran volume** yang diminta seperti pada file konfigurasi vpc berikut yang diberi nama **vpc-devops.yaml**.

```bash
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-devops
spec:
  storageClassName: local-storage
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/63405c8e10cdb9c70b2a76bd42747198](https://gist.github.com/sdcilsy/63405c8e10cdb9c70b2a76bd42747198)

Pada vpc tersebut, kita sudah mendefinisikan alokasi volume yang dibutuhkan.

Langkah selanjutnya adalah mengeksekusi perintah kubectl apply -f pvc-devops.yaml untuk membuat pvc.

```bash
kubectl apply -f vpc-devops.yaml

persistentvolumeclaim/pvc-devops created
```

Kita dapat melihat hasil pvc dengan perintah **kubectl get pv** dan **kubectl get pvc**.

![https://lh3.googleusercontent.com/vvMwYHw2rKrBHf3uabAMARLFl-frOhcHrdDGcDb5GV_XAF3nZ5fVBkZ1xJExIzhQsWjsU5ciuYh-jIcv9PuQAVurjQ2enL6yGZgrW11ikd8YjvvqQu0lT6fLjqq8GJCyK-6Fl9fxqpUVe4xB-Q](https://lh3.googleusercontent.com/vvMwYHw2rKrBHf3uabAMARLFl-frOhcHrdDGcDb5GV_XAF3nZ5fVBkZ1xJExIzhQsWjsU5ciuYh-jIcv9PuQAVurjQ2enL6yGZgrW11ikd8YjvvqQu0lT6fLjqq8GJCyK-6Fl9fxqpUVe4xB-Q)

Dapat dilihat bahwa VP sekarang statusnya bound dan VPC secara otomatis mengklaim VP yang sudah dibuat sebelumnya.

# **Menggunakan PVC pada Pod**

Lalu sekarang kita melakukan binding volume yang sudah diclaim ke pod. Kita akan membuat file konfigurasi pod dengan nama **pod-nginx.yaml** seperti berikut.

```bash
apiVersion: v1
kind: Pod
metadata:
  name: pod-nginx
spec:
  volumes:
    - name: pv-devops-storage
      persistentVolumeClaim:
        claimName: pvc-devops
  containers:
    - name: pod-nginx
      image: nginx
      ports:
        - containerPort: 80
          name: "http-server"
      volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: pvc-devops-storage
```

script dapat dilihat di [https://gist.github.com/sdcilsy/df19f357cd82aba77b4d9b093f636240](https://gist.github.com/sdcilsy/df19f357cd82aba77b4d9b093f636240)

Pod tadi menggunakan image nginx yang menggunakan volume **pv-devops-storage** dari PVC yang sudah di claim dari persistent volume. Lalu mounting ke directory **/usr/share/nginx/html** pada pod.

Pastikan pod yang sudah dibuat berjalan dengan perintah **kubectl get pod pod-nginx**

```bash
kubectl get pod pod-nginx
```

![https://lh3.googleusercontent.com/fwXIfECpemeMOmiQ6rf25Bbv8ezl8WyogolSYWCm2DvC__zc2D-VhFmJ5XWJZEKSl4lclS53BUjbyWfrFRfTVaLqpBR_ZwAAiLcYpW2a7EIWyKnP-un2oSc_5-9XOqG3Fd3Fl4zDpSACX5CSCg](https://lh3.googleusercontent.com/fwXIfECpemeMOmiQ6rf25Bbv8ezl8WyogolSYWCm2DvC__zc2D-VhFmJ5XWJZEKSl4lclS53BUjbyWfrFRfTVaLqpBR_ZwAAiLcYpW2a7EIWyKnP-un2oSc_5-9XOqG3Fd3Fl4zDpSACX5CSCg)

# **Membuat Service**

Setelah itu kita akan expose pod tersebut agar dapat diakses dari luar cluster menggunakan **service**. Service yang akan kita buat me listen di port 80. Kita buat file baru dengan nama **svc-devops.yaml**.

```bash
apiVersion: v1
kind: Service
metadata:
  name: nginx-pv
spec:
  type: NodePort
  selector:
    app: nginx-pv
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

script dapat dilihat di:

[https://gist.github.com/sdcilsy/4116c3a6ee4cf819896b64948a4d8a7a](https://gist.github.com/sdcilsy/4116c3a6ee4cf819896b64948a4d8a7a)

Kita akan mendapatkan port nat (31423) pada service tersebut.

![https://lh3.googleusercontent.com/ZZ5dbr43ZijE0TgB_dBWMQDhOK8CYwnZo8-uIg8qLeZcgLpZxqobmX_lknF3JJ8jgq2UU6T9ANxld2RjFgA8xvcKGz5Ob3PWsbHf6gfJkKuVhkYuC_IrICuZyNKguuSPw7em3SnvZC_Vp9K-Ow](https://lh3.googleusercontent.com/ZZ5dbr43ZijE0TgB_dBWMQDhOK8CYwnZo8-uIg8qLeZcgLpZxqobmX_lknF3JJ8jgq2UU6T9ANxld2RjFgA8xvcKGz5Ob3PWsbHf6gfJkKuVhkYuC_IrICuZyNKguuSPw7em3SnvZC_Vp9K-Ow)

Setelah itu kita akses IP/DNS instance master diikuti dengan port nat yang kita dapat dari service.

![https://lh3.googleusercontent.com/tt5wiPRLM8ATlqYtxBrQ6MxL852aT5W-nR4EUQKvByK2Qf_ANtl5OGVAV6QywZXnVFQuB7Kd-xBp_noy49cr6x6p_GBiO4kWDBWhGsQKwhsBqvA9rj3rcVBUQS57zwT21qGIEnwfdRry-zSVAg](https://lh3.googleusercontent.com/tt5wiPRLM8ATlqYtxBrQ6MxL852aT5W-nR4EUQKvByK2Qf_ANtl5OGVAV6QywZXnVFQuB7Kd-xBp_noy49cr6x6p_GBiO4kWDBWhGsQKwhsBqvA9rj3rcVBUQS57zwT21qGIEnwfdRry-zSVAg)

Note: Jika service tidak dapat diakses, coba cek kembali rule inbound pada security group **master**

atau bisa baca kembali section sebelumnya mengenai security groups.