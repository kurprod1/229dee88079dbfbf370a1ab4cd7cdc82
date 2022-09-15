# 2. Installasi dan Setup Ansible

Created: July 25, 2022 6:12 PM

# **Instalasi Ansible**

Pada tahap ini kita akan menginstallkan ansible, ansible sendiri membutuhkan python untuk memaksimalkan kinerjanya. Maka dari itu pertama kita harus mengupdate repository linux kita, lalu installkan python dan juga ansible seperti dibawah ini.

```bash
apt-get update
apt-get install python ansible
```

# **SSH Setup**

Ansible menggunakan koneksi SSH untuk berkomunikasi dengan target host, dan SFTP untuk transfer modul. Maka dari itu, kita harus mensetup terlebih dahulu SSH antara **Control Node** (yang menjalankan **Ansible**) dan **Managed Node** (target Ansible). Tujuan dari setup ini, agar kita tidak lagi memasukan username password apabila melakukan koneksi SSH.

Pastikan **Control Node** dan **Managed Node** sudah terinstall SSH. Pada **Control Node**, kita buat **RSA Key Pair** dengan mengeksekusi perintah berikut.

```bash
ssh-keygen
```

Lalu akan muncul prompt untuk menyimpan **RSA** nya dan password dari **RSA**. Untuk saat ini, kita biarkan default saja, jadi kita tinggal tekan tombol Enter saja.

```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/home/taufik/.ssh/id_rsa): 
Created directory '/home/taufik/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/taufik/.ssh/id_rsa
Your public key has been saved in /home/taufik/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:uPYfD6fYR7VOxe1XslmVW3N8r1kXDbEaNVaeTlZmyv0 taufik@hewlettpackard
```

Kurang lebih, setup nya akan seperti ini :

