MODE: CREATE
Target File: src/App.jsx (atau index.html jika vanilla JS)
Target Route: /
Task: Buat sebuah website personal professional/biodata (portfolio) satu halaman (single-page) yang modern, sleek, ultra-responsive, dan memiliki fitur dark mode.

Goals:
1. Website memiliki navigasi yang smooth (smooth scrolling) ke 7 section utama: Home, Bio, Pengalaman, Project, Pendidikan, Portofolio, dan Kontak.
2. Tampilan visual harus "memanjakan mata" (clean aesthetic) dengan whitespace yang pas, tipografi yang kuat, dan animasi transisi yang halus (subtle fade-in/slide-up saat scroll).
3. Memiliki tombol Toggle Dark Mode/Light Mode yang presisi di pojok kanan atas (sticky/fixed navbar) dan otomatis mendeteksi preferensi sistem perangkat pengguna saat pertama kali dibuka.
4. Layout harus 100% Mobile-First Responsive (terlihat seperti aplikasi native di HP, dan rapi dalam grid/kolom yang seimbang di monitor desktop).

Section Requirements:
1. Navigasi: Sticky navbar minimalis dengan logo inisial nama di kiri, menu navigasi di tengah (sembunyi jadi hamburger menu di mobile), dan tombol Toggle Dark Mode di kanan.
2. Home: Tampilkan Nama Lengkap (porsi teks besar/bold), Tagline Profesional (misal: Senior Fullstack Engineer), tombol Call-to-Action (CTA) "Hubungi Saya", dan komponen bingkai Foto Profil yang estetik (mendukung skeleton loading/placeholder).
3. Bio: Paragraf singkat yang menceritakan core value, keahlian utama, dan ringkasan profesional dengan gaya bahasa yang elegan.
4. Pengalaman: Tampilan berformat Timeline vertikal yang rapi. Setiap baris berisi: Nama Perusahaan, Posisi/Jabatan, Durasi Waktu (Tahun), dan 2-3 poin pencapaian utama.
5. Project: Tampilkan dalam bentuk Grid (1 kolom di mobile, 3 kolom di desktop). Setiap kartu project memiliki judul, deskripsi singkat teknologi yang digunakan (dalam bentuk badge/tags seperti React, Go, dll), dan tautan internal/eksternal.
6. Pendidikan: Informasi riwayat pendidikan formal atau sertifikasi penting, disusun dalam layout kartu yang bersih (clean cards).
7. Portofolio: Galeri visual (bisa berupa gambar/mockup hasil karya) yang memiliki efek hover interaktif (misalnya sedikit membesar atau memunculkan overlay teks saat kursor di atasnya).
8. Kontak: Section penutup berisi tautan sosial media profesional (GitHub, LinkedIn), email, dan tombol CTA besar yang terintegrasi langsung menuju WhatsApp dengan template pesan kustom.

Rules & Technical Constraints:
- UI Style: Gunakan pendekatan modern minimalis ala Apple/Vercel (Banyak whitespace, sudut melengkung/rounded-xl yang halus, border tipis yang elegan).
- Warna Light Mode: Background putih bersih (#FFFFFF) / abu-abu sangat muda (#F9FAFB), teks utama hitam/charcoal (#111827), aksen warna hijau segar (#22C55E) untuk tombol utama dan komponen aktif.
- Warna Dark Mode: Background gelap pekat (#0B0F19 atau #121212), teks utama putih abu-abu (#F3F4F6), komponen kartu menggunakan warna abu-abu gelap (#1F2937) dengan border tipis agar tidak flat.
- Interaktivitas: Gunakan transisi CSS (`transition-all duration-300`) pada setiap perubahan warna komponen saat dark mode diaktifkan dan saat tombol di-hover.
- Kualitas Kode: Tulis kode yang modular, komponen yang bersih, jangan ada fungsi/state yang redundan, dan pastikan tidak menggunakan library eksternal yang rumit jika bisa diselesaikan dengan CSS/Tailwind murni.
