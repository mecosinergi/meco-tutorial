# 01. Panduan-Github
### Ringkasan Alur Kerja Git

Secara sederhana, alur kerja dasar Git adalah sebagai berikut:
1.  **Modifikasi**: Anda mengubah file di folder proyek Anda (working directory).
2.  **Stage**: Anda memilih perubahan mana yang ingin Anda simpan (menambahkannya ke staging area).
3.  **Commit**: Anda menyimpan perubahan tersebut secara permanen di riwayat lokal proyek Anda.
4.  **Push**: Anda mengirimkan hasil `commit` Anda ke repositori remote di GitHub.

---

### Langkah 1: Instalasi dan Konfigurasi Awal

1.  **Instal Git for Windows**:
    *   Unduh dari situs resmi: [https://git-scm.com/download/win](https://git-scm.com/download/win)
    *   Jalankan installer. Untuk sebagian besar opsi, Anda bisa membiarkannya default. Pastikan **"Git Bash"** dan **"Git GUI"** ikut terinstal. VS Code akan otomatis mendeteksi instalasi Git ini.

2.  **Buka Terminal (Git Bash atau Terminal di VS Code)**:
    *   Anda bisa membuka **Git Bash** dari Start Menu.
    *   Atau, cara yang lebih mudah, buka Visual Studio Code, lalu buka terminal dengan menekan `Ctrl + ` (tanda backtick) atau melalui menu `Terminal > New Terminal`.

3.  **Konfigurasi Nama dan Email Anda**:
    Perintah ini wajib dijalankan sekali saja. Git akan menggunakan informasi ini untuk setiap `commit` yang Anda buat. Gunakan nama dan email yang sama dengan akun GitHub Anda.

    Jalankan perintah ini di terminal:
    ```bash
    git config --global user.name "Mecosinergi"
    git config --global user.email "email_github_anda@example.com"
    ```
    Ganti `"email_github_anda@example.com"` dengan email yang Anda gunakan untuk GitHub.

### Langkah 2: Memulai Proyek dengan Git

Ada dua cara umum untuk memulai:

**Opsi A: Memulai Proyek Baru dari Komputer Lokal**

Gunakan cara ini jika Anda sudah punya folder proyek di komputer yang ingin Anda unggah ke GitHub.

1.  **Buat Folder Proyek**: Buat sebuah folder baru untuk proyek Anda, misalnya `D:\Belajar\Catatan2025\Proyek-Git-Pertama`.
2.  **Buka Folder di VS Code**: Buka VS Code, lalu pilih `File > Open Folder...` dan pilih folder yang baru Anda buat.
3.  **Inisialisasi Git**: Di terminal VS Code, jalankan perintah:
    ```bash
    git init
    ```
    Perintah ini akan membuat sebuah sub-folder tersembunyi bernama `.git`. Di sinilah semua riwayat dan konfigurasi Git disimpan.

4.  **Buat Repositori Baru di GitHub**:
    *   Buka [github.com](https://github.com) dan login.
    *   Klik ikon `+` di pojok kanan atas, lalu pilih **"New repository"**.
    *   Beri nama repositori Anda (misalnya `proyek-git-pertama`).
    *   **PENTING**: *Jangan* centang "Add a README file", ".gitignore", atau "choose a license". Kita akan membuatnya dari lokal.
    *   Klik **"Create repository"**.

5.  **Hubungkan Proyek Lokal ke GitHub**:
    GitHub akan memberikan beberapa perintah. Anda hanya perlu menjalankan dua perintah ini di terminal VS Code Anda. Salin URL HTTPS yang diberikan di halaman GitHub.

    ```bash
    # Menghubungkan folder lokal ke remote repository di GitHub
    git remote add origin https://github.com/Yanvery-Code/proyek-git-pertama.git

    # Mengubah nama branch utama menjadi "main" (standar baru)
    git branch -M main
    ```

Sekarang proyek lokal Anda sudah terhubung ke GitHub. Lanjutkan ke **Langkah 3**.

**Opsi B: Mengkloning (Clone) Repositori yang Sudah Ada dari GitHub**

Gunakan cara ini jika repositori sudah ada di GitHub dan Anda ingin mengunduhnya ke komputer untuk mulai bekerja.

1.  **Buka Halaman Repositori di GitHub**: Pergi ke repositori yang ingin Anda unduh.
2.  **Salin URL**: Klik tombol hijau **"< > Code"**, pastikan tab **HTTPS** terpilih, lalu salin URL-nya.
3.  **Jalankan Perintah Clone**: Buka terminal di direktori tempat Anda ingin menyimpan proyek (misalnya `D:\Belajar\Catatan2025\Github-vercel`). Lalu jalankan:
    ```bash
    git clone https://github.com/Yanvery-Code/nama-repositori.git
    ```
    Ganti `nama-repositori` dengan nama repositori Anda. Git akan otomatis membuat folder dengan nama yang sama dan mengunduh semua isinya. Anda tidak perlu `git init` atau `git remote add`.

### Langkah 3: Alur Kerja Sehari-hari (Add, Commit, Push)

Ini adalah siklus yang akan Anda lakukan berulang kali.

1.  **Buat atau Ubah File**:
    Buat file baru (misalnya `index.html`) atau ubah file yang sudah ada di dalam folder proyek Anda menggunakan VS Code.

2.  **Lihat Status Perubahan (Sangat Berguna!)**:
    Jalankan perintah ini kapan pun Anda ragu:
    ```bash
    git status
    ```
    Git akan memberitahu Anda file mana yang baru, yang diubah (`modified`), atau yang belum dilacak (`untracked`).

3.  **Tambahkan Perubahan ke Staging Area (`git add`)**:
    Anggap "staging area" adalah keranjang untuk perubahan yang siap disimpan. Anda bisa memilih file satu per satu atau semuanya sekaligus.

    ```bash
    # Menambahkan satu file spesifik
    git add index.html

    # Atau, cara paling umum, menambahkan SEMUA perubahan di folder proyek
    git add .
    ```

4.  **Simpan Perubahan ke Riwayat Lokal (`git commit`)**:
    Setelah perubahan ada di "staging area", simpan dengan sebuah "commit". Setiap commit harus memiliki pesan yang menjelaskan perubahan yang Anda buat.

    ```bash
    git commit -m "Menambahkan file index.html pertama"
    ```
    Pesan commit yang baik sangat penting. Buatlah singkat tapi deskriptif.

5.  **Kirim Perubahan ke GitHub (`git push`)**:
    Setelah di-commit, perubahan masih ada di komputer lokal Anda. Untuk mengirimnya ke GitHub, jalankan:
    ```bash
    git push origin main
    ```
    *   `origin`: Nama remote yang kita atur di Langkah 2 (menunjuk ke URL GitHub Anda).
    *   `main`: Nama branch yang ingin Anda kirim.

    Saat pertama kali `push`, Windows mungkin akan meminta Anda login ke akun GitHub Anda.

### Langkah 4: Mengambil Perubahan dari GitHub (`git pull`)

Jika Anda bekerja di komputer lain atau ada orang lain yang mengubah kode di GitHub, Anda perlu memperbarui folder lokal Anda.

```bash
git pull origin main
```
Perintah ini akan mengunduh perubahan terbaru dari GitHub dan menggabungkannya dengan kode Anda. Biasakan menjalankan `git pull` sebelum mulai bekerja.

### Menggunakan Integrasi Git di Visual Studio Code

VS Code membuat semua ini lebih mudah tanpa harus selalu mengetik perintah.

1.  **Buka Tab Source Control**: Klik ikon cabang pohon di menu sebelah kiri (atau tekan `Ctrl + Shift + G`).
2.  **Staging (`git add`)**: Di daftar "Changes", Anda akan melihat semua file yang telah diubah. Arahkan mouse ke nama file dan klik ikon `+` untuk melakukan `git add` pada file tersebut.
3.  **Commit (`git commit`)**: Ketik pesan commit Anda di kotak teks di bagian atas, lalu klik ikon centang (✓) untuk melakukan `git commit`.
4.  **Push & Pull (`git push/pull`)**: Klik tombol **"Sync Changes"** di bagian bawah status bar, atau klik menu `...` di tab Source Control dan pilih **"Push"** atau **"Pull"**.
---
