# Hawa Trans Indonesia

Website company profile multilingual untuk Hawa Trans Indonesia, dibangun dengan Next.js 15 App Router, TypeScript, Tailwind CSS, next-intl, dan MongoDB. Aplikasi ini menampilkan halaman utama, tentang, layanan, blog, kontak, serta panel admin sederhana untuk mengelola konten blog, layanan, dan informasi kontak.

## Ringkasan Proyek

Proyek ini dibuat untuk memudahkan pengunjung melihat informasi perusahaan dalam beberapa bahasa, membaca artikel blog, dan menghubungi tim melalui WhatsApp, email, atau alamat kantor. Di sisi admin, tersedia fitur CRUD blog dan pengaturan konten yang disimpan ke MongoDB.

## Fitur Utama

- Multibahasa: Indonesia, Inggris, Jepang, Korea, dan Mandarin.
- Halaman company profile: Home, About, Services, Blog, Contact, dan Admin Login.
- Blog CRUD: tambah, baca, ubah, hapus post blog.
- Konten layanan dinamis: prosedur, interpreter, legalisasi, dan apostille.
- Informasi kontak dinamis: nomor WhatsApp, email, dan alamat kantor.
- Admin login demo berbasis state lokal/localStorage.
- SEO dasar: metadata, sitemap, robots, dan URL yang rapi.
- Tampilan responsif dengan Tailwind CSS.

## Stack Teknologi

- Next.js 15
- React 19
- TypeScript
- Tailwind CSS
- next-intl
- MongoDB + Mongoose
- react-quill-new untuk editor konten
- react-slick untuk carousel
- Netlify plugin untuk deployment

## Struktur Folder Penting

