![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 10 Mins](https://img.shields.io/badge/Durasi-10_Menit-blue?style=for-the-badge)
![Killer Feature](https://img.shields.io/badge/Fokus-Workflow_Agensi-purple?style=for-the-badge)

# 🧬 Mesin Kloning: Menghemat Ratusan Jam dengan Fitur Blueprints

Di bab sebelumnya, Anda telah menguasai cara menginstal WordPress dalam hitungan detik. Namun, kita tahu bahwa pekerjaan *developer* WordPress tidak berhenti di situ.

Setelah situs berhasil diinstal, Anda masih harus melakukan ritual pembersihan dan pengaturan panjang: menghapus *Hello World* post, menghapus *plugin* bawaan, mengatur *Permalink*, mengunduh *Elementor*, memasang *Yoast SEO*, menyetel tema favorit Anda, dsb.

Jika satu situs memakan waktu 30 menit untuk diatur, dan Anda membuat 10 *website* klien bulan ini, Anda telah membuang **5 jam hidup Anda** untuk tugas kuli yang diulang-ulang.

Mari kita bertransformasi dari sekadar pekerja kasar menjadi **Pemilik Pabrik**. Kita akan membuat cetakan (*Blueprint*) dan menggandakannya!

## 📋 Daftar Isi
- [Rahasia Dapur Agensi Raksasa](#-rahasia-dapur-agensi-raksasa)
- [Praktik 1: Merakit Sang "Induk Kloning"](#-praktik-1-merakit-sang-induk-kloning)
- [Praktik 2: Sihir Menggandakan Proyek](#-praktik-2-sihir-menggandakan-proyek)
- [Perawatan Mesin Kloning](#-pro-tip-perawatan-mesin-kloning)

---

## 🏢 Rahasia Dapur Agensi Raksasa

Tahukah Anda bagaimana agensi pembuat *website* raksasa bisa meluncurkan proyek klien hanya dalam hitungan hari? Senjata rahasia mereka adalah fitur **Blueprints**.

*Blueprint* (Cetak Biru) adalah fitur ajaib di aplikasi Local yang memungkinkan Anda mengambil "foto copy" dari sebuah situs WordPress yang sudah sempurna konfigurasinya, menyimpannya di dalam lemari besi, dan menggunakannya sebagai fondasi setiap kali Anda mendapat proyek klien baru.

---

## 🔬 Praktik 1: Merakit Sang "Induk Kloning"

Pertama-tama, kita harus membuat patung cetakan pertamanya.

1. Buka aplikasi Local, dan buat situs baru bernama **"Master Cetakan"** (Gunakan cara di Bab 1).
2. Masuk ke panel *WP Admin* dari "Master Cetakan" ini.
3. Lakukan ritual pembersihan dan persiapan Anda:
   - Hapus *post* "Hello World!" dan *Sample Page*.
   - Hapus semua *plugin* bawaan (seperti *Hello Dolly*).
   - Masuk ke *Settings > Permalinks* dan ubah ke **Post name**.
   - Unduh dan aktifkan *plugin* wajib Anda (misal: *Elementor, LiteSpeed Cache, Yoast SEO*).
   - Unggah dan aktifkan Tema favorit Anda (misal: *Astra* atau *Hello Elementor*).

Jika semuanya sudah dirasa sempurna layaknya kanvas bersih siap pakai, kembalilah ke jendela aplikasi **Local**.

1. **Klik Kanan** pada nama situs "Master Cetakan" di daftar sebelah kiri.
2. Pilih menu **"Save as Blueprint"**.
3. Beri nama *blueprint* Anda, misalnya: `Fondasi Web Perusahaan v1`.
4. Klik **Save Blueprint**.

Tunggu beberapa detik hingga Local memadatkan seluruh kerja keras (*database*, konfigurasi, *plugin*, dan tema) Anda menjadi satu cetak biru digital.

---

## 🎇 Praktik 2: Sihir Menggandakan Proyek

Tiga bulan kemudian, Anda mendapatkan klien baru: "Perusahaan Maju Jaya". Saatnya memanggil mesin kloning Anda beraksi!

1. Di jendela utama Local, klik tanda tambah hijau (**+ Add Local Site**) di pojok kiri bawah.
2. **JANGAN** pilih *Create a new site*. Alih-alih, pilih opsi **"Create from Blueprint"**.
3. Klik *Continue*.
4. Sebuah daftar akan muncul. Pilih cetak biru Anda: `Fondasi Web Perusahaan v1`.
5. Ketik nama situs baru untuk klien: `Maju Jaya Web`, lalu klik **Create Site**.

**BOM! 🤯 keajaiban mutlak terjadi.**
Local tidak membuat WordPress kosongan. Dalam hitungan detik, ia akan mencetak kloning yang **100% SAMA PERSIS** dengan "Master Cetakan" Anda. 

Saat Anda masuk ke *WP Admin* Maju Jaya Web, Anda akan melihat bahwa *Elementor* sudah terpasang, Tema *Astra* sudah aktif, *Permalink* sudah benar, dan tidak ada "Hello World" yang harus dihapus. Anda bisa langsung mendesain halaman web tanpa membuang waktu 1 detik pun untuk konfigurasi dasar.

Ini adalah sebuah penghematan waktu (*time-saver*) tingkat dewa!

---

## 🛠️ PRO TIP: Perawatan Mesin Kloning

Satu-satunya kelemahan dari mesin kloning adalah: *ia menghentikan waktu*. 

Artinya, jika Anda membuat *Blueprint* pada bulan Januari dengan Elementor versi `3.0`, dan menggunakannya di bulan Oktober, situs hasil kloningan Anda akan memiliki Elementor versi `3.0` (yang sudah sangat usang) dan memaksa Anda mengklik *Update* berkali-kali.

**Cara Merawatnya:**
1. Setiap 3-6 bulan sekali, jalankan situs "Master Cetakan" Anda.
2. Masuk ke *WP Admin*, lalu tekan tombol **Update All** (*Plugin, Tema, dan Core WordPress*).
3. Kembali ke Local, **Klik Kanan > Save as Blueprint** dan beri nama `Fondasi Web Perusahaan v2` (Versi 2).
4. Hapus *Blueprint* v1 yang sudah lama.

Dengan perawatan rutin ini, mesin kloning Anda akan selalu tajam, mutakhir, dan siap melahirkan karya seni WordPress instan kapan pun klien mengetuk pintu agensi Anda! 🚪🎨
