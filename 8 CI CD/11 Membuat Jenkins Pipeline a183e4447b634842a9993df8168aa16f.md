# 11. Membuat Jenkins Pipeline

Created: July 21, 2022 2:50 PM

Setelah memahami konsep dasar pipelining pada Jenkins, sekarang mari kita buat sebuah pipeline sederhana untuk melakukan **build** dan **deploy** pada aplikasi berbasis **React** ke **Remote Server**.

App yang akan kita gunakan masih menggunakan **cilist (**[https://github.com/sdcilsy/cilist](https://github.com/sdcilsy/cilist)) dan kita melanjutkan praktikum dari modul sebelumnya. Jadi requirementnya pun tak jauh berbeda dari praktikum sebelumnya.

# **Create Pipeline**

Seperti yang sudah disebutkan sebelumnya, kita masih menggunakan app yang sama dengan repository yang sudah teman teman fork pada praktikum sebelumnya. Kali ini kita akan memodifikasi repository dengan menambah **Jenkinsfile**.

Buat file bernama **Jenkinsfile** pada working directory dengan script berikut.

```bash
pipeline {
 agent any

 environment {
   GIT_COMMIT_SHORT = sh(returnStdout: true, script: '''echo $GIT_COMMIT | head -c 7''')
 }

 stages {
   stage('Prepare .env') {
     steps {
       sh 'echo GIT_COMMIT_SHORT=$(echo $GIT_COMMIT_SHORT) > .env'
     }
   }

   stage('Build database') {
     steps {
       dir('database') {
         sh 'docker build . -t cilist-pipeline-db:$GIT_COMMIT_SHORT'
         sh 'docker tag cilist-pipeline-db:$GIT_COMMIT_SHORT profesorgreen36/cilist-pipeline-db:$GIT_COMMIT_SHORT'
         sh 'docker push profesorgreen36/cilist-pipeline-db:$GIT_COMMIT_SHORT'
       }
     }
   }

   stage('Build backend') {
     steps {
       dir('backend') {
         sh 'docker build . -t cilist-pipeline-be:$GIT_COMMIT_SHORT'
         sh 'docker tag cilist-pipeline-be:$GIT_COMMIT_SHORT profesorgreen36/cilist-pipeline-be:$GIT_COMMIT_SHORT'
         sh 'docker push profesorgreen36/cilist-pipeline-be:$GIT_COMMIT_SHORT'
       }
     }
   }

   stage('Build frontend') {
     steps {
       dir('frontend') {
         sh 'docker build . -t cilist-pipeline-fe:$GIT_COMMIT_SHORT'
         sh 'docker tag cilist-pipeline-fe:$GIT_COMMIT_SHORT profesorgreen36/cilist-pipeline-fe:$GIT_COMMIT_SHORT'
         sh 'docker push profesorgreen36/cilist-pipeline-fe:$GIT_COMMIT_SHORT'
       }
     }
   }

   stage('Deploy to remote server') {
     steps {
       sshPublisher(publishers: [sshPublisherDesc(configName: 'Remote Server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''docker compose up -d
      
       sleep 40

       docker compose restart backend''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '.env,docker-compose.yaml')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
     }
   }
 }
}
```

Script dapat dilihat di [https://gist.github.com/sdcilsy/896712e4fdddcddb8e3f2a7d6b19c4de](https://gist.github.com/sdcilsy/896712e4fdddcddb8e3f2a7d6b19c4de)

Kita sedikit breakdown script Jenkinsfile yang kita buat tadi.

Script dibawah menginstruksikan agar Jenkins melakukan build pada agent yang tersedia. Pada kasus ini, karena tidak ada agent lain selain machine Jenkins sendiri, maka build akan dilakukan pada on premise Jenkins.

```bash
agent any
```

Block **environment** dibawah menginstruksikan agar Jenkins membuat **environment variable** bernama **GIT_COMMIT_SHORT** untuk nantinya digunakan untuk tag image. Selengkapnya bisa dilihat di [dokumentasi](https://www.jenkins.io/doc/book/pipeline/syntax/#environment).

```bash
environment {
    GIT_COMMIT_SHORT = sh(returnStdout: true, script: '''echo $GIT_COMMIT | head -c 7''')
  }
```

Block **Stages** dibagi menjadi stage stage lagi dengan nama masing masing.

Stage pertama yaitu mempersiapkan **.env** yang berisikan tag image yang akan di deploy ke remote server. Stage ini diberi nama **Prepare .env**.

```bash
stage('Prepare .env') {
     steps {
       sh 'echo GIT_COMMIT_SHORT=$(echo $GIT_COMMIT_SHORT) > .env'
     }
   }
```

Lalu dibawahnya ada **stage stage** yang berisikan instruksi untuk melakukan **build image** docker dan push ke registry menggunakan instruksi **shell** atau **sh**. Step dilakukan pada masing masing directory dengan bantuan instruksi **[dir()](https://www.jenkins.io/doc/pipeline/steps/workflow-basic-steps/#dir-change-current-directory)**.

```bash
stage('Build database') {
      steps {
        dir('database') {
          sh 'docker build . -t cilist-pipeline-db:$GIT_COMMIT_SHORT'
          sh 'docker tag cilist-pipeline-db:$GIT_COMMIT_SHORT profesorgreen36/cilist-pipeline-db:$GIT_COMMIT_SHORT'
          sh 'docker push profesorgreen36/cilist-pipeline-db:$GIT_COMMIT_SHORT'
        }
      }
    }

    stage('Build backend') {
      steps {
        dir('backend') {
          sh 'docker build . -t cilist-pipeline-be:$GIT_COMMIT_SHORT'
          sh 'docker tag cilist-pipeline-be:$GIT_COMMIT_SHORT profesorgreen36/cilist-pipeline-be:$GIT_COMMIT_SHORT'
          sh 'docker push profesorgreen36/cilist-pipeline-be:$GIT_COMMIT_SHORT'
        }
      }
    }

    stage('Build frontend') {
      steps {
        dir('frontend') {
          sh 'docker build . -t cilist-pipeline-fe:$GIT_COMMIT_SHORT'
          sh 'docker tag cilist-pipeline-fe:$GIT_COMMIT_SHORT profesorgreen36/cilist-pipeline-fe:$GIT_COMMIT_SHORT'
          sh 'docker push profesorgreen36/cilist-pipeline-fe:$GIT_COMMIT_SHORT'
        }
      }
    }
```

---

Pada stage **Deploy to remote server**, kita mengirimkan 2 file yaitu **.env**, dan **docker-compose.yaml** ke **Remote Server**. Lalu mengeksekusi command **docker compose**.

```bash
stage('Deploy to remote server') {
      steps {
        sshPublisher(publishers: [sshPublisherDesc(configName: 'Remote Server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''docker compose up -d
        
        sleep 40

        docker compose restart backend''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '.env,docker-compose.yaml')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
      }
    }
```

---

Karena block/section ini cukup sulit untuk kita sendiri yang buat, maka kita gunakan **snippet generator** dari Jenkins sendiri.

Teman teman bisa mencobanya di link **Pipeline Syntax** yang ada pada Job.

![https://lh4.googleusercontent.com/Y3JjOobA6ERLcvlThKXmWFVKPdRWGcmVnoH3gp0BAmtg0Fl_eTGTkWxDrM6BnOI8ZZifkwupKwkeLGhVTZ8lGiLjvdQwqqQ_aQpLTGQ_KiPFyj_jBX5MMbqiNAvIox9BO4OCWm8bRI2bEUIBg2FE9xOTfAl76QFMz5WBnLniX3t29NYnvBSUbrhm7w](https://lh4.googleusercontent.com/Y3JjOobA6ERLcvlThKXmWFVKPdRWGcmVnoH3gp0BAmtg0Fl_eTGTkWxDrM6BnOI8ZZifkwupKwkeLGhVTZ8lGiLjvdQwqqQ_aQpLTGQ_KiPFyj_jBX5MMbqiNAvIox9BO4OCWm8bRI2bEUIBg2FE9xOTfAl76QFMz5WBnLniX3t29NYnvBSUbrhm7w)

Kita akan generate step dari plugin Publish Over SSH dengan memilih sample step **sshPublisher: Send build artifacts over SSH**.

![https://lh3.googleusercontent.com/0ipQdAebu2jCPnR8p9IEw17zrQF8COhs6TyezPTfCRl8RRHnL0IWlnolTeAmMS9dghi7MqYdumuVh190BxolIRQUSSyrHUQ6tUx4pjIgEyD2z-ZnysrPWxFeT98lhLlAPvezV32FiCUzws0xzuSxdJ7T_6YPhGSYTiC8QetJAJCL0B7UiM_CJNiz1A](https://lh3.googleusercontent.com/0ipQdAebu2jCPnR8p9IEw17zrQF8COhs6TyezPTfCRl8RRHnL0IWlnolTeAmMS9dghi7MqYdumuVh190BxolIRQUSSyrHUQ6tUx4pjIgEyD2z-ZnysrPWxFeT98lhLlAPvezV32FiCUzws0xzuSxdJ7T_6YPhGSYTiC8QetJAJCL0B7UiM_CJNiz1A)

Seperti pada konfigurasi Job praktikum sebelumnya, kita masukan Name, Source Files, dan Exec Commands. Pada **source file**, kita mengirim 2 file dipisahkan dengan koma.

![https://lh5.googleusercontent.com/ZOIRnWvuquXPjp4VJq7DmsGic1hmGMtB-yf6igG3qSFBLzB2cKlb5aV_KrEiBKMyIH3bf8nZ_yOF67a-U8mMKczZMNQqcSujOl5CGEuZBqvaA4qoKrRNemgc9plVWOv-WmgJpsklBTfBwvpj93FrY8t9gmZlo7jfMAzSW6R1mx6-04CEtHtgDlhb9w](https://lh5.googleusercontent.com/ZOIRnWvuquXPjp4VJq7DmsGic1hmGMtB-yf6igG3qSFBLzB2cKlb5aV_KrEiBKMyIH3bf8nZ_yOF67a-U8mMKczZMNQqcSujOl5CGEuZBqvaA4qoKrRNemgc9plVWOv-WmgJpsklBTfBwvpj93FrY8t9gmZlo7jfMAzSW6R1mx6-04CEtHtgDlhb9w)

Setelah kita klik **Generate Pipeline Script**, kita akan dapat **step** yang dapat kita masukan kedalam **stage**.

![https://lh6.googleusercontent.com/cmfM7fpsTL5_1Je660wlJhqLFKr36bmHVV3IBSXEYSmg9WLa7wqzn91OLZzxdUzFGMss0ZEg03h2pgsLIap-IBh9Nk5eNkaXd0YipKZlr0aOLHXNaC1sDafnZfCU-h-sKYCuhJaUSp6d1aKkdlSYAjfEEH2xtteM5S3jNkJMFlyubNdp-6p_FRLGRg](https://lh6.googleusercontent.com/cmfM7fpsTL5_1Je660wlJhqLFKr36bmHVV3IBSXEYSmg9WLa7wqzn91OLZzxdUzFGMss0ZEg03h2pgsLIap-IBh9Nk5eNkaXd0YipKZlr0aOLHXNaC1sDafnZfCU-h-sKYCuhJaUSp6d1aKkdlSYAjfEEH2xtteM5S3jNkJMFlyubNdp-6p_FRLGRg)

# **Create Job**

Karena kita sudah melakukan **forking**, setup SSH ke remote server, setup webhook, dan setup lain sebagainya, yang kita akan lakukan saat ini adalah membuat Job baru dengan jenis Pipeline.

![https://lh5.googleusercontent.com/iBfpVMNOE4joF0I54-dfENODokR6q7tVsa4ZpbsRP5uYDpE15zvA3obEQbMJYFS70HNUunv8RHT3uE9qY-HZcLivS_WO38h0Mo8L2u2AYSW1z31iYN14FgakfWIQsDkpnm42Yzh25bjDmP6snvr-bUQ42gIdUU9LA-f3CWW_v1cYWFtUm9O3Hjootg](https://lh5.googleusercontent.com/iBfpVMNOE4joF0I54-dfENODokR6q7tVsa4ZpbsRP5uYDpE15zvA3obEQbMJYFS70HNUunv8RHT3uE9qY-HZcLivS_WO38h0Mo8L2u2AYSW1z31iYN14FgakfWIQsDkpnm42Yzh25bjDmP6snvr-bUQ42gIdUU9LA-f3CWW_v1cYWFtUm9O3Hjootg)

Pada section **Build Trigger**, kita dapat memilih opsi **GitHub hook trigger for GITScm polling** karena kita sudah mensetup webhook pada praktikum sebelumnya.

![https://lh4.googleusercontent.com/fdv9DGXUJ98oESJwJ6sLZGvCnU7qt8_61lxdLHs28FZsLMiJxcEpC8k9T2MqNsiPSi48UT5ZoOE3M5uEKG06edIKuYu56Ht6mxR2_IfbhoUm__jj9-I--iORxzKDmCtLf_T-ofl4Ez9f6pqI1PfsO1zqohy5KL8Nmyw5qYrrsFrwtMHS0TrRgVMBjQ](https://lh4.googleusercontent.com/fdv9DGXUJ98oESJwJ6sLZGvCnU7qt8_61lxdLHs28FZsLMiJxcEpC8k9T2MqNsiPSi48UT5ZoOE3M5uEKG06edIKuYu56Ht6mxR2_IfbhoUm__jj9-I--iORxzKDmCtLf_T-ofl4Ez9f6pqI1PfsO1zqohy5KL8Nmyw5qYrrsFrwtMHS0TrRgVMBjQ)

Lalu pada section Pipeline, kita set **Definition** menjadi pipeline Script from SCM karena kita menggunakan Jenkinsfile yang sudah ada di repository. **SCM** kita ubah menjadi git. Masukan repository beserta credential nya. Lalu kita set letak **Jenkinsfile** pada repository namun kita biarkan secara default.

![https://lh6.googleusercontent.com/sP_zgWgfN-Rd1D21OMVAZ-BndSJzh26RC3tla8I6YwkUB_uzPWVmDF9VrOpjLVra89I3VQPqJ25m__WZWa8RKYqImSrtG9wMZy0QR4w8xJj23P6XCQ8lvbRC3OlqlBMmOMrrDBTCMdrHcLhLKXEW-3Z8QyEYD6dkV8APhDNJU-KQwX8XQ3tFCmAn8w](https://lh6.googleusercontent.com/sP_zgWgfN-Rd1D21OMVAZ-BndSJzh26RC3tla8I6YwkUB_uzPWVmDF9VrOpjLVra89I3VQPqJ25m__WZWa8RKYqImSrtG9wMZy0QR4w8xJj23P6XCQ8lvbRC3OlqlBMmOMrrDBTCMdrHcLhLKXEW-3Z8QyEYD6dkV8APhDNJU-KQwX8XQ3tFCmAn8w)

Lalu kita dapat save Job.

# **Testing**

Kita tinggal melakukan perubahan pada repository dan melihat hasilnya.

```bash
git add .
git commit -m "edit readme"
git push
```

---

Build akan secara otomatis berjalan karena webhook.

![https://lh4.googleusercontent.com/6zp5UaVQ7sDX4ID32JZi6A0zFXsGA3r5Q8Nl40IAO1FQHK8hHCLf2q2WJjyp-pkzs5r2v68Qj6PbI2SUb5TindpGg4Pt5dB6bZc32LIILJnwoSwR_RitVdZlHnj_vi6EGq3qmQ36I2drE6oz-ZFa88TukLRAFD3LJS2dfuMxihmXYel-V25taY4dbA](https://lh4.googleusercontent.com/6zp5UaVQ7sDX4ID32JZi6A0zFXsGA3r5Q8Nl40IAO1FQHK8hHCLf2q2WJjyp-pkzs5r2v68Qj6PbI2SUb5TindpGg4Pt5dB6bZc32LIILJnwoSwR_RitVdZlHnj_vi6EGq3qmQ36I2drE6oz-ZFa88TukLRAFD3LJS2dfuMxihmXYel-V25taY4dbA)

Lalu pada dashboard Job kita dapat melihat eksekusi per stage dan waktu yang diperlukan.

![https://lh4.googleusercontent.com/Ibj27zpdJRabAmp0MbFnJR0dvVAnTfrKOCyGbT0qnpr2LOmKm-BiVnjzTN376Vi6qOnbVejb7aGghxDAX6sTdGqPFgz2Q6xlb2OlPDfQVK1goQCB4GVuW9jgCEp_-xfEsdv0zptOMEHR37j5_p7I06Xqgkdi60QWwzOrNqtCGakJauRZ02uKAu3PRA](https://lh4.googleusercontent.com/Ibj27zpdJRabAmp0MbFnJR0dvVAnTfrKOCyGbT0qnpr2LOmKm-BiVnjzTN376Vi6qOnbVejb7aGghxDAX6sTdGqPFgz2Q6xlb2OlPDfQVK1goQCB4GVuW9jgCEp_-xfEsdv0zptOMEHR37j5_p7I06Xqgkdi60QWwzOrNqtCGakJauRZ02uKAu3PRA)

Kita akan mengakses remote server dengan port 3000.

![https://lh5.googleusercontent.com/J7etixl_-9dHmPyboNGduA1gNstcGKMWk0fCiLlUrWxOIPYggrbo_5TQslXo3GrIPuv6NlWeW4rFX8_JWtxZCd09JY1CTgbz9xbDPovfSCEn28Bw6pFvytQkIEjhPFMj_SqlaLoIX0qq05_Tqgqd8ZXJ7AKaPEQjI80aTS9HCDyWoNfC-IOTkpCMqA](https://lh5.googleusercontent.com/J7etixl_-9dHmPyboNGduA1gNstcGKMWk0fCiLlUrWxOIPYggrbo_5TQslXo3GrIPuv6NlWeW4rFX8_JWtxZCd09JY1CTgbz9xbDPovfSCEn28Bw6pFvytQkIEjhPFMj_SqlaLoIX0qq05_Tqgqd8ZXJ7AKaPEQjI80aTS9HCDyWoNfC-IOTkpCMqA)