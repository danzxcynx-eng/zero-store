# Zero Store — versi production-ready

Ini bukan versi demo: listing disimpan di Cloudflare D1, akun memakai password hashing PBKDF2, sesi memakai cookie HttpOnly, dan listing dapat dipublikasikan melalui API.

## Struktur
- `public/index.html` — website
- `worker.js` — backend API
- `schema.sql` — database
- `wrangler.toml` — konfigurasi Cloudflare Workers

## Deploy Cloudflare

1. Buat D1 Database bernama `zero-store-db`.
2. Jalankan `schema.sql` pada database tersebut.
3. Salin Database ID ke `wrangler.toml`.
4. Pastikan `public/index.html` berada di folder `public/`.
5. Deploy project dengan Wrangler:
   `npx wrangler deploy`
6. Setelah deploy, buka domain Workers kamu.

Jika kamu menggunakan dashboard Cloudflare tanpa terminal, cara termudah adalah memakai GitHub dan menghubungkan repository ke Workers Builds, lalu menambahkan D1 binding `DB` pada Settings > Bindings.

## Catatan penting sebelum dibuka untuk publik
- Untuk foto barang, versi ini menerima URL gambar. Untuk marketplace produksi, sebaiknya pindahkan upload gambar ke Cloudflare R2.
- Untuk pembayaran/escrow, integrasikan payment gateway resmi; jangan menyimpan data kartu di aplikasi.
- Tambahkan verifikasi email, rate limiting, moderasi listing, laporan penipuan, dan backup database sebelum transaksi bernilai tinggi.
- Nomor WhatsApp dipublikasikan pada listing agar pembeli dapat menghubungi penjual.
