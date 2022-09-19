# 8. Membuat Kubernetes Cluster dengan Kops

Created: July 7, 2022 1:39 PM

# **Apa itu Kops ?**

Kops merupakan project resmi dari Kubernetes yang berfungsi untuk memudahkan Devops dalam mengelola cluster Kubernetes. Developer kops menganggapnya sebagai **kubectl** untuk **cluster**.

Kops tidak hanya akan membantu untuk membuat, menghapus, mengupgrade, dan memaintain cluster Kubernetes pada stage production, tetapi juga akan menyediakan infrastruktur cloud yang diperlukan.

Kops akan membuat infrastruktur sesuai yang dibutuhkan. Misalnya pada AWS, kops akan membuat beberapa resource misalnya EC2, Load Balancer, VPC, Security Group, dan sebagainya secara **otomatis**.

Kops secara resmi mendukung beberapa cloud provider diantaranya AWS (Amazon Web Services), DigitalOcean, GCE, dan OpenStack, Azure, AliCloud.

# **Requirement**

Pada praktikum kali ini, kita membutuhkan beberapa tools yang harus disiapkan yaitu :

- AWS Account
- AWS CLI
- Kubectl
- Kops v1.20.1
- Laptop or computer to access AWS
- Stable internet speed

# **Install Kubectl**

Pertama tama, pada **komputer** kita, kita installkan kubectl. Ini digunakan untuk mengelola cluster Kubernetes kita. Langkah instalasi sebelumnya sudah di praktikan. Namun kita akan lakukan instalasi kali ini juga.

Jika kubectl sudah terinstal dengan baik, anda bisa **lewati** langkah ini.

Update repository :

```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
```

Download Google Cloud GPG key :

```bash
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
```

Add Kubernetes repository :

