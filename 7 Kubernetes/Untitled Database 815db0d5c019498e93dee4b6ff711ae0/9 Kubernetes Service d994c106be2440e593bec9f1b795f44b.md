# 9. Kubernetes Service

Created: July 7, 2022 2:10 PM

Ketika kita memiliki deployment atau pod pada cluster dan ingin mengaksesnya dari luar cluster misalnya webserver. Hal tersebut tidak dapat secara langsung kita lakukan. Oleh karena itu Service hadir untuk mengekspose resource yang ada pada cluster agar dapat diakses dari luar cluster.

Seperti yang kita tahu, pod pada cluster tidak selamanya akan ada. Maksudnya resource tersebut akan dibuat, lalu dihapus kembali. Pod memiliki IP masing masing saat dibuat. Masalah akan muncul apabila ingin suatu pod ingin berkomunikasi dengan pod lain sebut saja pod frontend dan backend. Jika salah satu dari pod tersebut resourcenya dihapus, yang dalam kata lain alamatnya tidak ada, otomatis pod tidak dapat saling berkomunikasi.

Service hadir untuk menyelesaikan masalah itu dengan membuat sebuah alamat yang mengacu kepada resource pada cluster.

Untuk membuat Service, diperlukan selector pada pod/resource yang bersangkutan. Coba lihat konfigurasi Service berikut.

```yaml
apiVersion: v1
kind: Pod                 
metadata:           
  name: webserver
  labels:
    app: nginx
spec:              
  containers:
  - name: webserver
    image: nginx:latest
    ports:
    - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: webserver-svc
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 80
```

Script dapat dilihat di:

[https://gist.github.com/sdcilsy/72716310116d4a6cfd208e8af0d9e382](https://gist.github.com/sdcilsy/72716310116d4a6cfd208e8af0d9e382)

File konfigurasi diatas akan membuat:

1. pod dengan image nginx yang berjalan pada port 80
2. Service yang mengexpose resource dengan label app=nginx pada port 8080 dengan tipe NodePort

Service tersebut akan mengekspose resource dengan selector **app=nginx** dengan type NodePort**.** Resource tersebut listen pada port **80** yang akan diarahkan pada port **8080** oleh Service tersebut.

Jika kita lihat resource **service/svc** akan ada service baru berikut dengan informasi cluster ip, dan **ports**.

[https://lh4.googleusercontent.com/tU75_doavjDTv4Cc7v2H2VbPmpGSXM74F_7lhR_qrF2lXHbg72ABMzEY55GGu5Xv40LbaRH6dN6S7jEMwxKQYl11EtezNL4xBZMe86IHb595dWGlcDbYZyCwJNwkq09Lk43wjNraCVFZZYXYFA](https://lh4.googleusercontent.com/tU75_doavjDTv4Cc7v2H2VbPmpGSXM74F_7lhR_qrF2lXHbg72ABMzEY55GGu5Xv40LbaRH6dN6S7jEMwxKQYl11EtezNL4xBZMe86IHb595dWGlcDbYZyCwJNwkq09Lk43wjNraCVFZZYXYFA)

Ada yang unik dari resource diatas. Kita mendapatkan port **30047**. Apa maksud port tersebut? Port tersebut adalah port dari setiap node yang ada di cluster. Maka jika kita akses alamat dari master/node cluster kita diakhiri dengan port tersebut, maka kita akan melihat service yang diexpose.

[https://lh4.googleusercontent.com/xicqIUo2h-g15K7cIh5WgSKlsdmkEGAzkLw2-rP0_BsbS0oVojSJ6yd0vmeqouXembIMS2r99FJ-VVRaTJS40CpFxp6ED8sgamzEeUxBat-zs1KgAnTlti27l3nNNPZqht3gUQwQtYtq1kk2kw](https://lh4.googleusercontent.com/xicqIUo2h-g15K7cIh5WgSKlsdmkEGAzkLw2-rP0_BsbS0oVojSJ6yd0vmeqouXembIMS2r99FJ-VVRaTJS40CpFxp6ED8sgamzEeUxBat-zs1KgAnTlti27l3nNNPZqht3gUQwQtYtq1kk2kw)

Namun jika cluster dibuat menggunakan kops pada AWS, kita tidak dapat mengaksesnya secara langsung. Kita perlu membuat rule inbound untuk dapat mengakses port yang dimaksud.

[https://lh5.googleusercontent.com/jd9H84kn2LFXQBnobG8JJHnjMKMm1AP8EuZhLa5iqJfeyWShR32oTBdAnLpp8jGMvYbY2G8PjcerNa90aLxmcJS1mjc3F9NGaoVAGYO3bhQ-3DgeXQt2z_nNdyNF9GwO6bYoM7QkwKTEPy-Snw](https://lh5.googleusercontent.com/jd9H84kn2LFXQBnobG8JJHnjMKMm1AP8EuZhLa5iqJfeyWShR32oTBdAnLpp8jGMvYbY2G8PjcerNa90aLxmcJS1mjc3F9NGaoVAGYO3bhQ-3DgeXQt2z_nNdyNF9GwO6bYoM7QkwKTEPy-Snw)

Port yang tersedia pada tipe [NodePort](https://kubernetes.io/docs/concepts/services-networking/service/#type-nodeport) secara default antara 30000-32767.

[https://lh6.googleusercontent.com/FYt8ioOOdFrWySJQHngHAzAYqhv99n1AOQ2BYaweygr9irVFiqGdlYJQ2VmwHKK9fD6PDTIX2aVv-OZ4_OYGyfgvxEiycflgL1Z9iS4CxW6h1B58j-tu4ABrcCeXFrHnIEePhlWFb9pYVibl6w](https://lh6.googleusercontent.com/FYt8ioOOdFrWySJQHngHAzAYqhv99n1AOQ2BYaweygr9irVFiqGdlYJQ2VmwHKK9fD6PDTIX2aVv-OZ4_OYGyfgvxEiycflgL1Z9iS4CxW6h1B58j-tu4ABrcCeXFrHnIEePhlWFb9pYVibl6w)

Selain tipe NodePort ada lagi [tipe lain](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) untuk mengekspose resouce cluster:

- ClusterIP: Mengekspos resource pada IP internal cluster yang artinya resource hanya dapat diakses dari dalam cluster. Tipe ini adalah ServiceType default.
- LoadBalancer: Mengekspos resource secara eksternal menggunakan load balancer yang diprovide oleh cloud.
- ExternalName: Memetakan Service ke DNS name.