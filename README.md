# 🌿 Jamu Herbal Alami — Web Store

Toko online jamu herbal dengan sistem login, admin panel tersembunyi, dan realtime Firebase.

---

## 📁 Struktur File

```
├── index.html          # Storefront utama (produk, order, cek pesanan)
├── admin.html          # Admin panel (protected — hanya role=admin)
├── firebase-rules.json # Rules untuk Firebase Realtime Database
└── README.md
```

---

## 🚀 Deploy ke GitHub Pages

### Langkah 1 — Upload ke GitHub

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/USERNAME/REPO-NAME.git
git push -u origin main
```

### Langkah 2 — Aktifkan GitHub Pages

1. Buka repo di GitHub
2. Klik **Settings** → **Pages**
3. Di bagian **Source**, pilih branch `main` dan folder `/ (root)`
4. Klik **Save**
5. Website akan live di: `https://USERNAME.github.io/REPO-NAME/`

---

## 🔥 Setup Firebase

### 1. Firebase Authentication
Di [Firebase Console](https://console.firebase.google.com) → Authentication → Sign-in method:
- ✅ Aktifkan **Email/Password**
- ✅ Aktifkan **Google** (opsional)

### 2. Buat Akun Admin
Ada 2 cara:

**Cara A — Via Firebase Console (Recommended):**
1. Auth → Users → Add User
2. Masukkan email dan password admin
3. Salin UID-nya
4. Realtime Database → (klik `+`) tambahkan:
```
users/
  {UID_ADMIN}/
    nama: "Admin"
    email: "email@kamu.com"
    role: "admin"   ← ⚠️ INI YANG PENTING
    createdAt: 1234567890
```

**Cara B — Daftar dulu via website, lalu set role:**
1. Daftar akun biasa via `index.html`
2. Di Firebase Console → Realtime Database → users → {uid} → tambah field `role: "admin"`

### 3. Pasang Firebase Rules
1. Firebase Console → Realtime Database → **Rules**
2. Copy-paste isi `firebase-rules.json`
3. Klik **Publish**

> ⚠️ **PENTING:** Tanpa rules yang benar, siapapun bisa baca/tulis database kamu!

---

## 🔐 Sistem Keamanan Admin

- `admin.html` **tidak bisa diakses** tanpa login
- Setelah login, sistem cek `users/{uid}/role` di Firebase
- Kalau bukan `admin` → langsung dikeluarkan, halaman tersembunyi
- Link Admin Panel di navbar `index.html` **hanya muncul** untuk akun dengan `role: "admin"`
- Setiap login/logout admin dicatat di node `admin_log`

---

## 📦 Fitur

### Storefront (index.html)
- 🌿 Tampil produk dari Firebase secara realtime
- 🛒 Sistem order dengan ID unik & expiry 10 menit
- 🔍 Cek status pesanan realtime
- ⭐ Sistem ulasan/testimoni
- 🔐 Login / Daftar / Lupa Password (Firebase Auth)
- 📋 Riwayat pesanan per user

### Admin Panel (admin.html)
- 📊 Dashboard statistik (produk, pesanan, omzet)
- 📦 CRUD produk (tambah/edit/hapus + multi foto)
- 🛒 Manajemen pesanan + ubah status + notif WA otomatis
- 💰 Konfirmasi pembayaran instan
- ⭐ Kelola testimoni
- ⚙️ Pengaturan rekening & nomor WA
- 📥 Export CSV laporan pesanan
- 🔒 Login audit log

---

## ⚙️ Konfigurasi

Ubah konfigurasi Firebase di kedua file jika pakai project berbeda:

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    databaseURL: "https://YOUR_PROJECT-default-rtdb.REGION.firebasedatabase.app",
    projectId: "YOUR_PROJECT",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

Ubah nomor WhatsApp default:
```javascript
let OWNER_WA = "628XXXXXXXXXX";  // Format: 62 + nomor tanpa 0 depan
```

---

## 📱 Custom Domain (Opsional)

Kalau punya domain sendiri, bisa pakai GitHub Pages custom domain:
1. Settings → Pages → Custom domain → masukkan domain kamu
2. Buat file `CNAME` berisi nama domain:
```
tokomu.com
```

---

Made with ❤️ for Indonesia 🌿
