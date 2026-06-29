![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 15 Mins](https://img.shields.io/badge/Durasi-15_Menit-blue?style=for-the-badge)
![Concept & Practice](https://img.shields.io/badge/Fokus-Konsep_&_Praktik-purple?style=for-the-badge)

# 🌐 Jembatan Tol Bawah Laut: Menguasai Docker Network

Selamat datang kembali, Sang Arsitek!

Di bab sebelumnya, kita telah membangun "Kedai Kopi" yang canggih dan menempatkan harta kita di dalam "Brankas Database". Namun, jika Anda mencoba menjalankan aplikasi sungguhan, ada satu masalah teknis yang besar: **Secara *default*, setiap Container adalah pulau terpencil.** 

Mereka dikelilingi oleh tembok tebal isolasi. Kedai Kopi Anda tidak bisa mengobrol dengan Brankas Database. Di sinilah Anda perlu unjuk gigi sebagai ahli infrastruktur dengan merakit **Jembatan Tol Bawah Laut** (Docker Network).

Siapkan helm proyek Anda, kita akan menyambungkan pulau-pulau ini!

## 📋 Daftar Isi
- [Tragedi Pulau Terpencil (Mengapa Network Dibutuhkan?)](#-tragedi-pulau-terpencil)
- [Keajaiban Resolusi DNS Internal (The Magic)](#-keajaiban-resolusi-dns-internal-the-magic)
- [Misi Praktik: Menyambungkan WordPress & MySQL](#-misi-praktik-menyambungkan-wordpress--mysql)
- [Kesimpulan Arsitektur](#-kesimpulan-arsitektur)

---

## 🏝️ Tragedi Pulau Terpencil

Salah satu janji keamanan terbesar Docker adalah *isolasi*. Saat Anda menjalankan aplikasi web dan *database* di Container yang berbeda, mereka tidak saling mengenal, tidak saling melihat, dan tidak bisa saling berbicara. 

Ratusan pemula jatuh ke dalam jurang ini setiap harinya: Mereka mencoba menghubungkan aplikasi dengan database menggunakan *IP Address* bawaan laptop mereka (seperti `localhost` atau `127.0.0.1`). 

> ⚠️ **PERINGATAN KRUSIAL:**
> Di dalam Container, `localhost` merujuk pada **diri Container itu sendiri**, BUKAN komputer laptop Anda! Jika Container Web Anda mencoba memanggil `localhost:3306`, ia akan mengaduk-aduk perutnya sendiri mencari database (yang jelas tidak ada), lalu seketika mengalami *crash*.

Solusi elegan untuk masalah ini? Kita buatkan mereka satu **jaringan virtual eksklusif (*network*)** yang sama.

---

## 🎩 Keajaiban Resolusi DNS Internal (The Magic)

Sebelum kita mengetik perintah terminal, ada satu rahasia besar tentang *Docker Network* yang akan menghemat ribuan jam kerja Anda: **Automatic DNS Resolution**.

Di arsitektur jaringan tradisional, Anda harus susah payah menghafal *IP Address* statis (seperti `192.168.1.5`). 
Di dalam ekosistem *Docker Network*, Anda bisa memanggil Container lain **hanya dengan menggunakan nama Container-nya!** 

Docker bertindak layaknya buku telepon pintar rahasia. Jika Anda menamai Container database Anda `mysql-rahasia`, maka aplikasi web Anda cukup memasukkan `mysql-rahasia` pada kolom pengisian *Database Host*. Bebas repot, bebas pusing!

---

## 🚢 Misi Praktik: Menyambungkan WordPress & MySQL

Mari kita wujudkan keajaiban ini secara *real-time*. Misi kita: Membuat satu jaringan eksklusif, meletakkan database MySQL di sana, dan menyambungkan *Content Management System* (WordPress) agar bisa berkomunikasi intim dengannya.

### Langkah 1: Merakit Jembatan Tol
Pertama, kita harus membuat entitas jaringan (*network*) terlebih dahulu. Kita beri nama `jaringan-tol-kita`.

```bash
# Membuat jembatan (network) bertipe 'bridge' (tipe standar untuk pemakaian 1 laptop)
docker network create jaringan-tol-kita
```

### Langkah 2: Meletakkan Brankas Database di Jembatan
Kita jalankan MySQL, berikan *password*, dan **wajib** kita sambungkan ke `--network` yang baru saja kita rakit.

```bash
# -e MYSQL_DATABASE : Meminta MySQL untuk otomatis membuat database kosong bernama 'db_wordpress'
# --network : Menempelkan container ini ke jembatan tol rahasia kita
docker run -d --name mysql-server \
  --network jaringan-tol-kita \
  -e MYSQL_ROOT_PASSWORD=rahasia123 \
  -e MYSQL_DATABASE=db_wordpress \
  mysql:5.7
```

### Langkah 3: Menjalankan Aplikasi Web (WordPress)
Sekarang, mari luncurkan kapal WordPress, tempelkan ke jembatan yang *sama*, dan beri tahu WordPress siapa nama *host* database-nya.

```bash
# WORDPRESS_DB_HOST=mysql-server : Ini adalah THE WOW FACTOR! 
# Kita TIDAK mengetik IP Address acak, kita cukup memanggil nama container database-nya!
docker run -d --name web-wordpress \
  --network jaringan-tol-kita \
  -p 8080:80 \
  -e WORDPRESS_DB_HOST=mysql-server \
  -e WORDPRESS_DB_USER=root \
  -e WORDPRESS_DB_PASSWORD=rahasia123 \
  -e WORDPRESS_DB_NAME=db_wordpress \
  wordpress:latest
```

> 💡 **THE WOW FACTOR:**
> Tunggu sekitar 15-20 detik (WordPress butuh waktu sedikit untuk *booting*), lalu buka `http://localhost:8080` di browser Anda.
> 
> Halaman *Setup* Instalasi WordPress yang sangat ikonik itu akan menyapa Anda! Di balik layar, WordPress (Container A) berhasil "menelepon" MySQL (Container B) tanpa mengetahui IP Address-nya sama sekali, hanya bermodalkan *Nama Container* berkat magis dari **Jembatan Tol Bawah Laut** kita.

---

## 🎯 Kesimpulan Arsitektur

Dengan menguasai *Docker Network*, Anda telah berevolusi dari sekadar *operator* biasa menjadi seorang **Arsitek Infrastruktur Sejati**. Anda kini memegang prinsip bahwa:

1. Setiap Container secara alami diisolasi (pulau terpencil).
2. Jangan pernah menggunakan `localhost` untuk komunikasi antar-container.
3. Gunakan `docker network create` untuk merajut jembatan komunikasi yang kokoh.
4. Manfaatkan nama Container sebagai nama *Host* (DNS otomatis) untuk komunikasi yang sangat adaptif.

Karya seni arsitektur Anda hampir sempurna! Di bab berikutnya, kita akan beranjak dari sekadar menggunakan "Buku Resep" milik orang lain, menjadi **Seorang Koki Bintang Lima** yang meracik *Dockerfile* mahakaryanya sendiri! 👨‍🍳
