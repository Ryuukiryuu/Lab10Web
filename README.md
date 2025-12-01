# Lab10Web - PHP OOP

Praktikum 10: Implementasi Object-Oriented Programming (OOP) dengan PHP

## Deskripsi

Project ini merupakan implementasi konsep OOP dalam PHP dengan membuat sistem manajemen data mahasiswa yang dilengkapi fitur CRUD (Create, Read, Update, Delete) lengkap dengan konsep modularisasi menggunakan class library.

## Tujuan Praktikum

1. Memahami konsep dasar OOP (Object-Oriented Programming)
2. Memahami konsep Class dan Object dalam PHP
3. Mampu membuat program OOP sederhana menggunakan PHP
4. Mengimplementasikan konsep modularisasi dengan class library
5. Membuat aplikasi CRUD dengan arsitektur OOP

## Fitur Utama

- Dashboard dengan statistik data mahasiswa
- Fitur pencarian mahasiswa berdasarkan NIM, Nama, atau Jurusan
- Tambah data mahasiswa baru
- Lihat detail informasi mahasiswa
- Edit/Update data mahasiswa
- Hapus data mahasiswa
- Demo konsep OOP dasar dengan class Mobil
- Responsive design untuk berbagai ukuran layar
- Modern UI dengan gradient design

## Teknologi yang Digunakan

- PHP 7.4 atau lebih tinggi
- MySQL/MariaDB
- HTML5
- CSS3
- Konsep OOP (Class, Object, Encapsulation, Constructor, Method)

## Struktur File
```
lab10_php_oop/
├── config.php              # Konfigurasi koneksi database
├── database.php            # Class Database untuk operasi CRUD
├── form.php                # Class Form untuk generate form input
├── index.php               # Halaman dashboard utama
├── form_input.php          # Halaman form tambah data mahasiswa
├── proses_form.php         # Proses insert data ke database
├── database_view.php       # Halaman detail mahasiswa
├── database_edit.php       # Halaman form edit data mahasiswa
├── mobil_demo.php          # Demo konsep OOP dasar
└── README.md               # Dokumentasi project
```

## Konsep OOP yang Diterapkan

### 1. Class dan Object
- **Class Database**: Mengelola koneksi dan operasi database
- **Class Form**: Mengenerate form input secara dinamis
- **Class Mobil**: Demo konsep dasar OOP

### 2. Encapsulation
- Properti class dibuat private/protected
- Akses ke properti melalui method public

### 3. Constructor
- Method `__construct()` untuk inisialisasi object
- Otomatis dijalankan saat object dibuat

### 4. Method
- Method public untuk operasi CRUD (Create, Read, Update, Delete)
- Method private untuk konfigurasi internal

## Instalasi dan Konfigurasi

### 1. Persiapan Environment
```bash
# Pastikan XAMPP/WAMP sudah terinstall
# Aktifkan Apache dan MySQL
```

### 2. Clone Repository
```bash
git clone https://github.com/username/Lab10Web.git
cd Lab10Web
```

### 3. Konfigurasi Database

**A. Buat Database**
```sql
CREATE DATABASE lab10_db;
USE lab10_db;
```

**B. Buat Tabel Mahasiswa**
```sql
CREATE TABLE mahasiswa (
    id INT(11) AUTO_INCREMENT PRIMARY KEY,
    nim VARCHAR(10) NOT NULL UNIQUE,
    nama VARCHAR(100) NOT NULL,
    jurusan VARCHAR(50) NOT NULL,
    email VARCHAR(100),
    alamat TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

**C. Insert Data Sample (Opsional)**
```sql
INSERT INTO mahasiswa (nim, nama, jurusan, email, alamat) VALUES
('2024001', 'Ahmad Rizki Pratama', 'Teknik Informatika', 'ahmad.rizki@email.com', 'Jl. Merdeka No. 10, Jakarta Pusat'),
('2024002', 'Siti Nurhaliza', 'Sistem Informasi', 'siti.nurhaliza@email.com', 'Jl. Sudirman No. 25, Jakarta Selatan'),
('2024003', 'Budi Santoso', 'Teknik Komputer', 'budi.santoso@email.com', 'Jl. Gatot Subroto No. 5, Jakarta Barat');
```

### 4. Konfigurasi File config.php
```php
<?php
$config = array(
    'host' => 'localhost',
    'username' => 'root',
    'password' => '',
    'db_name' => 'lab10_db'
);
?>
```

### 5. Akses Aplikasi
```
http://localhost/lab10_php_oop/index.php
```

## Penjelasan Class Library

### Class Database (database.php)

Class ini berfungsi sebagai layer abstraksi untuk operasi database dengan fitur:

**Method yang tersedia:**
- `__construct()`: Inisialisasi koneksi database
- `query($sql)`: Menjalankan query SQL custom
- `get($table, $where)`: Mengambil satu record
- `getAll($table, $where, $order)`: Mengambil semua record
- `insert($table, $data)`: Insert data baru
- `update($table, $data, $where)`: Update data
- `delete($table, $filter)`: Hapus data
- `escape($value)`: Escape string untuk keamanan

**Contoh Penggunaan:**
```php
$db = new Database();

