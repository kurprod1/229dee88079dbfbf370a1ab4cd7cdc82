# 12. Membuat JenkinsFile Sederhana

Created: July 21, 2022 7:30 PM

Pada bagian ini, kita akan mengenal beberapa langkah sederhana untuk membuat JenkinsFile. Proses pembuatan JenkinsFile ini akan sangat mudah apabila kita sudah menguasai bash programming.

Berikut adalah beberapa contoh JenkinsFIle pada beberapa bahasa pemrograman.

# **Java**

Untuk membuat JenkinsFile yang memuat job Java, berikut adalah contoh sintaks sederhananya.

```bash
pipeline {
    agent { docker { image 'maven:3.3.3' } }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
            }
        }
    }
}
```

# **Node.js / Javascript**

```bash
pipeline {
    agent { docker { image 'node:14-alpine' } }
    stages {
        stage('build') {
            steps {
                sh 'npm --version'
            }
        }
    }
}
```

# **Ruby**

```bash
pipeline {
    agent { docker { image 'ruby' } }
    stages {
        stage('build') {
            steps {
                sh 'ruby --version'
            }
        }
    }
}
```

# **Python**

```bash
pipeline {
    agent { docker { image 'python:3.5.1' } }
    stages {
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
    }
}
```

# **PHP**

```bash
pipeline {
    agent { docker { image 'php' } }
    stages {
        stage('build') {
            steps {
                sh 'php --version'
            }
        }
    }
}
```

# **Exercise**

Praktek :

1. Buat sebuah Jenkins pipeline untuk melakukan deployment web sederhana menggunakan PHP!
2. Buat juga JenkinsFile-nya.
3. Pastikan bahwa aplikasi sudah berjalan dengan baik.