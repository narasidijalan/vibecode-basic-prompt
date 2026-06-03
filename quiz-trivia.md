STACK: HTML + CSS + Vanilla JS. Single file. No framework.
CDN allowed: Google Fonts, Font Awesome 6, Animate.css.

TASK: Aplikasi Game Edukasi Anak SD — 2 Game dalam 1 file.
      Tampilan ceria, ramah anak, mobile-first.
      Semua data soal hardcoded, no backend, no login.

═══════════════════════════════════════
DESIGN SYSTEM — ANAK SD
═══════════════════════════════════════
--color-primary:   #FF6B6B   /* merah coral */
--color-secondary: #4ECDC4   /* tosca */
--color-yellow:    #FFE66D   /* kuning ceria */
--color-purple:    #A78BFA   /* ungu soft */
--color-green:     #6BCB77   /* hijau */
--color-orange:    #FF9A3C   /* oranye */
--color-bg:        #FFF9F0   /* krem hangat */
--color-card:      #FFFFFF
--color-text:      #2D3436

--font-heading: 'Fredoka One', cursive        (Google Fonts)
--font-body:    'Nunito', sans-serif          (Google Fonts)
--font-size-base: 18px  /* lebih besar untuk anak */

VISUAL RULES:
- Rounded corners besar: border-radius 20–32px
- Shadow playful: 0 6px 0 rgba(0,0,0,0.15) (efek tombol 3D)
- Tombol tekan: translateY(4px) + shadow hilang saat :active
- Warna background setiap layar berbeda-beda (gradient ceria)
- Banyak emoji sebagai ilustrasi pengganti gambar
- Animasi: bounce, shake, pulse — gunakan Animate.css
- Confetti effect (pure JS/CSS) saat jawaban benar atau game selesai

═══════════════════════════════════════
STRUKTUR APLIKASI
═══════════════════════════════════════
LAYAR (render satu per satu, no multi-page):
  1. HOME SCREEN
  2. GAME SELECTOR
  3. GAME A — Kuis Trivia
     3a. Intro
     3b. Soal
     3c. Hasil
  4. GAME B — Tebak Kata (Hangman)
     4a. Intro
     4b. Permainan
     4c. Hasil
  5. LEADERBOARD (localStorage)

Navigasi: function showScreen(id) → sembunyikan semua, tampilkan target
Setiap layar: animasi masuk fadeInUp 300ms

═══════════════════════════════════════
LAYAR 1 — HOME SCREEN
═══════════════════════════════════════
- Background: gradient ungu ke biru muda
- Ilustrasi emoji besar: 🎓✨📚
- Judul besar: "Belajar Sambil Bermain!"
- Sub-judul: "Pilih game dan mulai petualanganmu!"
- Input nama pemain:
  - Label: "Siapa namamu? 👤"
  - Placeholder: "Tulis namamu di sini..."
  - Max 20 karakter
  - Simpan ke variable currentPlayer + localStorage
- Tombol "MULAI! 🚀" → ke Game Selector
  - Disabled + shake animation jika nama kosong
- Di bawah: "🏆 Lihat Papan Skor" → ke Leaderboard

═══════════════════════════════════════
LAYAR 2 — GAME SELECTOR
═══════════════════════════════════════
- Header: "Halo, [nama]! 👋 Mau main apa?"
- 2 kartu game besar, tap untuk pilih:

  KARTU A — Kuis Trivia
  - Emoji besar: 🧠
  - Nama: "Kuis Pintar"
  - Deskripsi: "Jawab 10 pertanyaan seru!"
  - Badge: "10 Soal • 3 Kategori"
  - Warna: gradient merah-orange
  - Tombol: "MAIN SEKARANG →"

  KARTU B — Tebak Kata
  - Emoji besar: 🔤
  - Nama: "Tebak Kata"
  - Deskripsi: "Tebak hurufnya sebelum habis!"
  - Badge: "20 Kata • 3 Level"
  - Warna: gradient tosca-hijau
  - Tombol: "MAIN SEKARANG →"

- Tombol kecil di bawah: "← Ganti Nama"