// Insert data
$data = array(
    'nim' => '2024001',
    'nama' => 'John Doe',
    'jurusan' => 'Teknik Informatika'
);
$db->insert('mahasiswa', $data);

// Get data
$mahasiswa = $db->get('mahasiswa', "nim='2024001'");

// Update data
$data = array('nama' => 'Jane Doe');
$db->update('mahasiswa', $data, "nim='2024001'");

// Delete data
$db->delete('mahasiswa', "nim='2024001'");
```

### Class Form (form.php)

Class ini berfungsi untuk generate form HTML secara dinamis dengan fitur:

**Method yang tersedia:**
- `__construct($action, $submit)`: Set action dan label button
- `addField($name, $label, $type, $options, $value)`: Tambah field form
- `displayForm()`: Render form HTML

**Contoh Penggunaan:**
```php
$form = new Form("proses.php", "Simpan Data");
$form->addField("txtnim", "NIM", "text");
$form->addField("txtnama", "Nama", "text");

$jurusan = array(
    "TI" => "Teknik Informatika",
    "SI" => "Sistem Informasi"
);
$form->addField("txtjurusan", "Jurusan", "select", $jurusan);

$form->displayForm();
```

## Fitur-Fitur Halaman

### 1. Dashboard (index.php)
- Menampilkan statistik total mahasiswa
- Tabel data mahasiswa dengan pagination
- Fitur search/pencarian
- Action buttons: Detail, Edit, Hapus

### 2. Form Input (form_input.php)
- Form tambah mahasiswa baru
- Validasi required field
- Dropdown untuk pilihan jurusan
- Textarea untuk alamat

### 3. Detail Mahasiswa (database_view.php)
- Menampilkan informasi lengkap mahasiswa
- Badge jurusan dengan warna berbeda
- Timestamp created dan updated
- Action buttons: Edit, Hapus

### 4. Edit Mahasiswa (database_edit.php)
- Form edit data mahasiswa
- Pre-filled dengan data existing
- Validasi NIM unique
- Update timestamp otomatis

### 5. Demo OOP (mobil_demo.php)
- Demonstrasi konsep Class dan Object
- Contoh Encapsulation
- Contoh penggunaan Constructor
- Contoh Method dalam class

## Konsep Modularisasi

Project ini menerapkan konsep modularisasi dengan:

1. **Separation of Concerns**: Setiap class memiliki tanggung jawab spesifik
2. **Reusability**: Class dapat digunakan di berbagai file
3. **Maintainability**: Mudah untuk maintenance dan update
4. **Scalability**: Mudah untuk menambah fitur baru

## Keamanan

Implementasi keamanan yang diterapkan:

1. **SQL Injection Prevention**: Menggunakan prepared statement
2. **XSS Prevention**: Menggunakan htmlspecialchars()
3. **Input Validation**: Validasi di sisi client dan server
4. **Unique Constraint**: NIM harus unique di database

## Cara Penggunaan

### Menambah Data Mahasiswa
1. Klik tombol "Tambah Mahasiswa"
2. Isi form dengan data lengkap
3. Klik "Simpan Data"

### Mencari Data Mahasiswa
1. Gunakan search box di dashboard
2. Ketik NIM, Nama, atau Jurusan
3. Klik "Cari"

### Mengedit Data Mahasiswa
1. Klik tombol "Edit" pada data mahasiswa
2. Ubah data yang diinginkan
3. Klik "Update Data"

### Menghapus Data Mahasiswa
1. Klik tombol "Hapus" pada data mahasiswa
2. Konfirmasi penghapusan
3. Data akan terhapus dari database

## Screenshot

### Dashboard
<img width="1365" height="734" alt="image" src="https://github.com/user-attachments/assets/9260b8d9-90e2-47c1-a985-52010f32686f" />

### Form Input
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/14ed4af9-1126-4ef9-ade8-b52b87290ce3" />

### Demo OOP
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/bc98b8ef-a3e0-4e85-b0af-3314f5eb09f2" />


