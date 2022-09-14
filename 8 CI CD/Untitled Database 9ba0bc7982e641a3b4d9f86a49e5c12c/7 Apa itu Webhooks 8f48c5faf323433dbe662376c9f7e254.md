# 7. Apa itu Webhooks ?

Created: July 21, 2022 2:35 PM

**Webhooks** adalah layanan yang memungkinkan kita membuat atau mengatur aplikasi GitHub yang meng-*subscribe* ke *event* tertentu di GitHub.com. Ketika salah satu dari *event* tersebut di *trigger*, maka akan mengirim payload HTTP POST ke URL konfigurasi webhook. Webhook dapat digunakan untuk memicu pembuatan CI, memperbarui *backup mirror*, atau bahkan men-*deploy* ke *server* *production*.

Webhooks dapat dipasang pada repositori tertentu. Setelah dipasang, webhook akan men-*trigger* setiap kali satu atau beberapa *event* dari *subscriber* terjadi. Kita dapat membuat hingga 20 webhook untuk setiap *event* pada setiap target pemasangan (organisasi spesifik atau repositori khusus).

Dengan menggunakan layanan webhooks ini kita bisa menghubungkan GitHub dengan Jenkins sehingga ketika kita melakukan *push program* ke GitHub, maka pada saat itu juga jenkins akan ter-

*trigger* dan melakukan *deploy* pada *server* yang kita sudah set sebelumnya.

# **Plugin Github**

Jenkins memiliki banyak sekali plugin yang berguna untuk memudahkan developer untuk melakukan CICD dengan integrasi ke platform lain, utilitas, dan lain sebagainya. Salah satu plugin Jenkins adalah [Github Plugin](https://plugins.jenkins.io/github/#plugin-content-github-hook-trigger-for-gitscm-polling). Ini adalah plugin yang memungkinkan integrasi antara Jenkins dan SCM (source control management) Github.

Salah satu fitur dari plugin Github ini adalah build trigger menggunakan webhook. Yaitu dengan menambahkan **/github-webhook/** sebagai url webhook jenkins lalu memasukannya kedalam setting webhook di Github.

Jadi kita dapat menginstall plugin Github agar dapat melakukan build trigger melalui webhook.