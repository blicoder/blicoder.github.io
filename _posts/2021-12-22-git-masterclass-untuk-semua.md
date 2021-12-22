---
layout: post
title: Git Masterclass Untuk Semua
---


## Perintah Dasar Linux
```
cat test.txt
rm test.txt
rmdir test.txt
man ls
rm -rf samples
```

## Konfigurasi Akun Git
```
// global
git config --global user.name "Diva Krishna"
git config --global user.email "divakrishnam@gmail.com"
git config --list

// local
git config --local user.name "Diva Krishna"
git config --local user.email "divakrishnam@gmail.com"
vim ~/.gitconfig
```

## Konfigurasi Default Editor
```
git config --global core.editor "vim"
```

## Git Workflow
```
git init
git add index.html
git add .
git commit -a
git commit -m "pesan"
git commit -am "pesan"
```

## Menghubungkan dengan SSH
```
ssh -T git@github.com

git remote add origin ...
git remote --v 
git remote set-url origin ...
git remote remove origin
```

## Fetch, Pull, Push
```
git push origin master

git pull origin master 
// bring a local branch up-to-date

git fetch origin master 
// update remote tracking branches
```

## History
```
git log
git log --oneline
git log --oneline --graph
```

## Membatalkan Commit
```
git checkout file.js
// membatalkan modified

git reset head file.js
// membatalkan stage

git commit --amend "komen baru"
// mengganti pesan commit

git reset --soft head^
// balik ke stage

git reset --hard head^
// balik ke awal (perubahan akan hilang)
```

## Membandingkan Working Directory dan Stagging Area
```
git diff
```

## Membandingkan Working Directory dan Local Repository
```
git diff head
```

## Membandingkan Staging Area dan Local Repository
```
git diff --staged head
```

## Menampilkan perbandingan pada suatu File
```
git diff -- file.js
```

## Membandingkan antar commit
```
git diff commitcode head
git diff commitcode commitcode
git diff head head^
```

## Membandingkan Local Repository dan Remote Repository
```
git diff master origin/master
```

## Perintah Branching
```
git branch

git branch -a
// cek local dan remote repo

git branch develop

git checkout develop

git checkout -b feature-one
// buat branch sekaligus pindah branch

git branch -m feature-two
// ganti nama branch

git branch -d feature-two
// hapus branch
```

## Fast Forward Merge
```
git merge branchname
// merge commit tetap terpisah
```

## No Fast Forward Merge
```
git merge branchname --no-ff
// merge commit jadi satu
```

## Auto Merging
```
// merge commit antar dua branch tp buat commit merge lagi
```

## Resolve Merge Conflict
```
git merge --abort
```

## Cherry Pick
```
git cherry-pick commitcode commitcode
// mengambil salah satu commit untuk dimerge

git cherry-pick commitcode -n
// mengambil perubahan file tanpa ambil commit
```

## Rebasing
```
git rebase master
```

## Rebasing Fix Conflict
```
git rebase --abort
```

## Pull Dengan Rebase
```
git pull --rebase origin master
```

## Stashing
```
git stash
// menyimpan perubahan tanpa commit

git stash apply
// mengembalikan sebelumnya di stash

git stash list

git stash drop
```
## Stashing Untracking File
```
git stash -u
```

## Multiple Stashes
```
git stash save "message"

git stash show stash@(1)
// melihat perubahan

git stash apply stash@(1)

git stash drop stash@(1)

git stash clear
// menghapus stash yang ada
```

## Stashing to new branch
```
git stash branch brachname
```

## Lightweight Tag
```
git tag tagname

git tag --list

git show tagname

git tag --delete tagname
```

## Annotated Tag
```
git tag -a v0.0.1 -m "release version v0.0.1"

git show v0.0.1

```

## Comparing Tags
```
git diff v0.0.2 v0.0.1
```

## Tagging
```
git tag -a v0.0.1-beta commitcode -m "release version 1 beta"
```

## Update Tagging
```
git tag -a v0.0.1-alpa commitcode -f
```

## Tag with remote repository
```
git push origin v0.0.1-alpa
git push origin master --tags

git push origin :v0.0.1-alpa
// hapus tag di remote repository
```

## Gitflow
- Stagging = sudah di develop tp blm di test
- Production = sudah di develop dan sudah di test

Workflow
- Master = app telah siap di deliver (tech lead)
- Hotfix = bug minor (kesalah kecil) (tech lead)
- Release = siap release (tech lead)
- Develop = staging app (tech lead)
- Bugfix = memperbaiki bug (developer)
- Feature = mengerjakan fitur-fitur (developer)

## Membuat Project GitFlow

```
git flow init

git checkout -b feature/chat
```

## Remote Multi Repository
```
git remote add gitlab ...
git push gitlab master
```