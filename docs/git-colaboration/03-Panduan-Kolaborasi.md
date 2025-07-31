
# 03. Panduan Kolaborasi Git

Repositori ini menggunakan alur kerja sederhana berbasis `main` dan branch fitur.

---

## 📌 Cabang Utama

- `main` → Branch untuk versi final / siap produksi

---

## 👨‍💻 Langkah Kerja Setiap Anggota Tim

### 1. Clone Repo (sekali saja)
```bash
git clone git@github.com:nama-org/nama-repo.git
cd nama-repo
```

### 2. Buat Branch Baru untuk Fitur
```bash
git checkout main
git pull origin main
git checkout -b fitur-nama-anda
```

### 3. Kerjakan Fitur Anda
```bash
# Edit kode, lalu commit
git add .
git commit -m "Deskripsi fitur yang dikerjakan"
```

### 4. Push ke GitHub
```bash
git push origin fitur-nama-anda
```

---

## 🔄 Sinkron dengan Perubahan dari `main`

Jika `main` sudah berubah:
```bash
git checkout main
git pull origin main

git checkout fitur-nama-anda
git merge main
```

> ⚠️ Jika ada konflik, selesaikan file yang konflik, lalu:
```bash
git add .
git commit -m "Selesai konflik dengan main"
```

---

## 🔁 Buat Pull Request ke `main`

1. Buka GitHub
2. Klik tombol **"Compare & pull request"**
3. Isi deskripsi perubahan
4. Klik **"Create pull request"**

Tunggu review dari pemilik repo sebelum digabung ke `main`.

---

## 🧩 Tips Tambahan

| Tujuan | Perintah |
|--------|----------|
| Lihat semua branch lokal | `git branch` |
| Hapus branch lokal | `git branch -d fitur-nama` |
| Hapus branch di GitHub | `git push origin --delete fitur-nama` |

---

## 🚫 Jangan Lakukan Dulu

- `git rebase`
- `git push --force`
- `git cherry-pick`, `stash`, dll.

---

## 🧠 Tujuan

Sederhana, mudah diikuti, dan menjaga agar semua tim bisa belajar Git dengan nyaman.

