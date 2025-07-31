Keren! Ini upgrade besar untuk sistem deployment Anda. Kita akan tambahkan:

1. ✅ **Notifikasi ke Telegram/Discord setelah deploy**
2. ✅ **Auto-deploy terpisah untuk `staging` dan `production`**
3. ✅ **Rollback otomatis jika deploy gagal**

---

## 🧩 1. Notifikasi ke Telegram atau Discord setelah Deploy

### 🟦 A. **Telegram**

#### 🔑 1. Buat Bot Telegram

1. Cari **@BotFather** di Telegram
2. Kirim `/newbot` → beri nama dan username bot
3. Catat **TOKEN API** (misalnya: `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`)
4. Kirim pesan ke bot → lalu buka:
   `https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates`
   Dapatkan **chat\_id**

#### 🔐 2. Tambahkan Secrets di GitHub

| Nama Secret        | Nilai                     |
| ------------------ | ------------------------- |
| `TELEGRAM_TOKEN`   | Token dari BotFather      |
| `TELEGRAM_CHAT_ID` | Chat ID (dari getUpdates) |

#### 🧑‍💻 3. Tambahkan Langkah ke Workflow

```yaml
- name: Notifikasi ke Telegram
  run: |
    curl -s -X POST https://api.telegram.org/bot${{ secrets.TELEGRAM_TOKEN }}/sendMessage \
      -d chat_id=${{ secrets.TELEGRAM_CHAT_ID }} \
      -d text="✅ *Deploy sukses!* Repository ${{ github.repository }} branch `${{ github.ref_name }}` berhasil dideploy ke server 🚀" \
      -d parse_mode=Markdown
```

---

### 💬 B. **Discord**

#### 🔗 1. Buat Webhook:

* Di Discord channel → Edit Channel → **Integrations** → **Webhooks** → **New Webhook**
* Salin URL (misal `https://discord.com/api/webhooks/....`)

#### 🔐 2. Tambahkan ke GitHub Secrets:

| Nama Secret       | Nilai                    |
| ----------------- | ------------------------ |
| `DISCORD_WEBHOOK` | URL webhook dari Discord |

#### 🧑‍💻 3. Tambahkan Langkah ke Workflow

```yaml
- name: Notifikasi ke Discord
  run: |
    curl -H "Content-Type: application/json" -X POST \
    -d "{\"content\": \"✅ Deploy sukses ke server untuk branch \`${{ github.ref_name }}\`\"}" \
    ${{ secrets.DISCORD_WEBHOOK }}
```

---

## 🔀 2. Auto-Deploy Terpisah untuk **Staging** & **Production**

### 💡 Strategi:

* Branch `main` → deploy ke **production**
* Branch `staging` → deploy ke **server staging**

### 📁 Buat dua file workflow:

#### `.github/workflows/deploy-prod.yml`

```yaml
name: Deploy ke Production

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy via SSH
        uses: appleboy/ssh-action@v1.0.0
        with:
          host: ${{ secrets.PROD_HOST }}
          username: ${{ secrets.PROD_USER }}
          key: ${{ secrets.PROD_SSH_KEY }}
          port: ${{ secrets.PROD_PORT }}
          script: |
            cd /var/www/production
            git pull origin main
            # perintah deploy lainnya
```

#### `.github/workflows/deploy-staging.yml`

```yaml
name: Deploy ke Staging

on:
  push:
    branches: [staging]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy ke staging
        uses: appleboy/ssh-action@v1.0.0
        with:
          host: ${{ secrets.STAGE_HOST }}
          username: ${{ secrets.STAGE_USER }}
          key: ${{ secrets.STAGE_SSH_KEY }}
          port: ${{ secrets.STAGE_PORT }}
          script: |
            cd /var/www/staging
            git pull origin staging
            # jalankan testing atau build untuk staging
```

---

## 🔁 3. Rollback Otomatis Jika Gagal Deploy

### 🧠 Konsep:

* Simpan commit terakhir (misalnya ke file `rollback.sh`)
* Jika `deploy` gagal, jalankan `git reset --hard <commit_id>` otomatis

### 🔧 Di server: buat skrip rollback

#### 📁 `/var/www/myapp/rollback.sh`

