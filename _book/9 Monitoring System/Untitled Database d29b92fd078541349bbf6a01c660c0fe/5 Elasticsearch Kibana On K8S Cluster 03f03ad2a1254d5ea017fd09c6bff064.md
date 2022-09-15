# 5. Elasticsearch Kibana On K8S Cluster

Created: July 25, 2022 1:54 PM

Saat menjalankan banyak service dan aplikasi pada cluster Kubernetes, logging dan monitoring pada cluster dapat membantu menganalisis data log besar dan resource yang dihasilkan dari Pod. Seperti yang disebutkan sebelumnya Kita dapat menggunakan tool monitoring untuk melakukannya. Salah satunya dengan Elasticsearch, Kibana dan Metricbeat.

Elasticsearch adalah search engine real-time, terdistribusi, dan scalable untuk pencarian dan analisis teks terstruktur yang lengkap. Elasticsearch biasanya digunakan untuk mengindeks dan mencari data log dalam jumlah besar, dan juga dapat digunakan untuk mencari berbagai jenis dokumen.

[https://lh3.googleusercontent.com/S0PTAQgeV_riisdE8NtsElZ0wGTji0bVVUKI8WSm2cgyLiPbmkNsgZAhkP1bw0H1CPjfpNgVxUW9iKfdoSfQT1WyHbQ_QOM5yqjHqVG2vSiFbQVOIIxbhJNBFF3qPi7Esnk118PitYfm3nc6ICnWVg](https://lh3.googleusercontent.com/S0PTAQgeV_riisdE8NtsElZ0wGTji0bVVUKI8WSm2cgyLiPbmkNsgZAhkP1bw0H1CPjfpNgVxUW9iKfdoSfQT1WyHbQ_QOM5yqjHqVG2vSiFbQVOIIxbhJNBFF3qPi7Esnk118PitYfm3nc6ICnWVg)

[https://lh5.googleusercontent.com/dsLAvYXnfKqUMwmcMr0oYVBMeWIeBpLTz9X4-xFIdIJB6vCilOR3Ya7OcyYIzcn_EE6pRdsdldPWFdAlCUKek4P8fDReQDl4Y_EVKnUbM7XUfG0JTQEkSQ18dm30-eCjj4WmNMaXQn-GZLCZ638XuQ](https://lh5.googleusercontent.com/dsLAvYXnfKqUMwmcMr0oYVBMeWIeBpLTz9X4-xFIdIJB6vCilOR3Ya7OcyYIzcn_EE6pRdsdldPWFdAlCUKek4P8fDReQDl4Y_EVKnUbM7XUfG0JTQEkSQ18dm30-eCjj4WmNMaXQn-GZLCZ638XuQ)

Elasticsearch biasanya digunakan dengan Kibana (data visualizer untuk memvisualisasikan data dan dasbor Elasticsearch). Kibana memungkinkan kita untuk menelusuri data log Elasticsearch melalui interface web dan membuat dasbor dan kueri dengan cepat dan mendapatkan insight dari aplikasi Kubernetes.

Dalam praktikum kali ini, kita akan menggunakan Metricbeat untuk mengumpulkan dan mengirim metric ke Elasticsearch. Kita akan menyiapkannya di cluster Kubernetes untuk mengekstrak metrics dari resource resource yang ada di cluster dan mengirimkannya ke Elasticsearch, tempat log akan diindeks dan disimpan.

Sebelum kita mulai praktek ini, ada prerequisites terlebih dahulu:

- Kubernetes cluster 1.23.x
    - master size : t2.xlarge
    - node size : t2.xlarge
- Helm 3.x (Baca kembali **Section Kubernetes - HELM**)
- Inbound rule for nodeport (baca kembali **Section Kubernetes - Service**)

Cluster yang dibuat sengaja menggunakan instance tipe t2.xlarge dengan 4 vCPU dan 16GB Memory karena stack ini membutuhkan resource yang sangat besar.

# **Elasticsearch Kibana**

Pada praktikum kali ini, seperti yang disebutkan diawal, kita akan menggunakan Elasticsearch, Kibana, dan Metricbeat untuk monitoring cluster Kubernetes.

[https://lh5.googleusercontent.com/-kuwqc1G8hL3WAeTRyJpqPjSTXZhuGGwE_g1iin_ZuIhfuHGoFSHoCRFlVEGyRRB8QWw5YKdjGQ8w44z75VMzCxDTY1Ijalo_VKTZ-1V0_vhrjaZoSPgWNqESk-Kd8T0rjzVC06f_HcvFd_cS6Vgdw](https://lh5.googleusercontent.com/-kuwqc1G8hL3WAeTRyJpqPjSTXZhuGGwE_g1iin_ZuIhfuHGoFSHoCRFlVEGyRRB8QWw5YKdjGQ8w44z75VMzCxDTY1Ijalo_VKTZ-1V0_vhrjaZoSPgWNqESk-Kd8T0rjzVC06f_HcvFd_cS6Vgdw)

Seperti yang kita lihat, Elasticsearch, Kibana dan Metricbeat berada pada cluster yang sama dimana tugas dari Metricbeat adalah untuk mengumpulkan metric dari kubernetes lalu mengirimkannya ke Elasticsearch untuk dibuat index lalu index tersebut ditampilkan oleh Kibana.

Metric yang dikirim Metricbeat berupa resource cluster seperti berapa jumlah memory pada cluster, CPU, penggunaan pada pod, dan lain lain.

Kita akan menginstal stack Elasticsearch Kibana Metricbeat ini menggunakan helm. Ini untuk memudahkan deployment.

## **Install Elasticsearch Chart**

Untuk menginstal Elasticsearch, ada beberapa Chart yang dapat ditemukan di [Artifacthub.io](https://artifacthub.io/packages/search?ts_query_web=elasticsearch&sort=relevance&page=1) namun pada praktikum kali ini kita akan menggunakan [Chart official](https://artifacthub.io/packages/helm/elastic/elasticsearch) dari **Elastic**.

```bash
helm repo add elastic https://helm.elastic.cohelm repo update
```

Kita dapat menginstal Elasticsearch chart menggunakan perintah berikut. Namun sebelum itu coba lihat terlebih dahulu [parameter](https://artifacthub.io/packages/search?ts_query_web=elasticsearch&sort=relevance&page=1) yang tertera pada repository.

```bash
helm install elasticsearch elastic/elasticsearch \
--set minimumMasterNodes=1 \
--set replicas=1
```

Perintah diatas, kita mendeploy Elasticsearch pada cluster dengan minimumMasterNode 1 dan replica 1.

Jika kita melihat pod, ada pod baru bernama elasticsearch-master-0. Tunggu beberapa saat agar pod benar benar running. Pastikan pod Elasticsearch ini sudah running sebelum melanjutkan ke langkah selanjutnya.

[https://lh5.googleusercontent.com/VmlcELD0m48hjO66MgFVPhqfj0u3_QsHNZswLtDXkj3qumSCzrHkBNfqvUC-hyxrsvFuPJwHldhZDISZrInTO_MfoIWt9POZlPd4Md_338xqLP4-MPRuB-o35iSvx7prK9ug_JAbK2OosHdIogv1Nw](https://lh5.googleusercontent.com/VmlcELD0m48hjO66MgFVPhqfj0u3_QsHNZswLtDXkj3qumSCzrHkBNfqvUC-hyxrsvFuPJwHldhZDISZrInTO_MfoIWt9POZlPd4Md_338xqLP4-MPRuB-o35iSvx7prK9ug_JAbK2OosHdIogv1Nw)

Jika kita lihat resource service, kita akan melihat ada 2 service baru yang ditambahkan. Jadi nanti ketika Kibana akan berkomunikasi dengan Elasticsearch, yang dipanggil adalah nama dari service Elasticsearch (elasticsearch-master).

[https://lh3.googleusercontent.com/523I2yKm5b3Z424HE6LcLgGSRl9MgOQWj86uhUY-weXrZGJQl1vMsmDkSA3VkuVW91nX4mHWhwVru4iTn5s8PSTB7pjYBbyFqWMxsPeAaRAdpR78hIPcI6Er9Hbpd8t7w93MdZrGVJYnI1_oycv3Bg](https://lh3.googleusercontent.com/523I2yKm5b3Z424HE6LcLgGSRl9MgOQWj86uhUY-weXrZGJQl1vMsmDkSA3VkuVW91nX4mHWhwVru4iTn5s8PSTB7pjYBbyFqWMxsPeAaRAdpR78hIPcI6Er9Hbpd8t7w93MdZrGVJYnI1_oycv3Bg)

Kita lakukan pengecekan apakah Elasticsearch sudah berjalan dengan baik dengan perintah berikut.

```bash
kubectl exec elasticsearch-master-0 -- curl elasticsearch-master-0:9200
```

Keterangan:

- elasticsearch-master-0	: nama pod Elasticsearch
- elasticsearch-master-0:9200	: service elasticsearch

Jika Elasticsearch sudah berjalan dengan baik, kita akan melihat output seperti berikut.

[https://lh3.googleusercontent.com/z0EegxLeLj0l3RCeAj67GlotqCVKIp_ax2KV3WFKcu-gCPzYqCUZaKWUEKAx-DCadDwYAoMHKPfur3CMohKcYAkaXpPQZEQmst0GGz13yCr0haV1SvwzvJLZLYUq2N7nMhlle0MzQrmU3YO0tkvx_Q](https://lh3.googleusercontent.com/z0EegxLeLj0l3RCeAj67GlotqCVKIp_ax2KV3WFKcu-gCPzYqCUZaKWUEKAx-DCadDwYAoMHKPfur3CMohKcYAkaXpPQZEQmst0GGz13yCr0haV1SvwzvJLZLYUq2N7nMhlle0MzQrmU3YO0tkvx_Q)

## **Install Metricbeat Chart**

Selanjutnya kita akan mendeploy Metricbeat pada cluster. Chart yang digunakan juga sama yaitu [chart official](https://artifacthub.io/packages/helm/elastic/metricbeat) dari elastic.

Kita dapat menginstal chart menggunakan command berikut.

```bash
helm install metricbeat elastic/metricbeat
```

[https://lh3.googleusercontent.com/m7GG0zJ8iytF4VBIbXwapJXnt3bMzgYRB68KLrIXUO0Dtf5oG-OGo5SlXFP3QCs3Vwj6FdAm_wvQQZoIscAFU1v9sJz3fzjgOe_KFpzIgsHRfo3yoR-PokQFY5hWCCWf_sea-lW7kVgarl7-jo-bPQ](https://lh3.googleusercontent.com/m7GG0zJ8iytF4VBIbXwapJXnt3bMzgYRB68KLrIXUO0Dtf5oG-OGo5SlXFP3QCs3Vwj6FdAm_wvQQZoIscAFU1v9sJz3fzjgOe_KFpzIgsHRfo3yoR-PokQFY5hWCCWf_sea-lW7kVgarl7-jo-bPQ)

Kita tidak usah mengatur parameter kali ini karena Metricbeat sudah mempunyai parameter default yaitu [ELASTICSEARCH_HOSTS](https://artifacthub.io/packages/helm/elastic/metricbeat?modal=values) untuk mengidentifikasi Elasticsearch untuk mengirim metric.

Pada saat instalasi selesai, maka kita akan dibuatkan **index** metricbeat pada elasticsearch. Untuk mengeceknya, bisa dengan command berikut.

```bash
kubectl exec elasticsearch-master-0 -- curl -X GET "elasticsearch-master-0:9200/_cat/indices/?v=true&s=index&pretty"
```

Command tersebut akan menghasilkan output dibawah. Index yang sudah dibuat bernama **metricbeat-7.17.1-2022.04.12-000001**.

[https://lh3.googleusercontent.com/OVDCZmCHCr_7LKPK_NNvegajv0NJIM0k7lX6zvr0nW40XjY8HCaqy3Z_ZYoP97Qs04Cu9Ft-hIajEFbyk0rY-T-eNJA0tpPbdo8A3OIjIoRA4teBkE1dTqN5AITaYMe9jF-Cyiy_2c2IycfLbp8iYg](https://lh3.googleusercontent.com/OVDCZmCHCr_7LKPK_NNvegajv0NJIM0k7lX6zvr0nW40XjY8HCaqy3Z_ZYoP97Qs04Cu9Ft-hIajEFbyk0rY-T-eNJA0tpPbdo8A3OIjIoRA4teBkE1dTqN5AITaYMe9jF-Cyiy_2c2IycfLbp8iYg)

## **Install Kibana Chart**

Selanjutnya kita akan menginstal [chart Kibana](https://artifacthub.io/packages/helm/elastic/kibana) untuk visualisasi data. Kita dapat menginstalnya dengan command berikut.

```bash
helm install kibana elastic/kibana \--set service.type=NodePort
```

Kita tetapkan [service.type](https://artifacthub.io/packages/helm/elastic/kibana?modal=values)=NodePort agar Kibana dapat diakses dari luar cluster. Untuk setting inbound rule, baca kembali **Section Kubernetes** mengenai **Service**.

Kita akan mendapatkan beberapa pod yang sudah dibuat oleh Chart. Pastikan semua pod running dengan baik.

[https://lh6.googleusercontent.com/MgYOl6vgVREMKz97FYBu6qz3vZfuzM_wRvdOpcqZ4i9xcvpbCewD55PKwQno_Sm9xuE7VePKJCL_lwhAekptWTcjE87zvvUPZn2DFpTJe5j7WRyRCsZLp2PiLoNlCIoAfB3idVOOpFr8qbw5D6TGeQ](https://lh6.googleusercontent.com/MgYOl6vgVREMKz97FYBu6qz3vZfuzM_wRvdOpcqZ4i9xcvpbCewD55PKwQno_Sm9xuE7VePKJCL_lwhAekptWTcjE87zvvUPZn2DFpTJe5j7WRyRCsZLp2PiLoNlCIoAfB3idVOOpFr8qbw5D6TGeQ)

Karena kita menset service.type pada Kibana menjadi NodePort, kita akan mendapatkan port NAT yang digunakan untuk mengakses service. Pada kasus ini adalah **30769**.

[https://lh3.googleusercontent.com/L2k2JKvomjZDmIHGyvJc1EcXKxob8O8CJYv0xOFatQUGg2XzA21RJQr_N38ihtZwklNzhlEHs5Ay9xoRB3ySUc12ZWhOtD0ImOfyzHViTAyOGWvfeKXwjowVSTZm2enVMJOEIM9BIUzK2JWLnsLLEg](https://lh3.googleusercontent.com/L2k2JKvomjZDmIHGyvJc1EcXKxob8O8CJYv0xOFatQUGg2XzA21RJQr_N38ihtZwklNzhlEHs5Ay9xoRB3ySUc12ZWhOtD0ImOfyzHViTAyOGWvfeKXwjowVSTZm2enVMJOEIM9BIUzK2JWLnsLLEg)

Kita bisa mengakses Kibana dengan IP/DNS public dari instance master diikuti dengan port NAT dari service.

Maka tampilan dari Kibana adalah sebagai berikut. Klik saja **Explore on my own**.

[https://lh3.googleusercontent.com/3pcPACTN4Wi9ojgHt3FRkXb1u98TKVqIC7KhpxHgjfgVW16w-TUFD-pPdbkjreUZHeC1n37O3rMmvsuQpptRrTxQcHPZUyIOlYVTbT02hxMilEDPY5lU-lIjG6te2VCPhKDN4eAd8EzXO_wjf223JQ](https://lh3.googleusercontent.com/3pcPACTN4Wi9ojgHt3FRkXb1u98TKVqIC7KhpxHgjfgVW16w-TUFD-pPdbkjreUZHeC1n37O3rMmvsuQpptRrTxQcHPZUyIOlYVTbT02hxMilEDPY5lU-lIjG6te2VCPhKDN4eAd8EzXO_wjf223JQ)

Hal pertama yang dilakukan adalah membuat **kibana index** dari index yang ada pada elasticsearch.

Caranya klik garis 3 pada pojok kiri atas lalu klik **Stack Management**.

[https://lh4.googleusercontent.com/q2H0h1w_y7xrNT-_YKsBTih_P32vgiIYlIDrbRlLbYsXRYIZfhKIbK2Jtxhlewp4gs0mFVesknkNxHkBirDxe2O2s1xeyPBSIvpQRgqVmVAS9dAokxJX8fLdj0NaB4rqZVL4w3YemE_KHbPbs3zOpg](https://lh4.googleusercontent.com/q2H0h1w_y7xrNT-_YKsBTih_P32vgiIYlIDrbRlLbYsXRYIZfhKIbK2Jtxhlewp4gs0mFVesknkNxHkBirDxe2O2s1xeyPBSIvpQRgqVmVAS9dAokxJX8fLdj0NaB4rqZVL4w3YemE_KHbPbs3zOpg)

Disini kita akan melihat index metricbeat pada elasticsearch. Index ini akan kita buat kibana index supaya index tersebut dapat divisualisasikan pada Kibana.

[https://lh6.googleusercontent.com/WfcUgw9eFXRlVbQ6JzC-kAd7lAdm9jm4YmaqLkvf_XokvX3ZKqDG9uqLw2Uclm9OjDO4cO0xaFF-Z4KGnxohZk52wzjrS3Uy5d32J97XjdSG06Lu1maJTKiaK5O2T-9panl189do2sviwjdms2rgWQ](https://lh6.googleusercontent.com/WfcUgw9eFXRlVbQ6JzC-kAd7lAdm9jm4YmaqLkvf_XokvX3ZKqDG9uqLw2Uclm9OjDO4cO0xaFF-Z4KGnxohZk52wzjrS3Uy5d32J97XjdSG06Lu1maJTKiaK5O2T-9panl189do2sviwjdms2rgWQ)

Dibawah menu Kibana, klik **Index Patterns** lalu **Create Index Pattern.**

[https://lh5.googleusercontent.com/mea0MR9xou8r1GU8VIC8yCV4pyxC7f7vQ_KgjIRfoH-6ElBXwR9saq87RRmFbkg8AszeTpYuk7tWsIs0Fb3XvNMdbXFZyQ3A94gz1h4iVuaIMocPZ5HPqIOv_La5Y-1Yal4-U5OULNegv8_L7jVt8Q](https://lh5.googleusercontent.com/mea0MR9xou8r1GU8VIC8yCV4pyxC7f7vQ_KgjIRfoH-6ElBXwR9saq87RRmFbkg8AszeTpYuk7tWsIs0Fb3XvNMdbXFZyQ3A94gz1h4iVuaIMocPZ5HPqIOv_La5Y-1Yal4-U5OULNegv8_L7jVt8Q)

Isikan nama dari index yang ada diikuti dengan character * untuk memasukan semua index (jika ada). Nama dari index pattern adalah **metricbeat-7.17.1-***. Tak lupa pilih **Timestamp filed** menjadi **@timestamp**. Ini field timestamp default yang ada pada saat chart di install. Klik **Create index pattern.**

[https://lh4.googleusercontent.com/vqX6YKpIM81VawTGzgVkequQeryz1J19hV_qxC3niNyfbDjfuYrPUIbTAB3-76uD_3pWvWpzI8SKeF8hQLNWQ-_SyL7HAK_s9IohDtdfDcuK6r3KlyakQbQ-Z9FzXIGPbFJqojz-NGL0aKLCeNMttw](https://lh4.googleusercontent.com/vqX6YKpIM81VawTGzgVkequQeryz1J19hV_qxC3niNyfbDjfuYrPUIbTAB3-76uD_3pWvWpzI8SKeF8hQLNWQ-_SyL7HAK_s9IohDtdfDcuK6r3KlyakQbQ-Z9FzXIGPbFJqojz-NGL0aKLCeNMttw)

Setelah itu kita beralih ke menu **Discover** yang ada pada menu disamping kiri. Kita akan melihat metric metric yang dikirim oleh Metricbeat ke Elasticsearch.

[https://lh3.googleusercontent.com/0GrZncmcqGL4MieDQUTJ1s9jhyA4xxeYiw6NyW9i719JYCTN00lbzfROsG3XGBrYj4lkfLxMphyynfLKWabECyXJAzIEahpgHuR0uMoAoONvka8ilibAGKIM-B_FZ-GS--fZ_7Kn2et8TJP8MegGrA](https://lh3.googleusercontent.com/0GrZncmcqGL4MieDQUTJ1s9jhyA4xxeYiw6NyW9i719JYCTN00lbzfROsG3XGBrYj4lkfLxMphyynfLKWabECyXJAzIEahpgHuR0uMoAoONvka8ilibAGKIM-B_FZ-GS--fZ_7Kn2et8TJP8MegGrA)

Untuk mendemonstrasikan kasus penggunaan dasar Kibana menjelajahi log terbaru untuk node yang diberikan, kita akan menggunakan node penghitung minimal yang mencetak nomor berurutan ke stdout.

Buat file konfigurasi dengan nama counter.yaml dengan menggunakan perintah berikut

```bash
nano p-counter-pod.yaml
```

Masukan konfigurasi berikut

```bash
apiVersion: v1
kind: Pod
metadata:
  name: counter
spec:
  containers:
  - name: count
    image: busybox
    args: [/bin/sh, -c,
            'i=0; while true; do echo "$i: $(date)"; i=$((i+1)); sleep 1; done']
```

script dapat dilihat di [https://gist.github.com/sdcilsy/6f43372d9a1b4abe9ff2dcd976d21160](https://gist.github.com/sdcilsy/6f43372d9a1b4abe9ff2dcd976d21160)

Save dan tutup text editor nano dengan menekan CTRL+X lalu tekan Y dan enter.

Jalan menggunakan perintah berikut

```bash
kubectl apply -f p-counter-pod.yaml
```

Dari halaman Discover, di bagian **search**, masukkan **kubernetes.pod.name : "counter"**. Lalu klik tombol refresh seperti pada gambar untuk memfilter data log.

[https://lh3.googleusercontent.com/pOxCp8LO3KnN8q8RUF3yI1oV8kQSgFA4CDDUWE5JWcq7Pra09vvB77abJTKJYSn077LfyYDd0fSQmsR-dVxitta0aBfGNVhVpLOqSG1y0RfLYa-n9uZYGT55xpyWgNmL41agGNHoF-qoFaburicrqg](https://lh3.googleusercontent.com/pOxCp8LO3KnN8q8RUF3yI1oV8kQSgFA4CDDUWE5JWcq7Pra09vvB77abJTKJYSn077LfyYDd0fSQmsR-dVxitta0aBfGNVhVpLOqSG1y0RfLYa-n9uZYGT55xpyWgNmL41agGNHoF-qoFaburicrqg)

Klik salah satu bar yang ada untuk melihat lebih detail log metric sesuai query. Kita bisa melihat log metric yang dikirim berisi resource memory dari pod, dan lain sebagainya. Coba lihat field lain yang ada.

[https://lh4.googleusercontent.com/oTaDl_sEy1Y9CB_RiXlXI6tno6u9qznddX4f9OLisNM6pZTMLeoS2Kf1CgI_FbMdXXFi1lk5J8VT-o_avKZqYurcUkDHcX7TY5oRafWkgQfhUPOVfaxRkFxYIxJdRBS_9ZkheMn-X39QMt9q0oVE9Q](https://lh4.googleusercontent.com/oTaDl_sEy1Y9CB_RiXlXI6tno6u9qznddX4f9OLisNM6pZTMLeoS2Kf1CgI_FbMdXXFi1lk5J8VT-o_avKZqYurcUkDHcX7TY5oRafWkgQfhUPOVfaxRkFxYIxJdRBS_9ZkheMn-X39QMt9q0oVE9Q)