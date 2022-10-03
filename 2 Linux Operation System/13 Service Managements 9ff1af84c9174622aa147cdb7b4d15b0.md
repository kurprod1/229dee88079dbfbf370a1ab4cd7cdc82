# 13. Service Managements

Created: June 27, 2022 2:34 PM

# **Belajar Manajemen Layanan**

## **Apa itu Manajemen Layanan?**

Di Server Linux kita selalu berurusan dengan yang namanya layanan. Disini kita mempelajari bagaimana dasar-dasar cara untuk me-restart layanan, menghentikan layanan, melihat status layanan tersebut aktif atau tidak, hingga cara menjalankan suatu layanan.

## **Mengecek Status Layanan**

Ini adalah perintah untuk mengetahui apakah layanan yang ingin kita cek sedang berjalan atau berhenti.

**Ubuntu**

```bash
service namalayanan status
systemctl status namalayanan
```

**Centos**

```bash
service namalayanan status
systemctl status namalayanan
```

Misalnya :

```bash
service ssh status

ssh.service - OpenBSD Secure Shell server
Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
Active: active (running) since Sat 2018-08-11 18:32:20 WIB; 5h 18min ago
Process: 1839 ExecReload=/bin/kill -HUP $MAINPID (code=exited, status=0/SUCCESS)
Main PID: 1192 (sshd)
CGroup: /system.slice/ssh.service
└─1192 /usr/sbin/sshd -D
```

Disana tertulis bahwa service SSH sedang active (running). Artinya service ssh pada server Linux tersebut sedang berjalan.

## **Merestart Layanan**

Perintah untuk memati-hidupkan layanan yang kita inginkan. Biasa digunakan sehabis kita melakukan suatu konfigurasi (biasanya konfigurasi baru berjalan setelah layanan direstart), atau ketika mengalami problem.

**Ubuntu**

```bash
service namalayanan restart
systemctl restart namalayanan
```

**Centos**

```bash
service namalayanan restart
systemctl restart namalayanan
```

## **Menghentikan Layanan**

Perintah untuk mematikan layanan yang kita inginkan. Biasa digunakan jika ingin mematikan layanan yang sudah tidak dibutuhkan lagi, atau ketika ada salah satu prosedur yang mengharuskan mematikan layanan terkait.

**Ubuntu**

```bash
service namalayanan stop
systemctl stop namalayanan
```

**Centos**

```bash
service namalayanan stop
systemctl stop namalayanan
```

## **Menjalankan Layanan**

Perintah untuk menghidupkan layanan yang kita inginkan. Layanan yang sudah diinstall di Linux Server tidak akan bisa dinikmati jika belum di jalankan.

**Ubuntu**

```bash
service namalayanan start
systemctl start namalayanan
```

**Centos**

```bash
service namalayanan start
systemctl start namalayanan
```

## **Mengecek & Membuat layanan aktif/tidak saat booting**

Setiap layanan yang sudah diinstall di server Linux, bisa diatur apakah layanan tersebut auto start atau tidak setiap server booting.

Sebelum mengaktifkan atau menonaktifkan autostart, perintah untuk mengecek status autostartnya adalah ini :

**Ubuntu**

```bash
systemctl is-enabled namalayanan
```

**Centos**

```bash
systemctl is-enabled namalayanan
```

Jika hasilnya enabled, maka layanan tersebut sudah auto start.

Lalu untuk mengaktifkannya adalah :

**Ubuntu**

```bash
systemctl enable namalayanan
```

**Centos**

```bash
systemctl enable namalayanan
```

Dan untuk menonaktifkannya :

**Ubuntu**

```bash
systemctl disable namalayanan
```

**Centos**

```bash
systemctl disable namalayanan
```

# **Exercise**

**Teori**

1. Kenapa kita perlu mempelajari Manajemen Layanan?

**Praktek**

Waktu pengerjaan : 5 menit

Masing-masing peserta praktekkan soal berikut ini di kolom terminal Linux masing-masing sambil melakukan sharing screen agar instruktur dapat melihat hasilnya.

1. Pertama-tama lakukan instalasi layanan webserver apache.
2. Jika sudah, buatlah layanan tersebut agar auto-start setiap booting.
3. Restart layanan webserver tersebut dan pastikan bahwa statusnya sudah running.