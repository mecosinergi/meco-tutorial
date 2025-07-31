# 02. Panduan-Git-add-push
```console
bash
```

```console
git pull origin main   perbahari local dari github bila ada perubahan langsung dari github
git status
git add index.html  atau
git add .  semua file
git commit -m "Menambahkan file index.html pertama" 
git push origin main
```
### Memulai 
```console
git config --global user.name "Mecosinergi"
git config --global user.email "email_github_anda@example.com"
git init
```

## contoh folder dan nama repositori Pembukaan

### create a new repository on the command line
```console

git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/Mecosinergi/coba.git
git push -u origin main


```
### or push an existing repository from the command line

```console
git remote add origin https://github.com/Mecosinergi/coba.git
git branch -M main
git push -u origin main
```
---
