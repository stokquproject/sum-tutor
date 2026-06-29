![Difficulty: Advanced](https://img.shields.io/badge/Tingkat-Mahir-red?style=for-the-badge)
![Time: 20 Mins](https://img.shields.io/badge/Durasi-20_Menit-blue?style=for-the-badge)
![Concept & Practice](https://img.shields.io/badge/Fokus-Konsep_&_Praktik-purple?style=for-the-badge)

# 🎼 Tongkat Konduktor: Mengelola Multi-Container dengan Docker Compose

Selamat datang di Puncak Level 3, Sang Maestro!

Sejauh ini, Anda telah sangat menguasai cara menjalankan satu aplikasi, membuat *Network*, dan merakit brankas *Volume*. Namun, di dunia kerja nyata, sebuah *startup* teknologi tidak hanya menjalankan satu *Container* tunggal. Mereka memiliki setidaknya *Web App* (Node.js), *Database* (PostgreSQL), dan *Cache Server* (Redis) yang harus dinyalakan bersamaan.

Bayangkan betapa tersiksanya Anda jika harus mengetik perintah `docker run ...` yang panjangnya mencapai tiga paragraf secara berulang-ulang, setiap kali Anda ingin menyalakan aplikasi untuk proses *coding*. Melelahkan, rawan salah ketik, dan sama sekali tidak elegan.

Di sinilah Anda membutuhkan sebuah **Tongkat Konduktor**. Mari berkenalan dengan keajaiban teknologi **Docker Compose**.

## 📋 Daftar Isi
- [Era Kegelapan: Kenapa Kita Butuh Compose?](#-era-kegelapan-kenapa-kita-butuh-compose)
- [Mengenal YAML: Kertas Partitur Sang Maestro](#-mengenal-yaml-kertas-partitur-sang-maestro)
- [Misi Praktik: Menggelar Konser Web + Redis](#-misi-praktik-menggelar-konser-web--redis)
- [Keajaiban Satu Tombol (The Wow Factor)](#-keajaiban-satu-tombol-the-wow-factor)

---

## 🌑 Era Kegelapan: Kenapa Kita Butuh Compose?

Jika kita memaksakan diri tanpa *Docker Compose*, untuk menyalakan arsitektur skala menengah (Web + Database), Anda harus mengetik serangkaian perintah manual yang sangat horor ini setiap pagi:

```bash
# Bencana jika harus diketik manual satu-satu setiap kali komputer restart:
docker network create jaringan-app
docker volume create db-data
docker run -d --name my-db --network jaringan-app -v db-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=rahasia mysql:5.7
docker run -d --name my-web --network jaringan-app -p 80:80 -e DB_HOST=my-db nginx:latest
```

Satu saja Anda salah mengetik spasi atau huruf kapital, seluruh sistem Anda akan hancur berantakan. 

**Docker Compose** diciptakan untuk membunuh penderitaan ini. Ia memberikan Anda kemampuan untuk mendeskripsikan *semua* kebutuhan infrastruktur di dalam satu *file* teks tunggal, lalu menjalankannya HANYA dengan satu baris mantra pendek.

---

## 📜 Mengenal YAML: Kertas Partitur Sang Maestro

File magis pembawa kedamaian ini wajib bernama **`docker-compose.yml`**. Ia menggunakan bahasa *YAML*, yang terkenal sangat bersih dan mudah dibaca manusia (karena tidak menggunakan kurung kurawal, hanya mengandalkan jarak spasi/indentasi).

Anggap saja *file* ini sebagai **Kertas Partitur Musik**. Di dalamnya, Anda secara rapi mencatat siapa saja musisi (Container) yang akan bermain, di mana mereka akan duduk (Network), dan alat musik tambahan apa yang mereka bawa (Volume).

Format dasarnya sangat terstruktur:
```yaml
version: '3.8' # Versi aturan tata bahasa Compose

services: # (Mulai mendata Daftar Musisi / Container)
  database_utama:
    image: mysql:5.7
    # ... konfigurasi kerumitan db diletakkan di sini
    
  website_frontend:
    image: nginx:latest
    # ... konfigurasi kerumitan web diletakkan di sini
```

> ⚠️ **PERINGATAN KRUSIAL:**
> Bahasa YAML **SANGAT** sensitif terhadap spasi vertikal. Jangan pernah sekali pun menggunakan tombol `TAB` pada keyboard Anda saat menulis file YAML. Gunakan murni 2 ketukan `SPASI` per blok turunan. Satu spasi bergeser, eksekusi Docker Compose akan seketika meledak (*syntax error*)!

---

## 🚀 Misi Praktik: Menggelar Konser Web + Redis

Mari kita praktikkan momen *Wow* ini. Kita akan membangun aplikasi web yang berpasangan erat dengan *Redis* (sistem *cache in-memory* yang super cepat) hanya dalam hitungan detik.

Buat sebuah folder baru bernama `konser-pertama`, buka *Terminal* di dalam folder tersebut, dan buat sebuah *file* murni bernama `docker-compose.yml`.

Isi *file* tersebut dengan arsitektur elegan di bawah ini:

```yaml
version: '3.8'

services:
  # Container 1: Sang Cache Server (Redis)
  cache_server:
    image: redis:alpine
    container_name: cache-super-cepat
    restart: always

  # Container 2: Sang Web Server Utama (Nginx)
  web_server:
    image: nginx:alpine
    container_name: web-frontend
    ports:
      - "8080:80"
    depends_on:
      - cache_server # Instruksi cerdas: Nginx wajib menunggu Redis menyala lebih dulu!
```

**Perhatikan kejeniusan partitur di atas:**
Apakah Anda melihat kita mengetik aturan *Docker Network*? Tidak! *Docker Compose* secara cerdas akan otomatis memahat *Network* tersembunyi, lalu mengintegrasikan `web_server` dengan `cache_server` sehingga mereka bisa langsung berpelukan (*terkoneksi*). 

---

## 🎇 Keajaiban Satu Tombol (The Wow Factor)

File partitur telah sempurna. Sekarang, angkat tongkat konduktor (*Terminal*) Anda, dan biarkan simfoni dimulai.

Buka terminal di folder tempat file `docker-compose.yml` Anda bersandar, lalu ketik perintah paling legendaris dan paling memuaskan di seluruh jagat Docker:

```bash
# Menyalakan dan mengorkestrasi seluruh arsitektur di background (Detached)
docker-compose up -d
```

> 💡 **THE WOW FACTOR:**
> Hanya dengan menekan tombol *Enter*, saksikan bagaimana *Docker Compose* secara otomatis:
> 1. Mengaudit dan membaca *file* YML Anda.
> 2. Menciptakan Jaringan Virtual (*Network*) secara gaib.
> 3. Mengunduh Image Redis dan Nginx ke laptop Anda (jika belum ada).
> 4. Menghidupkan *Redis* terlebih dahulu (karena patuh pada aturan `depends_on`).
> 5. Menghidupkan *Nginx* dan menjembatani *port* 8080.
>
> 5 langkah raksasa tersebut diselesaikan secara sempurna hanya oleh **satu perintah**!

Buktikan sendiri di radar Anda:
```bash
docker ps
```
Anda akan melihat kedua kapal (Container) berlayar megah secara beriringan.

### Menutup Konser dengan Anggun
Saat proses *development* telah usai dan Anda ingin mematikan *sekaligus* menyapu bersih semua Container dan Network yang barusan terbentuk, Anda sama sekali tidak perlu mengetik `docker rm` satu per satu. Cukup tutup dengan satu tebasan ini:

```bash
# Mematikan, membongkar, dan membersihkan seluruh arsitektur secara instan
docker-compose down
```

Luar biasa! Kini Anda bukan lagi sekadar pelaut biasa. Anda adalah **Sang Maestro** yang mampu memimpin ratusan Container raksasa hanya dari satu naskah.

Ambil napas panjang. Di materi pamungkas (*The Final Project*) berikutnya, kita akan meleburkan segalanya (Web + Database + Volume + Network + Compose) ke dalam satu arsitektur standar perusahaan teknologi skala menengah! 🏆
