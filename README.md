# 🚀 GitHub Komutları - Kapsamlı Rehber

Bu rehber, GitHub ile çalışırken kullanabileceğiniz tüm temel ve gelişmiş komutları içermektedir.

## 📋 İçindekiler

1. [Git Kurulum ve Yapılandırma](#git-kurulum-ve-yapılandırma)
2. [Repository İşlemleri](#repository-işlemleri)
3. [Dosya ve Değişiklik Yönetimi](#dosya-ve-değişiklik-yönetimi)
4. [Commit İşlemleri](#commit-işlemleri)
5. [Branch (Dal) Yönetimi](#branch-dal-yönetimi)
6. [Remote Repository İşlemleri](#remote-repository-işlemleri)
7. [Merge ve Rebase İşlemleri](#merge-ve-rebase-işlemleri)
8. [Tag İşlemleri](#tag-işlemleri)
9. [Log ve History](#log-ve-history)
10. [Stash İşlemleri](#stash-işlemleri)
11. [Reset ve Restore İşlemleri](#reset-ve-restore-işlemleri)
12. [GitHub CLI (gh) Komutları](#github-cli-gh-komutları)
13. [İleri Seviye İşlemler](#ileri-seviye-işlemler)
14. [Troubleshooting](#troubleshooting)

---

## 🛠️ Git Kurulum ve Yapılandırma

### Git Kurulum
```bash
# macOS (Homebrew ile)
brew install git

# Linux (Ubuntu/Debian)
sudo apt-get install git

# Windows
# Git for Windows'u indirin: https://git-scm.com/download/win
```

### İlk Yapılandırma
```bash
# Kullanıcı adı ve email ayarlama
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Varsayılan editör ayarlama
git config --global core.editor "code"  # VS Code için
git config --global core.editor "vim"   # Vim için

# Yapılandırmaları görüntüleme
git config --list
git config --global --list

# Belirli bir ayarı görüntüleme
git config user.name
git config user.email
```

### SSH Anahtarı Oluşturma
```bash
# SSH anahtarı oluşturma
ssh-keygen -t ed25519 -C "your.email@example.com"

# SSH agent'ı başlatma
eval "$(ssh-agent -s)"

# SSH anahtarını agent'a ekleme
ssh-add ~/.ssh/id_ed25519

# Public key'i görüntüleme (GitHub'a eklemek için)
cat ~/.ssh/id_ed25519.pub

# SSH bağlantısını test etme
ssh -T git@github.com
```

---

## 📁 Repository İşlemleri

### Yeni Repository Oluşturma
```bash
# Boş repository oluşturma
git init

# Belirli bir dizinde repository oluşturma
git init my-project

# GitHub'dan repository klonlama
git clone https://github.com/username/repository.git
git clone git@github.com:username/repository.git  # SSH ile

# Belirli bir branch'i klonlama
git clone -b branch-name https://github.com/username/repository.git

# Sadece son commit'i klonlama (shallow clone)
git clone --depth 1 https://github.com/username/repository.git
```

### Repository Bilgileri
```bash
# Repository durumunu görüntüleme
git status

# Kısa format
git status -s

# Repository bilgilerini görüntüleme
git remote -v
git remote show origin

# Repository'nin kök dizinini bulma
git rev-parse --show-toplevel
```

---

## 📄 Dosya ve Değişiklik Yönetimi

### Dosya Ekleme
```bash
# Belirli dosya ekleme
git add filename.txt

# Birden fazla dosya ekleme
git add file1.txt file2.txt

# Tüm dosyaları ekleme
git add .
git add -A

# Belirli uzantıdaki dosyaları ekleme
git add *.js
git add src/*.py

# Dizin ekleme
git add directory/

# İnteraktif ekleme
git add -i
git add -p  # Patch mode
```

### Dosya Çıkarma (Unstage)
```bash
# Belirli dosyayı unstage etme
git reset HEAD filename.txt
git restore --staged filename.txt

# Tüm dosyaları unstage etme
git reset HEAD
git restore --staged .
```

### Dosya Silme
```bash
# Dosyayı hem working directory'den hem de staging'den silme
git rm filename.txt

# Sadece Git'ten silme (dosya kalır)
git rm --cached filename.txt

# Dizin silme
git rm -r directory/

# Force silme
git rm -f filename.txt
```

### Dosya Taşıma/Yeniden Adlandırma
```bash
# Dosya taşıma/yeniden adlandırma
git mv old-name.txt new-name.txt
git mv file.txt directory/

# Manuel taşıma sonrası Git'e bildirme
mv old-name.txt new-name.txt
git add new-name.txt
git rm old-name.txt
```

---

## 💾 Commit İşlemleri

### Temel Commit
```bash
# Commit oluşturma
git commit -m "Commit message"

# Add ve commit'i birlikte yapma
git commit -am "Add and commit message"

# Detaylı commit mesajı
git commit  # Editör açılır

# Boş commit (test için)
git commit --allow-empty -m "Empty commit"
```

### Gelişmiş Commit
```bash
# Son commit'i değiştirme (amend)
git commit --amend -m "New commit message"

# Son commit'e dosya ekleme
git add new-file.txt
git commit --amend --no-edit

# Commit author'ını değiştirme
git commit --amend --author="New Author <new@email.com>"

# Commit tarihini değiştirme
git commit --amend --date="2024-01-01 12:00:00"
```

### Commit Template ve Hooks
```bash
# Commit template ayarlama
git config --global commit.template ~/.gitmessage

# Commit mesaj formatı örneği (~/.gitmessage)
# feat: add new feature
# 
# - Detailed description
# - What was changed
# - Why it was changed
#
# Fixes #123
```

---

## 🌿 Branch (Dal) Yönetimi

### Branch Oluşturma ve Değiştirme
```bash
# Yeni branch oluşturma
git branch feature-branch
git checkout -b feature-branch  # Oluştur ve geç
git switch -c feature-branch    # Modern syntax

# Branch'ler arası geçiş
git checkout main
git switch main

# Önceki branch'e geçiş
git checkout -
git switch -
```

### Branch Listeleme
```bash
# Local branch'leri listeleme
git branch

# Remote branch'leri de dahil etme
git branch -a

# Remote branch'leri listeleme
git branch -r

# Branch'leri detaylı listeleme
git branch -v

# Merge edilmiş branch'leri listeleme
git branch --merged
git branch --no-merged
```

### Branch Silme
```bash
# Local branch silme
git branch -d branch-name

# Force silme
git branch -D branch-name

# Remote branch silme
git push origin --delete branch-name
git push origin :branch-name  # Kısa syntax
```

### Branch Yeniden Adlandırma
```bash
# Aktif branch'i yeniden adlandırma
git branch -m new-branch-name

# Başka branch'i yeniden adlandırma
git branch -m old-name new-name

# Remote'ta da güncelleme
git push origin :old-name new-name
git push origin -u new-name
```

---

## 🌐 Remote Repository İşlemleri

### Remote Yönetimi
```bash
# Remote ekleme
git remote add origin https://github.com/username/repo.git

# Remote'ları listeleme
git remote -v

# Remote bilgilerini görüntüleme
git remote show origin

# Remote URL değiştirme
git remote set-url origin https://github.com/username/new-repo.git

# Remote silme
git remote remove origin
```

### Push İşlemleri
```bash
# Temel push
git push origin main

# İlk push (upstream ayarlama)
git push -u origin main

# Tüm branch'leri push etme
git push origin --all

# Tag'leri push etme
git push origin --tags

# Force push (dikkatli kullanın!)
git push --force origin main
git push --force-with-lease origin main  # Daha güvenli
```

### Pull ve Fetch İşlemleri
```bash
# Remote'tan değişiklikleri alma (fetch + merge)
git pull origin main

# Remote'tan değişiklikleri alma (rebase ile)
git pull --rebase origin main

# Sadece remote bilgilerini alma (merge yapmadan)
git fetch origin

# Tüm remote'ları fetch etme
git fetch --all

# Belirli branch'i fetch etme
git fetch origin feature-branch:feature-branch
```

---

## 🔀 Merge ve Rebase İşlemleri

### Merge İşlemleri
```bash
# Branch'i mevcut branch'e merge etme
git merge feature-branch

# Fast-forward merge'i engelleme
git merge --no-ff feature-branch

# Squash merge (tüm commit'leri tek commit'e çevirme)
git merge --squash feature-branch

# Merge conflict çözme
git status  # Conflicted dosyaları göster
# Dosyaları manuel düzenle
git add .
git commit
```

### Rebase İşlemleri
```bash
# Branch'i main üzerine rebase etme
git rebase main

# İnteraktif rebase
git rebase -i HEAD~3  # Son 3 commit

# Rebase devam etme (conflict çözümü sonrası)
git rebase --continue

# Rebase iptal etme
git rebase --abort

# Rebase atlama
git rebase --skip
```

### Cherry-pick
```bash
# Belirli commit'i mevcut branch'e alma
git cherry-pick <commit-hash>

# Birden fazla commit
git cherry-pick <commit1> <commit2>

# Range cherry-pick
git cherry-pick A..B
```

---

## 🏷️ Tag İşlemleri

### Tag Oluşturma
```bash
# Lightweight tag
git tag v1.0.0

# Annotated tag (önerilen)
git tag -a v1.0.0 -m "Version 1.0.0 release"

# Belirli commit'e tag
git tag -a v1.0.0 <commit-hash> -m "Version 1.0.0"

# Signed tag
git tag -s v1.0.0 -m "Signed version 1.0.0"
```

### Tag Listeleme ve Görüntüleme
```bash
# Tüm tag'leri listeleme
git tag

# Pattern ile filtreleme
git tag -l "v1.*"

# Tag bilgilerini görüntüleme
git show v1.0.0

# Tag'ler ve commit'leri listeleme
git tag -n
```

### Tag Silme ve Push
```bash
# Local tag silme
git tag -d v1.0.0

# Remote tag silme
git push origin :refs/tags/v1.0.0
git push origin --delete v1.0.0

# Tag'leri push etme
git push origin v1.0.0
git push origin --tags
```

---

## 📊 Log ve History

### Commit Geçmişi
```bash
# Temel log
git log

# Kısa format
git log --oneline

# Grafik gösterimi
git log --graph --oneline --decorate --all

# Belirli sayıda commit
git log -10

# Belirli tarih aralığı
git log --since="2024-01-01" --until="2024-12-31"

# Belirli author
git log --author="John Doe"

# Commit mesajında arama
git log --grep="bug fix"
```

### Dosya Geçmişi
```bash
# Belirli dosyanın geçmişi
git log filename.txt

# Dosya değişikliklerini gösterme
git log -p filename.txt

# Dosya satır değişiklikleri
git blame filename.txt

# Dosya satır geçmişi
git log -L 1,10:filename.txt  # 1-10. satırlar
```

### Diff İşlemleri
```bash
# Working directory ile staging arasındaki fark
git diff

# Staging ile son commit arasındaki fark
git diff --staged
git diff --cached

# İki commit arasındaki fark
git diff <commit1> <commit2>

# İki branch arasındaki fark
git diff main..feature-branch

# Belirli dosya için diff
git diff filename.txt
```

---

## 📦 Stash İşlemleri

### Stash Oluşturma
```bash
# Değişiklikleri stash'e alma
git stash

# Mesaj ile stash
git stash save "Work in progress on feature X"

# Untracked dosyaları da dahil etme
git stash -u

# Ignored dosyaları da dahil etme
git stash -a
```

### Stash Yönetimi
```bash
# Stash listesi
git stash list

# Stash içeriğini görüntüleme
git stash show
git stash show -p  # Detaylı

# Stash'i geri getirme
git stash pop
git stash apply

# Belirli stash'i geri getirme
git stash pop stash@{2}
git stash apply stash@{2}

# Stash silme
git stash drop
git stash drop stash@{2}

# Tüm stash'leri silme
git stash clear
```

---

## ⏪ Reset ve Restore İşlemleri

### Reset İşlemleri
```bash
# Soft reset (commit'i geri al, değişiklikleri staging'de tut)
git reset --soft HEAD~1

# Mixed reset (varsayılan - commit ve staging'i geri al)
git reset HEAD~1
git reset --mixed HEAD~1

# Hard reset (her şeyi geri al - DİKKATLİ!)
git reset --hard HEAD~1

# Belirli commit'e reset
git reset --hard <commit-hash>

# Belirli dosyayı reset etme
git reset HEAD filename.txt
```

### Restore İşlemleri (Modern Git)
```bash
# Working directory'deki değişiklikleri geri alma
git restore filename.txt

# Staging'den çıkarma
git restore --staged filename.txt

# Belirli commit'ten dosya geri getirme
git restore --source=<commit-hash> filename.txt

# Tüm dosyaları geri alma
git restore .
```

### Revert İşlemleri
```bash
# Commit'i geri alma (yeni commit oluşturarak)
git revert <commit-hash>

# Merge commit'i geri alma
git revert -m 1 <merge-commit-hash>

# Birden fazla commit'i geri alma
git revert <commit1>..<commit2>
```

---

## 🛠️ GitHub CLI (gh) Komutları

### Kurulum ve Giriş
```bash
# GitHub CLI kurulumu (macOS)
brew install gh

# GitHub'a giriş
gh auth login

# Token ile giriş
gh auth login --with-token < token.txt
```

### Repository İşlemleri
```bash
# Repository oluşturma
gh repo create my-repo --public
gh repo create my-repo --private

# Repository klonlama
gh repo clone username/repo

# Repository silme
gh repo delete username/repo

# Repository bilgileri
gh repo view
gh repo view username/repo
```

### Issue İşlemleri
```bash
# Issue'ları listeleme
gh issue list

# Issue oluşturma
gh issue create --title "Bug report" --body "Description"

# Issue görüntüleme
gh issue view 123

# Issue kapama
gh issue close 123

# Issue'ya yorum ekleme
gh issue comment 123 --body "This is a comment"
```

### Pull Request İşlemleri
```bash
# PR oluşturma
gh pr create --title "Feature X" --body "Description"

# PR'ları listeleme
gh pr list

# PR görüntüleme
gh pr view 456

# PR'ı merge etme
gh pr merge 456

# PR'ı checkout etme
gh pr checkout 456

# PR'ı kapatma
gh pr close 456
```

### Actions ve Workflow
```bash
# Workflow'ları listeleme
gh workflow list

# Workflow çalıştırma
gh workflow run workflow-name

# Run'ları listeleme
gh run list

# Run loglarını görüntüleme
gh run view 789
```

---

## 🔧 İleri Seviye İşlemler

### Submodule İşlemleri
```bash
# Submodule ekleme
git submodule add https://github.com/user/repo.git path/to/submodule

# Submodule'ları güncelleme
git submodule update --init --recursive

# Submodule'ları remote'tan güncelleme
git submodule update --remote

# Submodule silme
git submodule deinit path/to/submodule
git rm path/to/submodule
```

### Worktree İşlemleri
```bash
# Yeni worktree oluşturma
git worktree add ../feature-branch feature-branch

# Worktree'leri listeleme
git worktree list

# Worktree silme
git worktree remove ../feature-branch
```

### Bisect (Binary Search)
```bash
# Bisect başlatma
git bisect start

# İyi commit işaretleme
git bisect good <commit-hash>

# Kötü commit işaretleme
git bisect bad <commit-hash>

# Test sonrası işaretleme
git bisect good  # Bu commit iyi
git bisect bad   # Bu commit kötü

# Bisect bitirme
git bisect reset
```

### Clean İşlemleri
```bash
# Untracked dosyaları gösterme
git clean -n

# Untracked dosyaları silme
git clean -f

# Dizinleri de dahil etme
git clean -fd

# Ignored dosyaları da silme
git clean -fX
```

---

## 🔍 Troubleshooting

### Yaygın Problemler ve Çözümleri

#### Merge Conflict Çözme
```bash
# 1. Conflicted dosyaları görüntüle
git status

# 2. Dosyaları düzenle (conflict marker'ları temizle)
# <<<<<<< HEAD
# Your changes
# =======
# Their changes
# >>>>>>> branch-name

# 3. Düzenlenen dosyaları add et
git add .

# 4. Merge'i tamamla
git commit
```

#### Yanlış Commit'i Geri Alma
```bash
# Son commit'i geri al (değişiklikleri koru)
git reset --soft HEAD~1

# Son commit'i tamamen geri al
git reset --hard HEAD~1

# Public commit'i güvenli şekilde geri alma
git revert HEAD
```

#### Branch'i Yanlış Yere Merge Etme
```bash
# Merge'i geri alma
git reset --hard HEAD~1

# Doğru branch'e geç ve tekrar merge et
git checkout correct-branch
git merge feature-branch
```

#### Remote'tan Silinen Branch'i Temizleme
```bash
# Remote tracking branch'leri temizle
git remote prune origin

# Otomatik prune ayarlama
git config --global fetch.prune true
```

### Git Aliases (Kısayollar)
```bash
# Yararlı alias'lar ayarlama
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.pl pull
git config --global alias.ps push

# Daha karmaşık alias'lar
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
```

### Performance Optimizasyonu
```bash
# Repository'yi optimize etme
git gc

# Aggressive optimization
git gc --aggressive --prune=now

# Repository boyutunu kontrol etme
git count-objects -vH

# Large file'ları bulma
git rev-list --objects --all | git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | sed -n 's/^blob //p' | sort --numeric-sort --key=2 | tail -10
```

---

## 📚 En İyi Pratikler

### Commit Mesajları
- **Format**: `type: description`
- **Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`
- **Örnek**: `feat: add user authentication system`

### Branch Naming
- **Feature**: `feature/user-auth`
- **Bug Fix**: `bugfix/login-error`
- **Hotfix**: `hotfix/security-patch`

### .gitignore Örnekleri
```gitignore
# Dependencies
node_modules/
vendor/

# Build outputs
dist/
build/
*.o
*.exe

# Environment files
.env
.env.local

# IDE files
.vscode/
.idea/
*.swp

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
logs/
```

---

## 🆘 Acil Durum Komutları

```bash
# Tüm local değişiklikleri geri al
git reset --hard HEAD
git clean -fd

# Son working state'e dön
git reflog
git reset --hard HEAD@{1}

# Repository'yi tamamen temizle
git reset --hard origin/main
git clean -fd

# Yanlışlıkla silinen branch'i kurtarma
git reflog
git checkout <commit-hash>
git checkout -b recovered-branch
```

---

## 📖 Ek Kaynaklar

- **Official Git Documentation**: https://git-scm.com/doc
- **GitHub Docs**: https://docs.github.com/
- **Interactive Git Tutorial**: https://learngitbranching.js.org/
- **Git Cheat Sheet**: https://education.github.com/git-cheat-sheet-education.pdf

---

*Bu rehber, Git ve GitHub ile çalışırken ihtiyaç duyabileceğiniz tüm temel ve gelişmiş komutları içermektedir. Düzenli olarak güncellenecektir.*

**Son Güncelleme**: 2025

**Katkıda Bulunma**: Bu rehberi geliştirmek için pull request gönderebilirsiniz.

---

## 🏆 Hızlı Referans

### En Çok Kullanılan 20 Komut
```bash
git status          # Repository durumu
git add .           # Tüm değişiklikleri stage'e al
git commit -m "msg" # Commit oluştur
git push            # Remote'a gönder
git pull            # Remote'tan çek
git branch          # Branch'leri listele
git checkout -b     # Yeni branch oluştur ve geç
git merge           # Branch'i merge et
git log             # Commit geçmişi
git diff            # Değişiklikleri göster
git clone           # Repository klonla
git init            # Repository oluştur
git remote -v       # Remote'ları listele
git stash           # Değişiklikleri stash'e al
git reset           # Commit'leri geri al
git revert          # Commit'i güvenli şekilde geri al
git tag             # Tag oluştur
git fetch           # Remote bilgilerini al
git rebase          # Branch'i rebase et
git cherry-pick     # Belirli commit'i al
```

Bu rehber GitHub ve Git ile çalışırken ihtiyacınız olan her şeyi kapsamaktadır! 🎉