═══════════════════════════════════════
GAME A — KUIS TRIVIA "KUIS PINTAR"
═══════════════════════════════════════

── DATA SOAL ──────────────────────────
const quizData = [
  // KATEGORI: MATEMATIKA 🔢
  {
    id:1, category:"Matematika", icon:"🔢",
    question: "Berapakah hasil dari 7 × 8?",
    options: ["54","56","64","48"],
    answer: 1, // index jawaban benar
    explanation: "7 × 8 = 56. Ingat: 7 × 8 = 56! 🌟"
  },
  {
    id:2, category:"Matematika", icon:"🔢",
    question: "Pecahan manakah yang sama dengan 1/2?",
    options: ["2/3","3/4","4/8","5/9"],
    answer: 2,
    explanation: "4/8 = 1/2 karena 4÷4=1 dan 8÷4=2 ✨"
  },
  {
    id:3, category:"Matematika", icon:"🔢",
    question: "Bilangan prima manakah di antara ini?",
    options: ["9","15","17","21"],
    answer: 2,
    explanation: "17 adalah bilangan prima karena hanya bisa dibagi 1 dan 17 🎯"
  },
  {
    id:4, category:"Matematika", icon:"🔢",
    question: "Luas persegi dengan sisi 6 cm adalah...",
    options: ["24 cm²","30 cm²","36 cm²","12 cm²"],
    answer: 2,
    explanation: "Luas persegi = sisi × sisi = 6 × 6 = 36 cm² 📐"
  },

  // KATEGORI: IPA 🔬
  {
    id:5, category:"IPA", icon:"🔬",
    question: "Planet apakah yang paling dekat dengan Matahari?",
    options: ["Venus","Bumi","Merkurius","Mars"],
    answer: 2,
    explanation: "Merkurius adalah planet pertama dan terdekat dari Matahari 🌞"
  },
  {
    id:6, category:"IPA", icon:"🔬",
    question: "Hewan apakah yang mengalami metamorfosis sempurna?",
    options: ["Belalang","Kupu-kupu","Kecoa","Jangkrik"],
    answer: 1,
    explanation: "Kupu-kupu: telur → ulat → kepompong → kupu-kupu 🦋"
  },
  {
    id:7, category:"IPA", icon:"🔬",
    question: "Zat apakah yang dibutuhkan tumbuhan untuk fotosintesis?",
    options: ["Oksigen","Nitrogen","Karbon Dioksida","Hidrogen"],
    answer: 2,
    explanation: "Tumbuhan menyerap CO₂ + air + cahaya → menghasilkan O₂ 🌿"
  },

  // KATEGORI: IPS 🌏
  {
    id:8, category:"IPS", icon:"🌏",
    question: "Ibu kota provinsi Jawa Tengah adalah...",
    options: ["Surabaya","Semarang","Bandung","Yogyakarta"],
    answer: 1,
    explanation: "Semarang adalah ibu kota Provinsi Jawa Tengah 🏙️"
  },
  {
    id:9, category:"IPS", icon:"🌏",
    question: "Pancasila sebagai dasar negara disahkan pada tanggal...",
    options: ["17 Agustus 1945","18 Agustus 1945","1 Juni 1945","22 Juni 1945"],
    answer: 1,
    explanation: "Pancasila disahkan pada 18 Agustus 1945 bersama UUD 1945 🇮🇩"
  },
  {
    id:10, category:"IPS", icon:"🌏",
    question: "Suku Asmat berasal dari provinsi...",
    options: ["Maluku","NTT","Papua","Kalimantan"],
    answer: 2,
    explanation: "Suku Asmat adalah suku asli dari Papua, terkenal dengan ukiran kayunya 🎨"
  },
]

── INTRO KUIS ──────────────────────────
- Kartu besar dengan:
  - Emoji 🧠 animasi bounce
  - Judul "Kuis Pintar"
  - Rules:
    "✅ 10 pertanyaan pilihan ganda"
    "⏱️ 20 detik per soal"
    "⭐ +10 poin jawaban benar"
    "⚡ Bonus poin jika jawab cepat!"
  - Pilih kategori: [Semua 🎯 | Matematika 🔢 | IPA 🔬 | IPS 🌏]
  - Tombol "MULAI KUIS! 🚀"

