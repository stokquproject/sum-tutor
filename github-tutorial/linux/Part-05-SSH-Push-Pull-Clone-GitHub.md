![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 30 Mins](https://img.shields.io/badge/Durasi-30_Menit-blue?style=for-the-badge)
![Security: SSH](https://img.shields.io/badge/Keamanan-SSH_Key-success?style=for-the-badge&logo=openssh)

# 🔐 Koneksi Aman ke GitHub: SSH Key, Push, Pull & Clone

Di tutorial Windows, kita menggunakan *Personal Access Token* (PAT) untuk autentikasi ke GitHub. Di Linux, kita akan naik level.

Kita akan menggunakan **SSH Key** — metode autentikasi yang lebih elegan, lebih aman, dan sekali dikonfigurasi, tidak pernah perlu memasukkan password atau token lagi. Selamanya.

Ini bukan konfigurasi rumit yang hanya bisa dilakukan developer senior. Ini adalah prosedur standar yang akan Anda selesaikan dalam 10 menit — dan hasilnya akan menemani seluruh karier Anda.

## 📋 Daftar Isi
- [Mengapa SSH Lebih Baik dari HTTPS + Token?](#-mengapa-ssh-lebih-baik-dari-https--token)
- [Membuat SSH Key Pair](#-membuat-ssh-key-pair)
- [Mendaftarkan SSH Key ke GitHub](#-mendaftarkan-ssh-key-ke-github)
- [Menguji Koneksi SSH](#-menguji-koneksi-ssh)
- [Membuat & Menghubungkan Repositori ke GitHub](#-membuat--menghubungkan-repositori-ke-github)
- [git push — Mengirim Karya ke Cloud](#-git-push--mengirim-karya-ke-cloud)
- [git pull — Sinkronisasi dari GitHub](#-git-pull--sinkronisasi-dari-github)
- [git clone — Mengunduh Repositori](#-git-clone--mengunduh-repositori)
- [Workflow Harian Developer Linux](#-workflow-harian-developer-linux)

---

## 🤔 Mengapa SSH Lebih Baik dari HTTPS + Token?

| | **HTTPS + Token** | **SSH Key** |
|---|---|---|
| **Autentikasi** | Token berupa string panjang | Kriptografi kunci publik/privat |
| **Token kadaluarsa?** | ✅ Ya, perlu diperbaharui | ❌ Tidak, berlaku selamanya |
| **Perlu input tiap push?** | Kadang (sampai disimpan di cache) | ❌ Tidak pernah |
| **Bisa dicuri jika repo tersebar?** | ⚠️ Token bisa bocor di history | ✅ Kunci privat tidak pernah meninggalkan mesin Anda |
| **Revoke akses** | Hapus token di GitHub | Hapus kunci publik di GitHub |
| **Standar di industri server?** | Jarang | ✅ Universal |

SSH Key bekerja dengan prinsip **kriptografi asimetris**:
- **Private Key** (`~/.ssh/id_ed25519`): Tersimpan di mesin Anda. **Tidak pernah dibagikan ke siapapun.**
- **Public Key** (`~/.ssh/id_ed25519.pub`): Diberikan ke GitHub. Aman untuk disebar ke mana saja.

Saat Anda push, Git membuktikan identitas Anda dengan matematika kriptografi — tanpa mengirimkan satu pun karakter password melalui jaringan.

---

## 🔑 Membuat SSH Key Pair

```bash
# Generate SSH key dengan algoritma Ed25519 (modern, aman, cepat)
# Ganti email dengan email akun GitHub Anda
ssh-keygen -t ed25519 -C "email.anda@contoh.com"
```

Anda akan ditanya beberapa hal:

```
Enter file in which to save the key (/home/user/.ssh/id_ed25519):
```
→ Tekan **Enter** untuk menggunakan lokasi default.

```
Enter passphrase (empty for no passphrase):
```
→ Anda bisa menambahkan passphrase untuk keamanan ekstra, atau tekan **Enter** dua kali untuk tanpa passphrase. Untuk kemudahan sehari-hari, **Enter** saja sudah cukup.

**Output sukses:**
```
Generating public/private ed25519 key pair.
Your identification has been saved in /home/user/.ssh/id_ed25519
Your public key has been saved in /home/user/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx email.anda@contoh.com
```

Dua file kini ada di `~/.ssh/`:
```bash
ls -la ~/.ssh/
# -rw------- 1 user user  411 id_ed25519       ← PRIVATE KEY (jaga ketat!)
# -rw-r--r-- 1 user user   98 id_ed25519.pub   ← public key (aman dibagikan)
```

> ⚠️ **PERINGATAN KEAMANAN KRITIS:**
> File `id_ed25519` (tanpa `.pub`) adalah **kunci privat Anda**. Jangan pernah:
> - Membagikannya ke siapapun
> - Menaruhnya di repositori Git
> - Mengirimkannya via email atau chat
>
> Siapapun yang memiliki file ini bisa bertindak atas nama Anda di semua layanan yang menggunakan kunci ini. Perlakukan seperti password paling penting yang Anda miliki.

### Aktifkan SSH Agent (untuk Passphrase)

Jika Anda menambahkan passphrase, gunakan `ssh-agent` agar tidak perlu mengetiknya setiap saat:

```bash
# Jalankan ssh-agent
eval "$(ssh-agent -s)"

# Tambahkan kunci ke agent
ssh-add ~/.ssh/id_ed25519
```

Tambahkan dua baris ini ke `~/.bashrc` atau `~/.zshrc` agar berjalan otomatis:
```bash
eval "$(ssh-agent -s)" > /dev/null 2>&1
ssh-add ~/.ssh/id_ed25519 2>/dev/null
```

---

## 📋 Mendaftarkan SSH Key ke GitHub

Sekarang salin isi *public key* Anda:

```bash
# Tampilkan isi public key
cat ~/.ssh/id_ed25519.pub
```

Output akan terlihat seperti ini (satu baris panjang):
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx email.anda@contoh.com
```

**Salin seluruh baris tersebut**, lalu:

1. Login ke **GitHub** → Klik foto profil (kanan atas) → **Settings**
2. Di sidebar kiri: **SSH and GPG keys**
3. Klik **"New SSH key"**
4. **Title**: isi deskripsi mesin Anda (misal: "Laptop Ubuntu Kantor")
5. **Key type**: Authentication Key
6. **Key**: paste seluruh isi public key Anda
7. Klik **"Add SSH key"**

> 💡 **PRO TIP: Salin dari terminal tanpa mouse**
> Jika Anda bekerja di server remote atau ingin cara yang lebih cepat:
> ```bash
> # Install xclip jika belum ada
> sudo apt install xclip -y
>
> # Salin public key langsung ke clipboard
> xclip -selection clipboard < ~/.ssh/id_ed25519.pub
> ```
> Lalu tinggal `Ctrl+V` di browser.

---

## 🧪 Menguji Koneksi SSH

Sebelum melakukan apapun, verifikasi bahwa koneksi SSH ke GitHub bekerja:

```bash
ssh -T git@github.com
```

Anda mungkin melihat peringatan ini pertama kali:
```
The authenticity of host 'github.com (140.82.112.3)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Ketik `yes` dan tekan Enter. GitHub akan ditambahkan ke `~/.ssh/known_hosts`.

**Output sukses:**
```
Hi username-anda! You've successfully authenticated, but GitHub does not provide shell access.
```

Melihat nama akun GitHub Anda di sana? Koneksi SSH sudah sempurna. 🎉

---

## 🆕 Membuat & Menghubungkan Repositori ke GitHub

### Buat Repo Baru di GitHub

1. Klik **"+"** di pojok kanan atas → **"New repository"**
2. Isi nama repositori
3. Pilih **Public** atau **Private**
4. **Jangan centang** "Add a README file" jika sudah ada repo lokal
5. Klik **"Create repository"**

### Hubungkan Repo Lokal ke GitHub via SSH

```bash
# Pastikan Anda ada di folder proyek
cd ~/proyek/website-saya

# Tambahkan remote dengan URL SSH (perhatikan format git@github.com, bukan https://)
git remote add origin git@github.com:username-anda/nama-repo.git

# Verifikasi remote terdaftar
git remote -v
# Output:
# origin  git@github.com:username-anda/nama-repo.git (fetch)
# origin  git@github.com:username-anda/nama-repo.git (push)
```

**Perbedaan URL SSH vs HTTPS:**
```bash
# SSH (gunakan ini di Linux — autentikasi otomatis via key)
git@github.com:username/nama-repo.git

# HTTPS (membutuhkan token saat push)
https://github.com/username/nama-repo.git
```

---

## 🚀 git push — Mengirim Karya ke Cloud

```bash
# Push pertama kali — set upstream tracking
git push -u origin main
```

Flag `-u` menghubungkan branch lokal `main` dengan branch `main` di GitHub. Selanjutnya cukup:

```bash
git push
```

**Output sukses:**
```
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 8 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (9/9), 1.45 KiB | 1.45 MiB/s, done.
To git@github.com:username-anda/nama-repo.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

Tidak ada prompt password. Tidak ada token. Langsung berhasil — itulah keindahan SSH.

**Push branch lain ke GitHub:**
```bash
# Push branch fitur ke GitHub
git push -u origin fitur/dark-mode

# Push semua branch sekaligus
git push --all origin
```

---

## 📥 git pull — Sinkronisasi dari GitHub

```bash
# Ambil dan merge perubahan terbaru dari GitHub
git pull

# Equivalent eksplisit: ambil dari origin, merge ke branch aktif
git pull origin main

# Pull dengan rebase alih-alih merge (lebih bersih untuk history linear)
git pull --rebase
```

> 💡 **PRO TIP: `git pull --rebase` vs `git pull`**
> `git pull` default = `git fetch` + `git merge` → menciptakan merge commit ekstra.
> `git pull --rebase` = `git fetch` + `git rebase` → menempatkan commit lokal Anda *di atas* commit terbaru dari remote. Hasilnya: history yang lebih linear dan bersih.
>
> Untuk menjadikannya default:
> ```bash
> git config --global pull.rebase true
> ```

---

## 📦 git clone — Mengunduh Repositori

```bash
# Clone via SSH (setelah SSH key dikonfigurasi)
git clone git@github.com:username/nama-repo.git

# Clone ke folder dengan nama berbeda
git clone git@github.com:username/nama-repo.git nama-folder-saya

# Clone hanya branch tertentu (berguna untuk repo besar)
git clone --single-branch --branch main git@github.com:username/nama-repo.git

# Clone dengan semua submodule (untuk proyek yang menggunakan submodule)
git clone --recurse-submodules git@github.com:username/nama-repo.git
```

Setelah `git clone`, remote `origin` sudah otomatis terkonfigurasi dan mengarah ke URL SSH. Anda langsung siap push dan pull.

---

## 🔄 Workflow Harian Developer Linux

Tempel ini di terminal Anda sebagai referensi:

```bash
# ════════════════════════════════════════════
# RITUAL PAGI — Sebelum mulai coding
# ════════════════════════════════════════════

git switch main                        # Pastikan di branch utama
git pull                               # Ambil update terbaru
git switch -c fitur/nama-tugas-hari-ini  # Buat branch baru

# ════════════════════════════════════════════
# SELAMA CODING — Simpan progress berkala
# ════════════════════════════════════════════

git status                             # Cek kondisi
git diff                               # Review perubahan sebelum staging
git add .                              # Staging
git commit -m "Deskripsi yang jelas"   # Commit

# ════════════════════════════════════════════
# RITUAL SORE — Setelah selesai coding
# ════════════════════════════════════════════

git push -u origin fitur/nama-tugas-hari-ini  # Push ke GitHub
# Buka GitHub → Create Pull Request untuk review tim
```

---

## 🚑 Klinik Darurat

> [!WARNING]
> **Error: `Permission denied (publickey)`**
>
> ```
> git@github.com: Permission denied (publickey).
> fatal: Could not read from remote repository.
> ```
>
> **Penyebab**: GitHub tidak mengenali SSH key Anda. Kemungkinan: key belum didaftarkan, atau SSH agent tidak aktif.
>
> **Diagnosis**:
> ```bash
> # Cek apakah key ter-load di SSH agent
> ssh-add -l
>
> # Jika hasilnya "The agent has no identities", load keynya:
> ssh-add ~/.ssh/id_ed25519
>
> # Test koneksi ulang
> ssh -T git@github.com
> ```

> [!WARNING]
> **Error: `remote: Repository not found`**
>
> **Penyebab**: URL remote salah, atau Anda tidak punya akses ke repositori tersebut.
>
> **Solusi**: Verifikasi URL remote: `git remote -v`. Perbaiki jika salah: `git remote set-url origin git@github.com:username-benar/nama-repo-benar.git`

> [!WARNING]
> **Error: `Updates were rejected because the remote contains work that you do not have locally`**
>
> **Penyebab**: Ada commit di GitHub yang belum ada di lokal Anda.
>
> **Solusi**:
> ```bash
> git pull --rebase
> # Selesaikan conflict jika ada
> git push
> ```

> [!NOTE]
> **Mengganti URL remote dari HTTPS ke SSH (untuk repo yang sudah ada)**
>
> Jika sebelumnya Anda clone via HTTPS dan ingin beralih ke SSH:
> ```bash
> git remote set-url origin git@github.com:username/nama-repo.git
> git remote -v  # verifikasi
> ```

---

Koneksi SSH sudah terkonfigurasi. Push, pull, dan clone sudah dikuasai. Anda sekarang memiliki semua alat untuk bekerja secara profesional dengan GitHub dari terminal Linux Anda.

Saatnya menyatukan semua yang telah dipelajari dalam satu simulasi penuh. Di bab terakhir, kita jalani studi kasus kolaborasi tim nyata — lengkap dengan Pull Request, Code Review, dan penyelesaian Merge Conflict seperti yang terjadi di industri sesungguhnya. 🎬

---
*Sebelumnya: [Part 4 — Branch & Merge](Part-04-Branch-dan-Merge.md)*
*Selanjutnya: [Part 6 — Studi Kasus: Kolaborasi Tim Nyata di Linux](Part-06-Studi-Kasus-Kolaborasi-Tim.md)*
