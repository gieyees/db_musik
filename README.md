# 🎵 Music Database System (SQL Joins Exploration)

Proyek ini berisi dokumentasi langkah-langkah pembuatan database `db_musik` menggunakan **MariaDB** di lingkungan **XAMPP**. Proyek ini mencakup pembuatan tabel, relasi *foreign key*, operasi *CRUD* dasar, serta implementasi berbagai jenis `JOIN`.

**Server**: MariaDB via XAMPP 
**Database Name**: `db_musik`

## 🏗️ Struktur Tabel

Database terdiri dari dua tabel utama dengan relasi *One-to-Many* (Satu artis dapat memiliki banyak lagu).

### 1. Tabel `tb_artis`
Menyimpan informasi identitas musisi.
* `id_artis`: Primary Key (Auto Increment).
* `nama_artis`: Nama penyanyi atau grup band.

### 2. Tabel `tb_lagu`
Menyimpan daftar karya musik yang terelasi ke tabel artis.
* `id_lagu`: Primary Key (Auto Increment).
* `judul_lagu`: Judul lagu.
* `id_artis`: **Foreign Key** yang merujuk pada `tb_artis(id_artis)`.

---

## 📊 Eksperimen Query

### ⚡ LANGKAH 1 — Membuat Database
Tujuan: Membuat wadah untuk menyimpan tabel artis dan lagu.
```sql
-- Query Membuat Databas
CREATE DATABASE db_musik;

--  Query Menggunakan Database
USE db_musik;
```
### ⚡ LANGKAH 2 — Membuat Tabel Artis
Tujuan: Menyimpan data penyanyi atau band.
```sql
CREATE TABLE tb_artis (
    id_artis INT PRIMARY KEY AUTO_INCREMENT,
    nama_artis VARCHAR(50)
);
```
### ⚡ LANGKAH 3 — Membuat Tabel Lagu
Tujuan: Menyimpan lagu yang terhubung ke artis.
```sql
CREATE TABLE tb_lagu(
    id_lagu INT PRIMARY KEY AUTO_INCREMENT,
    judul_lagu VARCHAR(50),
    id_artis INT,
    FOREIGN KEY (id_artis) REFERENCES tb_artis(id_artis)
);
```
### ⚡ LANGKAH 4 — Mengisi Data Artis
Tujuan: Menambahkan data contoh.
```sql
INSERT INTO tb_artis
    -> (id_artis, nama_artis) values
    -> ('', 'Avril Lavigne');
    -> ('', 'One Direction'),
    -> ('', 'The Goo Goo Dolls'),
    -> ('', 'The 1975'),
    -> ('', 'Last Child');
```
### ⚡ LANGKAH 5 — Mengisi Data Lagu
Tujuan: Menambahkan lagu sesuai artisnya.
Note: Untuk Penyanyi/Band no 5 sengaja tidak ditambahkan lagunya.
```sql
INSERT INTO tb_lagu
    -> (id_lagu, judul_lagu, id_artis) values
    -> ('', 'Wish You Were Here', 1),
    -> ('', 'You & I', 2),
    -> ('', 'Iris', 3),
    -> ('', 'Im In Love With You', 4)
    -> ('', 'Sk8er Boi', 1);
```
### ⚡ LANGKAH 6 — Melihat Semua Data
```sql
SELECT * FROM tb_artis;
SELECT * FROM tb_lagu;

SELECT * FROM tb_artis;
+----------+-------------------+
| id_artis | nama_artis        |
+----------+-------------------+
|        1 | Avril Lavigne     |
|        2 | One Direction     |
|        3 | The Goo Goo Dolls |
|        4 | The 1975          |
|        5 | Last Child        |
+----------+-------------------+

SELECT * FROM tb_lagu;
+---------+---------------------+----------+
| id_lagu | judul_lagu          | id_artis |
+---------+---------------------+----------+
|       1 | Wish You Were Here  |        1 |
|       2 | You & I             |        2 |
|       3 | Iris                |        3 |
|       4 | Im In Love With You |        4 |
|       5 | Sk8er Boi           |        1 |
+---------+---------------------+----------+
```
## 🔎 INNER JOIN
Menampilkan hanya data yang saling cocok.
```sql
SELECT tb_lagu.judul_lagu, tb_artis.nama_artis
    -> FROM tb_lagu
    -> INNER JOIN tb_artis ON tb_lagu.id_artis = tb_artis.id_artis;
+---------------------+-------------------+
| judul_lagu          | nama_artis        |
+---------------------+-------------------+
| Wish You Were Here  | Avril Lavigne     |
| You & I             | One Direction     |
| Iris                | The Goo Goo Dolls |
| Im In Love With You | The 1975          |
| Sk8er Boi           | Avril Lavigne     |
+---------------------+-------------------+
```
📌 HASIL:
Menampilkan lagu beserta nama artisnya.

## 🔎 LEFT JOIN
Menampilkan semua artis walaupun tidak punya lagu.
```sql
SELECT tb_artis.nama_artis, tb_lagu.judul_lagu
    -> FROM tb_artis
    -> LEFT JOIN tb_lagu ON tb_artis.id_artis = tb_lagu.id_artis;
+-------------------+---------------------+
| nama_artis        | judul_lagu          |
+-------------------+---------------------+
| Avril Lavigne     | Wish You Were Here  |
| One Direction     | You & I             |
| The Goo Goo Dolls | Iris                |
| The 1975          | Im In Love With You |
| Avril Lavigne     | Sk8er Boi           |
| Last Child        | NULL                |
+-------------------+---------------------+
```
📌 HASIL:
Jika artis tidak punya lagu → hasilnya NULL.

## 🔎 RIGHT JOIN
Menampilkan semua artis dari tabel kanan.
```sql
SELECT tb_lagu.judul_lagu, tb_artis.nama_artis
    -> FROM tb_lagu
    -> RIGHT JOIN tb_artis ON tb_lagu.id_artis = tb_artis.id_artis;
+---------------------+-------------------+
| judul_lagu          | nama_artis        |
+---------------------+-------------------+
| Wish You Were Here  | Avril Lavigne     |
| You & I             | One Direction     |
| Iris                | The Goo Goo Dolls |
| Im In Love With You | The 1975          |
| Sk8er Boi           | Avril Lavigne     |
| NULL                | Last Child        |
+---------------------+-------------------+
```

## 🎯 Kesimpulan
Dalam project ini kita belajar:
* Cara membuat database
* Cara membuat tabel dengan Primary Key
* Cara membuat Foreign Key
* Relasi One-to-Many
* Perbedaan INNER, LEFT, dan RIGHT JOIN

## 👩‍💻 Author
**ANGGI RAHMAWATI**
Project Tugas Database – SQL JOIN Exploration
