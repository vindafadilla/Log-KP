#Log Senin, 25 Juli 2016

Aktivitas yang telah dilakukan:
1. Belajar dan latihan Golang web programming
2. Memahami gin-gonic

##Mengapa Memilih GoLang untuk WebApp?

1. GoLang merupakan bahasa pemrograman yang open source tapi di back up oleh perusahaan yang besar seperti Google. GoLang berkembang dengan sangat cepat dan mendukung untuk teknologi cloud, ini juga alasan GoLang dipilih.
2. Banyak perusahaan besar menggunakan GoLang untuk project mereka.
3. Cepat. Untuk dipelajari, dikembangkan, di compile, di deploy, dan dijalankan.
4. GoLang adalah modern language. GoLang mendukung untuk solusi modern, dengan kata lain, GoLang ke depannnya banyak mendukung untuk teknologi di masa depan. Contoh teknologi yang sekarang mendukung penggunaan GoLang adalah cloud.
5. GoLang sangatlah simpel. GoLang mempunyai sintaks yang sederhana dengan workflow berbasis teks, desain yang minimalis, dan spesifikasi bahasa yang jelas.
6.  Concurrent. Yang dapat memungkinkan dalam menjalankan banyak proses dalam waktu yang sama.
7. Pengembangan yang cepat dan komunitas yang terus berkembang.
8.  Mendukung cross-platform dengan baik.
9. GoLang aman. Dalam Go , setiap variabel harus memiliki tipe yang terkait dengannya , sehingga pengembang harus teliti dan tidak dapat melewatkan rincian yang kemudian mungkin menyebabkan bug .
10. Banyak open source library yang bagus untuk digunakan, yang dapat menambah library standard yang ada.
11. Scalable, modular, maintainable, high-performance.

##GoLang WebApp
Aplikasi web/ web app adalah sebuah program komputer yang
merespon sebuah http request oleh klien dan mengirimkan HTML kembali ke klien dalam HTTP response. 
Yang telah dipelajari:
1. Cara kerja WebApp
2. Pengenalan singkat HTTP
3. HTTP request 
4. Request method di GoLang
5. HTTP response
6. Penggunaan GoLang di webApp: Hello Go (Hello World GoLang di webApp).


#Log Selasa, 26 Juli 2016

##Membuat Milestone dan Logbook

##Membuat program GoLang sederhana (belum selesai dan masih error)
Membuat program GoLang sederhana untuk memeriksa bahasa pascal yang sebelumnya pernah saya buat di C.

#Log Rabu, 27 Juli 2016

##Memperbaiki program GoLang sederhana
Sebelumnya saya mencoba membuat program GoLang sederhana untuk memeriksa bahasa pascal yang sebelumnya pernah saya buat di C, namun karena kurangnya pemahaman dalam pembuatan project di GoLang, saya membuatnya dari awal kembali. 

##Mempelajari pembuatan project di GoLang
a. Code Organization

 - Go programmer biasanya menyimpan semua kode Go mereka di workspace tunggal .
 - Sebuah ruang workspace mengandung banyak repositori version control ( dikelola oleh Git , misalnya) .
 -  Setiap repositori berisi satu atau lebih paket .
 - Setiap package terdiri dari satu atau lebih Go file sumber dalam satu direktori .
 - Direktori dari path ke package yang menentukan jalan impor .
Catatan bahwa hal ini berbeda dari environment di pemrograman lain yang setiap proyeknya memiliki workspace yang terpisah dan workspace terikat erat dengan repositori version control. (Saya salah pengertian disini)

b. Membuat program

 - Pembuatan Workspace. Workspace adalah sebuah hirarki dengan 3 direktori pada rootnya:
	 - src
	 - pkg
	 - bin
 - Membuat library (masih mencoba)
 - Membuat package
 - Membaca suatu file
 - Hasil: Baru bisa membaca file, pembuatan packe masih error. Lihat hasil pada https://www.dropbox.com/s/w8olv5crc9gem6q/GoLang1.PNG?dl=0
 - Sumber : https://golang.org/doc/code.html

##Menginstall directori gin-gonic dan requirement directori lainnya seperti render di github

##Mencoba GoLang dengan html (sedang dalam proses)


#Log Kamis, 28 Juli 2016

##Mencoba package net/http dan simple web server

