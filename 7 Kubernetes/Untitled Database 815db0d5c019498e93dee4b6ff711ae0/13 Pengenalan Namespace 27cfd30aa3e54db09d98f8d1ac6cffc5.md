# 13. Pengenalan Namespace

Created: July 7, 2022 5:18 PM

Ketika bekerja dalam tim, maka ada baiknya untuk memisahkan resource sesuai kebutuhan setiap tim. Inilah dimana namespace masuk kedalam solusi tersebut. Namespace adalah sebuah kluster virtual dari kluster fisik dimana kita dapat mengalokasikan resource seperti RAM, CPU dan disk sesuai kebutuhan.

Ada 3 Namespace default yang sudah dibuat ketika sebuah kluster dibuat, yakni :

- default
    
    Namespace default untuk objek yang dibuat tanpa mencantumkan *namespace* pada spesifikasinya
    
- kube-system
    
    **namespace yang digunakan untuk objek yang dibuat oleh sistem Kubernetes
    
- kube-public
    
    namespace ini dibuat secara otomatis dan dapat diakses oleh semua pengguna (termasuk yang tidak diautentikasi).Namespace ini disediakan untuk penggunaan klaster, jika beberapa resouce harus terlihat dan dapat dibaca secara publik di seluruh klaster
    

# **Fungsi Namespace**

Berikut adalah beberapa fungsi penting dari Namespace di Kubernetes

- Namespaces membantu komunikasi *pod-to-pod* menggunakan Namespace yang sama.
- Namespace adalah *cluster* *virtual* yang dapat duduk di atas *cluster* fisik yang sama.
- Mereka memberikan pemisahan logis antara tim dan environment

# **Melihat Namespace**

Kita dapat melihat namespace yang adad menggunakan perintah **kubectl get ns** **atau **kubectl get namespaces***.*

```bash
kubectl get ns

NAME              STATUS   AGE
default           Active   56m
kube-public       Active   56m
kube-system       Active   56m
```

# **Membuat Namespace**

Langkah awal untuk membuat namespace adalah untuk menentukan kebutuhan dari namespace tersebut. Misalnya namespace tersebut digunakan untuk tim Developer untuk aplikasi yang sedang dikembangkannya. Maka kita dapat membuat namespace dengan menggunakan perintah ***kubectl create ns [nama namespacenya].***

```bash
kubectl create ns devopsnamespace/devops created
```

Kita juga dapat membuat namespace dari file yaml dengan perintah **kubectl apply -f [file namespacenya]**. Pertama tama, kita buat terlebih dahulu file bernama **ns-devops.yaml** dengan isi sebagai berikut

```bash
apiVersion: v1kind: Namespacemetadata:  name: devops
```

