![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 5 Mins](https://img.shields.io/badge/Durasi-5_Menit-blue?style=for-the-badge)
![Killer Feature](https://img.shields.io/badge/Fokus-Presentasi_Klien-purple?style=for-the-badge)

# 🌐 Jembatan Telepati: Presentasi Web ke Klien dengan Live Links

Mari kita gambarkan sebuah penderitaan yang sangat umum di dunia *Freelancer* dan Agensi Web.

Anda baru saja menyelesaikan mendesain halaman Beranda (*Homepage*) klien Anda yang spektakuler. Anda ingin segera meminta persetujuan revisi dari Klien. 
Namun, *website* tersebut masih bersarang dengan nyaman di dalam laptop Anda (`namaklien.local`). 

Apa yang harus Anda lakukan di era XAMPP?
Anda terpaksa membeli domain, menyewa *hosting staging*, mem-*backup database*, mengunggah *file* Zip bergiga-giga, me-*restore database*, lalu berdoa tidak ada *error URL mismatch*. Pekerjaan 1 jam hanya untuk menunjukkan *progress* 5 menit.

Di bab ini, aplikasi **Local** akan menganugerahkan Anda sebuah **Jembatan Telepati** yang memangkas waktu 1 jam tersebut menjadi **1 detik**.

## 📋 Daftar Isi
- [Mengenal Keajaiban Live Links](#-mengenal-keajaiban-live-links)
- [Praktik: Membuka Gerbang Antar Benua](#-praktik-membuka-gerbang-antar-benua)
- [Sistem Keamanan Bawaan (Username & Password)](#-sistem-keamanan-bawaan)
- [Peringatan Penting Penutup Sesi](#-pro-tip-peringatan-penting-penutup-sesi)

---

## ✨ Mengenal Keajaiban Live Links

Jika Anda telah membaca seri tutorial Laragon kami, Anda pasti mengenal integrasi Ngrok. Fitur **Live Links** pada aplikasi Local memiliki fondasi konsep yang sama (membuka terowongan dari internet ke laptop Anda), namun dieksekusi dengan keanggunan dan antarmuka (*UI*) kelas dewa yang tak tertandingi.

Tidak ada terminal hitam yang menakutkan. Tidak ada baris perintah (CLI) untuk memasukkan *authtoken*. WP Engine telah menanamkan infrastruktur raksasa ini ke dalam satu tombol elegan di dasar aplikasi Local Anda.

---

## 🚀 Praktik: Membuka Gerbang Antar Benua

Mari kita buktikan seberapa cepat Anda bisa memukau Klien Anda:

1. Buka aplikasi Local, dan pastikan *website* WordPress klien Anda sedang menyala (*Started*).
2. Perhatikan area paling bawah di jendela aplikasi Local. Di samping nama *website* Anda, terdapat fitur **Live Links**.
3. Klik tombol **"Enable"** (Nyalakan) di sebelahnya.
   > *(Catatan: Jika ini pertama kalinya, Local mungkin akan meminta Anda untuk Log In menggunakan akun gratis Localwp.com Anda. Lakukan saja, itu 100% gratis dan super cepat).*
4. Setelah aktif, tombol akan berubah menjadi hijau dan Anda akan melihat tautan rahasia (misalnya: `https://kucing-terbang-1234.loca.lt`).
5. Klik tautan tersebut untuk menyalinnya (*Copy*).
6. Buka WhatsApp atau Email, dan kirimkan tautan tersebut ke Klien Anda.

**BOOM! 🤯**
Saat klien mengklik tautan tersebut dari *smartphone* atau iPad mereka di kantornya, mereka akan melihat *website* yang secara fisik berada di dalam kamar tidur Anda! 

Mereka bisa melakukan *scroll*, menekan tombol, dan berselancar secara *real-time*. Jika mereka meminta Anda mengubah warna tombol saat itu juga via telepon, Anda cukup menekan `CTRL+S` di laptop, klien cukup menekan *Refresh* di *browser* mereka, dan warnanya berubah seketika di depan mata klien!

*(Ini adalah tingkat profesionalisme yang akan membuat harga jasa pembuatan web Anda layak dibayar tiga kali lipat).*

---

## 🔒 Sistem Keamanan Bawaan 

Pernahkah Anda khawatir jika tautan `loca.lt` Anda tersebar secara tidak sengaja ke publik, padahal *website* klien belum selesai dikerjakan?

Local memikirkan hal ini dengan sangat brilian. Saat Anda menyalakan **Live Links**, Local secara otomatis mengaktifkan fitur perlindungan kata sandi (*Basic Auth*). 

Jika Anda melihat ke kolom sebelah tombol *Live Links*, Anda akan menemukan **Username** dan **Password** yang dihasilkan secara acak (contoh User: `local`, Password: `abc123`). 

Jadi, pastikan saat Anda memberikan tautan kepada klien, Anda juga memberikan *Username* dan *Password* kecil tersebut agar klien bisa menembus gerbang keamanan. Ini memastikan privasi proyek Anda terjaga 100%.

---

## 🛑 PRO TIP: Peringatan Penting Penutup Sesi

> [!WARNING]
> Klien Anda pada dasarnya sedang menumpang *"Browsing"* melalui mesin dan koneksi internet laptop Anda. 
> 
> Jika Anda menutup layar laptop (masuk mode *Sleep*), koneksi WiFi Anda putus, atau Anda menekan tombol **"Disable"** pada Live Links, maka tautan tersebut akan **mati seketika** (menampilkan *error Offline* di HP klien).
> 
> Karena itu, gunakan fitur ini HANYA untuk sesi *meeting/presentasi live* atau pengecekan *progress* sesaat. Jangan menjadikannya sebagai *hosting* abadi untuk diakses Klien keesokan harinya!

Di bab selanjutnya, kita akan membongkar pilar kedua keprofesionalan: **Menguji Fitur Pengiriman Email**. Ucapkan selamat datang kepada pahlawan baru kita: *Mailpit*! 📬🔥