Note: Sebelumnya saya telah mencoba hal ini, hanya saja gagal, dikarenakan port yang saya gunakan ternyata telah digunakan pada Internet Information Service(IIS), setelah saya menonaktifkan IIS ini, akhirnya saya dapat menjalankan program go  tersebut, namun jika tidak ingin menonaktifkan IIS, kita bisa mengganti portnya saja.

package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hi there, I like %s!", r.URL.Path[1:])
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}

Fungsi main dimulai dengan panggilan ke http.HandleFunc, yang memberitahu http package untuk menangani semua permintaan ke web root ( "/") dengan handler.

Yang kemudian memanggil http.ListenAndServe, menentukan bahwa itu harus 'listen' pada port 8080 pada setiap interface ( ": 8080"). (Jangan khawatir tentang parameter kedua, nil, untuk saat ini.) Fungsi ini akan diblokir sampai program ini dihentikan.

Fungsi handler adalah tipe yang http.HandlerFunc. Dibutuhkan http.ResponseWriter dan http.Request sebagai argumen.

Nilai http.ResponseWriter merakit respon HTTP server; dengan menulisnya, kami mengirim data ke klien HTTP.

Sebuah http.Request adalah struktur data yang mewakili permintaan klien HTTP. r.URL.Path adalah komponen path URL request. trailing [1:] berarti "membuat sub-slice path dari karakter 1 sampai akhir." Ini menurunkan the leading "/" dari path name.

Jika Anda menjalankan program ini dan mengakses URL:

http: // localhost: 8080 / you

program akan menyajikan halaman yang berisi:

Hi there, I like you!

Lihat hasilnya pada https://www.dropbox.com/s/1h32gt6ev51xzxr/cobahttp.PNG?dl=0

menggunakan net/http untuk github page (sebenarnya seharusnya wiki page hanya saja saya ingin mengimplementasikannya di direktori github)

package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

type Page struct {
	Title string
	Body  []byte
}

func (p *Page) save() error {
	filename := p.Title + ".txt"
	return ioutil.WriteFile(filename, p.Body, 0600)
}

func loadPage(title string) (*Page, error) {
	filename := "C:\\Go\\src\\github.com\\vindafadilla\\Percobaan\\cobahttp4\\test.txt"
	body, err := ioutil.ReadFile(filename)
	if err != nil {
		return nil, err
	}
	return &Page{Title: title, Body: body}, nil
}

func viewHandler(w http.ResponseWriter, r *http.Request) {
	title := r.URL.Path[len("/view/"):]
	p, _ := loadPage(title)
	fmt.Fprintf(w, "<h1>%s</h1><div>%s</div>", p.Title, p.Body)
}

func main() {
	http.HandleFunc("/view/", viewHandler)
	http.ListenAndServe(":8080", nil)
}

Note : saya awalnya sedikit bingung disini karena read file di Go sedikit berbeda dibandingkan di C dan java. Tapi karena sebelumnya saya telah mencoba membuat scanner pascal dengan bahasa go saya sedikit terbantu.

Buatlah sebuah handler, viewHandler yang akan mengijinkan user untuk melihat github page. fungsi ini akan menangani URLs dengan prefix "/view/"

Pertama , fungsi ini mengekstrak page title dari r.URL.Path , komponen path dari URL request . Path tersebut di re-slice dengan [ len ( " / view / " ) : ] untuk menurukan the leading " / view / " komponen dari request . Hal ini karena path akan selalu dimulai dengan " / view / " , yang bukan bagian dari page's title .

Fungsi ini kemudian load page data , memformat page dengan string HTML sederhana , dan menulis ke w , http.ResponseWriter tersebut.

Sekali lagi , perhatikan penggunaan _ untuk mengabaikan error return value (nilai kembalian yang error) dari loadPage . Hal ini dilakukan di sini untuk simplicity (kesederhanan) dan pada umumnya dianggap praktik yang buruk . Kita akan memperhatikannya nanti.

Untuk menggunakan handler ini , kita menulis ulang fungsi utama kami untuk menginisialisasi http menggunakan viewHandler untuk menangani setiap permintaan di bawah path / view / .

Lalu, saya membuat page data (test.txt) yang berisi hello world.

Setelah itu saya menjalankan program tersebut dan memvisit web http://localhost:8080/view/test dan hasilnya akan tertera hello world.

Selanjutnya, saya juga membuat editing page 


