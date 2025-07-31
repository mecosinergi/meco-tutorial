Berikut panduan praktis untuk **Tools Pendukung GitHub**: `Issues`, `Pull Request`, dan `Projects`. Cocok digunakan dalam tim kecil untuk kolaborasi yang rapi dan terstruktur.

---

## 🛠️ 1. GitHub Issues – *Untuk Melacak Tugas & Masalah*

### 🔍 Apa itu Issues?

`Issues` digunakan untuk mencatat hal-hal seperti:

* Fitur baru yang ingin dibuat
* Bug/error yang ditemukan
* Pertanyaan diskusi internal
* TODO atau catatan penting

### 📝 Cara Membuat Issue:

1. Buka tab **"Issues"** di repository.
2. Klik **"New Issue"**.
3. Isi:

   * **Title:** ringkas, misalnya "Tampilan dashboard error di mobile"
   * **Description:** jelaskan detailnya, bisa pakai checklist:

     ```markdown
     - [x] Periksa breakpoint CSS
     - [ ] Tambahkan media query
     ```
4. (Opsional) Tambahkan **Label**: `bug`, `enhancement`, `question`, dll.
5. Klik **Submit new issue**.

### 📌 Tips:

* Gunakan prefix pada judul, contoh: `[BUG]`, `[FEAT]`, `[DOCS]`
* Assign orang yang bertanggung jawab

---

## 🔄 2. Pull Request (PR) – *Untuk Review Sebelum Merge*

### 🔍 Apa itu Pull Request?

`Pull Request` adalah permintaan untuk menggabungkan kode dari **branch lain ke main** (atau branch lainnya). PR memungkinkan review sebelum kode masuk ke versi final.

### 💡 Alur Kerja Umum:

1. Buat branch baru

   ```bash
   git checkout -b fitur-auth
   ```
2. Kerjakan fitur, commit, dan push ke GitHub

   ```bash
   git push origin fitur-auth
   ```
3. Di GitHub, klik tombol **"Compare & Pull Request"**.
4. Tambahkan deskripsi: apa yang dikerjakan, apakah sudah diuji, dll.
5. Assign reviewer (opsional), lalu klik **"Create Pull Request"**.
6. Reviewer memeriksa, jika OK, klik **"Merge"**.
7. Hapus branch jika sudah tidak dibutuhkan.

### 📌 Tips:

* Gunakan deskripsi PR yang jelas
* Jangan lupa `pull` terbaru dari `main` agar tidak konflik
* Jangan merge PR sendiri jika bukan owner (kecuali memang disetujui)

---

## 🗂️ 3. GitHub Projects – *Untuk Manajemen Tugas (Mirip Trello)*

### 🔍 Apa itu GitHub Projects?

Tool seperti **Kanban Board** yang membantu melihat status tugas: `Todo`, `In Progress`, `Done`, dll.

### 📝 Cara Membuat Project Board:

1. Masuk ke repository → Tab **Projects**.
2. Klik **"New Project"** → pilih template **"Board"**.
3. Beri nama project, misalnya: "Sprint Juli 2025".
4. Buat kolom seperti:

   * `📋 To Do`
   * `🚧 In Progress`
   * `✅ Done`

### ✏️ Menambahkan Card (Tugas):

* Klik **"Add cards"**
* Bisa tarik dari Issues, atau buat manual card baru
* Geser antar kolom sesuai progresnya

### 🔗 Hubungkan Issue & PR:

* Saat buat Issue/PR, klik kanan → **Add to project**
* Atau dari dalam Project → `+ Add card` → pilih dari Issue/PR

---

## 🧠 Rangkuman Singkat

| Tool             | Fungsi                 | Siapa yang Gunakan       |
| ---------------- | ---------------------- | ------------------------ |
| **Issues**       | Mencatat tugas & bug   | Semua kontributor        |
| **Pull Request** | Review & merge kode    | Kontributor + Reviewer   |
| **Projects**     | Manajemen visual tugas | Pemilik repo & semua tim |

---

Jika Anda mau, saya bisa bantu buat:

* Template *Issue* & *Pull Request* yang siap pakai
* Setup *GitHub Projects* dasar secara visual
* Automasi seperti: PR auto-close issue, label otomatis, dsb.

Apakah Anda ingin contoh file template `.github/ISSUE_TEMPLATE` dan `PULL_REQUEST_TEMPLATE` juga?
