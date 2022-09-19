# 13. Github Action

Created: July 21, 2022 9:52 PM

Github  sering kali digunakan para developer aplikasi untuk menyimpan repository serta berbagi source code antar developer. Selain itu Github juga memiliki fitur CI/CD yang disediakan untuk membantu para developer dalam automasi SDCL yang mereka gunakan agar lebih efektif dan efisien yaitu adalah **Github Action**.

![https://lh6.googleusercontent.com/LERjsyvXl-iIw7CcKXxFvKvYe-b283ZOF1t-wpG_HB4WST-BwZqImnyq9zlUSozpd33BmeV_vu7Lh4OL59absCgs2CtCNRP-knHgrsynqzdebC1NuQAzr210s9Y7N5xNB3yWih2MZyx76FG7u28C6Q](https://lh6.googleusercontent.com/LERjsyvXl-iIw7CcKXxFvKvYe-b283ZOF1t-wpG_HB4WST-BwZqImnyq9zlUSozpd33BmeV_vu7Lh4OL59absCgs2CtCNRP-knHgrsynqzdebC1NuQAzr210s9Y7N5xNB3yWih2MZyx76FG7u28C6Q)

CI/CD dari Github ini sering disebut **workflow** yang bisa kita buat dengan cara membuat directory **./github/workflows** dengan membuat sebuah file **.yaml** yang berisikan sekumpulan instruksi automatisasi untuk melakukan build, test, dan deploy aplikasi, hampir mirip seperti **Declarative Jenkins**.

![*Diagram Github Action*](https://lh4.googleusercontent.com/8sG6GBbXSj18miacUHyWh18KOvGjS0Lz2JCRjo71cgWaXLNC9iw6LkfruXEtyOizrdim4y6w9WwEAhcY8QJvb-XFDhGq2a_wABENu2tdOlN4KNunp3hhj0HjS9DEe2YKWDB36ttahfVGxILOPzDORw)

*Diagram Github Action*

Diagram diatas menunjukkan bagaimana Actions bekerja menjalankan CI/CD pada aplikasi yang sedang dikembangkan. Suatu **event** secara otomatis mentrigger **workflow**, yang berisi **jobs**. **Jobs** kemudian menggunakan **steps** untuk mengontrol urutan **action** yang dijalankan. **Action** ini adalah perintah yang mengotomatiskan pengujian aplikasi.

# **Components**

Ada beberapa component dari **Github Action** ini yang menyusun CI/CD pada aplikasi. Berikut adalah komponen komponen tersebut.

1. **Workflow**
    
    Workflow adalah prosedur otomatis yang ditambahkan ke repositori aplikasi. Workflow terdiri dari satu atau lebih **jobs** dan dapat dijadwalkan atau **trigger** oleh suatu **event**. Workflow dapat digunakan untuk build, test, package, release, atau deploy aplikasi di GitHub.
    
2. **Event**
    
    Seperti yang sudah disebutkan diawal, sebuah event dapat mentrigger workflow. Event ini dapat berupa commit code, push repository, pull request, dan lain sebagainya. Event ini lah yang nantinya akan memulai serangkaian **jobs** yang ada pada workflow.
    
3. **Jobs**
    
    Merupakan sebuah rangkaian task yang runner eksekusi. Runner ini secara default melakukan Jobs secara pararel. Kita juga dapat mengkonfigurasi ini agar berjalan secara sequential. Misalnya mengerjakan **job-2** apabila **job-1** sukses.
    
4. **Step**
    
    Step adalah tugas yang dapat menjalankan perintah dalam suatu **jobs**. Sebuah step dapat berupa **action** atau **perintah shell**. Setiap **step** dalam job dijalankan pada runner yang sama, memungkinkan action dalam pekerjaan itu untuk berbagi data satu sama lain. Misalnya ada step setup **node.js** untuk build dan mengetes aplikasi.
    
5. **Action**
    
    Action adalah perintah mandiri yang digabungkan menjadi step-step untuk membuat jobs. Action adalah blok step step yang digabung dari alur kerja. Anda dapat membuat action sendiri, atau menggunakan action yang dibuat oleh komunitas GitHub.
    
    Action dapat dianalogikan seperti API yang siap dipanggil untuk melakukan task tanpa kita harus membuat langkah langkah terlebih dahulu.
    

# **Membuat Workflow Sederhana**

Setelah memahami konsep CI/CD dari Github Action, kali ini kita akan membuat sebuah CI/CD menggunakan Github Action. Kita akan membuat CI/CD untuk build dan test aplikasi berbasis react menggunakan Github Action.

Prerequisite:

- Github Account
- Aplikasi yang digunakan ([https://github.com/sdcilsy/todo-react](https://github.com/sdcilsy/todo-react))

Pertama tama, login menggunakan Github Account masing masing untuk melakukan **fork** repository aplikasi yang akan digunakan.

![https://lh3.googleusercontent.com/sNuksrpOvkHRVlGZFJ8KcoiI-5ykoutPRQIBptSn39aM20rZWVOWLRG16YbOxcdlbgSdChpCO0xocKnEFzZQfauPUZ4hIKsbr5wJNZH8nSRovhsWR-aMZAJNlpYWsF9_cSOZR_Ih-5VET4aw9LP2cA](https://lh3.googleusercontent.com/sNuksrpOvkHRVlGZFJ8KcoiI-5ykoutPRQIBptSn39aM20rZWVOWLRG16YbOxcdlbgSdChpCO0xocKnEFzZQfauPUZ4hIKsbr5wJNZH8nSRovhsWR-aMZAJNlpYWsF9_cSOZR_Ih-5VET4aw9LP2cA)

Setelah itu silahkan untuk clone repository yang sudah di fork tadi dan membuka nya dengan text editor favorite masing masing.

Setelah itu, buat sebuah directory **.github/workflows** pada working directory. Disinilah kita akan menyimpan workflow untuk aplikasi yang akan kita build dan test.

```bash
mkdir -p .github/workflows
```

Setelah itu, kita akan membuat file dengan nama **ga-build-test.yaml** yang berisikan rangkaian instruksi untuk melakukan build dan test aplikasi pada environment github. Kita akan setting setiap kali ada push ke repository, maka CI/CD akan berjalan.

Isi dari **ga-build-test.yaml** adalah sebagai berikut.

```bash
name: Todo App Build Test

on:
  push:
    branches: ![ master ]
  pull_request:
    branches: ![ master ]

jobs:
  build_and_test:
    runs-on: ubuntu-latest
    steps:
    - name: Cloning project
      uses: actions/checkout@v2
    - name: List files
      run: |
        ls ${{ github.workspace }}
    - name: Setup Node.js 14
      uses: actions/setup-node@v2
      with:
        node-version: '14'
    - name: Install project
      run: npm install
    - name: Test project
      run: npm test
```

Kita akan melihat bagian bagian dari workflow sederhana yang kita buat.

Name merupakan nama dari workflow yang kita buat. Ini mengidentifikasi nama dari workflow serta informasi workflow tersebut. Nama ini akan terpampang di tab Action Github.

```bash
name: Todo App Build Test
```

**On** merupakan trigger yang dipasang untuk memicu workflow. Contoh ini menggunakan **event** push dan **pull request**, sehingga **jobs** akan otomatis tereksekusi setiap kali seseorang push changes ke branch **master** repository atau ada request untuk **pull**. Kita dapat mengatur workflow agar hanya berjalan di branch, path, atau tag tertentu.

```bash
on:
  push:
    branches: ![ master ]
  pull_request:
    branches: ![ master ]
```

**Jobs** seperti yang sudah dijelaskan diawal, terdapat beberapa aturan aturan/instruksi. Kita beri nama build_and_test dan terdapat konfigurasi **runs-on** dimana itu merupakan environment yang digunakan GitHub untuk mengeksekusi instruksi intruksi tersebut. Jika ingin menggunakan environment lain yang Github sediakan, silakan baca [dokumentasi](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners).

```bash
jobs:
  build_and_test:
    runs-on: ubuntu-latest
```

**Step** berisi beberapa instruksi instruksi individu yang berupa **action** atau **command shell**. Dapat dilihat, kita memiliki 5 step dengan masing masing memiliki nama. Perlu diingat, jika kita tidak bisa menggunakan action dan run bersamaan. karena akan berakibat error.

```bash
steps:
```

Pada step pertama, kita “menclone” repository kita. Ini bisa kita lakukan berkat actions yang sudah disiapkan github yaitu **checkout**.

```bash
- name: Cloning project
      uses: actions/checkout@v2
```

Step kedua, kita akan melihat list file yang terdapat pada repository kita. Kali ini kita menggunakan command shell yaitu **ls**. Dapat dilihat kita menggunakan environment variable dari Github Action. Selengkapnya bisa dibaca di [dokumentasi](https://docs.github.com/en/actions/learn-github-actions/environment-variables#default-environment-variables).

```bash
- name: List files
      run: |
        ls ${{ github.workspace }}
```

Step ketiga, kita setup node.js karena aplikasi yang digunakan berbasis react, kita perlu menggunakan Node.js. Dalam hal ini kita akan menggunakan versi major 14.

```bash
- name: Setup Node.js 14
      uses: actions/setup-node@v2
      with:
        node-version: '14'
```

Step keempat setelah kita setup Node.js, kita melakukan install package packages yang aplikasi butuhkan. Dalam hal ini package package tersebut dapat dihandle oleh perintah **npm** sebagai package manager Node.js.

```bash
- name: Install project
      run: npm install
```

Step kelima kita akan melakukan test pada aplikasi menggunakan npm.

```bash
- name: Test project
      run: npm test
```

Setelah semuanya beres, langkah selanjutnya adalah untuk push changes ke repository masing masing.

Ini akan mentrigger Github Action untuk secara otomatis melakukan build dan test kepada aplikasi kita.

```bash
git add .
git commit -m "add workflow"
git push
```

Setelah itu, mari kita lihat repository kita di Github. Lalu lihat tab action. Pilih “Todo App Build Test”.

![https://lh6.googleusercontent.com/OC4BJu8fj5yBvf6Cug2J7inECqH5rf2nEAUojZ9gBECiyem738CplgUvGlJy3iDB7uCo9ewzdnu-rfxBaMlu_vuYbMEjmsTzX5KqNPv__3OpHsJB1M7oiiLEd6PIJfzT2NHzOMuOebc8RdYCCb5nZQ](https://lh6.googleusercontent.com/OC4BJu8fj5yBvf6Cug2J7inECqH5rf2nEAUojZ9gBECiyem738CplgUvGlJy3iDB7uCo9ewzdnu-rfxBaMlu_vuYbMEjmsTzX5KqNPv__3OpHsJB1M7oiiLEd6PIJfzT2NHzOMuOebc8RdYCCb5nZQ)

Bisa kita lihat, workflow yang sudah kita buat akan segera di eksekusi dengan status **Queued**. Tunggu beberapa saat agar dapat melihat hasilnya.

![https://lh4.googleusercontent.com/1cK8Bs8jMsbA6cUDLgUIDx24sk5MPUYga9e2OTjiHnwP08pHn1PRXqiM6gbc_zRmEfX1USKa1UZruGDx_sbQSYVFe1xnlj8O57ikVB9pNAbp61PfyHtx_cCaDzKQqfn8AeebI0WmIQ847EWUZveBVQ](https://lh4.googleusercontent.com/1cK8Bs8jMsbA6cUDLgUIDx24sk5MPUYga9e2OTjiHnwP08pHn1PRXqiM6gbc_zRmEfX1USKa1UZruGDx_sbQSYVFe1xnlj8O57ikVB9pNAbp61PfyHtx_cCaDzKQqfn8AeebI0WmIQ847EWUZveBVQ)

Kita sudah berhasil membuat workflow dan hasil dari eksekusi CI/CD nya sukses.