Hasilnya bisa dilihat di: https://www.dropbox.com/s/58iif0f4p791uep/GoLanghttp5.PNG?dl=0
https://www.dropbox.com/s/w8csobfxod6zzl1/GoLanghttp7.PNG?dl=0
https://www.dropbox.com/s/6sr17kx7w3p1syc/GoLanghttp8.PNG?dl=0

##Mencoba html/template packege di Golang

package main

import (
	"html/template"
	"io/ioutil"
	"net/http"
)

type Page struct {
	Title string
	Body  []byte
}

func (p *Page) save() error {
	filename := p.Title + ".txt"
	return ioutil.WriteFile(filename, p.Body, 0600)
}

func loadPage(title string) (*Page, error) {
	filename := "C:\\Go\\src\\github.com\\vindafadilla\\Percobaan\\cobahttp6\\test.txt"
	body, err := ioutil.ReadFile(filename)
	if err != nil {
		return nil, err
	}
	return &Page{Title: title, Body: body}, nil
}

func renderTemplate(w http.ResponseWriter, tmpl string, p *Page) {
	t, _ := template.ParseFiles("C:\\Go\\src\\github.com\\vindafadilla\\Percobaan\\cobahttp6\\" + tmpl + ".html")
	t.Execute(w, p)
}

func viewHandler(w http.ResponseWriter, r *http.Request) {
	title := r.URL.Path[len("/view/"):]
	p, _ := loadPage(title)
	renderTemplate(w, "view", p)
}

func editHandler(w http.ResponseWriter, r *http.Request) {
	title := r.URL.Path[len("/edit/"):]
	p, err := loadPage(title)
	if err != nil {
		p = &Page{Title: title}
	}
	renderTemplate(w, "edit", p)
}

func saveHandler(w http.ResponseWriter, r *http.Request) {
    title := r.URL.Path[len("/save/"):]
    body := r.FormValue("body")
    p := &Page{Title: title, Body: []byte(body)}
    p.save()
    http.Redirect(w, r, "/view/"+title, http.StatusFound)
}

func main() {
	http.HandleFunc("/view/", viewHandler)
	http.HandleFunc("/edit/", editHandler)
	http.HandleFunc("/save/", saveHandler)
	http.ListenAndServe(":8080", nil)
}

Hasilnya bisa diliat di gambar sebelumnya.

##Mencoba ServeMux di GoLang

package main

import (
  "log"
  "net/http"
)

func main() {
  mux := http.NewServeMux()

  rh := http.RedirectHandler("http://example.org", 307)
  mux.Handle("/foo", rh)

  log.Println("Listening...")
  http.ListenAndServe(":3000", mux)
}

Hasilnya dapat dilihat di :  https://www.dropbox.com/s/qg7eg03rhywwjnn/GoLanghttp1.PNG?dl=0
https://www.dropbox.com/s/xoe4f7xg8rxyu00/GoLanghttp2.PNG?dl=0

#Jumat, 29 Juli 2016

##Membuat database dummy di MongoDB

Latihan Insert, Update, Delete. Sejauh ini masih aman, dengan kata lain belum ada masalah. 

Hasilnya:
https://www.dropbox.com/s/pbaoinvjockkpvz/MongoDBtry3.PNG?dl=0
https://www.dropbox.com/s/fdvgwb6iu6nnsvt/MongoDBtry2.PNG?dl=0
https://www.dropbox.com/s/5uvzpvo92sb76sv/MongoDBtry1.PNG?dl=0
https://www.dropbox.com/s/9j60l89upgzg6mb/MongoDBtry1_2.PNG?dl=0
https://www.dropbox.com/s/v2l6xz23wqn17y4/MongoDBtry1_3.PNG?dl=0
https://www.dropbox.com/s/yqcjfxuku96j0e6/MongoDBtry1_4.PNG?dl=0
https://www.dropbox.com/s/ty1agkdzc5gxp93/MongoDBtry4.PNG?dl=0
https://www.dropbox.com/s/u5aakpy7mnfm7u8/MongoDBtry5.PNG?dl=0
https://www.dropbox.com/s/b3m5yebdizc1t7o/MongoDBtry6.PNG?dl=0

Saya melakukannya dengan melihat step by step pada resource berikut:
https://docs.mongodb.com/manual/crud/

##Implementasi akses ke mongoDB dengan mango (mgo).

