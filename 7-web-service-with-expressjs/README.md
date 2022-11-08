# Membuat Web Service Dengan Express JS

## Web Service dan RESTful API
- Q: Wah, sepertinya menarik. Apa tuh Web Service ?
- A: Web Service itu gerbang data yang terhubung dengan penyimpanan maupun komputasi di server untuk diakses langsung oleh bahasa pemrograman
- Q: Hmm, jadi konsumennya itu bahasa pemrograman ya ?
- A: Iya, kalo koran Tribun kan konsumennya orang, dibaca orang, web service pembaca utamanya bahasa kayak Javascript, Java, Ruby, Go, dsb.
- Q: Ohh IC IC, trus emang bisa ngapain aja pake Web Service ?
- A: Ya,, kamu bisa request kesitu, misalnya menggunakan HTTP REQUEST, nambah mobil POST /mobil, beli beras POST /belanjaan, liat list buah GET /buah, dsb.
- Q: Ohh gitu,, hmm,, itu cuma bisa pake HTTP ?
- A: Bisa pake yang lain juga kok kayak RPC, dan lain2 (browsing weh :D)
- Q: Oke2, wkwkwk. Trus apa tuh RESTful API itu ?
- A: Standar format web service HTTP berbasis [REST](https://glints.com/id/lowongan/rest-adalah/) dengan url yang merepresentasikan objek (bukan perintah). Misal, kalo mau beli makanan, ga pake url POST /beli-makanan, tapi pake url POST /pembelian, dan GET /pembelian ketika ingin lihat kita sudah belanja apa aja.

## Instalasi Express JS
- Q: Oke2, trus apa hubungannya dengan praktikum kali ini ?
- A: Ya, kita bikin RESTful API menggunakan Express JS, framework Javacsript yang bisa dipakai untuk bikin web service (untuk mesin), maupun bikin web page (untuk orang)
- Q: Hmm, diinstall pake NPM ?
- A: Yoi, langsung aja dipraktekkan ya, sebelum install express, kita install dulu **nodemon**, **nodemon** ini dipake untuk eksekusi file javascript, mirip ama **node**, bedanya **nodemon** mantau perubahan filenya, dan auto restart kalo filenya diubah. Jadi ga usah repot stop start stop start kalo beres edit
```javascript
npm install -g nodemon  
```
- A: Diinstall nya pake tanda -g artinya global, diinstall disekomputereun. Agar dapat dipakai dari project2 lainnya
- A: Selanjutnya, dari terminal / command line, masuk ke folder tempat kamu akan bikin projectnya misal
```sh
cd naufal/praktikum/pertemuan-7
```
- A: Lalu, inisiasi project Node di dalam folder tersebut dengan perintah
```sh
npm init
```
- A: Setelah inisiasi project Node selesai, kita install package Express JS, bareng dengan package tetangganya yang namanya cors yang memudahkan web service kamu diakses dari mana aja
```javascript
npm install cors express
```

## Membuat File Inisiasi Aplikasi Express JS
- A: Buat file dengan nama **app.js** di dalam folder project tersebut, lalu isi dengan
```javascript
const express = require('express')
const cors = require('cors')
const app = express()
const port = 3000

app.use(cors({
    origin: '*'
}));

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```
- A: Jika sudah disave, selanjutnya kita jalankan Express JS nya via terminal dengan perintah
```sh
nodemon app.js
```

## Membuat Route RESTful API Sesuai Project Mandiri Temen-Temen
- A: Misal untuk aplikasi baca n rating buku
```javascript

// Mengimpor objek express ke variabel express
const express = require('express')

// Mengimpor objek cors ke variabel cors
const cors = require('cors')

// Inisiasi objek aplikasi express ke variabel app
const app = express()

// Port web service
const port = 3000

// Konfigurasi CORS yang mengizinkan halaman diakses oleh semua sumber
app.use(cors({
    origin: '*'
}));

// Lihat list buku
app.get('/buku', (req, res) => {
  res.json([
    {
      nama: "Harry Potter",
      halaman: 320,
    },
    {
      nama: "The Lord of The Rings",
      halaman: 532,
    }    
  ])
})

// Lihat detail buku
app.get('/buku/:id', (req, res) => {
  res.json(
    {
      nama: "Harry Potter",
      halaman: 320,
    }
  )
})

// Tambah buku
app.post('/buku', (req, res) => {
  res.json(
    {
      id: 32432,
      nama: "Harry Potter",
      halaman: 320,
    }
  )
})

// Hapus buku
app.delete('/buku/:id', (req, res) => {
  res.json(
    {
      id: 32432,
      nama: "Harry Potter",
      halaman: 320,
    }
  )
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

## Contoh RESTful API Project Rute Angkutan nya Umar

### Docker Run PostgreSQL nya
```sh
docker run --name expressjs-pg -e POSTGRES_PASSWORD=uinsgd -p 5432:5432 postgres
```

### Data

#### Inisiasi Database
```sql
CREATE DATABASE rute_angkutan;
```

#### Inisiasi Schema
```sql
CREATE SCHEMA app;
CREATE SCHEMA data_analytics;
```

#### Inisiasi Table
```sql
CREATE TABLE app.pemberhentian (
	id varchar(36) NOT NULL,
	nama varchar(40) NOT NULL,
	alamat varchar(240) NULL,
	kategori int2 NOT NULL,
	CONSTRAINT pemberhentian_pk PRIMARY KEY (id)
);
```

### Script app.js nya
Konfigurasi koneksi masih di file, lebih baik nanti disimpan di luar file, contoh di file lain atau di environment variable yang tidak masuk Git

```javascript
const express = require('express')
const cors = require('cors')
const { Client } = require("pg")
const { connectionString } = require('pg/lib/defaults')

const app = express()
const port = 3000

connectionSettings = {
  user: 'postgres',
  host: 'localhost',
  database: 'rute_angkutan',
  password: 'uinsgd',
  port: 5432,
}

app.use(cors({
    origin: '*'
}));

app.get('/', (objekRequest, objekResponse) => {

  objekResponse.send('Hello World!')
})

app.get('/terminal', (objekRequest, objekResponse) => {

  // Inisiasi database client menggunakan konfigurasi koneksi
  const client = new Client(connectionSettings)

  client.connect(kesalahan => {
    if(kesalahan) throw kesalahan 
    console.log("Koneksi berhasil")
  })

  // Method query(p1, p2) punya 2 parameter
  // P1 atau parameter 1, isinya string bahasa SQL yang mau dieksekusi
  // P2 atau parameter 2, isinya function yang punya dua parameter, p1: eror dan p2: hasil dari eksekusi query
  client.query(`
    select 
      p.id,
      p.nama,
      p.alamat,
      p.kategori
    from 
    app.pemberhentian p
  `, (errorDariDatabase, hasilDariDatabase) => {

    console.log(hasilDariDatabase)
    // Method json(p1) dari objek response, berfungsi menampilkan HTTP Response dengan format JSON
    objekResponse.json({
      data: hasilDariDatabase.rows,
    })
  })

})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})

```
