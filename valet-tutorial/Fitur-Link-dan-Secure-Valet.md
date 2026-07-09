![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 10 Mins](https://img.shields.io/badge/Durasi-10_Menit-blue?style=for-the-badge)
![Security & Routing](https://img.shields.io/badge/Fokus-Keamanan_dan_Routing-purple?style=for-the-badge)

# 🔒 Mengikat Bayangan: Trik valet link & valet secure

Kemampuan *Lahan Parkir* (valet park) di bab sebelumnya memang luar biasa, tetapi ada dua skenario umum di mana jurus tersebut tidak cukup.

**Skenario Pertama:** Bagaimana jika Anda tiba-tiba mengunduh sebuah *template website* dan menaruhnya di *Desktop*, dan Anda ingin segera melihatnya tanpa harus repot memindahkannya ke dalam lahan parkir `~/Sites`?

**Skenario Kedua (Lebih Krusial):** Anda sedang membangun aplikasi yang terintegrasi dengan *Payment Gateway* (seperti Midtrans atau Stripe) atau *WebRTC* (akses kamera). Fitur-fitur modern ini **WAJIB** meminta koneksi aman bersertifikat **HTTPS** (Gembok Hijau), meskipun Anda masih mengujinya di laptop lokal Anda!

Membuat sertifikat *SSL Self-Signed* lokal secara manual di Windows atau Mac adalah penderitaan yang luar biasa memusingkan. Di sinilah sang Ninja Valet kembali mengeluarkan dua mantra legendanya: **Jurus Tali Pengikat (Link)** dan **Jurus Perisai Cahaya (Secure)**.

## 📋 Daftar Isi
- [Jurus Tali Pengikat (valet link)](#-jurus-tali-pengikat-valet-link)
- [Praktik: Mengikat Folder Acak](#-praktik-mengikat-folder-acak)
- [Jurus Perisai Cahaya (valet secure)](#-jurus-perisai-cahaya-valet-secure)
- [Praktik: Menempa Gembok Hijau (HTTPS)](#-praktik-menempa-gembok-hijau-https)

---

## 🪢 Jurus Tali Pengikat (valet link)

Jika `valet park` bertindak sebagai "Pabrik", maka `valet link` bertindak sebagai **"Jangkar Tunggal"**.

Perintah ini akan memberitahu Valet: *"Hai Valet, abaikan di mana letak folder ini, tolong buatkan domain khusus (Symbolic Link) yang mengarah langsung ke folder ini."*

Perintah ini sangat cocok untuk folder *website* tunggal yang letaknya acak atau berserakan (di *Desktop*, di *Downloads*, atau di *Documents*).

---

## 🎯 Praktik: Mengikat Folder Acak

Mari kita uji coba mengikat sebuah bayangan.

1. Buka Terminal Anda, mari kita buat sebuah folder acak di *Desktop* Anda:
   ```bash
   mkdir ~/Desktop/proyek-rahasia
   cd ~/Desktop/proyek-rahasia
   ```
2. Buat satu *file* pancingan agar kita bisa melihat hasilnya:
   ```bash
   echo "<h1>Ini adalah Proyek Rahasia di Desktop</h1>" > index.php
   ```
3. Rapalkan mantra pengikat ini di dalam folder tersebut:
   ```bash
   valet link rahasia
   ```
   *(Kata `rahasia` di atas adalah nama custom domain yang Anda inginkan).*

4. Valet akan membalas dengan pesan *A symbolic link has been created*. 
5. Buka peramban Anda, dan akses: **`http://rahasia.test`**

**BOM! 🤯**
Valet berhasil menayangkan *website* Anda meskipun lokasinya terisolasi di *Desktop*. 

**Lalu, bagaimana cara melepaskannya?**
Jika proyek tersebut sudah selesai dan Anda ingin mencabut akses *domainnya*, cukup rapalkan mantra pemutus:
```bash
valet unlink rahasia
```

---

## 🛡️ Jurus Perisai Cahaya (valet secure)

Sekarang kita masuk ke fitur yang membuat *developer* lain iri kepada pengguna Mac.

Menciptakan koneksi `https://` yang tepercaya secara lokal (*trusted localhost SSL*) membutuhkan waktu berjam-jam untuk mengatur *OpenSSL*, menyuntikkan *Root Certificate* ke dalam *Keychain* Mac, dan mengonfigurasi `nginx.conf` secara manual.

Valet mengotomatiskan seluruh penyiksaan ini menjadi **1 baris perintah**.

---

## 🔐 Praktik: Menempa Gembok Hijau (HTTPS)

Mari kita ubah `http://rahasia.test` tadi menjadi terenkripsi tingkat militer.

1. Buka Terminal, pastikan Anda sedang berada di dalam folder yang memiliki *domain* Valet (entah itu yang di- *park* atau di- *link*). Dalam kasus kita:
   ```bash
   cd ~/Desktop/proyek-rahasia
   ```
2. Rapalkan mantra suci ini dan bersiaplah takjub:
   ```bash
   valet secure rahasia
   ```
   *(Sama seperti sebelumnya, gunakan nama domain target Anda).*

3. Terminal Anda akan berkedip. Valet secara otomatis (di latar belakang) men- *generate* sertifikat SSL palsu namun valid, menyuntikkannya ke *Keychain Access* Mac Anda (Anda mungkin akan diminta memasukkan *password* Mac atau *Touch ID*), dan me- *restart* Nginx. 

4. Buka peramban Anda, dan ketik: **`https://rahasia.test`** (Jangan lupa huruf **S** di HTTPS).

**Ajaib! 🤯**
Peramban Google Chrome atau Safari Anda tidak akan memunculkan layar merah *"Your connection is not private"*. Anda akan melihat sebuah **Gembok Abu/Hijau yang tertutup rapat** di sebelah URL Anda. Peramban Anda percaya 100% bahwa koneksi lokal tersebut telah terenkripsi!

Kini Anda bisa menguji coba *Payment Gateway* dan API modern tanpa hambatan!

**Bagaimana cara menurunkannya kembali ke HTTP biasa?**
Jika Anda tidak lagi membutuhkan SSL dan ingin performa yang sedikit lebih cepat tanpa enkripsi, rapalkan mantra ini:
```bash
valet unsecure rahasia
```

Gembok akan dihancurkan, dan Anda kembali ke jalur biasa. 

Di level selanjutnya (Level 3), kita akan menembus batas jaringan lokal dan memamerkan *website* Valet Anda ke dunia maya atau ke jaringan HP menggunakan mantra rahasia: **valet share**. Bersiaplah menembus dimensi! 🌐🚀
