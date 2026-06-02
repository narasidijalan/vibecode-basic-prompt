MODE: CREATE
Target File: src/components/Calculator.jsx (atau index.html jika vanilla JS)
Target Route: /kalkulator
Task: Buat sebuah aplikasi web (Web App) kalkulator interaktif khusus untuk menghitung [JENIS KALKULATOR]. Aplikasi harus berfungsi penuh secara client-side, responsif, dan sangat mudah dioperasikan melalui HP (Mobile-Friendly).

Goals:
1. Menghasilkan kalkulator dengan antarmuka (UI) yang bersih, minimalis, dan intuitif untuk pengguna awam.
2. Proses perhitungan harus terjadi secara instan (real-time) saat tombol "Hitung" diklik tanpa memuat ulang (refresh) halaman.
3. Struktur halaman memisahkan dengan jelas antara area Input (Formulir), area Output (Hasil Perhitungan), dan Panduan Penggunaan.

Input Requirements:
Sediakan komponen formulir input yang divalidasi dengan baik (hanya menerima angka/format yang sesuai) untuk data berikut:
- [INPUT 1, contoh: Berat Badan dalam Kg / Jumlah Pinjaman KPR]
- [INPUT 2, contoh: Tinggi Badan dalam Cm / Suku Bunga Per Tahun]
- [INPUT 3, jika ada, contoh: Tenor Pinjaman dalam Tahun]

Output Requirements:
Tampilkan hasil perhitungan di dalam komponen "Hasil/Result Box" yang mencolok dan mudah dibaca:
- [OUTPUT 1, contoh: Skor BMI Anda / Angka Cicilan Per Bulan]
- [OUTPUT 2, jika ada, contoh: Kategori Kesehatan (Kurus/Ideal/Obesitas) / Total Bunga Pinjaman]
- Berikan visualisasi warna pendukung pada hasil jika diperlukan (misal: Hijau untuk hasil aman/ideal, Merah untuk hasil peringatan/over-budget).

UX & Documentation Section:
Tambahkan satu section ringkas di bagian bawah atau di dalam *card* kalkulator yang berisi:
1. Judul: "Cara Menggunakan Kalkulator Ini"
2. Panduan langkah demi langkah (1, 2, 3) yang ditulis dengan bahasa yang sangat sederhana agar orang awam langsung paham.

Rules & Technical Constraints:
- Mobile-First Design: Ukuran tombol (buttons) dan bidang input (input fields) harus besar dan memiliki *padding* yang pas agar mudah diketuk oleh jari di layar HP (*touch-friendly*).
- Validasi Input: Cegah pengguna memasukkan angka minus atau teks kosong. Tampilkan pesan error yang ramah di bawah kolom input jika data yang dimasukkan tidak valid.
- UI Style: Desain simpel ala aplikasi modern (Clean-cut). Gunakan latar belakang netral (Putih/Abu-abu terang) dengan aksen warna yang kontras pada tombol eksekusi ("Hitung" / "Reset").
- Kualitas Kode: Tulis fungsi logika matematika perhitungan secara terpisah dari komponen UI, pastikan kode bersih, efisien, dan menggunakan *state management* yang tepat.
