![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 25 Mins](https://img.shields.io/badge/Durasi-25_Menit-blue?style=for-the-badge)
![Security: SSH + Keychain](https://img.shields.io/badge/Keamanan-SSH_+_Keychain-success?style=for-the-badge&logo=apple&logoColor=white)

# 🔐 Koneksi Aman ke GitHub: SSH + macOS Keychain

macOS punya keunggulan yang tidak dimiliki sistem lain saat berurusan dengan autentikasi GitHub: **Keychain** — sistem penyimpanan credential terenkripsi bawaan Apple yang terintegrasi sempurna dengan SSH.

Artinya: kita bisa mengkonfigurasi SSH Key satu kali, menyimpan passphrase-nya di Keychain, dan setelah itu... tidak pernah mengetikkan password atau token apapun lagi saat melakukan push ke GitHub. Selamanya.

Ini bukan scorcery. Ini macOS bekerja seperti seharusnya.

## 📋 Daftar Isi
- [SSH Key vs HTTPS + Token: Pilihan untuk macOS](#-ssh-key-vs-https--token-pilihan-untuk-macos)
- [Membuat SSH Key Pair di macOS](#-membuat-ssh-key-pair-di-macos)
- [Menyimpan Passphrase ke macOS Keychain](#-menyimpan-passphrase-ke-macos-keychain)
- [Mendaftarkan SSH Key ke GitHub](#-mendaftarkan-ssh-key-ke-github)
- [Menguji Koneksi SSH](#-menguji-koneksi-ssh)
- [Membuat & Menghubungkan Repositori ke GitHub](#-membuat--menghubungkan-repositori-ke-github)
- [git push — Kirim ke Cloud](#-git-push--kirim-ke-cloud)
- [git pull — Ambil dari Cloud](#-git-pull--ambil-dari-cloud)
- [git clone — Unduh Repositori](#-git-clone--unduh-repositori)
- [Workflow Harian Developer macOS](#-workflow-harian-developer-macos)

---

## 🤔 SSH Key vs HTTPS + Token: Pilihan untuk macOS

macOS mendukung kedua metode. Tapi ada satu perbedaan kunci:

| | **HTTPS + Token** | **SSH + Keychain** |
|---|---|---|
| **Setup** | Lebih mudah di awal | Perlu generate key (5 menit sekali) |
| **Token kadaluarsa** | ⚠️ Ya, perlu perbarui | ❌ Tidak pernah |
| **Push tanpa input** | Setelah disimpan di osxkeychain | ✅ Selalu, permanen |
| **Integrasi macOS** | `osxkeychain` credential helper | **Keychain native + SSH config** |
| **Keamanan** | Token bisa bocor di environment | Kunci privat tidak pernah dikirim |
| **Standar industri** | Umum untuk CI/CD | ✅ Standar untuk developer |

Keduanya bisa digunakan di macOS. Tutorial ini mengajarkan **SSH + Keychain** karena lebih aman, tidak pernah kadaluarsa, dan memberikan pengalaman push/pull yang paling mulus.

---

## 🔑 Membuat SSH Key Pair di macOS

macOS sudah dilengkapi `ssh-keygen` — tidak perlu install apapun.

```zsh
# Generate SSH key dengan algoritma Ed25519 (modern, aman, cepat)
# Ganti dengan email akun GitHub Anda
ssh-keygen -t ed25519 -C "email.anda@contoh.com"
```

Anda akan ditanya beberapa hal:

**Pertanyaan 1: Lokasi file**
```
Enter file in which to save the key (/Users/NamaAnda/.ssh/id_ed25519):
```
→ Tekan **Enter** untuk menggunakan lokasi default `~/.ssh/id_ed25519`

**Pertanyaan 2: Passphrase**
```
Enter passphrase (empty for no passphrase):
```
→ Masukkan passphrase yang kuat (sangat direkomendasikan). Anda hanya perlu mengingat ini *sekali* — setelah disimpan ke Keychain, macOS akan mengisinya otomatis selamanya.

**Output sukses:**
```
Generating public/private ed25519 key pair.
Your identification has been saved in /Users/NamaAnda/.ssh/id_ed25519
Your public key has been saved in /Users/NamaAnda/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx email.anda@contoh.com
The key's randomart image is:
+--[ED25519 256]--+
|    .  .         |
...
```

Dua file kini tersimpan di `~/.ssh/`:
```zsh
ls -la ~/.ssh/
# -rw-------  1 user  staff   419 id_ed25519      ← PRIVATE KEY
# -rw-r--r--  1 user  staff    98 id_ed25519.pub  ← public key
```

> ⚠️ **PERINGATAN:**
> File `id_ed25519` (tanpa `.pub`) adalah kunci privat Anda. Perlakukan seperti password paling penting yang Anda miliki. Jangan pernah bagikan, jangan masukkan ke repositori Git, dan jangan kirim via email atau chat.

---

## 🔑 Menyimpan Passphrase ke macOS Keychain

Inilah fitur eksklusif macOS yang membuat pengalaman SSH benar-benar mulus. Kita konfigurasikan SSH Agent untuk menggunakan macOS Keychain.

**Langkah 1: Tambahkan kunci ke SSH Agent + simpan passphrase ke Keychain**

```zsh
# Tambahkan kunci ke ssh-agent dan simpan passphrase ke macOS Keychain
# Flag --apple-use-keychain adalah fitur eksklusif macOS
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

macOS akan meminta passphrase Anda *sekali ini saja* — lalu menyimpannya di Keychain secara terenkripsi.

**Langkah 2: Buat file SSH config agar konfigurasi ini persisten**

```zsh
# Buat atau edit file SSH config
nano ~/.ssh/config
```

Tambahkan konfigurasi berikut:

```
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

Simpan dengan `Ctrl+X` → `Y` → `Enter`.

Penjelasan setiap baris:
- `AddKeysToAgent yes` — otomatis tambahkan kunci ke ssh-agent saat pertama digunakan
- `UseKeychain yes` — gunakan macOS Keychain untuk menyimpan/membaca passphrase
- `IdentityFile` — tentukan kunci mana yang digunakan untuk koneksi ke github.com

Dengan konfigurasi ini, passphrase SSH Anda **tidak akan pernah diminta lagi** setelah restart Mac sekalipun — Keychain mengisinya secara otomatis.

---

## 📋 Mendaftarkan SSH Key ke GitHub

Salin isi *public key* ke clipboard:

```zsh
# Salin public key ke clipboard macOS
pbcopy < ~/.ssh/id_ed25519.pub
```

`pbcopy` adalah perintah native macOS untuk menyalin ke clipboard — tidak perlu install apapun. Equivalent dari `Ctrl+C` untuk output terminal.

Sekarang buka GitHub:

1. Login → Klik foto profil (kanan atas) → **Settings**
2. Sidebar kiri: **SSH and GPG keys**
3. Klik **"New SSH key"**
4. **Title**: isi deskripsi yang jelas (misal: "MacBook Pro 2024 - Rumah")
5. **Key type**: Authentication Key
6. **Key**: `⌘+V` untuk paste
7. Klik **"Add SSH key"**

> 💡 **PRO TIP: Beri Nama yang Informatif**
> Nama seperti "MacBook Pro M3 - Kantor" atau "iMac 2023 - Studio" memudahkan Anda mengelola kunci di masa depan. Saat laptop hilang atau diganti, Anda tahu persis kunci mana yang harus dihapus dari GitHub.

---

## 🧪 Menguji Koneksi SSH

```zsh
ssh -T git@github.com
```

Pertama kali, Anda akan melihat peringatan fingerprint:
```
The authenticity of host 'github.com (140.82.112.3)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Ketik `yes` dan Enter. GitHub ditambahkan ke `~/.ssh/known_hosts`.

**Output sukses:**
```
Hi username-anda! You've successfully authenticated, but GitHub does not provide shell access.
```

Nama akun GitHub Anda muncul? Koneksi SSH + Keychain sudah sempurna. 🎉 Anda tidak akan pernah diminta password lagi.

---

## 🆕 Membuat & Menghubungkan Repositori ke GitHub

**Buat repo baru di GitHub:**
1. Klik **"+"** → **"New repository"**
2. Isi nama
3. Pilih Public/Private
4. **Jangan centang** "Add a README" jika sudah punya repo lokal
5. **"Create repository"**

**Hubungkan repo lokal ke GitHub via SSH:**

```zsh
# Di dalam folder proyek lokal Anda
cd ~/Developer/proyek-pertama

# Tambahkan remote dengan URL SSH
git remote add origin git@github.com:username-anda/proyek-pertama.git

# Verifikasi
git remote -v
# origin  git@github.com:username-anda/proyek-pertama.git (fetch)
# origin  git@github.com:username-anda/proyek-pertama.git (push)
```

**Perbedaan URL SSH vs HTTPS:**
```zsh
# SSH — gunakan ini untuk autentikasi tanpa password via Keychain
git@github.com:username/repo.git

# HTTPS — butuh token saat push
https://github.com/username/repo.git
```

---

## 🚀 git push — Kirim ke Cloud

```zsh
# Push pertama kali — set tracking upstream
git push -u origin main
```

Flag `-u` menghubungkan branch lokal `main` dengan branch `main` di GitHub. Selanjutnya, cukup:

```zsh
git push
```

Tidak ada dialog password. Tidak ada token. Keychain bekerja di balik layar secara transparan. Push selesai.

**Variasi push yang berguna:**

```zsh
# Push branch lain
git push -u origin fitur/dark-mode

# Push semua branch sekaligus
git push --all origin

# Push dan set tracking untuk branch baru
git push -u origin $(git branch --show-current)
```

---

## 📥 git pull — Ambil dari Cloud

```zsh
# Ambil dan gabungkan perubahan terbaru
git pull

# Pull dengan rebase — history lebih linear
git pull --rebase

# Ambil dari branch tertentu
git pull origin main
```

> 💡 **PRO TIP: Jadikan Rebase sebagai Default**
> `git pull --rebase` menghasilkan history yang lebih bersih dibanding merge biasa. Jadikan default:
> ```zsh
> git config --global pull.rebase true
> ```
> Setelah ini, setiap `git pull` otomatis menggunakan rebase.

---

## 📦 git clone — Unduh Repositori

```zsh
# Clone via SSH
git clone git@github.com:username/nama-repo.git

# Clone ke folder dengan nama berbeda
git clone git@github.com:username/nama-repo.git nama-folder

# Clone lalu langsung masuk ke folder (via subshell trick)
git clone git@github.com:username/nama-repo.git && cd nama-repo

# Clone repositori besar — shallow clone hanya ambil history terakhir
git clone --depth 1 git@github.com:username/nama-repo.git
```

Setelah clone via SSH, remote `origin` sudah otomatis terkonfigurasi — langsung siap push dan pull tanpa konfigurasi tambahan.

---

## 🔄 Workflow Harian Developer macOS

Simpan sebagai snippet atau tempel di dashboard:

```zsh
# ════════════════════════════════════════════
# RITUAL PAGI — Sebelum mulai coding
# ════════════════════════════════════════════
git switch main                            # Kembali ke branch utama
git pull                                   # Sinkronisasi dengan tim
git switch -c fitur/nama-tugas-hari-ini    # Buat branch baru

# ════════════════════════════════════════════
# SELAMA CODING — Save progress berkala
# ════════════════════════════════════════════
git status                                 # Cek kondisi
git diff                                   # Review sebelum staging
git add .                                  # Stage semua perubahan
git commit -m "Deskripsi yang jelas"       # Simpan snapshot

# ════════════════════════════════════════════
# RITUAL SORE — Selesai coding
# ════════════════════════════════════════════
git push -u origin fitur/nama-tugas-hari-ini  # Push ke GitHub
# Buka GitHub → Create Pull Request

# ════════════════════════════════════════════
# DARURAT — Perlu pindah branch saat coding
# ════════════════════════════════════════════
git stash push -m "WIP: deskripsi pekerjaan saat ini"
git switch main
# ... tangani hal mendesak ...
git switch -   # Kembali ke branch sebelumnya
git stash pop  # Ambil pekerjaan yang tadi disimpan
```

---

## 🚑 Klinik Darurat

> [!WARNING]
> **`ssh-add --apple-use-keychain` tidak dikenali**
>
> **Penyebab**: macOS versi lama menggunakan flag `-K` (sudah deprecated).
>
> **Solusi**: Coba dengan flag lama: `ssh-add -K ~/.ssh/id_ed25519`
> Atau update macOS ke versi yang lebih baru.

> [!WARNING]
> **`Permission denied (publickey)` setelah restart Mac**
>
> **Penyebab**: SSH key belum ditambahkan ke Keychain dengan benar, atau file `~/.ssh/config` belum ada/salah konfigurasi.
>
> **Solusi**:
> ```zsh
> # Cek apakah key sudah di-load
> ssh-add -l
>
> # Jika kosong, load ulang dan simpan ke Keychain
> ssh-add --apple-use-keychain ~/.ssh/id_ed25519
>
> # Pastikan ~/.ssh/config sudah berisi konfigurasi yang benar
> cat ~/.ssh/config
> ```

> [!NOTE]
> **Mengganti remote dari HTTPS ke SSH (untuk repo yang sudah ada)**
>
> ```zsh
> git remote set-url origin git@github.com:username/nama-repo.git
> git remote -v   # verifikasi
> ```

> [!NOTE]
> **Multi-akun GitHub di satu Mac (misal: akun personal + akun kerja)**
>
> Generate dua SSH key dengan nama berbeda dan tambahkan dua entri di `~/.ssh/config`:
> ```
> Host github.com-personal
>   HostName github.com
>   User git
>   IdentityFile ~/.ssh/id_ed25519_personal
>
> Host github.com-kerja
>   HostName github.com
>   User git
>   IdentityFile ~/.ssh/id_ed25519_kerja
> ```
> Lalu saat menambahkan remote, gunakan alias host yang sesuai:
> ```zsh
> git remote add origin git@github.com-kerja:namaorg/nama-repo.git
> ```

---

SSH sudah terkonfigurasi sempurna dengan Keychain. Push, pull, clone — semua berjalan mulus tanpa interruption.

Satu bab lagi: saatnya menyatukan semua yang telah dipelajari dalam simulasi penuh yang mencerminkan hari kerja developer profesional sesungguhnya di macOS. 🎬

---
*Sebelumnya: [Part 4 — Branch & Merge](Part-04-Branch-dan-Merge.md)*
*Selanjutnya: [Part 6 — Studi Kasus: Workflow Developer macOS Profesional](Part-06-Studi-Kasus-Kolaborasi-Tim.md)*
