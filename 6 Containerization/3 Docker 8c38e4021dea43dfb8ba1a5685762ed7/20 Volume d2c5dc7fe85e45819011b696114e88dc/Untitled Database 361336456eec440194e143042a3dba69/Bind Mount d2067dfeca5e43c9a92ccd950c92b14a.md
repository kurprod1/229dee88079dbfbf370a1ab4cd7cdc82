# Bind Mount

Kekurangan: • Sangat tergantung dengan letak persis file/folder dari Host. Misal folder /home/data di host A pasti tidak sama dengan host B. Maka data tentunya perlu disinkronkan dulu antara host A dan Host B yang tentunya cukup repot dan bisa terjadi banyak error. Tidak cocok untuk kebutuhan scale dan Fail over.
	
Kelebihan: • Relatif lebih cepat, karena langsung dari filesystem host.	
• Relatif lebih sederhana secara penggunaan. Tinggal mount suatu file/folder, selesai.
• Lebih cocok untuk local development.
• Lebih cocok untuk mounting file-file kecil atau file-file konfigurasi.Misalnya mounting /etc/nginx/nginx.conf saja atau /etc/php/php.ini saja.