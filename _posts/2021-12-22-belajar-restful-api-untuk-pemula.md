---
layout: post
title: Belajar RESTful API Untuk Pemula
---

##Integrasi Aplikasi
- Empat cara integrasi antar aplikasi, yaitu: file sharing, database sharing, remote procedure invocation, messaging
- **File Sharing** merupakan integrasi aplikasi dengan cara berbagai file. Biasanya aplikasi yang memiliki data akan membuat file (excel, csv, text, json) dan aplikasi yang membutuhkan data akan membaca data tersebut dari file
- **Database Sharing** merupakan integrasi antar aplikasi yang memanfaatkan database untuk berbagi data. Aplikasi hanya perlu menyimpan data ke database, dan secara otomatis aplikasi lain bisa membaca data tersebut dari database secara langsung
- **Remote Procedure Invocation** merupakan mekanisme integrasi antar aplikasi dengan cara membuat API yang bisa digunakan oleh aplikasi lain. Aplikasi yang memiliki data akan membuat API dan aplikasi yang membutuhkan akan menggunakan API tersebut untuk mendapatkan data dari aplikasi tersebut
- **Messaging** merupakan cara integrasi aplikasi yang memanfaatkan aplikasi message broker atau message bus. Aplikasi yang memiliki data akan mengirim data ke aplikasi message broker, dan aplikasi yang membutuhkan data akan mengambil data dari message broker.

##Pengenalan API
- API (Application Programming Interface) merupakan perantara yang menghubungkan satu pihak dengan pihak lain agar bisa saling berkomunikasi. API berisi kumpulan prosedur, fungsi, cara berkomunikasi atau peralatan untuk komunikasi. Pihak yang terlibat dalam API bisa dalam bentuk perangkat lunak ataupun perangkat keras.
- Contoh penggunaan API: Saat kita menggunakan sistem operasi, sistem operasi tidak bisa langsung berkomunikasi dengan perangkat keras bisa terdeteksi oleh sistem operasi. Saat kita ingin berkomunikasi dengan aplikasi Facebook, kita membutuhkan API dari Facebook agar aplikasi kita bisa berinteraksi dengan aplikasi Facebook.
- Contoh implementasi API: driver perangkat keras (sebagai API untuk sistem operasi), SOAP (Simple Object Access Protocol), CORBA (Common Object Request Broker Architecture), RESTful API, Apache Thrift, Protocol Buffer, GRPC, dll

##Pengenalan RESTful API
- REST (REpresentational State Transfer) merupakan salah satu implementasi API yang memanfaatkan HTTP sebagai protokol komunikasinya.
- Client -> Web Server (RESTful API, DB)

##Architectural Constraints
- REST di desain berjalan menggunakan HTTP dan sering digunakan sebagai web services
- Beberapa design principal agar web services benar-benar sesuai dengan RESTful API yaitu: client-server, stateless, cacheable, uniform interface, layered system, code on demand
- Pada Client Server, RESTful API haruslah memisahkan antara kompleksitas data internal dengan yang akan diekspose ke client, sehingga Client tidak perlu tahu kompleksitas logic yang terjadi di Server
- Pada Stateless, tiap interaksi harus tidak tergantung dengan interaksi sebelumnya atau setelahnya, sehingga mudah untuk di scaling
- Pada Cachable, bisa melakukan cache data di local, sehingga tidak perlu selalu meminta data terbaru dari Server
- Pada Uniform Interface, penggunaan antarmuka komunikasi yang seragam untuk semua pihak (client, server teknologi apapu)
- Pada Layered System menjadikan sistem bisa disusun sesuai dengan datanya, dan agar kompleksitas pada RESTful API tidak harus diketahui oleh Client.
- Code on Demand, memperbolehkan mengembalikan script yang bisa diekskusi oleh client jika diperlukan

##Resource Naming
- Resource adalah data yang sifatnya bisa satu atau banyak
- Gunakan kata benda, bukan kata kerja. Misal: **/products**
- Gunakan hirarki. Misal **/products/{productId}/images**
- Gunakan Action Pada Resource. Misal: **/users/forget-password**
- Gunakan dash dan lowercase
- Gunakan HTTP Method pada CRUD
- Gunakan query untuk filter


##Content Negotiation
- RESTful API akan menggunakan standard HTTP Header: Accept dan Content-Type
- Accept digunakan untuk memberitahu server tentang tipe data yang diterima oleh Client
- Content-Type digunakan untuk memberi tahu Server, tipe data apa yang dikirim oleh Client
- Contoh Standard:
```
{
 "took": 123, //brp ms
 "status": "OK",
 "data": {
   "name": "Diva"
 },
 "errors": null
}

{
 "took": 123, //brp ms
 "status": "ValidationError",
 "data": null,
 "errors": {
   "name": "is not blank"
 }
}
```

##Caching
- Cache adalah data bersifat sementara yang disimpan pada sistem penyimpanan
- Data cache biasanya disimpan di client

##Idempotent
- Idempotent, ketika membuat multiple request yang identik, harus memiliki efek yang sama seperti membuat satu request

##Security
- Authentication: memvalidasi kredensial untuk memverifikasi pemilik identitas (login)
- Authorization: memvalidasi hak akses untuk mengakses 
- Contoh Auth: basic auth, api-key, oauth 2, dll

##HATEOAS
- HATEOS (Hypermedia as the Engine of Application State)
- Hypermedia artinya content yang memiliki link menuju resource yang ada
```
{
  "id": 1,
  "name": "Diva",
  "_links": {
    "self": "/users/1"
  }
}
```
- Client bisa secara dinamis mendapatkan URL lokasi resource dari response data Server

##Development

| Kesalahan ketika membuat RESTful API |
|-|
| Selalu membuat CRUD API untuk table di database |
| Membuat response data sama dengan table di database |
| Membuat API terlebih dahulu, baru mengerjakan WEb menggunakan API yang sudah dibuat |
| Mengembalikan data selengkap-lengkapnya di API |
| Membuat API yang tidak dibutuhkan oleh Client |

- Tahapan membuat RESTful API
Business Flow -> UI/UX Screen -> API Documentation -> Develop RESTful API

##Maintenance
| Maintenance yang boleh dilakukan |
|-|
| Menambah data baru di API yang sudah ada |
| Menambah API baru di endpoint URL berbeda |
| Mempercepat proses di API yang sudah ada |
| Menggabungkan beberapa API menjadi satu, tanpa menghilangkan API lama |

| Maintenance yang tidak boleh dilakukan |
|-|
| Mengubah total response data di API yang sudah ada |
| Mengubah field response data di API yang sudah ada |
| Menghilangkan API yang sudah ada |
| Men-split API yang sudah ada menjadi dua atau lebih |
| Menggabungkan beberapa API menjadi satu dengan menghapus API lama |
