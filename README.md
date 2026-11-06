# 📱 NshStore - Mobile & Gadget Catalog App (Flutter CRUD)

Proyek aplikasi mobile katalog dan manajemen produk gadget (NshStore) berbasis **Flutter** dan RESTful API **PHP (Docker Compose + MySQL)**. Proyek ini dikembangkan untuk memenuhi tugas mata kuliah **Pengembangan Perangkat Bergerak (PPB)**.

---

## 📌 Daftar Isi
- [Tentang Aplikasi](#-tentang-aplikasi)
- [Fitur Utama](#-fitur-utama)
- [Teknologi yang Digunakan](#-teknologi-yang-digunakan)
- [Struktur Direktori](#-struktur-direktori)
- [Panduan Instalasi & Menjalankan](#-panduan-instalasi--menjalankan)
  - [1. Prasyarat](#1-prasyarat)
  - [2. Menjalankan Backend (Docker)](#2-menjalankan-backend-docker)
  - [3. Menjalankan Frontend (Flutter)](#3-menjalankan-frontend-flutter)
- [Konfigurasi Jaringan & Base URL](#-konfigurasi-jaringan--base-url)
- [Dokumentasi API Singkat](#-dokumentasi-api-singkat)
- [Anggota Tim / Pengembang](#-anggota-tim--pengembang)

---

## 📖 Tentang Aplikasi

**NshStore** adalah aplikasi toko gadget dan smartphone yang menerapkan konsep **CRUD (Create, Read, Update, Delete)** secara penuh, menghubungkan frontend mobile modern dengan backend RESTful service mandiri. 

Aplikasi dirancang dengan antarmuka bertema **Pastel Modern**, responsif, dan kaya fitur visual seperti pencarian realtime, filter kategori, slider promosi banner, ulasan produk, spesifikasi teknis, serta pengelolaan inventaris produk.

---

## ✨ Fitur Utama

- 🛍️ **Katalog Produk & Kategori**: Menampilkan daftar gadget/smartphone dengan filter kategori (`smartphones`, `laptops`, `tablets`, `mobile-accessories`).
- 🔍 **Live Search & Filter**: Pencarian instan berdasarkan nama produk, brand, dan deskripsi.
- ➕ **Tambah Produk Baru (Create)**: Form input produk dengan validasi (Title, Brand, Kategori, Harga, Diskon, Stok, Rating, Deskripsi, Thumbnail/Gambar).
- 📄 **Detail Produk Interaktif (Read)**: Informasi mendalam produk termasuk galeri gambar, status stok, garansi, estimasi pengiriman, kebijakan pengembalian, dan ulasan (*reviews*).
- ✏️ **Edit & Perbarui Produk (Update)**: Memperbarui data spesifikasi dan harga produk yang tersimpan di database.
- 🗑️ **Hapus Produk (Delete)**: Menghapus produk dari katalog disertai dialog konfirmasi keamanan.
- 🌐 **Opsi Pengaturan IP Host Dinamis**: Mendukung penggantian alamat server backend langsung dari aplikasi untuk pengujian di device fisik (HP asli via Wi-Fi) maupun emulator/desktop.

---

## 🛠️ Teknologi yang Digunakan

### Frontend (Mobile App)
- **Framework**: [Flutter](https://flutter.dev/) (SDK Dart 3.x)
- **Desain UI/UX**: Google Fonts (Plus Jakarta Sans), Custom Pastel Palette, Material 3
- **HTTP Client**: `http` package
- **Format Data**: JSON REST API

### Backend & Database (Dockerized)
- **Web Server & Reverse Proxy**: Caddy Server
- **Runtime**: PHP 8.2 (PHP-FPM)
- **Database**: MySQL 8.0
- **Database Management Tool**: phpMyAdmin
- **Orkestrasi**: Docker Compose

---

## 📂 Struktur Direktori

```plaintext
Flutter_CRUD/
├── backend/
│   ├── databases/            # Volume penyimpanan data MySQL
│   ├── htdocs/               # Kode sumber PHP REST API
│   │   ├── db.php            # Koneksi PDO & skema tabel database
│   │   ├── index.php         # Endpoint routing REST API CRUD
│   │   └── seed.php          # Seeder awal dummy data produk
│   ├── Caddyfile             # Konfigurasi reverse proxy Caddy
│   ├── docker-compose.yaml   # Orkestrasi container Docker
│   ├── Dockerfile            # Image build PHP-FPM
│   └── .env.example          # Template konfigurasi environment database
│
└── frontend/
    ├── lib/
    │   ├── models/           # Data model (Product, Review, Dimensi, dll.)
    │   ├── screens/          # Halaman tampilan (Home, Detail, Form Create/Edit)
    │   ├── services/         # Layanan API (HTTP request GET, POST, PUT, DELETE)
    │   ├── theme/            # Tema warna (Pastel Colors)
    │   ├── widgets/          # Komponen modular UI (Card, Slider, Chip, Search)
    │   └── main.dart         # Entry point aplikasi Flutter
    └── pubspec.yaml          # Manajemen dependensi Flutter
```

---

## 🚀 Panduan Instalasi & Menjalankan

### 1. Prasyarat
Pastikan tools berikut sudah terinstal di komputer Anda:
- [Git](https://git-scm.com/)
- [Flutter SDK](https://docs.flutter.dev/get-started/install) (versi stable terbaru)
- [Docker & Docker Desktop](https://www.docker.com/)

---

### 2. Menjalankan Backend (Docker)

1. Buka terminal dan masuk ke folder `backend`:
   ```bash
   cd backend
   ```

2. Siapkan file environment:
   Salin `.env.example` menjadi `.env` (sesuaikan username/password jika diperlukan):
   ```bash
   # Windows PowerShell:
   Copy-Item .env.example .env

   # Bash / macOS / Linux:
   cp .env.example .env
   ```

3. Jalankan container dengan Docker Compose:
   ```bash
   docker compose up -d --build
   ```

4. Service akan aktif pada port:
   - **REST API**: `http://localhost:8080`
   - **phpMyAdmin**: `http://localhost:8081`
   - **MySQL**: `localhost:3306`

5. Jalankan seed data awal (opsional, jika database masih kosong):
   Buka browser atau jalankan curl ke:
   ```text
   http://localhost:8080/seed.php
   ```

---

### 3. Menjalankan Frontend (Flutter)

1. Buka terminal baru dan masuk ke folder `frontend`:
   ```bash
   cd frontend
   ```

2. Unduh paket dependensi yang dibutuhkan:
   ```bash
   flutter pub get
   ```

3. Jalankan aplikasi pada target perangkat Anda:
   - **Chrome (Web)**:
     ```bash
     flutter run -d chrome
     ```
   - **Windows Desktop**:
     ```bash
     flutter run -d windows
     ```
   - **Android Emulator**:
     Pastikan emulator aktif di Android Studio, lalu:
     ```bash
     flutter run
     ```

---

## 🌐 Konfigurasi Jaringan & Base URL

Aplikasi Flutter secara otomatis menyesuaikan target Base URL API tergantung lingkungan eksekusi:

| Target Platform | URL API Default | Keterangan |
|---|---|---|
| **Android Emulator** | `http://10.0.2.2:8080` | Alias localhost mesin host untuk emulator |
| **Web & Windows** | `http://localhost:8080` | Mengakses port langsung di komputer host |
| **Perangkat Fisik (HP)** | `http://<IP-KOMPUTER-ANDA>:8080` | Atur IP Komputer (misal: `http://192.168.1.10:8080`) |

> 💡 **Tips Pengujian di HP Fisik:**  
> Pastikan smartphone dan laptop terhubung ke jaringan Wi-Fi yang sama, lalu gunakan fitur konfigurasi URL server yang ada di aplikasi atau sesuaikan variabel `customBaseUrl` pada `lib/services/api_service.dart`.

---

## 📡 Dokumentasi API Singkat

Semua endpoint mengembalikan data berformat JSON:

| Method | Endpoint | Keterangan |
|---|---|---|
| `GET` | `/products` | Mengambil seluruh daftar produk (dukung parameter limit, skip, search) |
| `GET` | `/products/{id}` | Mengambil detail produk berdasarkan ID |
| `GET` | `/products/category/{category}` | Mengambil daftar produk berdasarkan kategori tertentu |
| `GET` | `/products/categories` | Mendapatkan daftar kategori produk yang tersedia |
| `POST` | `/products/add` | Menambahkan data produk baru |
| `PUT` / `PATCH` | `/products/{id}` | Memperbarui data produk berdasarkan ID |
| `DELETE` | `/products/{id}` | Menghapus data produk berdasarkan ID |

---

## 👥 Pengembang / Kontributor

Proyek ini dibuat untuk tugas mata kuliah **Pengembangan Perangkat Bergerak (PPB)**.

- **Nama**: [Nama Mahasiswa]
- **NIM**: [NIM Mahasiswa]
- **Kelas / Program Studi**: [Kelas] - [Program Studi / Teknik Informatika]
- **Dosen Pengampu**: [Nama Dosen Pengampu]

---

⭐ *Jangan lupa beri bintang pada repositori ini jika bermanfaat!*
