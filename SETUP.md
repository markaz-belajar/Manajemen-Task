# Panduan Setup — Markaz Belajar

Aplikasi ini berjalan sepenuhnya di browser. Data disimpan di Google Drive pribadi Anda.  
Tidak ada server. Tidak ada database pihak ketiga.

---

## Langkah 1 — Upload ke GitHub

1. Buat akun di [github.com](https://github.com) jika belum punya
2. Klik **New repository**
3. Nama repo: `markaz-belajar` (atau apapun)
4. Pilih **Public**
5. Klik **Create repository**
6. Upload ketiga file ini: `index.html`, `config.js`, `SETUP.md`
7. Masuk ke **Settings → Pages**
8. Di bagian *Source*, pilih **Deploy from a branch → main → / (root)**
9. Klik **Save**
10. Tunggu 1–2 menit, lalu URL Anda akan aktif:
    ```
    https://USERNAME.github.io/markaz-belajar/
    ```
    Catat URL ini — Anda butuhkan di Langkah 2.

---

## Langkah 2 — Buat Google OAuth Client ID

1. Buka [console.cloud.google.com](https://console.cloud.google.com)
2. Klik dropdown project di atas → **New Project**
   - Nama: `Markaz Belajar`
   - Klik **Create**
3. Pastikan project `Markaz Belajar` aktif (cek dropdown atas)
4. Di menu kiri, masuk ke **APIs & Services → Library**
5. Cari **Google Drive API** → klik → klik **Enable**
6. Di menu kiri, masuk ke **APIs & Services → OAuth consent screen**
   - Pilih **External** → klik **Create**
   - Isi:
     - App name: `Markaz Belajar`
     - User support email: email Anda
     - Developer contact: email Anda
   - Klik **Save and Continue** di setiap langkah (boleh skip yang opsional)
   - Di halaman **Test users** → klik **Add users** → masukkan email Google Anda
   - Klik **Save and Continue** → **Back to Dashboard**
7. Di menu kiri, masuk ke **APIs & Services → Credentials**
8. Klik **+ Create Credentials → OAuth client ID**
   - Application type: **Web application**
   - Name: `Markaz Belajar Web`
   - Di bagian **Authorized JavaScript origins**, klik **Add URI** dan masukkan:
     ```
     https://USERNAME.github.io
     ```
     (ganti USERNAME dengan username GitHub Anda — tanpa slash di akhir)
   - Jika ingin test di lokal, tambahkan juga:
     ```
     http://localhost
     http://localhost:5500
     ```
   - Klik **Create**
9. Akan muncul popup **Your Client ID** — salin nilainya, contoh:
    ```
    123456789-abcdefghijklmnop.apps.googleusercontent.com
    ```

---

## Langkah 3 — Isi config.js

1. Buka file `config.js`
2. Ganti `YOUR_CLIENT_ID_HERE.apps.googleusercontent.com` dengan Client ID yang baru Anda salin:
    ```javascript
    const GOOGLE_CLIENT_ID = "123456789-abcde.apps.googleusercontent.com";
    ```
3. Simpan file
4. Upload ulang `config.js` ke GitHub (atau edit langsung via GitHub web)

---

## Langkah 4 — Buka Aplikasi

1. Buka URL GitHub Pages Anda:
    ```
    https://USERNAME.github.io/markaz-belajar/
    ```
2. Klik **Masuk dengan Google**
3. Pilih akun Google Anda
4. Izinkan akses ke Google Drive
5. Selesai — aplikasi siap digunakan!

---

## Cara Kerja Penyimpanan

| Apa | Di mana |
|---|---|
| Data tugas & kelompok | File `markaz-belajar-data.json` di Google Drive Anda |
| Dokumen yang diupload | Folder root Google Drive Anda, dengan nama `[MB-ID] namafile.pdf` |
| Repositori dokumen | Dibaca langsung dari data Drive |

Untuk berbagi akses dengan tim (ALI, ELIS, YESSI):
- Masing-masing orang **login dengan akun Google mereka sendiri**
- Setiap orang memiliki data & Drive masing-masing
- Nama pengerja tugas tersimpan otomatis dari nama akun Google

> **Catatan:** Saat ini app ini berada dalam mode *Testing* di Google. Artinya hanya akun yang Anda daftarkan di *Test Users* (Langkah 2 poin 6) yang bisa login. Jika ingin semua orang bisa login tanpa perlu didaftarkan, Anda perlu submit app untuk *Verification* di Google — tapi untuk penggunaan internal tim kecil, mode Testing sudah cukup.

---

## Troubleshooting

| Masalah | Solusi |
|---|---|
| "Access blocked: Authorization Error" | Pastikan Client ID sudah benar di `config.js` dan URL GitHub Pages sudah ditambahkan di *Authorized origins* |
| Tombol login tidak muncul / spinner terus | Pastikan Google Drive API sudah di-*Enable* |
| Upload gagal | Cek koneksi internet, atau coba login ulang |
| Data tidak tersimpan | Pastikan Anda sudah login Google dan ada koneksi internet |
