# 🚀 Kumpulan Template Prompt Vibe Coding (Siap Pakai)

Repositori ini berisi kumpulan template *prompt* terstruktur tingkat tinggi menggunakan metode **Structure-Based Prompting** (`MODE`, `Target File`, `Task`, `Goals`, `Rules`). Template ini dirancang khusus untuk membangun berbagai jenis website dan aplikasi web secara instan, presisi, dan minim error menggunakan AI Code Editor modern.

---

## 📋 Daftar Isi Template Prompt
1. [Prompt 1: Web Portofolio & Biodata Profesional](#1-web-portofolio--biodata-profesional)
2. [Prompt 2: Landing Page Bisnis Konversi Tinggi](#2-landing-page-bisnis-konversi-tinggi)
3. [Prompt 3: Aplikasi Web Kalkulator Interaktif](#3-aplikasi-web-kalkulator-interaktif)
4. [Prompt 4: Website Profil Sekolah & Madrasah](#4-website-profil-sekolah--madrasah)

---

## 🛠️ Cara Penggunaan di Berbagai Platform AI

Untuk mendapatkan hasil kode yang paling rapi dan sesuai ekspektasi, ikuti panduan penggunaan template ini di platform AI favorit Anda:

### 1. ⚡ Bolt.new (Web-Based Instant Deployment)
Bolt.new sangat cocok untuk membuat prototype web siap pakai dalam hitungan detik langsung dapet link url online.
* **Langkah-langkah:**
  1. Buka [Bolt.new](https://bolt.new) di browser Anda.
  2. Pilih framework yang Anda inginkan (misal: **Vite React**).
  3. Salin salah satu template prompt dari repositori ini, lalu isi bagian di dalam tanda kurung siku `[...]` sesuai kebutuhan Anda.
  4. Tempel (*paste*) prompt ke dalam kolom chat utama Bolt.new di bagian bawah layar, lalu tekan **Enter**.
  5. Perhatikan AI membangun aplikasi secara *live* di sebelah kanan. Jika sudah selesai, klik tombol **Deploy** di pojok kanan atas untuk meng-online-kan web Anda.

### 2. 🤖 Cursor IDE (Advanced AI Code Editor)
Cursor sangat kuat untuk mengedit file spesifik di dalam proyek lokal komputer Anda menggunakan fitur Composer.
* **Langkah-langkah:**
  1. Buka folder proyek Anda di aplikasi **Cursor**.
  2. Tekan tombol `Ctrl + I` (Windows) atau `Cmd + I` (Mac) untuk membuka fitur **AI Composer** (bukan chat biasa).
  3. Pastikan Anda mengetik simbol `@` lalu pilih file yang dituju pada bagian `Target File` agar AI langsung fokus ke file tersebut.
  4. Masukkan prompt terstruktur dari repositori ini, sesuaikan variabel `[...]`, lalu klik **Submit**.
  5. Tekan **Accept All** (atau `Ctrl + Enter`) setelah Anda meninjau perubahan kode yang dibuat oleh AI.

### 3. 🌊 Trae IDE (Next-Gen AI Code Builder)
Trae memiliki fitur "Builder Mode" yang sangat cerdas untuk mengeksekusi perintah pembuatan file baru maupun modifikasi dari nol.
* **Langkah-langkah:**
  1. Buka folder kerja Anda di dalam **Trae IDE**.
  2. Alihkan panel samping ke mode **Trae Copilot / Builder**.
  3. Pastikan mode berada di opsi **Builder** (bukan Chat biasa) agar AI memiliki izin untuk membuat dan memodifikasi file secara otomatis.
  4. Salin prompt dari repositori ini, lengkapi bagian variabel `[...]`, lalu kirim prompt tersebut.
  5. Trae akan membedah tugas Anda menjadi beberapa sub-task. Cukup klik tombol **Apply** atau **Approve** pada setiap perubahan file yang diajukan AI.

---

---

## 🗂️ Isi Master Template Prompt

### 1. Web Portofolio & Biodata Profesional
```text
MODE: CREATE
Target File: src/App.jsx (atau index.html)
Target Route: /
Task: Buat sebuah website personal professional/biodata (portfolio) satu halaman (single-page) yang modern, sleek, ultra-responsive, dan memiliki fitur dark mode.

Goals:
1. Website memiliki navigasi yang smooth ke 7 section utama: Home, Bio, Pengalaman, Project, Pendidikan, Portofolio, dan Kontak.
2. Tampilan visual harus "memanjakan mata" (clean aesthetic) dengan whitespace yang pas, tipografi yang kuat, dan animasi transisi yang halus.
3. Memiliki tombol Toggle Dark Mode/Light Mode yang presisi di pojok kanan atas dan otomatis mendeteksi preferensi sistem perangkat pengguna.
4. Layout harus 100% Mobile-First Responsive.

Rules & Technical Constraints:
- UI Style: Modern minimalis (Banyak whitespace, sudut melengkung/rounded-xl halus, border tipis elegan).
- Warna Light Mode: Background putih bersih (#FFFFFF), teks utama hitam (#111827), aksen warna hijau segar (#22C55E) untuk tombol utama.
- Warna Dark Mode: Background gelap pekat (#121212), teks utama putih abu-abu (#F3F4F6), komponen kartu menggunakan warna abu-abu gelap (#1F2937).
- Kualitas Kode: Tulis kode yang modular, komponen yang bersih, dan pastikan tidak menggunakan library eksternal yang rumit jika bisa diselesaikan dengan CSS/Tailwind murni.