1. Install mango
dengan go get gopkg.in/mgo.v2
Untuk mengetahui berhasil atau tidaknya dapat dilihat di folder src atau pkg. Dalam kasus saya dalam folder pkg. Hanya saja karena folder saya berantakan, saya sedikit sulit menemukannya.

2. Melakukan implementasi melalui kode yang ada sebelumnya. 

package main

import (
        "fmt"
	"log"
        "gopkg.in/mgo.v2"
        "gopkg.in/mgo.v2/bson"
)

type Person struct {
        Name string
        Phone string
}

func main() {
        session, err := mgo.Dial("127.0.0.1")
        if err != nil {
                panic(err)
        }
        defer session.Close()

        // Optional. Switch the session to a monotonic behavior.
        session.SetMode(mgo.Monotonic, true)

        c := session.DB("test").C("people")
        err = c.Insert(&Person{"Ale", "+55 53 8116 9639"},
	               &Person{"Cla", "+55 53 8402 8510"})
        if err != nil {
                log.Fatal(err)
        }

        result := Person{}
        err = c.Find(bson.M{"name": "Ale"}).One(&result)
        if err != nil {
                log.Fatal(err)
        }

        fmt.Println("Phone:", result.Phone)
}

Sebelumnya pada bagian url di mgo.Dial yang terdapat pada web adalah server.example.com, lalu saya ubah menjadi localhost menyesuaikan dengan server yang ada. Sedikit error pada awalnya karena saya salah menuliskan urlnya. Tapi sejauh ini masih bisa ditangani.

3. Menjalankan program go.
menjalankan program go yang telah dituliskan di cmd dan menjalankan servernya. maka akan keluar hasilnya nomor telepon Ale. 

4. Mengecek databasenya pada mongoDB.
Saya memeriksa database yang telah diinsertkan melalui cmd mongo.exe, lalu find collection people sesuai collection yang saya insertkan pada program go.

Hasil dan prosesnya dapat dilihat di:

https://www.dropbox.com/s/1orii76zk97r70c/MangoDB.PNG?dl=0
https://www.dropbox.com/s/glbwsfncfdjqt5d/MangoDB2.PNG?dl=0
https://www.dropbox.com/s/z9jdx4okvpksocd/MangoDB3.PNG?dl=0
https://www.dropbox.com/s/xqscx3n38e4f5xv/MangoDB4.PNG?dl=0
https://www.dropbox.com/s/a9d48iaqnj64kup/MangoDB5.PNG?dl=0


##Mempelajari REST API dengan dokumen yang diberikan, melalui tool mkdocs

Pertama, saya menginstall python. Awalnya saya menginstall yang release 3, tapi karena gagal terus, maka saya menginstall release 2. Pada release 2 juga sempat gagal karena pada saat instalasi saya lupa add pada path local. Jadi harus saya install ulang kembali. Setelah berhasil diinstall ulang saya malah lupa menambahkan environment variable nya python, tapi tidak perlu install ulang lagi. Hingga akhirnya berhasil menginstall mkdocs dan mempelajari REST APIs


#Log, 1 Agustus 2016

##Mempelajari implementasi context pada gin

Source code:
package main

import (
    "net/http"
    "github.com/gin-gonic/gin"
)

func main() {
    router := gin.Default()
    router.GET("/", func(c *gin.Context) {
        c.String(http.StatusOK, "Tampilan utama page")
    })
    router.GET("/ping", func(c *gin.Context) {
        c.String(http.StatusOK, "pong")
    })
    router.POST("/submit", func(c *gin.Context) {
        c.String(http.StatusUnauthorized, "not authorized, jika tidak terauthorisasi")
    })
    router.PUT("/error", func(c *gin.Context) {
        c.String(http.StatusInternalServerError, "an error happened :( jika error")
    })
    router.Run(":8080")
}
Hasil yg telah di capture dapat dilihat pada link berikut :
https://www.dropbox.com/s/j362qlbhiqeckvp/gincoba1.PNG?dl=0
https://www.dropbox.com/s/2iikwespywg7y7r/gincoba2.PNG?dl=0
https://www.dropbox.com/s/6z6uea5il3s3yxw/gincoba3.PNG?dl=0


##Mempelajari implementasi parameter in path pada gin

