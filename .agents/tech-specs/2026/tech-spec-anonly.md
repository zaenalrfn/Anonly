# Tech Spec: Anonly (Nuxt.js + Firebase)

| | |
|---|---|
| **Status** | Approved / Implementation Ready |
| **Stack** | Nuxt 4, Vue 3, Firebase (Auth, Firestore, Cloud Functions), Cloudflare Turnstile |
| **Date** | 14 September 2026 |

---

## 1. Arsitektur Sistem & Direktori Proyek (Nuxt 4)

Proyek menggunakan struktur standar Nuxt 4 dengan TypeScript:

```
anonly/
├── app/
│   ├── pages/
│   │   ├── index.vue              # Landing page
│   │   ├── login.vue              # Login & Register (Firebase Auth)
│   │   ├── dashboard.vue          # Inbox & manajemen pesan
│   │   └── u/
│   │       └── [username].vue     # Halaman publik pengirim pesan
│   ├── components/                # UI components (Tailwind CSS / Nuxt UI)
│   └── composables/               # Firebase composables (useAuth, useFirestore)
├── server/
│   └── api/                       # Nitro server routes (alternatif / pendukung Cloud Functions)
├── functions/                     # Firebase Cloud Functions (Node.js / TypeScript)
│   └── src/
│       └── index.ts               # validateAndSubmitMessage endpoint
├── nuxt.config.ts
└── package.json
```

---

## 2. Skema Database Firestore

### 2.1 Koleksi `users`
- **Document ID:** `uid` (dari Firebase Auth)
- **Fields:**
  - `username`: string (unique, indexed)
  - `email`: string
  - `createdAt`: timestamp
  - `photoURL`: string | null

### 2.2 Koleksi `messages`
- **Document ID:** `messageId` (auto-generated)
- **Fields:**
  - `recipientId`: string (ref -> users.uid)
  - `content`: string (max 500 chars)
  - `isRead`: boolean (default: `false`)
  - `createdAt`: timestamp
  - `flagged`: boolean (default: `false`)

### 2.3 Koleksi `reports`
- **Document ID:** `reportId` (auto-generated)
- **Fields:**
  - `messageId`: string
  - `reporterId`: string
  - `reason`: string
  - `createdAt`: timestamp

### 2.4 Koleksi `rateLimits` (Internal-only)
- **Document ID:** `ipHash` (sha256 IP address)
- **Fields:**
  - `count`: number
  - `windowStart`: timestamp
  - `lastRecipientId`: string

---

## 3. Alur Pengiriman Pesan & Validasi Anti-Abuse

1. **Client Request:**
   - Pengunjung mengakses `/u/{username}`.
   - Mengisi textarea pesan dan menyelesaikan challenge **Cloudflare Turnstile**.
   - Client mengirim request HTTPS Callable / API ke Cloud Function: `{ username, content, turnstileToken }`.

2. **Server-Side Validation (Cloud Function / Nitro API):**
   - **Step 1:** Verifikasi `turnstileToken` ke endpoint `https://challenges.cloudflare.com/turnstile/v0/siteverify`.
   - **Step 2:** Cek rate limit berdasarkan hash IP di koleksi `rateLimits` (maksimal 5 pesan / menit ke recipient yang sama).
   - **Step 3:** Filter kata kasar sederhana pada variabel `content`.
   - **Step 4:** Cari `recipientId` berdasarkan `username`.
   - **Step 5:** Tulis dokumen baru ke koleksi `messages` menggunakan Firebase Admin SDK (bypass security rules).

---

## 4. Firestore Security Rules

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    
    // Users: Public read (untuk cek ketersediaan username), write hanya oleh owner
    match /users/{userId} {
      allow read: if true;
      allow write: if request.auth != null && request.auth.uid == userId;
    }
    
    // Messages: Read hanya oleh recipient pemilik pesan. Write ditolak dari client (hanya Cloud Functions / Admin SDK)
    match /messages/{messageId} {
      allow read: if request.auth != null && resource.data.recipientId == request.auth.uid;
      allow write: if false;
    }
    
    // Reports: Auth user dapat membuat report
    match /reports/{reportId} {
      allow create: if request.auth != null;
      allow read: if false; // Hanya admin
    }
    
    // RateLimits: Tidak ada akses dari client sama sekali
    match /rateLimits/{rateLimitId} {
      allow read, write: if false;
    }
  }
}
```

---

## 5. Rencana Implementasi Bertahap
1. **Inisialisasi Project:** Setup Nuxt 4 + Firebase SDK.
2. **Autentikasi:** Halaman Login/Register dengan Firebase Auth.
3. **Halaman Publik:** Pembuatan halaman `/u/[username].vue` dengan Cloudflare Turnstile.
4. **Backend / Cloud Function:** Endpoint submit pesan dengan validasi Turnstile & rate limit.
5. **Dashboard Inbox:** Tampilan pesan masuk, fitur read/unread, delete, dan report.
