# 4. Installasi Kubernetes (Minikube)

Created: July 7, 2022 1:16 PM

Minikube adalah alat yang dapat dengan mudah menjalankan Kubernetes di komputer lokal. Minikube menjalankan node cluster Kubernetes di mesin virtual (VM) di laptop untuk pengguna yang ingin mencoba atau mengembangkan Kubernetes.

Meski minikube dijalankan pada lokal, fitur yang disediakan cukup merepresentasikan Kubernetes pada implementasi nyatanya. Fitur tersebut antara lain :

- DNS
- NodePort
- Configmap
- *Dashboard*
- *Container runtime* : Docker, CRI-O, dan containerd
- CNI (Container Network Interface)
- Ingress

# **Install Hypervisor**

Jika kita belum menginstal hypervisor, install salah satunya sekarang:

- KVM, yang juga menggunakan QEMU
- VirtualBox

Minikube juga mendukung opsi **--vm-driver = none** yang menjalankan komponen Kubernetes di host dan bukan di VM. Menggunakan driver ini membutuhkan Docker dan lingkungan Linux tetapi bukan hypervisor.

# **Install Minikube**

Pastikan kita sudah menginstall kubectl pada server-server

## ***Install Minikube via direct download***

Kita akan install minikube via direct download kita bisa bisa download stand alone binary menggunakan perintah berikut

```bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube
```

Berikut cara mudah untuk menambahkan Minikube

```bash
sudo mkdir -p /usr/local/bin/sudo install minikube /usr/local/bin/
```

## ***Install Minikube using Homebrew***

Sebagai alternatif lain, kira dapat menginstal Minikube menggunakan Linux Homebrew dengan perintah berikut

```bash
brew install minikube
```

# ***Confirm Installation***

Untuk mengkonfirmasi pemasangan hypervisor dan Minikube yang berhasil, kita dapat menjalankan perintah berikut untuk memulai local Kubernetes cluster:

```bash
minikube start --vm-driver=<driver_name>
```

Setelah minikube mulai selesai, jalankan perintah di bawah ini untuk memeriksa status cluster:

```bash
minikube status
```

Jika cluster kita berjalan, output dari status minikube sebagai berikut

```bash
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
timeToStop: Nonexistent
```

Untuk memberhentikan service dari minikube kita bisa masukan perintah berikut :

```bash
minikube stop
```

# ***Clean up local state***

Jika sebelumnya telah menginstal Minikube, dan jalankan perintah berikut

```bash
minikube start
```

dan setelah melakukan perintah diatas muncul error berikut

```bash
machine does not exist
```

kita perlu melakukan clear minikube local state dengan perintah berikut

```bash
minikube delete
```