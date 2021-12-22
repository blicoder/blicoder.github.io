---
layout: post
title: Belajar HTTP Untuk Pemula
---

#HTTP (Hypertext Transfer Protocol)


##Pengenalan HTTP
---
- HTTP merupakan protokol untuk melakukan transmisi (pengiriman dari satu tempat ke tempat lain) hypermedia document, seperti HTML, JS, CSS, Image, Audio, Video, dan lain-lain.
---
- HTTP mengikuti arsitektur client dan server
- Client mengirimkan HTTP Request untuk atau mengirim informasi ke server, lalu server membalasnya dengn HTTP Response
---
- HTTP merupakan protokol yang stateless
- Tiap HTTP Request merupakan request yang independen, tidak ada keterkaitan atau hubungan dengan HTTP Request sebelum atau setelahnya


##HTTP Terminology (Istilah, Teknologi)
---
- Web browser merupakan aplikasi untuk mengakses web menggunakan protokol HTTP
- TCP (Transmission Control Protocol) merupakan salah satu protokol dalam jaringan komputer. HTTP menggunakan TCP
- IP (Internet Protocol) merupakan identitas komputer di jaringan
- URL (Uniform Resource Locator) merupakan alamat dari sebuah resource di Web
- DNS (Domain Name Server) merupakan tempat yang berisi data katalog pemetaan antara nama domain di URL menuju lokasi IP komputer
- Web Server merupakan aplikasi yang berjalan di jaringan internet yang bertugas sebagai server. Web Server akan menerima request dari client, dan membalas request tersebut berupa informasi yang diminta client.

##HTTP Flow
- Client akan mengirimkan request dan server akan menerima request dan membalas dengan response
- Server merupakan sebuah komputer, dimana semua informasi disimpan pada komputer tersebut. Komputer server biasanya menjalankan aplikasi web server agar bisa menerima protocol HTTP
- Server (Web server, Data)
- Client merupakan komputer yang bertugas mengirim HTTP Request ke komputer server menggunakan aplikasi Web Browser
- Client (Web browser, dll)


##HTTP Message
- HTTP Request dan HTTP Response merupakan sebuah HTTP Message
- HTTP Message memiliki standarisasi format
- HTTP Message untuk Request
**Start Line** (POST /login HTTP/1.1)
**Header** (Host: example.com ...)
**Space**
**Body** ({"password": "rahasia", "username": "divakrishnam"})
- HTTP Message untuk Response
**Start Line** (HTTP/1.1 200)
**Header** (Set-Cookie: xxx ...)
**Space**
**Body** ({"status": "OK", "code": "200"})

##HTTP Method
- HTTP Method mirip seperti kategori request
- Jenis HTTP Method

| HTTP Method | Keterangan |
| - | - |
| GET | melakukan request data (hanya menerima data) |
| HEAD | melakukan request data tanpa membutuhkan response body |
| POST | mengirim data baru sehingga biasanya memiliki request body |
| PUT | mengganti semua data dengan data baru |
| DELETE | menghapus data |
| PATCH | mengubah sebagian data |
| OPTIONS | mendeskripsi opsi komunikasi yang tersedia |
| TRACE | request method untuk debugging |


##URL
- URL (Uniform Resource Locator) merupakan alamat dari sebuah resource di web
- Schema merupakan bagian awal di URL yang mengindikasikan protocol yang perlu digunakan oleh client (http, https)
**http**:\\\www.example.com:80/path
- Authority terdiri dari nama domain dan nomor port
http:\\\\**www.example.com**:**80**/path
- Path (tidak wajib) berisikan informasi menuju ke resource yang kita tuju http:\\\\www.example.com:80/**path**
- Parameters (tidak wajib) merupakan informasi tambahan yang berisi key=value, jika lebih dari satu parameter bisa ditambahkan karakter & http:\\\\www.example.com:80/path?key1=value1&key2=value2
- Anchor (tidak wajib) merupakan representasi bookmark dalam sebuah halaman website http:\\\\www.example.com:80/path#SomewhereInTheDocument

##HTTP Header
- HTTP Header merupakan informasi tambahan yang biasa dikirim di request atau response
- HTTP Header berisi key: value
- Contoh HTTP Header

| HTTP Header | Keterangan |
| - | - |
| Host | authority pada url |
| Content-Type | tipe data dari HTTP Body (text, video, image) |
| User-Agent | informasi user agent (seperti browser dan sistem informasi) |
| Accept | tipe data yang diterima client |
| Authorization | credential untuk authentikasi |

##HTTP Status
- HTTP Status merupakan kode HTTP Response yang mengindikasikan apakah sebuah request yang diterima Server sukses, gagal, atau ada hal lain


##HTTP Body
- HTTP Body merupakan data yang dikirim di HTTP Request, atau data yang diterima dari HTTP Response 


##Redirect
- Memaksa client melakukan redirect ke halaman lain, biasanya di Header ditambahkan Location: /dashboard

##HTTP Cookie
- HTTP Cookie merupakan informasi yang diberikan oleh server, dan client secara otomatis akan menyimpan data tersebut
- Ketika web browser melakukan request selanjutnya, maka web browser akan menyisipkan cookie yang sudah diterima di request sebelumnya
- Dari cookie tersebut, server nantinya bisa mengetahui apakah request tersebut merupakan request client yang telah login atau belum
- Informasi cookie yang diberikan dari server ditempatkan pada Header dengan value Set-Cookie
- Cookie bisa lebih dari satu, jika server memberikan lebih dari satu cookie, bisa menggunakan beberapa key Set-Cookie di Header

##HTTP Caching
- Menyimpan data di client sampai batas waktu yang sudah ditentukan, sehingga jika client ingin melakukan request resource yang sama, cukup ambil resourcenya di client tanpa harus meminta ulang ke server
- Cocok dilakukan untuk resource file static yang jarang berubah, seperti file, gambar, audio, video, dan lain-lain
- Tambahkan Cache-Control di Header