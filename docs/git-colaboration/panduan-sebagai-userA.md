Berikut adalah **panduan lengkap untuk kolaborator** seperti Anda (user pada branch `fitur-a`), terutama **jika `main` sudah berubah saat Anda sedang mengerjakan fitur.**

---

## 🎯 Tujuan:

* Anda kerja di branch `fitur-a`
* Branch `main` (utama) sudah berubah (diupdate oleh pembuat repo)
* Anda ingin tetap **sinkron**, dan nanti **merge aman** ke `main`

---

## 🛠️ 1. **Buat Branch Baru dari `main`**

Lakukan hanya sekali, di awal:

```bash
git checkout main
git pull origin main           # Ambil versi terbaru dari main
git checkout -b fitur-a        # Buat branch baru dari main
```

Mulai kerja coding di `fitur-a`.

---

## 📤 2. **Push Hasil Kerja Anda**

Saat sudah selesai atau ingin menyimpan progres:

```bash
git add .
git commit -m "Tambah fitur A"
git push origin fitur-a
```

---

## 🔄 3. **Jika `main` Sudah Berubah**

Anda bisa **merge** atau **rebase**. Contoh pakai merge (lebih aman untuk pemula):

```bash
# Pindah ke main dan ambil update terbaru
git checkout main
git pull origin main

# Pindah kembali ke fitur Anda
git checkout fitur-a

# Gabungkan perubahan dari main ke fitur Anda
git merge main
```

> ⚠️ Jika ada konflik, Git akan memberi tahu file mana yang konflik. Edit file, selesaikan konflik, lalu:

```bash
git add .
git commit -m "Selesaikan konflik merge dari main"
```

---

## ✅ 4. **Buat Pull Request (PR)**

Setelah sinkron, Anda bisa ajukan PR ke `main`:

* Pergi ke GitHub repo Anda
* Klik tombol **"Compare & pull request"**
* Tambahkan deskripsi, lalu klik **"Create pull request"**

Biasanya pemilik repo akan review dan merge.

---

## 💡 Tips Tambahan

| Kondisi             | Perintah                           |
| ------------------- | ---------------------------------- |
| Cek cabang lokal    | `git branch`                       |
| Cek cabang remote   | `git branch -r`                    |
| Hapus branch lokal  | `git branch -d fitur-a`            |
| Hapus branch remote | `git push origin --delete fitur-a` |

---

Kalau kamu ingin pakai **`rebase`** (versi lebih bersih dari `merge`), saya bisa bantu juga. Mau disertakan?

### 🔄 Apa Itu Rebase?

`git rebase` adalah cara untuk **menggabungkan perubahan dari satu branch ke branch Anda**, dengan **mengubah urutan histori commit** seolah-olah Anda membuat perubahan **di atas commit terbaru dari `main`**.

---

### 🔧 Perbandingan Rebase vs Merge:

| Aksi              | Hasil                                                                |
| ----------------- | -------------------------------------------------------------------- |
| `git merge main`  | Menambahkan commit baru seperti: `Merge branch 'main' into fitur-a`  |
| `git rebase main` | **Mengubah urutan commit Anda** agar seperti baru dibuat dari `main` |

---

### 🔍 Kapan Pakai `rebase`?

* Kalau Anda ingin **histori commit lebih bersih** (tidak banyak commit "merge").
* Kalau Anda sedang kerja di fitur, dan ingin update dari `main` **tanpa menambah commit extra**.

---

## 📌 Contoh Rebase Workflow

Misalnya Anda kerja di `fitur-a`, dan `main` sudah diupdate oleh orang lain.

### 1. Simpan hasil kerja Anda (jika belum):

```bash
git add .
git commit -m "Progres fitur A"
```

### 2. Ambil update terbaru dari `main`:

```bash
git checkout main
git pull origin main
```

### 3. Kembali ke branch fitur:

```bash
git checkout fitur-a
```

### 4. Rebase:

```bash
git rebase main
```

### 5. (Opsional) Jika terjadi konflik:

Git akan menghentikan rebase sementara. Anda harus menyelesaikan konflik file satu per satu:

```bash
# Edit file konflik, selesaikan
git add <file-yang-sudah-diperbaiki>
git rebase --continue
```

Ulangi sampai selesai.

---

### 6. Push hasil rebase ke remote:

Jika Anda sudah pernah push ke GitHub sebelumnya, maka:

```bash
git push origin fitur-a --force
```

> ⚠️ **Catatan penting**:
> `--force` harus hati-hati dipakai karena **mengganti histori commit**. Tapi aman jika Anda **satu-satunya orang yang kerja di branch itu**.

---

## 💬 Kesimpulan

* `merge` = aman, cepat, tapi banyak commit bercabang.
* `rebase` = histori bersih, tapi sedikit lebih teknis dan hati-hati.

Kalau proyek Anda punya **aturan kolaborasi khusus**, sebaiknya diskusikan dengan tim dulu apakah rebase diperbolehkan.

Mau saya bantu buat diagram alur merge vs rebase juga?