── LAYAR SOAL ──────────────────────────
HEADER:
- Progress bar soal: "Soal 3 dari 10"
  → bar terisi sesuai progress, warna gradient
- Skor saat ini: "⭐ 30 poin"
- Timer countdown visual:
  → Lingkaran SVG countdown 20 detik
  → Warna: hijau (>10s) → kuning (5–10s) → merah (<5s) + pulse animation
  → Suara tick (Web Audio API beep sederhana) 3 detik terakhir
  → Jika habis → otomatis lanjut, tandai salah

SOAL:
- Badge kategori + ikon di atas
- Teks soal, font besar (22px), centered, card putih shadow
- 4 tombol pilihan (A/B/C/D) — layout 2×2 di mobile
  - Warna berbeda per opsi: merah/biru/hijau/ungu
  - Efek 3D shadow saat hover/active
  - Setelah dipilih:
    → Benar: tombol hijau + ikon ✅ + animasi bounce + "+10 poin!" float up
    → Salah: tombol merah + ikon ❌ + animasi shake
    → Jawaban benar highlight hijau (jika pemain salah pilih)
  - Setelah dijawab: tampilkan card "explanation" slide up
  - Tombol "Lanjut →" muncul setelah 1.5 detik

BONUS POIN:
- Jawab dalam 5 detik pertama → +5 bonus → tampilkan "⚡ SUPER CEPAT! +15"
- Jawab 5–10 detik → +2 bonus
- Jawab > 10 detik → +10 saja

── HASIL KUIS ──────────────────────────
- Animasi confetti jika skor ≥ 70
- Emoji + pesan sesuai skor:
  90–100: "🏆 LUAR BIASA! Kamu jenius!"
  70–89:  "⭐ HEBAT! Kamu sangat pintar!"
  50–69:  "👍 BAGUS! Terus belajar ya!"
  < 50:   "💪 SEMANGAT! Coba lagi, pasti bisa!"
- Skor besar: "X / 100 poin"
- Ringkasan: ✅ Benar: X | ❌ Salah: X | ⏱️ Rata-rata waktu: Xs
- Review jawaban: accordion per soal
  (tampilkan soal, jawaban pemain, jawaban benar, penjelasan)
- 3 tombol: "🔄 Main Lagi" | "🏠 Menu" | "🏆 Papan Skor"
- Auto-simpan skor ke localStorage

═══════════════════════════════════════
GAME B — TEBAK KATA "HANGMAN"
═══════════════════════════════════════

── DATA KATA ──────────────────────────
const wordData = [
  // LEVEL MUDAH (4–5 huruf)
  { word:"APEL",    hint:"🍎 Buah berwarna merah atau hijau",        category:"Buah",    level:"mudah"  },
  { word:"BUKU",    hint:"📚 Tempat menyimpan ilmu pengetahuan",     category:"Benda",   level:"mudah"  },
  { word:"KUCING",  hint:"🐱 Hewan peliharaan yang suka mengeong",   category:"Hewan",   level:"mudah"  },
  { word:"MERAH",   hint:"🔴 Warna seperti darah atau apel",        category:"Warna",   level:"mudah"  },
  { word:"PANDA",   hint:"🐼 Hewan lucu hitam putih dari Cina",     category:"Hewan",   level:"mudah"  },
  { word:"MEJA",    hint:"🪑 Tempat kita belajar dan makan",        category:"Benda",   level:"mudah"  },
  { word:"SINGA",   hint:"🦁 Raja hutan yang mengaum keras",        category:"Hewan",   level:"mudah"  },

  // LEVEL SEDANG (6–7 huruf)
  { word:"JERAPAH", hint:"🦒 Hewan dengan leher sangat panjang",    category:"Hewan",   level:"sedang" },
  { word:"MENTARI", hint:"☀️ Bintang yang menyinari bumi kita",    category:"Alam",    level:"sedang" },
  { word:"SEKOLAH", hint:"🏫 Tempat kita belajar setiap hari",      category:"Tempat",  level:"sedang" },
  { word:"GARUDA",  hint:"🦅 Lambang negara Indonesia",             category:"Simbol",  level:"sedang" },
  { word:"PELANGI", hint:"🌈 Muncul setelah hujan, berwarna-warni", category:"Alam",    level:"sedang" },
  { word:"HARIMAU", hint:"🐯 Kucing besar bergaris hitam-oranye",   category:"Hewan",   level:"sedang" },

  // LEVEL SULIT (8+ huruf)
  { word:"INDONESIA",  hint:"🇮🇩 Nama negara kita tercinta",          category:"Negara",  level:"sulit"  },
  { word:"PANCASILA",  hint:"🛡️ Dasar negara Indonesia, 5 sila",     category:"PKN",     level:"sulit"  },
  { word:"FOTOSINTESIS",hint:"🌿 Proses tumbuhan membuat makanan",   category:"IPA",     level:"sulit"  },
  { word:"MATEMATIKA", hint:"🔢 Pelajaran hitung-menghitung",        category:"Mapel",   level:"sulit"  },
  { word:"PENGETAHUAN",hint:"💡 Hasil dari belajar dan membaca",     category:"Umum",    level:"sulit"  },
  { word:"PERSAHABATAN",hint:"🤝 Hubungan baik antar teman",         category:"Umum",    level:"sulit"  },
  { word:"KEMERDEKAAN",hint:"🏆 17 Agustus 1945, Indonesia...",      category:"Sejarah", level:"sulit"  },
]

