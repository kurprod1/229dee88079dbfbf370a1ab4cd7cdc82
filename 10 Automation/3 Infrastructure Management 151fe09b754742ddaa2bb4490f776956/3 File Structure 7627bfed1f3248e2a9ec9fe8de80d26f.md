# 3. File Structure

Created: July 25, 2022 3:12 PM

# **Struktur Folder Terraform**

Untuk memahami terraform sebelumnya, maka kita harus memahami struktur dari file atau terraform itu sendiri. Untuk kali ini struktur terraform di buat sebagai modul-modul yang dapat di gunakan berkali-kali dalam terraform. Berikut contoh atau gambar struktur terraform.

![*Ilustrasi Struktur folder terraform beserta isinya*](https://lh4.googleusercontent.com/pChye_6F9MjQm5gRh3_6HMs7gnXNGcS7-T0FVXgxCXvaFlAVZcXgdZ5hewIP-YT-2rv4kUwaQrh6teNjXz2bY0jF7EJOR_Qs3q3VurJ4RRSWtXoqeKEVfXfhameWBAk80Rqd4dJ7O3od5-0UFIs5qA)

*Ilustrasi Struktur folder terraform beserta isinya*

Pada gambar di atas dapat kita lihat ada folder utama yaitu teraform, selanjutnya ada sub folder **ec2** dengan file **main.tf** dan **variables.tf** dengan fungsi sebagai berikut :

1. main.tf : konfigurasi utama yang berisikan parameter untuk membuat ec2. Disini ada beberapa parameter yang dibiarkan default. Untuk lebih lengkapnya, silahkan baca dokumentasi aws intance provider aws [disini](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance).
2. variables.tf : berisi variable variable yang digunakan pada main.tf. Kita bisa memanggilnya dengan syntax var.(nama variable).

Pada terraform, ada yang dinamakan module. Module ini merupakan kumpulan file dengan ekstensi .tf yang berada dalam 1 directory. Berarti **main.tf** dan **variables.tf** merupakan 1 module didalam directory **ec2**.

Dengan adanya module ini, kita tidak perlu mendefinisikan mana **variables.tf** pada **main.tf** karena Terraform mengevaluasi semua file konfigurasi dalam sebuah module, secara efektif memperlakukan seluruh module sebagai satu dokumen. Memisahkan berbagai blok ke dalam file yang berbeda adalah murni untuk kenyamanan pembaca dan pengelola, dan tidak berpengaruh pada perilaku modul.

# **File dan Penjelasan fungsinya**

## ***File main.tf***

Berikut akan kita jabarkan isi dari file **main.tf** yang berada pada direktori **module/ec2/**

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
  access_key = var.aws_access_key
  secret_key = var.aws_secret_key
  profile = "default"
  region = var.region
}

resource "aws_instance" "devops" {
  ami = var.ami
  instance_type = var.instance_type
  key_name = var.key_name
  vpc_security_group_ids = var.vpc_security_group_ids
  associate_public_ip_address = var.associate_public_ip_address
  count = var.instance_count
  
  root_block_device {
    volume_type           = var.volume_type
    volume_size           = var.root_volume_size
    delete_on_termination = var.delete_on_termination
  }
  
  ebs_block_device {
    device_name = "/dev/sdb"
    volume_size = var.volume_size
    volume_type = var.volume_type
  }

  tags = {
    Name = var.tags["name"]
    Purpose = var.tags["purpose"]
    Env = var.tags["env"]
  }

  volume_tags = {
    Name = var.tags["name"]
    Purpose = var.tags["purpose"]
    Env = var.tags["env"]
  }

  provisioner "remote-exec" {
    inline = [
      "sudo apt update && sudo apt upgrade -y",
      "sudo apt install nginx -y"
    ]

    connection {
      host = self.public_ip
      type = "ssh"
      user = "ubuntu"
      private_key = "${file("/home/taufik/Documents/kerja/cilsy/modul/Sekolah Devops/taufik_kurikulum_kp.pem")}"
    }
  }
}
```

File di atas merupakan file lengkap dari **main.tf**, selanjutnya akan kita coba jabarkan secara detail isi dari file tersebut agar kita memahami isi dari script yang ada pada file tersebut.

- Block dibawah mendefinisikan provider yang kita akan gunakan yaitu AWS dari hashicorp sendiri dan versi Terraform yang digunakan. Selengkapnya, provider bisa dilihat [disini](https://registry.terraform.io/).
    
    ```bash
    terraform {
      required_providers {
        aws = {
          source = "hashicorp/aws"
          version = "4.9.0"
        }
      }
    }
    ```
    
- Block provider aws ini mendeklarasikan access key untuk membuat resource melalui Terraform pada region yang telah ditentukan
    
    ```bash
    provider "aws" {
      access_key = var.aws_access_key
      secret_key = var.aws_secret_key
      profile = "default"
      region = var.region
    }
    ```
    
- Perintah dibawah berguna untuk memanggil fungsi untuk membuat atau create, mengubah atau change , dan juga hapus atau destroy **EC2**. Ada banyak resource yang bisa kita manage, dokumentasi lengkapnya [disini](https://registry.terraform.io/providers/hashicorp/aws/latest/docs).
    
    ```bash
    resource "aws_instance" "devops" {
    ```
    
- Perintah dibawah berguna untuk memanggil atau deklarasi dari ami yang akan di gunakan. Misal dengan ubuntu dan centos dan lain-lain. Pada praktikum ini, AMI yang digunakan adalah Ubuntu Server 18.04 LTS (HVM).
    
    ```bash
    ami = var.ami
    ```
    
- Perintah dibawah berguna untuk memilih type instance yang akan di gunakan.
    
    ```bash
    instance_type = var.instance_type
    ```
    
- Perintah dibawah berguna untuk file key-pair yang akan di gunakan. Pada bagian setup, sudah disebutkan disini saya menggunakan key-pair yang sudah dibuat sebelumya.
    
    ```bash
    key_name = var.key_name
    ```
    
- Perintah dibawah berguna untuk memanggil dan memilih security group yang akan di gunakan. Pada bagian setup, sudah disebutkan disini saya menggunakan security group yang sudah dibuat sebelumya.
    
    ```bash
    vpc_security_group_ids = var.vpc_security_group_ids
    ```
    
- Perintah dibawah berguna untuk memanggil dan memilih ip publik akan di gunakan.
    
    ```bash
    associate_public_ip_address = var.associate_public_ip_address
    ```
    
- Perintah dibawah berguna untuk memanggil dan membuat EC2 sebanyak kita ingin kan.
    
    ```bash
    count = var.instance_count
    ```
    
- Pada perintah dibawah berguna untuk mengatur hardisk yang ingin digunakan, untuk hardisk ada 2 macam, pertama adalah **root block** seperti dibawah, selanjutnya adalah **EBS**.
    
    ```bash
    root_block_device {
      volume_type           = var.volume_type
      volume_size           = var.root_volume_size
      delete_on_termination = var.delete_on_termination
    }
    ```
    
- Seperti **root block**, **EBS** berguna sebagai hardisk yang akan di gunakan oleh EC2. Beda nya dengan root block, EBS adalah sebagai tempat untuk folder-folder home, opt dan lain-lain dari linux di dalam EC2.
    
    ```bash
    ebs_block_device {
        device_name = "/dev/sdb"
        volume_size = var.volume_size
        volume_type = var.volume_type
    }
    ```
    
- Selanjutnya adalah perintah tags. Seperti di perintah dibawah, perintah ini berguna untuk mengatur Nama yang akan di gunakan, hal yang di perlukan sebenarnya adalah Name saja, namun yang lain seperti Purpose atau Env merupakan tambahan saja.
    
    ```bash
    tags = {
      Name = var.tags["name"]
      Purpose = var.tags["purpose"]
      Env = var.tags["env"]
    }
    ```
    
- Selanjutnya selain pada EC2 kita juga dapat mengatur untuk volume atau EBS yang kita buat, sama seperti dengan perintah tags pada EC2 di atas.
    
    ```bash
    volume_tags = {
        Name = var.tags["name"]
        Purpose = var.tags["purpose"]
        Env = var.tags["env"]
    }
    ```
    
- Terdapat perintah yang terakhir pada file **main.tf** yaitu adalah **provisioner**, fungsi provisioner berguna untuk provisioning, atau untuk menginstall paket-paket atau aplikasi pada linux yang berada di EC2.
    
    Pada perintah dibawah kita dapat mengatur paket installasi yang akan kita installkan seperti contoh dibawah yaitu update repository, install **nginx**,
    
    Pada connection kita menggunakan ip public instance via **ssh** dengan user **ubuntu**, sedangkan private key dapat kita sesuaikan dengan lokasi file tersebut berada.
    
    ```bash
    provisioner "remote-exec" {
        inline = [
          "sudo apt update && sudo apt upgrade -y",
          "sudo apt install nginx -y"
        ]
    
        connection {
          host = self.public_ip
          type = "ssh"
          user = "ubuntu"
          private_key = "${file("/home/taufik/Documents/kerja/cilsy/modul/Sekolah Devops/taufik_kurikulum_kp.pem")}"
        }
      }
    }
    ```
    

## ***File Variable***

Berikut akan kita jabarkan isi dari file variable.tf yang berada pada direktori **module/ec2/**

```bash
variable "aws_access_key" {
    default = "AKIA5CHGDFVPGKW2FWGF"
}

variable "aws_secret_key" {
    default = "******wxYwinxVgf/hLkrwCKMCF1FM5DQ6k2Kll"
}

variable "region" {
  default = "us-east-1"
}

variable "availability_zone" {
    default = "us-east-1a"
}

variable "ami" {
    default = "ami-0e472ba40eb589f49"
}

variable "instance_type" {
    default = "t2.micro"
}

variable "root_volume_size" {
    default = 8 
}

variable "instance_count" {
    default = 1
}

variable "delete_on_termination" {
    default = true
}

variable "volume_size" {
    default = 20
}

variable "volume_type" {
    default = "gp2"
}

variable "key_name" {
    default = "taufik_kurikulum_kp"
}

variable "vpc_security_group_ids" {
    default = ["sg-0d1878abf7b359496"]
}

variable "associate_public_ip_address" {
    default = true
}

variable "tags" {
    type = map(string)
    default = {
        "name" = "sekolah-devops-instance"
        "purpose" = "praktikum-sekolah-devops"
        "env" = "dev"
    }
}
```

Perintah di atas merupakan file yang berasal dari **variable.tf.** File ini berisikan variable atau parameter yang akan di gunakan. Pada file ini berguna untuk mendefinisikan varible secara default. Berikut akan kita jelaskan setiap bagian dari isi file **variable.tf** tersebut.

- Pada perintah dibawah berguna untuk mendefinisikan aws access key dan secret key yang akan di gunakan pada **main.tf**. Pada bagian sebelumnya sudah dijelaskan bagaimana cara mendapatkannya.
    
    ```bash
    variable "aws_access_key" {
        default = "AKIA5CHGDFVPGKW2FWGF"
    }
    
    variable "aws_secret_key" {
        default = "******wxYwinxVgf/hLkrwCKMCF1FM5DQ6k2Kll"
    }
    ```
    
- Selanjutnya adalah variable untuk mengatur **region.** Pada praktikum ini, region yang digunakan adalah **us-east-1** atau region North Virginia.
    
    ```bash
    variable "region" {  default = "us-east-1"}
    ```
    
- Untuk daftar code region sendiri dapat kita lihat seperti tabel dibawah ini atau pada [link berikut](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-regions).
    
    ![*Daftar code region AWS*](https://lh5.googleusercontent.com/zq63GgTOGaxl2XB4vDbxF2xaSvlcv_vYTz8iGr4na1rS3EOpBu-ipwKT8PPsrZIpwl2pVREvunHY-n-9rEjynQOBYhyN4EirKqzfC6BK2i09-U_fpmLqIL3bVN6_MpC4rW_imk5lvq1vDQ8RgdPYZA)
    
    *Daftar code region AWS*
    

- Untuk zone N. Virginia kita dapat menggunakan us-east-1a atau us-east-1b seperti perintah dibawah. Availability zone dapat dilihat [disini](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-availability-zones).
    
    ```bash
    variable "availability_zone" {    default = "us-east-1a"}
    ```
    
- Perintah dibawah untuk mendefinisikan ami atau distro iso yang digunakan, kali ini kita dapat menggunakan ami dari distro ubuntu 18.04.
    
    ```bash
    variable "ami" {    default = "ami-0e472ba40eb589f49"}
    ```
    
- Untuk melihat ami-ami yang lain kita dapat melihat saat kita lauch EC2 seperti di bawah ini. Bisa kita lihat code AMI pada Ubuntu Server 18.04 LTS adalah **ami-0e472ba40eb589f49**. Perlu diingat, ami pada setiap region berbeda meskipun dengan nama yang sama.
    
    ![*Code AMI Image AWS*](https://lh6.googleusercontent.com/RGLiN8UvKWhTy0jLgIAqPHRF_xUxxQB-f2b1ce97ozPnS6rsiTj2RfgvDq_1RprJFOWSO8IVo_Ak5T3FkhgflcqyPv3bYPAUi2VQcaP-BX1B_V53tovsHyWdC0DLVW5ltSd6l0cMAKx7XC3fQEwCCA)
    
    *Code AMI Image AWS*
    

- Perintah dibawah berguna untuk memberikan nilai default variable yaitu t2.micro, t2.micro merupakan type pada EC2 AWS, semakin tinggi type maka spesifikasi server instance akan semakin tinggi
    
    ```bash
    variable "instance_type" {    default = "t2.micro"}
    ```
    
- Untuk pilihan type instance yang lainnya, kita dapat melihat pada pada gambar dibawah ini maupun pada link berikut [https://aws.amazon.com/id/ec2/instance-types/](https://aws.amazon.com/id/ec2/instance-types/)
- Pada perintah dibawah memberikan atau mendefinisikan variable default untuk hardisk root storage adalah 8 GB.
    
    ```bash
    variable "root_volume_size" {    default = 8 }
    ```
    
- Pada perintah dibawah memberikan atau mendefinisikan variable default jumlah instance yang ingin di buat adalah 1 server instance.
    
    ```bash
    variable "instance_count" {    default = 1}
    ```
    
- Pada perintah dibawah memberikan atau mendefinisikan variable default true saat menghapus EC2, maka hardisk yang sebelumnya telah di buat akan di hapus juga.
    
    ```bash
    variable "delete_on_termination" {    default = true}
    ```
    
- Pada perintah dibawah memberikan atau mendefinisikan variable default untuk hardisk EBS adalah 20 GB.
    
    ```bash
    variable "volume_size" {    default = 20}
    ```
    
- Pada perintah dibawah memberikan atau mendefinisikan variable default untuk hardisk type adalah gp2.
    
    ```bash
    variable "volume_type" {    default = "gp2"}
    ```
    
- Pada perintah dibawah memberikan atau mendefinisikan variable default untuk key_name adalah “taufik_kurikulum_kp".
    
    ```bash
    variable "key_name" {    default = "taufik_kurikulum_kp"}
    ```
    
    key_name dapat di buat pada menu key pairs pada halaman Dashboard EC2.
    
    ![https://lh4.googleusercontent.com/f1SrirR3trpvTNvB0bLM8nyOZqvq6h14fIegRtrqNijAJd2rbdChUw_zpfsBHYUiFSIm2xMJnyC8Ag-IVgr5FSjumS3WqXXYZspZlG6OsCpPxHwO0Aszmm1MvfPkg5uMiyO74xXTLWZkghWJOUqxOA](https://lh4.googleusercontent.com/f1SrirR3trpvTNvB0bLM8nyOZqvq6h14fIegRtrqNijAJd2rbdChUw_zpfsBHYUiFSIm2xMJnyC8Ag-IVgr5FSjumS3WqXXYZspZlG6OsCpPxHwO0Aszmm1MvfPkg5uMiyO74xXTLWZkghWJOUqxOA)
    
- Selanjutnya pada perintah dibawah, kita dapat mengatur default dari security group yang kita miliki, security group berguna sebagai firewall karena pada security group port-port atau ip di atur baik allow acces maupun deny access.
    
    ```bash
    variable "vpc_security_group_ids" {    default = ["sg-0d1878abf7b359496"]}
    ```
    
- Kita dapat melihat security group pada dashboard EC2 seperti di bawah ini.
    
    ![https://lh5.googleusercontent.com/lNVJXU2npsvmelJVeUJS3ki42cjIJYrV3mBOERdSFUssCnlOCfsyE1GvE27JmEiSFODrXKFVwUJyytGMoxuj6eoalXpUG8B0wXklpquqp8I_cFlJQ1jE-Z3kP0biT2-TH87XICQCHewIxqZ6c_OTmQ](https://lh5.googleusercontent.com/lNVJXU2npsvmelJVeUJS3ki42cjIJYrV3mBOERdSFUssCnlOCfsyE1GvE27JmEiSFODrXKFVwUJyytGMoxuj6eoalXpUG8B0wXklpquqp8I_cFlJQ1jE-Z3kP0biT2-TH87XICQCHewIxqZ6c_OTmQ)
    
- Perintah dibawah gunanya untuk memberikan nilai default **ip public**, secara default kita dapat membuat status true, sehingga setiap terraform di jalankan maka akan mendapatkan **ip public**.

```bash
variable "associate_public_ip_address" {    default = true}
```

- Pada perintah dibawah memberikan atau mendefinisikan variable default tags, tags di gunakan untuk memberikan nama atau deskripsi dari EC2 yang kita buat.
    
    ```bash
    variable "tags" {    type = map(string)    default = {        "name" = "sekolah-devops-instance"        "purpose" = "praktikum-sekolah-devops"        "env" = "dev"    }}
    ```
    

# **Exercise**

Soal Praktek :

1. Desain Sebuah infrastructure EC2 yang akan kalian buat.
2. Sesuaikan file-file konfigurasi terraform yang sudah dipelajari tadi sesuai dengan desain yang akan kalian buat, mulai dari Security Group, AMI, dan Subnet yang ada.