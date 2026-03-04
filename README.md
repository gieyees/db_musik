# 🎵 Music Database System (SQL Joins Exploration)

Proyek ini berisi dokumentasi langkah-langkah pembuatan database `db_musik` menggunakan **MariaDB** di lingkungan **XAMPP**. Proyek ini mencakup pembuatan tabel, relasi *foreign key*, operasi *CRUD* dasar, serta implementasi berbagai jenis `JOIN`.

## 🏗️ Persiapan Lingkungan

**Server**: MariaDB via XAMPP 
**Database Name**: `db_musik`

## 🏗️ Skema Database

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
```
### ⚡ LANGKAH 5 — Mengisi Data Lagu
Tujuan: Menambahkan lagu sesuai artisnya.
