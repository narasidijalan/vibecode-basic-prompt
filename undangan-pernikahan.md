STACK: HTML + CSS + Vanilla JS. Single file. No framework. 
CDN allowed: Google Fonts, AOS.js (animasi scroll), Tone.js (musik).

TASK: Digital Wedding Invitation — Single Page, Mobile-First

═══════════════════════════════════════
DYNAMIC DATA (via URL params)
═══════════════════════════════════════
Ambil dari URL: ?to=Budi%20Santoso
- Tampilkan sebagai: "Kepada Yth, Budi Santoso"
- Jika param tidak ada → tampilkan: "Kepada Yth, Tamu Undangan"
- Parse: const params = new URLSearchParams(window.location.search)
          const guestName = params.get('to') || 'Tamu Undangan'

═══════════════════════════════════════
STATIC DATA (hardcoded, mudah diedit)
═══════════════════════════════════════
const wedding = {
  groomName:     "Ahmad Rizki Pratama",
  groomNickname: "Rizki",
  brideName:     "Siti Nur Aisyah",
  brideNickname: "Aisyah",
  groomParents:  "Bpk. Hendra & Ibu Wulandari",
  brideParents:  "Bpk. Santoso & Ibu Marlina",

  akadDate:      "Sabtu, 14 Juni 2025",
  akadTime:      "08.00 – 10.00 WIB",
  receptionDate: "Sabtu, 14 Juni 2025",
  receptionTime: "11.00 – 14.00 WIB",
  venue:         "Gedung Graha Sarina, Jl. Mawar No. 12, Yogyakarta",
  mapsURL:       "https://maps.google.com/?q=Graha+Sarina+Yogyakarta",

  countdown:     "2025-06-14T08:00:00",
  bankName:      "BCA",
  bankNumber:    "1234567890",
  bankHolder:    "Ahmad Rizki Pratama",
}

═══════════════════════════════════════
SECTIONS (urutan scroll dari atas)
═══════════════════════════════════════
1. COVER
   - Background: full screen, gradient hijau sage + krem
   - Teks: "Bismillahirrahmanirrahim"
   - Nama pengantin besar: "[groomNickname] & [brideNickname]"
   - Teks kecil: "Kepada Yth, [guestName]"
   - Tombol CTA: "Buka Undangan" → trigger animasi reveal ke section berikutnya
   - Cover tersembunyi sampai tombol diklik (envelope reveal effect)

2. MEMPELAI
   - Foto placeholder (gunakan gradient circle, jangan <img> eksternal)
   - Nama lengkap pengantin pria & wanita
   - Nama orang tua masing-masing

3. ACARA
   - 2 kartu: Akad & Resepsi
   - Setiap kartu: ikon, tanggal, waktu, lokasi
   - Tombol "Lihat Lokasi" → buka mapsURL di tab baru

4. COUNTDOWN
   - Hitung mundur realtime ke wedding.countdown
   - Format: [DD] Hari [HH] Jam [MM] Menit [SS] Detik
   - Update tiap detik dengan setInterval
   - Jika sudah lewat → tampilkan "Alhamdulillah, kami telah menikah 🎉"

5. GALERI
   - 6 kotak foto placeholder (gradient warna-warni, label "Foto 1" dst)
   - Layout: CSS grid 3×2 desktop, 2×3 mobile
   - Klik → lightbox sederhana (overlay + close button)

6. RSVP
   - Form: Nama (prefill dari guestName), Jumlah Tamu (number), 
     Kehadiran (radio: Hadir / Tidak Hadir), Ucapan (textarea)
   - Simpan ke localStorage key: "rsvp_list" sebagai JSON array
   - Setelah submit → tampilkan pesan: 
     "Terima kasih, [nama]! Kami menantikan kehadiranmu 💚"
   - Tampilkan daftar ucapan yang sudah masuk di bawah form

7. AMPLOP DIGITAL
   - Tampilkan: nama bank, nomor rekening, nama pemilik
   - Tombol "Salin Nomor Rekening" → copy ke clipboard 
     + feedback teks "Tersalin!" selama 2 detik

8. FOOTER
   - "Dibuat dengan 💚 untuk [groomNickname] & [brideNickname]"
   - Ayat Al-Quran: Ar-Rum 30:21 (teks arab + terjemahan)

═══════════════════════════════════════
MUSIK
═══════════════════════════════════════
- Autoplay musik diblokir browser → gunakan trigger manual
- Tombol musik (ikon 🎵) fixed bottom-right
- Toggle play/pause
- Gunakan Web Audio API (Tone.js) untuk generate melodi 
  ambient sederhana (bukan file eksternal)

═══════════════════════════════════════
ANIMASI
═══════════════════════════════════════
- Gunakan AOS.js: setiap section fade-in saat scroll
- Nama pengantin di cover: animasi typewriter CSS
- Countdown angka: flip animation CSS saat berubah
- Transisi antar section: smooth scroll behavior

═══════════════════════════════════════
STYLE GUIDE
═══════════════════════════════════════
--color-primary:    #6B8F71   /* hijau sage */
--color-secondary:  #C9A96E   /* gold */
--color-bg:         #FAF7F2   /* krem */
--color-text:       #3D3D3D
--font-heading:     'Playfair Display', serif   (Google Fonts)
--font-body:        'Lato', sans-serif          (Google Fonts)
--font-arabic:      'Amiri', serif              (Google Fonts)

Mobile-first. Breakpoint desktop: min-width 768px.
Max-width container: 480px di mobile, 720px di desktop.

═══════════════════════════════════════
VALIDASI & EDGE CASES
═══════════════════════════════════════
- guestName dari URL: decode URI, trim spasi, max 50 karakter
- RSVP jumlah tamu: min 1, max 10
- Countdown tidak boleh tampil angka negatif
- Tombol salin rekening: fallback jika clipboard API tidak tersedia 
  → select text manual

═══════════════════════════════════════
ACCEPTANCE CRITERIA
═══════════════════════════════════════
[ ] URL ?to=Budi%20Santoso → tampil "Kepada Yth, Budi Santoso"
[ ] URL tanpa param → tampil "Kepada Yth, Tamu Undangan"
[ ] Countdown akurat dan update tiap detik
[ ] RSVP tersimpan di localStorage, muncul di daftar ucapan
[ ] Tombol salin rekening berfungsi + ada feedback visual
[ ] Semua section muncul dengan animasi AOS saat scroll
[ ] Tampilan rapi di layar 375px (iPhone SE) dan 768px (tablet)
[ ] Semua static data mudah diedit hanya di object `wedding` di atas
