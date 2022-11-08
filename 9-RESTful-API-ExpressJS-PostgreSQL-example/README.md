# Contoh RESTful API Project Rute Angkutan nya Umar

## Docker Run PostgreSQL nya
```sh
docker run --name expressjs-pg -e POSTGRES_PASSWORD=uinsgd -p 5432:5432 postgres
```

## Data

### Inisiasi Database
```sql
CREATE DATABASE rute_angkutan;
```

### Inisiasi Schema
```sql
CREATE SCHEMA app;
CREATE SCHEMA data_analytics;
```

### Inisiasi Table
```sql
CREATE TABLE app.pemberhentian (
	id varchar(36) NOT NULL,
	nama varchar(40) NOT NULL,
	alamat varchar(240) NULL,
	kategori int2 NOT NULL,
	CONSTRAINT pemberhentian_pk PRIMARY KEY (id)
);
```

## Script app.js nya
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
