# 6. Prometheus dan Grafana Stack

Created: July 25, 2022 2:51 PM

Pada praktikum kali ini, kita akan menggunakan Prometheus untuk mengirim metric dan Grafana untuk visualisasi data yang digunakan untuk memantau cluster kubernetes.

[https://lh5.googleusercontent.com/WG1vp5R5e7MG-Nr3e94PGEuPfP95r8OGFdEDJnDWX9EWiQ_ga3F3qO6l_17Wz-C4q4peRjHI09L4LaGOBE3QXpqqzg6SYOId8KjI-S3aHEYTrXLeKjpQjiDFxLG97W9pdB37SPPOvxt3415oys0wDA](https://lh5.googleusercontent.com/WG1vp5R5e7MG-Nr3e94PGEuPfP95r8OGFdEDJnDWX9EWiQ_ga3F3qO6l_17Wz-C4q4peRjHI09L4LaGOBE3QXpqqzg6SYOId8KjI-S3aHEYTrXLeKjpQjiDFxLG97W9pdB37SPPOvxt3415oys0wDA)

Prometheus adalah perangkat monitor dan sistem alerting open source yang awalnya dibuat di SoundCloud. Sejak didirikan pada tahun 2012, banyak perusahaan dan organisasi telah mengadopsi Prometheus, dan proyek tersebut memiliki komunitas pengembang dan pengguna yang sangat aktif. Sekarang, Prometheus adalah proyek open source independen dan dikelola secara independen dari perusahaan mana pun. Untuk menekankan poin ini dan memperjelas struktur tata kelola proyek, Prometheus bergabung dengan Cloud Native Computing Foundation pada tahun 2016, yang merupakan proyek terkelola kedua setelah Kubernetes. Biasanya juga, Prometheus ini dipasangkan dengan Grafana yang mampu menampilkan beragam jenis grafik yang bermanfaat dan juga memikat.

Sebelum memulai praktikum ada prerequisites :

- Kubernetes cluster 1.23.x
    - master size : t2.xlarge
    - node size : t2.xlarge
- Helm 3.x (Baca kembali **Section Kubernetes - HELM**)
- Inbound rule for nodeport (baca kembali **Section Kubernetes - Services**)

Cluster yang dibuat sengaja menggunakan instance tipe t2.xlarge dengan 4 vCPU dan 16GB

Memory karena stack ini membutuhkan resource yang sangat besar.

# **Install Prometheus Chart**

Prometheus mengambil metric dari **kube-state-metrics**. **Kube-state-metrics** adalah layanan sederhana yang terhubung dengan server Kubernetes API dan menghasilkan metrik tentang status objek. Objek tersebut seperti deployment, pod dan lain lain.

**Kube-state-metrics** adalah tentang menghasilkan metrik dari objek Kubernetes API tanpa modifikasi. Ini memastikan bahwa kube-state-metrics memiliki stabilitas yang sama dengan objek API Kubernetes itu sendiri. Metrik diekspor pada endpoint HTTP “/metrik” dengan port 8080. Metrik ini berbentuk plain text.

Berikut adalah beberapa objek utama yang dapat Anda pantau dengan metrik status kubernetes:

- Memantau status node, kapasitas node (CPU dan memori)
- Memantau replicaset (desired / available / unavailable)
- Monitor status pod (wait, running, ready, dll)
- Monitor request dan limit resource.
- Monitor job & status Cronjob

Sebelum menginstal Prometheus pada cluster, kita tambahkan repository chart terlebih dahulu.

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

Lalu kita bisa install Prometheus dengan command berikut.

```bash
helm install prometheus prometheus-community/prometheus
```

Jika Deployment berhasil, maka kita akan melihat beberapa pod baru sudah dibuat. Pastikan semua pod sudah running dengan baik.

[https://lh3.googleusercontent.com/4N7I-cKdxsCv0CLAxRM0yQVazUlDNx80ZOMFXL0IviSabFffDosR7v8gZU9I6_vOyrvXDS9jrv1gVQsqO9xPakKYLVcwHJSFm77wPSsj0KU9okN2knxtPBeXClv9URA5PtsNB0aQRtpQVz9YkdplJg](https://lh3.googleusercontent.com/4N7I-cKdxsCv0CLAxRM0yQVazUlDNx80ZOMFXL0IviSabFffDosR7v8gZU9I6_vOyrvXDS9jrv1gVQsqO9xPakKYLVcwHJSFm77wPSsj0KU9okN2knxtPBeXClv9URA5PtsNB0aQRtpQVz9YkdplJg)

Pada Service juga dapat kita lihat seperti berikut.

[https://lh3.googleusercontent.com/ircHCNI7XxNo1QDL9w_F12KPAh2QUa3ew18jq-CJkTnDQt62Zo2Y0_VD4pK5zQmBiDw2h9OLutQv5iOdPMkpMaXTvC18u33ycstGe4bshnOASqjZGnTqkxzRDoWdwGxhNv4cZDrtEZZgV9u-edDd9g](https://lh3.googleusercontent.com/ircHCNI7XxNo1QDL9w_F12KPAh2QUa3ew18jq-CJkTnDQt62Zo2Y0_VD4pK5zQmBiDw2h9OLutQv5iOdPMkpMaXTvC18u33ycstGe4bshnOASqjZGnTqkxzRDoWdwGxhNv4cZDrtEZZgV9u-edDd9g)

# **Install Grafana Chart**

Grafana merupakan sebuah software web console berbasis open source yang berfungsi membaca sebuah data metrics untuk dibuat menjadi sebuah grafik atau sebuah data tertulis. Grafana banyak sekali digunakan untuk melakukan analisis data dan monitoring, terutama pada environment berbasis container. Grafana mendukung banyak storage backends yang berbeda untuk data time series (Source Data). Setiap source data memiliki Query Editor tertentu yang disesuaikan untuk fitur dan kemampuan tertentu.

Kita tambahkan repository chart terlebih dahulu.

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
```

Lalu kita bisa install Prometheus dengan command berikut.

```bash
helm install grafana grafana/grafana \
--set persistence.enabled=true \
--set service.type=LoadBalancer
```

Parameter yang diubah adalah **persistence.enabled=true** supaya grafana membuat persistence volume agar data tetap ada. Lalu **service.type=LoadBalancer** untuk dapat mengakses Grafana dari luar cluster dengan Load Balancer.

Jika kita lihat ada pod baru bernama grafana dari deployment grafana. Pastikan pod nya sudah running dengan baik.

[https://lh5.googleusercontent.com/UCFoar1qBP_Mn0yehQF_FEJpKeK7lijoL7uM2dt-0SPiytEw7fnjKUr6qYYsF_5ZVF4PTaVaClBer7Wy2s01mIZTnwlavTxMX_dJQHX_xniraHr8ACHsqF9XR3QxOlU3mWw9kGMwkYZMm82FmzoIGg](https://lh5.googleusercontent.com/UCFoar1qBP_Mn0yehQF_FEJpKeK7lijoL7uM2dt-0SPiytEw7fnjKUr6qYYsF_5ZVF4PTaVaClBer7Wy2s01mIZTnwlavTxMX_dJQHX_xniraHr8ACHsqF9XR3QxOlU3mWw9kGMwkYZMm82FmzoIGg)

Karena service yang digunakan adalah LoadBalancer, maka kita akan mendapatkan external IP seperti berikut. Mohon tunggu apabila status **<pending>**.

[https://lh3.googleusercontent.com/rctPzigt6Vcaaa3vu_Kd6Mgw96GhmFKVx1YUqgyAJ_Wy4dxOha_HSYn3kDVtfH0OOwfrwkD1AdcvSO9JsWlyG2OzzKOvpOuEHEmqNlr7kefHPlxbibaXArmkYi41CugquQPaaxVTCOWMDFpEHefl1A](https://lh3.googleusercontent.com/rctPzigt6Vcaaa3vu_Kd6Mgw96GhmFKVx1YUqgyAJ_Wy4dxOha_HSYn3kDVtfH0OOwfrwkD1AdcvSO9JsWlyG2OzzKOvpOuEHEmqNlr7kefHPlxbibaXArmkYi41CugquQPaaxVTCOWMDFpEHefl1A)

Grafana menggunakan authentication username password untuk login kedalam aplikasi. Secara default username Grafana adalah **admin** dan passwordnya sudah ada didalam **Secret** Oleh karena itu kita dapat mengambil password dengan perintah berikut.

```bash
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

[https://lh4.googleusercontent.com/ZV-KoYt-kh3AOGQBl4MFwoqa12oTK1j46gaggsskIvTSeUriRQ4CWWXbRV3yiZ68vUpTYV0Yztngl0JJyXiUEN_t9H2YKDs7ZoCccBMJv81X0-Yxtz_PisWvE9ASKIf4SO7C9khK6MqurmVPsL3h-Q](https://lh4.googleusercontent.com/ZV-KoYt-kh3AOGQBl4MFwoqa12oTK1j46gaggsskIvTSeUriRQ4CWWXbRV3yiZ68vUpTYV0Yztngl0JJyXiUEN_t9H2YKDs7ZoCccBMJv81X0-Yxtz_PisWvE9ASKIf4SO7C9khK6MqurmVPsL3h-Q)

Setelah mendapatkan password, akses External IP dari service Grafana lalu masukan **username : admin**, dan password yang sudah didapatkan.

[https://lh4.googleusercontent.com/j4JJchpIM7399zn_CkbVcv-xOlkMbyIpLnpCIGQPSkJLfhCuhAAk2KfogCSyyUDFeEdmYfLaC6E6ILCp8jAF7i7jOTVJk8mQsB--nnmadh__cGTNsdrKuKGhahcHAm3M4i2szrYSqdwIjm-TLLOiXw](https://lh4.googleusercontent.com/j4JJchpIM7399zn_CkbVcv-xOlkMbyIpLnpCIGQPSkJLfhCuhAAk2KfogCSyyUDFeEdmYfLaC6E6ILCp8jAF7i7jOTVJk8mQsB--nnmadh__cGTNsdrKuKGhahcHAm3M4i2szrYSqdwIjm-TLLOiXw)

Setelah Login, kita akan melihat Dashboard Home Grafana. Langkah selanjutnya adalah untuk menambah datasource Prometheus. Ini berguna sebagai datasource untuk Dashboard yang akan kita buat. Klik **Data Sources**.

[https://lh4.googleusercontent.com/1lbGJcMogaxlpoU8_3pGjxrvdCjKigS7_vnnsFYEmwnjCj7RoOuLN9SEokc4EQy7IcaveDYm8VTjR24FJjwLQTMk-BLENdmaH0EX3yTiyAw4evJUhBsrBAWl6huh6lJjFztZCjSFxsCuwXSBtGWONQ](https://lh4.googleusercontent.com/1lbGJcMogaxlpoU8_3pGjxrvdCjKigS7_vnnsFYEmwnjCj7RoOuLN9SEokc4EQy7IcaveDYm8VTjR24FJjwLQTMk-BLENdmaH0EX3yTiyAw4evJUhBsrBAWl6huh6lJjFztZCjSFxsCuwXSBtGWONQ)

Setelah itu pilih jenis datasource. Ada banyak sekali datasource yang disediakan pada grafana ini. Kita pilih **Prometheus**.

[https://lh3.googleusercontent.com/HcXabzye0qTZxyIFJp3MtUDepORGi-TwpQbTdeomFOh4M2dXads_Uxxc8dyA0vGC8ja4MGKK0GaQdlUR_j6i9YK900sa8N9MIV7UFtC-Cxp2vBSsdsfTXpybs-nSragOEvuOGwA8g__7R8aFQGi8RQ](https://lh3.googleusercontent.com/HcXabzye0qTZxyIFJp3MtUDepORGi-TwpQbTdeomFOh4M2dXads_Uxxc8dyA0vGC8ja4MGKK0GaQdlUR_j6i9YK900sa8N9MIV7UFtC-Cxp2vBSsdsfTXpybs-nSragOEvuOGwA8g__7R8aFQGi8RQ)

Lalu kita akan mengkonfigurasi Datasource Prometheus tadi dengan memasukan nama, dan URL dari Prometheus. Kita isi URL dengan nama **service** **prometheus** yaitu **http:/./prometheus-server** seperti dibawah. Karena kita tidak menggunakan autentikasi dan lain sebagainya, maka setting lain kita abaikan.

[https://lh4.googleusercontent.com/IMQOQVjAaJssh2r30MdLD-Tt0MLFBPZBCzoVIYu6CX2Nzjmhgo8B_KgHOT1setY5-i13MoWigOutB4ScJVhv3L-GgrK3kfeoDiI8WmqXbwe9VPal-Xy9wP5v3xDFiLObJgJCMKAZBWCgwQhSOOEByw](https://lh4.googleusercontent.com/IMQOQVjAaJssh2r30MdLD-Tt0MLFBPZBCzoVIYu6CX2Nzjmhgo8B_KgHOT1setY5-i13MoWigOutB4ScJVhv3L-GgrK3kfeoDiI8WmqXbwe9VPal-Xy9wP5v3xDFiLObJgJCMKAZBWCgwQhSOOEByw)

Jika kita scroll kebawah, akan ada tombol **Save & test**. Ini berguna untuk menyimpan konfigurasi datasource dan mengetes koneksi ke datasource tersebut. Jika datasource valid maka akan ada peringatan **Data source is working**. Klik  **Save & test**.

[https://lh4.googleusercontent.com/8zbC2NK4wZP1yanbrNDzrRZGV6d-YFyXTPQZScXGl_Cdv-3usC434EQcX9DqVABpEW9lbwldvOSUW2m4XX4Yelkmq6GJgimaF6CcoAHTb63LacszKsDmJaqD2GAePmsf-PTqLBYFCTDJuv-Fh89jOg](https://lh4.googleusercontent.com/8zbC2NK4wZP1yanbrNDzrRZGV6d-YFyXTPQZScXGl_Cdv-3usC434EQcX9DqVABpEW9lbwldvOSUW2m4XX4Yelkmq6GJgimaF6CcoAHTb63LacszKsDmJaqD2GAePmsf-PTqLBYFCTDJuv-Fh89jOg)

Kita kembali ke Dashboard Home, kita akan membuat Dashboard untuk visualisasi metric dari Cluster kubernetes dari Prometheus.

Hover tanda (+) lalu klik Import.

[https://lh5.googleusercontent.com/Gc-ExX_6Er6hPgvHFCWKeHjy2cROdHJY04rPQK3mMajoi_uyrCfkJ_ih9yR7jqZstAbCqITu9l7ZBYAQVTIfz2km6YrqxrVh_OWDQ_bOOLrcyBsuF0sxk3WBNB7kDP0VFgErhedXmujxmVUaOMNi7Q](https://lh5.googleusercontent.com/Gc-ExX_6Er6hPgvHFCWKeHjy2cROdHJY04rPQK3mMajoi_uyrCfkJ_ih9yR7jqZstAbCqITu9l7ZBYAQVTIfz2km6YrqxrVh_OWDQ_bOOLrcyBsuF0sxk3WBNB7kDP0VFgErhedXmujxmVUaOMNi7Q)

Setelah itu akan ada konfigurasi dashboard yang harus diisi. Kita memiliki 2 opsi untuk import Dashboard:

1. Import dari [grafana.com](https://grafana.com/grafana/dashboards/) yang berisikan dashboard dari comunity. Caranya dengan memasukan ID dashboard pada field **Import via grafana.com**.
2. Import menggunakan json dari Dashboard yang sudah di export sebelumnya.

Kali ini kita menggunakan opsi ke 2 yaitu menggunakan json dan sudah kami siapkan dashboard untuk digunakan. Panel JSON bisa dilihat di  [https://gist.github.com/sdcilsy/9f4604a1906735e51bcd2b7ca433e64d](https://gist.github.com/sdcilsy/9f4604a1906735e51bcd2b7ca433e64d).

Caranya kita bisa meng-copy json dari gist diatas, lalu mem-paste kedalam field **Import via panel json**. Setelah itu klik **Load**.

[https://lh6.googleusercontent.com/Vq5aBXq7J3OutAvdqbiIX7PztQz_BpT94zEeumuQ_bPEruPUQHxaFcZ2CIHoih1gHPQtyXBiB6jnpqHtYxEHjJL8BymOzxDbSbfKkE2IPWynkT261D8smbVm2hd3oBKKE9GTQ60znQG01vcL6d6HHw](https://lh6.googleusercontent.com/Vq5aBXq7J3OutAvdqbiIX7PztQz_BpT94zEeumuQ_bPEruPUQHxaFcZ2CIHoih1gHPQtyXBiB6jnpqHtYxEHjJL8BymOzxDbSbfKkE2IPWynkT261D8smbVm2hd3oBKKE9GTQ60znQG01vcL6d6HHw)

Nantinya akan muncul konfirmasi untuk mengimport Dashboard seperti dibawah. Pilih Datasource **Prometheus** yang sudah dibuat sebelumnya. Klik **Import**.

[https://lh4.googleusercontent.com/PiQSkeKXtnqmKXv1sM6mwnMWRGU8ZpVn5Y-AFDSvcZ-2oGRMU2gYc8FvzeX_yHE-9SmvOWIyG684slzMyIQKrLLhNu9t8AxrkDlz4oGP56wbA7T1Hx2LOzJzCDxkfFcvlVYBmlu81TVXQ-yUvfWdQw](https://lh4.googleusercontent.com/PiQSkeKXtnqmKXv1sM6mwnMWRGU8ZpVn5Y-AFDSvcZ-2oGRMU2gYc8FvzeX_yHE-9SmvOWIyG684slzMyIQKrLLhNu9t8AxrkDlz4oGP56wbA7T1Hx2LOzJzCDxkfFcvlVYBmlu81TVXQ-yUvfWdQw)

Setelah import berhasil, kita bisa lihat hasilnya yaitu dashboard dengan informasi metric cluster seperti Memory, CPU usage, dan Network.

[https://lh5.googleusercontent.com/h3quruGzFTGMiqg5jRAeErG8wA7jg17wdwgZHZxOXTtA2h2qrMlM5dHB3ctpRO_pHp8xlxg9-KMvspCfhHQLkjpSRAxLVJwCg8hF_rBZnmCz2ZpZdS1J7INVav_3AsJzW873NS8hmE8xHB6ZlsY6tA](https://lh5.googleusercontent.com/h3quruGzFTGMiqg5jRAeErG8wA7jg17wdwgZHZxOXTtA2h2qrMlM5dHB3ctpRO_pHp8xlxg9-KMvspCfhHQLkjpSRAxLVJwCg8hF_rBZnmCz2ZpZdS1J7INVav_3AsJzW873NS8hmE8xHB6ZlsY6tA)