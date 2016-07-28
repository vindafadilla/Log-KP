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

##Mendownload directori gin-gonic dan requirement directori lainnya seperti render di github

##Mencoba GoLang dengan html (sedang dalam proses)

#Log Kamis, 28 Juli 2016