# HENTPRO Website

Website profil resmi HENTPRO untuk layanan terjemahan dan interpreting legal/bisnis.

## Ringkasan
Project ini adalah website statis berbasis HTML, CSS, dan JavaScript tanpa framework.

Fitur utama:
- Header dan navigasi responsif
- Section About, Services, Vision & Mission, Clients, Team, FAQ, Contact, dan Form
- Watermark logo pada background
- Client logo carousel
- Embedded Google Maps dan JotForm

## Struktur Folder
- `index.html` : Halaman utama website
- `style.css` : Seluruh styling eksternal
- `aset/` : Aset gambar utama
- `aset/client/` : Logo-logo klien
- `docs/` : Dokumentasi tambahan

## Menjalankan Secara Lokal
Karena ini website statis, cukup buka file `index.html` langsung di browser.

Alternatif dengan local server (disarankan):

### Opsi 1: VS Code Live Server
1. Install extension **Live Server**.
2. Klik kanan `index.html`.
3. Pilih **Open with Live Server**.

### Opsi 2: Python HTTP Server
Jalankan di root project:

```bash
python -m http.server 8080
```

Lalu buka:
- alamat server lokal yang ditampilkan di terminal/browser

## Deployment
Website ini cocok untuk deployment static hosting seperti:
- Netlify
- Vercel
- GitHub Pages

### Deploy ke Netlify (manual)
1. Login ke Netlify.
2. Pilih **Add new site** > **Deploy manually**.
3. Drag and drop folder project (atau connect repository).
4. Publish.

## Catatan Teknis
- Styling dipisah ke file `style.css` agar lebih aman dan maintainable untuk production.
- Pastikan semua path aset tetap relatif (contoh: `aset/logo biru.png`).
- Jika ada perubahan watermark, edit blok `body::before` di `style.css`.

## Kontak
Jika ada kebutuhan update konten/visual, perubahan bisa langsung dilakukan pada:
- `index.html`
- `style.css`

## Catatan Publikasi
README ini tidak memuat secret, token, kredensial, atau path lokal yang sensitif.