[https://lh4.googleusercontent.com/VLe-I9xI3GdfVNKauqigW-VQjKTIREYsd5iAvOlEKFWOkRiktmqDFGVTXea9j182XpZuaR_a5Ae2K2xJibtu6p4YrGC4AscuqttdTvr1_v4GCongK7JCRbZ-KkwzXdZnjpKNWGtH48O2PQ5C-ifpEw](https://lh4.googleusercontent.com/VLe-I9xI3GdfVNKauqigW-VQjKTIREYsd5iAvOlEKFWOkRiktmqDFGVTXea9j182XpZuaR_a5Ae2K2xJibtu6p4YrGC4AscuqttdTvr1_v4GCongK7JCRbZ-KkwzXdZnjpKNWGtH48O2PQ5C-ifpEw)

Langkah selanjutnya adalah untuk menyalin **Public key** ke **Managed Node**. Kita bisa melakukannya dengan mengeksekusi perintah berikut.

```bash
ssh-copy-id username@remote_host
```

Isi **username** dan **remote_host** sesuai dengan yang akan dijadikan **Managed Node**. Setelah itu, isikan **password** dari **username** tersebut. Kurang lebih setupnya menjadi seperti ini. **Anda harus mengganti username dan/atau IP target sesuai dengan target anda masing masing.**

[https://lh6.googleusercontent.com/gcpR3LC0h8ddhWgpfCWQsNn_an8HV6jcLjvP6DqvRCkEJeuI6_kXl5Gl9U9_d8lQ-AhxEJ8w1SwitQ00DnIk9sg4CUQ2ob6NIklz7x6SBEdnMEvSzOvhK0yNNiQiFu9bJh0NTnGjg6RyMZzJHEfsGA](https://lh6.googleusercontent.com/gcpR3LC0h8ddhWgpfCWQsNn_an8HV6jcLjvP6DqvRCkEJeuI6_kXl5Gl9U9_d8lQ-AhxEJ8w1SwitQ00DnIk9sg4CUQ2ob6NIklz7x6SBEdnMEvSzOvhK0yNNiQiFu9bJh0NTnGjg6RyMZzJHEfsGA)

# **Playbook Structure**

Setelah kita menginstall ansible, langkah selanjutnya adalah memahami struktur file dan folder ansible. File ansible dapat kita clone dengan menggunakan perintah di bawah ini.

```bash
git clone https://github.com/sdcilsy/nginx-setup-ansible.git
```

Setelah kita clone file ansible tersebut, kita bisa lihat isi file seperti berikut ini.

[https://lh4.googleusercontent.com/-7BH6lPDNVPksOwO0IaYUiKw5BYjMf6tZHYRsNLLLw96Ap_xqrzqPr7A12oiqsyA7Ug2mkYPn-nX5eArkSWUOz9UgvwR49SBDzoJqWk8mDvRNjrnrPLIP_2pwpC5j_cDKlk-DLuDF10q6FLPF8ZQJw](https://lh4.googleusercontent.com/-7BH6lPDNVPksOwO0IaYUiKw5BYjMf6tZHYRsNLLLw96Ap_xqrzqPr7A12oiqsyA7Ug2mkYPn-nX5eArkSWUOz9UgvwR49SBDzoJqWk8mDvRNjrnrPLIP_2pwpC5j_cDKlk-DLuDF10q6FLPF8ZQJw)

Pada ansible terdapat 2 folder yang bernama **group_vars** dan juga **roles** serta 1 file bernama **hosts**. Folder **group_var** berguna untuk mendefinisikan variable-varible untuk ansible, folder **roles** berguna untuk membuat fungsi-fungsi yang ada di ansible. Sedangkan file **hosts** berguna untuk mendeklarasikan ip server yang ingin kita provisioning atau install dengan ansible.

Pada bagian selanjutnya terdapat sebuah file dengan nama **all** pada folder **group_vars**. Nantinya file all akan berisi variable yang akan di gunakan pada ansible.

Kita akan mencoba install nginx dengan menggunakan ansible pada folder roles. Selanjutnya buat folder **nginx** dialam folder **roles**, di dalam folder nginx akan di buat folder **tasks**, **templates** dan **handlers**. Folder **tasks** berisikan file perintah yang di gunakan pada ansible, file yang berada pada folder **tasks** adalah **main.yml**, folder **templates** berisikan file yang akan di kirim ke server misal **nginx.conf**. Sedangkan folder **handlers** berguna untuk **restart** atau **start** service **nginx**.

[https://lh4.googleusercontent.com/-7BH6lPDNVPksOwO0IaYUiKw5BYjMf6tZHYRsNLLLw96Ap_xqrzqPr7A12oiqsyA7Ug2mkYPn-nX5eArkSWUOz9UgvwR49SBDzoJqWk8mDvRNjrnrPLIP_2pwpC5j_cDKlk-DLuDF10q6FLPF8ZQJw](https://lh4.googleusercontent.com/-7BH6lPDNVPksOwO0IaYUiKw5BYjMf6tZHYRsNLLLw96Ap_xqrzqPr7A12oiqsyA7Ug2mkYPn-nX5eArkSWUOz9UgvwR49SBDzoJqWk8mDvRNjrnrPLIP_2pwpC5j_cDKlk-DLuDF10q6FLPF8ZQJw)

Kita akan coba jelaskan isi file dari **main.yml** dari folder **task** sebagai berikut ini.

```bash
---
- name: Update repository
  apt: update_cache=true
  become: yes
```

Perintah di atas merupakan perintah untuk mengupdate repository dari remote server. Disini kita menggunakan privilege root yaitu dengan menambahkan **become: yes**.

```bash
- name: Install Nginx
  apt: name={{ variable }} state=present update_cache=true
```

Selanjutnya perintah di atas berguna untuk menginstall nginx. Kita menggunakan variable yang di ambil dari folder group_vars dan file all, sehingga kita dapat mengkonfigurasi ansible secara dynamic. Kelebihan kita menggunakan variable secara dynamic adalah saat ada perubahan value, kita cukup mengubah pada file all yang berada di group_vars.

Pada instruksi dibawah, akan dibuatkan directory /var/www/html dengan permission 775.

```bash
- name: Create web directory
  file: path=/var/www/html mode=775 state=directory

- name: Copy nginx configuration
  template: src=nginx.conf dest=/etc/nginx/conf.d/default.conf

- name: Copy index.html 
  template: src=index.html dest=/var/www/html/index.html
```

Selanjutnya perintah di atas berguna untuk mencopy atau transfer file ke server, file yang kita transfer kita masukkan pada folder templates seperti gambar di bawah ini.

[https://lh4.googleusercontent.com/25r9KeDoD05eBeQ5AGsAr3qscAObs8OPAs2SCAO8T4-6CGZfys1_zS-5ppst3TEQyBeAkdcZjURhOk5dYSj1WUuITZw--qO28FbacjAqslNHdNirq0-hW8TnNXkJOcNWqpesC1KxW6quu68Up1kLwQ](https://lh4.googleusercontent.com/25r9KeDoD05eBeQ5AGsAr3qscAObs8OPAs2SCAO8T4-6CGZfys1_zS-5ppst3TEQyBeAkdcZjURhOk5dYSj1WUuITZw--qO28FbacjAqslNHdNirq0-hW8TnNXkJOcNWqpesC1KxW6quu68Up1kLwQ)

Selanjutnya adalah folder **handlers** yang berguna untuk malakukan start maupun restart service nginx. Pada folder handlers berisikan file **main.yml**, adapun struktur file direktori dapat kita lihat seperti di bawah ini.

[https://lh6.googleusercontent.com/TFau21rqcJe_uBStaumD0AigexgcwcR2uXLQUv4bPTZoAjYXhLtCNynu_ZLYQoylchhizQ-kEXjBA0-JfmplMaquwNfoj1K6oQEKB6KFbvFyrviMgliaCBqz1KJjxXTauSnqNjITwmxFL75WLctzBA](https://lh6.googleusercontent.com/TFau21rqcJe_uBStaumD0AigexgcwcR2uXLQUv4bPTZoAjYXhLtCNynu_ZLYQoylchhizQ-kEXjBA0-JfmplMaquwNfoj1K6oQEKB6KFbvFyrviMgliaCBqz1KJjxXTauSnqNjITwmxFL75WLctzBA)

File **main.yml** yang berada pada folder handler berisikan beberapa script perintah. Kita dapat melihat isinya seperti dibawah ini.

```bash
---
- name: start nginx
  service: name=nginx state=started

- name: reload nginx
  service: name=nginx state=reloaded

- name: restart nginx
  service: name=nginx state=restarted
```

File yang terakhir yang harus kita pahami adalah file **hosts**, file ini berguna untuk mengatur server yang akan kita provisioning atau  install melalui ansible. Berikut merupakan isi dari file host tersebut. **Anda harus mengganti ip pada Group Client dibawah, sesuai dengan target anda masing masing**.

```bash
[local]
127.0.0.1 ansible_ssh_private_key_file=/vagrant/awskeyprivate.pem
[client]
172.17.0.3
```

Perintah di atas merupakan contoh dari file hosts, file host berisikan ip server yang ingin kita provisioning atau install melalui ansible. Karena kita sudah setup SSH, kita tidak perlu lagi memasukan username serta password.

Setelah folder dan file dari ansible sudah kita siapkan, selanjutnya untuk menjalankan ansible kita memerlukan file yml. Misalkan kita akan menggunakan nama **nginx.yml**, struktur file dapat kita lihat seperti gambar dibawah ini.

[https://lh5.googleusercontent.com/fMgtKhYygPJiL3sdX-3UXOZsgX-Cx70GFN71boTbiwjfu56inFigDzGZ_rfXe-5ewINBu5Blt2XUdGsA_nMKUotwu5z6v6QaaNwY-k4huTi2qaG8maNvTsAGo6HP_L_yMe1eCUekmz3xmwcFULmLKg](https://lh5.googleusercontent.com/fMgtKhYygPJiL3sdX-3UXOZsgX-Cx70GFN71boTbiwjfu56inFigDzGZ_rfXe-5ewINBu5Blt2XUdGsA_nMKUotwu5z6v6QaaNwY-k4huTi2qaG8maNvTsAGo6HP_L_yMe1eCUekmz3xmwcFULmLKg)

Disini kita akan coba jelaskan beberapa fungsi dari komponen script yang ada pada file nginx.yml sebagai berikut.

- **name** berguna untuk menampilkan nama proses saat di jalankan
- **hosts : client** merupakan server yang akan di install menggunakan ansible file harus sesuai dengan file hosts
- **become : yes** merupakan perintah untuk menjalankan perintah sudo pada server yang akan kita install dengan ansible
- **roles :** - **nginx** merupakan kumpulan perintah yang berada di folder roles, sedangkan nginx adalah folder yang berada di roles

Setelah semua konfigurasi atau settingan telah di lakukan, sekarang kita dapat menjalankan ansible dengan menggunakan perintah seperti di bawah ini pada folder devops ansible.

```bash
ansible-playbook -i hosts nginx.yml
```

Maka hasilnya bisa kita lihat jika berhasil maka akan muncul seperti di bawah ini.

![Untitled](2%20Installasi%20dan%20Setup%20Ansible%209759faefd56049dcbc203b18199b7802/Untitled.png)