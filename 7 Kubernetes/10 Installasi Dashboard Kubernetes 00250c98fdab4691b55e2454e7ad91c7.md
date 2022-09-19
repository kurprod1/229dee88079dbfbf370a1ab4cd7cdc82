# 10. Installasi Dashboard Kubernetes

Created: July 7, 2022 2:11 PM

Untuk mengakses dashboard dari kubernetes maka kita dapat menjalankan perintah seperti di bawah ini.

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.0/aio/deploy/recommended.yaml
```

atau jika versi sudah terupdate, bisa dilihat di link berikut

[https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/#deploying-the-dashboard-ui](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/#deploying-the-dashboard-ui)

karena kita menggunakan Gossip DNS, maka saat kita ingin mengakses kedalam cluster, kita harus mengakses **Load Balancer** nya. Load Balancer ini sudah dibuat oleh kops, namun ada batasan untuk akses port port tertentu. Oleh karena itu, kita akan membuat inbound rule baru untuk cluster kita.

Caranya buka menu Load Balancer, lalu pilih **api-cilsy-k8s-local-******* lalu klik **sg-0571***********.

![https://lh5.googleusercontent.com/pehbiABIfsfoZ6hdQE1NrX92_XIzEplVS14GVjVWZ8BEdIyUnRTzFLwerd-3Lo5LeIVUM5t-du1AtaolopseLRmwgsmT0dTSAk4rlaYsvYzITrvcCxMFRtWeYAQFOXlN1YeZ6Gs_ks4rpsFsDA](https://lh5.googleusercontent.com/pehbiABIfsfoZ6hdQE1NrX92_XIzEplVS14GVjVWZ8BEdIyUnRTzFLwerd-3Lo5LeIVUM5t-du1AtaolopseLRmwgsmT0dTSAk4rlaYsvYzITrvcCxMFRtWeYAQFOXlN1YeZ6Gs_ks4rpsFsDA)

Kita akan melihat ada 2 Security Group yaitu **master** dan **api**. Yang digunakan oleh Load Balancer adalah api, jadi kita pilih yang api, lalu klik **edit inbound rules**.

![https://lh5.googleusercontent.com/VcKRzjdgG5__QCDBbeInyiiMFj0LC4GNkilQkEqayPtd6DzTZlkOp5n9M8xdeXoTaBcc9C6nRGug-14w70WAzg5fBHb-l0sDXLceIoPCl5wZ0SLw4GcRgIdRg82I3BhrjcHBo2nwx-CEt0BPbg](https://lh5.googleusercontent.com/VcKRzjdgG5__QCDBbeInyiiMFj0LC4GNkilQkEqayPtd6DzTZlkOp5n9M8xdeXoTaBcc9C6nRGug-14w70WAzg5fBHb-l0sDXLceIoPCl5wZ0SLw4GcRgIdRg82I3BhrjcHBo2nwx-CEt0BPbg)

Ubah menjadi seperti ini. Setelah itu, **save rule**.

![https://lh4.googleusercontent.com/_UX525HcezihmYtmJ9u2w7PwVAuQZVH920GTBB5zhFLBmipsbHcQGnPWmAEyMsMZmTi20gkNGerB7GpyZH0EVpPSc1It_zQpjKbEBS3_YCBIUlrzDUtOKkIW9Y47EpXzoCStvF5xjX9D4j5u0A](https://lh4.googleusercontent.com/_UX525HcezihmYtmJ9u2w7PwVAuQZVH920GTBB5zhFLBmipsbHcQGnPWmAEyMsMZmTi20gkNGerB7GpyZH0EVpPSc1It_zQpjKbEBS3_YCBIUlrzDUtOKkIW9Y47EpXzoCStvF5xjX9D4j5u0A)

Setelah itu, karena kita akan mengakses Dashboard **diluar Cluster**, maka kita membutuhkan account saat kita menggunakan Dashboard.

```bash
kubectl create serviceaccount dashboard-admin-sa
```

![https://lh5.googleusercontent.com/W5wnEftMs5sLVAI4LF7Ogwy-9B-v3lV6RrdjzmQRh57-M5MvBKvsw-vhIsA4SZVBQhwCUPLR75A0TKF_pS-a8T3cvh0DttvqhrQIP8b7p4yTy5ARq2MTMQ5St8BZ_dE_hHK2xYm3iSr-4NhY8g](https://lh5.googleusercontent.com/W5wnEftMs5sLVAI4LF7Ogwy-9B-v3lV6RrdjzmQRh57-M5MvBKvsw-vhIsA4SZVBQhwCUPLR75A0TKF_pS-a8T3cvh0DttvqhrQIP8b7p4yTy5ARq2MTMQ5St8BZ_dE_hHK2xYm3iSr-4NhY8g)

```bash
kubectl create clusterrolebinding dashboard-admin-sa --clusterrole=cluster-admin --serviceaccount=default:dashboard-admin-sa
```

![https://lh4.googleusercontent.com/t3BLVeywjW45iMair0PxQlmEGEdgbSHL9EFu5KsP1H3yvSPgx3F5gKqRmuQiqa-gKvLsKpvPL8xxmk55LFR9-T5ApMfVBQ4N3pxjtoGQqSe_T9yjLMMss3ydlmj10iqfgclB4cwGtyBBjBszmA](https://lh4.googleusercontent.com/t3BLVeywjW45iMair0PxQlmEGEdgbSHL9EFu5KsP1H3yvSPgx3F5gKqRmuQiqa-gKvLsKpvPL8xxmk55LFR9-T5ApMfVBQ4N3pxjtoGQqSe_T9yjLMMss3ydlmj10iqfgclB4cwGtyBBjBszmA)

setelah itu, kita lihat secret (nama secret mungkin **berbeda**)

```bash
kubectl get secrets
```

![https://lh4.googleusercontent.com/SonWb0y9bZSr6eU37qoJq7t2dJYsIvSsXimW342nKVUIYhExG_PRbzYxlEIYKow5M9IuFuyM0_ZWALaAscGCRDe_J9XNeEHRmtGlYkijY_k_m6V8Xtzh9HVZ9HdGIFA04BnTysaZzhMXCpPdng](https://lh4.googleusercontent.com/SonWb0y9bZSr6eU37qoJq7t2dJYsIvSsXimW342nKVUIYhExG_PRbzYxlEIYKow5M9IuFuyM0_ZWALaAscGCRDe_J9XNeEHRmtGlYkijY_k_m6V8Xtzh9HVZ9HdGIFA04BnTysaZzhMXCpPdng)

untuk melihat token, kita menggunakan perintah berikut (nama secret mungkin **berbeda**). Token inilah yang kita pakai saat nanti login Dashboard. Copy token ini.

```bash
kubectl describe secret dashboard-admin-sa-token-ls2fm
```

![https://lh5.googleusercontent.com/YzF8GTrYCFl3Vq3PaYuz48n5ItMhw9wbd2uDVcyNkwDPxMlS5vIpvR9OITK79xDcz35lw6dN25_DpE8RnQs9fScwPwP-qDhlYDyJvB019Lo8MtC0ldpWT1iDwzt9h-avYPgp_yhRzUy26JXidw](https://lh5.googleusercontent.com/YzF8GTrYCFl3Vq3PaYuz48n5ItMhw9wbd2uDVcyNkwDPxMlS5vIpvR9OITK79xDcz35lw6dN25_DpE8RnQs9fScwPwP-qDhlYDyJvB019Lo8MtC0ldpWT1iDwzt9h-avYPgp_yhRzUy26JXidw)

setelah **token** dicopy, langkah selanjutnya mengekspose dashbord Kubernetes agar bisa diakses dari luar cluster. Kita disediakan berbagai metode oleh kubernetes, dokumentasi nya ada [di sini](https://github.com/kubernetes/dashboard/tree/master/docs/user/accessing-dashboard). Tapi disini kita menggunakan metode **port-forward**. Command ini dieksekusi dari kubectl local.

```bash
kubectl port-forward -n kubernetes-dashboard service/kubernetes-dashboard 8080:443 --address 0.0.0.0
```

![https://lh6.googleusercontent.com/acDVcYrI1MemcKdYeD3IAvZH9lSJv4sRe9GnqLd86nl2gUgetRv1gpnv0MeqR8hxdrn1402t-NkCdJ9gNDHKHX81L8HMgQ8_Yyob9-vLNt9C2OvC25fAYiIlsWsQFv1FqTaZHoRGXRmWyzfM0w](https://lh6.googleusercontent.com/acDVcYrI1MemcKdYeD3IAvZH9lSJv4sRe9GnqLd86nl2gUgetRv1gpnv0MeqR8hxdrn1402t-NkCdJ9gNDHKHX81L8HMgQ8_Yyob9-vLNt9C2OvC25fAYiIlsWsQFv1FqTaZHoRGXRmWyzfM0w)

saatnya kita buka browser kesayangan kita (direkomendasikan Firefox), lalu masukan link berikut. ![https://localhost:8080/](https://54.84.18.114:8080/)

![https://lh3.googleusercontent.com/elJ8YczRBeyANf3-YeQKoq0pF_ck3m2buBUY0KwImODvdd-bRKw2c2-CXRxvcDYbCMXXN-iEfRvNAlIyM7xEOr6zroS11SqJFkZUB2BK3-dTh3NgFwTmR1SbuBO6epCyuONKUE7ZvlbGn0QhOw](https://lh3.googleusercontent.com/elJ8YczRBeyANf3-YeQKoq0pF_ck3m2buBUY0KwImODvdd-bRKw2c2-CXRxvcDYbCMXXN-iEfRvNAlIyM7xEOr6zroS11SqJFkZUB2BK3-dTh3NgFwTmR1SbuBO6epCyuONKUE7ZvlbGn0QhOw)

Jika ada warning seperti dibawah, klik **Advance > Accept the Risk and Continue**.

![https://lh4.googleusercontent.com/I8bbGve0cwxHchlKeAT-U7R83UnZ_hBj20iPQObgW0TAR5PC0-x3Bw1Pw6OOS6yRcEjZbotWRmA3OyDcWb-ggOtExfgE2ybeJlICXQ45JNC9Kh-t4B5b9W3xq5StkVSwTMZus8tPzMUpdqGq6w](https://lh4.googleusercontent.com/I8bbGve0cwxHchlKeAT-U7R83UnZ_hBj20iPQObgW0TAR5PC0-x3Bw1Pw6OOS6yRcEjZbotWRmA3OyDcWb-ggOtExfgE2ybeJlICXQ45JNC9Kh-t4B5b9W3xq5StkVSwTMZus8tPzMUpdqGq6w)

paste kan **Token** yang sudah kita copy sebelumnya. Setelah itu, **sign in**.

tampilan awal, akan seperti ini, karena tidak ada resource yang berjalan di namespace **default**.

![https://lh5.googleusercontent.com/BT6EKeTaoFAEDXOraJiTmbhoh-d7y74V78xj_xIoo1rx3gsdQzLVTix_ndSbd557EFTAM8LVSy5WfLsT1M47ZJ73PPOxhrQxJwAxu9xe6fP6iUxEJLGr3SOYYEAXfAa4IbguQon0pfq7y3rBiw](https://lh5.googleusercontent.com/BT6EKeTaoFAEDXOraJiTmbhoh-d7y74V78xj_xIoo1rx3gsdQzLVTix_ndSbd557EFTAM8LVSy5WfLsT1M47ZJ73PPOxhrQxJwAxu9xe6fP6iUxEJLGr3SOYYEAXfAa4IbguQon0pfq7y3rBiw)

Untuk itu, kita ganti namespace menjadi **all namespaces**.

![https://lh4.googleusercontent.com/g2ROFmGyi6JAjOiojYz8wNMpciNwmxWeUJC5xPNemBNrdCqIQp_i9KvdRwxRZbE3gl8Kxzz1YhzeR3_6otUGfEjUjEfntJGKiKQcMvHZ40XvEW8jZdafMl50ybTpV_y0v8u5Oa8_9_ORyGhbBg](https://lh4.googleusercontent.com/g2ROFmGyi6JAjOiojYz8wNMpciNwmxWeUJC5xPNemBNrdCqIQp_i9KvdRwxRZbE3gl8Kxzz1YhzeR3_6otUGfEjUjEfntJGKiKQcMvHZ40XvEW8jZdafMl50ybTpV_y0v8u5Oa8_9_ORyGhbBg)

Jadinya akan seperti ini. Kita bisa melakukan monitoring terhadap resource yang berjalan.

![*Dashboard Web Dashboard Kubernetes*](https://lh3.googleusercontent.com/FQvUzNPo9kGvhY5D1dsjhpNZcqnD5j8tRxgOsUactbz_lHzcWHfGWII_P1ZAmCQrW_B24Duv-WD03MboEOjntsx0Uu_NbYjwYFr3NbvRu-HL1ljQ8Q79TH4xeztBk_9fcgCIhw6r0anMTRDKhg)

*Dashboard Web Dashboard Kubernetes*

# **Perintah Kubernetes Lainnya**

1. **Melihat list cluster**
    
    ```bash
    kops get cluster
    ```
    
2. **Edit node instance group**
    
    ```bash
    kops edit ig --name cilsy.k8s.local nodes
    ```
    
3. **Edit master instance group**
    
    ```bash
    kops edit ig --name cilsy.k8s.local master-us-east-1a
    ```
    

# **Exercise**

Soal Praktek :

1. **Install Kubernetes pada server yang kalian miliki**
2. **Buat 4 Node pada cluster dengan tipe instance t2.micro**
3. **Buat 1 Master pada cluster dengan tipe instance t2.micro**