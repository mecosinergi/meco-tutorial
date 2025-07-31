Berikut adalah **template siap pakai** untuk `ISSUE_TEMPLATE` dan `PULL_REQUEST_TEMPLATE` yang bisa Anda taruh di dalam folder `.github/` di repository Anda.

---

## 📁 Struktur Folder

```
.github/
├── ISSUE_TEMPLATE/
│   ├── bug_report.md
│   └── feature_request.md
├── PULL_REQUEST_TEMPLATE.md
```

---

## 🐞 `.github/ISSUE_TEMPLATE/bug_report.md`

```markdown
---
name: 🐛 Laporan Bug
about: Laporkan kesalahan atau error di sistem
title: "[BUG] Judul masalah"
labels: bug
assignees: ''

---

## 🧩 Deskripsi Masalah
Jelaskan bug secara jelas dan singkat.

## 🪟 Langkah Reproduksi
Langkah-langkah untuk mereproduksi bug:
1. Buka halaman ...
2. Klik tombol ...
3. Lihat hasil yang salah

## 🧪 Perilaku yang Diharapkan
Jelaskan apa yang seharusnya terjadi.

## 🖼️ Screenshot (jika ada)
Upload gambar jika perlu.

## 🛠️ Informasi Tambahan
- Browser/OS: ...
- Versi Aplikasi: ...
```

---

## ✨ `.github/ISSUE_TEMPLATE/feature_request.md`

```markdown
---
name: ✨ Permintaan Fitur Baru
about: Ajukan ide atau fitur yang dibutuhkan
title: "[FEAT] Judul fitur"
labels: enhancement
assignees: ''

---

## 🔧 Deskripsi Fitur
Apa yang Anda ingin tambahkan?

## 📈 Manfaat / Tujuan
Kenapa fitur ini penting?

## 💡 Alternatif / Catatan Tambahan
Apakah ada solusi atau referensi lainnya?
```

---

## 🔀 `.github/PULL_REQUEST_TEMPLATE.md`

```markdown
# 🚀 Pull Request

## ✅ Ringkasan
Jelaskan perubahan yang Anda buat. Contoh:
- Menambahkan halaman login
- Memperbaiki bug validasi form
- Mengupdate dokumentasi `README.md`

## 🔗 Terkait Issue
Closes #123  
Refs #456

> Gunakan keyword seperti `Closes` atau `Fixes` agar Issue tertutup otomatis saat PR di-merge.

## 🧪 Langkah Uji Coba
- [ ] Saya sudah menjalankan aplikasi dan memverifikasi perubahan
- [ ] Saya sudah memastikan tidak ada file sensitif yang ikut ter-commit
- [ ] Tidak ada konflik dengan branch `main`

## 📸 Screenshot / Bukti
Tambahkan gambar/video jika relevan (opsional)

## 🙏 Reviewer
Silakan review: @username1 @username2
```

---

## 📌 Langkah Penerapan

1. Buat folder `.github` di root repo Anda.
2. Buat folder `ISSUE_TEMPLATE` di dalamnya.
3. Letakkan file `bug_report.md` dan `feature_request.md` di dalam `ISSUE_TEMPLATE/`.
4. Letakkan file `PULL_REQUEST_TEMPLATE.md` di dalam `.github/` langsung.
5. Commit dan push ke repository.

---

Siap digunakan!

Kalau Anda ingin otomatisasi lebih lanjut seperti:

* **Label otomatis**
* **Assign reviewer otomatis**
* **CI linting/tes otomatis saat PR**

Saya bisa bantu juga. Mau dilanjutkan ke sana?
