![Difficulty: Expert](https://img.shields.io/badge/Tingkat-Pakar-red?style=for-the-badge)
![Time: 15 Mins](https://img.shields.io/badge/Durasi-15_Menit-blue?style=for-the-badge)
![Disaster Recovery](https://img.shields.io/badge/Fokus-Penyelamatan_Data-purple?style=for-the-badge)

# 🚑 Misi Pertolongan Pertama: Mengatasi MySQL InnoDB Crash

Ini adalah momen paling mematikan bagi seorang pengguna XAMPP.

Anda menyalakan laptop di pagi hari, membuka XAMPP Control Panel, menekan tombol **Start** pada MySQL, dan seketika jantung Anda berhenti berdetak saat melihat teks neraka berwarna merah ini:

> *"Error: MySQL shutdown unexpectedly. This may be due to a blocked port, missing dependencies, improper privileges, a crash, or a shutdown by another method."*

Anda mencoba menekan *Start* berkali-kali, namun MySQL terus menolak untuk menyala. Di dalam sana, terdapat *database* skripsi Anda atau proyek klien bernilai jutaan Rupiah yang belum sempat Anda *backup*.

Tenang, bernapaslah. Anda sedang mengalami apa yang disebut **InnoDB Crash / Data Corruption**. Di bab ini, kenakan sarung tangan bedah Anda. Kita akan menyelamatkan pasien kritis ini tanpa kehilangan satu pun tetes data berharga Anda.

## 📋 Daftar Isi
- [Mendiagnosis Penyebab Kematian](#-mendiagnosis-penyebab-kematian)
- [Tahap 1: Karantina dan Pencadangan](#-tahap-1-karantina-dan-pencadangan)
- [Tahap 2: Transfusi Darah (Pemulihan)](#-tahap-2-transfusi-darah-pemulihan)
- [Peringatan Keras Pemeliharaan](#-pro-tip-peringatan-keras-pemeliharaan)

---

## 🩺 Mendiagnosis Penyebab Kematian

Mengapa MySQL tiba-tiba meledak?
XAMPP menggunakan *storage engine* bernama **InnoDB** untuk menyimpan tabel *database* Anda. InnoDB sangat rentan terhadap gangguan listrik mendadak. 

Jika Anda mematikan paksa (*Force Shutdown*) laptop Anda saat MySQL sedang menulis data, atau laptop Anda kehabisan baterai secara mendadak, struktur *file* log InnoDB akan patah (korup). MySQL akan menolak menyala sebagai sistem pertahanan diri agar kerusakan tidak menyebar.

Mari kita obati.

---

## 🧫 Tahap 1: Karantina dan Pencadangan

Aturan pertama dalam operasi bedah adalah: **Jangan memperburuk keadaan.** Kita harus mengamankan sisa-sisa *file* yang masih ada.

1. Buka **XAMPP Control Panel**, pastikan semuanya dalam keadaan **Stop** dan tutup (Exit) aplikasinya dari *System Tray* di pojok kanan bawah Windows Anda.
2. Buka *File Explorer*, navigasikan ke jantung XAMPP: **`C:\xampp\mysql`**.
3. Di dalam sana, Anda akan melihat folder bernama **`data`**. Ini adalah ruang gawat daruratnya. Folder ini berisi seluruh *database* Anda yang rusak.
4. **Klik Kanan** pada folder `data` tersebut, lalu ganti namanya (*Rename*) menjadi **`data_rusak`**.
5. Buat sebuah folder baru yang benar-benar kosong, dan beri nama **`data`**.

Kini, kita memiliki satu pasien di ruang karantina (`data_rusak`) dan satu ruang operasi yang steril (`data`).

---

## 💉 Tahap 2: Transfusi Darah (Pemulihan)

XAMPP sangat cerdas. Di dalam `C:\xampp\mysql`, mereka menyimpan sebuah cadangan (*backup*) murni yang berisi struktur dasar MySQL kosongan, terletak di dalam folder bernama **`backup`**. Kita akan menggunakan ini untuk membangun ulang MySQL.

**Langkah Bedah 1: Menginjeksi Sistem Inti**
1. Masuk ke folder **`C:\xampp\mysql\backup`**.
2. *Copy* (Salin) **seluruh isi** folder tersebut (pilih semua file dan folder).
3. Kembali, dan *Paste* (Tempel) di dalam folder **`data`** yang baru dan kosong tadi.

**Langkah Bedah 2: Mengambil Harta Karun Anda**
1. Sekarang, masuk ke folder karantina **`C:\xampp\mysql\data_rusak`**.
2. Di sini, Anda akan melihat banyak folder. Setiap folder mewakili satu *database* yang Anda buat (Misalnya: `db_skripsi`, `db_tokoonline`).
3. *Copy* (Salin) **HANYA** folder-folder *database* milik Anda sendiri.
4. **HARAM HUKUMNYA (DILARANG KERAS)** untuk men- *copy* folder bernama `mysql`, `performance_schema`, atau `phpmyadmin` dari sini.
5. *Paste* (Tempel) folder-folder *database* Anda tersebut ke dalam folder **`data`** yang baru. *(Jika ditanya untuk menimpa/overwrite, pilih Yes).*

**Langkah Bedah 3: Transplantasi Tulang Belakang (ibdata1)**
Langkah ini adalah kunci dari seluruh operasi ini. Folder yang Anda pindahkan tadi hanyalah cangkang. Seluruh isinya (tabel dan relasi) tersimpan di satu urat nadi bernama `ibdata1`.

1. Masuk kembali ke folder karantina **`C:\xampp\mysql\data_rusak`**.
2. Gulir ke bawah, cari *file* berukuran besar yang bernama persis **`ibdata1`**.
3. *Copy* *file* tersebut.
4. Masuk ke folder **`data`** yang baru, lalu *Paste* (Tempel). 
5. Windows akan bertanya apakah Anda ingin menimpa (*Replace the file in the destination*). Klik **YES / Replace**.

---

## 🏁 Menjahit Pasien & Kebangkitan

Operasi bedah besar telah selesai. Bersihkan keringat Anda.

1. Buka kembali **XAMPP Control Panel** Anda.
2. Tarik napas dalam-dalam.
3. Klik tombol **Start** pada modul MySQL.

**BOM! 🤯**
Latar belakang MySQL berubah menjadi hijau terang! Port 3306 kembali berdetak! 

Buka `http://localhost/phpmyadmin`, dan Anda akan melihat seluruh *database* Anda (`db_skripsi`, `db_tokoonline`) kembali duduk manis di tempatnya tanpa kehilangan satu pun *row* data. Anda baru saja menyelamatkan nyawa proyek Anda.

> [!CAUTION]
> **PRO TIP: Peringatan Keras Pemeliharaan**
> Meskipun Anda berhasil membangkitkan data dari kematian hari ini, jangan pernah mengandalkan folder *Copy-Paste* MySQL sebagai *backup* permanen Anda. 
> 
> Selalu gunakan fitur **Export (Ekspor)** di dalam phpMyAdmin secara berkala untuk mencetak *database* Anda menjadi *file* murni `.sql` (Teks). Sebuah *file* `.sql` 100% mustahil mengalami kerusakan *InnoDB Crash* dan bisa dipulihkan ke *server* mana pun di dunia.

Di bab terakhir (Penutup), kita akan mengeksplorasi kemampuan paling memukau dari XAMPP: **Cara menembus localhost dan memamerkan website Anda ke ponsel pintar (Smartphone) klien melalui jaringan WiFi lokal (LAN)**. Siapkan ponsel Anda! 📱📶
