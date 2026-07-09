![Difficulty: Expert](https://img.shields.io/badge/Tingkat-Pakar-red?style=for-the-badge)
![Time: 20 Mins](https://img.shields.io/badge/Durasi-20_Menit-blue?style=for-the-badge)
![Advanced Routing](https://img.shields.io/badge/Fokus-Routing_Tingkat_Tinggi-purple?style=for-the-badge)

# 🛠️ Sang Pandai Besi: Menciptakan Custom Valet Driver

Selama ini, Anda mungkin takjub mengapa Valet sangat pintar. 

Jika Anda meletakkan folder *WordPress* di Lahan Parkir, Valet tahu bahwa file utamanya ada di `index.php` (luar). 
Jika Anda meletakkan folder *Laravel*, Valet tahu bahwa ia harus masuk ke dalam folder `public/index.php`. 
Semua *magic* ini terjadi tanpa Anda mengonfigurasi rute apa pun. 

Valet dibekali dengan belasan **Driver** bawaan untuk kerangka kerja (*framework*) populer seperti Laravel, WordPress, Symfony, Magento, dan Statamic.

Namun, bagaimana jika Anda memelihara aplikasi lawas buatan kantor Anda sendiri (*In-House Framework*) atau kerangka kerja eksotis di mana *file* utamanya tersembunyi di dalam folder `core/app/index.php`? 

Valet akan kebingungan, menyerah, dan memberikan Anda halaman **404 Not Found**. 

Di bab pamungkas ini, tanggalkan seragam Ninja Anda. Pakailah apron pelindung, nyalakan tungku perapian, dan jadilah seorang **Pandai Besi**. Kita akan menempa *Driver* Valet buatan kita sendiri!

## 📋 Daftar Isi
- [Anatomi Otak Valet](#-anatomi-otak-valet)
- [Tahap 1: Menciptakan Senjata Khusus](#-tahap-1-menciptakan-senjata-khusus-localvaletdriverphp)
- [Tahap 2: Menempa Logika Driver](#-tahap-2-menempa-logika-driver)
- [Epilog: Sang Hokage Valet](#-epilog-sang-hokage-valet)

---

## 🧠 Anatomi Otak Valet

Setiap kali Anda mengetik `http://aplikasi-aneh.test`, Valet akan bertanya ke sekumpulan *Driver* secara berurutan:
1. *"Hai Driver Laravel, apakah ini aplikasimu?"* (Laravel menjawab: Tidak).
2. *"Hai Driver WordPress, apakah ini milikmu?"* (WordPress menjawab: Tidak).
3. *"Hai Driver Basic, apakah ini kodemu?"* (Tidak).

Ketika semua *Driver* menolak, terjadilah 404.
Tugas kita adalah mencegat aliran ini. Sebuah *Driver* pada dasarnya hanyalah sebuah *file* PHP biasa yang harus bisa menjawab **3 Pertanyaan Suci** dari Valet:
1. **serves()** : Apakah kamu bertanggung jawab atas *website* ini?
2. **isStaticFile()** : Apakah pengunjung sedang meminta *file* statis (CSS/JS/Gambar)?
3. **frontControllerPath()** : Di manakah letak *file* `index.php` utama dari *website* ini?

---

## 🗡️ Tahap 1: Menciptakan Senjata Khusus (LocalValetDriver.php)

Mari kita asumsikan Anda memiliki *website* yang logika utamanya ada di `folder-rahasia/index.php`.

1. Buka Terminal dan masuklah ke dalam folder proyek aneh Anda tersebut:
   ```bash
   cd ~/Sites/aplikasi-aneh
   ```
2. Anda cukup membuat sebuah *file* sakti bernama **`LocalValetDriver.php`** tepat di *root* (bagian paling luar) dari folder proyek Anda.
3. Buka *file* tersebut di Teks Editor (VS Code).

---

## ⚒️ Tahap 2: Menempa Logika Driver

Salin dan tempelkan cetakan besi (*blueprint*) kode di bawah ini ke dalam `LocalValetDriver.php`. Perhatikan bagaimana kita menjawab 3 Pertanyaan Suci Valet tadi:

```php
<?php

class LocalValetDriver extends ValetDriver
{
    /**
     * Pertanyaan 1: Apakah Driver ini yang melayani proyek ini?
     * Karena file ini kita taruh di dalam folder proyek spesifik,
     * kita selalu merespons: IYA (true).
     */
    public function serves($sitePath, $siteName, $uri)
    {
        return true; 
    }

    /**
     * Pertanyaan 2: Apakah URL yang diakses adalah file statis?
     * Jika pengunjung mengakses .css atau .jpg, kita arahkan
     * Valet untuk langsung mengambilnya tanpa melibatkan PHP.
     */
    public function isStaticFile($sitePath, $siteName, $uri)
    {
        // Mengecek apakah file tersebut nyata ada di dalam hardisk
        if (file_exists($staticFilePath = $sitePath.'/folder-rahasia/'.$uri)) {
            return $staticFilePath;
        }

        return false;
    }

    /**
     * Pertanyaan 3: Di manakah letak file index utama?
     * Semua rute (URL) yang bukan file statis akan dilempar
     * masuk ke dalam file index ini.
     */
    public function frontControllerPath($sitePath, $siteName, $uri)
    {
        // Mengarahkan ke file index spesifik milik kerangka kerja kita
        return $sitePath.'/folder-rahasia/index.php';
    }
}
```

Simpan *file* tersebut (`CTRL + S`).

**BOM! 🤯**
Anda tidak perlu me-*restart* Valet, Nginx, atau PHP. 
Detik itu juga Anda menyimpan *file* `LocalValetDriver.php` tersebut, Valet akan langsung menelannya, menyadari keberadaannya, dan ketika Anda membuka `http://aplikasi-aneh.test`, Valet akan mengeksekusi `folder-rahasia/index.php` dengan mulus!

Anda baru saja berhasil menjinakkan mesin *Routing* tingkat tinggi secara instan!

---

## 🏅 Epilog: Sang Hokage Valet

> *"Ninja terbaik tidak menyalahkan pedangnya; ia menempanya sendiri."*

Dengan selesainya *Custom Driver* ini, berakhirlah sudah Masterclass pamungkas kita di seri **Laravel Valet**.

Anda telah menempuh perjalanan yang menakjubkan. Anda memulai dari bawah dengan memahami kelemahan arsitektur Docker dan XAMPP di Mac. Anda memasang radar *Dnsmasq*, membangun pabrik *domain* `valet park`, memanipulasi *SSL* dan *port* lokal, membelah diri dengan *Per-Site PHP*, meracik brankas *DBngin*, mengebor portal dengan *Ngrok*, hingga memodifikasi otak rute dengan *Custom Valet Driver*.

Anda bukan lagi seorang *developer* Mac biasa yang panik saat menjumpai *Error 502 Bad Gateway*. Anda telah menguasai aliran bayangan. Anda mengendalikan angin (Nginx) dan tanah (Sistem File Mac) dalam harmoni yang sempurna.

Anda kini adalah sang **Hokage Valet**.
Selamat menikmati kecepatan pengembangan web yang tak tertandingi ini, dan semoga karya-karya revolusioner lahir dari ujung jari Anda! 🥷💻🥂
