# 4. Ansible Tower

Created: July 25, 2022 6:27 PM

# **Mengenal Ansible Tower**

Ansible Tower  adalah sebuah provisioning tool yang dikembangkan oleh RedHat. Ansible memiliki tampilan visualisasi yang berguna untuk membantu dan memudahkan dalam menggunakan ansible. Ansible tower merupakan aplikasi yang berbayar, terdapat 2 paket ansible tower seperti gambar dibawah ini.

![https://lh3.googleusercontent.com/eEJDoAoS_FUmwNena860-V5njrqjbPhKiwJtmYm51fjQ9p9vUJJJXDnU-gv3uUaWLqjVJptMNJeidoY0VsPwUIXiVWeJnqE84TyWQIqPZRxEHn6dy48R_yNJDfjXMXZklRuTYovQGGdbFPiplYAdzA](https://lh3.googleusercontent.com/eEJDoAoS_FUmwNena860-V5njrqjbPhKiwJtmYm51fjQ9p9vUJJJXDnU-gv3uUaWLqjVJptMNJeidoY0VsPwUIXiVWeJnqE84TyWQIqPZRxEHn6dy48R_yNJDfjXMXZklRuTYovQGGdbFPiplYAdzA)

Disana terdapat kedua paket yang memiliki kelebihannya tersendiri seperti paket standart yang memberikan beberapa support selama 6x5. Sedangkan yang premium memiliki jadwal support sampai 24x7.

# **Fitur-Fitur Ansible Tower**

Ansible tower memiliki fitur yang lebih komplit dari pada ansible yang lain, hal ini di karenakan ansible tower memang berbayar, sehingga dapat dukungan penuh dari Redhat yang dapat memudahkan penggunanya, adapun fitur-fitur ansible tower sebagai berikut.

1. ***Dasbor Tower***
    
    Ansible menyediakan tampilan yang dapat membantu pekerjaan menjadi lebih mudah, pada dasbor ansible tower kita dapat melihat host dan status inventaris kita. Kita dapat mengatur pekerjaan dan status pekerjaan dengan sebuah grafik yang dapat di monitoring secara langsung. Berikut adalah gambarannya.
    
    ![https://lh3.googleusercontent.com/EY8dLWKgegcvaXczwhC3H5HnI8Ap4uGaRmF8IxOHOy7jlddeuSN4SoW5q0J0EoJcxapw9PhBzqEXz06rzx9LWcL47dZ1e6zjWdsJHQHfyVbP3juC2RpQWxNSfWL_mrrna6ihQzQydmQU83cwGXj1fg](https://lh3.googleusercontent.com/EY8dLWKgegcvaXczwhC3H5HnI8Ap4uGaRmF8IxOHOy7jlddeuSN4SoW5q0J0EoJcxapw9PhBzqEXz06rzx9LWcL47dZ1e6zjWdsJHQHfyVbP3juC2RpQWxNSfWL_mrrna6ihQzQydmQU83cwGXj1fg)
    
2. ***Streaming Real Time***
    
    Di dalam Ansible Tower, playbook menjalankan streaming secara real time. Saat Ansible mengotomatiskan seluruh infrastruktur, kita akan melihat pekerjaan dan tugas selesai pada setiap mesin dan setiap keberhasilan atau kegagalan deploy.
    
    ![https://lh6.googleusercontent.com/RVlPbM8FXda3DqnIwQ5buhKKJPNgl2fIIa5zHakcEN8Mv3fuzgSkQHUJWtTNLuzNKZP3rP-PQGwK67hYt8p9_pZFJ-ml5MMZ2-3alQjXbB1b_977VoVffTDXfNdAPZsB-Y-hv96F5MdTWqgCm6hCwQ](https://lh6.googleusercontent.com/RVlPbM8FXda3DqnIwQ5buhKKJPNgl2fIIa5zHakcEN8Mv3fuzgSkQHUJWtTNLuzNKZP3rP-PQGwK67hYt8p9_pZFJ-ml5MMZ2-3alQjXbB1b_977VoVffTDXfNdAPZsB-Y-hv96F5MdTWqgCm6hCwQ)
    
3. ***Multi-Playbook/Multi Job***
    
    Ansible Tower dapat menjalankan multi-playbook atau multi job secara sekaligus. Alur kerja Ansible tower memungkinkan banyak peoses. Kita dapat membangun kerja, menerapkan konfigurasi sistem , dan mendeploy aplikasi.
    
    ![https://lh6.googleusercontent.com/v8P_kpsC5WgIW0wF5bJgCI0-Ss7gqLpVAtu7VvTDR64Ia95n2-hizREohF7-ZjX2ZBDLSI2mntkkHpDmqtwYsbKCCmpGOgUZkFXTRYe1N-_AmTDHHxb1WUKJMS984YmCm3LA2ukktN8NCzKwBJo5fg](https://lh6.googleusercontent.com/v8P_kpsC5WgIW0wF5bJgCI0-Ss7gqLpVAtu7VvTDR64Ia95n2-hizREohF7-ZjX2ZBDLSI2mntkkHpDmqtwYsbKCCmpGOgUZkFXTRYe1N-_AmTDHHxb1WUKJMS984YmCm3LA2ukktN8NCzKwBJo5fg)
    
4. ***Secure***
    
    Dengan Ansible Tower, semua aktivitas otomasi disimpan dengan aman. Siapa yang menjalankannya, bagaimana mereka menyesuaikannya, apa yang dilakukannya, di mana itu terjadi semua disimpan dengan aman dan dapat dilihat kemudian, atau diekspor melalui API Ansible Tower.
    
    ![https://lh3.googleusercontent.com/L2TMr9bIjBGDMFrrcll0Djrn0eZcBGKNksdeDcpyI9BkibsVAWJoF2IYJ5kaj_096owKtV8KoKDB3LPgVjwGYKF7Vufeb3jiAVQ1l6BSbe9dL3Uu_JOBb2JHeYeihTx5hqyli8k8HFeRu3UvIAgsvw](https://lh3.googleusercontent.com/L2TMr9bIjBGDMFrrcll0Djrn0eZcBGKNksdeDcpyI9BkibsVAWJoF2IYJ5kaj_096owKtV8KoKDB3LPgVjwGYKF7Vufeb3jiAVQ1l6BSbe9dL3Uu_JOBb2JHeYeihTx5hqyli8k8HFeRu3UvIAgsvw)
    

# **Integrated Notification**

Ansible memiliki beberapa kelebihan lain yang diantaranya adalah integrasi dengan aplikasi slack. Dengan integrasinya ansible dan slack memungkinkan semua tim mendapatkan notifikasi ketika ansible dijalankan maupun berjalan.

![https://lh6.googleusercontent.com/oP5sZrkpMJl-ahuoLIVY2YqWA_SFt12877WmfOe0AlME5CDgRa2NkWc2tpiANrMJuTmVUBpwIb5ND1_hw320TEfsxhbrUlVw16UM9AQBO8mFk2RrNilBJDiJI6Mg-iwsxgVScJJd_FDprHhPftBbWg](https://lh6.googleusercontent.com/oP5sZrkpMJl-ahuoLIVY2YqWA_SFt12877WmfOe0AlME5CDgRa2NkWc2tpiANrMJuTmVUBpwIb5ND1_hw320TEfsxhbrUlVw16UM9AQBO8mFk2RrNilBJDiJI6Mg-iwsxgVScJJd_FDprHhPftBbWg)

# **Installasi Ansible Tower**

Pada bagian ini kita akan mempelajari bagaimana cara installasi ansible tower. Untuk tahap installasinya kita dapat mengklik launch instance di dashboard EC2 seperti di bawah ini.

![https://lh5.googleusercontent.com/rvbRkmJ6-0B-lLnyZWyE6glObKtG5oiV-inoa-mlVOD6GBGxbD_fCOc5z-2EZ4c7XNIlfSxN4GRIoCKq3L1UbhoClkEZvo9NIiwpK4ffUoI8yzSwGLldcj078yJt2QVPXB-kIoYuvBBht-pugi50og](https://lh5.googleusercontent.com/rvbRkmJ6-0B-lLnyZWyE6glObKtG5oiV-inoa-mlVOD6GBGxbD_fCOc5z-2EZ4c7XNIlfSxN4GRIoCKq3L1UbhoClkEZvo9NIiwpK4ffUoI8yzSwGLldcj078yJt2QVPXB-kIoYuvBBht-pugi50og)

Setelah itu pada bagian **search bar**, kita isikan **ansible-tower**, lalu kita klik **Community AMIs**. Kemudian pilih ansible tower dengan versi paling baru (disini v3.6.3, mungkin nanti ada pembaharuan) seperti gambar di bawah.

![https://lh5.googleusercontent.com/f96Blb4R8UHYGRU8A3jWQuyQBGbtI9Rw8l7sVBLWyqqT2zt_4a-sYxKKEYHSBhwgR0tmH6CA-ujIbuWehqGGT9B5SOEwtW29s2BrbjQkSQsczexJnKZXuYXwdDz7c4Ycv_RGeMHasw6zcRf3qBXavw](https://lh5.googleusercontent.com/f96Blb4R8UHYGRU8A3jWQuyQBGbtI9Rw8l7sVBLWyqqT2zt_4a-sYxKKEYHSBhwgR0tmH6CA-ujIbuWehqGGT9B5SOEwtW29s2BrbjQkSQsczexJnKZXuYXwdDz7c4Ycv_RGeMHasw6zcRf3qBXavw)

Selajutnya pilih type instance yang akan kita gunakan, disini kita gunakan t2.micro.

![https://lh5.googleusercontent.com/_XSDmPIpijqII-Ozu5n9wuw0B65OhfJvQ31HBvDsyq3-wRBhmBjNvVyeRtqGIQ7xRUDc5NbPiI2XkslZzdXcsPCWbr2QY7sWluIN9DX3kGfE_7PQ2LEVb3JDHhiNhNZNLA6yU3XrQt69WsergATrQg](https://lh5.googleusercontent.com/_XSDmPIpijqII-Ozu5n9wuw0B65OhfJvQ31HBvDsyq3-wRBhmBjNvVyeRtqGIQ7xRUDc5NbPiI2XkslZzdXcsPCWbr2QY7sWluIN9DX3kGfE_7PQ2LEVb3JDHhiNhNZNLA6yU3XrQt69WsergATrQg)

Kemudian lakukan konfigurasi pada storage, biarkan saja secara default. Setelah itu klik next untuk melanjutkan.

![https://lh3.googleusercontent.com/JXYTOwkEoKhCD6F2RlkLyEYvMPS7Q7g2W568Mg9e4LkVUBs2bzWYWiD9fS593t7A7pQw02--rpQhD8pWiQDM3Qy3Pqzz9G3gUXnK8USQAC8V8RI8NTo1SAdqRAWU7OCHx_iZvu_XGHtg2onYg1AcAw](https://lh3.googleusercontent.com/JXYTOwkEoKhCD6F2RlkLyEYvMPS7Q7g2W568Mg9e4LkVUBs2bzWYWiD9fS593t7A7pQw02--rpQhD8pWiQDM3Qy3Pqzz9G3gUXnK8USQAC8V8RI8NTo1SAdqRAWU7OCHx_iZvu_XGHtg2onYg1AcAw)

Selanjutnya adalah membuat nama tags, isikan nama tag seperti gambar di bawah , dan klik Next Configuration Security Group untuk melanjutkan.

![https://lh5.googleusercontent.com/X8cK_2ogXHxNlZ2lV9jdGagJ-aA3NIYqVEsq0I9Ua5psOGBukSkf6QuxZemtZBMyb5UapM_hbUicDH0xdOy79S1jkdLYLxNQ6OtpVfYzT7p8klp7rS09ObjP-zLVWgU3usYPM-gXmw-pb_Q0x0sttA](https://lh5.googleusercontent.com/X8cK_2ogXHxNlZ2lV9jdGagJ-aA3NIYqVEsq0I9Ua5psOGBukSkf6QuxZemtZBMyb5UapM_hbUicDH0xdOy79S1jkdLYLxNQ6OtpVfYzT7p8klp7rS09ObjP-zLVWgU3usYPM-gXmw-pb_Q0x0sttA)

Untuk bagian security group kita isikan beberapa protocol menggunakan port 80, 443, dan 22 seperti gambar dibawah ini.

![https://lh6.googleusercontent.com/B0_mdc3jEFazwFpe40--F65HftFGEIk4ZGdeDNi_FU8PSUWc-BS-i89-J34-r-r-_DzYGgcAJKlvi_S8EFcJXv6bHIkp9cSaK7IB2nnTgAvm9O9KGYELsdJtGamgJYAtoLCfzrouWLpvNJ5Zg_kCYw](https://lh6.googleusercontent.com/B0_mdc3jEFazwFpe40--F65HftFGEIk4ZGdeDNi_FU8PSUWc-BS-i89-J34-r-r-_DzYGgcAJKlvi_S8EFcJXv6bHIkp9cSaK7IB2nnTgAvm9O9KGYELsdJtGamgJYAtoLCfzrouWLpvNJ5Zg_kCYw)

Selanjutnya klik next hingga kita selesai membuat sebuah instance baru dengan menggunakan Ansible Tower yang berbayar.

Setelah selesai dikonfigurasi, kita dapat mengakses ansible tower dengan membuka browser dan mengetikan alamat server kita seperti di bawah ini.

![https://lh4.googleusercontent.com/kZIy1WnV2xDbwKQh_h81A7pm8TY3JaM6e8bLp66331_tLNMmoq7TfDXGOW0Ox5j3FQ-e3lwhXHqgCcNTA6nbxlKqZQF9-w83zJdtDHYQnxpZZLpsroUHAncgDF8Ybhyl9WvGhNYbaIR5K2U-Qj4neg](https://lh4.googleusercontent.com/kZIy1WnV2xDbwKQh_h81A7pm8TY3JaM6e8bLp66331_tLNMmoq7TfDXGOW0Ox5j3FQ-e3lwhXHqgCcNTA6nbxlKqZQF9-w83zJdtDHYQnxpZZLpsroUHAncgDF8Ybhyl9WvGhNYbaIR5K2U-Qj4neg)

Untuk mendapatkan username dan password untuk login pada web GUI Ansible, kita hanya perlu melakukan remote SSH terlebih dahulu pada server ansible tersebut. Lakukan perintah seperti gambar berikut, sehingga kita bisa mendapatkan user dan password login ansible.

![https://lh3.googleusercontent.com/0xuC4FhOJrazdtCu6mnFx7PghvSFXzlwT3d-2VI8ICKuX75xlHzACk2sYFfAfsOB_JUoUDbQXg57I1WofgS8GtrB6DD0DzC0ivlV107MHQ5918PrL6aFL8ebxvG0zYDP0ePL1tuODtp2hwP4vu4ZKw](https://lh3.googleusercontent.com/0xuC4FhOJrazdtCu6mnFx7PghvSFXzlwT3d-2VI8ICKuX75xlHzACk2sYFfAfsOB_JUoUDbQXg57I1WofgS8GtrB6DD0DzC0ivlV107MHQ5918PrL6aFL8ebxvG0zYDP0ePL1tuODtp2hwP4vu4ZKw)

Selanjutnya kita coba lakukan login dengan menggunakan username dan password yang sudah kita dapatkan tadi. Kemudian kita akan mendapat halaman untuk request free trial seperti di bawah ini. Klik tombol Requst Lisence.

![https://lh6.googleusercontent.com/azBCUTEaLq673tbe1LdH3BSmiwAE-mdbHb3yHTAw-zLMaljG5pXUF94Dw4mGmPQB5Im5koHHVzS1mesVcVHA7RrUFZZiYqtRUXSQWJG3oXaa9wd7DgOlBQF15KmyVEnzYZDd7x9TH7TbtA-RqhPbJw](https://lh6.googleusercontent.com/azBCUTEaLq673tbe1LdH3BSmiwAE-mdbHb3yHTAw-zLMaljG5pXUF94Dw4mGmPQB5Im5koHHVzS1mesVcVHA7RrUFZZiYqtRUXSQWJG3oXaa9wd7DgOlBQF15KmyVEnzYZDd7x9TH7TbtA-RqhPbJw)

Setelah request di klik, maka akan muncul tampilan dashboard seperti dibawah ini.

![https://lh4.googleusercontent.com/SQxVuWno3L3obJ1Yco894CbJTB9T2cOXWEAvy3BwZas_qXSmXthBS3OFJS3QG5rLATQLMiTdmXNkpZ92s8SEr7o3tupVfk4OKlsz9v3_6mSSEyp2Mzy19Aiv2fP5uqg91COdSssa_ekmMfQw76DHIw](https://lh4.googleusercontent.com/SQxVuWno3L3obJ1Yco894CbJTB9T2cOXWEAvy3BwZas_qXSmXthBS3OFJS3QG5rLATQLMiTdmXNkpZ92s8SEr7o3tupVfk4OKlsz9v3_6mSSEyp2Mzy19Aiv2fP5uqg91COdSssa_ekmMfQw76DHIw)

Jika kita sudah mendapatkan email konfirmasi, maka kita bisa ikuti link dan diarahkan ke halaman dashboard Ansible

![https://lh6.googleusercontent.com/k7x48SxxgV5fyCP8XPCIgcRmpw84kZqzsfZ0k9RzyBAMOP_O3G0blttxa3XqUfJ28nrvG_rDdaJvHN8Oqfa8utFGybTrhdqoMHRfdBnAvyJUnVhfgOCVvSAJbcZutCcUz8FI0E-sW2yipinUxLyKoA](https://lh6.googleusercontent.com/k7x48SxxgV5fyCP8XPCIgcRmpw84kZqzsfZ0k9RzyBAMOP_O3G0blttxa3XqUfJ28nrvG_rDdaJvHN8Oqfa8utFGybTrhdqoMHRfdBnAvyJUnVhfgOCVvSAJbcZutCcUz8FI0E-sW2yipinUxLyKoA)