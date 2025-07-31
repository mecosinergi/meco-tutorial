Berikut adalah **panduan lengkap untuk auto-deploy ke server via SSH dari repository GitHub private**, menggunakan **GitHub Actions**. Metode ini aman dan umum digunakan oleh tim developer untuk mem-push kode langsung ke server saat `push` atau `merge` ke `main`.

---

## 🎯 Tujuan

Saat Anda merge ke `main`, GitHub akan otomatis:

* Masuk ke server via SSH
* Menarik perubahan terbaru (pull)
* Menjalankan perintah deploy jika perlu (seperti `npm install`, `php artisan`, dsb.)

---

## 🧩 Struktur Dasar:

* Repositori: Private di GitHub
* Server: Ubuntu (misalnya VPS atau shared server yang support SSH)
* GitHub Action: Menggunakan `appleboy/ssh-action` (aman & populer)

---

## 🛠️ 1. Persiapkan SSH Akses di Server

### Di server Anda:

1. **Buat user khusus deploy** (jika belum ada):

   ```bash
   sudo adduser deployer
   ```

2. **Buat folder deploy jika perlu**:

   ```bash
   mkdir -p /var/www/myapp
   ```

3. **Berikan akses SSH public key nanti di step 2** ke file:

   ```bash
   ~/.ssh/authorized_keys
   ```

---

## 🔐 2. Buat SSH Key dan Tambahkan ke GitHub Secrets

### Di komputer lokal Anda:

1. Buat SSH key khusus untuk deploy (jangan gunakan key default):

   ```bash
   ssh-keygen -t rsa -b 4096 -C "github-action-deploy" -f ~/.ssh/id_deploy -N ""
   ```

   * Hasil: `id_deploy` (private key) dan `id_deploy.pub` (public key)

2. **Salin public key ke server**:

   ```bash
   ssh-copy-id -i ~/.ssh/id_deploy.pub deployer@your.server.ip
   ```

3. Masuk ke repo GitHub → **Settings** → **Secrets and variables** → **Actions** → **New Repository Secret**.

| Nama Secret | Nilai                                         |
| ----------- | --------------------------------------------- |
| `HOST`      | IP atau domain server (contoh: `192.168.1.2`) |
| `USERNAME`  | `deployer` (user di server Anda)              |
| `PORT`      | `22` (atau port SSH Anda)                     |
| `SSH_KEY`   | Salin isi `id_deploy` (private key)           |

---

## ⚙️ 3. Tambahkan GitHub Action untuk Deploy

### 📁 File: `.github/workflows/deploy.yml`

```yaml
name: 🚀 Deploy ke Server (SSH)

on:
  push:
    branches:
      - main

jobs:
  deploy:
    name: Deploy via SSH
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repo
      uses: actions/checkout@v4

    - name: Deploy via SSH
      uses: appleboy/ssh-action@v1.0.0
      with:
        host: ${{ secrets.HOST }}
        username: ${{ secrets.USERNAME }}
        key: ${{ secrets.SSH_KEY }}
        port: ${{ secrets.PORT }}
        script: |
          cd /var/www/myapp
          git pull origin main
          npm install
          npm run build
          pm2 restart app-name # atau restart apache/nginx
```

---

## 📌 Contoh Script `script:` untuk Laravel:

```bash
cd /var/www/mylaravel
git pull origin main
composer install --no-dev --optimize-autoloader
php artisan migrate --force
php artisan config:cache
php artisan route:cache
php artisan view:cache
sudo systemctl reload php8.1-fpm
sudo systemctl reload nginx
```

---

## 🧠 Tips Keamanan

* Jangan pernah commit SSH key ke repo.
* Gunakan user dengan **akses terbatas** (jangan pakai `root`).
* Gunakan `.env.production` yang berbeda dari `.env.local`.
* Batasi IP untuk SSH di server (gunakan firewall / `ufw`).

---

## ✅ Ringkasan

| Komponen              | Fungsi                                     |
| --------------------- | ------------------------------------------ |
| `appleboy/ssh-action` | Login SSH dari GitHub Action               |
| `SSH_KEY`             | Kunci privat tersimpan di GitHub Secrets   |
| `git pull + command`  | Jalankan perintah di server setelah deploy |

---

Kalau Anda mau:

* Menambahkan **notifikasi ke Telegram/Discord setelah deploy**
* Membuat versi **staging** & **production** auto-deploy terpisah
* Atau **rollback otomatis jika gagal deploy**

Saya bisa bantu buatkan lanjutannya. Mau?
