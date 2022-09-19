# 16. Study Case: Writing Dockerfiles

Created: July 5, 2022 10:45 AM

Kalau Anda melihat docker file diatas, pasti pusing, bukan? Apalagi kita masih dalam tahap belajar. Pada bagian ini, kita akan mempelajari beberapa studi kasus membuat Dockerfile yang sederhana.

# **Menambahkan Landing Page ke Container NGINX**

Masih ingat landing page yang ada di materi Linux sebelumnya? Untuk membuat NGINX menampilkan landing page tersebut tentunya ada beberapa konfigurasi yang perlu dilakukan. Kali ini kita akam mulai belajar menyusun Dockerfile dari hal yang sederhana, yaitu meng-”*inject*” file html dan php ke image NGINX.

Langkah pertama, kita clone terlebih dahulu file landing page yang akan dimasukkan kedalam *image* Docker. Apabila Anda telah memiliki file ini, Anda bisa langsung ke langkah selanjutnya.

```bash
$ git clone https://github.com/sdcilsy/landing-page.git
```

Untuk membuat Dockerfile, kita perlu membuat direktori khusus dimana file *source code* disimpan di direktori yang sama dengan Dockerfile. Selanjutnya, kita akan melakukan *pull* terhadap image nginx dengan versi alpine dengan perintah berikut.

```bash
$ docker pull nginx:alpine
```

