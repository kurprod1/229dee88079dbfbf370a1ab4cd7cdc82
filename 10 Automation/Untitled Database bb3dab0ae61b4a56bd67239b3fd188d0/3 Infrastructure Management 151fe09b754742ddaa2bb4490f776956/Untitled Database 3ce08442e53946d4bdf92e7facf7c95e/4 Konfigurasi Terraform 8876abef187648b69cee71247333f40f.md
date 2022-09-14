# 4. Konfigurasi Terraform

Created: July 25, 2022 3:21 PM

# **Konfigurasi EC2**

## ***Membuat EC2***

Selanjutnya adalah membuat EC2 dengan menggunakan terraform, file pada terraform sendiri sudah kita jelaskan sebelumnya. Jika ada yang bingung tentang sintak-sintak atau perintah dari terraform maka dapat membaca penjelasan kembali di atas,

Untuk membuat EC2 dengan menggunakan EC2 terraform maka kita harus membuat struktur file seperti di bawah ini. Sebenarnya kita sudah membuatnya tadi, jadi kita hanya perlu mengikuti ke proses selanjutnya.

[*Ilustrasi Struktur File Terraform*](https://lh4.googleusercontent.com/pChye_6F9MjQm5gRh3_6HMs7gnXNGcS7-T0FVXgxCXvaFlAVZcXgdZ5hewIP-YT-2rv4kUwaQrh6teNjXz2bY0jF7EJOR_Qs3q3VurJ4RRSWtXoqeKEVfXfhameWBAk80Rqd4dJ7O3od5-0UFIs5qA)

*Ilustrasi Struktur File Terraform*

Selanjutnya masuk ke terminal pada folder terraform/ec2 lalu ketik perintah **terraform init**. Pada proses ini, terraform menyiapkan dependensi seperti backend, provider yang digunakan. Setelah selesai, terraform akan membuat file **state** pada directory tersebut.

```bash
cd ec2
terraform  init
```

Maka hasilnya akan seperti dibawah ini.

[https://lh6.googleusercontent.com/CIxYX-VfLaOT7-zEHEaYViq28fnrNcdkgZlvpA3D1BnYU-ZY0ndTjVu5-64ZHiHQS-sR84t_C111AQC6JHIQoY2s4liqWriAOdmNpqPh5aPa2Xloi-fXcHJkpGkZ_lwz6kBTjKGAJTFsIxjSi2ZoKw](https://lh6.googleusercontent.com/CIxYX-VfLaOT7-zEHEaYViq28fnrNcdkgZlvpA3D1BnYU-ZY0ndTjVu5-64ZHiHQS-sR84t_C111AQC6JHIQoY2s4liqWriAOdmNpqPh5aPa2Xloi-fXcHJkpGkZ_lwz6kBTjKGAJTFsIxjSi2ZoKw)

Setelah itu ketikan perintah plan seperti dibawah ini.

```bash
terraform plan
```

Setelah menjalankan perintah di atas maka, teraform akan mengecek semua perintah yang ada di file .tf apakah sudah tepat, jika masih ada yang belum tepat, maka lihatlah kembali pada sub bab yang di atas.

[https://lh4.googleusercontent.com/JtM7-R0qO7ZHUIBw3xMobQeOnX5iDN29B3nkVkCp21PsMKsbYo3ZqmhcrqJTTsFda5YJm6ptHDoLUQLUUaA9On3OKD83IfKLWPPjK9Y-fWyU3Q5Ps2Wj-kJvJegulwPwIigUcdV_0jnGt4X5hqsQ8g](https://lh4.googleusercontent.com/JtM7-R0qO7ZHUIBw3xMobQeOnX5iDN29B3nkVkCp21PsMKsbYo3ZqmhcrqJTTsFda5YJm6ptHDoLUQLUUaA9On3OKD83IfKLWPPjK9Y-fWyU3Q5Ps2Wj-kJvJegulwPwIigUcdV_0jnGt4X5hqsQ8g)

Pada akhir output, ada keterangan seperti berikut yang artinya, kita akan membuat resource sesuai dengan konfigurasi di **main.tf**.

[https://lh4.googleusercontent.com/NoGcEZXnrVe0vn46w3H_HL4pp8DITC0dxjB6y1_mWyDs52O1kt41ic8tS-xuIovCadJEsJ8mwzRSwRKkp14Sn1430YeYH2ZAEREviBmB03ipp_IhvNo9gXJumhDQyw1iv6c33yXVwFNteGZAotX_Wg](https://lh4.googleusercontent.com/NoGcEZXnrVe0vn46w3H_HL4pp8DITC0dxjB6y1_mWyDs52O1kt41ic8tS-xuIovCadJEsJ8mwzRSwRKkp14Sn1430YeYH2ZAEREviBmB03ipp_IhvNo9gXJumhDQyw1iv6c33yXVwFNteGZAotX_Wg)

Langkah selanjutnya adalah menjalankan program terraform dengan menggunakan perintah berikut ini.

```bash
terraform apply
```

[https://lh6.googleusercontent.com/dlOC_dXEdfZgvd7r8IBNY1k3_aHDiqJoFuIKcVXFQLl-VWpPOWIxLr1KJ2JagsrW_6kW8UPTVcWtcILLbQArRND5T2AonlUTRhZfsfweciXbgh03xXkCpHm7Fzi9vXwIG7pZfoK8GZd7AwE9N4T9JQ](https://lh6.googleusercontent.com/dlOC_dXEdfZgvd7r8IBNY1k3_aHDiqJoFuIKcVXFQLl-VWpPOWIxLr1KJ2JagsrW_6kW8UPTVcWtcILLbQArRND5T2AonlUTRhZfsfweciXbgh03xXkCpHm7Fzi9vXwIG7pZfoK8GZd7AwE9N4T9JQ)

Untuk mengkonfirmasi apakah konfigurasi sudah dirasa benar, kita masukan yes untuk konfirmasi.

[https://lh6.googleusercontent.com/tKyZQVVpnC_wLcwFWI3AChjzkAgbPxyq57souOHSZowDx6ZfZ8w3mhxPZXcJgGCXMiTIAo7NArpuye1c00wUoyNI8nUlF7Q96MrUJuMYLwTJ7aEuHZs5XzTmuu3IFbJnL6_T6GdXsd9o4RRjAP_eug](https://lh6.googleusercontent.com/tKyZQVVpnC_wLcwFWI3AChjzkAgbPxyq57souOHSZowDx6ZfZ8w3mhxPZXcJgGCXMiTIAo7NArpuye1c00wUoyNI8nUlF7Q96MrUJuMYLwTJ7aEuHZs5XzTmuu3IFbJnL6_T6GdXsd9o4RRjAP_eug)

Tunggu sampai tampilan seperti di atas, maka terraform yang kita jalankan telah berhasil membuat 1  instance EC2 pada AWS .

[https://lh3.googleusercontent.com/Awu7RNHdEjdelyKNIZ2xbEniH-f_H8Me7ETAPvqewE8YXY105-NFk1vc_MAuFL1PMmDMrEdCzxZ94Gr9YsU1Tf8Cng8M_dSuFJBE-Zddbkf1ka6OzDu2rZIn3_5IKw159bmmSeiv64hV1dISyEwzKA](https://lh3.googleusercontent.com/Awu7RNHdEjdelyKNIZ2xbEniH-f_H8Me7ETAPvqewE8YXY105-NFk1vc_MAuFL1PMmDMrEdCzxZ94Gr9YsU1Tf8Cng8M_dSuFJBE-Zddbkf1ka6OzDu2rZIn3_5IKw159bmmSeiv64hV1dISyEwzKA)

Jika berhasil maka akan muncul pada dashboard EC2 seperti dibawah ini.

[*Hasil EC2 dari Terraform*](https://lh3.googleusercontent.com/jQ8xXH8zfwxgyuCpB7gIBzkZYTRuXVl3nGL9DxXk098wyta57LlU2RwOd3aAXUvxt5rIrt9aHd8cnP_RS14iB0xUa-xBbBIrdKwJj-56u-7Op36n77onyuI578iKPiLA20NrEwjAY-KGIxtNuo6TFw)

*Hasil EC2 dari Terraform*

kita bisa mengecek service nginx pada instance tersebut dengan mengakses ip public dari instance tersebut.

[https://lh5.googleusercontent.com/tHKP1hGKJmFi5YMvpSpA8FaDrT4AEadgCWY2j9CEihNbS_MudR2HIp8ZmSHe_SodFwOV8db2R8sEwjD-sJolF1fzYlxRVv8oJl5YvMtJ1rjn5dnRgBy4AEAdX-iItjiucvG0ZbLJBj6F4fIqQlOKxg](https://lh5.googleusercontent.com/tHKP1hGKJmFi5YMvpSpA8FaDrT4AEadgCWY2j9CEihNbS_MudR2HIp8ZmSHe_SodFwOV8db2R8sEwjD-sJolF1fzYlxRVv8oJl5YvMtJ1rjn5dnRgBy4AEAdX-iItjiucvG0ZbLJBj6F4fIqQlOKxg)

## ***Manage EC2***

Setelah kita membuat EC2, selanjutnya kita manage EC2 dengan terraform. Cukup dengan mengubah **variable.tf** yang ada pada folder **ec2/**.

```bash
variable "tags" {
    type = map(string)
    default = {
        "name" = "sekolah-devops-instance"
        "purpose" = "praktikum-sekolah-devops"
        "env" = "dev"
    }
}
```

Pada bagian name dan env kita ubah menjadi staging.

```bash
variable "tags" {
    type = map(string)
    default = {
        "name" = "sekolah-devops-staging"
        "purpose" = "praktikum-sekolah-devops"
        "env" = "staging"
    }
}
```

Selanjutnya jalankan kembali perintah plan untuk melihat perubahan.

```bash
terraform plan
```

[https://lh4.googleusercontent.com/C9Epq21bbY_Xmk3Qw4-471JUUfXHvc22ij8GzGp1zx0Kw7pqljp-2DsU2E0RktGjgdRAK_coHsT-P301Yw6DobtWpwzJ7nnPe4sgix0t2kQurk1k6mf4dbE8NyZJMvkpsLlyVXyd2oZ0mX_vCVD9oA](https://lh4.googleusercontent.com/C9Epq21bbY_Xmk3Qw4-471JUUfXHvc22ij8GzGp1zx0Kw7pqljp-2DsU2E0RktGjgdRAK_coHsT-P301Yw6DobtWpwzJ7nnPe4sgix0t2kQurk1k6mf4dbE8NyZJMvkpsLlyVXyd2oZ0mX_vCVD9oA)

[https://lh3.googleusercontent.com/azwpHOKSxaTWVjd-XCYsHxC7qHmxT6R9POEFxgRmIyldTVCvK-e3cfL8DePcL94ga9S1Zib3IkgQI7ICPC31JT7keJz6W0kUcfl-uNIZ7DMjgMXZunntVXBAkb6RX1pAJwjEfJbnOtg3BgUVTquuoQ](https://lh3.googleusercontent.com/azwpHOKSxaTWVjd-XCYsHxC7qHmxT6R9POEFxgRmIyldTVCvK-e3cfL8DePcL94ga9S1Zib3IkgQI7ICPC31JT7keJz6W0kUcfl-uNIZ7DMjgMXZunntVXBAkb6RX1pAJwjEfJbnOtg3BgUVTquuoQ)

Pada gambar di atas kita dapat melihat perubahan yang terjadi, setelah perubahan sudah benar maka selanjutnya adalah menjalankan perintah apply.

```bash
terraform apply
```

Selanjutnya akan muncul gambar seperti dibawah, maka dengan ini terraform kita telah berhasil menjalankan file main.tf dengan baik.

[https://lh5.googleusercontent.com/KsbJztQ9eqrkvdwcw8cUAFOWne78UIJAXFMIhSxOZsbXTW-4zHaxBtc4iNWfWGneCXTqjPy-FtjFT97JlQNYpaAaCD9aTsyqig7FepAi0VodCFGZvFr5J7lkjChKxDejWIpmpwqc8d2wnmxHQJsn4A](https://lh5.googleusercontent.com/KsbJztQ9eqrkvdwcw8cUAFOWne78UIJAXFMIhSxOZsbXTW-4zHaxBtc4iNWfWGneCXTqjPy-FtjFT97JlQNYpaAaCD9aTsyqig7FepAi0VodCFGZvFr5J7lkjChKxDejWIpmpwqc8d2wnmxHQJsn4A)

Untuk melihat hasilnya pada dashboard EC2, kita akan melihat perubahan nama yang sudah kita lakukan sebelumnya.

[*Hasil Manage EC2 Terraform*](https://lh6.googleusercontent.com/2zLWNh19RpGlD-42wB3ROKmhNjlJgk2bB3VrkfzJBduxKCBfujLzszmHqkd3WezF-VDthrLFwpwopauVmwXxHTxVKWBh9R1ftaLo_jyOk7PjaUvw5grzows5HGiEQHBnCF-h6mzMDl_nK-iy4dRQYw)

*Hasil Manage EC2 Terraform*

## ***Menghapus EC2***

Untuk mendelete atau destroy EC2 yang sudah kita buat tadi, sekarang cukup dengan menjalankan perintah seperti di bawah ini.

```bash
terraform destroy
```

[https://lh6.googleusercontent.com/k5l28s5ZpZ1E2jnfgvOdfYdmALKw_PLx9fHSWJPa9pqFTwdnWLgEVO9C5DJuXa0uVy0-0NhYx8nNtLVR30NaC3IydTtfbIZcydnD73An8SaSZfz0HjmaeJhvHfln9blSIzHhFW2LyWICIgwbgu5juA](https://lh6.googleusercontent.com/k5l28s5ZpZ1E2jnfgvOdfYdmALKw_PLx9fHSWJPa9pqFTwdnWLgEVO9C5DJuXa0uVy0-0NhYx8nNtLVR30NaC3IydTtfbIZcydnD73An8SaSZfz0HjmaeJhvHfln9blSIzHhFW2LyWICIgwbgu5juA)

Untuk konfirmasi menghapus resource, ketikan yes

[https://lh6.googleusercontent.com/RzTHf99JPwL-4Hc3AAkAHGTZ6jHC5YyNfF7LW8Dh9-ducf6t0I5drBOMBc4Tl5eluoiwyre5fnj7-NcMNPujmj-7OrnDDwVhlobhdH7GJSHbWcGvCiZwMPMRU2Uc92v5Wv702QoLb-Q29uF-HYMo0w](https://lh6.googleusercontent.com/RzTHf99JPwL-4Hc3AAkAHGTZ6jHC5YyNfF7LW8Dh9-ducf6t0I5drBOMBc4Tl5eluoiwyre5fnj7-NcMNPujmj-7OrnDDwVhlobhdH7GJSHbWcGvCiZwMPMRU2Uc92v5Wv702QoLb-Q29uF-HYMo0w)

Tunggu beberapa saat agar Terraform menghapus resource.

[https://lh5.googleusercontent.com/2TWe8rOofly-uFGeuS_DaBmoUxpjmGXt2tj-FEAIB1UNlMrEnfELhoOZec0-AsWFECTVC-WvU9XIhWd7lMAyBw6EBwMJtcRYGGJPFrQKbOQ6QGwrkMjPpNpoNCtHkh5ExX1VGFhnkmUrY6417XfdPw](https://lh5.googleusercontent.com/2TWe8rOofly-uFGeuS_DaBmoUxpjmGXt2tj-FEAIB1UNlMrEnfELhoOZec0-AsWFECTVC-WvU9XIhWd7lMAyBw6EBwMJtcRYGGJPFrQKbOQ6QGwrkMjPpNpoNCtHkh5ExX1VGFhnkmUrY6417XfdPw)

Cek **dashboard EC2** kita dapat melihat seperti di atas ini. Apakah resource berubah menjadi **terminated** ?

# **Konfigurasi S3**

## ***Membuat Bucket S3***

Selanjutnya pada bagian ini kita akan coba membuat Bucket S3 baru menggunakan Terraform, pada pembahasan di atas kita tidak membahas mengenai script yang ada pada pembuatan S3 dikarenakan tidak banyak script yang akan kita gunakan, maka kita akan jelaskan disini sembari mencobanya.

Untuk buat sebuah direktori baru didalam direktori terraform yaitu S3 seperti dibawah ini.

[https://lh5.googleusercontent.com/dxRUKaeKFyx90ZqUvbCbaL5KSAW9IYFXGsPCO-jhrVRSST5fF8WhQTnjwRfcftK--b2V6eEjpPuw6VfAHuK1ziWMJDsX71-1EgkzpVBqIZBx52Dkc2824zKvK8WL-oO9ICWGrpuS5Nsns616g9s3uA](https://lh5.googleusercontent.com/dxRUKaeKFyx90ZqUvbCbaL5KSAW9IYFXGsPCO-jhrVRSST5fF8WhQTnjwRfcftK--b2V6eEjpPuw6VfAHuK1ziWMJDsX71-1EgkzpVBqIZBx52Dkc2824zKvK8WL-oO9ICWGrpuS5Nsns616g9s3uA)

Setelah itu masuk kedalam folder s3 tersebut, kita lihat file main.tf. Konfigurasinya tidak jauh sama dengan EC2, namun kali ini ada beberapa input/argument khusus resource s3 bucket seperti bucket, acl, versioning dll. Seperti biasa, dokumentasi nya ada [disini](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket).

```bash
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "4.9.0"
    }
  }
}

provider "aws" {
  access_key = "AKIA5CHGDFVPGKW2FWGF"
  secret_key = "*******wxYwinxVgf/hLkrwCKMCF1FM5DQ6k2Kll"
  region = "us-east-2"
}

resource "aws_s3_bucket" "bucket_devops_cilsy" {
  bucket = "bucket-devops-cilsy"
  acl = "private"
  
  versioning {
    enabled = true
  }

  tags = {
    Name = "bucket-devops-cilsy"
  }
}
```

Setelah itu simpan konfigurasi tersebut. Jika kita lihat pada script diatas tidak berbeda jauh dengan konfigurasi pembuatan EC2 pada bagian sebelumnya, dan jika kalian memahami cara pembuatan S3 sendiri mungkin tidak akan terlalu sulit pada saat melihat maksud dari script diatas.

Untuk beberapa opsional script lanjutan pada S3 ini dapat kalian akses melalui web documentasi official dari terraform sendiri, yaitu sebagai berikut : [https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket)

Lanjut pada pembuatan, selanjutnya kita jalankan init, dan plan pada folder S3 tersebut.

```bash
terraform init
```

[https://lh5.googleusercontent.com/-Sx1r5ZaMHjfxew1k991bjZ3UasaWd4hBhakHcnztVE7a-4dstAWv-0zKmuIq0cuSjFljDkaZZbW19rKgWYu8Lzoc72ksgeUXAleJXGaFnUjah24tw4iqjlQcHAQRlL97GExlEE0WafkJwOeshvKBg](https://lh5.googleusercontent.com/-Sx1r5ZaMHjfxew1k991bjZ3UasaWd4hBhakHcnztVE7a-4dstAWv-0zKmuIq0cuSjFljDkaZZbW19rKgWYu8Lzoc72ksgeUXAleJXGaFnUjah24tw4iqjlQcHAQRlL97GExlEE0WafkJwOeshvKBg)

Lalu kita lakukan perintah berikut untuk melihat konfigurasi yang akan dibangun.

```bash
terraform plan
```

[https://lh4.googleusercontent.com/D9GXe_ufUpePL7L4ngYQUzGmLCSmeWP4els6KaGY2IoF9nwAqflxMSimPl9hhzQLIO8XCU9qRxmjOMpYgy-Q0gUKQ-NYeLxm7NHCB9ii8lwJMZYLn05vvcT_3j5bG9ZfC6iRd3ryv_129l2rD9H-7A](https://lh4.googleusercontent.com/D9GXe_ufUpePL7L4ngYQUzGmLCSmeWP4els6KaGY2IoF9nwAqflxMSimPl9hhzQLIO8XCU9qRxmjOMpYgy-Q0gUKQ-NYeLxm7NHCB9ii8lwJMZYLn05vvcT_3j5bG9ZfC6iRd3ryv_129l2rD9H-7A)

Setelah berhasil melakukan terraform plan, selanjutnya kita jalankan apply untuk membuild bucket S3 menggunakan terraform.

```bash
terraform apply
```

[https://lh3.googleusercontent.com/Wsy-IONVzQL7s6oVMTfzE-EOgjob9dJLDL87QaCADUgVoJr5l1lKT-SWD67LgEdF5g-9s29tekcTVwAlzRYTM8yO1XCUIpgue8_auT2fV_50nRfl8p0Y-wOI0dUGERwtKS8x6rKGkENQuOgvvgSkBg](https://lh3.googleusercontent.com/Wsy-IONVzQL7s6oVMTfzE-EOgjob9dJLDL87QaCADUgVoJr5l1lKT-SWD67LgEdF5g-9s29tekcTVwAlzRYTM8yO1XCUIpgue8_auT2fV_50nRfl8p0Y-wOI0dUGERwtKS8x6rKGkENQuOgvvgSkBg)

[https://lh6.googleusercontent.com/nZUzLkWoSPIdU3tOz38ijLZkBaEtrRy6KAaQPPF0djneoD8QKlxNLzRkIoye-F37pLxcdYqLBXiNmpnYV47zHxdutt8_XTmkvDW8afdefInkWzqB9PexOlkoFbqy2XZtFhL4o_JwYNVzNpVPFfb9_Q](https://lh6.googleusercontent.com/nZUzLkWoSPIdU3tOz38ijLZkBaEtrRy6KAaQPPF0djneoD8QKlxNLzRkIoye-F37pLxcdYqLBXiNmpnYV47zHxdutt8_XTmkvDW8afdefInkWzqB9PexOlkoFbqy2XZtFhL4o_JwYNVzNpVPFfb9_Q)

jangan lupa untuk konfirmasi dengan mengetik yes

[https://lh5.googleusercontent.com/hVqePeop_zY6usX0GDfzoctcZY_UtnkD49bGh9fFRppg3nKBTJASzuJUedMJZ-0i-38srRsBnHWIsaPj8qBfdMqlfCS7b8JeGv1YOPNaVWa7X7jWj8VQ7jqLVBAjLFJbwfoXEfR236RJBo-h6eU-Bw](https://lh5.googleusercontent.com/hVqePeop_zY6usX0GDfzoctcZY_UtnkD49bGh9fFRppg3nKBTJASzuJUedMJZ-0i-38srRsBnHWIsaPj8qBfdMqlfCS7b8JeGv1YOPNaVWa7X7jWj8VQ7jqLVBAjLFJbwfoXEfR236RJBo-h6eU-Bw)

[https://lh6.googleusercontent.com/PX64-itEhvftSo47ZjPCd_pK8TlF8fSERJg99pcPp_Ir9-5HlSF1FuZghI65z_yHgEs5MNyP5VJWXMxuqTirHvrnR_dg3ZfUllpq_sXt5yzsPYxlXiCw_EGWgFWeumLHeGvwZVrrBQqi8-DLxfQoSQ](https://lh6.googleusercontent.com/PX64-itEhvftSo47ZjPCd_pK8TlF8fSERJg99pcPp_Ir9-5HlSF1FuZghI65z_yHgEs5MNyP5VJWXMxuqTirHvrnR_dg3ZfUllpq_sXt5yzsPYxlXiCw_EGWgFWeumLHeGvwZVrrBQqi8-DLxfQoSQ)

Setelah berhasil, kita bisa lihat hasilnya didalam console AWS untuk S3 seperti berikut

[https://lh6.googleusercontent.com/ux9NQ74C57zpV25YqW__1XTE8Cgl0RthgK0ZQ7exhvYy3np-N9h3v8NNIudSPSlLr5tp5fvWVdnWW-V1Tqq7c-jteP_JS-wkGq2hmkZ0M-qQm4Zvwot3ASY_IIvkMam72QEfrmPjqWXxqdlE1jpWIw](https://lh6.googleusercontent.com/ux9NQ74C57zpV25YqW__1XTE8Cgl0RthgK0ZQ7exhvYy3np-N9h3v8NNIudSPSlLr5tp5fvWVdnWW-V1Tqq7c-jteP_JS-wkGq2hmkZ0M-qQm4Zvwot3ASY_IIvkMam72QEfrmPjqWXxqdlE1jpWIw)

Dengan begini pembuatan S3 menggunakan terraform sudah berhasil dilakukan, kalian dapat mencoba untuk memodifikasi script yang ada dengan tambahan komponen yang lainnya.

## ***Manage Bucket S3***

Sama seperti EC2, segala perubahan pada file main.tf bisa dimaintain untuk di apply. Misalnya mengubah nama bucket dan lain lain.

Setelah itu, jalankan perintah berikut

```bash
terraform planterraform apply
```

Terakhir, konfirmasi dengan mengetik yes.

## ***Menghapus Bucket S3***

Untuk mengapusnya sendiri perintahnya tidak berbeda dengan penghapusan EC2 sebelumnya, kita bisa menggunakan perintah berikut.

```bash
terraform destroy
```

Lalu konfirmasi dengan mengetik yes.

# **Konfigurasi Amazon RDS**

## ***Membuat Database RDS***

Selanjutnya pada bagian ini kita akan coba melakukan konfigurasi pada Amazon RDS, sehingga kita dapat membuat sebuah database RDS baru dengan menggunakan terrafrom. Konfigurasi tersebut bisa kalian dapatkan di link yang sebelumnya sudah diberikan, disana akan terdapat dua file yaitu **main.tf** dan **variable.tf**

[https://lh6.googleusercontent.com/MOJNAUWotyqlmaxE6wYO_VBk47CiHwCVI9oD-jzq6DoyLaGlmxrgx-b_8Rk43mWY_eLofKymqIlwSmN-b_A7eyZHeWnqTT8t510cBR9KcszieEXk2rZeHtfCYUhg0RzoD04WG-RwzDR3yCUVvbWFKA](https://lh6.googleusercontent.com/MOJNAUWotyqlmaxE6wYO_VBk47CiHwCVI9oD-jzq6DoyLaGlmxrgx-b_8Rk43mWY_eLofKymqIlwSmN-b_A7eyZHeWnqTT8t510cBR9KcszieEXk2rZeHtfCYUhg0RzoD04WG-RwzDR3yCUVvbWFKA)

Kita dapat coba untuk menyesuaikan isi yang ada pada file **variable.tf** seperti dibawah ini, sebagai contoh yang kita akan coba buat disini adalah database mysql.

```bash
variable "aws_access_key" {
    default = "AKIA5CHGDFVPB3GEAVPJ"
}

variable "aws_secret_key" {
    default = "lt7foQ/I3m23BY86AbJtAV5Izkv2ZN*******"
}

variable "db_instance" {
  default = "db.t2.micro"
}

variable "rds_engine" {
  default = "mysql"
}

variable "rds_engine_version" {
  default = "5.7"
}

variable "rds_identifier" {
  default = "terraformrds"
}

variable "rds_db_name" {
  default = "terraformrds"
}

variable "rds_db_username" {
  default = "devopscilsy"
}

variable "rds_db_password" {
  default = "1234567890"
}

variable "rds_parameter_group_name" {
  default = "default.mysql5.7"
}
```

Disana kalian dapat melakukan set pada database yang akan digunakan, database name, password dan juga identifier pada RDS yang akan kalian buat. Untuk parameter lebih detailnya kalian dapat mengakses pada situs resminya berikut. [https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/db_instance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/db_instance)

Lanjut pada pembuatan, selanjutnya kita jalankan init, dan plan pada folder rds tersebut.

```bash
terraform initterraform plan
```

[https://lh6.googleusercontent.com/S0xZIoX6yyLjq9j3PztgdHhAKZyR5fgbs_fhavoiLSbim8fLHAMLpGqGbOjsfAx4-3NRvztir7rxopPz43rYyS5Y9VUINRN5PHirKC_803ZRBH1O2GNa9CLwKP2sfZiMTied65S_bZmhctQF0UJ_dQ](https://lh6.googleusercontent.com/S0xZIoX6yyLjq9j3PztgdHhAKZyR5fgbs_fhavoiLSbim8fLHAMLpGqGbOjsfAx4-3NRvztir7rxopPz43rYyS5Y9VUINRN5PHirKC_803ZRBH1O2GNa9CLwKP2sfZiMTied65S_bZmhctQF0UJ_dQ)

Setelah berhasil melakukan terraform plan, selanjutnya kita jalankan apply untuk membuild database RDS menggunakan terraform. Memang proses ini membutuhkan waktu sekitar 15-17 menit. Jadi siapkan kopi untuk santai sejenak.

```bash
terraform apply
```

[https://lh3.googleusercontent.com/2OLDpcNgcPQPoTiKVZ2tGkpQkZKnnodzq3JKzT3NDE8oQFSyo6rQ_YXuT_4b0ORGrxn__pzO3Q37mVdY9UISTY0-qftNfjNE2ALnxMdeHv3Wlp3clsNT42W_PKK7N18BvMeX7Tz6YAVUM5tLaZd7Dg](https://lh3.googleusercontent.com/2OLDpcNgcPQPoTiKVZ2tGkpQkZKnnodzq3JKzT3NDE8oQFSyo6rQ_YXuT_4b0ORGrxn__pzO3Q37mVdY9UISTY0-qftNfjNE2ALnxMdeHv3Wlp3clsNT42W_PKK7N18BvMeX7Tz6YAVUM5tLaZd7Dg)

Setelah berhasil, kita bisa lihat hasilnya didalam console AWS untuk melihat database RDS tersebut seperti berikut.

[https://lh4.googleusercontent.com/7Eug6kXI7dTNuYg7ASAgiNiaRXpy7X8Vb0DQtgxqrGy080OhmyeGfA6htJOYPg3ktbnSFlD9DhkP_GCOeiQuL9whEn1hPBrQVLrtQnR4D6BaxniDnt34QgwT88gHJp5Ejq5hGvW5sWQ3XR63HekAuw](https://lh4.googleusercontent.com/7Eug6kXI7dTNuYg7ASAgiNiaRXpy7X8Vb0DQtgxqrGy080OhmyeGfA6htJOYPg3ktbnSFlD9DhkP_GCOeiQuL9whEn1hPBrQVLrtQnR4D6BaxniDnt34QgwT88gHJp5Ejq5hGvW5sWQ3XR63HekAuw)

Dengan begini kita sudah berhasil membuat sebuah database mysql baru pada amazon RDS menggunakan terraform, kita dapat melakukan modifikasi pada database sesuai yang akan kita gunakan.

## ***Menghapus database RDS***

Untuk mengapusnya sendiri perintahnya tidak berbeda dengan sebelumnya, kita bisa menggunakan perintah berikut.

```bash
terraform destroy
```

# **Exercise**

Soal Praktek :

1. Build sebuah Instance baru mengguakan sistem operasi Amazon Linux dan Juga CentOS.
2. Build sebuah bucket S3 dan juga database mysql di RDS
3. Pastikan Semua Sistem Operasi , bucket dan database dapat diakses
4. Setelah semua dapat di akses, screenshot hasilnya.
5. Destroy semua instance, S3 dan database yang sudah dibuat