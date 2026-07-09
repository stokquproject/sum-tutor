![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 25 Mins](https://img.shields.io/badge/Durasi-25_Menit-blue?style=for-the-badge)
![Practice: Hands-On](https://img.shields.io/badge/Metode-Hands--On_Practice-red?style=for-the-badge)

# 🌐 Menghubungkan ke Dunia: Push, Pull & Clone ke GitHub

Selama empat bab terakhir, semua keajaiban Git terjadi di satu tempat: laptop Anda sendiri. Repositori lokal, commit lokal, branch lokal — semuanya tersimpan rapi di dalam folder `.git` di komputer Anda.

Sekarang saatnya kita membuka pintunya.

Kita akan menghubungkan kerja keras lokal kita ke **GitHub** — dan dalam prosesnya, Anda akan menguasai tiga perintah yang menjadi tulang punggung kolaborasi tim modern di seluruh dunia: **push**, **pull**, dan **clone**.

## 📋 Daftar Isi
- [Prasyarat: Akun GitHub & Autentikasi](#-prasyarat-akun-github--autentikasi)
- [Membuat Repositori Baru di GitHub](#-membuat-repositori-baru-di-github)
- [git remote — Mendaftarkan Alamat GitHub](#-git-remote--mendaftarkan-alamat-github)
- [git push — Mengirim Karya ke Cloud](#-git-push--mengirim-karya-ke-cloud)
- [git pull — Mengambil Pembaruan dari Cloud](#-git-pull--mengambil-pembaruan-dari-cloud)
- [git clone — Mengunduh Repositori Orang Lain](#-git-clone--mengunduh-repositori-orang-lain)
- [Workflow Harian: Ritual Lengkap Push & Pull](#-workflow-harian-ritual-lengkap-push--pull)

---

## 🔑 Prasyarat: Akun GitHub & Autentikasi

Jika belum punya akun GitHub, daftar di **[github.com](https://github.com)** — gratis untuk selamanya bagi proyek publik maupun privat.

### Menyiapkan Personal Access Token (PAT)

GitHub sudah tidak lagi menerima password biasa untuk operasi Git via terminal. Sebagai gantinya, kita menggunakan **Personal Access Token (PAT)** — semacam "kunci tamu" khusus untuk terminal.

**Cara membuat PAT:**

1. Login ke GitHub → Klik foto profil (kanan atas) → **Settings**
2. Scroll ke bawah → **Developer settings** (di sidebar kiri paling bawah)
3. **Personal access tokens** → **Tokens (classic)** → **Generate new token (classic)**
4. Isi **Note** (misal: "Laptop Windows Rumah")
5. Set **Expiration**: pilih **90 days** atau **No expiration** untuk keperluan belajar
6. Di bagian **Select scopes**, centang: **`repo`** (ini memberi akses penuh ke repositori Anda)
7. Klik **Generate token**

> ⚠️ **PERINGATAN KRITIS:**
> Token Anda hanya ditampilkan **SEKALI SAJA** saat ini. Segera salin dan simpan di tempat aman (misal: aplikasi password manager seperti Bitwarden atau 1Password). Jika lupa, Anda harus membuat token baru.

Token Anda akan terlihat seperti ini:
```
ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

**Saat terminal meminta password**, masukkan token ini (bukan password GitHub Anda). Windows akan menyimpannya secara otomatis di *Credential Manager* sehingga Anda tidak perlu memasukkannya berulang-ulang.

> 💡 **PRO TIP: Credential Manager Windows**
> Windows punya sistem yang nyaman bernama *Git Credential Manager* yang sudah terbundle di Git for Windows. Pertama kali Anda berhasil melakukan push, Windows akan menyimpan token Anda secara otomatis. Selanjutnya, Git akan menggunakannya secara transparan — tanpa perlu mengetik token lagi.

---

## 🆕 Membuat Repositori Baru di GitHub

1. Di GitHub, klik tombol **"+"** di pojok kanan atas → **"New repository"**
2. Isi **Repository name** (misal: `proyek-pertama-saya`)
3. Pilih **Public** atau **Private**
4. **PENTING:** Jangan centang *"Add a README file"* jika Anda sudah punya repo lokal yang ingin dihubungkan. Repositori harus kosong.
5. Klik **Create repository**

Setelah repo dibuat, GitHub akan menampilkan halaman dengan instruksi. Anda akan melihat bagian **"…or push an existing repository from the command line"** — itulah yang akan kita gunakan.

---

## 📡 git remote — Mendaftarkan Alamat GitHub

*Remote* adalah nama panggilan yang kita berikan untuk alamat URL repositori GitHub kita. Namanya bisa apa saja, tapi konvensi yang dipakai seluruh dunia adalah **`origin`**.

```bash
# Daftarkan URL GitHub sebagai remote bernama "origin"
git remote add origin https://github.com/username-anda/proyek-pertama-saya.git

# Verifikasi remote sudah terdaftar
git remote -v
```

**Output `git remote -v`:**
```
origin  https://github.com/username-anda/proyek-pertama-saya.git (fetch)
origin  https://github.com/username-anda/proyek-pertama-saya.git (push)
```

Dua baris itu menunjukkan bahwa `origin` terdaftar untuk dua arah: **fetch** (mengambil dari GitHub) dan **push** (mengirim ke GitHub).

---

## 🚀 git push — Mengirim Karya ke Cloud

Saatnya operasi yang paling ditunggu-tunggu. Perintah `push` mengirimkan *commit* dari repo lokal Anda ke GitHub.

```bash
# Perintah push pertama — flag -u untuk set "upstream" (koneksi default)
git push -u origin main
```

Flag `-u` (atau `--set-upstream`) perlu dipakai **hanya sekali** di push pertama. Fungsinya adalah menghubungkan branch lokal `main` Anda dengan branch `main` di GitHub, sehingga untuk selanjutnya Anda cukup mengetik:

```bash
# Push berikutnya — cukup ini saja
git push
```

**Output sukses:**
```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (5/5), 1.23 KiB | 1.23 MiB/s, done.
Total 5 (delta 0), reused 0 (delta 0)
To https://github.com/username-anda/proyek-pertama-saya.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

Sekarang buka GitHub Anda — kode Anda sudah hidup di internet! 🎉

---

## 📥 git pull — Mengambil Pembaruan dari Cloud

`pull` adalah kebalikan dari `push`. Ia mengambil semua *commit* terbaru dari GitHub dan menggabungkannya ke repo lokal Anda.

```bash
# Ambil dan gabungkan perubahan terbaru dari GitHub
git pull
```

Kapan Anda perlu `git pull`?
- **Saat bekerja di tim**: Rekan Anda baru saja *push* perubahan baru. Jalankan `git pull` agar Anda mendapatkan versi terbaru sebelum mulai bekerja.
- **Saat kerja di beberapa komputer**: Anda *push* dari laptop kantor kemarin, sekarang mau melanjutkan di laptop rumah. Jalankan `git pull` di laptop rumah untuk sinkronisasi.

> ⚠️ **PERINGATAN:**
> Selalu jalankan `git pull` sebelum mulai bekerja dan sebelum melakukan `git push`. Ini mencegah *conflict* yang tidak perlu dan merupakan kebiasaan baik yang membedakan developer junior dari senior.

---

## 📦 git clone — Mengunduh Repositori Orang Lain

`clone` digunakan untuk mengunduh salinan lengkap sebuah repositori dari GitHub ke komputer Anda — termasuk seluruh sejarah *commit* dan semua branch-nya.

```bash
# Clone repo dengan HTTPS (paling mudah untuk pemula)
git clone https://github.com/username/nama-repo.git

# Clone ke folder dengan nama yang berbeda
git clone https://github.com/username/nama-repo.git nama-folder-saya
```

Setelah `clone`, folder baru akan dibuat dan remote `origin` sudah otomatis terdaftar. Anda langsung bisa bekerja.

**Kapan menggunakan `clone`?**
- Saat bergabung dengan tim dan perlu mendapatkan kode proyek yang sudah ada.
- Saat ingin mencoba/berkontribusi pada proyek *open source* yang Anda temukan di GitHub.
- Saat setup laptop baru dan perlu mengambil semua proyek Anda dari GitHub.

---

## 🔄 Workflow Harian: Ritual Lengkap Push & Pull

Inilah pola yang akan Anda jalani setiap hari sebagai developer. Tempel ini di monitor Anda:

```bash
# ═══════════════════════════════════════════════
# RITUAL PAGI: Sebelum mulai coding
# ═══════════════════════════════════════════════

# 1. Pastikan Anda di branch yang benar
git switch main

# 2. Ambil pembaruan terbaru dari tim
git pull

# 3. Buat branch baru untuk pekerjaan hari ini
git switch -c fitur/nama-fitur-hari-ini


# ═══════════════════════════════════════════════
# SELAMA CODING: Siklus save progress
# ═══════════════════════════════════════════════

# 4. Cek apa yang berubah
git status

# 5. Staging perubahan
git add .

# 6. Commit dengan pesan yang deskriptif
git commit -m "Tambah komponen kartu produk"


# ═══════════════════════════════════════════════
# RITUAL SORE: Setelah selesai coding
# ═══════════════════════════════════════════════

# 7. Push branch ke GitHub
git push -u origin fitur/nama-fitur-hari-ini

# 8. Buka GitHub → buat Pull Request untuk diulas tim
```

---

## 🚑 Klinik Darurat: Error Push yang Paling Sering

> [!WARNING]
> **Error: `rejected — non-fast-forward`**
>
> ```
> ! [rejected]        main -> main (non-fast-forward)
> error: failed to push some refs to 'origin'
> ```
>
> **Penyebab**: Ada commit di GitHub yang belum ada di repo lokal Anda. Ini terjadi ketika ada orang lain (atau Anda sendiri dari komputer lain) yang melakukan push lebih dulu.
>
> **Solusi**: Selalu `git pull` sebelum `git push`.
> ```bash
> git pull
> # Selesaikan conflict jika ada
> git push
> ```

> [!WARNING]
> **Error: `Authentication failed`**
>
> ```
> remote: Support for password authentication was removed.
> fatal: Authentication failed for 'https://github.com/...'
> ```
>
> **Penyebab**: Anda memasukkan password akun GitHub, bukan Personal Access Token.
>
> **Solusi**: Buka **Windows Credential Manager** (cari di Start Menu) → **Windows Credentials** → Cari entry `github.com` → **Edit atau Remove** → Coba push lagi dan masukkan token (bukan password) saat diminta.

> [!NOTE]
> **Pertanyaan Umum: Apa perbedaan `git pull` dan `git fetch`?**
>
> `git fetch` hanya **mengunduh** perubahan dari GitHub tanpa menggabungkannya ke kode lokal Anda. `git pull` = `git fetch` + `git merge` dalam satu perintah. Untuk pemula, `git pull` sudah lebih dari cukup.

---

Anda baru saja melampaui batas yang memisahkan seorang programmer yang hanya kerja sendiri dengan seorang developer yang siap berkolaborasi secara profesional.

Push. Pull. Clone. Tiga perintah sederhana yang menjadi fondasi kolaborasi semua tim di dunia — dari startup kecil hingga perusahaan raksasa.

Sekarang, saatnya menyatukan semua yang telah kita pelajari. Di bab terakhir kita, kita akan menjalani simulasi **studi kasus kolaborasi tim nyata** — lengkap dengan *Pull Request*, *Code Review*, dan menyelesaikan *conflict* seperti yang terjadi di dunia industri sesungguhnya. 🎬

---
*Sebelumnya: [Part 4 — Branch & Merge](Part-04-Branch-dan-Merge.md)*
*Selanjutnya: [Part 6 — Studi Kasus: Simulasi Kolaborasi Tim Nyata](Part-06-Studi-Kasus-Kolaborasi-Tim.md)*
