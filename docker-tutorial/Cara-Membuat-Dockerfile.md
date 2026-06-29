![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 20 Mins](https://img.shields.io/badge/Durasi-20_Menit-blue?style=for-the-badge)
![Code: Dockerfile](https://img.shields.io/badge/Kode-Dockerfile-purple?style=for-the-badge)

# 👨‍🍳 Dapur Bintang Lima: Meracik Dockerfile Sempurna

Selamat datang di dapur utama, *Chef*! 

Sejauh ini, kita hanya menjadi pelanggan yang baik: mengambil "Buku Resep" (Image) buatan orang lain (seperti MySQL atau Nginx) dari *Docker Hub*, lalu menyeduhnya. Namun, sebagai seorang *Software Engineer* sejati, Anda pasti memiliki aplikasi mahakarya Anda sendiri (berupa *code* Node.js, Python, atau PHP) yang ingin Anda kemas ke dalam Container.

Untuk itu, Anda harus mampu menulis resep Anda sendiri. Di dunia Docker, kertas resep yang sakral ini bernama **Dockerfile**. 

Mari kenakan celemek Anda, kita akan meracik mahakarya pertama Anda dari nol.

## 📋 Daftar Isi
- [Anatomi Sebuah Resep (Kosakata Dockerfile)](#-anatomi-sebuah-resep-kosakata-dockerfile)
- [Misi Praktik: Mengemas Aplikasi Node.js](#-misi-praktik-mengemas-aplikasi-nodejs)
- [Bakar di Oven: Proses Build & Run](#-bakar-di-oven-proses-build--run)
- [Rahasia Koki Bintang Lima (.dockerignore & Alpine)](#-rahasia-koki-bintang-lima-dockerignore--alpine)

---

## 🔪 Anatomi Sebuah Resep (Kosakata Dockerfile)

*Dockerfile* hanyalah sebuah *file teks biasa* tanpa ekstensi apa pun (ya, namanya secara literal harus `Dockerfile`). Di dalamnya berisi sekumpulan instruksi berurutan layaknya resep memasak yang dibaca oleh mesin.

Berikut adalah 6 kosakata (instruksi) wajib yang harus Anda kuasai di luar kepala:

1. **`FROM`**: Bahan dasar. Kita tidak pernah benar-benar merakit *server* dari nol. Kita selalu meminjam OS mini (misal: Ubuntu tipis atau Node OS) sebagai fondasi.
2. **`WORKDIR`**: Talenan (meja kerja). Menentukan secara spesifik di folder (direktori) mana kita akan bekerja di dalam Container nanti.
3. **`COPY`**: Tindakan memindahkan/menyalin bahan dari dapur fisik Anda (Laptop lokal) ke dalam panci Container.
4. **`RUN`**: Mengeksekusi perintah terminal *pada saat proses memasak/build berlangsung* (misal: menginstal dependensi dengan `npm install`).
5. **`EXPOSE`**: Sebuah plang pengumuman ke dunia luar, port ke berapa yang akan digunakan oleh aplikasi ini.
6. **`CMD`**: Perintah puncak (*final execution*) saat Container *mulai dihidupkan* (menyajikan hidangan). Sebuah *Dockerfile* hanya boleh memiliki maksimal satu `CMD`!

---

## 🍳 Misi Praktik: Mengemas Aplikasi Node.js

Bayangkan Anda baru saja selesai membuat aplikasi *backend* Node.js sederhana (berisi file `package.json` dan `server.js`). Mari kita tulis resep *deployment*-nya. 

Buat sebuah file bernama `Dockerfile` (tanpa .txt) di dalam folder *source code* Anda, lalu tulis arsitektur elegan berikut:

```dockerfile
# 1. BAHAN DASAR (Kita gunakan lingkungan Node.js versi 18 LTS)
FROM node:18

# 2. MEJA KERJA (Semua aktivitas selanjutnya akan diisolasi di dalam folder /app)
WORKDIR /app

# 3. MASUKKAN RESEP DEPENDENSI LEBIH DULU 
# (Trik optimasi tingkat tinggi: Copy package.json sebelum file source code utama)
COPY package.json .

# 4. INSTAL DEPENDENSI (Mengaduk adonan dengan NPM)
RUN npm install

# 5. MASUKKAN SISA KODE APLIKASI
# Copy semua file dari laptop (titik pertama) ke dalam WORKDIR container (titik kedua)
COPY . .

# 6. BUKA PINTU KONEKSI (Beritahu infra bahwa aplikasi kita mendengarkan di port 3000)
EXPOSE 3000

# 7. SAJIKAN HIDANGAN! (Perintah stater saat container 'docker run' dipanggil)
CMD ["node", "server.js"]
```

> 💡 **THE WOW FACTOR (Rahasia Caching):**
> Mengapa kita sengaja memisahkan `COPY package.json` (Langkah 3) dan `COPY . .` (Langkah 5)? 
> Ini adalah sihir *Docker Layer Caching*! Jika Anda besok hanya mengubah warna tombol di *file* HTML/JS Anda, Docker tidak perlu membuang waktu dan kuota 100MB untuk me-*reinstall* semua `node_modules`. Ia cukup menggunakan *cache* Langkah 4 dan langsung melompat memproses Langkah 5. Ini memangkas waktu *build* aplikasi Anda dari 3 Menit menjadi **kurang dari 2 Detik**!

---

## 🔥 Bakar di Oven: Proses Build & Run

Resep tulisan tangan Anda sudah siap. Sekarang saatnya menyerahkan kertas resep tersebut ke mesin cuci Docker agar dibentuk wujudnya menjadi sebuah **Image** (Cetak Biru permanen). Proses vital ini disebut **Build**.

Buka terminal persis di lokasi folder yang sama dengan *file* `Dockerfile` Anda berada, dan ucapkan mantra ini:

```bash
# -t : (Tag) Memberikan nama merek dagang pada image Anda (contoh: aplikasi-kopi-saya)
# TITIK (.) di akhir SANGAT KRUSIAL! Artinya "Gunakan Dockerfile yang ada di folder ini"
docker build -t aplikasi-kopi-saya .
```

Terminal Anda akan mulai berjalan bak adegan di film The Matrix. Docker membaca resep Anda baris demi baris, mengunduh OS Node.js dari *cloud*, dan merekatkannya dengan *source code* Anda menjadi satu bongkahan Image yang kokoh.

Setelah selesai, buktikan keberhasilannya:
```bash
# Cek apakah Image 'aplikasi-kopi-saya' sudah memajang diri di rak lokal Anda
docker images
```

Sekarang, sajikan hidangan (Image) tersebut menjadi **Container** yang hidup:
```bash
docker run -d --name web-kopi -p 3000:3000 aplikasi-kopi-saya
```

**Boom!** Aplikasi Anda kini hidup secara mandiri dan terisolasi di dalam Container. Keindahan terbesarnya? Anda bisa membawa *Image* `aplikasi-kopi-saya` ini ke server *Linux*, *Mac*, atau *Windows* mana pun di muka bumi, dan ia **DIJAMIN** akan berjalan dengan absolut tanpa sedikit pun *error* "*It works on my machine*"!

---

## 🌟 Rahasia Koki Bintang Lima (.dockerignore & Alpine)

Seorang pemula (*Junior*) seringkali menghasilkan Image bengkak sebesar **1.5 GB**. 
Seorang *Chef Profesional (Senior)* bisa menghasilkan Image dengan fitur yang sama persis, tapi berukuran hanya **50 MB**.

Inilah dua resep rahasia mereka:

### 1. Tameng `.dockerignore`
Sama persis filosofinya dengan `.gitignore`, *file* sakti ini akan melarang Docker untuk ikut membungkus (*COPY*) *file-file* sampah raksasa (seperti folder `node_modules` bawaan di laptop Anda, atau log sisa *debugging*) ke dalam Image.
Buat *file* `.dockerignore` dan lindungi *project* Anda dengan baris ini:
```text
node_modules
npm-debug.log
.git
.env
```

### 2. Diet Ketat dengan "Alpine" Linux
Saat memilih pondasi bahan dasar (`FROM`), para ahli akan selalu berburu versi **`alpine`**. Alpine adalah sebuah varian distro Linux yang sudah dipangkas habis-habisan khusus demi mengejar efisiensi di dunia Docker (ukuran dasar OS-nya gila-gilaan, hanya sekitar **~5 MB**!).

Cukup ubah baris teratas Dockerfile Anda dari `FROM node:18` menjadi:
```dockerfile
# Menggunakan versi Alpine (Diet) yang super ramping dan ngebut
FROM node:18-alpine
```

> ⚠️ **PERINGATAN:**
> *Alpine* ukurannya sangat kecil karena secara sengaja membuang banyak perkakas dasar yang ada di Linux pada umumnya. Terkadang, jika aplikasi Anda sangat bergantung pada sistem kompilasi biner C++ yang agresif (seperti *node-gyp* atau instalasi pustaka Python berbasis C tertentu), proses kompilasi di *Alpine* akan *error*. Jika Anda menabrak tembok itu, mundurlah sedikit menggunakan versi tipe `slim` (misal: `node:18-slim`) sebagai *middle-ground*.

---

**Penghormatan untuk Anda, Chef!** 🥂
Hari ini, Anda tidak hanya belajar menikmati masakan orang lain. Anda berhasil meracik, membangun, dan menyajikan mahakarya resep (Image) Anda sendiri. Image buatan Anda kini sudah berstatus Sangat Portabel, Sangat Ringan, dan **Siap Diluncurkan ke Production!**
