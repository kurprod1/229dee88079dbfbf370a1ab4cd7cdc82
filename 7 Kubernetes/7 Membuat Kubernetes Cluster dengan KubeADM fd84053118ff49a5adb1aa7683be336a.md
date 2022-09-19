# 7. Membuat Kubernetes Cluster dengan KubeADM

Created: July 7, 2022 1:31 PM

Bahan bacaan: 

[Creating a cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)

# **Persiapan Mesin**

- catatan: jika tidak diminta, silahkan lakukan step-step berikut sebagai user biasa, tanpa tambahan sudo.

Siapkan 3 buah mesin untuk percobaan ini. 1 mesin sebagai control-planner dan 2 mesin sebagai worker.

# ***Desain Kubernetes***

![https://lh4.googleusercontent.com/jTaa-KZ4S16uatA-loU-Q8cGIEGSjpRDOb6IQwY_ICPfMVQm9rOlHuFnhFj_p8OOhN3Q-L-yyrnXMju4w8krc0YVziJIXBnjhMpUNTHejdW6-XmqhHjC9RSuygef1UY9dkOUrhGxOOTKxbSEjQ](https://lh4.googleusercontent.com/jTaa-KZ4S16uatA-loU-Q8cGIEGSjpRDOb6IQwY_ICPfMVQm9rOlHuFnhFj_p8OOhN3Q-L-yyrnXMju4w8krc0YVziJIXBnjhMpUNTHejdW6-XmqhHjC9RSuygef1UY9dkOUrhGxOOTKxbSEjQ)

# ***Spesifikasi Mesin***

Lakukan penggantian hostname dengan perintah:

```bash
sudo suhostnamectl set-hostname master-01
```

Kita buat 3 EC2 dengan instance type **t2.medium** dengan disk size 40GB

|Hostname|master-01                         |
|--------|----------------------------------|
|IP (Wajib EIP)|0                                 |
|Core    |2                                 |
|RAM     |4                                 |
|HDD     |40                                |

|Hostname|node-01                           |
|--------|----------------------------------|
|IP (Wajib EIP)|0                                 |
|Core    |2                                 |
|RAM     |4                                 |
|HDD     |40                                |

|Hostname|node-02                           |
|--------|----------------------------------|
|IP (Wajib EIP)|0                                 |
|Core    |2                                 |
|RAM (GB)|4                                 |
|HDD     |40                                |

## ***Security Group***

Untuk percobaan kali ini, security group kita **set open all**.

# **Persiapan Umum**

Persiapan ini dilakukan disetiapp machine (**master-01, node-01, node-2**). Lakukan setiap instalasi  containerd dan Kubernetes Tool (**kubeadm, kubectl, kubelet**).

## ***Install Containerd***

Semenjak Kubernetes versi 1.20, Kubernetes akan [menghilangkan support docker sebagai container runtime](https://kubernetes.io/blog/2020/12/02/dont-panic-kubernetes-and-docker/). Sebagai gantinya, Kubernetes menggunakan runtime berstandar CRI lainnya yaitu [containerd](https://containerd.io/).

Pertama tama, kita update repository machine kita menggunakan perintah berikut

```bash
sudo apt-get update
```

Kita dapat menggunakan command berikut untuk menginstall containerd.

```bash
sudo apt install containerd
```

Setelah itu, kita membuat akan menyalakan ip forward pada machine. Ini menjadi [syarat bagi kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/) dalam membuat cluster dan join cluster. Dengan menyalakan module **br_netfilter**, kubernetes mengakses bridge dari machine kita. Kita dapat mengaktifkan module tersebut dengan perintah berikut.

```bash
sudo modprobe br_netfilter
```

Setelah itu kita configurasi iptable agar dapat mengakses bridge dengan perintah berikut.

```bash
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
br_netfilter
EOF
```

```bash
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
```

```bash
cat <<EOF | sudo tee /proc/sys/net/ipv4/ip_forward
1
EOF
```

```bash
sudo sysctl --system
```

Untuk testing **containerd** sudah terinstal dengan baik, kita bisa melakukannya dengan mengecek versi containerd.

```bash
containerd -v
```

![https://lh6.googleusercontent.com/VUDSzSsstCfStT1lFBmnv0GeT-2HSB-cs2ZBEfFti8rcymENkZzU5-dZsGWzyBOgIfBNGR1hQf2SmFHFUphh61D6rnaCdYsfAZpBYW43GGGCr2jtZ_R73CYzDDDOvEYUZXAGTHYmBl9-0j7q9w](https://lh6.googleusercontent.com/VUDSzSsstCfStT1lFBmnv0GeT-2HSB-cs2ZBEfFti8rcymENkZzU5-dZsGWzyBOgIfBNGR1hQf2SmFHFUphh61D6rnaCdYsfAZpBYW43GGGCr2jtZ_R73CYzDDDOvEYUZXAGTHYmBl9-0j7q9w)

# ***Install Kubernetes Tools (kubeadm, kubelet, kubectl)***

Pertama, kita update repository dan menginstal beberapa paket. Sebetulnya paket paket ini sudah diinstalkan pada step install **Docker**. Namun jika belum diinstal, kita akan menginstalnya sekarang.

```bash
sudo apt-get updatesudo apt-get install -y apt-transport-https ca-certificates curl
```

Memasukan GPG Key Google Cloud

```bash
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
```

Memasukan repository Kubernetes

```bash
echo "deb ![signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

Setelah itu, kita instalkan tools Kubernetes berikut.

```bash
sudo apt-get updatesudo apt-get install -y kubelet kubeadm kubectlsudo apt-mark hold kubelet kubeadm kubectl
```

# **Inisiasi Cluster**

## ***Config Control-Planner***

Perintah berikut dilakukan di mesin **master-01**. Perintah ini kan menginisiasi untuk membuat Kubernetes Cluster.

```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16 --control-plane-endpoint=18.222.93.10
```

Kita menggunakan ip public **master-01** sebagai control plane endpoint bila suatu saat ingin meningkatkan cluster ini ke High Availability.

![https://lh5.googleusercontent.com/sUiBm75Hhb9IGR5i4zfntC2QO--kdHbzrh8gociEeJhjPVSSWjiHk3dBSFHOiYBVe7itb6wLgnrou-K1bLpkvbI3iE2j32jyApCDtUF68KiW4MJcTGkxmvyGTuvC5uNKzqT-rTPNKOtv3fMNEg](https://lh5.googleusercontent.com/sUiBm75Hhb9IGR5i4zfntC2QO--kdHbzrh8gociEeJhjPVSSWjiHk3dBSFHOiYBVe7itb6wLgnrou-K1bLpkvbI3iE2j32jyApCDtUF68KiW4MJcTGkxmvyGTuvC5uNKzqT-rTPNKOtv3fMNEg)

Proses itu akan menghasilkan output kira-kira seperti ini:

![https://lh5.googleusercontent.com/vHftoe9wc7RxP7WK1eXR37nay_AeJrav-UhxVoI7AOB6wUXRhOfE5n7JSjiDLAmKupeE6vODb21AmkAAQn8bhMlPQisCqW8ImYD8ZaZ94-geUvi12ILxZ0BRdlOZGkUoDXblFHj0hX4AROpFMg](https://lh5.googleusercontent.com/vHftoe9wc7RxP7WK1eXR37nay_AeJrav-UhxVoI7AOB6wUXRhOfE5n7JSjiDLAmKupeE6vODb21AmkAAQn8bhMlPQisCqW8ImYD8ZaZ94-geUvi12ILxZ0BRdlOZGkUoDXblFHj0hX4AROpFMg)

untuk menjadikan master-01 menjadi control plane, kita bisa mengikuti petunjuk dari output tersebut.

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

lalu kita cek nodes dari cluster kita saat ini. Untuk saat ini, control plane belum ready. Namun akan kita lanjutkan untuk join worker-node (node)

![https://lh6.googleusercontent.com/FY34-dWNhcgKtiMhy9g59ccasNoYS9duTatzISZK3TptxzX6ZdFeHxKlf5oIL69h0V1lOQE3NCG73-2mXpn_AgQ41yrzh3hCyywC27eclYpMV2cFHJv6CKXjxzlaLKRMjvx0N6pCEQXtSWkPnA](https://lh6.googleusercontent.com/FY34-dWNhcgKtiMhy9g59ccasNoYS9duTatzISZK3TptxzX6ZdFeHxKlf5oIL69h0V1lOQE3NCG73-2mXpn_AgQ41yrzh3hCyywC27eclYpMV2cFHJv6CKXjxzlaLKRMjvx0N6pCEQXtSWkPnA)

## ***Config Worker (node-01 & node-02)***

Selanjutnya adalah mengeksekusi perintah **kubeadm join** kepada setiap node. Perintah ini terdapat pada output saat perintah **kubeadm init** dieksekusi. Perintah ini dilakukan di setiap worker:

```bash
sudo su
kubeadm join 18.222.93.10:6443 --token t7fvl1.lbvtlyuwf9ufxyy5 --discovery-token-ca-cert-hash sha256:206e907c8f6adec532bfc98150d518a83c476a10870aed20f616d3eecc077bd9
```

Outputnya akan seperti ini

![https://lh4.googleusercontent.com/5cqqiUZBZwZMkJMpJb6X-c4w5s7VE1CaoSjM3fjY47uiLqap_OH3A_NX2Bpla4T50iV26C9TKv4o4wvW2DKz0OisoacXnnxMzfxIeklES7WEYBxdG3oWTL053sJX2QWDMtgMqFjD4JkPmQAiSg](https://lh4.googleusercontent.com/5cqqiUZBZwZMkJMpJb6X-c4w5s7VE1CaoSjM3fjY47uiLqap_OH3A_NX2Bpla4T50iV26C9TKv4o4wvW2DKz0OisoacXnnxMzfxIeklES7WEYBxdG3oWTL053sJX2QWDMtgMqFjD4JkPmQAiSg)

# **Setup Network**

Setelah kedua worker sudah join cluster, sekarang mari kita setup network agar seluruh node bisa Ready dan berkomunikasi 1 sama lain. Ada beberapa pilihan untuk setup network ini. Dokumentasi ada di [sini](https://kubernetes.io/docs/concepts/cluster-administration/addons/#networking-and-network-policy).

Perintah ini dilakukan dari control-plane (**master-01**).

```bash
kubectl create -f https://docs.projectcalico.org/manifests/tigera-operator.yaml
kubectl create -f https://docs.projectcalico.org/manifests/custom-resources.yaml
```

# **Finalisasi Cluster**

Untuk melihat seluruh node, gunakan perintah berikut pada control-plane (**master-01**)

```bash
kubectl get nodes
```

![https://lh3.googleusercontent.com/i0Q1_YwNQ8NajtvPI7HE1k2j_JjzjAqyMcO1B02LPcdzAlAvsIuCsqSZQ9Gen912_RQwz53KOlU9pky-AcWoDDV2G2UYOu0PYkr3PJWEM1SlwMfUjuxT-vBO_g7s4fBq8lWMCFUpQB1p-2V0vg](https://lh3.googleusercontent.com/i0Q1_YwNQ8NajtvPI7HE1k2j_JjzjAqyMcO1B02LPcdzAlAvsIuCsqSZQ9Gen912_RQwz53KOlU9pky-AcWoDDV2G2UYOu0PYkr3PJWEM1SlwMfUjuxT-vBO_g7s4fBq8lWMCFUpQB1p-2V0vg)

Seperti yang bisa kita lihat, seluruh node sudah berstatus ready. Namun untuk node worker, memilii role **<none>**. Kita bisa menggantinya menjadi worker dengan cara berikut.

```bash
kubectl label node node-01 node-role.kubernetes.io/worker=worker
kubectl label node node-02 node-role.kubernetes.io/worker=worker
sudo kubectl get nodes
```

![https://lh5.googleusercontent.com/Xjr1QP1HCH3a8FD55b71ni_6gke5tZjLMLsFri5WrUlOgiqt2v3eWjgSEtPSZ2L_XYqhNwKHaV98s5I_xLNzTd5MQ7GLoFMJgs3VW_cHmhxHgfDfsCki_DvPDc5ItMTeQwTMsgo4HeDMFW0OJg](https://lh5.googleusercontent.com/Xjr1QP1HCH3a8FD55b71ni_6gke5tZjLMLsFri5WrUlOgiqt2v3eWjgSEtPSZ2L_XYqhNwKHaV98s5I_xLNzTd5MQ7GLoFMJgs3VW_cHmhxHgfDfsCki_DvPDc5ItMTeQwTMsgo4HeDMFW0OJg)

# **Cleanup Cluster**

Kebalikan dari kubeadm init, kita bisa mengeluarkan node dari cluster dengan perintah berikut.

```bash
kubectl drain <node name> --delete-local-data --force --ignore-daemonsets
kubectl delete node <node name>
```

lalu untuk mereset node yang ada pada cluster, kita bisa menggunakan command seperti berikut.

```bash
sudo kubeadm reset
```