# Instalasi dan Inisiasi Database PostgreSQL

PostgreSQL merupakan database relasional yang dapat digunakan untuk transaksi operasional maupun sebagai data warehouse. PostgreSQL juga memiliki support yang sangat baik untuk data spasial melalui plugin PostGIS.

1. Buka [https://www.postgresql.org/download/windows/](https://www.postgresql.org/download/windows/)
2. Download installernya [https://www.enterprisedb.com/downloads/postgres-postgresql-downloads](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads) PostgreSQL versi 14
3. Lakukan proses instalasi dan inisiasi database [https://www.postgresqltutorial.com/postgresql-getting-started/install-postgresql/](https://www.postgresqltutorial.com/postgresql-getting-started/install-postgresql/)

# Instalasi Dbeaver

Dbeaver merupakan tools untuk jelajah berbagai macam database. Kali ini kita akan gunakan Dbeaver untuk jelajah PostgreSQL yang telah diinstall.

1. Buka [https://dbeaver.io/download/](https://dbeaver.io/download/)
2. Download installernya [https://dbeaver.io/files/dbeaver-ce-latest-x86_64-setup.exe](https://dbeaver.io/files/dbeaver-ce-latest-x86_64-setup.exe)

# Instalasi Node-Postgres

Node-Postgres merupakan library NodeJS untuk mengakses dan mengelola PostgreSQL.

1. Masuk ke project NodeJS yang sudah teman-teman buat
2. Instalasi Node-Postgres dengan cara
```sh
npm install pg
```
3. Ikuti tutorial penggunaan Node-Postgres di [https://node-postgres.com/](https://node-postgres.com/)

# Akses PostgreSQL dari Aplikasi ExpressJS
```nodejs
const express = require('express')
const cors = require('cors')

const app = express()
const port = 3000

connectionSettings = {
    user: 'postgres',
    host: 'localhost',
    database: 'postgres',
    password: 'uinsgd',
    port: 5444,
}

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
