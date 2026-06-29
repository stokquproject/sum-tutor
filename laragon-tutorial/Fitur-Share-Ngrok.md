![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 10 Mins](https://img.shields.io/badge/Durasi-10_Menit-blue?style=for-the-badge)
![Killer Feature](https://img.shields.io/badge/Fitur-Ngrok_Share-critical?style=for-the-badge)

# 🌍 Berbagi Web Lokal ke Seluruh Dunia dengan Satu Klik (Ngrok)

Bayangkan skenario ini: Anda baru saja menyelesaikan desain *website* memukau di laptop Anda. Sang Klien menelepon dan berkata, *"Bisa saya lihat progressnya sekarang?"*

Jantung Anda berdegup. *Website* itu masih berada di dalam `http://proyek-klien.test`. Tentu saja klien tidak bisa membuka alamat tersebut dari ponsel mereka, karena itu adalah domain lokal (hanya hidup di laptop Anda). 

Apakah Anda harus menyewa *hosting* dan mengunggah *file* Anda secara manual hanya untuk memamerkan progress? **TIDAK.**

Di bab ini, Laragon akan memamerkan otot aslinya dengan fitur berbagi (*Share*) terintegrasi yang akan membuat Klien Anda takjub.

## 📋 Daftar Isi
- [Dilema Isolasi Lokal](#-dilema-isolasi-lokal)
- [Sang Penyelamat Bernama Ngrok](#-sang-penyelamat-bernama-ngrok)
- [Praktik: Sihir "Satu Klik" Laragon](#-praktik-sihir-satu-klik-laragon)
- [Klinik Darurat: Otentikasi Ngrok](#-klinik-darurat-mengatasi-error-otentikasi)

---

## 🔒 Dilema Isolasi Lokal

Sejak zaman batu, kelemahan terbesar *Localhost* adalah sifatnya yang terisolasi. Jaringan internet luar tidak bisa menembus masuk ke dalam laptop Anda karena dilindungi oleh *router* dan *firewall*.

Dulu, untuk menembus tembok ini, seorang *programmer* harus memahami ilmu *Port Forwarding*, masuk ke halaman pengaturan *Router Indihome/Biznet* yang rumit, dan mempertaruhkan keamanan jaringan rumah mereka. Sebuah proses yang sangat menyiksa.

---

## 🚇 Sang Penyelamat Bernama Ngrok

Kemudian datanglah **Ngrok**. Ia adalah sebuah teknologi *tunneling* (pembuat terowongan). 

Secara sederhana, Ngrok akan menggali terowongan aman dari server mereka di awan, langsung menembus ke dalam folder `C:\laragon\www` milik Anda. Mereka lalu memberikan sebuah *URL* publik berakhiran `ngrok.io` atau `ngrok-free.app`.

Siapapun di muka bumi ini—entah itu klien di Jakarta, maupun atasan Anda di New York—yang mengklik *URL* publik tersebut, akan secara gaib sedang "mengintip" dan berselancar langsung di dalam laptop Anda secara *real-time*.

Hal yang paling luar biasa? **Laragon sudah menyuntikkan Ngrok ke dalam sistemnya!**

---

## 🎇 Praktik: Sihir "Satu Klik" Laragon

Mari kita buka terowongan Anda ke dunia luar. Pastikan laptop Anda terhubung ke internet.

1. Buka aplikasi Laragon dan pastikan Apache/Nginx sudah **Start**.
2. Klik kanan di area putih kosong pada jendela Laragon.
3. Arahkan kursor ke menu **Share**, lalu klik opsi **Share -> tokoku.test** (Pilih nama *virtual host* proyek yang ingin Anda pamerkan).
4. Sebuah jendela terminal hitam (Command Prompt) akan tiba-tiba muncul.
5. Perhatikan baris yang bertuliskan **`Forwarding`**. Anda akan melihat tautan ajaib berwarna hijau. Contohnya: `https://a1b2c3d4.ngrok-free.app`.
6. Blok tautan `https://...` tersebut, lalu tekan **Klik Kanan** pada *mouse* Anda untuk men-*copy* teksnya (Di CMD Windows, blok teks lalu klik kanan = Copy).
7. Kirim tautan (*link*) tersebut ke WhatsApp Klien Anda.

**BOOM! 🤯**
Saat klien Anda membuka tautan tersebut dari *smartphone* mereka, mereka akan melihat *website* yang ada di laptop Anda dengan sempurna. 

Setiap kali Anda menekan `CTRL + S` (Save) pada kode Anda, klien Anda hanya perlu me-*refresh* peramban mereka untuk melihat perubahannya secara *live*! 

> [!TIP]
> **Tutup Terowongan Setelah Selesai!**
> Karena Klien mengakses web langsung dari laptop Anda, jika laptop Anda dimatikan atau internet Anda putus, *website* tersebut juga akan mati (*Offline*). Selalu ingat untuk menutup terminal Ngrok (klik tombol X merah) setelah sesi *demo* klien selesai demi keamanan lalu lintas data Anda.

---

## 🚑 Klinik Darurat: Mengatasi Error Otentikasi

Meskipun sihir ini sangat hebat, sejak tahun 2023 Ngrok memperketat keamanannya dan **mewajibkan** penggunanya memiliki *Authtoken* (Kunci Otentikasi) gratis.

Jika terminal hitam Anda langsung tertutup sendiri atau menampilkan *error* otentikasi saat menekan tombol *Share*, jangan panik. Ikuti langkah anti-gagal ini:

1. Kunjungi website [ngrok.com](https://ngrok.com/) dan buat akun gratis (Bisa *Login with Google*).
2. Setelah masuk ke *Dashboard* Ngrok, cari menu **Your Authtoken** di bilah kiri.
3. Anda akan melihat sebuah kode panjang (misal: `1xY2Z...`). Salin (*Copy*) kode tersebut.
4. Buka *Terminal* biasa di laptop Anda (CMD/PowerShell).
5. Ketik perintah ini untuk menanamkan token tersebut ke dalam PC Anda:
   ```bash
   ngrok config add-authtoken KODE_PANJANG_ANDA_TADI
   ```
6. Selesai! Sekarang ulangi kembali langkah *Klik Kanan -> Share* di aplikasi Laragon. Kali ini, terowongannya dijamin akan terbuka lebar tanpa hambatan!

Di bab selanjutnya, kita akan belajar bagaimana menggunakan *Database* MySQL di Laragon. Lupakan `localhost/phpmyadmin` yang lambat, karena Laragon membawakan "Senjata Rahasia" yang jauh lebih mematikan! ⚔️
