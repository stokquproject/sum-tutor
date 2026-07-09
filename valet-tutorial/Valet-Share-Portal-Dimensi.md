![Difficulty: Advanced](https://img.shields.io/badge/Tingkat-Mahir-red?style=for-the-badge)
![Time: 10 Mins](https://img.shields.io/badge/Durasi-10_Menit-blue?style=for-the-badge)
![Network Expose](https://img.shields.io/badge/Fokus-Eksposur_Jaringan-purple?style=for-the-badge)

# 🌐 Membuka Portal Dimensi: Memamerkan Web dengan valet share

Sebagai seorang Grandmaster, kelincahan bukan hanya diukur dari seberapa cepat Anda mengoding, tetapi seberapa cepat Anda bisa mendapatkan persetujuan (*approval*) dari klien.

Bayangkan klien Anda yang berada di kota (atau benua) lain meminta *update* desain. Alih-alih melakukan *commit*, me-*push* ke GitHub, dan men- *deploy* kode ke *server Staging* yang memakan waktu 10 menit, sang Ninja memiliki cara yang jauh lebih mematikan.

Kita akan membuka sebuah Portal Dimensi. Kita akan mengekspos *website* yang berjalan di laptop Anda langsung ke internet publik dalam waktu 2 detik!

## 📋 Daftar Isi
- [Kemitraan dengan Sang Terowongan (Ngrok)](#-kemitraan-dengan-sang-terowongan-ngrok)
- [Tahap 1: Membuka Portal Dimensi](#-tahap-1-membuka-portal-dimensi)
- [Tahap 2: Menembus Batas Benua (Region)](#-tahap-2-menembus-batas-benua-region)
- [Tahap 3: Memasang Gembok Dimensi (Autentikasi)](#-tahap-3-memasang-gembok-dimensi-autentikasi)

---

## 🚇 Kemitraan dengan Sang Terowongan (Ngrok)

Bagaimana mungkin laptop lokal kita yang terhalang *Router* dan *Firewall* bisa diakses oleh orang dari luar? 

Di balik layar, Valet menjalin kemitraan erat dengan **Ngrok**—sebuah layanan *tunneling* paling populer di dunia. Ngrok bertugas mengebor sebuah terowongan aman (*secure tunnel*) dari *server* pusat mereka langsung menembus masuk ke dalam port lokal Mac Anda. 

Hebatnya, Valet telah menanamkan Ngrok ini ke dalam aliran darahnya, sehingga Anda tidak perlu menginstal Ngrok secara terpisah apalagi mengonfigurasinya.

---

## 🕳️ Tahap 1: Membuka Portal Dimensi

Mari kita ciptakan tautan sakti (*magic link*) untuk klien Anda.

1. Buka Terminal, dan masuklah ke dalam folder proyek Anda (Misal: proyek yang berada di lahan parkir Anda).
   ```bash
   cd ~/Sites/portal-berita
   ```
2. Rapalkan satu mantra pembuka portal ini:
   ```bash
   valet share
   ```
3. Terminal Anda akan berubah wajah menjadi *dashboard* hitam milik Ngrok. 
4. Cari baris yang bertuliskan **Forwarding**. Anda akan melihat sebuah URL acak, misalnya: 
   `https://a1b2c3d4.ngrok-free.app -> http://portal-berita.test`
5. Salin URL `https://a1b2c3d4.ngrok-free.app` tersebut dan kirimkan ke WhatsApp klien Anda.

Saat klien Anda mengklik *link* tersebut di HP atau laptop mereka, mereka secara harfiah sedang mengakses *file* Nginx langsung dari dalam *Hardisk* Mac Anda. Jika Anda mengubah teks di laptop Anda dan menekan *Save*, klien Anda cukup me-*refresh* *browser* mereka dan perubahannya akan langsung terlihat secara *real-time*!

*(Untuk menutup portal dan memutuskan koneksi klien, cukup tekan `CTRL + C` di layar Terminal Anda).*

---

## 🌏 Tahap 2: Menembus Batas Benua (Region)

Satu masalah yang sering dialami adalah koneksi terasa *lambat*. 
Ini terjadi karena secara bawaan (*default*), Ngrok akan mengebor terowongan ke *server* pusatnya yang ada di **Amerika Serikat (US)**. Jika Anda dan klien Anda berada di Indonesia, data harus terbang ke Amerika lalu kembali lagi ke Asia.

Sebagai Grandmaster, Anda bisa memerintahkan Valet untuk membelokkan terowongan tersebut ke benua yang lebih dekat, misalnya **Asia Pasifik (ap)**.

Alih-alih menggunakan `valet share` biasa, sisipkan parameter *region* ke dalamnya:
```bash
valet share --region=ap
```

Kini portal Anda diteruskan melalui *server* Singapura/Jepang, sehingga klien Anda akan merasakan kecepatan *loading website* layaknya mengakses *server* lokal yang sangat kencang.

---

## 🔐 Tahap 3: Memasang Gembok Dimensi (Autentikasi)

Mengirim URL publik tentu memiliki risiko keamanan. Bagaimana jika kompetitor atau *hacker* iseng menemukan *link* acak tersebut? 
Jika Anda sudah mendaftarkan akun di Ngrok dan memasukkan *Authtoken* Anda ke dalam sistem Mac, Anda bisa menambahkan fitur perisai yang luar biasa.

Anda bisa mengunci portal Anda dengan nama pengguna (*username*) dan kata sandi (*password*) dasar (*Basic Auth*). 
Perintahkan Valet untuk meneruskan perintah ini ke Ngrok:

```bash
valet share --basic-auth="client:rahasia123"
```

**BOM! 🤯**
Kini, saat klien (atau siapa pun) membuka *link* Ngrok tersebut, peramban akan memunculkan sebuah jendela abu-abu kaku (*Browser Prompt*) yang memaksa mereka untuk memasukkan *Username* (`client`) dan *Password* (`rahasia123`) sebelum mereka bisa melihat sekilas pun isi *website* Anda.

Pekerjaan terlindungi, klien puas, dan reputasi Ninja Anda semakin melegenda! 

Di bab penutup Masterclass ini, kita akan mempelajari jurus terlarang yang paling elit: **Sang Pandai Besi (Custom Valet Driver)**. Bagaimana cara mengajari Valet untuk menyajikan kerangka kerja (*framework*) buatan Anda sendiri? Siapkan diri Anda! 🛠️🔥
