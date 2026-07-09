![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 5 Mins](https://img.shields.io/badge/Durasi-5_Menit-blue?style=for-the-badge)
![Architecture](https://img.shields.io/badge/Fokus-Filosofi_Arsitektur-purple?style=for-the-badge)

# 🥷 Prolog: Mengapa Ninja Tidak Butuh Kapal Kargo?

Selamat datang di Dojo, Sang Ninja! 🥷

Jika Anda adalah pengguna Mac (macOS), Anda mungkin pernah merasakan penderitaan ini: Anda membuka **Docker Desktop**, dan tiba-tiba kipas laptop Anda menderu kencang seperti mesin pesawat jet. Baterai Anda terkuras habis dalam 2 jam, dan RAM laptop Anda termakan hingga 4GB hanya untuk menampilkan tulisan *"Hello World"* di peramban.

Dalam dunia pengembangan *software*, **Docker dan Vagrant** adalah sebuah **Kapal Kargo Raksasa**. Mereka bisa mengangkut apa saja, menjamin lingkungan yang 100% sama dengan *server* asli, namun mengorbankan kelincahan dan kecepatan laptop Anda karena mereka harus menjalankan sebuah Sistem Operasi (OS) utuh di dalam OS laptop Anda.

Di sinilah **Laravel Valet** hadir. Valet bukanlah Kapal Kargo; Valet adalah seorang **Ninja**. Ia bergerak dalam senyap di latar belakang (*background*), sangat ringan, mematikan, dan menawarkan kecepatan pengembangan (*development speed*) yang tak tertandingi.

Di bab pembuka ini, kita akan membedah filosofi mengapa Valet bisa begitu luar biasa cepat tanpa membuat Mac Anda berkeringat.

## 📋 Daftar Isi
- [Beban Sang Kapal Kargo](#-beban-sang-kapal-kargo)
- [Membedah Aliran Ninja (Arsitektur Valet)](#-membedah-aliran-ninja-arsitektur-valet)
- [Sihir Tak Kasat Mata (Dnsmasq)](#-sihir-tak-kasat-mata-dnsmasq)
- [Kapan Anda Harus Menjadi Ninja?](#-kapan-anda-harus-menjadi-ninja)

---

## 🚢 Beban Sang Kapal Kargo

Mari kita luruskan sebuah fakta teknis: Docker dan Vagrant memakan banyak *resource* komputer karena metode **Virtualisasi**.

Saat Anda menyalakan Docker, ia akan mengalokasikan RAM (misalnya 2GB) dan inti CPU secara permanen untuk menghidupkan sebuah "komputer Linux virtual" kecil di dalam Mac Anda. Walaupun Anda sedang tidak mengoding dan hanya menonton YouTube, Linux virtual tersebut tetap menyala, memakan memori, dan menguras daya baterai Anda secara konstan.

Ini adalah harga mahal yang harus dibayar demi mendapatkan lingkungan *server* yang terisolasi.

---

## 🗡️ Membedah Aliran Ninja (Arsitektur Valet)

Valet membuang konsep virtualisasi ke tempat sampah.
Valet menggunakan kekuatan asli bawaan (*native*) dari sistem operasi Mac Anda sendiri.

Bukannya menciptakan komputer Linux virtual yang berat, Valet menggunakan **Homebrew** (Manajer Aplikasi Mac) untuk menginstal mesin web super cepat bernama **Nginx** langsung ke jantung sistem macOS Anda.

Saat Anda menyalakan Mac, Valet akan ikut menyala secara diam-diam. Nginx akan berjalan dengan konsumsi RAM yang sangat kecil (hanya dalam hitungan MegaByte, bukan GigaByte). Tidak ada virtualisasi, tidak ada alokasi *hardware* yang disandera. Seluruh proses mengeksekusi kode PHP dan melayani pengunjung web dilakukan secara langsung oleh sistem Mac Anda sendiri.

Hasilnya? Aplikasi web merespons dalam hitungan milidetik, baterai laptop tetap awet, dan kipas Mac Anda akan diam membisu.

---

## 🎩 Sihir Tak Kasat Mata (Dnsmasq)

Jika Anda membaca seri tutorial XAMPP kami sebelumnya, Anda pasti ingat siksaan di mana Anda harus mengedit *file* `hosts` dan merakit *Virtual Hosts* secara manual hanya untuk mendapatkan domain keren seperti `http://proyekku.local`.

Valet adalah seorang penyihir yang menguasai teknik **Dnsmasq**.
Dnsmasq adalah sebuah radar pengalih sinyal lokal. Valet akan memasang Dnsmasq di Mac Anda dan memberinya satu perintah sakti:

> *"Hai Mac, jika pengguna mengetikkan kata apa pun yang berakhiran **.test** di perambannya, jangan cari ke Google. Arahkan langsung ke folder laptop ini!"*

Berkat sihir Dnsmasq, Anda tidak perlu lagi menyentuh konfigurasi *Virtual Host* selamanya.
Anda cukup membuat folder baru bernama `toko-baju` di laptop Anda, dan dalam 0 detik, Anda langsung bisa mengaksesnya di *browser* dengan alamat **`http://toko-baju.test`**. 

Tidak ada tombol *Start/Stop*, tidak ada *Control Panel*, tidak ada antarmuka yang mengganggu. Ia hanya berjalan, senyap, dan seketika ada saat Anda membutuhkannya.

---

## ⚖️ Kapan Anda Harus Menjadi Ninja?

Valet adalah mahakarya seni yang indah, namun ia memiliki batasan kodratnya sendiri.

**Gunakan Valet (Jadilah Ninja) jika:**
- Anda adalah *Solo Developer* atau *Freelancer*.
- Anda memprioritaskan kecepatan (*agility*) dan membenci kelambatan.
- Anda bekerja berpindah-pindah kafe dan ingin menghemat baterai Mac Anda semaksimal mungkin.
- Proyek Anda mayoritas adalah Laravel, WordPress, atau aplikasi PHP murni yang tidak membutuhkan arsitektur *Microservices* yang sangat kompleks.

**Gunakan Docker (Jadilah Kapal Kargo) jika:**
- Anda bekerja di tim besar dengan puluhan anggota yang memakai sistem operasi campur aduk (Mac, Windows, Linux).
- Proyek Anda mewajibkan versi *environment* yang sama persis antara laptop Anda dan *Server Production*.
- Proyek Anda membutuhkan konfigurasi spesifik seperti *Redis Cluster*, *Elasticsearch*, atau *Message Broker (RabbitMQ)* tingkat lanjut yang rumit jika di- *install* secara manual.

Di bab selanjutnya, kita akan meletakkan teori ini, menarik pedang pertama kita, dan mulai menginstal infrastruktur sang Ninja ini ke dalam terminal Mac Anda. Bersiaplah melesat! ⚡🥷