```bash
echo "deb ![signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

## Install Kubectl

```bash
sudo apt-get updatesudo apt-get install -y kubectl
```

## Verify Kubectl

```bash
kubectl version
```

![https://lh4.googleusercontent.com/HYCpDdGOjcm--U3Qit2D9MCARhOlF1FAQQxYLnF-Nyuc4TVsutqr9Q6thnhdyNf6cUiBco_ZZ-LzCdWaqCyJ2ED6ZJ4Ygf-YWkrzXrPcoedctvSwM6_MaBOMnsAWAgEn-L0fYbhqyAbS_NbKhw](https://lh4.googleusercontent.com/HYCpDdGOjcm--U3Qit2D9MCARhOlF1FAQQxYLnF-Nyuc4TVsutqr9Q6thnhdyNf6cUiBco_ZZ-LzCdWaqCyJ2ED6ZJ4Ygf-YWkrzXrPcoedctvSwM6_MaBOMnsAWAgEn-L0fYbhqyAbS_NbKhw)

Kita sudah selesai dengan instalasi **Kubectl**. Kita bisa lanjut ke step selanjutnya.

# **Install Kops**

Pada praktikum kali ini kita akan menggunakan latest version dari kOps yaitu versi **v1.20.1**.

Pertama tama, kita akan mengunduh file dari github resmi kOps dengan cara berikut.

```bash
curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
```

- note : hilangkan char “\” pada “…download/$**\**(curl…”

Setelah itu, kita atur chmod dari file tersebut agar bisa dieksekusi

```bash
chmod +x kops
```

Lalu kita pindahkan file tersebut ke direktori **/usr/local/bin**.

```bash
sudo mv kops /usr/local/bin/kops
```

## Verify kops

```bash
kops version
```

![https://lh4.googleusercontent.com/nZJIvIGWT6C19IGw1YQGeI16bBy-iyBxEqWipwHRqv74N0UvvhzEXe_M1bJj7tkJl7VJCqXQ7_oJhx9WVhntWpej3a2R0tj-Ga55KVbPZikjLsNPZKbLOdKzVlfPfx8tIalUzNUIIRwtVhnsnQ](https://lh4.googleusercontent.com/nZJIvIGWT6C19IGw1YQGeI16bBy-iyBxEqWipwHRqv74N0UvvhzEXe_M1bJj7tkJl7VJCqXQ7_oJhx9WVhntWpej3a2R0tj-Ga55KVbPZikjLsNPZKbLOdKzVlfPfx8tIalUzNUIIRwtVhnsnQ)

Bagus ! Kita bisa melanjutkan ke langkah selanjutnya.

# **Configure AWS CLI**

Kali ini kita akan menginstalkan AWS CLI untuk mengelola resource AWS kita secara remote. Kita bisa menggunakan akun AWS kita dengan menggunakan access key id yang sebentar lagi akan kita praktikan.

Untuk mengkonfigurasi AWS CLI kita agar terhubung ke akun AWS kita memerlukan access key id untuk “login”. Maka dari itu, kita dapatkan access key id tersebut! Baca kembali modul  **9. Bab 6 - AWS Basic Server Production Part 4 IAM & Budgeting**.

Pertama tama, kita masuk ke console AWS

Lalu buka menu **My Security Credentials** seperti berikut.

![https://lh4.googleusercontent.com/RYAe85FjKbi_eG8DJ8RzeguYvoOV4Clc8CXx9rPqWH6R4HdczmlvwDBEMgCCVCJGNgUqyvPIxFXOX6ars9k50ee-Y2KEHjL5UQsyFpzwuOzXqNfTx-EYiZtrc0CeEmgEGEydfdeebS-rmp2rgw](https://lh4.googleusercontent.com/RYAe85FjKbi_eG8DJ8RzeguYvoOV4Clc8CXx9rPqWH6R4HdczmlvwDBEMgCCVCJGNgUqyvPIxFXOX6ars9k50ee-Y2KEHjL5UQsyFpzwuOzXqNfTx-EYiZtrc0CeEmgEGEydfdeebS-rmp2rgw)

Lalu kita akan menemukan menu **Access key (…)** seperti berikut

![https://lh6.googleusercontent.com/shOBeFs1ppmbyEh3iimHJG89VT4w12tvvggWwv5RDvEneyQhPFH0Cb7u8iBZ84feBMz5lCg3P0S2iPrIQ6EGT7Z10-2ci1X9eeaJghVma6_2mj43Fs4yAKq_2xNuAeJKpi9w3U2wthCK_Pkugw](https://lh6.googleusercontent.com/shOBeFs1ppmbyEh3iimHJG89VT4w12tvvggWwv5RDvEneyQhPFH0Cb7u8iBZ84feBMz5lCg3P0S2iPrIQ6EGT7Z10-2ci1X9eeaJghVma6_2mj43Fs4yAKq_2xNuAeJKpi9w3U2wthCK_Pkugw)

Jika masih kosong, kalian bisa buat Access Key dengan mengeklik tombol **Create New Access Key**.

Nantinya akan muncul popup yang berisikan access key id dan secret access key seperti berikut.

![https://lh6.googleusercontent.com/3rhqGTZ7rX6J3QH7v2It2HA9FB0G2DIIKVJ4i-Ib-ts3Or3TBj0TXkvfCEYB0lIiWUj49oW_l2bWgLGczp-wsJ9soz-tp7FGadQO8FEbNk8uEtp08OVSSgyf5H-Zc47VOAiSF0Nq9e68o3yYfg](https://lh6.googleusercontent.com/3rhqGTZ7rX6J3QH7v2It2HA9FB0G2DIIKVJ4i-Ib-ts3Or3TBj0TXkvfCEYB0lIiWUj49oW_l2bWgLGczp-wsJ9soz-tp7FGadQO8FEbNk8uEtp08OVSSgyf5H-Zc47VOAiSF0Nq9e68o3yYfg)

Nahh sudah muncul kan Access Key Dan Secret nya ? Kalian hanya diberi kesempatan 1 kali untuk menyimpan Secret Access Key yaitu pada saat muncul popup itu. Jadi direkomendasikan untuk mendownload Access Key dengan cara mengeklik tombol **Download File Key**. Nantinya isi file tersebut berisikan Access Key Id dan Secret Access Key.

Selanjutnya kita masukan Access Key yang sudah kita buat tadi dengan mengeksekusi perintah berikut.

```bash
aws configure
```

![https://lh3.googleusercontent.com/n3yKjvqF6ZpgSyqBI2QnsWzClqHIIN-5UljI1VLXpyXval1NoxyYFzlsa5dHuI426a5m6o67041xbU8mFUdJUtX7PxyTVjcUiz9T0BfD40I7fFMeV6asWR8uPwWZ_-u0F7tdyasPv_F_Tc_hQg](https://lh3.googleusercontent.com/n3yKjvqF6ZpgSyqBI2QnsWzClqHIIN-5UljI1VLXpyXval1NoxyYFzlsa5dHuI426a5m6o67041xbU8mFUdJUtX7PxyTVjcUiz9T0BfD40I7fFMeV6asWR8uPwWZ_-u0F7tdyasPv_F_Tc_hQg)

Untuk yang masih bingung mengenai region name, bisa lihat referensi dokumentasi AWS [disini](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html#Concepts.RegionsAndAvailabilityZones.Regions).

Untuk mengecek apakah kita berhasil mengkoneksikan akun AWS kita atau tidak, kita bisa mengeksekusi salah satu command AWS cli ini.

```bash
aws ec2 describe-instances
```

![https://lh6.googleusercontent.com/ghFAmaF4_1P4nrbX5oUtxyzUPiKPvVm3o41IRBKLw0-SVUj6cXKl6zAVqCAcQMxIfaKVdQ1uuYcoyZXKZ3gYtbpGWnrxAXxNSD2JX0UvV4ETovsftqxr5Y5FX4T4bH3tI2FIBNOCcDDQafXDrQ](https://lh6.googleusercontent.com/ghFAmaF4_1P4nrbX5oUtxyzUPiKPvVm3o41IRBKLw0-SVUj6cXKl6zAVqCAcQMxIfaKVdQ1uuYcoyZXKZ3gYtbpGWnrxAXxNSD2JX0UvV4ETovsftqxr5Y5FX4T4bH3tI2FIBNOCcDDQafXDrQ)

Perintah diatas, artinya mengecek list EC2 yang ada di AWS kita. Berhubung tidak ada EC2 instance yang berjalan di region us-east-2, maka hasilnya seperti itu. Dapat disimpulkan kita berhasil mengkoneksikan akun AWS menggunakan AWS CLI.

Well done ! Kita bisa melanjutkan ke langkah selanjutnya.

# **Create DNS**

Kops menggunakan DNS untuk melakukan discovery didalam clusternya sehingga kita dapat mencapai server API kubernetes dari client. Jika kita menggunakan kops, kita harus menggunakan nama cluster dengan nama DNS yang valid, sehingga kita tidak akan membuat bingung cluster dengan alamat IP Address dan kita dapat membagi cluster secara jelas.

Kops sendiri merekomendasikan kita menggunakan subdomain untuk membagi cluster misalkan **dev.sdcilsy-trainer.web.id**. Ini dikarenakan agar cluster kita nantinya tidak mengganggu domain intinya dan menyebabkan kekacauan.

Jika anda memiliki **DNS** yang sudah fully-qualified, bisa menggunakannya untuk cluster Kubernetes kita. Namun jika belum, tenang! Kops menyediakan alternatif lain yakni dengan menggunakan **gossip DNS**.

Pstt ! Membuat cluster Kubernetes menggunakan **DNS**, ada di modul berikutnya!

**Gossip** ini bukan gosip ibu ibu yaa. Gossip disini itu teknologi jaringan peer-to-peer untuk menyebarkan informasi, dalam hal ini alamat API K8s. Ini berarti bahwa layanan DNS yang dihosting secara eksternal **tidak diperlukan**/**optional**.

Gossip juga merupakan satu-satunya opsi jika Anda ingin menerapkan cluster di salah satu wilayah AWS tanpa Route 53, seperti China dan GovCloud.

Untuk menggunakan DNS berbasis **Gossip**, konfigurasikan nama domain cluster untuk diakhiri dengan .k8s.local. Misalnya **cilsy.k8s.local**. Sesimple itu.

Nah pada praktikum kali ini, kita akan menggunakan metode **Gossip DNS**. Jadi kita tidak mengkonfigurasi **Route 53** pada AWS. Namun jika anda sudah memiliki DNS, silahkan saja mengisikan nama cluster Kubernetes dengan domain DNS kalian.

# **Create Kops State Store**

kOps memiliki gagasan tentang 'state store'; lokasi tempat kops menyimpan konfigurasi cluster kita. State disimpan di sini tidak hanya saat kita pertama kali membuat cluster, tetapi juga dapat mengubah status dan menerapkan perubahan ke cluster yang sedang berjalan.

Langkah selanjutnya adalah membuat file penyimpanan config kubernetes pada S3. Tempat penyimpanan config kubernetes sendiri akan di simpan pada S3, karena EC2 yang kita pakai nanti akan sangat dinamis, dapat berkurang dan bertambah dengan cepat sesuai kebutuhan maka tidak memungkinkan jika kita menyimpan konfigurasi disana.

Jadi kita tak perlu repot repot lagi untuk menyimpan konfigurasi Cluster. Semua konfigurasi cluster akan disimpan di State Store ini.

Kita bisa menggunakan beberapa provider cloud untuk menyimpan Kops State Store ini. Diantaranya adalah berikut.

- AWS
- Digital Ocean
- AliCloud
- Openstack Swift
- Google Cloud
- Vault

Semuanya memiliki konfigurasi yang berbeda satu sama lain. Jika anda penasaran, dokumentasi nya ada [di sini](https://kops.sigs.k8s.io/state/).

Ada beberapa cara untuk mengonfigurasi state store. Berikut dalam urutan prioritas :

- argumen perintah **-state s3://yourstatestore**
- environment variable **KOPS_STATE_STORE=s3://yourstatestore**
- file konfigurasi **$HOME/.kops.yaml**
- file konfigurasi **$HOME/.kops/config**

Setelah memahami konsep dari state store, tanpa berlama lama lagi, kita buat state store pada S3 AWS.

Kita akan menggunakan AWS CLI untuk membuat state store ini. Kita bisa menggunakan perintah sebagai berikut.

```bash
aws s3api create-bucket --bucket taufik-kops-state --region us-east-1
```

Perintah diatas akan membuat bucket S3 dengan nama **taufik-kops-state** pada region **us-east-1**. Kita bisa saja untuk menset nama sesuai kebutuhan.

Selanjutnya, kita nyalakan fitur versioning pada bucket agar dapat mengetahui perubahan setiap melakukan update pada cluster. Kita bisa melakukannya dengan cara berikut.

```bash
aws s3api put-bucket-versioning --bucket taufik-kops-state --region us-east-1 --versioning-configuration Status=Enabled
```

Untuk melihat list bucket S3, kita bisa menggunakan perintah berikut.\

```bash
aws s3 ls
```

![https://lh6.googleusercontent.com/d2w4hiEV4vhrXfgNstfB-VoGR48OTeZ2R7dEmJ17U2kROSA6pXELDKf0gNqfBb0XYVSDVOkjYOeD8AueZuBVvT-JpqYgB3R2Vgc0e5fzSHn_fykJLiKkrbouHteLMR_s8Thm-7ocraoLA5OMlw](https://lh6.googleusercontent.com/d2w4hiEV4vhrXfgNstfB-VoGR48OTeZ2R7dEmJ17U2kROSA6pXELDKf0gNqfBb0XYVSDVOkjYOeD8AueZuBVvT-JpqYgB3R2Vgc0e5fzSHn_fykJLiKkrbouHteLMR_s8Thm-7ocraoLA5OMlw)

untuk melihat isi dari bucket tersebut, bisa menggunakan perintah berikut.

```bash
aws s3 ls taufik-kops-state
```

# **Create Cluster**

Setelah semua sudah siap, langkah selanjutnya adalah membuat cluster Kubernetes kita.

Caranya menggunakan perintah seperti berikut.

```bash
kops create cluster --name cilsy.k8s.local --zones us-east-1a --master-size t2.medium --node-size t2.medium --state s3://taufik-kops-state
```

![https://lh4.googleusercontent.com/iG5kxNHpOf3su9YNM8Ib1lEIkSzcoozqwGkFHi1c0oDw-SwrmLlKLYu3b6Jsu5JIAg_r-Y5TGnfFue-V7b16S4S9l4VfEAiwTB1TBIW1JvCyNg7n64bAjani_rasTFI82BLz9XAEwuxGqwmaAg](https://lh4.googleusercontent.com/iG5kxNHpOf3su9YNM8Ib1lEIkSzcoozqwGkFHi1c0oDw-SwrmLlKLYu3b6Jsu5JIAg_r-Y5TGnfFue-V7b16S4S9l4VfEAiwTB1TBIW1JvCyNg7n64bAjani_rasTFI82BLz9XAEwuxGqwmaAg)

Perintah tersebut akan membuat cluster Kubernetes dengan nama **cilsy.k8s.local** di zona **1a** pada region **us-east-1** dengan EC2 instance untuk master dan node adalah **t2.medium** masing masing 1 buah EC2.

Eits, jangan salah tangkap, create cluster disini, bukan berarti seluruh cluster sudah terbuat. Melainkan **kops** akan membuat **state** dan mengisikannya ke **kops state store** yang sudah kita buat sebelumnya. State inilah  Jika kita periksa S3 kita, sekarang sudah terisi dengan nama dari cluster kita, yaitu folder **cilsy.k8s.local**. Dalam folder ini, terdapat konfigurasi konfigurasi cluster kita mulai dari spesifikasi cluster, certificate SSL, secret, config dan lain lain.

```bash
aws s3 ls taufik-kops-state
```

![https://lh5.googleusercontent.com/RjonosWvCYxBnW5kdZ8qK-ALRTQ-DTCsi98hbrpqEztJMQwSy5kaishYEPgaZsvUn7cy4yjCw3pWVtJ6Xrv3FL5aY1alsbim6nrEFMkKuAvo95aPbOuENO003LCpJSpWiOv3-6780T4ETmQVpQ](https://lh5.googleusercontent.com/RjonosWvCYxBnW5kdZ8qK-ALRTQ-DTCsi98hbrpqEztJMQwSy5kaishYEPgaZsvUn7cy4yjCw3pWVtJ6Xrv3FL5aY1alsbim6nrEFMkKuAvo95aPbOuENO003LCpJSpWiOv3-6780T4ETmQVpQ)

aws s3 ls taufik-kops-state --recursive

![https://lh4.googleusercontent.com/Y2CkRjD3XRcav4-F3lK75c1-9CKkKbVyAQU9bnc-kb_Z4xarHG7BImvjqJjCIDqDtlDwgtazgonAemi2Z8ThYwU7RQoM3uQf1VN4H7-JschHgFgzwMB7VdkVlq2YoRk5w0dkDteIPA-nF3G7rw](https://lh4.googleusercontent.com/Y2CkRjD3XRcav4-F3lK75c1-9CKkKbVyAQU9bnc-kb_Z4xarHG7BImvjqJjCIDqDtlDwgtazgonAemi2Z8ThYwU7RQoM3uQf1VN4H7-JschHgFgzwMB7VdkVlq2YoRk5w0dkDteIPA-nF3G7rw)

Jika kalian ingat pada pembahasan **Gossip DNS**, cilsy.k8s.local adalah salah satu contohnya. Dan kita isikan gossip DNS tersebut menjadi **nama cluster**. Begitu juga dengan yang menggunakan DNS fully qualified.

Kita dapat mendefinisikan jumlah instance dari master dan node dengan menggunakan parameter sebagai berikut.

```bash
--master-count 2      # akan dibuatkan 2 EC2 instance untuk master
--node-count 5        # akan dibuatkan 5 EC2 instance untuk node
```

Jika kita ingin melihat cluster yang sudah dibuat tadi, bisa menggunakan perintah berikut.

```bash
kops get cluster --state s3://taufik-kops-state
```

![https://lh4.googleusercontent.com/Fxq7a-CYD1sNLh9NP5OAJMnChV5HkRrLmHuH_3tvD0MhxV5c2j92j0wNmSzR_zBC-aE8kmXjNsIOoqdxN4EsYXSwwYkbf6wFNY9o9xQ1RHxtvo_17hMLL1Pkb_LO8DV6LPX09yR68002Ehcrdw](https://lh4.googleusercontent.com/Fxq7a-CYD1sNLh9NP5OAJMnChV5HkRrLmHuH_3tvD0MhxV5c2j92j0wNmSzR_zBC-aE8kmXjNsIOoqdxN4EsYXSwwYkbf6wFNY9o9xQ1RHxtvo_17hMLL1Pkb_LO8DV6LPX09yR68002Ehcrdw)

# **Examine Configuration**

Berhubung cluster kita belum dibuat dan hanya ada file konfigurasi konfigurasinya saja, saatnya kita melihat apa yang akan kops buat pada cluster kita.

Kops akan membuat resource AWS berikut secara otomatis :

- Autoscaling Group
- Classic Load Balancer
- EBS Volume
- IAM
- Security Group
- VPC
- dll

Oleh karena itu, jika konfigurasi default tersebut terasa berlebihan atau tidak sesuai, kita bisa mengeditnya sesuai kebutuhan saja.

Caranya, kita bisa menggunakan perintah berikut.

```bash
kops edit cluster --name cilsy.k8s.local --state s3://taufik-kops-state
```

![https://lh4.googleusercontent.com/8OqZRZ43ev_XhCV42yY581SS-E74PI7rlO9Wps5ssQ_Y-ZQ79Wgi-B-IpE0RtOScSCIW1_gef4mU4iANe3_IBalCJUQVO-0TWPLlk52ZPA8cT0eskV2EV-JiK9BCHYG-1yQEAFsDq1TYYaf8Ow](https://lh4.googleusercontent.com/8OqZRZ43ev_XhCV42yY581SS-E74PI7rlO9Wps5ssQ_Y-ZQ79Wgi-B-IpE0RtOScSCIW1_gef4mU4iANe3_IBalCJUQVO-0TWPLlk52ZPA8cT0eskV2EV-JiK9BCHYG-1yQEAFsDq1TYYaf8Ow)

![https://lh3.googleusercontent.com/EWuVx0FQpC1tzKVJlY3HLsqLXtVq4DwcAvva6FEcstJgrxI53VUvSfkAwxRe4ksJ1NOiPRATTTIXbUcsPSRTckx6VYyVqkIqTLsu5I-jRj12CGSEfSYGpo85L96UTu8Tp6QUTFLRot6JSuxkMg](https://lh3.googleusercontent.com/EWuVx0FQpC1tzKVJlY3HLsqLXtVq4DwcAvva6FEcstJgrxI53VUvSfkAwxRe4ksJ1NOiPRATTTIXbUcsPSRTckx6VYyVqkIqTLsu5I-jRj12CGSEfSYGpo85L96UTu8Tp6QUTFLRot6JSuxkMg)

Seperti yang bisa kita lihat, ada beberapa konfigurasi yang bisa kita atur seperti nama cluster, cpu request untuk etcd, CIDR network, versi Kubernetes dan lain lain.

Untuk kali ini, kita biarkan seperti adanya. Untuk keluar dari editor, kita tinggal memasukan input **:q!**.

```bash
**Cluster Goes Up!**
```

Saatnya yang ditunggu tunggu yaitu membuat cluster (literally). Kops akan membaca state dari state store untuk membuat cluster ini. Untuk membuat cluster, kita tinggal mengeksekusi perintah berikut.

```bash
kops update cluster --name cilsy.k8s.local --state s3://taufik-kops-state --yes --admin
```

![https://lh5.googleusercontent.com/fqWVpIPHAsCKcUtdo7P1o8I7GuEZI9tkM4Bv7nyqWWKKeZ-j5suay5jPMjtgWL9R9Roa-0HPqOM2g4CsTWlHkuzbkPhjQZoS7A4abPykSBQx3dWcNEhEj7YV3j_VI0S0Xq8fepz2E1rObcECbg](https://lh5.googleusercontent.com/fqWVpIPHAsCKcUtdo7P1o8I7GuEZI9tkM4Bv7nyqWWKKeZ-j5suay5jPMjtgWL9R9Roa-0HPqOM2g4CsTWlHkuzbkPhjQZoS7A4abPykSBQx3dWcNEhEj7YV3j_VI0S0Xq8fepz2E1rObcECbg)

Kita bisa biarkan kops membuat cluster sambil kita membuat kopi. Nah setelah command sudah selesai, coba lihat EC2 pada AWS kita. Pada case ini, kita lihat zona us-east-1.

![https://lh3.googleusercontent.com/fk5nxFjAY0Zao44OH5D0U7_NAO7a3IDyX48pLhTnATorA8-fut9sn-0fzcil9NUnoxEDFYB6mpKBnUmz6jeueV-P9sahojmvuO_SzcaCcz_3aAOCOYnLPndwYqjKIPbvDjrA2gU29Veca5qG6g](https://lh3.googleusercontent.com/fk5nxFjAY0Zao44OH5D0U7_NAO7a3IDyX48pLhTnATorA8-fut9sn-0fzcil9NUnoxEDFYB6mpKBnUmz6jeueV-P9sahojmvuO_SzcaCcz_3aAOCOYnLPndwYqjKIPbvDjrA2gU29Veca5qG6g)

Bisa kita lihat ada 2 instance baru yang dibuat oleh Kops yaitu **nodes-us-east-1a.cilsy.k8s.local** dan **master-us-east-1a.masters.cilsy.k8s.local**. Dan Jika anda mengecek resource lain seperti ELB, Security Group, VPC dan lainnya, akan ada resource baru hasil dari kops tadi.

# **Testing**

Pada saat pembuatan cluster, status node dan master belum ready. oleh karena itu kita butuh waktu beberapa saat agar cluster dapat ready. Untuk mengecek cluster kita sudah dalam kondisi up sepenuhnya atau belum, kita bisa menggunakan perintah berikut.

```bash
kops validate cluster --name cilsy.k8s.local --state s3://taufik-kops-state --wait 10m
```

![https://lh4.googleusercontent.com/kcHiuVySktk16tQVsE2OnwWiLFGW5_WCYnAAuwt9Zuk1r1_oKOgI3SB8g-8CGEeRtj6vv0kfppSeEoGDNKlXLccHKyZ3P92TvqgevL36d2YXH-MwfbtzMGQ2fAmSLlsv3IbDUnupxs8OuhvqBA](https://lh4.googleusercontent.com/kcHiuVySktk16tQVsE2OnwWiLFGW5_WCYnAAuwt9Zuk1r1_oKOgI3SB8g-8CGEeRtj6vv0kfppSeEoGDNKlXLccHKyZ3P92TvqgevL36d2YXH-MwfbtzMGQ2fAmSLlsv3IbDUnupxs8OuhvqBA)

Perintah tersebut akan memeriksa status dari Master dan Node apakah berstatus Ready atau belum.

Pada saat pembuatan cluster, kops mengkonfigurasi **context kubectl** pada local ke cluster cilsy.k8s.local. Untuk mengetes cluster, kita bisa melihat anggota cluster dari komputer kita dengan cara mengeksekusi perintah berikut.

```bash
kubectl get nodes
```

![https://lh5.googleusercontent.com/-qyW0sLg6z2AuYe6lv-nXlLrpZHpJq8njZHAGqZol4rEao5lHUJ1J3oBQ_DzI62E3NV4IhIbBmsI8n29lnFPgOYTNXbZvLKi_at3Qmz8dvBNwptlqxfwI_ab-2nhVJ1UZouZ9onR17p4shREWg](https://lh5.googleusercontent.com/-qyW0sLg6z2AuYe6lv-nXlLrpZHpJq8njZHAGqZol4rEao5lHUJ1J3oBQ_DzI62E3NV4IhIbBmsI8n29lnFPgOYTNXbZvLKi_at3Qmz8dvBNwptlqxfwI_ab-2nhVJ1UZouZ9onR17p4shREWg)

Untuk melakukan koneksi SSH ke **master**, kita perlu mengetahui IP atau DNS public dari instance tersebut. Setelah itu, tinggal menggunakan public key yang kops buat saat membuat cluster. Public tersebut terletak di **~/.ssh/id_rsa**.

Kita bisa menggunakan perintah berikut untuk melakukan koneksi ke **master**

```bash
ssh -i ~/.ssh/id_rsa ubuntu@api.<nama cluster>
```

![https://lh4.googleusercontent.com/dDTgnxPtn0cv31kE_UtMQaaIqI2yWa-4ZqxUysEyPk9sic_sY83FmuIpCbjlsjwYeMDPZHxhdx6Dj-klz4bklMQFdTUAaJ4C4CBCxO3DPQEA_cWnucDW66Sq8zW1XmP1vzgxOu7o24srPvLBkg](https://lh4.googleusercontent.com/dDTgnxPtn0cv31kE_UtMQaaIqI2yWa-4ZqxUysEyPk9sic_sY83FmuIpCbjlsjwYeMDPZHxhdx6Dj-klz4bklMQFdTUAaJ4C4CBCxO3DPQEA_cWnucDW66Sq8zW1XmP1vzgxOu7o24srPvLBkg)

Kubectl sudah terinstall di Master Cluster. Kita bisa cek seperti berikut.

![https://lh5.googleusercontent.com/TEVO3faHnwiU9jrpr7pAmMYd--vQkLtImA0auKFhu2OwZ0E8TUzqT3WhlCTzDLZ0LjH1J8DCogcQzHT-2HeWJC9rSFqWRyd33hcKkidZ84Ppo-jJneVwtm54qjBpeqjRUbTI7NSvHlBUvjbJ5w](https://lh5.googleusercontent.com/TEVO3faHnwiU9jrpr7pAmMYd--vQkLtImA0auKFhu2OwZ0E8TUzqT3WhlCTzDLZ0LjH1J8DCogcQzHT-2HeWJC9rSFqWRyd33hcKkidZ84Ppo-jJneVwtm54qjBpeqjRUbTI7NSvHlBUvjbJ5w)

# **Cleanup**

Kita dapat menghapus cluster dari kops menggunakan perintah berikut.

```bash
kops delete cluster --name cilsy.k8s.local --state s3://taufik-kops-state --yes
```