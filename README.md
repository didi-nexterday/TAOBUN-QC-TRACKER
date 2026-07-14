# QC Tracker — Konsistensi Rasa & Kualitas (versi Firebase + GitHub Pages)

Tracker QC untuk 3 cabang F&B. Data tersimpan real-time di Firestore (Firebase),
tampilan di-hosting gratis lewat GitHub Pages.

## Yang Anda butuhkan
- Akun Google (untuk Firebase — gratis)
- Akun GitHub (gratis)
- Tidak perlu bisa coding — tinggal salin-tempel

---

## Langkah 1 — Buat project Firebase

1. Buka https://console.firebase.google.com
2. Klik **Add project**, beri nama misalnya `qc-tracker-fnb`, lanjutkan sampai selesai
   (Google Analytics boleh dimatikan, tidak diperlukan)
3. Di sidebar kiri, klik **Build > Firestore Database** → **Create database**
   → pilih **Start in production mode** → pilih lokasi server terdekat (misal `asia-southeast2`) → Enable
4. Setelah Firestore aktif, buka tab **Rules** di halaman Firestore, ganti isinya dengan
   isi file `firestore.rules` yang ada di folder ini, lalu klik **Publish**
   (rules ini membatasi akses hanya untuk baca/tulis data QC, bukan seluruh database)
5. Kembali ke halaman utama project → klik ikon **⚙️ Project settings**
6. Scroll ke bagian **Your apps** → klik ikon web `</>` → beri nama app (bebas) → **Register app**
7. Firebase akan menampilkan blok kode `firebaseConfig = { apiKey: "...", ... }` —
   **salin seluruh blok ini**, akan dipakai di Langkah 2

## Langkah 2 — Isi config di index.html

1. Buka file `index.html` di folder ini
2. Cari bagian berikut (ada di dalam tag `<script type="module">`):
   ```js
   const firebaseConfig = {
     apiKey: "GANTI_DENGAN_API_KEY",
     authDomain: "GANTI.firebaseapp.com",
     projectId: "GANTI_PROJECT_ID",
     storageBucket: "GANTI.appspot.com",
     messagingSenderId: "GANTI",
     appId: "GANTI"
   };
   ```
3. Ganti seluruh blok ini dengan config yang Anda salin dari Firebase di Langkah 1
4. Simpan file

## Langkah 3 — Push ke GitHub

1. Buat repository baru di https://github.com/new (nama bebas, misal `qc-tracker-fnb`, set **Public**)
2. Upload `index.html` dan `firestore.rules` ke repo tersebut
   (paling gampang: klik **Add file > Upload files** di halaman repo, lalu drag & drop)
3. Buka tab **Settings** di repo → sidebar **Pages**
4. Di bagian **Branch**, pilih `main` dan folder `/ (root)` → **Save**
5. Tunggu 1-2 menit, GitHub akan menampilkan link seperti:
   `https://namauser.github.io/qc-tracker-fnb/`
6. Link ini yang dibagikan ke tim di 3 cabang — bisa dibuka dari HP atau laptop

## Cara pakai sehari-hari

Sama seperti versi sebelumnya: shift leader tiap cabang buka link, isi skor 1-5
untuk rasa, porsi, presentasi, kebersihan, dan suhu penyajian. Data langsung
tersimpan di Firestore dan muncul real-time di semua perangkat yang membuka link
yang sama. Dashboard ringkasan otomatis menandai cabang dengan rata-rata di bawah
4.0 sebagai "Perlu tindakan".

## Catatan keamanan

`firestore.rules` yang disertakan mengizinkan siapa saja yang punya link untuk
membaca dan menulis data QC (tanpa login) — cukup untuk pemakaian internal tim.
Kalau nanti butuh lebih ketat (misal setiap shift leader harus login dulu), Firebase
punya fitur **Authentication** yang bisa ditambahkan — bisa dibantu kalau
dibutuhkan.

## Biaya

Firestore punya kuota gratis (Spark plan) yang cukup besar untuk pemakaian
3 cabang — puluhan ribu baca/tulis per hari gratis. Untuk skala 3 cabang,
kemungkinan besar tidak akan kena biaya sama sekali.
