# 4. Instalasi dan Konfigurasi Git

Created: July 14, 2022 1:11 PM

# **Instalasi Git di Linux**

Cara paling mudah untuk menginstall git pada Linux adalah menggunakan command line. Seperti biasa, dengan APT kita bisa menginstal git dengan nama paket git.

```bash
sudo apt install git
sudo apt-get install git
```

Untuk keluarga Fedora dapat menggunakan perintah yum seperti berikut.

```bash
sudo yum install git
```

Untuk mengecek versi Git kita bisa gunakan perintah dibawah ini.

```bash
git --version
```

# **Instal Git di Windows**

Untuk instalasi git pada Windows, tidaklah sulit karena tinggal klik klik saja sesuai instruksi. Ada file yang perlu di download terlebih dahulu yaitu di [git-scm.com](https://git-scm.com/)

- Untuk Mendownload Git cukup kita buka website resminya Git ([git-scm.com](https://git-scm.com/)). Kemudian unduh Git sesuai dengan arsitektur komputer kita. Kalau menggunakan 64bit, unduh yang 64bit. Begitu juga kalau menggunakan 32bit.
- klik 2x file installer Git yang sudah didownload.

[https://lh4.googleusercontent.com/iQbK3KWfXw9FEAXDjWpkx7r0wGESMR4seteqZ1JiIcw6toD-MqxLAZY9Z9gw84IZ6mBG5dhPwSi1zEVwZEOuqruaL7X3-lJQNl6mAHghPOybcMIpA9jY8W_aLs6ADT4BPjySNjYd_bj_GjIYHg](https://lh4.googleusercontent.com/iQbK3KWfXw9FEAXDjWpkx7r0wGESMR4seteqZ1JiIcw6toD-MqxLAZY9Z9gw84IZ6mBG5dhPwSi1zEVwZEOuqruaL7X3-lJQNl6mAHghPOybcMIpA9jY8W_aLs6ADT4BPjySNjYd_bj_GjIYHg)

- Setelah itu akan muncul informasi lisensi Git, klik Next > untuk melanjutkan.

[https://lh5.googleusercontent.com/X59pHtQzFecpTH3x_dKAUUGMjalBtzoYgHndvQ1bIl51cVaWMvEfcowUPwEMtA1YdUf0VzMAg1f83A4aDlLG6OpKjqdbB9P06GlHmbrni_YF5A4L-gA5dnNjCzYjMYyLB5KGKrA3kEtFMCpsFQ](https://lh5.googleusercontent.com/X59pHtQzFecpTH3x_dKAUUGMjalBtzoYgHndvQ1bIl51cVaWMvEfcowUPwEMtA1YdUf0VzMAg1f83A4aDlLG6OpKjqdbB9P06GlHmbrni_YF5A4L-gA5dnNjCzYjMYyLB5KGKrA3kEtFMCpsFQ)

- Selanjutnya menentukan lokasi instalasi. Biarkan saja apa adanya, kemudian klik Next

[https://lh5.googleusercontent.com/-XwR94SpvCaJQSbaK42PHqhjf1eVNvNCp8hWvkpaRybrDz_ygds80tTpy7j3WLtOx7pxabKAFXEU4n1KFMXqVqcDLxZRFo3fuGVJEWd7AwAzFkdl76_sSVFGZ5mdzJqU1vywJvHbw-tS1I1TrQ](https://lh5.googleusercontent.com/-XwR94SpvCaJQSbaK42PHqhjf1eVNvNCp8hWvkpaRybrDz_ygds80tTpy7j3WLtOx7pxabKAFXEU4n1KFMXqVqcDLxZRFo3fuGVJEWd7AwAzFkdl76_sSVFGZ5mdzJqU1vywJvHbw-tS1I1TrQ)

- Selanjutnya pemilihan komoponen, biarkan saja seperti ini kemudian klik Next.

[https://lh4.googleusercontent.com/-RPWFWM5Aplt2q_i7n2gPGmbIODdWbXuek-_yaR_B5pxVRcZVRrgBVgIpXKz7G1hsbJPhWOhHTxwtLoXoKDDWGMIWFQASEZy3QSFCy8cSOPbp8om-41tCPX6b5VwAXZl8--spko3HaF0-ec_Mw](https://lh4.googleusercontent.com/-RPWFWM5Aplt2q_i7n2gPGmbIODdWbXuek-_yaR_B5pxVRcZVRrgBVgIpXKz7G1hsbJPhWOhHTxwtLoXoKDDWGMIWFQASEZy3QSFCy8cSOPbp8om-41tCPX6b5VwAXZl8--spko3HaF0-ec_Mw)

- Selanjutnya pemlilihan direktori start menu, klik Next

[https://lh3.googleusercontent.com/y3uTSH5yq160GWEp5RVhgZ838UYYXK1rZTocGmRsBqYwQvXECV_gqAuSijXWPIFaATys1CRDFVpLQilI9oYuCYyc5Y9zp_4DGvdVVkhadXegzuRq1fquERhuZFTej2GHircUqgTwPZc0E5vrAA](https://lh3.googleusercontent.com/y3uTSH5yq160GWEp5RVhgZ838UYYXK1rZTocGmRsBqYwQvXECV_gqAuSijXWPIFaATys1CRDFVpLQilI9oYuCYyc5Y9zp_4DGvdVVkhadXegzuRq1fquERhuZFTej2GHircUqgTwPZc0E5vrAA)

- Selanjutnya pengaturan PATH Environment. Pilih yang tengah agar perintah git dapat di kenali di Command Prompt (CMD). Setelah itu klik Next

[https://lh4.googleusercontent.com/tsl6ln7IXavYcH30dKfAjCvw3bpKSQLI40LW-Ly86nK9dWnu0K21XzsYqBlmaB6d5rfj4_TJ6XpD7v_FSbAVuCp9gaaSZwaune6DFjp9Xipu2Xt_nLGLSGobOIuj8-uzXuE71so76Umpcii1hA](https://lh4.googleusercontent.com/tsl6ln7IXavYcH30dKfAjCvw3bpKSQLI40LW-Ly86nK9dWnu0K21XzsYqBlmaB6d5rfj4_TJ6XpD7v_FSbAVuCp9gaaSZwaune6DFjp9Xipu2Xt_nLGLSGobOIuj8-uzXuE71so76Umpcii1hA)

- Selanjutnya konversi line ending. Biarkan saja seperti ini, kemudian klik Next >

[https://lh3.googleusercontent.com/74WcXK-sJpL_O-ycRK5a6uDuUsWk7m3KXXDFXjQTiRC07hb7EyNx-gegwqCQKKJD__VeivdHSg3zIYjRdkKTxTdHUD02nP9T3NXXig6b1DgKEdXZd0cmytvzBd6ruVrbu6Ak6qI35ZboUmMyyQ](https://lh3.googleusercontent.com/74WcXK-sJpL_O-ycRK5a6uDuUsWk7m3KXXDFXjQTiRC07hb7EyNx-gegwqCQKKJD__VeivdHSg3zIYjRdkKTxTdHUD02nP9T3NXXig6b1DgKEdXZd0cmytvzBd6ruVrbu6Ak6qI35ZboUmMyyQ)

- Pada pemilihan emulator terminal. Pilih saja windows console, kemudian klik Next.

[https://lh5.googleusercontent.com/nokri5nUvVwsww8XRFEsITL8c6CJRFuLsbh575mewirF_0Qsa53Ec3Ov0DM1Et9HonCrDm_mtKYx6UHyYd6TPfDvAglwopBblj7i3zHUJ9KVXou2lwff50qHiynzSTFykFc02BlnQCshNGnxyA](https://lh5.googleusercontent.com/nokri5nUvVwsww8XRFEsITL8c6CJRFuLsbh575mewirF_0Qsa53Ec3Ov0DM1Et9HonCrDm_mtKYx6UHyYd6TPfDvAglwopBblj7i3zHUJ9KVXou2lwff50qHiynzSTFykFc02BlnQCshNGnxyA)

- Selanjutnya pemilihan opsi ekstra. Klik saja Next.

[https://lh3.googleusercontent.com/5wI3Z3HpGWHmC0brLeyWkUpobfva_YEjB-VhAgE58QO39jMigt7Ap9lzDygvMwru0HZti10Qg2lCcuf8eEzcmwkjSxDbJ215zAUi15fmVDxHlSyoMJxTtCl4odhHx8bhuzw0gCndhphQG9G9KA](https://lh3.googleusercontent.com/5wI3Z3HpGWHmC0brLeyWkUpobfva_YEjB-VhAgE58QO39jMigt7Ap9lzDygvMwru0HZti10Qg2lCcuf8eEzcmwkjSxDbJ215zAUi15fmVDxHlSyoMJxTtCl4odhHx8bhuzw0gCndhphQG9G9KA)

- Selanjutnya pemilihan opsi eksperimental, langsung saja klik Install untuk memaulai instalasi.

[https://lh3.googleusercontent.com/E-gS0XVsaRNHzD7oWD3RF9Xqti3wPHFGtmQ8fVO8CkkYZrwIDcMSll3PQPhpxebieSSpKrr4VNMOlqjYaKDiZfjfigX-NeFU3jSKHIvXPGu7CyUNDYpy5M6cQoVjWHgZynYKP9YBrwcyHLQKHA](https://lh3.googleusercontent.com/E-gS0XVsaRNHzD7oWD3RF9Xqti3wPHFGtmQ8fVO8CkkYZrwIDcMSll3PQPhpxebieSSpKrr4VNMOlqjYaKDiZfjfigX-NeFU3jSKHIvXPGu7CyUNDYpy5M6cQoVjWHgZynYKP9YBrwcyHLQKHA)

- Tunggu beberapa saat, instalasi sedang dilakukan.

[https://lh4.googleusercontent.com/bmEMyIEZJtKIerfWUWEVzls31t4y-QnAcXyyPYpI6voAIlXsbrqTRWsDF7nVlijpnz8ZdMRFwtEPyrf2dlOgXnfbImrxaKoNCdmui2T4naa8W-Cx-UrjCfZ0ZolwQDX0mjn5A_QKJcw-TYGJvg](https://lh4.googleusercontent.com/bmEMyIEZJtKIerfWUWEVzls31t4y-QnAcXyyPYpI6voAIlXsbrqTRWsDF7nVlijpnz8ZdMRFwtEPyrf2dlOgXnfbImrxaKoNCdmui2T4naa8W-Cx-UrjCfZ0ZolwQDX0mjn5A_QKJcw-TYGJvg)

- Setelah selesai, kita bisa langsung klik Finish.

[https://lh5.googleusercontent.com/gGl3ShADt89eIJe5Ve8wRprjsLDvVzDlmYRqhakcnyKjdY6C1dLGoiEDKs1Vv3N8iTgB190jA6F1kyijQHhVvYTp-e8kJjlfNrU5LwHMQi2LkJ5H1mJDhjMaC1cRfDSeJPuAaUW06Dg-5b_qjw](https://lh5.googleusercontent.com/gGl3ShADt89eIJe5Ve8wRprjsLDvVzDlmYRqhakcnyKjdY6C1dLGoiEDKs1Vv3N8iTgB190jA6F1kyijQHhVvYTp-e8kJjlfNrU5LwHMQi2LkJ5H1mJDhjMaC1cRfDSeJPuAaUW06Dg-5b_qjw)

Git sudah terinstal di Windows. Untuk mencobanya, silahkan buka CMD atau PowerShell, kemudian ketik perintah git --version.

# **Konfigurasi Git**

Ada beberapa konfigurasi yang harus dipersiapkan sebelum mulai menggunakan Git, seperti name dan email. Silahkan lakukan konfigurasi dengan perintah berikut ini.

```bash
git config --global user.name "Irfan Herfiandana"
git config --global user.email irfanherfiandana@gmail.com
```

Kemudian periksa konfigurasinya dengan menggunakan perintah berikut.

```bash
git config --list
```

Apabila berhasil tampil seperti gambar berikut ini, berarti konfigurasi berhasil.

[*Konfigurasi Git*](https://lh3.googleusercontent.com/W3MPZ7kqGJQwRP-TTNq_7ep8kTiYneRLohCmsLqSlGV3AWvGATAEEn4Da0NMSNoFPe6LFgOrVAu48NxO7HRJSpx7oG6TuqkqmBHrp-Z43KgZiFES6bnYTVbpRC7ucx08iNgcxIxNvsWRajtBCQ)

*Konfigurasi Git*