URI path parameter merupakan bagian dari path segmen yang dijalankan setelah name. Path parameters menawarkan kesempatan unik untuk mengontrol representasi resource. Karena mereka tidak dapat dimanipulasi oleh bentuk-bentuk Web standar, mereka harus dibangun out of band. Karena mereka bagian dari path, mereka sekuensial, seperti query string. Yang paling penting, bagaimanapun, perilaku mereka tidak secara eksplisit didefinisikan.

Ketika mendefinisikan kendala untuk sintaks path parameter, kita bisa mengambil karakteristik ini ke account, dan menentukan parameter yang menumpuk berurutan, dan masing-masing mengambil beberapa nilai.

Spesifikasi URI menyarankan menggunakan semicolon;, equal sign = dan comma, pada tiap multiple values. Karena itu:

    semicolon; akan membatasi parameternya sendiri. Artinya, apa pun di segmen path yang berada di kanan semicolon, maka akan diperlakukan sebagai parameter baru, seperti ini: / path / nama; param1; p2; p3.
    equal sign = akan memisahkan nama parameter dari value mereka, harus parameter tertentu mendapat value. Artinya, dalam parameter path, segala sesuatu di sebelah kanan tanda sama dengan diperlakukan sebagai value, seperti ini: param = nilai; p2.
    comma, akan memisahkan value individu disahkan menjadi satu parameter, seperti ini:; param = VAL1, VAL2, val3.
    Ini berarti bahwa meskipun mungkin secara visual membingungkan, nama-nama parameter dapat mengambil comma tapi tidak ada equal sign, value dapat mengambil equal sign tapi tidak ada comma, dan tidak ada bagian dari segmen path dapat mengambil semicolon harfiah. Semua sub-pembatas lainnya harus persen-dikodekan.
    Ini juga berarti bahwa peluang seseorang untuk mengekspresikan diri dengan jalur URI lebih lanjut dibatasi.
    sumber:http://doriantaylor.com/policy/http-url-path-parameter-syntax

Parameter path dalam gin

source code:
package main
import (
	"github.com/gin-gonic/gin"
	"net/http"
)


func main() {

	router := gin.Default()
	router.GET("/user/:name", func(c *gin.Context) {
		name := c.Param("name")
		c.String(http.StatusOK, "Hello %s", name)
	})

	router.GET("/user/:name/:action", func(c *gin.Context) {
		name := c.Param("name")
		action := c.Param("action")
		message := name + " is " + action
		c.String(http.StatusOK, message)
	})

	router.Run(":8080")
}

Hasil yg telah di capture dapat dilihat pada link berikut :
https://www.dropbox.com/s/bb51j6gvfbhnfv6/gincoba4.PNG?dl=0
https://www.dropbox.com/s/6lke02bn5k71ktw/gincoba5.PNG?dl=0
https://www.dropbox.com/s/lmgb2b2by42fc5h/gincoba6.PNG?dl=0

##Mempelajari implementasi middleware pada gin
Middleware adalah software komputer yang menyediakan layanan untuk aplikasi perangkat lunak di luar yang tersedia dari sistem operasi . Hal ini dapat digambarkan sebagai " software glue"

Dalam konteks pengembangan web, "middleware" biasanya merupakan "bagian dari aplikasi yang membungkus aplikasi asli, menambahkan fungsi tambahan". Ini adalah konsep yang biasanya tampaknya agak kurang dihargai, tapi saya pikir middleware sangat bagus.

Untuk seseorang, middleware yang baik memiliki tanggung jawab tunggal, pluggable dan mandiri. Itu berarti kita dapat pasang aplikasi di tingkat antarmuka dan memilikinya hanya bekerja. Ini tidak mempengaruhi gaya coding kita, itu bukan kerangka, tetapi hanya lapisan lain dalam permintaan kita dalam menangani siklus. Tidak perlu menulis ulang source code: jika memutuskan bahwa kita ingin menggunakan middleware, kita dapat menambahkannya ke dalam persamaan, jika kita berubah pikiran, kita dapat menghapusnya. Itu dia.

Untuk Go sendiri, HTTP middleware cukup lazim, bahkan di librari standar. Meskipun mungkin tidak jelas pada awalnya, fungsi dalam paket net / http, seperti StripPrefix atau TimeoutHandler adalah persis apa yang kita didefinisikan middleware seharusnya: mereka membungkus handler Anda dan mengambil langkah-langkah tambahan ketika berhadapan dengan permintaan atau tanggapan.

