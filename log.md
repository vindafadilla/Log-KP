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
