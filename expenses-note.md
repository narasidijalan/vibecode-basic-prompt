STACK: HTML + CSS + Vanilla JS. Single file. No framework.
CDN allowed: Google Fonts, Chart.js, Font Awesome 6, AOS.js.

TASK: Aplikasi Catatan Pengeluaran Pribadi
      Semua data tersimpan di localStorage — no backend, no login.

═══════════════════════════════════════
DATA STRUCTURE (localStorage)
═══════════════════════════════════════
key: "expenses_data"
value: JSON array of:
{
  id:        string (Date.now().toString()),
  date:      string "YYYY-MM-DD",
  amount:    number,
  category:  string,
  source:    string,
  note:      string,
  createdAt: string ISO date
}

key: "budget_data"
value: JSON object:
{
  monthly: number  // budget bulanan, default 0
}

═══════════════════════════════════════
STATIC CONFIG
═══════════════════════════════════════
const SOURCES = [
  { id:"cash",     label:"Cash",     icon:"💵", color:"#6B7280" },
  { id:"mbanking", label:"M-Banking",icon:"🏦", color:"#2563EB" },
  { id:"dana",     label:"DANA",     icon:"💙", color:"#118EEA" },
  { id:"gopay",    label:"GoPay",    icon:"💚", color:"#00AED6" },
  { id:"ovo",      label:"OVO",      icon:"💜", color:"#4C3494" },
  { id:"lainnya",  label:"Lainnya",  icon:"💳", color:"#9CA3AF" },
]

const CATEGORIES = [
  { id:"makan",      label:"Makan & Minum",   icon:"🍽️" },
  { id:"transport",  label:"Transportasi",     icon:"🚗" },
  { id:"belanja",    label:"Belanja",          icon:"🛍️" },
  { id:"kesehatan",  label:"Kesehatan",        icon:"💊" },
  { id:"hiburan",    label:"Hiburan",          icon:"🎮" },
  { id:"tagihan",    label:"Tagihan",          icon:"📄" },
  { id:"pendidikan", label:"Pendidikan",       icon:"📚" },
  { id:"lainnya",    label:"Lainnya",          icon:"📦" },
]

═══════════════════════════════════════
LAYOUT — BOTTOM NAV (mobile-first)
═══════════════════════════════════════
Fixed bottom navigation bar, 4 tab:
  🏠 Beranda  |  ➕ Tambah  |  📊 Laporan  |  ⚙️ Pengaturan

Aktif tab: highlight warna aksen + label bold
Konten setiap tab render di area atas (single page, no reload)

═══════════════════════════════════════
TAB 1 — BERANDA
═══════════════════════════════════════
SUMMARY CARD (atas, full width, gradient)
- Judul: "Pengeluaran Bulan Ini"
- Nominal total besar: Rp X.XXX.XXX
- Progress bar: total vs budget bulanan
  → hijau jika < 75%, kuning jika 75–99%, merah jika ≥ 100%
- Sub-teks: "Sisa budget: Rp X.XXX.XXX" atau "Melebihi budget!"
- Selector bulan/tahun (prev/next arrow) untuk lihat bulan lain

SUMBER PENGELUARAN (row horizontal scroll)
- 6 kartu kecil per sumber (Cash, M-Banking, DANA, GoPay, OVO, Lainnya)
- Setiap kartu: ikon, label, total nominal bulan ini
- Highlight sumber terbesar dengan border warna aksen

TRANSAKSI TERBARU
- Heading "Transaksi Terbaru" + link "Lihat Semua →" (ke tab Laporan)
- Tampilkan 5 transaksi terakhir
- Setiap baris:
  - Kiri: ikon kategori + nama kategori + note (truncate 20 char)
  - Tengah: badge sumber (warna per sumber)
  - Kanan: nominal merah + tanggal kecil
- Jika belum ada data → ilustrasi kosong:
  "Belum ada pengeluaran. Yuk catat sekarang! ➕"

═══════════════════════════════════════
TAB 2 — TAMBAH PENGELUARAN
═══════════════════════════════════════
FORM (card putih, shadow)

Nominal (input utama, paling atas):
- Input angka besar (font 2rem, bold, center)
- Prefix "Rp" di kiri
- Format otomatis dengan titik ribuan saat mengetik
- Placeholder: "0"

Tanggal:
- Input date, default hari ini
- Tampil sebagai: "Senin, 3 Juni 2025"

Kategori:
- Grid 4×2 tombol pill dengan ikon + label
- Satu pilihan aktif, highlight border + background aksen
- Wajib dipilih

Sumber Pembayaran:
- Grid 3×2 kartu dengan ikon + label + warna per sumber
- Satu pilihan aktif, highlight border + background sesuai warna sumber
- Wajib dipilih

Catatan (opsional):
- Textarea max 100 karakter
- Counter karakter di pojok kanan bawah

Tombol SIMPAN:
- Full width, warna aksen, disabled jika nominal = 0
- Efek loading 500ms → success state → reset form
- Success: muncul toast "✅ Pengeluaran berhasil dicatat!"

MODE EDIT:
- Saat edit transaksi dari daftar → form terisi data existing
- Tombol berubah jadi "UPDATE" + tombol "Hapus" (merah)
- Konfirmasi hapus: dialog sederhana "Yakin hapus transaksi ini?"

