# 6. Kubernetes Menggunakan Amazon EKS

Created: July 7, 2022 1:27 PM

Amazon Elastic Kubernetes Services (Amazon EKS) adalah layanan Cloud AWS yang dapat digunakan untuk mengelola cluster Kubernetes pada cloud. EKS adalah tempat terbaik menjalankan Kubernetes karena beberapa alasan. Pertama, Kita dapat memilih untuk menjalankan cluster EKS dengan menggunakan AWS Fargate, yang merupakan komputasi tanpa server untuk kontainer. Fargate menghilangkan perlunya menyediakan dan mengelola server, memungkinkan kita menentukan dan membayar sumber daya per aplikasi, dan meningkatkan keamanan melalui isolasi aplikasi sesuai desain. Kedua, EKS sangat terintegrasi dengan layanan seperti Amazon CloudWatch, Auto Scaling Groups, AWS Identity and Access Management (IAM), dan Amazon Virtual Private Cloud (VPC), Kita tidak perlu repot untuk memantau, menskalakan, dan menyeimbangkan beban aplikasi Kita. Ketiga, EKS terintegrasi dengan AWS App Mesh dan menghadirkan pengalaman asli Kubernetes dalam penggunaan fitur-fitur layanan mesh dan menghadirkan observabilitas yang kaya, kontrol trafik, dan fitur keamanan untuk aplikasi. Selain itu, EKS menyediakan bidang kontrol terskala dan sangat tersedia yang beroperasi di beberapa availability zone untuk menghilangkan satu titik kegagalan.

EKS menjalankan Kubernetes hulu dan bersertifikat sesuai dengan Kubernetes sehingga Kita dapat memanfaatkan semua kelebihan tooling sumber terbuka dari komunitas. Migrasi aplikasi Kubernetes standar apa pun ke EKS dapat dilakukan dengan mudah tanpa perlu mengubah kode yang kita buat. Ada beberapa keuntungan untuk ketika kita menggunakan EKS antara lain :

1. **Ketersediaan Tinggi**
    
    Amazon EKS menjalankan infrastruktur manajemen Kubernetes di beberapa AWS Availability Zone, secara otomatis mendeteksi dan mengganti simpul bidang kontrol yang tidak sehat, dan memberikan pemutakhiran dan patching sesuai permintaan.
    
2. **Opsi tanpa server**
    
    EKS mendukung AWS Fargate untuk menyediakan komputasi tanpa server untuk kontainer. Fargate menghilangkan perlunya menyediakan dan mengelola server, memungkinkan Anda menentukan dan membayar sumber daya per aplikasi, dan meningkatkan keamanan melalui isolasi aplikasi sesuai desain.
    
3. **Aman**
    
    EKS secara otomatis menerapkan patch keamanan terbaru untuk bidang kontrol kluster Kita. AWS juga bekerja erat dengan komunitas untuk memastikan masalah keamanan kritis diatasi sebelum rilis dan patch baru diterapkan ke kluster yang ada.
    
4. **Dibangun bersama Komunitas**
    
    Amazon EKS menjalankan Kubernetes hulu dan bersertifikat sesuai dengan Kubernetes, sehingga aplikasi yang dikelola dengan EKS sepenuhnya kompatibel dengan aplikasi yang dikelola dengan lingkungan Kubernetes standar. AWS aktif bekerja sama dengan komunitas Kubernetes, termasuk berkontribusi pada basis kode Kubernetes yang membantu Anda memanfaatkan layanan dan fitur AWS.
    

Berikut cara kerja dari EKS :

