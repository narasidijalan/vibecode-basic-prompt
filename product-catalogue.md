STACK: HTML + CSS + Vanilla JS. 2 file terpisah. No framework.
CDN allowed: Google Fonts, AOS.js, Font Awesome 6.

TASK: Product Catalog Website — 2 Pages

═══════════════════════════════════════
FILE STRUCTURE
═══════════════════════════════════════
index.html   → Landing page (1 halaman scroll)
catalog.html → Halaman katalog lengkap + pagination

Navigasi antar halaman: <a href="..."> biasa (no SPA routing)

═══════════════════════════════════════
STATIC DATA (hardcoded, mudah diedit)
═══════════════════════════════════════
const brand = {
  name:      "Nusantara Craft",
  tagline:   "Kerajinan Tangan Asli Indonesia, Dikirim ke Seluruh Dunia",
  logo:      "🪵",
  phone:     "+62 812-3456-7890",
  whatsapp:  "6281234567890",
  email:     "hello@nusantaracraft.id",
  address:   "Jl. Malioboro No. 88, Yogyakarta 55271",
  mapsURL:   "https://maps.google.com/?q=Malioboro+Yogyakarta",
  instagram: "@nusantaracraft",
  hours:     "Senin – Sabtu, 08.00 – 17.00 WIB",
}

const products = [
  { id:1,  name:"Tas Anyam Pandan",      category:"Tas",       price:185000,  badge:"Terlaris",  rating:4.8, sold:320, desc:"Tas anyaman pandan premium, ringan dan kuat" },
  { id:2,  name:"Kotak Bambu Ukir",      category:"Dekorasi",  price:235000,  badge:"Baru",      rating:4.7, sold:180, desc:"Kotak penyimpanan bambu dengan ukiran motif Jawa" },
  { id:3,  name:"Dompet Kulit Batik",    category:"Aksesoris", price:155000,  badge:"Terlaris",  rating:4.9, sold:540, desc:"Dompet kulit asli dengan motif batik klasik" },
  { id:4,  name:"Lampu Rotan Bulat",     category:"Dekorasi",  price:320000,  badge:"",          rating:4.6, sold:95,  desc:"Lampu hias rotan untuk interior rumah modern" },
  { id:5,  name:"Sandal Enceng Gondok",  category:"Alas Kaki", price:125000,  badge:"Baru",      rating:4.5, sold:210, desc:"Sandal unik dari serat enceng gondok natural" },
  { id:6,  name:"Topi Anyam Lebar",      category:"Aksesoris", price:95000,   badge:"",          rating:4.7, sold:430, desc:"Topi pantai anyaman bambu anti panas" },
  { id:7,  name:"Cermin Bingkai Jati",   category:"Dekorasi",  price:480000,  badge:"Premium",   rating:4.9, sold:67,  desc:"Cermin dengan bingkai kayu jati ukir tangan" },
  { id:8,  name:"Tempat Tisu Rotan",     category:"Dekorasi",  price:85000,   badge:"",          rating:4.4, sold:290, desc:"Tempat tisu rotan minimalis untuk meja kantor" },
  { id:9,  name:"Gelang Kayu Cendana",   category:"Aksesoris", price:65000,   badge:"Terlaris",  rating:4.8, sold:670, desc:"Gelang kayu cendana harum alami" },
  { id:10, name:"Rak Bambu 3 Susun",     category:"Furnitur",  price:550000,  badge:"Premium",   rating:4.7, sold:88,  desc:"Rak penyimpanan bambu kokoh 3 tingkat" },
  { id:11, name:"Tudung Saji Anyam",     category:"Dapur",     price:75000,   badge:"",          rating:4.5, sold:350, desc:"Tudung saji tradisional anyaman bambu" },
  { id:12, name:"Figura Foto Kayu",      category:"Dekorasi",  price:110000,  badge:"Baru",      rating:4.6, sold:145, desc:"Figura foto kayu natural ukuran 4R dan 5R" },
]

