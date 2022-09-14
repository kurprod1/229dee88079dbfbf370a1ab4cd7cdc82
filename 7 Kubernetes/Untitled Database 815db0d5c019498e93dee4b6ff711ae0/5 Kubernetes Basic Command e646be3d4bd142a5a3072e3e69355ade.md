# 5. Kubernetes Basic Command

Created: July 7, 2022 1:24 PM

Kita akan berkenalan dengan salah satu tool yang Kubernetes berikan untuk memanage dan mengontrol kluster **Kubernetes** kita. Ya, namanya adalah **kubectl**. Kubectl sering digunakan untuk membuat resource untuk kluster seperti membuat sebuah service, deployment, pod, scaling, persistent volume, hingga melihat info dari resource tersebut. Kita juga dapat menggunakan kubectl untuk mengkonfigurasi sebuah resource dari file berekstensi yaml.

# ***Create***

Perintah yang paling umum adalah **kubectl create** dimana perintah ini digunakan untuk membuat resource pada Kubernetes. Contohnya adalah deployment.

```bash
kubectl create deployment [nama deployment] --image=[container image]
```

```bash
kubectl create deployment nginx-depl --image=nginx
deployment.apps/nginx-depl created
```

Perintah tersebut akan membuat **deployment** dengan nama nginx-depl, **replicasets** dan **pod** dengan image nginx.

# ***Apply***

Perintah lainnya adalah kubectl **apply**. Perintah ini digunakan untuk menerapkan sebuah konfigurasi ke resource cluster menggunakan file konfigurasi atau stdin. Kegunaan perintah ini hampir mirip dengan **kubectl create** yaitu membuat suatu resource kluster, namun jika resource tersebut membutuhkan opsi atau atribut yang tidak dapat dilakukan oleh perintah **kubectl create**, maka kita gunakan **kubectl apply**. Perintah ini sangat  direkomendasikan untuk production. Misalnya saya ingin membuat deployment dengan file bernama **nginx-prod.yaml**.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-prod
  labels:
    app: nginx-prod
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-prod
  template:
    metadata:
      labels:
        app: nginx-prod
    spec:
      containers:
      - name: nginx-prod
        image: nginx
        ports:
        - containerPort: 80
```

Script dapat dilihat di [https://gist.github.com/sdcilsy/ae521c9b488429fae8409a5b0c788540](https://gist.github.com/sdcilsy/ae521c9b488429fae8409a5b0c788540)

kita bisa menambahkan resource tersebut dengan mengeksekusi perintah **kubectl apply -f nginx-prod.yaml**.

```bash
kubectl apply -f nginx-prod.yaml
deployment.apps/nginx-prod created
```

# ***Describe***

Perintah selanjutnya adalah **kubectl describe** dimana perintah ini digunakan untuk memberikan detail resource pada kluster. Misalnya adalah detail **deployment** seperti berikut.

```bash
kubectl describe [resource] [resource name]
```

```bash
kubectl describe deployment nginx-depl

Name:                   nginx-depl
Namespace:              default
CreationTimestamp:      Wed, 24 Mar 2021 19:17:28 +0700
Labels:                 app=nginx-depl
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=nginx-depl
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=nginx-depl
  Containers:
   nginx:
    Image:        nginx
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   nginx-depl-5c8bf76b5b (1/1 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  7m14s  deployment-controller  Scaled up replica set nginx-depl-5c8bf76b5b to 1
```

# ***Get***

Perintah lainnya yang tak kalah penting adalah **kubectl get**. Perintah ini digunakan untuk menampilkan resource pada kluster. Berbeda dengan perintah **describe**, **get** lebih menampilkan resource secara general. Misalnya saya ingin melihat ada berapa pod yang berjalan dengan perintah **kubectl get pod**.

```bash
kubectl get pod

NAME                       READY   STATUS    RESTARTS   AGE
nginx-depl-84dd4db-22qk8   1/1     Running   0          11m
nginx-depl-84dd4db-8s667   1/1     Running   0          11m
nginx-depl-84dd4db-st8c8   1/1     Running   0          11m
```

# ***Delete***

Jika ingin menghapus resource pada kluster, kita dapat menggunakan perintah **kubectl delete**. Misalnya saya ingin menghapus deployment dengan nama **nginx-depl** dengan perintah **kubectl delete deployment nginx-depl**.

```bash
kubectl delete deployment nginx-depl
deployment.apps "nginx-depl" deleted
```

# ***Expose***

Pod pada kubernetes secara default memang hanya bisa diakses oleh network pada jaringan kluster Kubernetes saja (lihat materi Service selanjutnya). Agar pod dapat diakses oleh jaringan luar. maka kita bisa membuat service menggunakan perintah kubectl expose [resource] [nama resource] --port=[port fisik] --target-port=[port container]

```bash
kubectl expose deployment nginx-depl --port=80 --target-port=80
service/nginx-depl exposed
```

# ***Exec***

Ketika kita ingin mengeksekusi perintah didalam kontainer, maka kita bisa mengunakan perintah **kubectl exec**. Misalnya saya ingin mengeksekusi perintah **date** pada pod dengan nama **nginx-depl-5c8bf76b5b-q4f69**, maka kita bisa menggunakan perintah berikut

```bash
kubectl exec nginx-depl-5c8bf76b5b-q4f69 -- date
Wed Mar 24 13:19:22 UTC 2021
```

# ***Logs***

Selanjutnya adalah perintah kubectl logs yang digunakan untuk menampilkan log dari container pada pod. Misalnya saya ingin melihat log pada pod **nginx-depl-5c8bf76b5b-q4f69** maka kita bisa menggunakan perintah seperti berikut.

```bash
kubectl logs nginx-depl-5c8bf76b5b-q4f69

/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
```