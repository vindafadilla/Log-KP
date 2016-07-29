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