const reasons = [
  { icon:"🤲", title:"100% Handmade",        desc:"Setiap produk dibuat tangan oleh pengrajin lokal berpengalaman" },
  { icon:"🌿", title:"Bahan Natural",         desc:"Menggunakan bahan alami ramah lingkungan dan berkelanjutan" },
  { icon:"🚚", title:"Pengiriman Ke Seluruh Indonesia", desc:"Dikemas aman, dikirim cepat ke seluruh wilayah Indonesia" },
  { icon:"✅", title:"Garansi Kualitas",      desc:"Tidak puas? Kami kembalikan uang Anda tanpa syarat" },
  { icon:"💬", title:"Respon Cepat",          desc:"Tim kami siap membantu via WhatsApp dalam 1x24 jam" },
  { icon:"🎁", title:"Custom Order",          desc:"Terima pesanan custom dengan nama atau motif pilihan Anda" },
]

═══════════════════════════════════════
PAGE 1: index.html
═══════════════════════════════════════

SECTION 1 — NAVBAR
- Logo (emoji + brand.name), sticky top, blur backdrop
- Menu: Beranda | Katalog | Tentang | Kontak
- Tombol CTA: "Lihat Katalog" → href="catalog.html"
- Hamburger menu di mobile (toggle show/hide nav links)

SECTION 2 — HERO
- Full viewport height (100vh)
- Background: gradient mesh 2 warna (gunakan CSS gradient, 
  no gambar eksternal)
- Konten tengah (centered):
  - Badge kecil: "✨ Produk Kerajinan #1 Yogyakarta"
  - H1: brand.tagline (animasi typewriter CSS)
  - Paragraf deskripsi singkat brand (2 kalimat)
  - 2 tombol CTA:
    - Primary: "Lihat Katalog" → catalog.html
    - Secondary: "Hubungi Kami" → wa.me/brand.whatsapp
  - Stats row: "320+ Produk" | "10.000+ Pembeli" | "4.8★ Rating"
- Scroll indicator bouncing arrow di bawah

SECTION 3 — ALASAN MEMILIH KAMI
- Heading: "Mengapa Memilih Kami?"
- Grid 3×2 desktop, 1×6 mobile
- Setiap kartu: ikon besar, judul, deskripsi
- Hover effect: lift shadow + border warna aksen
- AOS: fade-up per kartu dengan delay stagger 100ms

SECTION 4 — PRODUK POPULER
- Heading: "Produk Terlaris"
- Tampilkan hanya produk dengan badge "Terlaris" dari array products
- Grid: 3 kolom desktop, 2 kolom tablet, 1 kolom mobile
- Setiap kartu produk:
  - Placeholder gambar (gradient unik per kategori, tampilkan ikon kategori)
  - Badge jika ada (Terlaris/Baru/Premium) — warna berbeda per badge
  - Nama produk
  - Harga format Rp (titik ribuan)
  - Rating bintang + jumlah terjual
  - Tombol "Pesan via WA" → buka wa.me dengan pesan preset:
    "Halo, saya tertarik dengan produk [nama produk] seharga [harga]"
- Tombol di bawah grid: "Lihat Semua Produk →" → catalog.html

SECTION 5 — ALAMAT & KONTAK
- Layout 2 kolom desktop, 1 kolom mobile
- Kolom kiri:
  - Heading "Temukan Kami"
  - List info: 📍 Alamat, 📞 Telepon, ✉️ Email, 🕐 Jam Operasional
  - Tombol "Buka di Google Maps" → brand.mapsURL
  - Tombol "Chat WhatsApp" → wa.me/brand.whatsapp
- Kolom kanan:
  - Placeholder peta (kotak abu dengan teks "📍 Peta Lokasi" 
    dan tombol yang buka mapsURL — no iframe)

SECTION 6 — FOOTER
- Background gelap
- Kolom 3: Brand info | Quick links | Kontak
- Baris bawah: copyright + "Made with ❤️ in Yogyakarta"
- Social media icons (Font Awesome): Instagram, WhatsApp, Email