Anda juga dapat menggunakan middleware untuk:

    1. Mitigasi serangan PELANGGARAN dengan length hiding
    2. Rate-limiting
   3.  Memblokir 'evil' bot
    4. Memberikan informasi debugging
    5. Menambahkan HSTS, header X-Frame-Options
    6. Memulihkan dari serangan panik
    dll

Sumber:
https://justinas.org/writing-http-middleware-in-go/
http://codereview.stackexchange.com/questions/98779/gin-web-framework-middleware

Source code:

package main

import (
  "log"
  "net/http"
)

func middlewareOne(next http.Handler) http.Handler {
  return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
    log.Println("Executing middlewareOne")
    next.ServeHTTP(w, r)
    log.Println("Executing middlewareOne again")
  })
}

func middlewareTwo(next http.Handler) http.Handler {
  return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
    log.Println("Executing middlewareTwo")
    if r.URL.Path != "/" {
      return
    }
    next.ServeHTTP(w, r)
    log.Println("Executing middlewareTwo again")
  })
}

func final(w http.ResponseWriter, r *http.Request) {
  log.Println("Executing finalHandler")
  w.Write([]byte("OK"))
}

func main() {
  finalHandler := http.HandlerFunc(final)

  http.Handle("/", middlewareOne(middlewareTwo(finalHandler)))
  http.ListenAndServe(":3000", nil)
}

Hasil yg telah di capture dapat dilihat pada link berikut :
https://www.dropbox.com/s/c2vy7lqfeokqhsp/gincoba7.PNG?dl=0
https://www.dropbox.com/s/myesmsoqi1gvobf/gincoba8.PNG?dl=0

Hasil yang lain:
https://www.dropbox.com/s/tg6v8j85u4aom0l/gincoba9.PNG?dl=0
https://www.dropbox.com/s/48s8c9utddkrg29/gincoba10.PNG?dl=0


#Log Selasa, 2 Agustus 2016

##Mempelajari REST API di go

RESTful API merupakan implementasi dari API
REST adalah singkatan dari Representational State Transfer yaitu suatu software arsitektur yang berjalan dengan teknologi WWW.
Diperkenalkan dan didefinisikan oleh Roy Fielding pada tahun 2000 dalam  desertasinya.

REST adalah salah satu jenis web service yang menerapkan konsep perpindahan antar state. State disini dapat digambarkan seperti jika browser meminta suatu halaman web, maka serverakan mengirimkan state halaman web yang sekarang ke browser. Bernavigasi melalui link-link yang disediakan sama halnya dengan mengganti state dari halaman web. Begitu pula REST bekerja, dengan bernavigasi melalui link-link HTTP untuk melakukan aktivitas tertentu, seakan-akan terjadi perpindahan state satu sama lain. Perintah HTTP yang bisa digunakan adalah fungsi GET, POST, PUT atau DELETE. Balasan yang dikirimkan adalah dalam bentuk XML sederhana tanpa ada protokol pemaketan data, sehingga informasi yang diterima lebih mudah dibaca dan diparsing disisi client.
         Dalam pengaplikasiannya, REST lebih banyak digunakan untuk web serviceyang berorientasi pada resource. Maksud orientasi pada resource adalah orientasi yang menyediakan resource-resource sebagai layanannya dan bukan kumpulan-kumpulan dari aktifitas yang mengolah resource itu.Alasan mengapa REST tidak digunakan dalam skripsi ini karena orientasi pada resourcenya itu,sedangkan aplikasi event calendar membutuhkan pemanggilan metode yang bisa dikerjakan terhadap kumpulan resource event. Selain itu, karena standarnya yang kurang sehingga tidak begitu cocok diterapkan dalam aplikasi yang membutuhkan kerjasama antar aplikasi lain, dimana standar yang baik akan sangat berguna karena berbicara dalam satu bahasa yang sama. Beberapa contoh web service yang menggunakan REST adalah: Flickr API(Application ProgramInterface), YouTube API, Amazon API.
 Prinsip Kerja:
1. Download plugin JSON API dari http://wordpress.org/extend/plugins/json-api/ atau dari plugin menu dashboard anda, setelah itu aktifkan plugin tersebut.
Masuk ke menu Settings lalu klik JSON API, makan anda akan masuk ke halaman konfigurasinya.