```bash
#!/bin/bash
echo "⚠️ Rolling back to previous commit..."
git reset --hard $(cat .last_commit)
echo "✅ Rollback selesai."
```

### 📝 Di GitHub Workflow:

```yaml
- name: Simpan Commit ID untuk rollback
  run: |
    ssh ${{ secrets.USERNAME }}@${{ secrets.HOST }} -p ${{ secrets.PORT }} <<EOF
      cd /var/www/myapp
      git rev-parse HEAD > .last_commit
EOF

- name: Deploy (berisiko gagal)
  uses: appleboy/ssh-action@v1.0.0
  with:
    # ... deploy steps ...

- name: Rollback jika deploy gagal
  if: failure()
  run: |
    ssh ${{ secrets.USERNAME }}@${{ secrets.HOST }} -p ${{ secrets.PORT }} <<EOF
      cd /var/www/myapp
      bash rollback.sh
EOF
```

---

## 🚀 Bonus: Notifikasi Gagal Deploy

Tambahkan ke akhir workflow:

```yaml
- name: Kirim notifikasi jika deploy gagal
  if: failure()
  run: |
    curl -s -X POST https://api.telegram.org/bot${{ secrets.TELEGRAM_TOKEN }}/sendMessage \
      -d chat_id=${{ secrets.TELEGRAM_CHAT_ID }} \
      -d text="❌ *Deploy GAGAL!* Branch `${{ github.ref_name }}`. Otomatis rollback dilakukan." \
      -d parse_mode=Markdown
```

---

## 🔒 Secrets Tambahan yang Anda Butuhkan

| Secret Name        | Untuk                       |
| ------------------ | --------------------------- |
| `PROD_HOST`        | IP/domain server production |
| `STAGE_HOST`       | IP/domain server staging    |
| `SSH_KEY`          | SSH private key             |
| `DISCORD_WEBHOOK`  | Webhook Discord             |
| `TELEGRAM_TOKEN`   | Bot token dari BotFather    |
| `TELEGRAM_CHAT_ID` | Chat ID penerima notifikasi |

---

Itu pendekatan yang sangat bijak—menunggu keputusan tim sebelum menentukan framework.

Untuk menjaga agar *workflow GitHub Actions* dan *skrip deployment* tetap fleksibel, berikut beberapa hal yang bisa Anda lakukan **terlepas dari framework**:

---

## ✅ Yang Sudah Cocok untuk Semua Framework

### 1. Struktur Workflow

File `.github/workflows/deploy-prod.yml` dan `deploy-staging.yml` sudah:

* Mendukung `git pull`, `npm install`, `build`
* Bisa diubah jadi `composer install` atau `go build`, dll.

### 2. Rollback

File `rollback.sh` hanya mengembalikan ke commit sebelumnya, **tanpa tergantung bahasa/framework**.

### 3. Notifikasi

Notifikasi Telegram dan Discord sudah netral.

---

## ✏️ Cara Menyesuaikan Berdasarkan Framework (Nanti)

### Jika pakai Laravel (PHP):

```bash
composer install --no-dev --optimize-autoloader
php artisan migrate --force
php artisan config:cache
php artisan route:cache
```

### Jika pakai React/Vue/Next:

```bash
npm install
npm run build
```

### Jika pakai Express/Node.js API:

```bash
npm install
pm2 restart my-app
```

### Jika pakai Python Django:

```bash
pip install -r requirements.txt
python manage.py migrate
python manage.py collectstatic --noinput
sudo systemctl restart gunicorn
```

---

## 📦 Tips Kolaborasi Multi-Framework

Jika tim mempertimbangkan berbagai opsi, Anda bisa:

* Tambahkan **template switch** di skrip:

  ```bash
  if [ -f package.json ]; then
    echo "Node.js project"
    npm install
    npm run build
  elif [ -f composer.json ]; then
    echo "Laravel project"
    composer install
    php artisan migrate --force
  fi
  ```

* Gunakan `.env` di server untuk mendeteksi jenis project

---

Kalau nanti sudah ada keputusan framework, saya bisa bantu:

* Menyesuaikan deploy script
* Setup environment `.env` aman di GitHub
* Integrasi CI/CD lanjutan (linting, test, dsb.)

Mau saya bantu buatkan template *framework switcher* yang fleksibel?
