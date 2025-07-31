# 04. Panduan Berkontribusi

Terima kasih sudah menjadi bagian dari proyek ini. Berikut adalah panduan kerja sama yang harus diikuti:

## ✅ Persiapan Awal
1. Pastikan Anda sudah menerima undangan sebagai kolaborator.
2. Clone repo:
   ```bash
   git clone https://github.com/[username]/[nama-repo].git
   cd [nama-repo]
````

## 🔁 Alur Kerja Kolaborasi

### 1. Update dari Remote

Selalu update repository lokal Anda:

```bash
git pull origin main
```

### 2. Buat Branch Baru

Untuk fitur/bug per kontributor:

```bash
git checkout -b nama-fitur-anda
```

### 3. Commit Perubahan

```bash
git add .
git commit -m "Deskripsikan apa yang Anda kerjakan"
```

### 4. Push Branch

```bash
git push origin nama-fitur-anda
```

### 5. Buat Pull Request

* Masuk ke GitHub
* Buat pull request dari `nama-fitur-anda` ke `main`
* Tunggu review dari pemilik repo atau kolaborator lain
* Merge setelah disetujui

## ⚠️ Konflik

Jika Anda mengalami konflik saat `git pull`:

* Periksa file yang bermasalah
* Perbaiki secara manual
* Simpan dan lakukan:

  ```bash
  git add .
  git commit -m "Selesaikan konflik"
  git push
  ```

## 🔐 Catatan Penting

* Jangan pernah langsung push ke `main` jika sudah ada aturan proteksi
* Gunakan `.gitignore` untuk mengecualikan file yang tidak perlu
* Jangan upload file rahasia seperti `.env`, credential, dll