Di sana Anda akan melihat controller dan penjelasannya, intinya adalah:

    Posts controller, jika diaktifkan maka anda mengijinkan aplikasi client yang anda buat melakukan posting content ke blog wordpress Anda.
    Core controller, ini adalah metode-metode yang pasti dipakai oleh aplikasi client (seperti menarik data post, page, dan category).
    Respond controller, jika diaktifkan maka anda mengijinkan aplikasi client yang anda buat melakukan post comment ke blog wordpress Anda
    API base, adalah halaman yang diakses ketika requesting data dari controller-controller di atas.

3. Setelah diaktifkan sekarang saatnya kita coba, coba anda akses URL ini di browser anda http://dev.magikube.com/experiment/api/get_post/?post_id=6 (ini adalah url experiment server saya :) ). Anda akan mendapatkan hasil seperti ini.

Gambar di atas adalah hasil data yang sama jika anda membuat “the loops” pada template, hanya saja dalam format JSON. Untuk membandingkannya silahkan anda ketik <?php while(have_posts()): the_posts(); print_r($post); endwhile; ?> pada salah satu file template wordpress anda, maka anda akan mendapat hasil data yang sama.

sumber:
http://www.hafidmukhlasin.com/2015/12/08/mengenal-restful-web-service/
http://s4nbao.blogspot.co.id/2013/01/rest-api.html
http://slides.com/ferrisutanto/mengenal-restful-api#/8
http://thenewstack.io/make-a-restful-json-api-go/
https://github.com/gin-gonic/gin/blob/master/README.md
http://godoc.org/github.com/gin-gonic/gin
https://github.com/gin-gonic/contrib
https://github.com/gin-gonic/gin/blob/develop/examples/basic/main.go
https://gist.github.com/EtienneR/5eb48ae7d849cec6f55a
https://medium.com/@etiennerouzeaud/how-to-create-a-basic-restful-api-in-go-c8e032ba3181#.as3n1wikq
http://stackoverflow.com/questions/35306780/create-a-simple-restful-api-using-golang-gin-framework-and-mongodb
https://github.com/charles-haynes/angular-oauth
https://forum.golangbridge.org/t/golang-connection-to-angularjs/1434/4
https://github.com/manucorporat/sse
https://github.com/jkbrzt/httpie


Sampai saat ini saya baru mengimplementasikan gin.BasicAuth(), belum lebih jauh menggunkan RESTful API pada Go dengan framework gin-gonic. 
Untuk sementara, karena saya masih mempelajari implementasi dari REST API pada go, saya akan mencoba implementasi db yang telah di berikan pada go. 
Terimakasih.


#Log Rabu, 3 Agustus 2016

##Implementasi database

Saya menggunakan database yang diberikan untuk dapat digunakan pada web server pada golang menggunakan package mgo atau mango.

package main

import (
	"fmt"
	"log"
    
    "gopkg.in/mgo.v2"
    "gopkg.in/mgo.v2/bson"
	"github.com/gin-gonic/gin"
)

type User struct {
        Id string `json:"id" bson:"_id"`
        Pass string `json:"password" bson:"password"`
        Verified string `json:"verified" bson:"verified"`
        Challenge int `json:"challenge" bson:"challenge"`
        Key int `json:"key"  bson:"key"`
        Gcmregid string `json:"gcmregid" bson:"gcmregid"`
        Counter string `json:"counter" bson:"counter"`
        Created_at string `json:"created_at" bson:"created_at"`
        Updated_at string `json:"updated_at" bson:"updated_at"`
        Country_code string `json:"country_code" bson:"country_code"`
        Continent string `json:"continent" bson:"continent"`
}

var DB = make(map[string]string)

