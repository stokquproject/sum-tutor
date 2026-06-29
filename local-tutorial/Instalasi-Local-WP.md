![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 5 Mins](https://img.shields.io/badge/Durasi-5_Menit-blue?style=for-the-badge)
![Killer Feature](https://img.shields.io/badge/Fitur-One_Click_WP-critical?style=for-the-badge)

# 🚀 Prolog: Instalasi WordPress dalam 10 Detik (Tanpa Stres)

Bagi seorang kreator WordPress, *Agensi Web*, atau *Freelancer*, waktu adalah uang. 

Mari kita hitung berapa banyak waktu yang terbuang saat Anda ingin memulai proyek *website* klien baru menggunakan cara tradisional (XAMPP/WAMP):
1. Pergi ke *wordpress.org* > Unduh file `.zip`.
2. Buka folder `htdocs`, buat folder baru, lalu ekstrak puluhan ribu *file* WP.
3. Buka peramban, buka `localhost/phpmyadmin` yang lambat.
4. Buat *database* baru secara manual.
5. Buka tab baru `localhost/proyek-baru`.
6. Isi konfigurasi *database* (user: `root`, *password* kosong).
7. Tunggu instalasi selesai.

Tujuh langkah menyiksa ini bisa memakan waktu hingga **15-20 menit** hanya untuk melihat halaman kosong WordPress. 

Hari ini, kita akan menghancurkan rutinitas tersebut. Kita akan berkenalan dengan sebuah alat ajaib yang memangkas waktu 15 menit menjadi **10 detik**. Mari berkenalan dengan **Local** (sebelumnya dikenal sebagai *Local by Flywheel*).

## 📋 Daftar Isi
- [Kematian Era Setup Manual](#-kematian-era-setup-manual)
- [Apa itu "Local"?](#-apa-itu-local)
- [Praktik: Sihir 3 Klik WordPress](#-praktik-sihir-3-klik-wordpress)
- [The "Wow" Factor: Gembok Hijau SSL (HTTPS)](#-the-wow-factor-gembok-hijau-ssl-https)

---

## ⚰️ Kematian Era Setup Manual

XAMPP dan Laragon adalah alat yang luar biasa hebat bagi *programmer* yang menulis kode dari nol (*PHP native* atau Laravel). Namun, jika **90% hidup Anda** hanya dihabiskan untuk membuat *website* WordPress, menggunakan XAMPP ibarat memakai mobil *Dump Truck* hanya untuk pergi membeli kopi di depan rumah.

Anda butuh sebuah kendaraan *sport* yang didesain 100% khusus untuk ekosistem WordPress. Sebuah alat di mana Anda tidak perlu lagi menyentuh *file* `wp-config.php`, tidak perlu tahu apa itu *Database User*, dan tidak perlu dipusingkan dengan folder ekstraksi.

---

## ⚡ Apa itu "Local"?

**Local (localwp.com)** adalah aplikasi revolusioner gratis yang diciptakan oleh WP Engine, salah satu raksasa *hosting* WordPress dunia.

Aplikasi ini memiliki satu filosofi: **Biarkan mesin yang bekerja, biarkan manusia yang berkreativitas.**

Local menyembunyikan semua kerumitan *server*, *database*, dan konfigurasi Apache/Nginx di balik sebuah antarmuka (*UI*) yang sangat elegan, modern, dan semudah menggunakan aplikasi pemutar musik.

---

## 🪄 Praktik: Sihir 3 Klik WordPress

Mari kita panggil kendaraan *sport* ini ke garasi Anda:

1. Kunjungi **[localwp.com](https://localwp.com/)** dan unduh aplikasinya (Tersedia untuk Mac, Windows, dan Linux).
2. Lakukan instalasi biasa layaknya aplikasi normal (hanya *Next* dan *Next*).
3. Setelah terinstal, buka aplikasi **Local**.

**Perhatikan jam Anda, dan bersiaplah untuk terpukau:**

1. Di jendela utama Local, klik ikon plus hijau raksasa bertuliskan **"Add Local Site"**.
2. Pilih opsi **"Create a new site"** dan klik *Continue*.
3. **Klik ke-1:** Ketik nama proyek klien Anda (Misal: `Toko Baju Keren`), klik *Continue*.
4. **Klik ke-2:** Biarkan pilihan di *Preferred* (Local akan mencarikan versi PHP dan MySQL terbaik secara otomatis), klik *Continue*.
5. **Klik ke-3:** Ketik *Username* dan *Password* untuk masuk ke WordPress Anda (Misal: `admin` & `password`), lalu klik **Add Site**.

**Selesai. Anda sudah boleh bersandar.** ☕

Dalam hitungan detik, Local akan membangun arsitektur *server*, membuat *database*, mengunduh WordPress terbaru, menginstalnya, menyambungkannya, dan mendaftarkan *domain* cantik `tokobajukeren.local` ke laptop Anda.

Klik tombol **"Open Site"** atau **"WP Admin"** di kanan atas, dan Anda akan langsung dibawa ke halaman *login* WordPress yang sudah hidup dan bernapas!

---

## 🔒 The "Wow" Factor: Gembok Hijau SSL (HTTPS)

Pernahkah Anda membuat web di XAMPP, lalu menyadari alamatnya adalah `http://localhost`, dengan peringatan menyebalkan berwarna merah bertuliskan **"Not Secure"** di peramban Chrome Anda? 

Di era modern, membuat *website* tanpa SSL (HTTPS) akan merusak banyak fitur integrasi modern (*seperti Payment Gateway atau API tertentu yang mewajibkan HTTPS*). Mengatur SSL secara lokal di Windows/Mac adalah sebuah mimpi buruk teknis yang melibatkan *OpenSSL* dan sertifikat buatan sendiri yang sering ditolak peramban.

**Bagaimana cara Local mengatasinya?**
1. Di halaman detail *website* Anda pada aplikasi Local, perhatikan baris bertuliskan **"SSL"**.
2. Di sebelah kanan, ada tombol **"Trust"**. Klik tombol tersebut.
3. *Windows/Mac* Anda akan meminta izin, klik *Yes*.

**BOOM! 🤯**
Buka situs Anda. Peringatan merah yang menyebalkan itu telah lenyap. Digantikan oleh **Gembok Hijau** (atau ikon aman) yang menandakan bahwa situs lokal Anda kini berjalan di jalur **HTTPS murni** (`https://tokobajukeren.local`). 

Tanpa baris kode, tanpa stres, murni keajaiban dalam satu tombol "Trust".

Di bab selanjutnya, kita akan membongkar senjata rahasia andalan para *Agensi Web* raksasa: **Fitur Blueprint**. Bayangkan memiliki mesin fotokopi yang bisa menggandakan struktur *website*, tema, dan *plugin* favorit Anda secara tak terbatas dalam hitungan detik! 🧬