script dapat dilihat pada [https://gist.github.com/sdcilsy/c296293ec35b740df31b0b8e354826d2](https://gist.github.com/sdcilsy/c296293ec35b740df31b0b8e354826d2)

Lalu kita buat namespace tersebut menggunakan perintah **kubectl apply -f [file namespacenya]**

```bash
kubectl apply -f ns-devops.yaml

namespace/devops created
```

Kita bisa melihat hasil dari perintah tersebut dengan perintah **kubectl get ns.**

```bash
kubectl get ns

NAME              STATUS   AGE
default           Active   160m
devops            Active   43s
kube-node-lease   Active   160m
kube-public       Active   160m
kube-system       Active   160m
```

# **Menentukan Resource pada Namespace**

Seperti yang sudah dijelaskan pada awal materi, bahwa namespace dapat digunakan untuk mengalokasikan resource kluster fisik ke kluster virtual. Ini dapat dilakukan dengan cara membuat Resource Quota yang terapkan pada namespace.

Pertama tama, kita buat dulu file konfigurasi Resource Quota dengan nama **rq-devops.yaml** yang akan dibind  ke namespace yang sudah dibuat sebelumnya. Lalu kita masukan resource yang diinginkan.

```bash
apiVersion: v1
kind: ResourceQuota
metadata:
  name: mem-cpu
  namespace: devops
spec:
  hard:
    requests.cpu: "0.5"
    requests.memory: 512Mi
    limits.cpu: "1"
    limits.memory: 1Gi
```

Script dapat dilihat di[https://gist.github.com/sdcilsy/c4d774c99925c49a9612ef82a9d33853](https://gist.github.com/sdcilsy/c4d774c99925c49a9612ef82a9d33853)

Pada file konfigurasi tersebut, ada namespace yang harus diisi terlebih dahulu. Karena kita menggunakan namespace yang sudah dibuat sebelumnya, maka kita tinggal memasukannya. Lalu untuk resource yang dialokasikan untuk namespace tersebut bisa kita atur sesuai kebutuhan.

Lalu kita eksekusi perintah **kubectl apply -f [file resource quotanya]**

```bash
kubectl apply -f rq-devops.yaml 

resourcequota/mem-cpu created
```

Hasil dari resource quota ini bisa kita lihat dengan menggunakan perintah **kubectl describe quota -n devops**.

```bash
kubectl describe quota -n devops

Name:            mem-cpu
Namespace:       devops
Resource         Used  Hard
--------         ----  ----
limits.cpu       0     1
limits.memory    0     1Gi
requests.cpu     0     500m
requests.memory  0     512Mi
```

# **Binding Pod ke Namespace**

Setelah kita berhasil membuat namespace dan mengalokasikan resource ke namespace tersebut, langkah selanjutnya adalah membuat pod dan melakukan bind ke namespace yang sudah dibuat. Caranya adalah kita membuat file konfigurasi pod dengan nama **pod-nginx.yaml** dan menuliskan namespace yang sudah dibuat, lalu berapa banyak resource yang dibutuhkan.

```bash
apiVersion: v1
kind: Pod
metadata:
  namespace: devops
  name: nginx-app
  labels:
     app: nginx-app
spec:
  containers:
  - name: nginx-app
    image: nginx:alpine
    ports:
    - containerPort: 80
    resources:
      limits:
        memory: "400Mi"
        cpu: "0.3"      
      requests:
        memory: "300Mi"
        cpu: "0.2"
```

script dapat dilihat di [https://gist.github.com/sdcilsy/7e9898d9664ef758463e7b699b0a0fa8](https://gist.github.com/sdcilsy/7e9898d9664ef758463e7b699b0a0fa8)

kita sudah membuat pod yang yang ditautkan ke namespace devops dengan resource yang dipakai adalah ram sebesar 300Mb, dan cpu sebesar 0,2.

Dan jika kita melihat alokasi resource untuk namespace **devops** tersebut menggunakan perintah **kubectl describe quota -n devops**, maka akan terlihat perbedaan setelah membuat pod.

```bash
kubectl describe quota -n devops

Name:            mem-cpu
Namespace:       devops
Resource         Used   Hard
--------         ----   ----
limits.cpu       300m   1
limits.memory    400Mi  1Gi
requests.cpu     200m   500m
requests.memory  300Mi  512Mi
```

Jika kita merequest resource diatas limit yang sudah ditentukan, maka akan terjadi error. Kita buat lagi file konfigurasi pod dengan nama **pod-nginx-err.yaml** yang hampir mirip dengan yang sebelumnya dibuat, namun pada bagian resourcenya yang berbeda.

```bash
apiVersion: v1
kind: Pod
metadata:
  namespace: devops
  name: nginx-app-err
  labels:
     app: nginx-app-err
spec:
  containers:
  - name: nginx-app-err
    image: nginx:alpine
    ports:
    - containerPort: 80
    resources:
      limits:
        memory: "700Mi"
        cpu: "0.6"      
      requests:
        memory: "600Mi"
        cpu: "0.6"
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/ca5ec49950038c7bb5511a774dfaa08e](https://gist.github.com/sdcilsy/ca5ec49950038c7bb5511a774dfaa08e)

Maka ketika kita masukan perintah **kubectl apply -f pod-nginx-err.yaml** akan menghasilkan output seperti berikut.

```bash
kubectl apply -f pod-nginx-err.yaml
 
Error from server (Forbidden): error when creating "pod-nginx-err.yaml": pods "nginx-app-err" is forbidden: exceeded quota: mem-cpu, requested: requests.cpu=600m,requests.memory=600Mi, used: requests.cpu=0,requests.memory=0, limited: requests.cpu=500m,requests.memory=512Mi
```

Error tersebut terjadi karena request resource pada pod melebihi kapasitas yang tersedia.