═══════════════════════════════════════
PAGE 2: catalog.html
═══════════════════════════════════════

NAVBAR: sama dengan index.html

FILTER BAR (sticky di bawah navbar)
- Search input: cari by nama produk (realtime filter)
- Filter kategori: tombol pill [Semua] [Tas] [Dekorasi] 
  [Aksesoris] [Alas Kaki] [Furnitur] [Dapur]
  → generate otomatis dari unique category di array products
- Sort dropdown: [Terbaru | Harga ↑ | Harga ↓ | Terlaris | Rating]
- Counter: "Menampilkan X dari Y produk"

PRODUCT GRID
- 4 kolom desktop, 2 kolom tablet, 1 kolom mobile
- Kartu produk: sama dengan index.html
- Jika hasil filter kosong → tampilkan ilustrasi kosong + teks 
  "Produk tidak ditemukan. Coba kata kunci lain."

PAGINATION
- Tampilkan 8 produk per halaman
- Komponen pagination: [« Prev] [1] [2] [3] [Next »]
- Halaman aktif: highlight warna aksen
- Prev/Next disabled + style berbeda jika di halaman pertama/terakhir
- Saat ganti halaman: scroll smooth ke atas product grid
- Pagination reset ke halaman 1 saat filter/search berubah

LOGIC URUTAN:
  1. Filter by kategori
  2. Filter by search keyword
  3. Sort hasil
  4. Paginate hasil akhir
  5. Render kartu

FOOTER: sama dengan index.html

═══════════════════════════════════════
STYLE GUIDE
═══════════════════════════════════════
--color-primary:    #2D6A4F   /* hijau hutan */
--color-secondary:  #D4A853   /* amber/gold */
--color-accent:     #74C69D   /* hijau muda */
--color-bg:         #FAFAF8   /* putih hangat */
--color-card:       #FFFFFF
--color-text:       #1B1B1B
--color-muted:      #6B7280
--color-dark:       #1A2E1E   /* footer */

--radius-card:  12px
--shadow-card:  0 2px 12px rgba(0,0,0,0.08)
--shadow-hover: 0 8px 24px rgba(0,0,0,0.15)

--font-heading: 'Playfair Display', serif   (Google Fonts)
--font-body:    'Plus Jakarta Sans', sans-serif (Google Fonts)

Mobile-first. Breakpoint: 640px (tablet), 1024px (desktop)
Max container width: 1200px, centered, padding 16px

BADGE COLORS:
- "Terlaris"  → background #FEF3C7, text #D97706
- "Baru"      → background #DCFCE7, text #16A34A
- "Premium"   → background #EDE9FE, text #7C3AED

GRADIENT PER KATEGORI (placeholder gambar):
- Tas       → #667eea → #764ba2
- Dekorasi  → #f093fb → #f5576c
- Aksesoris → #4facfe → #00f2fe
- Alas Kaki → #43e97b → #38f9d7
- Furnitur  → #fa709a → #fee140
- Dapur     → #a18cd1 → #fbc2eb

═══════════════════════════════════════
ACCEPTANCE CRITERIA
═══════════════════════════════════════
[ ] index.html tampil sempurna di 375px dan 1280px
[ ] catalog.html tampil sempurna di 375px dan 1280px
[ ] Navbar hamburger berfungsi di mobile
[ ] Search filter bekerja realtime tanpa tombol submit
[ ] Filter kategori + search + sort bekerja bersamaan
[ ] Pagination menampilkan tepat 8 produk per halaman
[ ] Halaman 1 saat filter berubah → reset otomatis ke page 1
[ ] Tombol WA membuka pesan preset dengan nama & harga produk
[ ] Semua link antar halaman berfungsi (index ↔ catalog)
[ ] Semua data bisa diedit hanya di object brand & array products
[ ] AOS animasi aktif saat scroll di kedua halaman