── INTRO TEBAK KATA ──────────────────────
- Emoji 🔤 animasi bounce
- Judul "Tebak Kata"
- Rules:
  "🔤 Tebak huruf satu per satu"
  "❤️ 6 kesempatan salah"
  "💡 Ada petunjuk untuk membantumu"
  "⭐ Makin sedikit salah, makin besar poin!"
- Pilih level: [Semua | 😊 Mudah | 😐 Sedang | 😤 Sulit]
- Tombol "MULAI! 🎮"

── LAYAR PERMAINAN ──────────────────────
HEADER:
- Level badge + kategori kata
- Skor: "⭐ X poin"
- Kata ke: "Kata 3 dari 5"

HANGMAN VISUAL (ASCII art → CSS styled divs):
- Gambar hangman bertahap dari 0–6 kesalahan
- Gunakan emoji/karakter unicode, bukan canvas:
  0 salah: hanya tiang gantungan
  1 salah: + kepala (😶)
  2 salah: + badan
  3 salah: + tangan kiri
  4 salah: + tangan kanan
  5 salah: + kaki kiri
  6 salah: kepala berubah 😵 + game over
- Animasi: setiap bagian baru → fadeIn + shake ringan

AREA KATA:
- Kotak per huruf: _ _ _ _ _
  → Kotak kosong jika belum ditebak
  → Tampil huruf jika sudah ditebak benar
  → Font besar, bold, spacing lebar
  → Huruf muncul dengan animasi bounceIn

PETUNJUK:
- Teks hint tersembunyi → tombol "💡 Lihat Petunjuk"
  → Klik pertama: tampilkan hint (kurangi 3 poin dari potensi skor)
  → Badge "Petunjuk digunakan (-3 poin)"

NYAWA TERSISA:
- Tampilkan ❤️ × sisa nyawa (maksimal 6)
- Animasi: ❤️ hilang satu per satu saat salah + shake

KEYBOARD:
- 26 tombol huruf A–Z, layout QWERTY
- Tombol huruf besar, mudah ditekan (min 44px)
- Status per tombol:
  → Default: warna warni (tiap baris warna berbeda)
  → Benar: hijau + ✓
  → Salah: abu gelap + ✗ + disabled
- Juga support input keyboard fisik (keydown event)
- Tombol yang sudah diklik: disabled

FEEDBACK REAL-TIME:
- Huruf benar → kotak muncul + sound beep tinggi (Web Audio)
- Huruf salah → hangman bertambah + sound beep rendah + shake keyboard
- Seluruh kata terisi → animasi rainbow + "🎉 BENAR!"

── HASIL PER KATA ──────────────────────
- Tampil sebentar (2 detik) sebelum kata berikutnya:
  Benar: card hijau "✅ BENAR! +[poin] poin"
  Salah: card merah "❌ Kata yang benar: [KATA]"
