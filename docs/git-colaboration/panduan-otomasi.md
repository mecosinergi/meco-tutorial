Mantap! Kita akan lanjut dengan **otomatisasi GitHub repository private Anda** untuk mempercepat kolaborasi tim dan menjaga kualitas kode.

---

## ⚙️ Tujuan Otomatisasi

Yang akan kita siapkan:

1. **Label otomatis untuk Issue dan PR**
2. **Reviewer otomatis berdasarkan direktori atau tim**
3. **Linting/Test otomatis saat PR dibuat** (CI)
4. *(Opsional bonus)* Bot yang memberi komentar otomatis di PR

---

## 🧩 1. Label Otomatis – `github-actions/labeler`

### 📁 File: `.github/labeler.yml`

```yaml
# Labeler untuk memberi label otomatis pada file/folder tertentu
frontend:
  - frontend/**
  - src/frontend/**

backend:
  - backend/**
  - src/backend/**

docs:
  - README.md
  - docs/**

config:
  - .github/**
  - .env.example
```

### 📁 File: `.github/workflows/labeler.yml`

```yaml
name: Label PR Otomatis

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  label:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/labeler@v5
        with:
          repo-token: "${{ secrets.GITHUB_TOKEN }}"
```

---

## 🧑‍🤝‍🧑 2. Reviewer Otomatis – `CODEOWNERS`

### 📁 File: `.github/CODEOWNERS`

```text
# Aturan reviewer otomatis
/frontend/       @frontenddev1 @frontenddev2
/backend/        @backenddev1
/docs/           @yourgithubusername
```

> 📌 Jika file dalam folder `/frontend/` diubah, reviewer yang ditentukan akan otomatis di-assign di PR.

---

## ✅ 3. Linting & Test Otomatis (CI) – `GitHub Actions`

Contoh untuk project Node.js (sesuaikan jika Laravel, Python, dst.)

### 📁 File: `.github/workflows/ci.yml`

```yaml
name: CI - Test & Lint

on:
  pull_request:
    branches: [main]

jobs:
  test-and-lint:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4

    - name: Setup Node.js
      uses: actions/setup-node@v4
      with:
        node-version: 20

    - name: Install dependencies
      run: npm install

    - name: Linting
      run: npm run lint

    - name: Run Tests
      run: npm test
```

> 💡 Bisa disesuaikan: `npm run lint` → `php artisan test`, `pytest`, `go test`, dll.

---

## 🤖 Bonus: Komentar Otomatis di PR

Gunakan [actions/github-script](https://github.com/actions/github-script) untuk memberi komentar otomatis di setiap PR:

### 📁 File: `.github/workflows/pr-comment.yml`

```yaml
name: Komentar Otomatis Saat PR Dibuat

on:
  pull_request:
    types: [opened]

jobs:
  comment:
    runs-on: ubuntu-latest
    steps:
      - name: Comment on PR
        uses: actions/github-script@v7
        with:
          script: |
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: "Terima kasih sudah membuat PR! 🎉 Tim akan segera mereview. Jangan lupa sertakan screenshot dan testing info ya 🙏"
            })
```

---

## 📦 Rangkuman

| Fitur              | File Konfigurasi                      | Fungsi                                 |
| ------------------ | ------------------------------------- | -------------------------------------- |
| Label otomatis     | `.github/labeler.yml` + `labeler.yml` | Tambah label otomatis berdasarkan path |
| Reviewer otomatis  | `.github/CODEOWNERS`                  | Assign reviewer berdasarkan folder     |
| Lint/Test otomatis | `.github/workflows/ci.yml`            | Jalankan test & lint saat PR           |
| Komentar bot PR    | `.github/workflows/pr-comment.yml`    | Komentar sambutan otomatis             |

---

## Mau Saya Buatkan ZIP Siap Pakai?

Saya bisa buatkan semua file konfigurasi di atas jadi satu ZIP, atau ditampilkan sebagai struktur folder yang tinggal Anda salin. Mau versi mana?

* 📁 Struktur file copy-paste?
* 📦 ZIP siap unduh?
* 📜 Mau disesuaikan ke framework Anda dulu (Laravel, Next.js, Python, dsb)?