[*Ilustarsi Cara Kerja EKS*](https://lh4.googleusercontent.com/2SayFlBdBf6wULgyQdHCcg9_1aI-h_YKWC6E3dKc_q_SHm-zvSDbAMd8fZwGOVvASXq3ch2ib0vHDrXWwr1zV2bjLyahQzQ6X0CDGcF-ToWSs2aer7LIhBsfSQzXoIypsgDSb6j0k2NQ2SVYmA)

*Ilustarsi Cara Kerja EKS*

# **Penerapan EKS**

Beberapa penerapan EKS antara lain :

1. **Penerapan Hibrid**
    
    Kita dapat menggunakan EKS pada AWS Outposts untuk menjalankan aplikasi berkontainer yang mensyaratkan latensi rendah pada sistem lokal. AWS Outposts adalah layanan terkelola penuh yang memperluas infrastruktur AWS, layanan AWS, API, dan alat untuk hampir semua situs yang terhubung. Dengan EKS pada Outposts, Anda dapat mengelola kontainer lokal yang sama mudahnya dengan Anda mengelola kontainer di cloud.
    
2. **Machine Learning**
    
    Kubeflow dengan EKS dapat digunakan untuk pemodelan alur kerja pembelajaran mesin Anda dan menjalankan tugas pelatihan yang didistribusikan secara efisien dengan menggunakan jenis instans EC2 terbaru yang ditenagai GPU. Anda juga dapat menggunakan AWS Deep Learning Containers untuk menjalankan pelatihan dan inferensi dalam TensorFlow pada EKS.
    
3. **Pemrosesan Batch**
    
    Kita dapat menjalankan beban kerja sekuensial atau paralel di klaster EKS dengan menggunakan Kubernetes Jobs API. Dengan EKS, Kita dapat merencanakan, menjadwalkan, dan mengeksekusi beban kerja komputasi batch yang ada di seluruh rentang layanan dan fitur komputasi AWS, seperti Amazon EC2 dan Instans Spot.
    
4. **Aplikasi Web**
    
    Kita dapat membangun aplikasi web yang secara otomatis naik dan turun dan berjalan dalam konfigurasi yang sangat tersedia di beberapa Availability Zone. Dengan berjalan di EKS, aplikasi web yang kita bangun beroleh manfaat dari kinerja, skala, keandalan, dan ketersediaan AWS. Selain itu, layanan kita mendapatkan integrasi kontan dengan layanan jaringan dan keamanan AWS, seperti Application Load Balancers untuk distribusi beban aplikasi web Anda dan VPC untuk jaringan.
    

Contoh Perusahaan yang menggunakan EKS:

[*Contoh Perusahaan Menggunakan EKS*](https://lh5.googleusercontent.com/s28WRep3oYncmv1HfQWEwF6ugsHaDnc6-RVniBbS_qTlJD_kNnMuGDavHDIGI5100mM4o0IPntL22E7o7o23r4bgdJFSWgJ6NulvqiyAQnk3eEyYlt_1idulpYEyhlZZlkDTKM2R_Z0rrhDIcQ)

*Contoh Perusahaan Menggunakan EKS*

# **Create K8s EKS**

Membuat Cluster dengan EKS terbilang cukup mudah karena kita cukup mengkonfigurasi AWS CLI, membuat cluster, lalu mengkonfigurasi kubectl.

Prerequisite:

- AWS CLI configured (lihat modul 9. Bab 6 - AWS Basic Server Production Part 4 IAM & Budgeting - AWS CLI)
- Kubectl installed

Setelah AWS CLI telah terhubung ke AWS menggunakan Key ID dan Access key, maka langkah selanjutnya kita bisa menginstal **eksctl**.

Eksctl merupakan tools official dari AWS yang dibuat oleh Weaveworks yang digunakan untuk mengelola resource EKS pada AWS. Kita dapat membuat, menghapus, dan mengkonfigurasi cluster pada EKS dengan catatan AWS CLI sudah terkonfigurasi.

Menurut [dokumentasi eksctl](https://eksctl.io/introduction/#installation), kita dapat menginstal eksctl pada berbagai platform. Salah satunya menginstal sebagai package.

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmpsudo mv /tmp/eksctl /usr/local/bin
```

Setelah menginstal, verify eksctl dengan mengecek versi dari eksctl.

```bash
eksctl version
```

[https://lh4.googleusercontent.com/Fknw7SNjQzC_P5TEJmkHPLgyjj2t2PWxyRMgxi9_2AEkTSv0ULqLagZ3-Xsh-nN-w7FgTsJd-6EsuBxb2LRd0UvORDpUDRV2J78SIP-NkEB_YMtFBDHbHCDftDZKWf_GcVFvWoBcWFSwJ5Paqg](https://lh4.googleusercontent.com/Fknw7SNjQzC_P5TEJmkHPLgyjj2t2PWxyRMgxi9_2AEkTSv0ULqLagZ3-Xsh-nN-w7FgTsJd-6EsuBxb2LRd0UvORDpUDRV2J78SIP-NkEB_YMtFBDHbHCDftDZKWf_GcVFvWoBcWFSwJ5Paqg)

## ***Create EKS Cluster***

Untuk membuat k8s cluster menggunakan EKS, kita dapat melakukannya di Dashboard EKS. Klik **create cluster**.

[https://lh5.googleusercontent.com/MDbLnD9x00fc8ESKEQXFvSlFc5ugD62pPRPleLX90Kqq0Ajko2xeXlAM-0QLXY1nZKcn1l2HV-j_9PJbwFmwYYvxBoFgAW3O7XZ-f7H8yJzQo7g0S_8S92Vu2dv26P6VnGU2BwsrBnqM9XqD3w](https://lh5.googleusercontent.com/MDbLnD9x00fc8ESKEQXFvSlFc5ugD62pPRPleLX90Kqq0Ajko2xeXlAM-0QLXY1nZKcn1l2HV-j_9PJbwFmwYYvxBoFgAW3O7XZ-f7H8yJzQo7g0S_8S92Vu2dv26P6VnGU2BwsrBnqM9XqD3w)

[https://lh4.googleusercontent.com/l8E6tgiow0ukj151xSQ7JufDulPsXjG-UI1yphsBunQS-MtxnRXVFy9uo_dT_TjLNKW_d8Ies0cZsD1yVGObDQyjX28Rw29OJa0sHcd5zTP-nSTe6oDupTfbNYoJT-XZjyLgtxVKPWEFmPw_9g](https://lh4.googleusercontent.com/l8E6tgiow0ukj151xSQ7JufDulPsXjG-UI1yphsBunQS-MtxnRXVFy9uo_dT_TjLNKW_d8Ies0cZsD1yVGObDQyjX28Rw29OJa0sHcd5zTP-nSTe6oDupTfbNYoJT-XZjyLgtxVKPWEFmPw_9g)

Isikan nama cluster. Kubernetes version dan Service Role biarkan seperti default. Klik **Next**.

[https://lh3.googleusercontent.com/nF_Ya3aEvBSoUhEKZ7bPt-pYPIzmjsg1mJbTPavv-z4lynlWI7l_LNOm6w4UnpgnYUBqBkoTBlj0suyqwcWRrVaDO2y6_ChExAm9xT3BqTxInoO-Oyw2YX0SYPpKbvSvNxiWX4Gpz8AkE7Mutw](https://lh3.googleusercontent.com/nF_Ya3aEvBSoUhEKZ7bPt-pYPIzmjsg1mJbTPavv-z4lynlWI7l_LNOm6w4UnpgnYUBqBkoTBlj0suyqwcWRrVaDO2y6_ChExAm9xT3BqTxInoO-Oyw2YX0SYPpKbvSvNxiWX4Gpz8AkE7Mutw)

Pada Network, kita akan menggunakan VPC dan Subnet default. Pada Endpoint Access, ada 3 pilihan yaitu public, public and private, dan private.

1. Public memungkinkan cluster dan worker untuk diakses dari luar VPC.
2. Public and private memungkinkan cluster diakses dari luar VPC tapi traffic worker node di dalam VPC.
3. Private hanya dapat diakses melalui VPC.

Kita pilih **public and private**. Klik **Next**.

[https://lh5.googleusercontent.com/XTVJe68S9ZL-koSO8RHM1r3HqFU_bRkrhvDCL_5Pgzu33CpzP4e9ZwIFU2JfQJvARP-n8Gecurx71pfuR1hwBmbOYrRcqGvd8I_LhzqNqL0m81PBGhiJxAGe-6yovja1Zvgm2AE0wSjUaWEVkg](https://lh5.googleusercontent.com/XTVJe68S9ZL-koSO8RHM1r3HqFU_bRkrhvDCL_5Pgzu33CpzP4e9ZwIFU2JfQJvARP-n8Gecurx71pfuR1hwBmbOYrRcqGvd8I_LhzqNqL0m81PBGhiJxAGe-6yovja1Zvgm2AE0wSjUaWEVkg)

Pada bagian **Configure Logging** kita biarkan secara default (disable semua).

Dan terakhir untuk **Review**, kita tinggal klik **Next**.

[https://lh5.googleusercontent.com/9P7PtilgWKwVkvK_29Oj5p1qz8iAhDFgXJx1G-RWaWYfW829s9FB6nrNr5AHzT629iDi_3FIHB18-bBTEhNhQM9x_cn4TfluMqj4ZbCSR9FWguYvdXTMmoV8eHq4SkiYwFbNTtssn09fFAhCFw](https://lh5.googleusercontent.com/9P7PtilgWKwVkvK_29Oj5p1qz8iAhDFgXJx1G-RWaWYfW829s9FB6nrNr5AHzT629iDi_3FIHB18-bBTEhNhQM9x_cn4TfluMqj4ZbCSR9FWguYvdXTMmoV8eHq4SkiYwFbNTtssn09fFAhCFw)

## ***Create Node Group Role***

Proses pembuatan EKS ini cukup lama yaitu sekitar 10-15 menit. Sambil menunggu kita melanjutkan ke langkah selanjutnya yaitu membuat **role** untuk **node group**. **Node group** merupakan worker node yang merupakan bagian dari EC2 dan di provision oleh EKS untuk cluster. Jadi jika cluster membutuhkan node baru, maka secara otomatis auto-scaling dari EC2 akan menghadle pembuatan node baru.

Seperti yang dijelaskan sebelumnya, node group ini nantinya akan diprovision EKS maka dari itu, dibutuhkan akses API untuk membuat node baru jika dibutuhkan. Role ini minimal harus memiliki policy:

- AmazonEKSWorkerNodePolicy
- AmazonEKS_CNI_Policy
- AmazonEC2ContainerRegistryReadOnly

Mari kita buat role ini dengan nama **cilsy-eks-node-role**.

[https://lh3.googleusercontent.com/RFkt-_G4BlVhwXqsPUjoy7hsBWU-9geKembA56Co2848fOLloYy66utz2CMnu0jTbaQGC5JzuySgkdKbP0AuRLXNaBDM8mGIVqFGlE3rqi6ejTBQrgekVCIbdviBi7iPcsZ1zJH1Vu3sjegOOQ](https://lh3.googleusercontent.com/RFkt-_G4BlVhwXqsPUjoy7hsBWU-9geKembA56Co2848fOLloYy66utz2CMnu0jTbaQGC5JzuySgkdKbP0AuRLXNaBDM8mGIVqFGlE3rqi6ejTBQrgekVCIbdviBi7iPcsZ1zJH1Vu3sjegOOQ)

Pilih Service **EC2**. Lalu klik **Next: Permission**.

[https://lh6.googleusercontent.com/rQdMxn_zbIcqMvOsHNGC7xf2o41gzsF9FUbFrMpK29zf3Dd1lCOjqoKoiexu2iIlHT74fX0TVf4Ym2XiOJ7ujNeFTTdwZpyQDZPCD3pGS2A-Zt9XfjjhSEZ07an-ZjNFNJTWNhIjx_MLfiAT3w](https://lh6.googleusercontent.com/rQdMxn_zbIcqMvOsHNGC7xf2o41gzsF9FUbFrMpK29zf3Dd1lCOjqoKoiexu2iIlHT74fX0TVf4Ym2XiOJ7ujNeFTTdwZpyQDZPCD3pGS2A-Zt9XfjjhSEZ07an-ZjNFNJTWNhIjx_MLfiAT3w)

Untuk permission, kita pilih  **AmazonEKS_CNI_Policy, AmazonEKSWorkerNodePolicy,** dan **AmazonEC2ContainerRegistryReadOnly.**

[https://lh3.googleusercontent.com/Hq1Y3FKjPfAcMhe9frNZ0Wpjca75212PNh5Gm3m0AhzGjJQ964THhxnci9PtN29BsgEB5k8a_FVQe8h86FtmvIiTscnBsQB6ZgBGec_-6b7HST0PLyqrcWd9Cg6Ce_j8ydbKOY5HAMU2Mq99ww](https://lh3.googleusercontent.com/Hq1Y3FKjPfAcMhe9frNZ0Wpjca75212PNh5Gm3m0AhzGjJQ964THhxnci9PtN29BsgEB5k8a_FVQe8h86FtmvIiTscnBsQB6ZgBGec_-6b7HST0PLyqrcWd9Cg6Ce_j8ydbKOY5HAMU2Mq99ww)

[https://lh3.googleusercontent.com/v1ZkT4ImaVO0K9Gv4IMnFfv3DxEonPn1tVUwPnfmvW2uPUsViPeBfc0CjaaU6-YJ3E-_sN77PN3x4uXhyntpW6tORmgigdIRopRXJtetBgUl-n6pgfoRSW4_atwjasJ0ju-tjBX9OkRGBGg87g](https://lh3.googleusercontent.com/v1ZkT4ImaVO0K9Gv4IMnFfv3DxEonPn1tVUwPnfmvW2uPUsViPeBfc0CjaaU6-YJ3E-_sN77PN3x4uXhyntpW6tORmgigdIRopRXJtetBgUl-n6pgfoRSW4_atwjasJ0ju-tjBX9OkRGBGg87g)

[https://lh5.googleusercontent.com/JM2o_VSpS49ksqOViASWHQ8IP7_23zA_lV9RmbVmr6sX3O703d8xKTJJQqBEsnPlKpNbp2z4D1RnDcNqphbNIFzIX1YVNySMbpX79oaVmqO-Zm4K8Wc01kHD6ZfPZiss1s2PVjt10l9kONWktQ](https://lh5.googleusercontent.com/JM2o_VSpS49ksqOViASWHQ8IP7_23zA_lV9RmbVmr6sX3O703d8xKTJJQqBEsnPlKpNbp2z4D1RnDcNqphbNIFzIX1YVNySMbpX79oaVmqO-Zm4K8Wc01kHD6ZfPZiss1s2PVjt10l9kONWktQ)

Setelah itu, isikan nama role kita. Saya memilih nama **cilsy-eks-node-role**. Klik **Create Role**.

[https://lh3.googleusercontent.com/lLmHveGb3Q3I-Y0S8p5kIQi8wIJ0Poj6W5-I4FUj1KUW2Ea_D0XRyxoQNnoKzHLIvTgfDQUZq4gFaCJGGZRY2imUkEUptgYNTXV25r6Z6jp8WgLQo3JHmXrrbP9YSHkL1M6rig3W1WyEVZ9b6Q](https://lh3.googleusercontent.com/lLmHveGb3Q3I-Y0S8p5kIQi8wIJ0Poj6W5-I4FUj1KUW2Ea_D0XRyxoQNnoKzHLIvTgfDQUZq4gFaCJGGZRY2imUkEUptgYNTXV25r6Z6jp8WgLQo3JHmXrrbP9YSHkL1M6rig3W1WyEVZ9b6Q)

## ***Create Node Group***

Jika kita sudah membuat role dan cluster sudah berstatus active, kita bisa membuat node group.

[https://lh3.googleusercontent.com/OoWSn09QblM8Q-ef9ajZANigkykvHcig8hhGM-IXbXU-G1Rlz537YNu8m6GDP7vkD7LS_kGa9L_zNenhIeVcHMA5WWQmM1THSPuHLEd-XAp4y9UimpdaMKd38-iDPfb_RbrZ3uMgbDmTrSecOg](https://lh3.googleusercontent.com/OoWSn09QblM8Q-ef9ajZANigkykvHcig8hhGM-IXbXU-G1Rlz537YNu8m6GDP7vkD7LS_kGa9L_zNenhIeVcHMA5WWQmM1THSPuHLEd-XAp4y9UimpdaMKd38-iDPfb_RbrZ3uMgbDmTrSecOg)

Isikan nama node group tersebut. Lalu isikan juga **role** yang sudah dibuat sebelumnya.

[https://lh5.googleusercontent.com/9OTCwb1vIKTy6N_s6vfsdYhHigFi8QtY2FoEs3Co3cnjZ133DI0LUuN6WSUVu6dZqp1I9tDoYITscmtwDnkKovRSWM5SgqnJ58W0iCmXYOPZSCH1cFYMKyaSfPhEMfXSTKrVdvhLVch8ROiYBg](https://lh5.googleusercontent.com/9OTCwb1vIKTy6N_s6vfsdYhHigFi8QtY2FoEs3Co3cnjZ133DI0LUuN6WSUVu6dZqp1I9tDoYITscmtwDnkKovRSWM5SgqnJ58W0iCmXYOPZSCH1cFYMKyaSfPhEMfXSTKrVdvhLVch8ROiYBg)

Kita bisa menambahkan Tag seperti ini. Lalu klik **Next.**

[https://lh5.googleusercontent.com/t60zSu3VKp1LqS3f83AoR1pzLCjlW6SvPXOLM9ZWzf6JV2RXep7uf6qOqwuVWSyvP2hFEGEClWlBcioIMyeykIMca_wJKYGmmp4Kqi0dN8muHLUZ5Am03WSU9pKQ95D5yhC9Q8cEMG1Vqwt3AQ](https://lh5.googleusercontent.com/t60zSu3VKp1LqS3f83AoR1pzLCjlW6SvPXOLM9ZWzf6JV2RXep7uf6qOqwuVWSyvP2hFEGEClWlBcioIMyeykIMca_wJKYGmmp4Kqi0dN8muHLUZ5Am03WSU9pKQ95D5yhC9Q8cEMG1Vqwt3AQ)

Pada bagian **Node Group compute configuration**, kita bisa memilih tipe instance yang akan digunakan. Kali ini kita membuatnya dengan t2.small saja.

[https://lh3.googleusercontent.com/4rIo-uMUaiq0ELEyGBCCjlI1HzaJiWe6UQWMhytM9vbyb5KzjCfVlMJCSG9dxtwXXnGxc_5axlLzTcRN2Vf_OsPB83vmi7j4VKw0sQjHEJGYgT5OSYLMFKoCKuM4pWFVM5RfGmQUkQ-KEm_Ijg](https://lh3.googleusercontent.com/4rIo-uMUaiq0ELEyGBCCjlI1HzaJiWe6UQWMhytM9vbyb5KzjCfVlMJCSG9dxtwXXnGxc_5axlLzTcRN2Vf_OsPB83vmi7j4VKw0sQjHEJGYgT5OSYLMFKoCKuM4pWFVM5RfGmQUkQ-KEm_Ijg)

Lalu pada **Node Group scaling configuration** kita set desired size nya menjadi 1 saja. Lalu Klik Next.

[https://lh6.googleusercontent.com/0MsFcA7qTKDxWqhou7kvysB02rLCrGU6kBkTeNQDarefps7Czop9MLXqnCw-0bmLyNzbeM2_o32fXb89al4o-Hvpusx1kc5YESOJFQQT-ZIoiYUpoA7Pq4Fg2SuI2ge3kE5Ih7g_Gj7Yt9-svA](https://lh6.googleusercontent.com/0MsFcA7qTKDxWqhou7kvysB02rLCrGU6kBkTeNQDarefps7Czop9MLXqnCw-0bmLyNzbeM2_o32fXb89al4o-Hvpusx1kc5YESOJFQQT-ZIoiYUpoA7Pq4Fg2SuI2ge3kE5Ih7g_Gj7Yt9-svA)

Untuk bagian **network**, kita biarkan menggunakan VPC dan subnet default saja.

[https://lh6.googleusercontent.com/u0JQe4ooHngwzdqUmHTATfBIUmy0A3z5hg5_JFDeE5m6TpX0xWqphs9yxvNE5YblaJQUqgE5csrETKjRu36V-L8t71eQqTL2ZxS-fi0zJ92j-JhYjgrRJXjc_Ovc-GSlCejmwNo7oJvE131KAw](https://lh6.googleusercontent.com/u0JQe4ooHngwzdqUmHTATfBIUmy0A3z5hg5_JFDeE5m6TpX0xWqphs9yxvNE5YblaJQUqgE5csrETKjRu36V-L8t71eQqTL2ZxS-fi0zJ92j-JhYjgrRJXjc_Ovc-GSlCejmwNo7oJvE131KAw)

Terakhir bagian Review, tinggal klik **Create** saja. Tunggu beberapa saat agar node dapat running.

## ***Configure Kubectl***

Langkah terakhir adalah untuk mengkonfigurasi kubectl agar dapat mengelola resource di EKS. Caranya kita update kubeconfig kubectl kita untuk dapat terhubung ke EKS menggunakan perintah berikut.

```bash
aws eks update-kubeconfig --name cilsy-eks
```

[https://lh6.googleusercontent.com/04L094scXInvSTu8_KU5Z1p8MvcYDOGsh_jRCgfPFxIyPrmLIDJziAJE6gtV67kYDSFYxWEGvNtcmH9lhE9YX0czrQxKuI8xr3gtxHLFnAcqx8iI04jI5xKEW4gNSpZBmRZjdWx1aBpZvkETHA](https://lh6.googleusercontent.com/04L094scXInvSTu8_KU5Z1p8MvcYDOGsh_jRCgfPFxIyPrmLIDJziAJE6gtV67kYDSFYxWEGvNtcmH9lhE9YX0czrQxKuI8xr3gtxHLFnAcqx8iI04jI5xKEW4gNSpZBmRZjdWx1aBpZvkETHA)

## ***Verify***

Sekarang kita tes apakah kita sudah dapat menkonfigurasi k8s pada EKS. Caranya dengan mengecek apakah kita dapat melihat resource yang ada pada cluster. Contohnya adalah node.

[https://lh4.googleusercontent.com/fPnEenFoSBMnKfO0484QYh9eb5571O1lA9_6bDqau8wY7fGxkhEGjgmObCRQXnVTzddm5WidO_eYiv25-zOSOkDbGjowcjZdmVCKPmqmEC7QZ8LC28lMmIvOcJMtPxe1vSUPLwLU5dYdh1VDpw](https://lh4.googleusercontent.com/fPnEenFoSBMnKfO0484QYh9eb5571O1lA9_6bDqau8wY7fGxkhEGjgmObCRQXnVTzddm5WidO_eYiv25-zOSOkDbGjowcjZdmVCKPmqmEC7QZ8LC28lMmIvOcJMtPxe1vSUPLwLU5dYdh1VDpw)

Kita dapat memverifikasi resource tersebut yang berarti praktikum berhasil dilakukan.