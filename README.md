# SISTEM PENTAKSIRAN PROGRAM BIG
**Hak Cipta Terpelihara © 2026 Unit Kokurikulum, IPG Kampus Darulaman.**

> **Penafian:** Sistem ini untuk kegunaan dalaman Unit Kokurikulum IPG Kampus Darulaman **sahaja**. Sebarang penyalinan, pengubahsuaian, pengedaran atau penggunaan oleh pihak lain tanpa kebenaran bertulis adalah dilarang. Data peribadi dan kesihatan pelajar adalah SULIT dan tertakluk kepada Akta Perlindungan Data Peribadi 2010.

GitHub Pages (`index.html`) + Google Apps Script (`Code.gs`) + Google Sheet

## Fail

| Fail | Letak di | Fungsi |
|---|---|---|
| `Code.gs` | Editor Apps Script | Backend API |
| `index.html` | GitHub Pages | Web app (telefon & komputer) |

> Nama fail mesti **`index.html`** (huruf kecil). Jika dinamakan `Index.html`, GitHub Pages akan papar 404.

---

## A. Kemas kini Apps Script (URL kekal sama)

1. Buka Google Sheet **BIG_Pentaksiran_2026**, kemudian **Extensions → Apps Script**.
2. Padam semua kod dalam `Code.gs`, tampal kandungan `Code.gs` baharu, dan tekan **Ctrl+S**.
3. **Tukar kod pendaftaran** pada baris ini, dan beri kod itu kepada pensyarah sahaja:
   ```js
   var KOD_DAFTAR = "BIG2026";
   ```
4. Pilih fungsi **setupSpreadsheet** dan klik **Run** sekali. Ini menetapkan lajur No KP dan telefon sebagai teks.
5. **Deploy → Manage deployments → ✏️ Edit → Version: New version → Deploy**.
   URL `/exec` anda kekal sama.

> Jika anda cipta *New deployment* (bukan Edit), URL akan berubah. Anda perlu tukar `GAS_URL` dalam `index.html` juga.

## B. Kemas kini GitHub

1. Dalam repository, buka `index.html` (atau padam `Index.html` lama), klik ✏️, tampal kandungan baharu, dan klik **Commit changes**.
2. `GAS_URL` sudah diisi dengan URL anda:
   `https://script.google.com/macros/s/AKfycbwA93jJ.../exec`
3. Tunggu 1–2 minit, kemudian buka `https://username.github.io/BIG-Pentaksiran-2026/`.

---

## Cara guna

**Pensyarah**
- Kali pertama: klik *Pengguna baharu? Daftar di sini*, kemudian isi nama, peranan, IPG Kampus dan **Kod Pendaftaran**.
- Seterusnya: email dan kata laluan sahaja. Anda kekal log masuk selama 6 jam.
- **Pelajar**: cari, tapis, dan tekan nama pelajar untuk menilai Perkhemahan / Jalinan, mengisi refleksi, melihat borang, atau edit/padam.
- **Laporan**: tapis mengikut siri / status, kemudian tekan **Cetak / PDF**.

**Pelajar**: log masuk dengan No. KP (dengan atau tanpa sengkang), kemudian isi **B1 Akuan Status Kesihatan** dan **C1 Akuan Lepas Tanggung** (item sama seperti e-RAMS), isi refleksi, dan semak status. Selepas menghantar, pelajar boleh **Cetak Borang B1 & C1**.
- Soalan bahagian C (khusus peserta perempuan) hanya dipaparkan kepada pelajar yang Jantina bukan "Lelaki".
- Pelajar yang menjawab YA ditanda **⚠ Kesihatan** dalam senarai pensyarah. Tapis melalui *Ada isu kesihatan (B1)*.
- Senarai soalan B1 terletak dalam `Code.gs` (`B1_SOALAN`). Nama program, tarikh dan institusi C1 lalai ditetapkan di bahagian atas `index.html` (`C1_PROGRAM`, `C1_TARIKH`, `C1_INSTITUSI`).

**e-RAMS (admin/pensyarah sahaja)**: menu **e-RAMS** membuka aplikasi e-RAMS penuh (A1–D4) di dalam sistem ini. Aplikasi itu menggunakan backend dan Sheet e-RAMS sendiri. Pautan ditetapkan melalui `ERAMS_URL` dalam `index.html`.

**Profil pelajar**: pelajar mengemas kini sendiri Siri, Kumpulan, Jawatan dalam kumpulan, No dalam kumpulan, Jantina, Kelas, Angka giliran, No tel kecemasan, alahan dan ubat. Jantina, Siri, Kumpulan dan Jawatan adalah **wajib**. Selagi belum lengkap, ia dipaparkan sebagai tindakan di halaman Utama pelajar. Nama dan No KP hanya boleh ditukar oleh pensyarah.

**Refleksi**: taip jawapan, dan/atau muat naik **PDF** (maks 10MB) jika refleksi panjang.
- PDF disimpan dalam folder Drive **BIG_Refleksi_PDF**, dengan nama fail `NoKP_Nama_refleksi.pdf`. Muat naik baharu menggantikan PDF lama.
- Pautan PDF disimpan di sheet **Refleksi** (lajur `URL_PDF`). Lajur ini ditambah secara automatik pada sheet lama.
- Refleksi dipaparkan bersama markah dan keputusan di: Status pelajar, butiran pelajar (pensyarah), lajur Refleksi dalam Laporan, dan borang cetakan (bahagian C + pautan lampiran PDF).

**Tema**: butang bulat di atas bertukar antara *ikut peranti → cerah → gelap*.

**Telefon**: Chrome → ⋮ → *Add to Home screen* · Safari → Kongsi → *Add to Home Screen*.

---

## Penyelesaian masalah

| Masalah | Penyelesaian |
|---|---|
| "Respons pelayan tidak sah" | Deployment mesti **Execute as: Me**, **Who has access: Anyone** |
| "Sesi tamat" | Log masuk semula (sesi tamat selepas 6 jam) |
| Pensyarah lama tidak dapat log masuk | Kata laluan mesti sama seperti dahulu. Selepas log masuk pertama, kata laluan disimpan dalam bentuk hash |
| Logo tidak kelihatan | Fail logo di Google Drive mesti dikongsi **Anyone with the link → Viewer**. Atau muat naik logo ke repo GitHub dan tukar `LOGO_URL` kepada `"logo.png"` |
| Gambar pelajar tidak kelihatan | Domain ipgm.edu.my mungkin menyekat perkongsian awam. Gambar tetap tersimpan dalam folder Drive **BIG_Gambar_Pelajar** |
| Tetingkap cetak tidak keluar | Benarkan pop-up untuk laman ini |
| No telefon lama hilang sifar depan | Data lama yang telah rosak perlu dibetulkan secara manual dalam Sheet. Data baharu tidak akan rosak lagi |
