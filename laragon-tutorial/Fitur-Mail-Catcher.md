![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 10 Mins](https://img.shields.io/badge/Durasi-10_Menit-blue?style=for-the-badge)
![Killer Feature](https://img.shields.io/badge/Fitur-Mail_Catcher-critical?style=for-the-badge)

# 📬 Kotak Pos Hantu: Menguji Email Lokal Tanpa Spam

Mari kita bedah sebuah ketakutan klasik para *developer*.

Anda sedang membangun fitur **"Lupa Password"** atau **"Kirim Struk Pembelian"** di aplikasi web Anda. Bagaimana cara menguji apakah email tersebut berhasil dikirim dan format tampilannya (*HTML/CSS*) tidak berantakan?

Mencoba mengirim email *sungguhan* dari *localhost* (laptop Anda) adalah mimpi buruk. Anda harus:
1. Mendaftar layanan SMTP raksasa (Mailgun/Sendgrid).
2. Memasukkan kata sandi email asli Anda ke dalam kode (sangat tidak aman).
3. Mengirim puluhan email uji coba ke alamat Gmail Anda sendiri, yang pada akhirnya akan membuat Gmail memblokir Anda karena dianggap sebagai *Spammer*.

Laragon melihat penderitaan ini dan menciptakan sebuah **Kotak Pos Hantu** (*Mail Catcher*).

## 📋 Daftar Isi
- [Apa itu Kotak Pos Hantu (Mail Catcher)?](#-apa-itu-kotak-pos-hantu-mail-catcher)
- [Praktik: Menghidupkan Sang Penangkap Email](#-praktik-menghidupkan-sang-penangkap-email)
- [Eksperimen: Mengirim Email Palsu](#-eksperimen-mengirim-email-palsu)
- [Mengapa Fitur Ini Menyelamatkan Karir Anda?](#-mengapa-fitur-ini-menyelamatkan-karir-anda)

---

## 👻 Apa itu Kotak Pos Hantu (Mail Catcher)?

*Mail Catcher* adalah program kecil bawaan Laragon yang bertindak sebagai "lubang hitam" untuk semua email yang keluar dari aplikasi Anda.

Sistem kerjanya sangat brilian:
Saat kode PHP/Node.js Anda berteriak, *"Kirim email ini ke presiden@negara.com!"*, email tersebut **TIDAK AKAN PERNAH** benar-benar pergi ke internet. 

Alih-alih terkirim ke dunia nyata, *Mail Catcher* Laragon akan menangkap email tersebut di udara, mencekiknya, dan menampilkannya di sebuah jendela kecil di layar Anda. 

Anda bisa melihat subjek, alamat penerima, hingga desain HTML email tersebut, dengan jaminan keamanan 100% bahwa email tersebut tidak akan pernah sampai ke *inbox* siapapun.

---

## 🔮 Praktik: Menghidupkan Sang Penangkap Email

Mari kita panggil "Kotak Pos Hantu" ini ke layar Anda:

1. Buka aplikasi Laragon Anda.
2. **Klik Kanan** di area putih yang kosong.
3. Masuk ke menu **Tools** > **Mail Catcher**.
4. Sebuah jendela *Mail Catcher* kecil akan muncul. Biarkan jendela ini tetap terbuka.
   *(Jika Anda menggunakan Laragon versi lama, fitur ini otomatis aktif saat aplikasi mengirim email).*

Itu saja! Anda tidak perlu mengkonfigurasi file `.env` yang rumit, tidak perlu mengatur *Port SMTP*, dan tidak perlu memasukkan *password* email asli Anda.

---

## ✉️ Eksperimen: Mengirim Email Palsu

Mari kita buktikan sihir ini dengan menulis kode pengirim email yang sangat sederhana.

1. Buka *File Explorer*, masuk ke `C:\laragon\www`.
2. Buat folder baru bernama `uji-email`.
3. Di dalam folder `uji-email`, buat sebuah *file* bernama `kirim.php`.
4. Buka `kirim.php` dan masukkan mantra PHP murni ini:

```php
<?php
// Tujuan palsu
$to = "presiden@negara.com";
$subject = "Rencana Rahasia Laragon";
$message = "<h1>Halo Pak Presiden!</h1><p>Ini adalah email dari Kotak Pos Hantu.</p>";

// Header agar email dibaca sebagai HTML
$headers = "MIME-Version: 1.0" . "\r\n";
$headers .= "Content-type:text/html;charset=UTF-8" . "\r\n";
$headers .= "From: hacker@local.test" . "\r\n";

// Eksekusi pengiriman!
mail($to, $subject, $message, $headers);

echo "Sihir email telah dirapal!";
?>
```

5. Buka *browser* Anda dan ketik: **`http://uji-email.test/kirim.php`**
6. Sekarang, periksa aplikasi Laragon atau jendela **Mail Catcher** Anda. 

**BOOM! 🤯**
Sebuah notifikasi akan muncul, menampilkan *file* berformat `.eml` yang berisi email yang baru saja Anda kirim. Buka *file* tersebut, dan Anda akan melihat desain `<h1/>` dan `<p/>` persis seperti saat dibuka di *inbox* Gmail, padahal internet Anda mati sekalipun!

---

## 🛡️ Mengapa Fitur Ini Menyelamatkan Karir Anda?

> [!CAUTION]
> **Mimpi Buruk Production**
> Banyak insiden di mana seorang *developer* menguji aplikasi *(testing)* menggunakan *database* asli, lalu tanpa sengaja mengirim email *Spam* "TESTING 123" ke 50.000 pelanggan aktif perusahaan. 

Dengan membiasakan diri menggunakan *Mail Catcher* saat *development*, Anda membangun tembok pertahanan anti-bocor. Anda bisa bereksperimen dengan desain *Newsletter* ribuan kali di laptop Anda, merasa tenang, aman, dan tanpa pernah takut merusak reputasi domain perusahaan Anda.

Di bab selanjutnya (Level 3), kita akan memasuki kelas **Dewa**. Kita akan membahas cara memadukan Laragon dengan *Framework* tingkat tinggi seperti Laravel dan WordPress secara instan! ⚡
