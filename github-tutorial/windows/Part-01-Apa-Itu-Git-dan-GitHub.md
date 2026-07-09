![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 10 Mins](https://img.shields.io/badge/Durasi-10_Menit-blue?style=for-the-badge)
![Concept: Core](https://img.shields.io/badge/Konsep-Fundamental-orange?style=for-the-badge)

# 🕰️ Mesin Waktu Programmer: Mengenal Git & GitHub

Pernahkah Anda membuat file bernama `skripsi_final.docx`, lalu `skripsi_final_v2.docx`, lalu `skripsi_final_BENAR.docx`, lalu `skripsi_final_BENAR_REVISI_DOSPEM.docx`?

Jika iya, selamat — Anda sudah secara tidak sadar menciptakan sistem *version control* Anda sendiri. Versi yang menyakitkan, berantakan, dan menghabiskan 3 GB penyimpanan laptop Anda.

**Git** hadir untuk mengakhiri ritual penyiksaan diri itu, selamanya.

## 📋 Daftar Isi
- [Git: Bukan Sekadar "Tombol Undo"](#-git-bukan-sekadar-tombol-undo)
- [GitHub: Bukan Sekadar "Google Drive untuk Kode"](#-github-bukan-sekadar-google-drive-untuk-kode)
- [Perbedaan Git vs GitHub (Sekali untuk Selamanya)](#-perbedaan-git-vs-github-sekali-untuk-selamanya)
- [Mengapa Setiap Developer WAJIB Menguasainya?](#-mengapa-setiap-developer-wajib-menguasainya)
- [Konsep Inti yang Harus Anda Kuasai Sekarang](#-konsep-inti-yang-harus-anda-kuasai-sekarang)

---

## ⏪ Git: Bukan Sekadar "Tombol Undo"

**Git** adalah sebuah *Version Control System* (VCS) — perangkat lunak yang bekerja di balik layar di komputer Anda untuk merekam setiap perubahan yang terjadi pada kode Anda, dari waktu ke waktu.

Tapi jangan bayangkan Git hanya sebagai "tombol Undo" biasa. Itu terlalu meremehkannya.

Bayangkan Git sebagai **Mesin Waktu pribadi Anda**. Anda bisa:
- 🔙 Kembali ke kondisi kode minggu lalu, setelah Anda menghancurkan semuanya tadi malam.
- 🔀 Membuat "linimasa paralel" (disebut *branch*) untuk mencoba fitur baru yang berani, tanpa pernah menyentuh kode utama yang sedang berjalan.
- 🤝 Menyatukan pekerjaan dari 10 programmer yang bekerja secara bersamaan, tanpa saling menimpa kode satu sama lain.

Git tidak berjalan di internet. Ia murni bekerja di laptop Anda secara *offline*. Di sinilah kebanyakan orang salah kaprah tentang perbedaannya dengan GitHub.

> 💡 **PRO TIP: Asal-usul Nama**
> Git diciptakan oleh **Linus Torvalds** — orang yang sama yang menciptakan kernel Linux — pada tahun 2005. Hanya dalam 10 hari. Dalam satu wawancara, ia mengaku menamai proyek ini "Git" (bahasa gaul Inggris yang berarti "orang menyebalkan") sebagai lelucon pribadi. Jenius yang eksentrik.

---

## ☁️ GitHub: Bukan Sekadar "Google Drive untuk Kode"

**GitHub** adalah sebuah platform berbasis web yang menjadi *rumah online* bagi repositori Git Anda.

Analoginya begini: Jika **Git** adalah kamera canggih yang Anda gunakan untuk memotret setiap momen perkembangan kode, maka **GitHub** adalah **album foto digital di cloud** tempat Anda menyimpan, memajang, dan berbagi foto-foto tersebut ke seluruh dunia.

Tapi GitHub jauh lebih dari sekadar penyimpanan. Ia adalah:

- 🌍 **Portofolio Profesional Anda**: Profil GitHub Anda *adalah* CV terbaik seorang developer. Recruiter tech di seluruh dunia melihat GitHub Anda sebelum mereka membaca CV formal Anda.
- 🤝 **Pusat Kolaborasi Tim**: Tempat tim mendiskusikan kode, memberikan ulasan (*code review*), melaporkan *bug*, dan mengelola fitur yang sedang dikerjakan.
- 🌐 **Jantung Open Source Dunia**: Hampir semua proyek open source legendaris — Linux, React, Laravel, TensorFlow — hidup di sini. Anda bisa berkontribusi pada proyek yang digunakan jutaan orang dari kamar tidur Anda sendiri.

---

## ⚖️ Perbedaan Git vs GitHub (Sekali untuk Selamanya)

Ini adalah pertanyaan yang paling sering membingungkan pemula. Jawaban singkatnya tertuang dalam tabel berikut:

| | **Git** | **GitHub** |
|---|---|---|
| **Jenis** | Perangkat Lunak (Software) | Platform Web (Website) |
| **Letak** | Di laptop/komputer Anda | Di server cloud milik Microsoft |
| **Butuh Internet?** | ❌ Tidak | ✅ Ya |
| **Fungsi Utama** | Merekam & mengelola perubahan kode | Menyimpan & berbagi kode secara online |
| **Analogi** | Kamera | Album Foto di Cloud |
| **Bisa Berdiri Sendiri?** | ✅ Ya | ❌ Tidak (butuh Git untuk mengisinya) |

> 💡 **PRO TIP:**
> Git bisa digunakan tanpa GitHub sama sekali — misalnya untuk proyek pribadi yang tidak perlu dibagikan. Namun GitHub **tidak bisa berfungsi** tanpa Git. GitHub hanyalah *antarmuka visual* yang indah di atas mesin Git yang sesungguhnya.

---

## 🚀 Mengapa Setiap Developer WAJIB Menguasainya?

Bukan lebay. Ini kenyataan industri:

**Tanpa Git**, Anda adalah seorang pengrajin yang bekerja sendirian di gubuk, tanpa catatan apapun tentang apa yang sudah dikerjakan.

**Dengan Git**, Anda adalah seorang arsitek profesional dengan cetak biru lengkap, riwayat revisi mendetail, dan kemampuan bekerja bersama tim lintas benua secara real-time.

Coba bayangkan skenario ini:
- Anda diminta join tim startup dan perlu berkontribusi pada kode yang sudah ada.
- Bos Anda meminta fitur baru dikerjakan paralel dengan *bug fix* yang mendesak.
- Klien tiba-tiba minta "kembalikan saja ke versi 2 minggu lalu, versi baru ini saya tidak suka".

Tanpa Git? Semua skenario itu adalah mimpi buruk. Dengan Git? Semua diselesaikan dengan beberapa baris perintah.

---

## 🗺️ Konsep Inti yang Harus Anda Kuasai Sekarang

Sebelum kita masuk ke aksi, kenali dulu terminologi fondasi ini. Kita akan bertemu mereka terus-menerus sepanjang seri tutorial ini:

| Istilah | Penjelasan Manusiawi |
|---|---|
| **Repository (Repo)** | "Folder ajaib" yang dilacak oleh Git. Setiap proyek punya satu repo. |
| **Commit** | Sebuah "foto" dari kondisi kode Anda pada satu titik waktu. Disertai pesan deskriptif. |
| **Branch** | "Linimasa paralel". Ruang kerja terpisah untuk fitur atau eksperimen baru. |
| **Merge** | Proses menyatukan dua *branch* menjadi satu. |
| **Clone** | Mengunduh salinan lengkap sebuah repo dari GitHub ke laptop Anda. |
| **Push** | Mengirim *commit* dari laptop Anda ke GitHub (menyimpan ke cloud). |
| **Pull** | Mengambil perubahan terbaru dari GitHub ke laptop Anda. |
| **Remote** | Nama panggilan untuk server GitHub yang menyimpan repo online Anda. Default-nya: `origin`. |

Jangan paksa diri Anda untuk menghafal semua istilah ini sekarang. Pahami saja garis besarnya — maknanya akan mengkristal secara alami saat kita praktik langsung di bab-bab berikutnya.

---

Anda baru saja selesai meletakkan fondasi pemahaman yang banyak developer abaikan. Kebanyakan orang langsung loncat ke `git push` tanpa tahu apa yang sebenarnya sedang terjadi di balik layar. Anda tidak demikian.

Di bab selanjutnya, kita akan memasang **Git** di Windows Anda dan melakukan konfigurasi identitas pertama Anda — ritual inisiasi wajib sebelum kita bisa mulai merekam sejarah kode kita. ⚙️

---
*Selanjutnya: [Part 2 — Instalasi Git di Windows & Konfigurasi Pertama](Part-02-Instalasi-Git-di-Windows.md)*
