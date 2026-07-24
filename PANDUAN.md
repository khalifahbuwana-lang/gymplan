# GymPlan — Panduan Pasang (Akun Cloud + Hosting Gratis)

Aplikasi ini adalah **PWA**: satu situs web yang bisa dipasang di layar HP seperti aplikasi biasa, dengan **akun** dan **data tersimpan di cloud** (sinkron di semua perangkat). Backend memakai **Supabase** (gratis), hosting memakai **Netlify** atau **GitHub Pages** (gratis).

Total waktu: ± 15 menit. Tidak perlu bisa coding.

Isi folder `GymPlan_app`:
- `index.html` — aplikasinya
- `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png` — pelengkap PWA
- `supabase-setup.sql` — skrip database
- `PANDUAN.md` — file ini

---

## BAGIAN A — Buat backend (Supabase)

1. Buka **https://supabase.com** → **Start your project** → daftar (bisa pakai akun GitHub/Google).
2. Klik **New project**. Isi nama (mis. `gymplan`), buat password database (catat saja), pilih region terdekat (Singapore), lalu **Create new project**. Tunggu ± 1–2 menit.
3. Di menu kiri buka **SQL Editor** → **New query**. Buka file `supabase-setup.sql`, salin **semua** isinya ke editor, lalu **Run**. Harus muncul "Success".
4. (Disarankan, biar login instan) Menu kiri **Authentication → Sign In / Providers → Email**: matikan **Confirm email**, lalu Save. *(Kalau dibiarkan aktif, tiap pendaftar harus klik link konfirmasi di email dulu — tetap bisa, hanya kurang praktis.)*
5. Menu kiri **Project Settings → API**. Catat dua nilai ini:
   - **Project URL** — mis. `https://abcd1234.supabase.co`
   - **anon public** key — teks panjang di bagian "Project API keys".

---

## BAGIAN B — Masukkan kunci ke aplikasi

1. Buka `index.html` dengan aplikasi teks apa saja (Notepad, TextEdit, VS Code).
2. Cari (Ctrl/Cmd+F) tulisan `GANTI_DENGAN`. Ada 2 baris di dekat atas bagian script:

   ```js
   const SUPABASE_URL      = "GANTI_DENGAN_URL_SUPABASE";
   const SUPABASE_ANON_KEY = "GANTI_DENGAN_ANON_KEY";
   ```

3. Ganti isinya dengan nilai dari Bagian A langkah 5 (tetap di dalam tanda kutip), contoh:

   ```js
   const SUPABASE_URL      = "https://abcd1234.supabase.co";
   const SUPABASE_ANON_KEY = "eyJhbGciOi...panjang...";
   ```

4. **Simpan** file. (Anon key memang aman ditaruh di sisi klien — keamanan dijaga oleh Row Level Security yang sudah dibuat skrip SQL.)

---

## BAGIAN C — Hosting (pilih salah satu)

### Opsi 1 — Netlify Drop (paling cepat, tanpa akun)
1. Buka **https://app.netlify.com/drop**.
2. **Seret seluruh folder `GymPlan_app`** ke area itu.
3. Selesai — kamu dapat URL seperti `https://nama-acak.netlify.app`. Itu alamat aplikasimu.
4. (Opsional) daftar Netlify gratis agar situs tidak kedaluwarsa & bisa ganti nama.

### Opsi 2 — GitHub Pages
1. Buat akun **github.com** → **New repository** (mis. `gymplan`), set **Public**.
2. **Add file → Upload files** → unggah semua isi folder `GymPlan_app` → **Commit**.
3. **Settings → Pages** → Source: **Deploy from a branch** → Branch `main` / folder `/root` → Save.
4. Tunggu ± 1 menit; URL muncul: `https://namakamu.github.io/gymplan/`.

> Penting: file utama harus bernama **index.html** (sudah). PWA butuh **HTTPS** — Netlify & GitHub Pages sudah otomatis HTTPS.

---

## BAGIAN D — Pasang di HP

1. Buka URL hasil Bagian C di browser HP (**Chrome** untuk Android, **Safari** untuk iPhone).
2. Pasang ke layar utama:
   - **Android/Chrome**: menu ⋮ → **Add to Home screen / Install app**.
   - **iPhone/Safari**: tombol Share ⬆️ → **Add to Home Screen**.
3. Buka ikon GymPlan dari home screen → **Daftar** (email + password) → mulai pakai.
4. Login dengan akun sama di HP/perangkat lain → semua data (profil, log set, scan) otomatis muncul.

---

## Catatan
- **Belum sempat setup cloud?** Aplikasi tetap bisa dipakai: di layar awal pilih **"Pakai tanpa akun (data lokal HP)"**. Data tersimpan di HP itu saja.
- **Status sinkron** terlihat di pojok kanan atas ("tersimpan ✓" / "offline — tersimpan di HP").
- **Lupa/ganti perangkat**: cukup login lagi, data ditarik dari cloud.
- **Gratis**: Supabase free tier & Netlify/GitHub Pages sangat cukup untuk pemakaian pribadi/keluarga.
- **Update aplikasi**: ganti `index.html` di hosting; di HP tarik-segarkan / buka ulang. (Naikkan `gymplan-v1` → `gymplan-v2` di `sw.js` bila ingin memaksa perbarui cache.)
