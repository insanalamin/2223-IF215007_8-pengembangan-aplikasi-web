# File & Folder Mode and Ownership

## File & Folder Mode

Lihat dalam folder saat ini ada file dan folder apa saja
```sh
ls -l
```

Lalu lihat di sebelah kanan dari tiap file
```sh
---------- ini menggambarkan permission / ijin dari file tersebut

-rw-r--r-- 1 insan insan 0 Nov 24 04:49 brankas

Karakter ke 1 : jenis filenya
Karakter 2 - 4 : ijin untuk pemilik file (2 Read, 3 Write, 4 Execute)
Karakter 5 - 7 : ijin untuk grup (5 Read, 6 Write, 7 Execute)
Karakter 8 - 10 : ijin untuk seluruh pengguna (8 Read, 9 Write, 10 Execute)

Dari karakter ke 2 - 10:
  tanda - artinya tidak diijinkan
  tanda r / w / x artinya diijinkan Read / Write / Execute
```

Urutan Karakter | Tidak Diijinkan | Diijinkan | Deskripsi
--- | --- | --- | ---
1 | | | Tipe file
2 | - | r | Pemilik diijinkan Read
3 | - | w | Pemilik diijinkan Write
4 | - | x | Pemilik diijinkan Executer
5 | - | r | Grup diijinkan Read
6 | - | w | Grup diijinkan Write
7 | - | x | Grup diijinkan Executer
8 | - | r | Dunia diijinkan Read
9 | - | w | Dunia diijinkan Write
10 | - | x | Dunia diijinkan Executer


```sh
chmod 000 ./nama-file
```

### chmod angka
Urutan Angka | User
--- | --- 
1 | Pemilik
2 | Grup
3 | World

Mode | Deskripsi | Nilai Angka
--- | --- | ---
Read | Membaca isi file | 4
Write | Menulis isi file | 2
Execute | Menjalankan / mengeksekusi perintah-perintah di dalam file | 1


## File & Folder Ownership
