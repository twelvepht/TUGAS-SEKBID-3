# Prompt untuk Claude Code: Website Daftar Tugas Tim

Salin semua isi di bawah garis ini, lalu tempel ke Claude Code di folder proyek kosong.

---

Buatkan saya website **Daftar Tugas Tim** lengkap dan siap dijalankan di folder ini. Semua tampilan (UI) menggunakan **Bahasa Indonesia**.

## Tujuan
Website untuk menampilkan dan mengelola daftar tugas tim. Ada dua tampilan:

1. **Tampilan Penonton (publik)**: siapa saja bisa membuka tanpa login, hanya bisa **melihat** (read-only).
2. **Tampilan Admin**: harus **login dengan username dan password admin** dulu. Admin bisa menambah, mengubah, menghapus, dan mengubah status tugas.

## Tech stack
- Backend: **Node.js + Express**
- Database: **SQLite** (pakai `better-sqlite3`), file database otomatis dibuat saat pertama kali dijalankan
- Frontend: **HTML, CSS, dan JavaScript biasa** (tanpa framework) yang disajikan oleh Express
- Autentikasi: **session** berbasis cookie (`express-session`), password di-hash dengan **bcrypt**
- Keamanan tambahan: `helmet`, `express-rate-limit`, `dotenv`

## Halaman
- `/` : Tampilan Penonton
- `/login` : Halaman login admin
- `/admin` : Dashboard admin (hanya bisa diakses setelah login; kalau belum login, arahkan ke `/login`)

## Fitur Tampilan Penonton (`/`)
- Menampilkan daftar tugas dalam bentuk kartu atau tabel yang rapi
- Setiap tugas menampilkan: judul, deskripsi, penanggung jawab, prioritas (Rendah/Sedang/Tinggi), status (Belum Dikerjakan / Sedang Dikerjakan / Selesai), dan tenggat (deadline)
- Ringkasan di atas: jumlah total tugas, jumlah per status, dan **progress bar** persentase tugas selesai
- Filter berdasarkan status, prioritas, dan penanggung jawab, serta kolom pencarian
- Tugas yang melewati deadline dan belum selesai diberi tanda merah "Terlambat"
- Tombol kecil "Login Admin" di pojok atas yang mengarah ke `/login`
- Tidak ada tombol tambah/ubah/hapus sama sekali di tampilan ini

## Fitur Tampilan Admin (`/admin`)
- Semua yang ada di tampilan penonton, ditambah:
  - Tombol **Tambah Tugas** (form modal)
  - Tombol **Edit** dan **Hapus** di setiap tugas (hapus dengan konfirmasi)
  - Ubah status cepat langsung dari daftar (dropdown)
- Tombol **Logout**
- Tampilkan nama admin yang sedang login

## Autentikasi
- Username dan password admin diambil dari file `.env` (`ADMIN_USERNAME`, `ADMIN_PASSWORD`), lalu saat server start password di-hash dengan bcrypt dan disimpan di memori atau database. **Jangan** menyimpan password plain text di kode.
- Sediakan file `.env.example` dengan contoh nilai, dan pastikan `.env` masuk ke `.gitignore`
- Session cookie: `httpOnly`, `sameSite: 'lax'`, `secure` aktif saat `NODE_ENV=production`
- Batasi percobaan login (maksimal 5 kali per 15 menit per IP) dengan `express-rate-limit`
- Pesan error login umum saja ("Username atau password salah"), jangan bocorkan mana yang salah

## API
- `GET /api/tugas` : publik, mengembalikan semua tugas
- `POST /api/tugas` : **admin saja**
- `PUT /api/tugas/:id` : **admin saja**
- `DELETE /api/tugas/:id` : **admin saja**
- `POST /api/login`, `POST /api/logout`, `GET /api/me`
- Perlindungan admin **harus diterapkan di server** (middleware), bukan hanya menyembunyikan tombol di frontend
- Validasi semua input di server (judul wajib, panjang maksimal, nilai status/prioritas harus sesuai daftar yang diizinkan) dan gunakan prepared statements untuk mencegah SQL injection
- Escape teks saat dirender di frontend untuk mencegah XSS

## Desain
- Tampilan modern, bersih, dan **responsif** (nyaman di HP maupun laptop)
- Warna konsisten: badge warna berbeda untuk status dan prioritas
- Sediakan opsi **mode gelap/terang**
- Beri data contoh (seed) 5-6 tugas saat database masih kosong agar tampilan langsung terlihat

## Struktur proyek yang diinginkan
```
/
├── server.js
├── package.json
├── .env.example
├── .gitignore
├── README.md
├── db.js
├── middleware/auth.js
├── routes/ (auth.js, tugas.js)
└── public/
    ├── index.html      (penonton)
    ├── login.html
    ├── admin.html
    ├── css/style.css
    └── js/ (penonton.js, admin.js, login.js)
```

## Yang saya minta darimu
1. Buat semua file di atas dan install dependensinya.
2. Buat `README.md` dalam Bahasa Indonesia berisi: cara install, cara mengatur `.env`, cara menjalankan (`npm start`), dan cara mengganti username/password admin.
3. Jalankan server dan uji: login berhasil, login gagal, penonton tidak bisa mengubah data (API mengembalikan 401), dan CRUD tugas berfungsi untuk admin.
4. Di akhir, ringkas apa yang sudah dibuat dan URL untuk mengaksesnya (misalnya `http://localhost:3000`).
