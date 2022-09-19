# 6. Terraform Backend

Created: July 25, 2022 3:27 PM

Apa itu backend? Backend adalah tempat **state** disimpan. State merupakan kondisi resource yang di manage. Bayangkan dari konfigurasi EC2 yang sudah kita buat sebelumnya. Pada awal nya, resource belum exist. Setelah kita mengeksekusi **terraform apply**, akan dibuatkan state dari resource EC2 tersebut. Sama halnya saat kita **mengedit** resource yang sudah dibuat. Semuanya di catat dan di track oleh **state**. State ditandai dengan file **terraform.tfstate**.

![https://lh3.googleusercontent.com/pQ0y5_es9UEeuAK1XaJQRzhDsNH66aAevka02wN9WNNwaexGWl_dht8b3JFAGPJPUTJ2zZJC9LD9DELDbxpETLHUy1lSstZ9aS6gF0U_rgMxneqD4_d4FUTZSVGPn4Wb7TjaLo-Ddc1tKcrm-s2u_A](https://lh3.googleusercontent.com/pQ0y5_es9UEeuAK1XaJQRzhDsNH66aAevka02wN9WNNwaexGWl_dht8b3JFAGPJPUTJ2zZJC9LD9DELDbxpETLHUy1lSstZ9aS6gF0U_rgMxneqD4_d4FUTZSVGPn4Wb7TjaLo-Ddc1tKcrm-s2u_A)

Terraform memiliki backend default yaitu **local**. Jadi state akan disimpan pada local machine. State ini tentunya dapat disimpan di cloud sehingga dapat diakses oleh beberapa developer. Namun hati hati dengan state ini karena data yang ada didalamnya sangat sensitive. Untuk mengamankan state, bisa dengan membackupnya secara berkala.

Ada beberapa jenis backend yang terraform sediakan. Salah satunya adalah [S3](https://www.terraform.io/language/settings/backends/s3) dimana kita dapat menyimpan state di bucket S3.

Untuk menambahkan backend, kita tinggal masukan block **backend** pada block **terraform** seperti dibawah.

```bash
terraform {
  ...
  backend "s3" {
    bucket = "mybucket"
    key    = "path/to/my/key"
    region = "us-east-1"
  }
}
```

Pada praktikum kali ini, kita akan membuat instance EC2 menggunakan backend S3 yang kita buat dengan terraform.

Pertama tama, tentunya kita harus memiliki bucket terlebih dahulu. Kita bisa gunakan bucket pada praktikum sebelumnya dengan membuat bucket dengan terraform.

Jika bucket sudah dibuat, pada file **ec2/main.tf**, kita akan menambahkan block backend seperti berikut.

```bash
terraform {
  backend "s3" {
    bucket = "bucket-devops-cilsy"
    key = "sekolah-devops-instance-tfstate"
    region = "us-east-2"
    
  }
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "4.9.0"
    }
  }
}
```

Keterangan:

- bucket = nama bucket yang digunakan. Pada case ini, adalah **bucket-devops-cilsy**.
- key = directory yang digunakan untuk menyimpan state. Pada case ini adalah **sekolah-devops-instance-tfstate**. Nanti terraform akan membuat directory ini dan mengisinya dengan **state**.
- Region = region dimana bucket berada.

Setelah itu, kita harus menginisiasi ulang terraform agar mengupdate backend yang digunakan dengan perintah berikut.

```bash
terraform init -reconfigure
```

![https://lh6.googleusercontent.com/gSMK5zhFUdc56NG6_xaeXuNuTQmF5HZtUbgJoExnr3UVrCB-XFoVBL08rbm2aXTkY4Hn4JubSBY4Vyc-4r1zGxIGBZ1nnfVeis_9y1xUR7bZn6ZnhTapF2hIU_RdiuP-Taei2xmRqJv7JpytehQ-jg](https://lh6.googleusercontent.com/gSMK5zhFUdc56NG6_xaeXuNuTQmF5HZtUbgJoExnr3UVrCB-XFoVBL08rbm2aXTkY4Hn4JubSBY4Vyc-4r1zGxIGBZ1nnfVeis_9y1xUR7bZn6ZnhTapF2hIU_RdiuP-Taei2xmRqJv7JpytehQ-jg)

Sekarang state akan disimpan di bucket S3 dan bukan di local lagi.

Lalu kita eksekusi command berikut untuk mulai membuat resource.

```bash
terraform planterraform apply
```

Ketika resource berhasil di buat, state akan ada berada di bucket didalam directory yang sudah kita tentukan sebelumnya.

![https://lh6.googleusercontent.com/lkVw7wwTyP7rTL7mkES1vmIYIgaQ8Mz1P9yjt8O3niDOf7Ions6epJyfBcft8YJvoz4nOsr3PaiFPhb04XKEv5TYo1clzHjo9zRWI2yI08Q-O86fCtEcKRIedO6jW0OcxsNu3v2UDY6GV3xpGzlC3g](https://lh6.googleusercontent.com/lkVw7wwTyP7rTL7mkES1vmIYIgaQ8Mz1P9yjt8O3niDOf7Ions6epJyfBcft8YJvoz4nOsr3PaiFPhb04XKEv5TYo1clzHjo9zRWI2yI08Q-O86fCtEcKRIedO6jW0OcxsNu3v2UDY6GV3xpGzlC3g)