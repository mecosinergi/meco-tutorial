# 05 Tim Pemula:


Kalau tim kamu **pemula semua**, maka **pakai `git merge` saja** — ini pilihan **yang paling aman, sederhana, dan mudah dipahami.**


### 1. Semua kerja di branch masing-masing:

```bash
git checkout -b fitur-a
```

### 2. Push hasil kerja ke GitHub:

```bash
git add .
git commit -m "Kerjakan fitur A"
git push origin fitur-a
```

### 3. Kalau `main` sudah di-update orang lain:

```bash
git checkout main
git pull origin main

git checkout fitur-a
git merge main
```

> 💡 Kalau ada konflik, Git akan kasih tahu. Selesaikan, lalu:

```bash
git add .
git commit -m "Selesai konflik dengan main"
```

### 4. Lalu buat Pull Request ke `main` dari GitHub UI.

---

## 🛑 Jangan Gunakan Dulu:

* `git rebase`
* `git push --force`
* atau strategi yang terlalu rumit

---