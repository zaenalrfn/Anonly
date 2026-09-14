# PRD: Aplikasi Pesan Anonim (Codename: "Anonly")

| | |
|---|---|
| **Versi Dokumen** | 1.0 |
| **Tanggal** | 14 September 2026 |
| **Status** | Draft / Active |
| **Stack** | Nuxt.js (Nuxt 4), Firebase (Auth, Firestore, Hosting, Cloud Functions), Cloudflare Turnstile |

---

## 1. Latar Belakang
Aplikasi ini terinspirasi dari NGL.link — memungkinkan seorang pengguna (recipient) membagikan tautan pribadi ke media sosial, sehingga siapa pun (sender) dapat mengirim pesan teks secara **anonim** kepadanya. Recipient hanya dapat membaca isi pesan, tanpa mengetahui identitas pengirim.

## 2. Tujuan Produk
- Memungkinkan pengguna membuat akun dan mendapatkan tautan unik untuk dibagikan.
- Memungkinkan siapa pun mengirim pesan teks tanpa perlu login/registrasi.
- Menjamin anonimitas pengirim secara teknis (bukan hanya di tampilan UI).
- Mencegah penyalahgunaan (spam, bot, konten berbahaya) melalui Cloudflare Turnstile dan rate limiting.

### 2.1 Non-Goals (di luar cakupan versi 1.0)
- Tidak ada fitur chat dua arah (reply tidak terkirim balik ke sender).
- Tidak ada fitur monetisasi (langganan premium, "hint" siapa pengirim, dsb).
- Tidak ada aplikasi mobile native — fokus web app responsif (Nuxt.js SSR) dulu.

## 3. Target Pengguna
- Remaja/dewasa muda yang aktif di Instagram/WhatsApp Story dan suka format interaksi "tanya-jawab anonim".
- Pengguna umum yang ingin menerima kritik/saran/curhat secara anonim dari circle pertemanan.

## 4. User Stories

| ID | Sebagai | Saya ingin | Agar |
|---|---|---|---|
| US-1 | Pengguna baru | Mendaftar dan memilih username unik | Punya tautan pribadi untuk dibagikan |
| US-2 | Pengguna terdaftar | Menyalin/membagikan tautan saya | Orang lain bisa mengirim pesan ke saya |
| US-3 | Pengirim (tanpa akun) | Membuka tautan dan mengisi pesan | Pesan saya sampai tanpa perlu daftar |
| US-4 | Pengirim | Melewati verifikasi manusia yang cepat | Tidak terganggu tapi tetap terhindar dari bot |
| US-5 | Pengguna terdaftar | Melihat daftar pesan masuk | Membaca semua pesan yang dikirim ke saya |
| US-6 | Pengguna terdaftar | Melaporkan pesan yang tidak pantas | Membantu moderasi konten berbahaya |
| US-7 | Pengguna terdaftar | Menghapus pesan | Mengelola kotak masuk saya sendiri |

## 5. Functional Requirements (MVP)

### 5.1 Autentikasi & Akun
- FR-1: Registrasi via Email/Password dan Google OAuth (Firebase Auth).
- FR-2: Setiap akun memiliki `username` unik (case-insensitive, alfanumerik + underscore), dicek real-time saat dibuat.
- FR-3: Halaman profil sederhana untuk mengubah username (dengan cooldown, misal 1x per 30 hari).

### 5.2 Tautan Publik & Pengiriman Pesan
- FR-4: URL publik berformat `domain.com/u/{username}`, dapat diakses tanpa login (di-render via Nuxt.js SSR).
- FR-5: Halaman publik menampilkan form: textarea pesan (limit 500 karakter) + tombol kirim.
- FR-6: Sebelum submit, sender wajib lolos **Cloudflare Turnstile** (invisible/managed mode).
- FR-7: Setelah terkirim, tampilkan konfirmasi "Pesan terkirim" tanpa redirect yang membocorkan status ke recipient.
- FR-8: Sistem TIDAK menyimpan/menampilkan identitas sender (nama, akun, email) ke recipient dalam bentuk apa pun di UI.

### 5.3 Kotak Masuk (Inbox)
- FR-9: Recipient login → dashboard Nuxt menampilkan daftar pesan, urut dari terbaru.
- FR-10: Status "belum dibaca" vs "sudah dibaca".
- FR-11: Recipient dapat menghapus pesan individual.
- FR-12: Recipient dapat melaporkan pesan (submit ke koleksi `reports`).

### 5.4 Moderasi & Anti-Abuse
- FR-13: Filter kata kasar/dilarang dijalankan di Firebase Cloud Function sebelum pesan disimpan.
- FR-14: Rate limiting per IP/device: maksimum N pesan per menit ke recipient yang sama.
- FR-15: Verifikasi token Turnstile divalidasi di server (Cloud Function) via Cloudflare Siteverify API.

## 6. Non-Functional Requirements

| Kategori | Requirement |
|---|---|
| **Keamanan** | Firestore Security Rules memastikan sender tidak bisa membaca koleksi `messages` milik siapa pun; hanya Cloud Function (admin SDK) yang boleh menulis pesan setelah validasi Turnstile. |
| **Privasi** | Metadata sender (IP hash, user-agent) disimpan terpisah di koleksi internal yang tidak bisa diakses dari client. |
| **Performa** | Halaman publik pengirim harus load < 1.5 detik (Nuxt.js SSR). |
| **Skalabilitas** | Firestore + Cloud Functions + Nuxt on Vercel/Firebase Hosting. |

## 7. Arsitektur Teknis
- **Frontend:** Nuxt.js (SSR / SPA)
- **Backend:** Firebase Cloud Functions (HTTPS Callable)
- **Database:** Firestore (`users`, `messages`, `reports`, `rateLimits`)
- **Keamanan:** Cloudflare Turnstile + Firestore Rules

## 8. Roadmap Rilis
- **v1.0 (MVP):** FR-1 s/d FR-15 dengan Nuxt.js & Firebase.
- **v1.1:** Notifikasi email saat ada pesan baru.
- **v1.2:** Fitur "reply" berupa generate gambar untuk Instagram/WhatsApp Story.