func main() {

	session, err := mgo.Dial("127.0.0.1")
    if err != nil {
    	panic(err)
    }
    defer session.Close()

    // Optional. Switch the session to a monotonic behavior.
    session.SetMode(mgo.Monotonic, true)

    c := session.DB("cdr-dump").C("user")
        
   results := User{}
        err = c.Find(bson.M{"_id": "+15555215554"}).One(&results)
        if err != nil {
                log.Fatal(err)
        }

        fmt.Println("Responder:", results.Id)

	r := gin.Default()

	// Ping test
	r.GET("/ping", func(c *gin.Context) {
		c.String(200, "pong")
	})

	// Get user value
	r.GET("/user/:name", func(c *gin.Context) {
		user := c.Params.ByName("name")
		value, ok := DB[user]
		if ok {
			c.JSON(200, gin.H{"user": results.Id, "value": value, "pass" : results.Pass})
		} else {
			c.JSON(200, gin.H{"user": results.Id, "status": "no value", "pass" : results.Pass})
		}
	})
	// Authorized group (uses gin.BasicAuth() middleware)
	// Same than:
	// authorized := r.Group("/")
	// authorized.Use(gin.BasicAuth(gin.Credentials{
	// "foo": "bar",
	// "manu": "123",
	//}))
	authorized := r.Group("/", gin.BasicAuth(gin.Accounts{
		"results.Id": "results.Pass", // user:foo password:bar
	}))

	authorized.POST("admin", func(c *gin.Context) {
		user := c.MustGet(gin.AuthUserKey).(string)
		// Parse JSON
		var json struct {
			Value string `json:"value" binding:"required"`
		}
		if c.Bind(&json) == nil {
			DB[user] = json.Value
			c.JSON(200, gin.H{"status": "ok"})
		}
	})
	// Listen and Server in 0.0.0.0:8080
	r.Run(":8080")
}

Hasil yg telah di capture dapat dilihat pada link berikut :
https://www.dropbox.com/s/ow2t34ywn03u32v/gincoba11.PNG?dl=0
https://www.dropbox.com/s/aeh76xc5mddt6qg/gincoba12.PNG?dl=0

##Mempelajari pembuatan RESTful di golang menggunakan jwt (JSON Web Token)

Saya mempelajarinya dengan menggunakan HTTP Basic Authentication. Didefinisikan dalam spesifikasi HTTP resmi, pada dasarnya melibatkan pengaturan header pada respon server yang menunjukkan otentikasi diperlukan. Klien harus merespon dengan melampirkan identitasnya, termasuk password mereka, untuk setiap permintaan berikutnya. Jika kredensial sesuai, informasi pengguna yang tersedia untuk aplikasi server sebagai sebagai variabel.

Pendekatan kedua sangat mirip, tetapi menggunakan mekanisme otentikasi aplikasi sendiri. Hal ini biasanya melibatkan memeriksa kredensial disediakan terhadap mereka dalam penyimpanan. Seperti HTTP Basic Authentication, ini mengharuskan kredensial pengguna yang disertakan dengan setiap panggilan.

Pendekatan ketiga adalah OAuth (atau OAuth2). Dirancang untuk sebagian besar untuk otentikasi terhadap layanan pihak ketiga, dapat lebih menantang untuk diaplikasikan, setidaknya pada server-side.

Pendekatan keempat adalah menggunakan token. Nah, inilah yang akan saya pelajari. Kita akan melihat sebuah implementasi yang memanfaatkan JavaScript pada bagian frontend dan backend.

#Log, Kamis 4 Agustus 2016

## JSON Web Token
JSON Web Token ( JWT ) adalah compact URL - safe  mewakili klaim yang akan ditransfer antara dua pihak . Klaim dalam JWT di encode sebagai objek JSON yang ditandatangani secara digital menggunakan JSON Web Signature ( JWS ) .

Sebuah JWT terdiri dari tiga komponen utama : objek header, klaim object , dan signature. Ketiga sifat di encode menggunakan base64 , kemudian digabungkan dengan periode sebagai pemisah .

JWT object claims terdiri dari informasi keamanan tentang pesannya. Contohnya:

1. iss. Is the issuer of the claim. Connect menggunakannya untuk mengidentifikasi aplikasi untuk pembuatan panggilan.
2. iat. Issued-at time. Terdiri dari UTC Unix time dimana token ini menjadi issue. Tidak ada requirement yang sulit seputar klaim ini tetapi bukan berarti hal ini akan berlaku secara signifikan setelahnya. Juga, old issued-at times bisa dikarenakan token lama yang mencurigakan.
3. sub. subjek dari token ini. Ini merupakan user yang berasosiasi dengan aksi yang relevan, dan kemungkinan tidak akan dimunculkan jika tidak log pada user.


##Otentikasi dengan JWT
JSON Web Token (JWT) merupakan pendekatan yang lebih modern untuk otentikasi. Sebagai web berubah ke pemisahan yang cukup besar antara klien dan server, JWT menyediakan alternatif yang luar biasa dibandingkan model otentikasi berorientasi cookie tradisional..

JWT menyediakan jalan untuk klien untuk mengotentikasi setiap request tanpa harus memaintain session atau secara berulang melewati login credential ke server.
 