- [src/app/[locale]/page.tsx](src/app/%5Blocale%5D/page.tsx) - halaman home per bahasa.
- [src/app/[locale]/about/page.tsx](src/app/%5Blocale%5D/about/page.tsx) - halaman tentang.
- [src/app/[locale]/services/page.tsx](src/app/%5Blocale%5D/services/page.tsx) - halaman layanan dan harga.
- [src/app/[locale]/blog/page.tsx](src/app/%5Blocale%5D/blog/page.tsx) - daftar artikel blog.
- [src/app/[locale]/contact/page.tsx](src/app/%5Blocale%5D/contact/page.tsx) - halaman kontak dan edit kontak admin.
- [src/app/[locale]/admin/login/page.tsx](src/app/%5Blocale%5D/admin/login/page.tsx) - login admin.
- [src/app/api/*](src/app/api) - endpoint blog, kontak, dan layanan.
- [src/components](src/components) - komponen UI utama seperti Navigation, Footer, Carousel, ProtectedRoute.
- [src/contexts](src/contexts) - state global untuk auth dan blog.
- [src/models](src/models) - schema Mongoose.
- [src/data/blogPosts.ts](src/data/blogPosts.ts) - data awal artikel blog.
- [messages](messages) - file terjemahan per bahasa.
- [src/i18n](src/i18n) - routing dan request config next-intl.

## Alur Kerja Aplikasi

1. Pengguna membuka website melalui route bahasa.
2. Next.js memuat layout, navigation, dan footer.
3. next-intl mengambil teks dari file di folder [messages](messages).
4. Halaman blog, layanan, dan kontak mengambil data dari API route.
5. API route berkomunikasi dengan MongoDB melalui [src/lib/mongodb.ts](src/lib/mongodb.ts).
6. Admin login disimpan sementara di localStorage untuk demo.

## Halaman yang Tersedia

- `/` - Home bahasa Indonesia.
- `/en` - Home bahasa Inggris.
- `/ja` - Home bahasa Jepang.
- `/ko` - Home bahasa Korea.
- `/zh` - Home bahasa Mandarin.
- `/about` - Tentang perusahaan.
- `/services` - Layanan dan harga.
- `/blog` - Daftar blog.
- `/blog/[slug]` - Detail artikel.
- `/blog/create` - Buat artikel baru.
- `/blog/edit/[slug]` - Edit artikel.
- `/contact` - Informasi kontak.
- `/admin/login` - Login admin.

## API Endpoint

### Blog

- `GET /api/blog` - ambil semua post blog.
- `GET /api/blog?locale=en` - ambil post berdasarkan bahasa.
- `POST /api/blog` - buat post baru.
- `GET /api/blog/[slug]` - ambil detail post.
- `PUT /api/blog/[slug]` - update post.
- `DELETE /api/blog/[slug]` - hapus post.
- `POST /api/blog/seed` - isi data awal blog ke database.

### Konten Layanan

- `GET /api/services/prices` - ambil daftar harga layanan.
- `POST /api/services/prices` - simpan ulang semua harga layanan.
- `PUT /api/services/prices` - update 1 layanan.
- `DELETE /api/services/prices?id=...` - hapus 1 layanan.
- `GET /api/services/content` - ambil konten prosedur/interpreter/legalisasi/apostille.
- `PUT /api/services/content` - update konten layanan.

### Kontak

- `GET /api/contact-settings` - ambil data kontak dari database.
- `PUT /api/contact-settings` - update nomor WhatsApp, email, dan alamat.

## Model Data

### BlogPost

Menyimpan judul, ringkasan, isi konten, penulis, slug, bahasa, tag, dan tanggal publikasi.

### ContactSettings

Menyimpan:

- nomor WhatsApp untuk link chat,
- nomor WhatsApp format tampilan,
- email,
- alamat kantor.

### TranslationService

Menyimpan daftar bahasa dan harga terjemahan general/sworn.

### ServiceContent

Menyimpan konten editor untuk:

- prosedur,
- interpreter,
- legalisasi,
- apostille.

## Konfigurasi Environment

Buat file `.env.local` di root project dan isi variabel yang dibutuhkan aplikasi, terutama koneksi MongoDB.

Catatan:

- `MONGODB_URI` wajib ada supaya koneksi database berjalan.
- Nilai rahasia untuk autentikasi admin tidak dicantumkan di dokumentasi ini. Simpan di environment lokal atau secret manager sesuai kebutuhan deployment.

## Cara Menjalankan Lokal

1. Install dependency:

```bash
npm install
```

2. Jalankan development server:

```bash
npm run dev
```

3. Buka browser di:

```text
http://localhost:3000
```

## Build Production

```bash
npm run build
npm start
```

## Login Admin

Autentikasi admin tersedia untuk kebutuhan pengelolaan konten. Detail kredensial tidak ditulis di README dan sebaiknya dikelola secara aman melalui environment lokal atau mekanisme autentikasi backend yang sesuai.

## Terjemahan Bahasa

Teks UI dikelola di folder [messages](messages). Jika ingin menambah atau mengubah bahasa, sesuaikan file JSON berikut:

- [messages/id.json](messages/id.json)
- [messages/en.json](messages/en.json)
- [messages/ja.json](messages/ja.json)
- [messages/ko.json](messages/ko.json)
- [messages/zh.json](messages/zh.json)

Routing bahasa diatur oleh:

- [src/i18n/routing.ts](src/i18n/routing.ts)
- [src/i18n/request.ts](src/i18n/request.ts)
- [src/middleware.ts](src/middleware.ts)

## Deployment

Project ini sudah menyiapkan konfigurasi Netlify lewat [netlify.toml](netlify.toml). Build command yang dipakai adalah `npm run build`.

## Catatan Pengembangan

- Data blog awal disimpan di [src/data/blogPosts.ts](src/data/blogPosts.ts).
- Koneksi MongoDB memakai cache singleton di [src/lib/mongodb.ts](src/lib/mongodb.ts).
- Admin authentication saat ini masih sederhana dan berbasis localStorage.
- Beberapa konten SEO dan metadata masih bisa disesuaikan lagi sebelum production.

## Pengembangan Lanjutan yang Disarankan

1. Pindahkan autentikasi admin ke sistem backend yang aman.
2. Tambahkan file `.env.example` untuk memudahkan setup.
3. Tambahkan screenshot aplikasi ke README.
4. Rapikan metadata domain, sitemap, dan robots untuk domain final produksi.

## Lisensi

Proyek ini dibuat untuk kebutuhan internal dan demonstrasi pengembangan website company profile.