═══════════════════════════════════════
TAB 3 — LAPORAN
═══════════════════════════════════════
FILTER BAR
- Selector periode: [Minggu Ini | Bulan Ini | 3 Bulan | Custom]
- Jika Custom: muncul input date range (dari–sampai)
- Filter sumber: dropdown multi-pilih (default: Semua)
- Filter kategori: dropdown multi-pilih (default: Semua)

RINGKASAN ANGKA (3 kartu row)
- Total Pengeluaran
- Rata-rata per hari
- Transaksi terbanyak (nominal terbesar)

GRAFIK 1 — Pengeluaran Harian (Chart.js)
- Bar chart: sumbu X = tanggal, sumbu Y = total per hari
- Warna bar: warna aksen
- Tooltip: "Rp X.XXX.XXX — N transaksi"

GRAFIK 2 — Per Kategori (Chart.js)
- Doughnut chart
- Legend di bawah: label + persentase + nominal
- Klik slice → filter daftar transaksi by kategori tsb

GRAFIK 3 — Per Sumber (Chart.js)
- Horizontal bar chart
- Warna bar sesuai warna sumber
- Tampilkan nominal + persentase di ujung bar

DAFTAR TRANSAKSI (di bawah grafik)
- Grouped by tanggal (header tanggal + total hari itu)
- Setiap item: ikon kategori | nama + note | badge sumber | nominal | 
  tombol ✏️ edit → pindah ke Tab 2 mode edit
- Infinite scroll ATAU load more button (tambah 20 per klik)
- Jika filter tidak ada hasil → tampilkan pesan kosong

EXPORT:
- Tombol "Export CSV" → download file expenses_[bulan]_[tahun].csv
- Kolom CSV: Tanggal, Kategori, Sumber, Catatan, Nominal

═══════════════════════════════════════
TAB 4 — PENGATURAN
═══════════════════════════════════════
BUDGET BULANAN
- Input nominal budget per bulan
- Tombol Simpan → update localStorage "budget_data"
- Tampilkan budget aktif saat ini

RINGKASAN DATA
- Total transaksi tersimpan
- Transaksi tertua (tanggal mulai mencatat)
- Ukuran data (KB) di localStorage

KELOLA DATA
- Tombol "Export Semua Data (JSON)" → download backup lengkap
- Tombol "Import Data (JSON)" → upload file backup → merge atau replace
- Tombol "Hapus Semua Data" → konfirmasi 2 langkah:
  Step 1: dialog "Yakin? Semua data akan dihapus permanen"
  Step 2: ketik "HAPUS" untuk konfirmasi → baru eksekusi

PREFERENSI TAMPILAN
- Toggle dark mode (simpan ke localStorage "theme")
- Dark mode: ubah semua CSS variable ke palet gelap

═══════════════════════════════════════
DARK MODE PALETTE
═══════════════════════════════════════
--bg-primary:   #0F172A
--bg-card:      #1E293B
--bg-nav:       #1E293B
--text-primary: #F1F5F9
--text-muted:   #94A3B8
--border:       #334155

═══════════════════════════════════════
STYLE GUIDE (LIGHT MODE)
═══════════════════════════════════════
--color-primary:  #6366F1   /* indigo */
--color-success:  #10B981   /* hijau */
--color-warning:  #F59E0B   /* kuning */
--color-danger:   #EF4444   /* merah */
--color-bg:       #F8FAFC
--color-card:     #FFFFFF
--color-text:     #0F172A
--color-muted:    #64748B
--color-border:   #E2E8F0

--radius-card: 16px
--shadow-card: 0 2px 12px rgba(0,0,0,0.06)

--font-heading: 'Plus Jakarta Sans', sans-serif
--font-body:    'Plus Jakarta Sans', sans-serif
(satu font family, variasi weight 400/500/600/700)

Max width: 480px, centered. Pure mobile-first.

═══════════════════════════════════════
UTILITY FUNCTIONS (wajib ada)
═══════════════════════════════════════
formatRupiah(number)   → "Rp 1.250.000"
parseRupiah(string)    → 1250000
formatDate(dateStr)    → "Senin, 3 Juni 2025"
getMonthName(month)    → "Juni"
generateId()           → Date.now().toString()
saveData(data)         → localStorage.setItem(...)
loadData()             → JSON.parse(localStorage.getItem(...)) || []
filterByPeriod(data, period, from, to) → filtered array
groupByDate(data)      → { "2025-06-03": [...], ... }

═══════════════════════════════════════
ACCEPTANCE CRITERIA
═══════════════════════════════════════
[ ] Tambah transaksi → muncul di Beranda & Laporan realtime
[ ] Format Rp otomatis saat input (1000000 → "1.000.000")
[ ] Progress bar budget berubah warna sesuai persentase
[ ] 6 sumber tampil dengan warna & ikon masing-masing
[ ] Chart.js render 3 grafik dengan data aktual
[ ] Filter laporan (periode + sumber + kategori) bekerja bersamaan
[ ] Edit & hapus transaksi berfungsi + data terupdate di semua tab
[ ] Export CSV menghasilkan file yang bisa dibuka di Excel
[ ] Dark mode toggle berfungsi + tersimpan saat refresh
[ ] Semua data persist setelah browser di-refresh (localStorage)
[ ] Tampilan rapi di 375px (iPhone SE)
