# 🏍️ Project Database Rental Motor (MySQL)
![MySQL](https://img.shields.io/badge/mysql-%2300f.svg?style=for-the-badge&logo=mysql&logoColor=white)
![Database](https://img.shields.io/badge/Database-Relational-blue?style=for-the-badge)

🖇️ My Linkedin : www.linkedin.com/in/kemala-putri-oktaviani-70476239b

👨‍💻 Kelompok 2 Anggota :
- Kemala Putri Oktaviani (16)
- Muhammad Satria Nabil (21)
- Salatin Nibras Bama Kerti (32)

## 📌 Deskripsi Project

Project ini merupakan simulasi sistem **Rental Motor** menggunakan database **MySQL**.
Database ini dibuat untuk mempelajari dasar SQL, meliputi:

* DDL (Data Definition Language)
* DML (Data Manipulation Language)
* JOIN (INNER JOIN & LEFT JOIN)
* AGGREGATE FUNCTION
* VIEW

Database terdiri dari 3 tabel utama:

* `motor` → data motor
* `pelanggan` → data penyewa
* `rental` → data transaksi rental

---

## 🗄️ 1. Membuat Database

```sql id="y4y23h"
CREATE DATABASE rental_motor;
USE rental_motor;
```

### Penjelasan

* `CREATE DATABASE` digunakan untuk membuat database baru.
* `USE` digunakan untuk memilih database yang aktif.

---

## 🧱 2. Membuat Tabel

### Tabel Motor

```sql id="u7w2ei"
CREATE TABLE motor (
  id_motor INT PRIMARY KEY,
  merk_motor VARCHAR(50),
  plat_nomor VARCHAR(15),
  harga_sewa INT,
  status VARCHAR(20)
);
```

**Penjelasan:**

* Menyimpan data motor yang tersedia untuk disewa.
* `id_motor` sebagai primary key (unik).

---

### Tabel Pelanggan

```sql id="hsjd9l"
CREATE TABLE pelanggan (
  id_pelanggan INT PRIMARY KEY,
  nama VARCHAR(50),
  no_hp VARCHAR(15),
  alamat VARCHAR(100)
);
```

**Penjelasan:**

* Menyimpan informasi pelanggan rental.

---

### Tabel Rental

```sql id="e4k6gh"
CREATE TABLE rental (
  id_rental INT PRIMARY KEY,
  id_motor INT,
  id_pelanggan INT,
  tanggal_sewa DATE,
  lama_sewa INT,
  total_bayar INT
);
```

**Penjelasan:**

* Menyimpan data transaksi penyewaan.
* Menghubungkan tabel motor dan pelanggan.

---

## 🔧 3. Modifikasi Struktur Tabel (ALTER TABLE)

### Mengubah ukuran kolom

```sql id="if7v0j"
ALTER TABLE motor MODIFY merk_motor VARCHAR(100);
```

➡️ Mengubah panjang karakter kolom `merk_motor`.

### Menambahkan kolom baru

```sql id="bhj1q0"
ALTER TABLE motor ADD COLUMN warna VARCHAR(100);
```

➡️ Menambahkan kolom warna.

### Mengganti nama kolom

```sql id="k6b0p1"
ALTER TABLE motor CHANGE warna color VARCHAR(100);
```

➡️ Mengubah nama kolom.

### Menghapus kolom

```sql id="lrm4xb"
ALTER TABLE motor DROP COLUMN color;
```

➡️ Menghapus kolom yang tidak dipakai.

---

## 🧾 4. Melihat Struktur Tabel

```sql id="5o5qaj"
DESCRIBE motor;
```

**Penjelasan:**
Menampilkan informasi kolom, tipe data, key, dan default value.

---

## ✏️ 5. Insert Data (DML)

### Data Motor

```sql id="wgxa4m"
INSERT INTO motor VALUES
(1,'Vario','B1234XX',80000,'tersedia'),
(2,'NMAX','B5678YY',120000,'tersedia'),
(3,'Beat','B2222AA',70000,'tersedia'),
(4,'PCX','B3333BB',130000,'tersedia'),
(5,'Aerox','B4444CC',110000,'tersedia');
```

**Penjelasan:**
Menambahkan 5 data motor ke tabel.

---

### Data Pelanggan

```sql id="5p3vsz"
INSERT INTO pelanggan VALUES
(1,'Nabil','08123456789','Jakarta'),
(2,'Bama','08234567890','Bekasi'),
(3,'Citra','08345678901','Depok'),
(4,'Doni','08456789012','Tangerang'),
(5,'Eka','08567890123','Bogor');
```

**Penjelasan:**
Menambahkan data pelanggan.

---

### Data Rental

```sql id="dsxnxj"
INSERT INTO rental VALUES
(1,1,1,'2026-02-20',3,240000),
(2,2,2,'2026-02-21',2,240000),
(3,3,3,'2026-02-22',4,280000),
(4,4,4,'2026-02-23',1,130000),
(5,5,5,'2026-02-24',2,220000);
```

**Penjelasan:**
Setiap transaksi menghubungkan:

* motor
* pelanggan
* durasi sewa
* total pembayaran

---

## 🔄 6. Menampilkan Data

```sql id="rq3r69"
SELECT * FROM motor;
SELECT * FROM pelanggan;
SELECT * FROM rental;
```

**Penjelasan:**
Menampilkan seluruh isi tabel.

---

## 🛠️ 7. Update Data

```sql id="h2qwsk"
UPDATE motor SET merk_motor = 'MIO'
WHERE merk_motor = 'PCX';
```

**Penjelasan:**
Mengubah data motor dengan merk PCX menjadi MIO.

---

## 🔗 8. JOIN TABLE

### INNER JOIN

```sql id="gs8qem"
SELECT pelanggan.nama, motor.merk_motor, rental.tanggal_sewa
FROM rental
INNER JOIN pelanggan ON rental.id_pelanggan = pelanggan.id_pelanggan
INNER JOIN motor ON rental.id_motor = motor.id_motor;
```

**Penjelasan:**
Menampilkan data gabungan pelanggan, motor, dan tanggal sewa.
Hanya data yang memiliki pasangan di semua tabel yang tampil.

---

### LEFT JOIN

```sql id="y3rq4c"
SELECT motor.merk_motor, pelanggan.nama, rental.tanggal_sewa
FROM motor
LEFT JOIN rental ON motor.id_motor = rental.id_motor
LEFT JOIN pelanggan ON rental.id_pelanggan = pelanggan.id_pelanggan;
```

**Penjelasan:**
Menampilkan semua data motor walaupun tidak memiliki transaksi rental.

---

## 📊 9. Aggregate Function

### Menghitung jumlah transaksi

```sql id="mepanv"
SELECT COUNT(*) AS jumlah_transaksi FROM rental;
```

➡️ Hasil: **5 transaksi**

### Menghitung total pendapatan

```sql id="juqejp"
SELECT SUM(total_bayar) AS total_pendapatan FROM rental;
```

➡️ Hasil: **1.110.000**

---

## 👁️ 10. View (Laporan Rental)

```sql id="wum3x2"
CREATE VIEW laporan_rental AS
SELECT pelanggan.nama, motor.merk_motor,
rental.tanggal_sewa, rental.lama_sewa, rental.total_bayar
FROM rental
JOIN pelanggan ON rental.id_pelanggan = pelanggan.id_pelanggan
JOIN motor ON rental.id_motor = motor.id_motor;
```

**Penjelasan:**
View digunakan sebagai tabel virtual untuk mempermudah melihat laporan rental tanpa menulis query JOIN berulang.

---

## 📋 11. Menampilkan Semua Tabel

```sql id="h0q1fv"
SHOW TABLES;
```

**Penjelasan:**
Menampilkan daftar tabel yang ada dalam database.

---

## 🧩 Relasi Antar Tabel

* `motor.id_motor` → terhubung ke `rental.id_motor`
* `pelanggan.id_pelanggan` → terhubung ke `rental.id_pelanggan`

---

## 🎯 Kesimpulan

Project ini menunjukkan implementasi dasar database MySQL mulai dari:

* Pembuatan database & tabel (DDL)
* Pengisian dan perubahan data (DML)
* Penggabungan data antar tabel (JOIN)
* Perhitungan data (Aggregate)
* Pembuatan laporan menggunakan VIEW

# 👨‍💻 Dibuat Oleh – Kelompok 2
**© 2026 Kelompok 2 – Database Mini Project**
