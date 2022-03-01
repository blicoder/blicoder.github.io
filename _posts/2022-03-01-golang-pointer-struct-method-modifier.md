---
layout: post
title: Belajar Golang (Pointer, Struct, Method, Modifier)
---


## Table of Contents
- [Pointer](#pointer)
- [Struct](#struct)

## Random
#### Penggunaan Fungsi strings.Split()
```
strings.Split("ethan hunt", " ")
// ["ethan", "hunt"]
```

## A.23 Pointer <a name="pointer"></a>
Pointer adalah reference atau alamat memori. Variabel pointer berarti variabel yang berisi alamat memori suatu nilai. Sebagai contoh sebuah variabel bertipe integer memiliki nilai 4, maka yang dimaksud pointer adalah alamat memori di mana nilai 4 disimpan, bukan nilai 4 itu sendiri.

Variabel-variabel yang memiliki reference atau alamat pointer yang sama, saling berhubungan satu sama lain dan nilainya pasti sama. Ketika ada perubahan nilai, maka akan memberikan efek kepada variabel lain (yang referensi-nya sama) yaitu nilainya ikut berubah.

### A.23.1. Penerapan Pointer
```
var numberA int = 4
var numberB *int = &numberA

fmt.Println("numberA (value)   :", numberA)  // 4
fmt.Println("numberA (address) :", &numberA) // 0xc20800a220

fmt.Println("numberB (value)   :", *numberB) // 4
fmt.Println("numberB (address) :", numberB)  // 0xc20800a220
```

### A.23.3. Parameter Pointer
```
package main

import "fmt"

func main() {
    var number = 4
    fmt.Println("before :", number) // 4

    change(&number, 10)
    fmt.Println("after  :", number) // 10
}

func change(original *int, value int) {
    *original = value
}
```

## A.24. Struct <a name="struct"></a>
Struct adalah kumpulan definisi variabel (atau property) dan atau fungsi (atau method), yang dibungkus sebagai tipe data baru dengan nama tertentu. Property dalam struct, tipe datanya bisa bervariasi. Mirip seperti map, hanya saja key-nya sudah didefinisikan di awal, dan tipe data tiap itemnya bisa berbeda.

### A.24.1. Deklarasi Struct
```
type student struct {
    name string
    grade int
}
```

### A.24.2. Penerapan Struct
```
func main() {
    var s1 student
    s1.name = "john wick"
    s1.grade = 2

    fmt.Println("name  :", s1.name)
    fmt.Println("grade :", s1.grade)
}
```

### A.24.3. Inisialisasi Object Struct
```
var s1 = student{}
s1.name = "wick"
s1.grade = 2

var s2 = student{"ethan", 2}

var s3 = student{name: "jason"}

var s5 = student{grade: 2, name: "bruce"}

fmt.Println("student 1 :", s1.name)
fmt.Println("student 2 :", s2.name)
fmt.Println("student 3 :", s3.name)
```

### A.24.4. Variabel Objek Pointer
```
var s1 = student{name: "wick", grade: 2}

var s2 *student = &s1
fmt.Println("student 1, name :", s1.name)
fmt.Println("student 4, name :", s2.name)

s2.name = "ethan"
fmt.Println("student 1, name :", s1.name)
fmt.Println("student 4, name :", s2.name)
```

Meskipun s2 bukan variabel asli, property nya tetap bisa diakses seperti biasa. Inilah keistimewaan property dalam objek pointer, tanpa perlu di-dereferensi nilai asli property tetap bisa diakses.

### A.24.5. Embedded Struct
```
package main

import "fmt"

type person struct {
    name string
    age  int
}

type student struct {
    grade int
    person
}

func main() {
    var s1 = student{}
    s1.name = "wick"
    s1.age = 21
    s1.grade = 2

    fmt.Println("name  :", s1.name)
    fmt.Println("age   :", s1.age)
    fmt.Println("age   :", s1.person.age)
    fmt.Println("grade :", s1.grade)
}
```

### A.24.6. Embedded Struct Dengan Nama Property Yang Sama
```
package main

import "fmt"

type person struct {
    name string
    age  int
}

type student struct {
    person
    age   int
    grade int
}

func main() {
    var s1 = student{}
    s1.name = "wick"
    s1.age = 21        // age of student
    s1.person.age = 22 // age of person

    fmt.Println(s1.name)
    fmt.Println(s1.age)
    fmt.Println(s1.person.age)
}
```

### A.24.7. Pengisian Nilai Sub-Struct
```
var p1 = person{name: "wick", age: 21}
var s1 = student{person: p1, grade: 2}

fmt.Println("name  :", s1.name)
fmt.Println("age   :", s1.age)
fmt.Println("grade :", s1.grade)
```

### A.24.8. Anonymous Struct
Anonymous struct adalah struct yang tidak dideklarasikan di awal sebagai tipe data baru, melainkan langsung ketika pembuatan objek. Teknik ini cukup efisien untuk pembuatan variabel objek yang struct-nya hanya dipakai sekali.

```
package main

import "fmt"

type person struct {
    name string
    age  int
}

func main() {
    var s1 = struct {
        person
        grade int
    }{}
    s1.person = person{"wick", 21}
    s1.grade = 2

    fmt.Println("name  :", s1.person.name)
    fmt.Println("age   :", s1.person.age)
    fmt.Println("grade :", s1.grade)
}
```

```
// anonymous struct tanpa pengisian property
var s1 = struct {
    person
    grade int
}{}

// anonymous struct dengan pengisian property
var s2 = struct {
    person
    grade int
}{
    person: person{"wick", 21},
    grade:  2,
}
```

### A.24.9. Kombinasi Slice & Struct
```
type person struct {
    name string
    age  int
}

var allStudents = []person{
    {name: "Wick", age: 23},
    {name: "Ethan", age: 23},
    {name: "Bourne", age: 22},
}

for _, student := range allStudents {
    fmt.Println(student.name, "age is", student.age)
}
```

### A.24.10. Inisialisasi Slice Anonymous Struct
Anonymous struct bisa dijadikan sebagai tipe sebuah slice. Dan nilai awalnya juga bisa diinisialisasi langsung pada saat deklarasi.
```
var allStudents = []struct {
    person
    grade int
}{
    {person: person{"wick", 21}, grade: 2},
    {person: person{"ethan", 22}, grade: 3},
    {person: person{"bond", 21}, grade: 3},
}

for _, student := range allStudents {
    fmt.Println(student)
}
```

### A.24.11. Deklarasi Anonymous Struct Menggunakan Keyword var
```
var student struct {
    person
    grade int
}

student.person = person{"wick", 21}
student.grade = 2
```

Statement type student struct adalah contoh cara deklarasi struct. Maknanya akan berbeda ketika keyword type diganti var, seperti pada contoh di atas var student struct, yang artinya dicetak sebuah objek dari anonymous struct kemudian disimpan pada variabel bernama student.

```
// hanya deklarasi
var student struct {
    grade int
}

// deklarasi sekaligus inisialisasi
var student = struct {
    grade int
} {
    12,
}
```

### A.24.12. Nested struct
```
type student struct {
    person struct {
        name string
        age  int
    }
    grade   int
    hobbies []string
}
```

### A.24.13. Deklarasi Dan Inisialisasi Struct Secara Horizontal
```
type person struct { name string; age int; hobbies []string }
```

```
var p1 = struct { name string; age int } { age: 22, name: "wick" }
var p2 = struct { name string; age int } { "ethan", 23 }
```

### A.24.14. Tag property dalam struct
Tag merupakan informasi opsional yang bisa ditambahkan pada masing-masing property struct.

```
type person struct {
    name string `tag1`
    age  int    `tag2`
}
```

Tag biasa dimanfaatkan untuk keperluan encode/decode data json. Informasi tag juga bisa diakses lewat reflect. Nantinya akan ada pembahasan yang lebih detail mengenai pemanfaatan tag dalam struct, terutama ketika sudah masuk chapter JSON.

### A.24.15. Type Alias
Sebuah tipe data, seperti struct, bisa dibuatkan alias baru, caranya dengan type NamaAlias = TargetStruct. 

```
type Person struct {
    name string
    age  int
}
type People = Person

var p1 = Person{"wick", 21}
fmt.Println(p1)

var p2 = People{"wick", 21}
fmt.Println(p2)
```

Casting dari objek (yang dicetak lewat struct tertentu) ke tipe yang merupakan alias dari struct pencetak, hasilnya selalu valid. Berlaku juga sebaliknya.

```
people := People{"wick", 21}
fmt.Println(Person(people))

person := Person{"wick", 21}
fmt.Println(People(person))
```

Pembuatan struct baru juga bisa dilakukan lewat teknik type alias.

```
type People1 struct {
    name string
    age  int
}
type People2 = struct {
    name string
    age  int
}
```


## A.25. Method
Method adalah fungsi yang menempel pada type (bisa struct atau tipe data lainnya). Method bisa diakses lewat variabel objek.

### A.25.1. Penerapan Method
```
package main

import "fmt"
import "strings"

type student struct {
    name  string
    grade int
}

func (s student) sayHello() {
    fmt.Println("halo", s.name)
}

func (s student) getNameAt(i int) string {
    return strings.Split(s.name, " ")[i-1]
}

func main() {
    var s1 = student{"john wick", 21}
    s1.sayHello()

    var name = s1.getNameAt(2)
    fmt.Println("nama panggilan :", name)
}
```

### A.25.2. Method Pointer
Method pointer adalah method yang variabel objek pemilik method tersebut berupa pointer.

Kelebihan method jenis ini adalah, ketika kita melakukan manipulasi nilai pada property lain yang masih satu struct, nilai pada property tersebut akan di rubah pada reference nya.

```
package main

import "fmt"

type student struct {
    name  string
    grade int
}

func (s student) changeName1(name string) {
    fmt.Println("---> on changeName1, name changed to", name)
    s.name = name
}

func (s *student) changeName2(name string) {
    fmt.Println("---> on changeName2, name changed to", name)
    s.name = name
}

func main() {
    var s1 = student{"john wick", 21}
    fmt.Println("s1 before", s1.name)
    // john wick

    s1.changeName1("jason bourne")
    fmt.Println("s1 after changeName1", s1.name)
    // john wick

    s1.changeName2("ethan hunt")
    fmt.Println("s1 after changeName2", s1.name)
    // ethan hunt
}
```

Keistimewaan lain method pointer adalah, method itu sendiri bisa dipanggil dari objek pointer maupun objek biasa.

```
// pengaksesan method dari variabel objek biasa
var s1 = student{"john wick", 21}
s1.sayHello()

// pengaksesan method dari variabel objek pointer
var s2 = &student{"ethan hunt", 22}
s2.sayHello()
```

## A.26. Properti Public dan Private (Exported vs Unexported)
Chapter ini membahas mengenai property modifier public dan private dalam Go. Kapan sebuah struct, fungsi, atau method bisa diakses dari package lain dan kapan tidak.

Di Go sebenarnya tidak ada istilah public modifier dan private modifier. Yang ada adalah exported yang kalau di bahasa lain ekuivalen dengan public modifier, dan unexported untuk private modifier.

### A.26.2. Exported Package dan Unexported Package
Di Go, setiap folder atau sub-folder adalah satu package, file-file yang ada di dalam sebuah folder package-nya harus sama. Dan package pada file-file tersebut harus berbeda dengan package pada file-file lainnya yang berada pada folder berbeda.

Jadi mudahnya, 1 folder adalah 1 package.


Ada 2 jenis hak akses di Go:

- Hak akses Exported atau public. Menandakan komponen tersebut diperbolehkan untuk diakses dari package lain yang berbeda
- Hak akses Unexported atau private. Berarti komponen hanya bisa diakses dalam package yang sama, bisa dalam satu file saja atau dalam beberapa file yang masih 1 folder.

Di Go cara menentukan level akses atau modifier sangat mudah, penandanya adalah character case huruf pertama nama fungsi, struct, variabel, atau lainnya. Ketika namanya diawali dengan huruf kapital menandakan kalau exported (atau public). Dan sebaliknya, jika diawali huruf kecil, berarti unexported (atau private).

### A.26.4. Penggunaan Hak Akses Exported dan Unexported pada Struct dan Propertinya
Level akses exported (atau public) dan unexported (atau private) juga bisa diterapkan di fungsi, struct, method, maupun property variabel. Cara penggunaannya sama seperti pada pembahasan sebelumnya, yaitu dengan menentukan character case huruf pertama nama komponen, apakah huruf besar atau kecil.

### A.26.5. Import Dengan Prefix Tanda Titik
Di Go, komponen yang berada di package lain yang di-import bisa dijadikan se-level dengan komponen package peng-import, caranya dengan menambahkan tanda titik (.) setelah penulisan keyword import. Maksud dari se-level di sini adalah, semua properti di package lain yg di-import bisa diakses tanpa perlu menuliskan nama package, seperti ketika mengakses sesuatu dari file yang sama.

```
import (
    . "belajar-golang-level-akses/library"
    "fmt"
)

func main() {
    var s1 = Student{"ethan", 21}
    fmt.Println("name ", s1.Name)
    fmt.Println("grade", s1.Grade)
}
```

### A.26.6. Pemanfaatan Alias Ketika Import Package
Fungsi yang berada di package lain bisa diakses dengan cara menuliskan nama-package diikuti nama fungsi-nya, contohnya seperti fmt.Println(). Package yang sudah di-import tersebut bisa diubah namanya dengan cara menggunakan alias pada saat import. 

```
import (
    f "fmt"
)

func main() {
    f.Println("Hello World!")
}
```

### A.26.7. Mengakses Properti Dalam File Yang Package-nya Sama
Sekarang terdapat 2 file berbeda (main.go dan partial.go) dengan package adalah sama, main. Pada saat go build atau go run, semua file dengan nama package main harus dituliskan sebagai argumen command.

```
go run main.go partial.go
```

Cara lain untuk menjalankan program bisa dengan perintah go run *.go, dengan cara ini tidak perlu menuliskan nama file nya satu per satu.

### A.26.7.1. Fungsi init()
Selain fungsi main(), terdapat juga fungsi spesial, yaitu init(). Fungsi ini otomatis dipanggil pertama kali ketika aplikasi di-run. Jika fungsi ini berada dalam package main, maka dipanggil lebih dulu sebelum fungsi main() dieksekusi.
```
package library

import "fmt"

var Student = struct {
    Name  string
    Grade int
}{}

func init() {
    Student.Name = "John Wick"
    Student.Grade = 2

    fmt.Println("--> library/library.go imported")
}
```

Dalam sebuah package diperbolehkan ada banyak fungsi init() (urutan eksekusinya adalah sesuai file mana yg terlebih dahulu digunakan). Fungsi ini dipanggil sebelum fungsi main(), pada saat eksekusi program.