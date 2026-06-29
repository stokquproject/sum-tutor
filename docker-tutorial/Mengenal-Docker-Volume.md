![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 15 Mins](https://img.shields.io/badge/Durasi-15_Menit-blue?style=for-the-badge)
![Concept & Practice](https://img.shields.io/badge/Fokus-Konsep_&_Praktik-purple?style=for-the-badge)

# 💾 Brankas Anti-Badai: Menyelamatkan Data dengan Docker Volume

Selamat datang di Level 2, Sang Arsitek!

Di akhir Level 1, kita menghadapi kenyataan teknis yang pahit: Saat Anda meratakan "Kedai Kopi" (Container) dengan perintah `docker rm`, semua racikan kopi, mesin kasir, dan catatan pembukuan di dalamnya ikut lenyap tak bersisa. 

Dalam dunia nyata, jika ini terjadi pada *database* pelanggan Anda, itu adalah sebuah bencana fatal (sekaligus surat pemecatan instan!). 

Sifat dasar container memang *ephemeral* (sementara). Untuk menyimpan data yang berharga secara permanen dan menembus batas usia hidup container, kita butuh sebuah **Brankas Anti-Badai**. Mari kita bangun brankas tersebut.

## 📋 Daftar Isi
- [Dua Senjata Utama: Bind Mounts vs Volumes](#-dua-senjata-utama-bind-mounts-vs-volumes)
- [Peta Visual: Bagaimana Data Mengalir?](#-peta-visual-bagaimana-data-mengalir)
- [Praktik 1: Menggunakan Bind Mount (Flashdisk Eksternal)](#-praktik-1-menggunakan-bind-mount-flashdisk-eksternal)
- [Praktik 2: Menggunakan Docker Volume (Brankas Bank)](#-praktik-2-menggunakan-docker-volume-brankas-bank)
- [Jadi, Saya Harus Pilih yang Mana?](#-jadi-saya-harus-pilih-yang-mana)

---

## ⚔️ Dua Senjata Utama: Bind Mounts vs Volumes

Agar data Anda selamat meski Container-nya meledak berkeping-keping, Docker menyediakan dua mekanisme elegan untuk menitipkan data ke sistem komputer utama Anda (*Host*).

1. **Bind Mounts (Sang Flashdisk Eksternal)**
   Anda menunjuk satu folder spesifik di laptop Anda (misal: `C:\Proyek\data`), dan seolah-olah "mencolokkannya" ke dalam Container. Perubahan sekecil apa pun pada file di laptop Anda akan seketika berubah di dalam Container, begitu pula sebaliknya. Teknik ini ibarat dewa bagi *developer* yang sedang melakukan proses *coding*.

2. **Docker Volumes (Sang Brankas Bank Rahasia)**
   Anda meminta Docker membuat sebuah brankas khusus yang letaknya dirahasiakan (dikelola 100% secara tertutup oleh Docker, Anda tidak perlu pusing memikirkan letak foldernya di mana). Ini adalah cara paling aman, cepat, dan paling disarankan untuk menyimpan data produksi yang sakral (seperti Database).

---

## 🗺️ Peta Visual: Bagaimana Data Mengalir?

Mari kita bedah perbedaan mendasarnya melalui arsitektur visual ini:

```mermaid
graph TD
    subgraph Komputer Host (Laptop Anda)
        B[Folder Bebas Milik Anda<br/>Misal: /Users/mac/proyek]:::bind
        C[Area Rahasia Docker<br/>/var/lib/docker/volumes/...]:::vol
    end

    subgraph Dunia Container
        D((Container Web / Database)):::cont
    end

    B <==>|1. Bind Mount| D
    C <==>|2. Docker Volume| D

    classDef bind fill:#ffcccc,stroke:#ff0000,stroke-width:2px;
    classDef vol fill:#ccddff,stroke:#0000ff,stroke-width:2px;
    classDef cont fill:#ccffcc,stroke:#00aa00,stroke-width:4px;
```

*(Perhatikan bagaimana Docker Volume diisolasi di area yang aman dari intervensi campur tangan manusia secara langsung).*

---

## 🔌 Praktik 1: Menggunakan Bind Mount (Flashdisk Eksternal)

Mari kita ulangi studi kasus "Kedai Kopi" Nginx, tapi kali ini dengan kekuatan ajaib **Bind Mount**. Kita akan menyambungkan folder di laptop Anda secara *real-time* ke dalam *web server*.

Buat folder baru bernama `website-saya` di komputer Anda, dan buat file teks biasa `index.html` di dalamnya. Lalu buka terminal tepat di folder tersebut.

```bash
# -v : Singkatan dari Volume/Mount (Teknik menyambungkan folder).
# Aturan penulisannya adalah: -v /path/laptop/anda:/path/dalam/container
# $(pwd) adalah trik Linux/Mac untuk mengambil path lokasi folder Anda saat ini secara otomatis.

docker run -d --name kedai-kopi-bind -p 8080:80 \
  -v $(pwd)/website-saya:/usr/share/nginx/html \
  nginx:alpine
```

**Momen Aha!**
Sekarang, cobalah edit file `index.html` menggunakan editor favorit Anda (VS Code, Notepad, dll). Simpan file tersebut, lalu *refresh* browser Anda di `http://localhost:8080`. 

Tada! Halaman web berubah secara instan tanpa perlu me-*restart* Container atau masuk secara manual menggunakan perintah `docker exec`. Inilah kekuatan *Live Reloading* dari *Bind Mount*!

---

## 🏦 Praktik 2: Menggunakan Docker Volume (Brankas Bank)

Bagaimana jika kita ingin mengamankan database raksasa seperti MySQL? Kita tidak peduli *file* mentahnya disimpan di mana, yang terpenting adalah data tersebut dijamin aman, tidak lambat diakses, dan bebas konflik. Inilah panggung utama bagi **Docker Volume**!

**Langkah 1: Membuat Brankas**
```bash
# Memerintahkan Docker untuk memahat sebuah brankas baru bernama "brankas-db"
docker volume create brankas-db
```

**Langkah 2: Menyambungkan Brankas ke Mesin Database**
```bash
# Menjalankan MySQL dan menempelkan "brankas-db" tepat di urat nadinya: /var/lib/mysql
docker run -d --name database-rahasia \
  -e MYSQL_ROOT_PASSWORD=superrahasia \
  -v brankas-db:/var/lib/mysql \
  mysql:latest
```

> 💡 **THE WOW FACTOR:**
> Uji keberanian Anda: Jalankan perintah torpedo ini `docker rm -f database-rahasia` untuk menghancurkan database tersebut hingga rata dengan tanah.
> 
> Hancur? Ya. Tapi data pelanggannya? **Tetap tertata rapi di dalam `brankas-db`!** Anda hanya perlu menjalankan ulang perintah di *Langkah 2*, dan seketika semua data pelanggan Anda kembali utuh tanpa cacat sedikit pun. Anda baru saja menguasai teknik menyelamatkan miliaran rupiah!

---

## ⚖️ Jadi, Saya Harus Pilih yang Mana?

Banyak pemula kebingungan harus menggunakan skema yang mana. Jadikan tabel ini kompas emas Anda:

| Kondisi / Kasus Penggunaan | Senjata Terbaik | Alasan Utama |
| :--- | :--- | :--- |
| Anda sedang asyik *coding* (*Live Reloading*) | **Bind Mounts** 🔌 | Memungkinkan Anda merombak *source code* secara *real-time* langsung dari laptop. |
| Menyimpan data vital Database (MySQL, Postgres) | **Docker Volumes** 🏦 | Performa I/O jauh lebih ngebut, sangat aman, dan 100% dikelola oleh Docker. |
| Sekadar menyisipkan *config file* tunggal | **Bind Mounts** 🔌 | Praktis untuk melempar satu file `nginx.conf` dari luar ke dalam Container. |
| Container harus dipindah-pindah OS (Win/Mac/Linux) | **Docker Volumes** 🏦 | Ekstrem adaptif karena tidak bergantung pada struktur direktori OS (*bebas dari tragedi konflik `C:\` vs `/`*). |

Luar biasa! Sekarang Anda bisa tidur nyenyak di malam hari tanpa ketakutan kehilangan data. Bangunan (Container) Anda boleh roboh berkali-kali diterjang badai, namun Brankas Anda akan tetap abadi. 

Selanjutnya, kita akan membangun "Infrastruktur Jembatan" agar Kedai Kopi kita bisa mengobrol eksklusif dengan Brankas Database ini melalui Jaringan Bawah Laut (*Docker Network*)! 🌐
