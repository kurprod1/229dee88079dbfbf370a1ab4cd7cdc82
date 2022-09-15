# 19. Dynamic Volume Provisioning

Created: July 12, 2022 12:07 PM

**Dynamic Volume Provisioning** memungkinkan volume penyimpanan dibuat sesuai permintaan. Tanpa Dynamic Volume Provisioning, administrator cluster harus secara manual memanggil cloud atau penyedia penyimpanan mereka untuk membuat volume penyimpanan baru, lalu membuat objek PersistentVolume di Kubernetes. Fungsi dinamis ini menghilangkan kebutuhan administrator klaster untuk melakukan pra-konfigurasi penyimpanan. Sebaliknya, ini akan secara otomatis mengatur ruang penyimpanan ketika pengguna memintanya.

Dengan menggunakan Dynamic Volume Provisioning, apabila kita ingin menggunakan volume pada kubernetes, kita hanya mendeklarasikan saja **VPC** dengan object **StorageClass** yang sudah dibuat oleh platform yang kita gunakan. Si **StorageClass** ini lah yang akan mengatur request volume yang kita minta.

Singkatnya, dengan menggunakan Dynamic Volume Provisioning, secara otomatis, request volume kita akan dihandle oleh **StorageClass.**

Ada beberapa StorageClass yang tersedia diberbagai Cloud Provider contohnya seperti pada tabel berikut

[Untitled](19%20Dynamic%20Volume%20Provisioning%20912132aa6b1245328130fc0305afaeec/Untitled%20Database%20deb58bb08e8e43478d85dd70a72ce6e9.csv)

# **Dynamic Volume Provisioning Best Practice**

Pada praktikum kali ini kita akan menggunakan cluster kubernetes pada AWS. Platform AWS tentunya memiliki provisioner untuk dynamic volume. Jika kita lihat storageClass yang ada pada cluster, kita menemukan ada **default** dan **gp2**. Keduanya menggunakan provisioner aws-ebs yang artinya PVC yang kita request akan dibuatkan EBS.

[https://lh5.googleusercontent.com/ro18OO4zxG3OKTwc7lBZ3Ccv1ufED0SAnusPyZrk3LFGUWrDaG50mw_K8KGCFKt8cLOlUZSW-8K6gPUfj0ObwrF7Li2gmLldZcai2-QYPcb16Urf6NVApgvMQOiRe5ukuZnJd8rQ9cVi8x75Gw](https://lh5.googleusercontent.com/ro18OO4zxG3OKTwc7lBZ3Ccv1ufED0SAnusPyZrk3LFGUWrDaG50mw_K8KGCFKt8cLOlUZSW-8K6gPUfj0ObwrF7Li2gmLldZcai2-QYPcb16Urf6NVApgvMQOiRe5ukuZnJd8rQ9cVi8x75Gw)

## ***Membuat PVC***

Langkah selanjutnya adalah kita membuat file konfigurasi **PVC** bernama **pvc-dynamic.yaml** dengan storage **standard** dengan request volume 1GB.

```bash
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: dynamic-volume
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: default
  resources:
    requests:
      storage: 1Gi
```

script dapat dilihat di

[https://gist.github.com/sdcilsy/ce5d0be085d5fbb02ba1a2958af188f9](https://gist.github.com/sdcilsy/ce5d0be085d5fbb02ba1a2958af188f9)

Kita bisa mengeksekusi perintah berikut untuk membuat **PVC**

```bash
kubectl apply -f pvc-dynamic.yaml

persistentvolumeclaim/dynamic-volume created
```

Kita bisa melihat hasil dari **PVC** ini menggunakan perintah **kubectl get PVC**.

Jika kita lihat ke menu EBS pada EC2 Dashboard, kita akan melihat ada EBS baru sesuai PVC yang kita buat dengan tipe gp2 dan

**storage 1GB**

.

[https://lh6.googleusercontent.com/Rln32905np0r0iXhNp321vJDVP5ZwhsCkgMq6SGlEC2vNP9z3kDTtRjtgLUZwe7FqsmC2wbrzagQVcW4oMLeuV4POMUXAJXY5tJUFctWvD-GCWwaZzm34WhrbA48EuV6MU-AQcySl_4afsna6g](https://lh6.googleusercontent.com/Rln32905np0r0iXhNp321vJDVP5ZwhsCkgMq6SGlEC2vNP9z3kDTtRjtgLUZwe7FqsmC2wbrzagQVcW4oMLeuV4POMUXAJXY5tJUFctWvD-GCWwaZzm34WhrbA48EuV6MU-AQcySl_4afsna6g)

[https://lh4.googleusercontent.com/a-52VYZn6jsQdJL0Tw5yrsOKzS2hUg67fotxUibCT3v-Pe5PkvENX0ZcIaM1jYykJR86-AEpSaIE1xk24-QByQ7G1s8Pw-MSRdwnwHNArA0p4UCVwWFw0dOIGpgnhv3Y3AmkzRWO5GoOVIId4A](https://lh4.googleusercontent.com/a-52VYZn6jsQdJL0Tw5yrsOKzS2hUg67fotxUibCT3v-Pe5PkvENX0ZcIaM1jYykJR86-AEpSaIE1xk24-QByQ7G1s8Pw-MSRdwnwHNArA0p4UCVwWFw0dOIGpgnhv3Y3AmkzRWO5GoOVIId4A)