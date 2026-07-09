![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 5 Mins](https://img.shields.io/badge/Durasi-5_Menit-blue?style=for-the-badge)
![Database Setup](https://img.shields.io/badge/Fokus-Infrastruktur_Data-purple?style=for-the-badge)

# 🗄️ Pasangan Sejati: Meracik Valet dengan DBngin

Peringatan pertama bagi pengungsi XAMPP dan MAMP yang baru saja hijrah ke Valet: **Anda akan kebingungan mencari di mana letak MySQL dan phpMyAdmin.**

Valet secara harfiah diciptakan HANYA untuk mengurus server web (Nginx) dan PHP. Tidak ada yang lain. 
Ini bukan sebuah kekurangan, melainkan filosofi kesempurnaan. Sang Ninja tidak membawa bagasi berat; ia hanya membawa pedang. Untuk membawa perbekalan data, Ninja membutuhkan rekan seperjalanan.

Dulu, meracik MySQL atau PostgreSQL di Mac mengharuskan kita berurusan lagi dengan rumitnya instalasi via *Homebrew*. Namun hari ini, saya akan memperkenalkan Anda pada pasangan sejati sang Ninja: sebuah aplikasi mahakarya bernama **DBngin**.

## 📋 Daftar Isi
- [Filosofi Tanpa Bagasi](#-filosofi-tanpa-bagasi)
- [Memperkenalkan DBngin (Sang Brankas Mewah)](#-memperkenalkan-dbngin-sang-brankas-mewah)
- [Praktik: Membangun Pabrik Data](#-praktik-membangun-pabrik-data)
- [Mengintip Isi Brankas (Alternatif phpMyAdmin)](#-mengintip-isi-brankas-alternatif-phpmyadmin)

---

## 🎒 Filosofi Tanpa Bagasi

Mengapa Valet tidak mem- *bundle* (membungkus) MySQL di dalam *installer*-nya?

Karena dunia modern sangatlah dinamis. 
Mungkin hari ini proyek Anda menggunakan **MySQL**. Besok, klien menuntut penggunaan **PostgreSQL**. Lusa, fitur aplikasi Anda mewajibkan antrean *cache* berkecepatan tinggi menggunakan **Redis**.

Jika Valet memaksakan satu jenis *database*, ia akan mengkhianati kelincahannya sendiri. Oleh karena itu, Valet menyerahkan hak prerogatif pemilihan senjata data sepenuhnya ke tangan Anda.

---

## 💎 Memperkenalkan DBngin (Sang Brankas Mewah)

Bertarung dengan *Homebrew* untuk menginstal 3 jenis *database* berbeda adalah hal yang memusingkan. 
Sebagai gantinya, gunakan **DBngin** (dbngin.com).

DBngin adalah sebuah aplikasi Mac (*GUI*) gratis, sangat ringan, dan memiliki antarmuka yang sangat indah (dibuat oleh kreator aplikasi TablePlus). 
DBngin bertindak sebagai *Switchboard* (Papan Kendali) pelayan data. Dengan aplikasi ini, Anda bisa menyalakan berbagai versi MySQL, PostgreSQL, dan Redis hanya dengan satu klik *mouse* layaknya memutar kunci kontak mobil.

---

## 🏭 Praktik: Membangun Pabrik Data

Mari kita meracik pelayan setia untuk sang Ninja.

1. Buka peramban, unduh dan instal **DBngin** dari situs resminya (`https://dbngin.com`).
2. Buka aplikasi DBngin. Anda akan disambut oleh antarmuka minimalis yang elegan.
3. Klik tombol **`+` (New Server)** di pojok kanan atas.
4. Pilih Service: **MySQL** (Atau PostgreSQL/Redis sesuai selera Anda).
5. Pilih Version: (Gunakan versi terbaru yang tersedia, misalnya 8.0).
6. Beri nama server ini (misal: `MySQL Lokal`), lalu klik **Create**.
7. Di layar utama, Anda akan melihat *server* Anda tertidur. Klik tombol **Start**.

Lampu hijau menyala, dan *database* Anda kini hidup di *port default* (`3306`).
**Selesai!** Tidak ada *command line*, tidak ada *error* konfigurasi. Anda memiliki pelayan data yang sempurna untuk Valet.

*(Penting: Default Username MySQL di DBngin adalah `root` dengan Password kosong).*

---

## 👁️ Mengintip Isi Brankas (Alternatif phpMyAdmin)

Karena XAMPP tidak ada, maka `localhost/phpmyadmin` otomatis hilang dari hidup Anda.
Bagaimana cara Anda membuat *database* atau melihat isi tabel? Anda memiliki dua opsi berkelas:

**Opsi 1: Sang Profesional (Gunakan Aplikasi Desktop - Direkomendasikan)**
Karena Anda sudah menggunakan Mac, unduhlah aplikasi **TablePlus**, **Sequel Ace** (Gratis), atau **DBeaver**. Aplikasi ini menempel langsung ke *database* Anda dengan kecepatan super, jauh lebih responsif dan aman daripada phpMyAdmin berbasis peramban.

**Opsi 2: Pejuang Tradisi (Menginstal phpMyAdmin di Valet)**
Jika Anda masih *kangen* dengan phpMyAdmin, Anda bisa meletakkannya di Valet!
1. Unduh *file zip* phpMyAdmin dari situs resminya dan ekstrak.
2. Ganti nama foldernya menjadi `phpmyadmin` dan pindahkan folder tersebut ke dalam *Lahan Parkir* (misal: `~/Sites/phpmyadmin`).
3. Buka peramban Anda, dan ketik **`http://phpmyadmin.test`**.
Ajaib! phpMyAdmin Anda kembali hidup melayani *database* dari DBngin.

Anda kini memiliki Ekosistem Lokal Mac yang paling ditakuti: **Valet** untuk kecepatan *routing*, dan **DBngin** untuk manajemen data.

Anda menyebutkan adanya **Level 4**! Apa misi pamungkas yang disiapkan Sang Arsitek untuk sang Ninja ini? 🥷🚀
