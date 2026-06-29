![Difficulty: Expert](https://img.shields.io/badge/Tingkat-Pakar-red?style=for-the-badge)
![Time: 30 Mins](https://img.shields.io/badge/Durasi-30_Menit-blue?style=for-the-badge)
![Hands-on: Project](https://img.shields.io/badge/Praktik-Proyek_Akhir-critical?style=for-the-badge)

# 🚀 Misi Puncak: Deploy Arsitektur Skala Menengah ala Senior DevOps

Selamat datang di garis *finish*, Kapten! 

Sejak awal perjalanan ini, Anda telah menyerap puluhan konsep berat: mulai dari membedakan resep dengan kue (*Image vs Container*), membuat brankas data tahan banting (*Volumes*), membentangkan jembatan komunikasi (*Networks*), meracik resep buatan sendiri (*Dockerfile*), hingga memegang tongkat ajaib (*Compose*). 

Kini saatnya merangkai **seluruh** potongan *puzzle* tersebut menjadi satu kesatuan raksasa. Misi puncak kita adalah membangun ekosistem aplikasi dunia nyata yang sangat sering digunakan di fase *Production*: **Sebuah Web CMS (WordPress), Database (MySQL), dan Panel Manajemen GUI (phpMyAdmin)**—semuanya diotomatisasi dari dalam satu *file* sakti.

Mari kita selesaikan ini dengan gaya dan ketenangan seorang *Senior DevOps*!

## 📋 Daftar Isi
- [Mengenal Arsitektur Tiga Pilar](#-mengenal-arsitektur-tiga-pilar)
- [Naskah Orkestra Utama (docker-compose.yml)](#-naskah-orkestra-utama-docker-composeyml)
- [Membedah Anatomi Sang Mahakarya](#-membedah-anatomi-sang-mahakarya)
- [Tombol Peluncuran Roket](#-tombol-peluncuran-roket)
- [The "Wow" Factor: Keajaiban Ekosistem Utuh](#-the-wow-factor-keajaiban-ekosistem-utuh)
- [Epilog: Gelar Ksatria Docker Anda](#-epilog-gelar-ksatria-docker-anda)

---

## 🏛️ Mengenal Arsitektur Tiga Pilar

Di dunia kerja nyata, *developer* kelas dunia tidak pernah mengutak-atik *database* secara "buta" melalui baris perintah hitam putih jika tidak terpaksa. Mereka membangun antarmuka visual (GUI) elegan untuk mengelola data, sambil tetap menyalakan aplikasi utamanya secara simultan.

Ekosistem yang akan kita rilis hari ini terdiri dari 3 pilar masif:
1. **MySQL**: Sebagai Brankas Bawah Tanah (Server Database).
2. **WordPress**: Sebagai Etalase Toko (Web App) yang akan hidup mengambil data dari MySQL.
3. **phpMyAdmin**: Sebagai Ruang Kontrol (GUI) yang juga menempel ke MySQL untuk mengatur tabel dan data melalui layar peramban (*browser*).

Ketiga pilar raksasa ini akan diselimuti oleh satu **Network** raksasa untuk berkomunikasi, dan dilindungi oleh satu **Volume** permanen untuk ketahanan data.

---

## 📜 Naskah Orkestra Utama (docker-compose.yml)

Buat folder baru bernama `proyek-akhir-docker`, dan buat *file* `docker-compose.yml` murni di dalamnya. Tarik napas, dan tempelkan seluruh arsitektur *masterpiece* ini:

```yaml
version: '3.8'

services:
  # Pilar 1: Database (Sang Brankas Bawah Tanah)
  db:
    image: mysql:5.7
    container_name: proyek_db
    restart: always # Otomatis menyala sendiri jika laptop/server di-restart
    environment:
      MYSQL_ROOT_PASSWORD: password_rahasia
      MYSQL_DATABASE: wordpress_db
    volumes:
      - db_data:/var/lib/mysql

  # Pilar 2: Web CMS (Sang Etalase Toko)
  wordpress:
    image: wordpress:latest
    container_name: proyek_wordpress
    restart: always
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db:3306 # <--- Lihat kejeniusan ini!
      WORDPRESS_DB_USER: root
      WORDPRESS_DB_PASSWORD: password_rahasia
      WORDPRESS_DB_NAME: wordpress_db
    depends_on:
      - db

  # Pilar 3: Database GUI (Sang Ruang Kontrol)
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: proyek_phpmyadmin
    restart: always
    ports:
      - "8081:80"
    environment:
      PMA_HOST: db # <--- PHPMyAdmin juga bisa langsung melihat dan menyapa 'db'!
      PMA_PORT: 3306
    depends_on:
      - db

# Deklarasi Brankas Eksternal untuk Persistensi Data
volumes:
  db_data:
```

---

## 🔬 Membedah Anatomi Sang Mahakarya

Tatap tajam dan pandangi kode di atas. Jika Anda membaca dan meresapi seri tutorial ini dari Bab 1, Anda pasti bisa menerjemahkan kode di atas layaknya membaca novel favorit Anda.

1. **Keajaiban Network**: Pernahkah Anda menyadari bahwa kita sama sekali tidak mengetik blok `networks:` secara manual? *Docker Compose* sudah terlalu pintar. Ia secara magis menciptakan satu payung jaringan abstrak yang secara otomatis membungkus `db`, `wordpress`, dan `phpmyadmin` di dalamnya.
2. **Sihir DNS Resolution**: Bukti nyatanya terlihat jelas pada kode `WORDPRESS_DB_HOST: db` dan `PMA_HOST: db`. WordPress dan phpMyAdmin tidak perlu pusing melacak IP Address yang berubah-ubah. Mereka cukup memanggil nama panggilannya yakni `"db"`, dan jembatan tol Docker langsung menghubungkan mereka ke jantung MySQL.
3. **Perlindungan Volume**: Terdapat deklarasi `volumes: - db_data:/var/lib/mysql`. Kita dengan tegas memerintahkan mesin: *"Buatkan sebuah brankas baja bernama db_data, dan tancapkan langsung menembus ke dalam jantung urat nadi MySQL."*

---

## 🚀 Tombol Peluncuran Roket

Waktunya mengubah teks statis di atas menjadi sistem yang hidup dan berdenyut. Buka *Terminal* Anda di folder `proyek-akhir-docker`, dan tarik tuas peluncurannya:

```bash
docker-compose up -d
```

Layar Terminal Anda akan segera diwarnai oleh proses intens pengunduhan 3 Image raksasa, pembuatan Network abstrak, pembangunan brankas Volume, dan *booting* 3 Container yang direkayasa sedemikian presisi agar tertata berurutan.

Setelah semuanya hening, silakan lakukan inspeksi dengan radar Anda:
```bash
docker-compose ps
```

---

## 🎇 The "Wow" Factor: Keajaiban Ekosistem Utuh

Inilah puncak kepuasan dari seluruh hasil keringat Anda!

1. Buka browser dan meluncurlah ke **`http://localhost:8080`**.
   Seketika, Anda akan disambut oleh halaman instalasi cantik WordPress. Aplikasi Web Utama Anda telah bernapas!
   
2. Sekarang, buka tab *browser* kedua dan meluncurlah ke **`http://localhost:8081`**.
   **Boom!** Layar *login* biru khas **phpMyAdmin** langsung tersaji di depan mata. 
   - Masukkan *Username*: `root`
   - Masukkan *Password*: `password_rahasia`
   
   Klik *Log In*, dan seketika Anda berada di ruang kontrol seluruh arsitektur database Anda. Bahkan, di sebelah kiri, Anda bisa melihat basis data `wordpress_db` yang sedang diisi secara otomatis oleh WordPress!

> 💡 **PRO TIP PAMUNGKAS:**
> Ingin membuktikan ketahanan absolut dari *arsitektur* yang baru saja Anda bangun? 
> Kembali ke terminal dan ketik `docker-compose down` (Boom! Semua hancur lebur, website mati total). 
> Lalu dengan tenang ketik lagi `docker-compose up -d` (Seluruh ekosistem bangkit kembali dari debu).
> 
> Buka lagi WordPress atau phpMyAdmin Anda. Data pengaturan WordPress, artikel web Anda, dan database Anda **TIDAK AKAN HILANG ATAU TERGORES SATU HURUF PUN**. Itulah kekuatan arsitektur infrastruktur abadi sekelas *Senior DevOps*!

---

## 🤯 Keajaiban Pamungkas: Portabilitas Tanpa Drama

Pernahkah Anda mencoba memindahkan proyek *XAMPP* atau *Laragon* dari laptop Anda ke laptop rekan kerja, atau dari OS Windows ke Mac? Anda pasti ingat betapa horornya drama *error* versi PHP yang berbeda, *database* yang rusak saat di-*export/import*, hingga konfigurasi *Apache/Nginx* yang berbenturan dengan *port* aplikasi lain.

Di sinilah letak keunggulan absolut dari Docker:
Cukup *copy* folder `proyek-akhir-docker` milik Anda (yang hanya berisi satu *file* teks kecil `docker-compose.yml`) dan kirimkan ke laptop teman Anda lewat Flashdisk, Email, atau bahkan WhatsApp. 

Minta teman Anda membuka *Terminal* di folder tersebut dan mengetik satu baris mantra yang sama: `docker-compose up -d`.

**BOOM!** 
Seluruh ekosistem raksasa tersebut (MySQL, WordPress, phpMyAdmin) akan langsung *booting* dan menyala dengan versi, spesifikasi, dan lingkungan OS yang **100% SAMA PERSIS** seperti di laptop Anda. Tanpa drama, tanpa *error*, dan tanpa perlu repot mencocokkan *installer* XAMPP. 

Inilah wujud kebebasan sejati dan titik tamat dari kalimat kutukan klasik para programmer: *"Lho aneh, padahal aplikasinya jalan lancar di laptop saya!"*.

---

## 🏆 Epilog: Gelar Ksatria Docker Anda

**Hormat saya untuk Anda, Kapten.** 

Dengan ditutupnya halaman ini, **Seri Tutorial Masterclass Docker** telah resmi usai. Anda telah memenangkan perjalanan epik panjang dari sekadar seorang turis yang meraba-raba "apa itu Container", berevolusi menjadi arsitek infrastruktur yang mumpuni membangun sistem skala menengah yang stabil, terisolasi, portabel, dan anti-hilang data.

Bawalah pedoman ilmu "Kitab Suci" ini ke proyek bisnis Anda, sematkan keahlian luar biasa ini ke dalam lembar CV Anda, dan bangunlah infrastruktur impian yang tak pernah goyah oleh badai. 

Sampai jumpa kembali di petualangan merangkai kode di samudera teknologi lainnya! 🚢⚓
