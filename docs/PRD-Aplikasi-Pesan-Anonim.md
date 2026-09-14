# PRD: Aplikasi Pesan Anonim (Codename: "Anonly")

| | |
|---|---|
| **Versi Dokumen** | 1.0 |
| **Tanggal** | 12 September 2026 |
| **Status** | Draft |
| **Stack** | Vue.js, Firebase (Auth, Firestore, Hosting, Functions), Cloudflare Turnstile |

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
- Tidak ada aplikasi mobile native — fokus web app responsif dulu.

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
- FR-3: Halaman profil sederhana untuk mengubah username (dengan cooldown, misal 1x per 30 hari, agar tautan lama tidak mudah "dibajak").

### 5.2 Tautan Publik & Pengiriman Pesan
- FR-4: URL publik berformat `domain.com/u/{username}`, dapat diakses tanpa login.
- FR-5: Halaman publik menampilkan form: textarea pesan (limit karakter, misal 500) + tombol kirim.
- FR-6: Sebelum submit, sender wajib lolos **Cloudflare Turnstile** (invisible/managed mode).
- FR-7: Setelah terkirim, tampilkan konfirmasi "Pesan terkirim" tanpa redirect yang membocorkan status ke recipient.
- FR-8: Sistem TIDAK menyimpan/menampilkan identitas sender (nama, akun, email) ke recipient dalam bentuk apa pun di UI.

### 5.3 Kotak Masuk (Inbox)
- FR-9: Recipient login → dashboard menampilkan daftar pesan, urut dari terbaru.
- FR-10: Status "belum dibaca" vs "sudah dibaca".
- FR-11: Recipient dapat menghapus pesan individual.
- FR-12: Recipient dapat melaporkan pesan (submit ke koleksi `reports`).

### 5.4 Moderasi & Anti-Abuse
- FR-13: Filter kata kasar/dilarang dijalankan di Firebase Cloud Function sebelum pesan disimpan (server-side, bukan client-side, agar tidak bisa dilewati).
- FR-14: Rate limiting per IP/device: maksimum N pesan per menit ke recipient yang sama (disarankan mulai dari 5/menit, disesuaikan setelah observasi).
- FR-15: Verifikasi token Turnstile divalidasi di server (Cloud Function) via Cloudflare Siteverify API — **jangan** percaya validasi dari client saja.

## 6. Non-Functional Requirements

| Kategori | Requirement |
|---|---|
| **Keamanan** | Firestore Security Rules memastikan sender tidak bisa membaca koleksi `messages` milik siapa pun; hanya Cloud Function (admin SDK) yang boleh menulis pesan setelah validasi Turnstile. |
| **Privasi** | Metadata sender (IP hash, user-agent) disimpan terpisah di koleksi internal yang tidak bisa diakses dari client, hanya untuk investigasi kasus penyalahgunaan berat. |
| **Performa** | Halaman publik pengirim harus load < 2 detik (statis/SSR ringan) karena traffic dari link viral bisa tinggi tapi sesaat. |
| **Skalabilitas** | Firestore + Cloud Functions dipilih karena auto-scaling; pantau kuota Cloud Functions saat traffic spike. |
| **Ketersediaan** | Uptime target 99.5% (bergantung pada SLA Firebase). |

## 7. Arsitektur Teknis

```
[Vue.js SPA/SSR]
   |-- Halaman Publik (/u/:username)  --> Cloudflare Turnstile widget
   |-- Halaman Auth (login/register)  --> Firebase Auth SDK
   |-- Dashboard Inbox                --> Firestore (read, real-time listener)
        |
        v
[Firebase Cloud Functions] (HTTPS Callable)
   |-- validateAndSubmitMessage()
   |     1. Terima payload: { username, content, turnstileToken }
   |     2. Verifikasi token ke Cloudflare Siteverify API
   |     3. Cek rate limit (berdasar IP hash, simpan di Firestore/Redis)
   |     4. Jalankan filter kata kasar
   |     5. Tulis ke koleksi `messages` dengan recipientId, TANPA data sender
   |
[Firestore]
   |-- users/{uid}
   |-- messages/{messageId}
   |-- reports/{reportId}
   |-- rateLimits/{ipHash}  (internal, tidak bisa diakses client)
```

**Alasan pesan tidak ditulis langsung dari client ke Firestore:** agar validasi Turnstile, rate limit, dan filter konten tidak bisa dilewati (client-side rules mudah dimanipulasi). Semua logic sensitif ditaruh di Cloud Function.

## 8. Skema Data (Firestore)

```
users (collection)
  {uid} (doc)
    - username: string (unique, indexed)
    - email: string
    - createdAt: timestamp
    - photoURL: string | null

messages (collection)
  {messageId} (doc)
    - recipientId: string (ref -> users.uid)
    - content: string
    - isRead: boolean (default false)
    - createdAt: timestamp
    - flagged: boolean (default false, diisi otomatis jika filter kata kasar mendeteksi sesuatu yang borderline)

reports (collection)
  {reportId} (doc)
    - messageId: string
    - reporterId: string (uid recipient yang lapor)
    - reason: string
    - createdAt: timestamp

rateLimits (collection, internal-only, tidak ada security rule akses client)
  {ipHash} (doc)
    - count: number
    - windowStart: timestamp
    - lastRecipientId: string
```

### Firestore Security Rules (ringkasan)
- `users/{uid}`: read publik (untuk cek username tersedia/tidak), write hanya oleh owner.
- `messages/{id}`: read hanya oleh `recipientId == request.auth.uid`; **create ditolak dari client**, hanya via Cloud Function (Admin SDK bypass rules).
- `reports/{id}`: create oleh authenticated user; read hanya oleh admin/moderator.
- `rateLimits/{id}`: tidak ada akses client sama sekali (read maupun write).

## 9. Metrik Keberhasilan (Success Metrics)

| Metrik | Target Awal |
|---|---|
| Jumlah akun terdaftar (30 hari pertama) | Baseline, pantau growth mingguan |
| Rasio sender-to-recipient (viralitas) | > 3 pesan per akun aktif |
| Tingkat pesan yang di-flag/reported | < 2% dari total pesan |
| Bounce rate halaman publik pengirim | < 40% |
| Waktu load halaman publik | < 2 detik (p75) |

## 10. Risiko & Mitigasi

| Risiko | Mitigasi |
|---|---|
| Penyalahgunaan untuk cyberbullying/ancaman | Filter konten server-side, fitur report, kebijakan privasi jelas soal penyimpanan IP untuk kasus hukum |
| Bot spam massal | Cloudflare Turnstile + rate limiting per IP/device di server |
| Username squatting (rebutan nama bagus) | Cooldown ganti username, mungkin verifikasi tambahan untuk username premium di masa depan |
| Biaya Firebase membengkak saat viral | Pantau kuota Firestore reads/writes & Cloud Functions invocations, set budget alert di GCP |

## 11. Roadmap Rilis

- **v1.0 (MVP):** FR-1 s/d FR-15 seperti di atas.
- **v1.1:** Notifikasi email saat ada pesan baru, statistik dasar di dashboard.
- **v1.2:** Fitur "reply" berupa generate gambar untuk dibagikan ke Instagram/WhatsApp Story.
- **v2.0:** Panel admin/moderator untuk menangani laporan secara terpusat.

## 12. Open Questions

- Apakah perlu batas usia minimum / disclaimer terkait konten sensitif?
- Apakah pesan yang di-flag otomatis langsung diblokir, atau tetap masuk inbox dengan label "berpotensi tidak pantas"?
- Domain & branding final untuk produk ini?