![https://lh4.googleusercontent.com/2VSLsAk0eTPZNe00tlKdYjXbX2IoMyhNYnfct-mZCxqgCJ_TBcvFPQqXdWvYbRlgVZbRC3xf-S1krw_Do_ZVWig2XyO3WJBXo7mFjJBYAQ8rhLYthref-4XOctch_SglWojwnLM8czYTYTM0wQ](https://lh4.googleusercontent.com/2VSLsAk0eTPZNe00tlKdYjXbX2IoMyhNYnfct-mZCxqgCJ_TBcvFPQqXdWvYbRlgVZbRC3xf-S1krw_Do_ZVWig2XyO3WJBXo7mFjJBYAQ8rhLYthref-4XOctch_SglWojwnLM8czYTYTM0wQ)

Kemudian kita edit Dockerfile dengan menambahkan konfigurasi berikut.

```docker
FROM nginx:alpine
COPY landing-page/ /usr/share/nginx/html/
```

![https://lh3.googleusercontent.com/QXNq1qQsH8MnQslcDIabWDtn5DVWWyuokDi4Yc7vRcoIgEfYtzv4wem5pE-T97lScNo7XjyH9wpHEZdaolU-ZCoRCjbZbQxspgl-HZSobFplkCpZi-HI8PU9XfQBxzkF-K85Dk3JiHi-vC2n2Q](https://lh3.googleusercontent.com/QXNq1qQsH8MnQslcDIabWDtn5DVWWyuokDi4Yc7vRcoIgEfYtzv4wem5pE-T97lScNo7XjyH9wpHEZdaolU-ZCoRCjbZbQxspgl-HZSobFplkCpZi-HI8PU9XfQBxzkF-K85Dk3JiHi-vC2n2Q)

Penjelasan:

- FROM nginx:alpine, artinya kita menggunakan image nginx versi alpine yang telah di-pull sebelumnya.
- COPY landing-page /usr/share/nginx/html/, artinya kita melakukan penyalinan file-file yang ada di direktori landing-page ke direktori /usr/share/nginx/html/ yang ada pada image NGINX nantinya.

Setelah itu, lakukan perintah docker build untuk membuat docker image yang telah ditambahkan file landing page diatas. Lakukan perintah berikut:

```bash
$ docker image build -t nginx-lp:1.0 .
```

Setelah berhasil melakukan build image, coba jalankan image tersebut dengan perintah berikut.

![https://lh5.googleusercontent.com/MHyflf1tAjlPNapyiHSGEMjjvIsUbmozqT2c_8FeQaDy4PbeKUFDQy1G0rZBOdoCNNOKd9tUS61IdHCk5HEQ_Huld2gq5Zvj6b1UGVusqHjO-phr1pmkbBSf1U2YmAzNphpWqAegSXu0Qgt3oA](https://lh5.googleusercontent.com/MHyflf1tAjlPNapyiHSGEMjjvIsUbmozqT2c_8FeQaDy4PbeKUFDQy1G0rZBOdoCNNOKd9tUS61IdHCk5HEQ_Huld2gq5Zvj6b1UGVusqHjO-phr1pmkbBSf1U2YmAzNphpWqAegSXu0Qgt3oA)

```bash
$ docker run --rm -it -p 8080:80 nginx-lp:1.0
```

Selanjutnya, kita akses menggunakan web browser dengan alamat ![http://localhost:8080](http://localhost:8080/)

![https://lh5.googleusercontent.com/_1TBCKu4IKo6BYIg1NU8ZiBBis8_cDyIubTBu6HV-bsvpP69T6sYdOqvxbFKcBFhJBIe3kov0Pd_KqnX31IX_nnFkNM_jxsCgXDkBtgDVOli1sWG-Yi2zhlVf7RScl45YBLvOqtnLGAyK-wEvQ](https://lh5.googleusercontent.com/_1TBCKu4IKo6BYIg1NU8ZiBBis8_cDyIubTBu6HV-bsvpP69T6sYdOqvxbFKcBFhJBIe3kov0Pd_KqnX31IX_nnFkNM_jxsCgXDkBtgDVOli1sWG-Yi2zhlVf7RScl45YBLvOqtnLGAyK-wEvQ)

# **Membuat Dockerfile untuk Aplikasi Python**

Aplikasi yang menggunakan Python saat ini memang sedang cukup *hype* lagi, karena adanya trend *Artificial Intelligence* dan *Machine Learning*, ditambah adanya data science, yang menggunakan Python untuk menjalankan aplikasi mereka. Pada studi kasus kali ini, kita akan membuat Dockerfile untuk mendeploy aplikasi Python.

Langkah awal yang perlu dilakukan sama seperti sebelumnya, yaitu membuat direktori yang nantinya akan diisi file aplikasi Python dan Dockerfile. Kemudian, kita siapkan terlebih dahulu aplikasi Python yang akan dijalankan. Nama aplikasi yang akan kita jalankan bernama my_script.py.

```bash
$ nano my_script.py

# Sample taken from pyStrich GitHub repository

# https://github.com/mmulqueen/pyStrich

from pystrich.datamatrix import DataMatrixEncoder

encoder = DataMatrixEncoder('This is a DataMatrix.')

encoder.save('./datamatrix_test.png')

print(encoder.get_ascii())
```

![https://lh4.googleusercontent.com/uPm_wes_3Rqw8Pg5ru_Hjd0zpfh8Sk1r2T1PKo2OsHBG66OSBG0K1Va7-DqzBoBGppmZ49jnjyL5owbIlCS5PTKfISkvGH5ZQT5G6Yf6AgNfI4ZSOyMolGaTlQ-QR6jqEuxO1MIf-WHcvRFRSA](https://lh4.googleusercontent.com/uPm_wes_3Rqw8Pg5ru_Hjd0zpfh8Sk1r2T1PKo2OsHBG66OSBG0K1Va7-DqzBoBGppmZ49jnjyL5owbIlCS5PTKfISkvGH5ZQT5G6Yf6AgNfI4ZSOyMolGaTlQ-QR6jqEuxO1MIf-WHcvRFRSA)

Setelah itu, kita buat Dockerfile pada direktori yang sama.

![https://lh5.googleusercontent.com/gMgbhbIC_4tMsJMbUi6E67lxNRpeuTMRugN0f4OgQOArnKmZhGHLmHibSDhJXNYfHtHbNs840BygPMjcJBeoWKf6WDEksU4uNd0IkpRhMX4Pig30IsKeuRvG4XWDYU9Gqqajh12KjxlVkB7Hcw](https://lh5.googleusercontent.com/gMgbhbIC_4tMsJMbUi6E67lxNRpeuTMRugN0f4OgQOArnKmZhGHLmHibSDhJXNYfHtHbNs840BygPMjcJBeoWKf6WDEksU4uNd0IkpRhMX4Pig30IsKeuRvG4XWDYU9Gqqajh12KjxlVkB7Hcw)

Penjelasan:

- FROM python:3 → Command ini berarti kita akan menggunakan image python:3
- ADD my_script.py / → Fungsi ini bertujuan untuk memasukkan my_script.py ke dalam image Python dengan path /.
- RUN pip install pystrich → Berfungsi untuk melakukan instalasi pystrich pada Python, yang merupakan dependencies module untuk menjalankan my_script.py
- CMD ![ "python", "./my_script.py" ] → bertujuan untuk menjalankan command ketika image di-load.

Setelah itu, save Dockerfile.

Kemudian lakukan compile menggunakan perintah berikut.

```bash
docker build -t python-barcode .
```

Setelah selesai, kita akan coba menjalankan image python-barcode dengan menggunakan perintah berikut.

```bash
docker run python-barcode
```

![https://lh4.googleusercontent.com/5QOPTpe90UA8H83Cspwljsufqex0sRjmOh1Vj8uXfYcfwrY1uHnQQgPGL6ltWphsbhZCRC5tSZel5j-FkjOZ3WPkYzVGkCbJ3FV0m7fMTOe8_Y7SceleBfjwVdhvQEF4LkVYTh5JRPuA-FcR3A](https://lh4.googleusercontent.com/5QOPTpe90UA8H83Cspwljsufqex0sRjmOh1Vj8uXfYcfwrY1uHnQQgPGL6ltWphsbhZCRC5tSZel5j-FkjOZ3WPkYzVGkCbJ3FV0m7fMTOe8_Y7SceleBfjwVdhvQEF4LkVYTh5JRPuA-FcR3A)

Kita akan melihat hasil generate ASCII QR code .

# **Membuat Dockerfile untuk Aplikasi GoLang**

Golang (atau biasa disebut dengan Go) adalah bahasa pemrograman baru yang dikembangkan di Google oleh Robert Griesemer, Rob Pike, dan Ken Thompson pada tahun 2007 dan mulai diperkenalkan di publik tahun 2009. Penciptaan bahasa Go didasari bahasa C dan C++, oleh karena itu gaya sintaks-nya mirip.

Saat ini, cukup banyak startup dan industri yang menggunakan Golang dalam proses development aplikasi mereka. Maka dari itu, tidak ada salahnya kita belajar mengenai membuat Dockerfile untuk aplikasi dengan bahasa Go.

Pertama-tama, buatlah sebuah file bernama hello_server.go yang berisi script sebagai berikut.

```go
package main
 
import (
	"context"
	"fmt"
	"log"
	"net/http"
	"os"
	"os/signal"
	"syscall"
	"time"
 
	"github.com/gorilla/mux"
	"gopkg.in/natefinch/lumberjack.v2"
)
 
func handler(w http.ResponseWriter, r *http.Request) {
	query := r.URL.Query()
	name := query.Get("name")
	if name == "" {
		name = "Guest"
	}
	log.Printf("Received request for %s\n", name)
	w.Write(![]byte(fmt.Sprintf("Hello, %s\n", name)))
}
 
func main() {
	// Create Server and Route Handlers
	r := mux.NewRouter()
 
	r.HandleFunc("/", handler)
 
	srv := &http.Server{
		Handler:      r,
		Addr:         ":8080",
		ReadTimeout:  10 * time.Second,
		WriteTimeout: 10 * time.Second,
	}
 
	// Configure Logging
	LOG_FILE_LOCATION := os.Getenv("LOG_FILE_LOCATION")
	if LOG_FILE_LOCATION != "" {
		log.SetOutput(&lumberjack.Logger{
			Filename:   LOG_FILE_LOCATION,
			MaxSize:    500, // megabytes
			MaxBackups: 3,
			MaxAge:     28,   //days
			Compress:   true, // disabled by default
		})
	}
 
	// Start Server
	go func() {
		log.Println("Starting Server")
		if err := srv.ListenAndServe(); err != nil {
			log.Fatal(err)
		}
	}()
 
	// Graceful Shutdown
	waitForShutdown(srv)
}
 
func waitForShutdown(srv *http.Server) {
	interruptChan := make(chan os.Signal, 1)
	signal.Notify(interruptChan, os.Interrupt, syscall.SIGINT, syscall.SIGTERM)
 
	// Block until we receive our signal.
	<-interruptChan
 
	// Create a deadline to wait for.
	ctx, cancel := context.WithTimeout(context.Background(), time.Second*10)
	defer cancel()
	srv.Shutdown(ctx)
 
	log.Println("Shutting down")
	os.Exit(0)
}
```

Siapkan juga file dependencies berupa file go.mod dengan isi script sebagai berikut.

```go
module github.com/callicoder/go-docker
 
require (
	github.com/gorilla/context v1.1.1
	github.com/gorilla/mux v1.6.2
	gopkg.in/natefinch/lumberjack.v2 v2.0.0-20170531160350-a96e63847dc3
)
```

Kemudian, buatlah file go.sum dengan isi script sebagai berikut

```go
github.com/gorilla/context v1.1.1/go.mod h1:kBGZzfjB9CEq2AlWe17Uuf7NDRt0dE0s8S51q0aT7Yg=
github.com/gorilla/mux v1.6.2 h1:Pgr17XVTNXAk3q/r4CpKzC5xBM/qW1uVLV+IhRZpIIk=
github.com/gorilla/mux v1.6.2/go.mod h1:1lud6UwP+6orDFRuTfBEV8e9/aOM/c4fVVCaMa2zaAs=
gopkg.in/natefinch/lumberjack.v2 v2.0.0-20170531160350-a96e63847dc3 h1:AFxeG48hTWHhDTQDk/m2gorfVHUEa9vo3tp3D7TzwjI=
gopkg.in/natefinch/lumberjack.v2 v2.0.0-20170531160350-a96e63847dc3/go.mod h1:l0ndWWf7gzL7RNwBG7wST/UCcT4T24xpD6X8LsfU/+k=
```

Setelah itu, buatlah Dockerfile di direktori yang sama dengan script diatas. Isi dari Dockerfilenya adalah sebagai berikut.

```docker
# Dockerfile References: https://docs.docker.com/engine/reference/builder/
 
# Start from the latest golang base image
FROM golang
 
# Add Maintainer Info
MAINTANER Your Name "youremail@domain.tld"
 
# Set the Current Working Directory inside the container
WORKDIR /app
 
# Copy go mod and sum files
COPY go.mod go.sum ./
 
# Download all dependencies. Dependencies will be cached if the go.mod and go.sum files are not changed
RUN go mod download
 
# Copy the source from the current directory to the Working Directory inside the container
COPY . .
 
# Build the Go app
RUN go build -o main .
 
# Expose port 8080 to the outside world
EXPOSE 8080
 
# Command to run the executable
CMD !["./main"]
```

![https://lh6.googleusercontent.com/9xAxvu6jtS9m_cbgQULEPsJDY4ioZ3nhWJbnnGOJTvGgdg4UDlNaNwkdau_70BKNBjLdQKJZf_2UrXckCsaY8a9Z2t4ubdqfpf8V4o1795VQPNysoTnU89wvjXuUyCFzRa3ttCyel2GMsG7zsw](https://lh6.googleusercontent.com/9xAxvu6jtS9m_cbgQULEPsJDY4ioZ3nhWJbnnGOJTvGgdg4UDlNaNwkdau_70BKNBjLdQKJZf_2UrXckCsaY8a9Z2t4ubdqfpf8V4o1795VQPNysoTnU89wvjXuUyCFzRa3ttCyel2GMsG7zsw)

Selanjutnya, kita *build* Dockerfile diatas menggunakan perintah berikut.

```docker
docker build -t go-docker .
```

![https://lh3.googleusercontent.com/OfmlCOnfR1JQxP6em861UG9k0zb6fnJfxbBYFC-d4Ql6_-pTK4al0qLPWZ_wcjbfUHRvZhr4J8onGoJr13pvizRbJ928q9L658skHt2LZHP--ZN6QpogYUB8cnGtgIsBvl5yk2oyhQcLkEX95Q](https://lh3.googleusercontent.com/OfmlCOnfR1JQxP6em861UG9k0zb6fnJfxbBYFC-d4Ql6_-pTK4al0qLPWZ_wcjbfUHRvZhr4J8onGoJr13pvizRbJ928q9L658skHt2LZHP--ZN6QpogYUB8cnGtgIsBvl5yk2oyhQcLkEX95Q)

Untuk mengetes docker images yang telah dibuat, Anda dapat menggunakan perintah berikut.

```bash
$ docker run -d -p 8080:8080 go-docker
```

Untuk mencoba aplikasi yang telah dijalankan, kita coba menggunakan perintah berikut.

```bash
$ curl http://localhost:8080?name=SDCilsy
```

Hello, SDCilsy

![https://lh5.googleusercontent.com/Lxu3qezMUxS_-AkauNJklShVCgFecm5aOf0rhmp97wSEQxN0vZaknVH0U0lG-nYBjnANPTwWAt3gFgv18McJQyAgZC95JiDhTIiTUE9QtfKyBZkpT9sSxzFYFoBndHImK3VU0o7_37yUkXwmTw](https://lh5.googleusercontent.com/Lxu3qezMUxS_-AkauNJklShVCgFecm5aOf0rhmp97wSEQxN0vZaknVH0U0lG-nYBjnANPTwWAt3gFgv18McJQyAgZC95JiDhTIiTUE9QtfKyBZkpT9sSxzFYFoBndHImK3VU0o7_37yUkXwmTw)

kita juga dapat melakukan pengujian lewat web browser dengan menggunakan alamat ![http://localhost:8080](http://localhost:8080/), sehingga akan muncul tampilan sebagai berikut.

![https://lh6.googleusercontent.com/uU8GHJ08WzfGwqi72NpVPCbL22mTDE0JiWD4L280D9DZh-jFguCz-B8wW1t9cBZXtxW7LI0GY4tgFBgQVmWf_V8kUuBFSmcQMZH6x_Ov1DVy6wBtfKGf4LFaiV7_yLpT-jxdtcLI-mJmpw32og](https://lh6.googleusercontent.com/uU8GHJ08WzfGwqi72NpVPCbL22mTDE0JiWD4L280D9DZh-jFguCz-B8wW1t9cBZXtxW7LI0GY4tgFBgQVmWf_V8kUuBFSmcQMZH6x_Ov1DVy6wBtfKGf4LFaiV7_yLpT-jxdtcLI-mJmpw32og)