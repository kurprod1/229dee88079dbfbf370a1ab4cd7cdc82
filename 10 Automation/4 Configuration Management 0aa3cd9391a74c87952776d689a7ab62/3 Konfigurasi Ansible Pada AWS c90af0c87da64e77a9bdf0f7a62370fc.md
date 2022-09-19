# 3. Konfigurasi Ansible Pada AWS

Created: July 25, 2022 6:18 PM

# **Install Web Server dengan Ansible Single Server**

## ***Konfigurasi EC2***

Pada bagian ini kita akan coba menginstallkan nginx dan php dengan menggunakan ansible pada 1 buah server EC2. Tahap pertama yang akan kita lakukan adalah membuat EC2, kita bisa membuatnya dengan mengikuti beberapa tahapan berikut.

![https://lh5.googleusercontent.com/biB8DN0TczXinH4sclDOJJ0S53VwCCL4yFdZnvHcJqFWF1P1hIsev4uTwD0FASv9uNIfY9VPy8xGEEAwwKYupUvruvCJk3aUNr2RnC_2dEhTW1lb9_hh6AISF8N8lfixFoQTR-UCrfwirUldhGA87A](https://lh5.googleusercontent.com/biB8DN0TczXinH4sclDOJJ0S53VwCCL4yFdZnvHcJqFWF1P1hIsev4uTwD0FASv9uNIfY9VPy8xGEEAwwKYupUvruvCJk3aUNr2RnC_2dEhTW1lb9_hh6AISF8N8lfixFoQTR-UCrfwirUldhGA87A)

Setelah kita melakukan klik launch pada EC2 dashboar, sekarang kita pilih AMI Linux **Ubuntu Server 18.04** yang akan kita gunakan untuk ansible.

![https://lh3.googleusercontent.com/mMmJk48ZL_TFkhLcq6ZQSQuLwIMJFaVHyknsvTwNZQ_Dq26xbuB8p0LqLiOa7jWnBuJzdvMoum-qb10KCyv-22daDTWL4VajC9rd8PyrpY84cF6pGbZfOUncwsqcB3ObgX7NMbTec66X8Ds9oOaCag](https://lh3.googleusercontent.com/mMmJk48ZL_TFkhLcq6ZQSQuLwIMJFaVHyknsvTwNZQ_Dq26xbuB8p0LqLiOa7jWnBuJzdvMoum-qb10KCyv-22daDTWL4VajC9rd8PyrpY84cF6pGbZfOUncwsqcB3ObgX7NMbTec66X8Ds9oOaCag)

Pilih type instance yang akan kita gunakan, menggunakan t2.micro saya rasa sudah cukup.

![https://lh6.googleusercontent.com/nIFoJnDN5tyQAuEYjuFeFtWK3AEfnzN9GQEjz3riG2y8IHttic81XNShgEyeZpXKe30JiYy5eSE2aAUT3BiYPVU_NmGNAvg4gSBDwoD8tNB6i3yC43-sjRZ6AFdFxWnfFoIcwNTjJc75BaJ-9JDqdw](https://lh6.googleusercontent.com/nIFoJnDN5tyQAuEYjuFeFtWK3AEfnzN9GQEjz3riG2y8IHttic81XNShgEyeZpXKe30JiYy5eSE2aAUT3BiYPVU_NmGNAvg4gSBDwoD8tNB6i3yC43-sjRZ6AFdFxWnfFoIcwNTjJc75BaJ-9JDqdw)

Pada langkah selanjutnya, kita biarkan default saja, kecuali anda ingin mengubah VPC, atau jumlah dari instancenya.

![https://lh3.googleusercontent.com/gGLnIikzxzCrbMhq83C-rLOaSqnaygzl8Vxs7gAph8R0FkobO5qFB_Go_p21K3_FWX9anZqX69_qtXz22S_evSijwJD0QPdO7WVv7pesyiNMuHENRl1e2obr0pvOm9M-nAZKTXfPpVC5QjlLB2U5Yg](https://lh3.googleusercontent.com/gGLnIikzxzCrbMhq83C-rLOaSqnaygzl8Vxs7gAph8R0FkobO5qFB_Go_p21K3_FWX9anZqX69_qtXz22S_evSijwJD0QPdO7WVv7pesyiNMuHENRl1e2obr0pvOm9M-nAZKTXfPpVC5QjlLB2U5Yg)

Kita akan masuk kedalam menu storage, disini kita biarkan saja default lalu klik Next.

![https://lh3.googleusercontent.com/OdXwVPu4ZiXHLUYyZ7l92ufZLq7b9T25FrbR7VgQAgqmT4NA2Mwvls3SwozoozanLIR37F8oaHaihsscPI_gs_Hs5VcEWo3Nf6a9ZFPDNy8A5nBNIchCd2u42Es09RL9olpVkaRGpOhASqw9Netehg](https://lh3.googleusercontent.com/OdXwVPu4ZiXHLUYyZ7l92ufZLq7b9T25FrbR7VgQAgqmT4NA2Mwvls3SwozoozanLIR37F8oaHaihsscPI_gs_Hs5VcEWo3Nf6a9ZFPDNy8A5nBNIchCd2u42Es09RL9olpVkaRGpOhASqw9Netehg)

Langkah selanjutnya adalah membuat nama tags. Isi **Name** dengan value **ansible**, lalu klik Next Configuration Security Group. 

![https://lh4.googleusercontent.com/NjJBpNGs1Er5OPe2r2z6rlDBB6LTn4-mcEf8xw9gqqbxIkglN3xNzj953p5uyf7UAWSqC6I8IKA1vV74lb-JqJ5fNOK5uXTadJ5jBqcI329zVxLjU0y_Z_ETUv2L3xPMNNqAqVBwtTtuWSWru7hAMA](https://lh4.googleusercontent.com/NjJBpNGs1Er5OPe2r2z6rlDBB6LTn4-mcEf8xw9gqqbxIkglN3xNzj953p5uyf7UAWSqC6I8IKA1vV74lb-JqJ5fNOK5uXTadJ5jBqcI329zVxLjU0y_Z_ETUv2L3xPMNNqAqVBwtTtuWSWru7hAMA)

Selanjutnya adalah bagian security group, buat sebuah type protocol dengan **SSH**, **TCP Port 8080** dan **ICMP IPv4** dengan source **anywhere** seperti gambar dibawah ini. Lalu klik review untuk melanjutkan.

![https://lh3.googleusercontent.com/tuyFL_fs3yCirVHk9f-fDiQ7MBdE44scvPfaOSjLqovs3bamc_56v4wjiqFrMcOUWudQbLc20FmQVbUFXVUUGHHMXPnIovPeNmA2o5yNAS1Fv9D-MkoYKvHh_iMfafnRHqoWwa2VJn83VqA5XEvDHg](https://lh3.googleusercontent.com/tuyFL_fs3yCirVHk9f-fDiQ7MBdE44scvPfaOSjLqovs3bamc_56v4wjiqFrMcOUWudQbLc20FmQVbUFXVUUGHHMXPnIovPeNmA2o5yNAS1Fv9D-MkoYKvHh_iMfafnRHqoWwa2VJn83VqA5XEvDHg)

Pada bagian review, kita tinggal mengeklik tombol **Launch**

![https://lh4.googleusercontent.com/n7ZTvjdx0UuOL1HKww8AHRqpR5kMamtsW6gwgpL4d6ef8nrQ5soD22D0gEu6FcizgwY79ZwYSjZoq-Qwxv5fmB5jOR_3TVRw6mJn1gCqt2TQilgAsVXDC9nE8JvwR1OBhW8Lb1xWVyF3jrVGDDRPfw](https://lh4.googleusercontent.com/n7ZTvjdx0UuOL1HKww8AHRqpR5kMamtsW6gwgpL4d6ef8nrQ5soD22D0gEu6FcizgwY79ZwYSjZoq-Qwxv5fmB5jOR_3TVRw6mJn1gCqt2TQilgAsVXDC9nE8JvwR1OBhW8Lb1xWVyF3jrVGDDRPfw)

Lalu, buat **key** **pair** baru untuk koneksi SSH. Isikan nama, lalu download. Kemudian klik **Launch**.

![https://lh6.googleusercontent.com/ATgew_lc3nfGHNDdUwHS9IeJVIPvbdVP76DE0hq-KJKQUY3LeRXhZUJqlsmTDCOsZGEIz-BzUFjSSXUXZ2VDNwTJvlYvQGXcDgTl9ZeypNgyUuKocIuZxHwO13KF5b7wza0-Hi-7VgwlrwySE9BEYw](https://lh6.googleusercontent.com/ATgew_lc3nfGHNDdUwHS9IeJVIPvbdVP76DE0hq-KJKQUY3LeRXhZUJqlsmTDCOsZGEIz-BzUFjSSXUXZ2VDNwTJvlYvQGXcDgTl9ZeypNgyUuKocIuZxHwO13KF5b7wza0-Hi-7VgwlrwySE9BEYw)

Tunggu sampai EC2 berjalan. Langkah selanjutnya adalah untuk menginstall nginx+php pada server EC2 yang telah di buat.

## ***Install nginx dan php***

Untuk menginstal nginx+php dengan menggunakan ansible kita harus menyiapkan struktur file dan folder sebagai berikut. Kita bisa menggunakan repository yang sudah dibuat.

```bash
git clone https://github.com/sdcilsy/nginx-php-setup-ansible.git
```

Namun, kita perlu untuk mengedit beberapa file. Kita akan membahasnya sebentar lagi.

![https://lh4.googleusercontent.com/FwtHIADoH0bZ-dW75YRgrCJri7B48it7eOtC3XxVB85hAX0uVyYf3sNBOWQ8qkslXukl-5FgJAjtTsqE0e-iPZPtjnPYGuF4h44EBtzcpe-BO0wtNg2-PnACApEjdpWihh-uIFnLtpfh-5Hqgh5prA](https://lh4.googleusercontent.com/FwtHIADoH0bZ-dW75YRgrCJri7B48it7eOtC3XxVB85hAX0uVyYf3sNBOWQ8qkslXukl-5FgJAjtTsqE0e-iPZPtjnPYGuF4h44EBtzcpe-BO0wtNg2-PnACApEjdpWihh-uIFnLtpfh-5Hqgh5prA)

Langkah selanjutnya, kita cek ip public dari instance EC2 yang telah kita buat sebelumnya, catat ip public tersebut untuk selanjutnya kita akan pergunakan pada ansible.

![https://lh5.googleusercontent.com/YrdH4TyJG_Z24xRx5qUyNrvRPl4LdYrMqmizJQboUy0tGW8GEbn9QSwiUy2JFiWzQvNRMz16swC9-lE11XydERXcOd3nEexLmJ2WHNXzBtttOcY2TruJwQl8Gndh1cu9VNnfZGCVzJOxbuht1FO5Vw](https://lh5.googleusercontent.com/YrdH4TyJG_Z24xRx5qUyNrvRPl4LdYrMqmizJQboUy0tGW8GEbn9QSwiUy2JFiWzQvNRMz16swC9-lE11XydERXcOd3nEexLmJ2WHNXzBtttOcY2TruJwQl8Gndh1cu9VNnfZGCVzJOxbuht1FO5Vw)

Folder yang perlu kita atur adalah **nginx** dan **php** yang berada di folder **roles**, selanjutnya kita akan menkonfigurasi file **main.yml** berada pada folder **nginx/task** seperti di bawah ini struktur folder dan filenya.

![https://lh4.googleusercontent.com/uPpcYXLvOcz0vr8gKWBwqWwhVwo3t38jY6KPXLZMUwelvrJcRCSUSDJ2Q5XggwrDFj2U4pQM1Hz_rp780IKr8MsXJly-Zvm08juWFwLRvFb8zTxqOgWR9xZvrW5bh4bz2qshmWUuQRUhdE3G8OZRvg](https://lh4.googleusercontent.com/uPpcYXLvOcz0vr8gKWBwqWwhVwo3t38jY6KPXLZMUwelvrJcRCSUSDJ2Q5XggwrDFj2U4pQM1Hz_rp780IKr8MsXJly-Zvm08juWFwLRvFb8zTxqOgWR9xZvrW5bh4bz2qshmWUuQRUhdE3G8OZRvg)

File **main.yml** tersebut kita edit beberapa perintah script seperti di bawah ini.

```bash
---
- name: Update Repository
  apt: update_cache=true
  become: yes

- name: Install Nginx
  apt: name=nginx state=present update_cache=true
  notify:
  - start nginx

- name: Copy nginx configuration
  template: src=default.conf dest=/etc/nginx/sites-enabled/default
  notify: 
  - restart nginx

- name: Copy web html
  template: src=index.html dest=/var/www/html/index.html
```

Selanjutnya kita akan mengecek file yang ada pada **templates**,  file **nginx.conf** yang akan kita kirim pada server isinya kurang lebih seperti di bawah ini.

```bash
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	root /var/www/html;
	# Add index.php to the list if you are using PHP
	index index.html index.php index.htm index.nginx-debian.html;
	server_name _;
	location / {
	# First attempt to serve request as file, then
	# as directory, then fall back to displaying a 404.
	try_files $uri $uri/ =404;
	}

	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
		fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;      
	}
}
```

Jika kita ingin mengirim file web (**index.html**), kita dapat meletakkan file tersebut pada **templates** dengan isi sebagai berikut.

```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YAY, ANSIBLE SUCCESSFULLY SETUP NGINX</title>
</head>
<body>
    <h1>Welcome to Sekolah Devops Cilsy</h1>
</body>
</html>
```

Kemudian pada folder **handlers** terdapat file **main.yml** yang isinya sebagai berikut.

```bash
---
- name: start nginx
  service: name=nginx state=started

- name: reload nginx
  service: name=nginx state=reloaded

- name: restart nginx
  service: name=nginx state=restarted
```

Setelah semua file pada folder **nginx** sudah kita buat, maka selanjutnya kita akan buat file yang ada di folder **php** dibawah folder **roles**. Setelah  folder **php** sudah kita buat,  kita akan membuat file **main.yml** pada folder **tasks** dengan isi sebagai berikut ini.

```bash
---
- name: Install PHP Package
  apt: name={{ php_ver }} state=present update_cache=true
  become: yes
```

Setelah selesai dengan file di atas, selanjutnya kita konfigurasi file **host** pada ansible. Adapun struktur file dan folder bisa kita lihat seperti berikut.

![https://lh3.googleusercontent.com/6zRBRnpxxyb-pUl_WwpG5RSJ08APMOMItSymdb86Dm74xX3ehixGeFXGfOLVd4PGCAHY8-myOsw569Tk5rzQHdEfFPW_lR_hOaKTD3_r_kp-CgilYerJr2zTExcm6ZgqZX3OpvtNNV6az_Wj1J5QLQ](https://lh3.googleusercontent.com/6zRBRnpxxyb-pUl_WwpG5RSJ08APMOMItSymdb86Dm74xX3ehixGeFXGfOLVd4PGCAHY8-myOsw569Tk5rzQHdEfFPW_lR_hOaKTD3_r_kp-CgilYerJr2zTExcm6ZgqZX3OpvtNNV6az_Wj1J5QLQ)

Isikan IP Public yang tadi sudah kita simpan dari EC2 instance, lalu isi keypair yang sebelumnya sudah didownload. Kita akan melakukan login menggunakan user **Ubuntu**. **Anda harus mengganti IP dan juga Key pair pada file host**

```bash
[client]
18.191.138.82 ansible_ssh_private_key_file=/home/taufik/ansible-do_13-1.pem

[all:vars]
ansible_user=ubuntu
```

Selanjutnya kita akan membuat file nginx.yml seperti di bawah ini. File **nginx.yml** sendiri berada di dalam folder devops_ansible atau folder ansible.

```bash
---
- name: Install Nginx+PHP with ansible
  hosts: client
  become: yes
  roles:
  - nginx
  - php
```

Setelah semua sudah di buat maka langkah selanjutnya adalah dengan menjalanlan ansible dengan menggunakan perintah berikut.

```bash
ansible-playbook -i hosts nginx.yml
```

Jika berhasil, maka akan muncul tampilan seperti gambar dibawah ini.

![https://lh5.googleusercontent.com/fSBFZ5oDDNNXeykgPwUuIZ4ODHh4AjaLoZFlbn-crJY_XNL-O3r9oL7600X3QlP7_bNAH2Q-2DtfuBSm4M4S3q6fr-UA4Q9CrZSu1oxco2bf8A6I6yU_oloKJsf74vqaHCXk0zCsRuiQSmt8fY1hHg](https://lh5.googleusercontent.com/fSBFZ5oDDNNXeykgPwUuIZ4ODHh4AjaLoZFlbn-crJY_XNL-O3r9oL7600X3QlP7_bNAH2Q-2DtfuBSm4M4S3q6fr-UA4Q9CrZSu1oxco2bf8A6I6yU_oloKJsf74vqaHCXk0zCsRuiQSmt8fY1hHg)

Setelah itu kita check aplikasi yang sudah kita setting tadi dengan mengakses **IP Public** ke browser denga port **8080** dan hasilnya akan muncul seperi gambar dibawah ini.

![https://lh5.googleusercontent.com/rAAMAVzbSuhsD0o87g3FTnRzjkwi4vY8lwNhHwOMIWj_h2w3t3ntLYHQYEAlE9LN4oHYKEnCXiJa87q67ktzl-LNFgWtq2yk5AzitcF-LzeAHtKw0Gv3fJUcOMAD26vwRZaMJ_IBt79_zlkkPHMSTA](https://lh5.googleusercontent.com/rAAMAVzbSuhsD0o87g3FTnRzjkwi4vY8lwNhHwOMIWj_h2w3t3ntLYHQYEAlE9LN4oHYKEnCXiJa87q67ktzl-LNFgWtq2yk5AzitcF-LzeAHtKw0Gv3fJUcOMAD26vwRZaMJ_IBt79_zlkkPHMSTA)

# **Install Web Server dengan Ansible pada Multiserver**

Pada bagian ini kita akan meginstall nginx dan php pada 2 server EC2, berbeda dengan yang sebelumnya yang hanya menggunakan 1 server EC2. Kita hanya perlu menambahkan hosts atau server yang ingin kita install, langkah konfigutasinya tidak jauh berbeda dengan yang sebelumnya.

Langkah pertama adalah megecek IP Public pada EC2 Instance yang sudah kita buat sebelumnya, seperti gambar dibawah ini.

![https://lh3.googleusercontent.com/gLYEe5BxOF8AsVxlE-69XemgRePw6N6VJFi1xeRq_-B2Db-X2kwU_TCI_hncsIHQvh_rpz97hQZE6xYdcx6QbQ-927kAfdfvrLl2kA3En55BDElG88dqFYxR46SNgwGCMpPHMY3zjZcjNzB3vEYyag](https://lh3.googleusercontent.com/gLYEe5BxOF8AsVxlE-69XemgRePw6N6VJFi1xeRq_-B2Db-X2kwU_TCI_hncsIHQvh_rpz97hQZE6xYdcx6QbQ-927kAfdfvrLl2kA3En55BDElG88dqFYxR46SNgwGCMpPHMY3zjZcjNzB3vEYyag)

![https://lh4.googleusercontent.com/kPKWwIp0IjoAwhXUdROS8LVqHPnJAHC2Kvq5m8H7r0RY03x9AZO8QSPn3OElzTUy5soQ3X_jesxL0QwSVdHwleoxuN3rpVzPXyZhKEg8a9FCJY5AWInKF_MvVE2oexMAb_k7OhA-G4NDzEqn4puH9g](https://lh4.googleusercontent.com/kPKWwIp0IjoAwhXUdROS8LVqHPnJAHC2Kvq5m8H7r0RY03x9AZO8QSPn3OElzTUy5soQ3X_jesxL0QwSVdHwleoxuN3rpVzPXyZhKEg8a9FCJY5AWInKF_MvVE2oexMAb_k7OhA-G4NDzEqn4puH9g)

Bisa kita lihat disana terdapat dua buah instance yang masing-masing memiliki IP Public yaitu **18.191.138.82** dan  **3.23.79.20**. Selanjutnya ip tersebut kita masukkan ke dalam file hosts , adapun struktur file atau folder bisa kita lihat sebagai berikut.

![https://lh3.googleusercontent.com/6zRBRnpxxyb-pUl_WwpG5RSJ08APMOMItSymdb86Dm74xX3ehixGeFXGfOLVd4PGCAHY8-myOsw569Tk5rzQHdEfFPW_lR_hOaKTD3_r_kp-CgilYerJr2zTExcm6ZgqZX3OpvtNNV6az_Wj1J5QLQ](https://lh3.googleusercontent.com/6zRBRnpxxyb-pUl_WwpG5RSJ08APMOMItSymdb86Dm74xX3ehixGeFXGfOLVd4PGCAHY8-myOsw569Tk5rzQHdEfFPW_lR_hOaKTD3_r_kp-CgilYerJr2zTExcm6ZgqZX3OpvtNNV6az_Wj1J5QLQ)

Ubah file host menjadi seperti dibawah ini.

```bash
[client]
18.191.138.82 ansible_ssh_private_key_file=/home/taufik/ansible-do_13-1.pem
3.23.79.20 ansible_ssh_private_key_file=/home/taufik/ansible-do_13-1.pem

[all:vars]
ansible_user=ubuntu
```

Jika sudah kita konfigurasi, selanjutnya kita simpan file host tersebut. Langkah selanjutnya adalah menjalankan kembali ansible dengan menggunakan perintah berikut.

```bash
ansible-playbook -i hosts nginx.yml
```

Jika berhasil maka akan muncul seperti gambar dibawah ini. Pada awal eksekusi, anda akan diminta untuk mengkonfirmasi koneksi menuju **instace ke-2**. Anda bisa mengetik **yes** untuk melanjutkan.

![https://lh6.googleusercontent.com/Pgt9_O7Bahk-U1AyunaDB5Vmz3PwAJXoUogq_QhkKq9Zif5z_lUwBRR6cG1t5CVcDzbortqQXXsS5eO4NzdWeU4ELnw0Yv9AAUHZAar1rmqEuRRG2znvotBeE7DEtbk9Wy0lnyPY4Dojlw3eb8aFJQ](https://lh6.googleusercontent.com/Pgt9_O7Bahk-U1AyunaDB5Vmz3PwAJXoUogq_QhkKq9Zif5z_lUwBRR6cG1t5CVcDzbortqQXXsS5eO4NzdWeU4ELnw0Yv9AAUHZAar1rmqEuRRG2znvotBeE7DEtbk9Wy0lnyPY4Dojlw3eb8aFJQ)

Ada beberapa perbedaan yakni ada yang statusnya **OK** dan **Changed**. Mengapa instance pertama **OK** semua, sedangkan instance kedua ada yang **Changed** ?

Ini terjadi karena pada **instance pertama**, kita sudah mengkonfigurasi sebelumnya, sedangkan pada **instance kedua**, kita baru mengkonfigurasi pertama kali.

Kita hanya perlu mengecek hasil yang sudah kita buat tadi dengan mengakses IP Public dengan menggunakan browser seperti dibawah ini.

Instance pertama.

![https://lh5.googleusercontent.com/rAAMAVzbSuhsD0o87g3FTnRzjkwi4vY8lwNhHwOMIWj_h2w3t3ntLYHQYEAlE9LN4oHYKEnCXiJa87q67ktzl-LNFgWtq2yk5AzitcF-LzeAHtKw0Gv3fJUcOMAD26vwRZaMJ_IBt79_zlkkPHMSTA](https://lh5.googleusercontent.com/rAAMAVzbSuhsD0o87g3FTnRzjkwi4vY8lwNhHwOMIWj_h2w3t3ntLYHQYEAlE9LN4oHYKEnCXiJa87q67ktzl-LNFgWtq2yk5AzitcF-LzeAHtKw0Gv3fJUcOMAD26vwRZaMJ_IBt79_zlkkPHMSTA)

Instance kedua

![https://lh3.googleusercontent.com/EvECVoN7DJ2tYU2PsQ_DMqfJcbP6S98O8kUvcBEkdJYdL4EM98_m94GPfAdDNSYFWYZLpisCZtzpNE4U_YIZ-A3IYyI2TcxJPKAjMljPpSP6l_2Xpkn4CkPUnaDG0S2HTncGIC1-JWPpZxX3WyoyhQ](https://lh3.googleusercontent.com/EvECVoN7DJ2tYU2PsQ_DMqfJcbP6S98O8kUvcBEkdJYdL4EM98_m94GPfAdDNSYFWYZLpisCZtzpNE4U_YIZ-A3IYyI2TcxJPKAjMljPpSP6l_2Xpkn4CkPUnaDG0S2HTncGIC1-JWPpZxX3WyoyhQ)

Untuk mencoba instalasi paket-paket linux yang baru, kita dapat menggunakan ansible-playbook. Kita dapat mengambilnya dengan menclone repository seperti berikut.

```bash
git clone https://github.com/adisaputra10/ansible-examples.git
```

Berikut merupakan file atau data mengenai ansible-example yang dapat kita lihat seperi dibawah ini.

![https://lh4.googleusercontent.com/XL91YGodLxH08o1cwOhW7_j_HH0RVFHrQ4mnyUP98AISKeFpvbhg1phtMycJ33C9Ptq9IPExFZU_EoTS3sEt5jGR8fbr-LOnqZcbTxtBJFy7qGhI0WhfdzY8Gn2wNAtlC1CQrQw6usrGFWsOumblHw](https://lh4.googleusercontent.com/XL91YGodLxH08o1cwOhW7_j_HH0RVFHrQ4mnyUP98AISKeFpvbhg1phtMycJ33C9Ptq9IPExFZU_EoTS3sEt5jGR8fbr-LOnqZcbTxtBJFy7qGhI0WhfdzY8Gn2wNAtlC1CQrQw6usrGFWsOumblHw)

Untuk dapat menjalankan beberapa konfigurasi tersebut, kita hanya perlu masuk ke folder, lalu setup host sesuai ip tujuan. Kemudian di jalankan.

Misalkan kita akan coba menjalankan konfigurasu lampe simpe, pertama kita pindah kedalam folder berikut.

```bash
cd  lampe_simple
```

Kemudian seting host atau alamat ip yang akan kita gunakan pada saat saling tukan-menukar informasi. Script dapat kita lihat sebagai berikut.

```bash
[web]
127.0.0.1

[client]
52.221.216.43 ansible_ssh_private_key_file=/vagrant/awskeyprivate.pem
```

Setelah itu jalankan dengan ansible dengan perintah.

```bash
ansible-playbook -i hosts site.yml
```

Untuk file konfigurasi yang lain tidak jauh berbeda cara mengaksesnya dengan yang barusan. Kita hanya perlu melakuakn beberapa step seperti berikut.

```bash
cd <nama_direktori>
#cek file host ,lalu jalankan perintah seperti di bawah ini
ansible-playbook -i hosts site.yml
```

Untuk mendapatkan contoh lebih banyak mengenai ansible, kita dapat mengakses alamat berikut [https://docs.ansible.com/ansible/2.5/user_guide/playbooks.html](https://docs.ansible.com/ansible/2.5/user_guide/playbooks.html)

# **Exercise**

Soal Kasus : Bayangkan kalian sedang bekerja di perusahaan Sangkuriang Corp, disana kalian memiliki 5 instance yang masih kosong dan harus di installakn nginx dan php untuk kebutuhan web server. Maka dari itu

1. Konfigurasi kelima server tersebut menggunakan layanan Ansible.