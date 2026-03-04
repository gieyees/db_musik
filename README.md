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

### ⚡ Membuat Struktur & Data
Langkah awal melibatkan pembuatan tabel dan pengisian data contoh (seperti Avril Lavigne, One Direction, dll.).

```sql
-- Contoh Query Pembuatan Tabel Lagu dengan Foreign Key
CREATE TABLE tb_lagu(
    id_lagu INT PRIMARY KEY AUTO_INCREMENT,
    judul_lagu VARCHAR(50),
    id_artis INT,
    FOREIGN KEY (id_artis) REFERENCES tb_artis(id_artis)
);
```
