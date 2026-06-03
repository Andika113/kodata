# Koruna / Document Validation App

Koruna adalah aplikasi MERN untuk validasi dokumen, layanan penerjemahan tersumpah, webinar, blog, autentikasi, dan dashboard admin. Struktur proyek dibagi menjadi dua bagian utama:

- [backend](backend) berisi Express, MongoDB, autentikasi, payment, storage, dan integrasi AI/Google API.
- [frontend](frontend) berisi aplikasi React + Vite untuk user, admin, translator, dan halaman publik.

## Gambaran Arsitektur

Alur utamanya berjalan seperti ini:

1. Frontend memanggil API di backend melalui `VITE_API_BASE_URL`.
2. Backend memproses autentikasi, data dokumen, histori, pembayaran, blog, webinar, dan dashboard internal.
3. Penyimpanan file bisa lokal atau Google Cloud Storage, tergantung `STORAGE_PROVIDER` dan `DISABLE_GOOGLE`.
4. Layanan AI dan Google API memakai credential dari environment atau Application Default Credentials, bukan file key yang disimpan di repo.

## Struktur Penting

### Backend

- [backend/server.js](backend/server.js) adalah entry point Express, memasang CORS, middleware, route, sitemap, dan static upload.
- [backend/src/config/db.js](backend/src/config/db.js) menghubungkan aplikasi ke MongoDB.
- [backend/src/config/passport.js](backend/src/config/passport.js) menangani Google OAuth login.
- [backend/src/middlewares/verifyToken.js](backend/src/middlewares/verifyToken.js) memvalidasi JWT dan memuat user dari database.
- [backend/src/utils/gcsUploader.js](backend/src/utils/gcsUploader.js) mengelola upload file ke GCS atau local storage.
- [backend/src/utils/documentAI.js](backend/src/utils/documentAI.js) mengekstrak teks dari file menggunakan Google Document AI.
- [backend/src/utils/aiService.js](backend/src/utils/aiService.js) menjadi wrapper AI provider seperti Gemini, Groq, dan Elice.

### Frontend

- [frontend/src/main.jsx](frontend/src/main.jsx) menginisialisasi aplikasi React.
- [frontend/src/App.jsx](frontend/src/App.jsx) mendefinisikan routing publik, admin, translator, dan halaman terproteksi.
- [frontend/src/AuthContext.jsx](frontend/src/AuthContext.jsx) menyimpan status autentikasi user.
- [frontend/src/LanguageContext.jsx](frontend/src/LanguageContext.jsx) mengelola bahasa tampilan.
- [frontend/src/ServiceUtils.jsx](frontend/src/ServiceUtils.jsx) berisi helper untuk alur layanan dokumen.

## Modul Fungsional

- Autentikasi: register, login, Google OAuth, dan proteksi route.
- Dokumentasi dan validasi dokumen: unggah, proses, hasil ekstraksi, dan histori.
- Penerjemahan tersumpah: alur form layanan, dashboard translator, dan status pekerjaan.
- Payment: integrasi Midtrans untuk top up atau transaksi terkait layanan.
- Konten publik: blog, about page, webinar, feedback, dan homepage marketing.
- Admin tools: manajemen user, blog, about content, shipping, feedback, dan generator nomor registrasi.

## Konfigurasi Aman

Repo ini disiapkan agar aman untuk GitHub:

- File credential Google yang sempat hardcoded sudah dipindahkan dari repo dan diganti menjadi konfigurasi berbasis environment.
- Gunakan [\.env.example](.env.example) sebagai acuan, lalu buat `.env` sendiri untuk development lokal.
- Jangan menaruh private key, client secret, server key, atau service account JSON ke dalam repository.

## Menjalankan Proyek

1. Salin [\.env.example](.env.example) menjadi `.env` di root repo dan isi nilai yang diperlukan.
2. Install dependency di folder [backend](backend) dan [frontend](frontend).
3. Jalankan backend dan frontend sesuai script pada masing-masing `package.json`.

## Catatan Keamanan

- Credential sensitif harus disimpan di environment lokal, secret manager, atau file di luar repo.
- Jika memakai Google Cloud, arahkan `GOOGLE_APPLICATION_CREDENTIALS`, `GCS_KEY_FILE_PATH`, atau `DOCUMENT_AI_KEY_FILE_PATH` ke lokasi file key yang tidak ikut di-commit.
- Pastikan log, screenshot, dan dokumentasi publik tidak memuat token, key, atau URL privat.