- Poin per kata:
  Benar tanpa petunjuk, 0 salah   → 20 poin
  Benar tanpa petunjuk, 1–2 salah → 15 poin
  Benar tanpa petunjuk, 3+ salah  → 10 poin
  Benar dengan petunjuk           → dikurangi 3 poin
  Salah (6 nyawa habis)           → 0 poin

── HASIL AKHIR TEBAK KATA ──────────────
- Confetti jika benar ≥ 4 dari 5 kata
- Emoji + pesan sesuai hasil
- Total skor + ringkasan per kata (benar/salah/poin)
- 3 tombol: "🔄 Main Lagi" | "🏠 Menu" | "🏆 Papan Skor"
- Auto-simpan skor ke localStorage

═══════════════════════════════════════
LAYAR LEADERBOARD
═══════════════════════════════════════
- Header: "🏆 Papan Skor Terbaik"
- 2 tab: [Kuis Trivia] [Tebak Kata]
- List top 10 skor per game
  → Rank 1: 🥇 | Rank 2: 🥈 | Rank 3: 🥉 | Rank 4+: angka
  → Nama pemain + skor + tanggal main
  → Highlight baris jika nama = pemain saat ini
- Animasi: slide in per baris dengan delay stagger
- Tombol "🗑️ Reset Skor" (konfirmasi dulu)
- Tombol "← Kembali ke Menu"

DATA STRUCTURE localStorage:
key: "edu_game_scores"
value: {
  trivia:  [ { name, score, date, category }, ... ],
  hangman: [ { name, score, date, level }, ... ]
}
Simpan max 10 skor teratas per game.

═══════════════════════════════════════
AUDIO (Web Audio API — no file eksternal)
═══════════════════════════════════════
function playSound(type):
  "correct"  → oscillator 800Hz, 0.1s, sine wave
  "wrong"    → oscillator 200Hz, 0.3s, sawtooth
  "tick"     → oscillator 1000Hz, 0.05s (timer countdown)
  "win"      → arpeggio C-E-G-C naik, durasi 0.5s
  "gameover" → oscillator turun 400→100Hz, 0.5s

Toggle mute: tombol 🔊/🔇 di pojok kanan atas, persist localStorage.

═══════════════════════════════════════
CONFETTI (pure JS — no library)
═══════════════════════════════════════
function launchConfetti():
- Buat 80 div confetti
- Warna acak dari palet brand
- Posisi acak di atas viewport
- Animasi: jatuh + rotate + fade out
- Auto-remove setelah 3 detik

═══════════════════════════════════════
ACCEPTANCE CRITERIA
═══════════════════════════════════════
GENERAL:
[ ] Nama wajib diisi sebelum lanjut — shake jika kosong
[ ] Semua layar tampil rapi di 375px (iPhone SE)
[ ] Animasi masuk/keluar layar: fadeInUp smooth
[ ] Toggle mute berfungsi + tersimpan

KUIS TRIVIA:
[ ] Timer 20 detik countdown SVG berfungsi akurat
[ ] Warna timer berubah hijau → kuning → merah
[ ] Bonus poin dihitung sesuai kecepatan menjawab
[ ] Setelah dijawab: highlight benar hijau, salah merah
[ ] Explanation tampil setelah jawab
[ ] Filter kategori memfilter soal dengan benar
[ ] Skor tersimpan ke leaderboard

TEBAK KATA:
[ ] Keyboard A–Z semua muncul, bisa diklik + keyboard fisik
[ ] Tombol huruf disable setelah diklik
[ ] Hangman bertambah setiap salah (0–6 tahap)
[ ] Petunjuk mengurangi potensi poin
[ ] Kata acak, tidak repeat dalam 1 sesi
[ ] Skor per kata dihitung sesuai formula
[ ] Skor tersimpan ke leaderboard

LEADERBOARD:
[ ] Top 10 tersimpan di localStorage
[ ] Nama pemain saat ini di-highlight
[ ] Tab trivia dan hangman terpisah
[ ] Reset skor berfungsi dengan konfirmasi
