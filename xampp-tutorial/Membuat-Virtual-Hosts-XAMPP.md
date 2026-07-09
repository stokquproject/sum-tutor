![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 20 Mins](https://img.shields.io/badge/Durasi-20_Menit-blue?style=for-the-badge)
![Advanced Config](https://img.shields.io/badge/Fokus-Konfigurasi_Sistem-purple?style=for-the-badge)

# 🚧 Arsitektur Jalan Raya: Membangun Virtual Hosts Manual

Selamat datang di Level 2, Sang Mekanik! 🛠️

Di level pertama, Anda telah belajar bahwa semua *website* harus diletakkan di dalam `htdocs` dan diakses menggunakan `http://localhost/namaproyek`. 

Untuk proyek sederhana, ini tidak masalah. Namun, bayangkan Anda sedang membangun aplikasi **Laravel** yang mewah, di mana titik masuk utamanya (*entry point*) berada di dalam folder `public`. 
Tiba-tiba, URL *website* Anda berubah menjadi pemandangan yang sangat jelek:
👉 `http://localhost/aplikasi-kasir/public`

URL yang panjang dan menukik seperti ini bukan hanya merusak pemandangan, tapi sering kali merusak rute gambar (*broken image paths*) saat *website* dinaikkan ke internet sesungguhnya. 

Sebagai *developer* profesional, Anda menginginkan nama *domain* lokal yang elegan, bersih, dan berkelas, seperti:
👉 **`http://kasir.local`**

Di bab ini, kita akan melatih kemampuan Anda sebagai Mekanik dengan melakukan modifikasi sistem operasi (*Windows*) dan jantung Apache sekaligus untuk menciptakan arsitektur jalan raya tersebut yang dikenal sebagai **Virtual Host**.

## 📋 Daftar Isi
- [Tahap 1: Membajak Peta Navigasi Windows](#-tahap-1-membajak-peta-navigasi-windows)
- [Tahap 2: Menyetor Peta ke Resepsionis (Apache)](#-tahap-2-menyetor-peta-ke-resepsionis-apache)
- [Tahap 3: Uji Coba Jalan Raya Baru](#-tahap-3-uji-coba-jalan-raya-baru)
- [Refleksi: Mengapa Laragon Lebih Superior](#-refleksi-mengapa-laragon-lebih-superior)

---

## 🗺️ Tahap 1: Membajak Peta Navigasi Windows

Agar Anda bisa mengetik `kasir.local` dan tidak diarahkan ke pencarian Google, kita harus menipu sistem operasi Windows agar percaya bahwa *domain* tersebut ada di dalam laptop Anda sendiri.

1. Buka *Start Menu* Windows Anda, ketik **Notepad**.
2. **JANGAN** langsung diklik! *Klik Kanan* pada Notepad, lalu pilih **Run as Administrator** (Sangat Penting, tanpa ini Anda tidak akan bisa menyimpan *file*!).
3. Di Notepad, klik *File* > *Open*.
4. Navigasikan ke lorong terdalam Windows: `C:\Windows\System32\drivers\etc`
5. Di pojok kanan bawah jendela (di atas tombol *Open*), ubah *"Text Documents (*.txt)"* menjadi **"All Files (*.*)"**.
6. Anda akan melihat sebuah *file* tanpa ekstensi bernama **`hosts`**. Buka *file* tersebut.
7. Gulir ke baris paling bawah, tekan *Enter* untuk membuat baris baru, dan ketik mantra pembajak ini:

```text
127.0.0.1       kasir.local
```
*(Artinya: Hai Windows, jika ada orang yang mencari kasir.local, jangan cari ke internet, tapi arahkan ke 127.0.0.1 alias laptop ini sendiri).*

8. Tekan `CTRL + S` untuk menyimpan.

---

## 🚦 Tahap 2: Menyetor Peta ke Resepsionis (Apache)

Sekarang Windows sudah tahu jalannya, tugas berikutnya adalah memberitahu Apache (Sang Resepsionis XAMPP) ke laci mana ia harus mencarikan *file* saat ada pengunjung masuk ke `kasir.local`.

1. Buka *File Explorer*, pergi ke `C:\xampp\apache\conf\extra`.
2. Cari *file* bernama **`httpd-vhosts.conf`**, klik kanan, dan *Open with Notepad* (Teks Editor).
3. Gulir ke baris paling bawah.
4. Anda harus menulis deklarasi *Virtual Host*. Agar mudah, salin dan tempel struktur di bawah ini:

```apache
<VirtualHost *:80>
    DocumentRoot "C:/xampp/htdocs/aplikasi-kasir/public"
    ServerName kasir.local
</VirtualHost>
```

> [!WARNING]
> **Perhatikan Tanda Slash (/)**
> Berbeda dengan format Windows standar yang menggunakan *Backslash* (`\`), di dalam dunia Apache Anda **WAJIB** menggunakan *Slash* biasa (`/`) untuk menulis alamat *DocumentRoot*, atau Apache Anda akan meledak dan mati (merah) saat dinyalakan.

5. Tekan `CTRL + S` untuk menyimpan *file* `httpd-vhosts.conf`.

---

## 🏎️ Tahap 3: Uji Coba Jalan Raya Baru

Modifikasi mesin telah selesai, saatnya melakukan penyalaan awal (*Ignition*).

1. Buka aplikasi **XAMPP Control Panel**.
2. Anda **WAJIB** mematikan (*Stop*) modul Apache, dan menyalakannya (*Start*) kembali. Ini dilakukan agar Apache membaca *file* konfigurasi yang baru saja Anda tulis.
3. Buka peramban (*Chrome/Firefox*).
4. Di kolom pencarian atas (URL), ketik: **`http://kasir.local`**

**BOM! 🤯**
Anda tidak lagi melihat alamat kotor `localhost/aplikasi-kasir/public`. Anda baru saja mendarat di alamat situs web *Custom Domain* buatan Anda sendiri layaknya sebuah *website* seharga jutaan Rupiah di internet!

---

## 🧘‍♂️ Refleksi: Mengapa Laragon Lebih Superior

Berhentilah sejenak, dan renungkan apa yang baru saja Anda lalui.
Untuk mendapatkan *satu* domain lokal (`.local`), Anda harus:
- Melawan *Administrator Rights* Windows.
- Mengedit *file* OS inti yang berbahaya jika salah ketik.
- Menulis blok kode konfigurasi Apache secara manual yang rentan *error (typo)*.
- Melakukan *Restart* Apache secara manual setiap saat.

Jika Anda memiliki 20 proyek klien bulan ini, Anda harus melakukan penyiksaan 4 langkah ini sebanyak 20 kali!

**Inilah alasan mengapa Anda wajib membaca Seri Tutorial Laragon kami sebelumnya.**
Di Laragon, seluruh bab ini diringkas menjadi **NOL LANGKAH**. 
Saat Anda membuat folder baru bernama `aplikasi-kasir`, Laragon akan menciptakan *domain* `http://aplikasi-kasir.test`, mengedit *hosts* Windows, menulis *vhosts.conf*, dan me-*restart* Apache **secara otomatis di latar belakang dalam waktu 0,5 detik** tanpa Anda sadari.

Itulah perbedaan antara seorang Mekanik Tradisional dengan seorang Arsitek Modern!

*(Meski begitu, kemampuan manual ini sangat krusial jika suatu saat Anda terjebak mengelola server kuno tanpa Panel otomatis). Di bab selanjutnya, kita akan melatih insting Ksatria Penjaga Gerbang: **Cara mengamankan phpMyAdmin dan MySQL XAMPP dari peretas lokal**.* 🛡️⚔️
