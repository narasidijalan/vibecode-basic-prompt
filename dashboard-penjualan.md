STACK: HTML + CSS + Vanilla JS. Single file. No framework.
CDN allowed: Google Fonts, Chart.js, Font Awesome 6, AOS.js.

TASK: Business Dashboard — Real-time data dari Google Sheets publik.
      No backend. No login. Single file HTML.

═══════════════════════════════════════
CARA KERJA FETCH DATA
═══════════════════════════════════════
Google Sheet publik di-export sebagai CSV per sheet/tab:
URL format:
https://docs.google.com/spreadsheets/d/{SHEET_ID}/gviz/tq?tqx=out:csv&sheet={SHEET_NAME}

const CONFIG = {
  SHEET_ID: "GANTI_DENGAN_SHEET_ID_KAMU",
  REFRESH_INTERVAL: 60000, // auto-refresh tiap 60 detik

  SHEETS: {
    penjualan:  "Penjualan",
    pengeluaran:"Pengeluaran",
    stok:       "Stok",
    leads:      "Leads",
    target:     "Target",
  }
}

FETCH LOGIC:
async function fetchSheet(sheetName) {
  const url = `https://docs.google.com/spreadsheets/d/${CONFIG.SHEET_ID}
               /gviz/tq?tqx=out:csv&sheet=${sheetName}`
  const res  = await fetch(url)
  const text = await res.text()
  return parseCSV(text) // → array of objects, header row sebagai key
}

parseCSV(text):
- Split by newline → rows
- Baris pertama → headers (trim + lowercase + replace spasi dengan _)
- Baris berikutnya → array of { header: value, ... }
- Handle nilai dalam tanda kutip (CSV standard)
- Return array of objects

Saat load:
- Fetch semua sheet paralel: Promise.all([...])
- Tampilkan skeleton loader selama fetch
- Jika fetch gagal → tampilkan banner error + tombol "Coba Lagi"
- Jika SHEET_ID masih placeholder → tampilkan panduan setup

═══════════════════════════════════════
STRUKTUR GOOGLE SHEET (dokumentasikan
sebagai komentar di dalam HTML)
═══════════════════════════════════════

Tab "Penjualan" — kolom wajib:
  tanggal | produk | kategori | qty | harga_satuan | total | sumber

Tab "Pengeluaran" — kolom wajib:
  tanggal | keterangan | kategori | nominal | metode_bayar

Tab "Stok" — kolom wajib:
  kode_produk | nama_produk | kategori | stok_awal | masuk | keluar | stok_akhir | minimum_stok

Tab "Leads" — kolom wajib:
  tanggal | nama | sumber | status | nilai_potensi | catatan
  (status: Baru / Follow-up / Closing / Batal)

Tab "Target" — kolom wajib:
  bulan | target_omzet | target_leads | target_closing

═══════════════════════════════════════
LAYOUT — SIDEBAR + MAIN CONTENT
═══════════════════════════════════════
Desktop: sidebar kiri fixed 240px + main content scrollable
Mobile:  sidebar hidden → hamburger toggle → overlay drawer

SIDEBAR:
- Logo + nama bisnis (hardcode: bisa diedit)
- Menu navigasi:
  🏠 Overview
  💰 Penjualan
  💸 Pengeluaran
  📦 Stok
  👥 Leads
  🎯 Target
- Divider
- 🔄 Refresh Data (manual) + timestamp "Terakhir diperbarui: HH:MM"
- Auto-refresh countdown kecil (misal "Refresh dalam 45 detik")
- Di bawah sidebar: indikator status koneksi Sheet (● Online / ● Error)

TOPBAR (main area):
- Nama halaman aktif
- Selector periode: [Hari Ini | Minggu Ini | Bulan Ini | Tahun Ini | Custom]
  → Custom: date range picker (dari–sampai)
- Chip filter periode tampil aktif dengan highlight

═══════════════════════════════════════
PAGE 1 — OVERVIEW
═══════════════════════════════════════
KPI CARDS ROW (4 kartu, responsive grid)
Hitung dari data sesuai periode aktif:
  💰 Total Omzet       → sum(penjualan.total)
  💸 Total Pengeluaran → sum(pengeluaran.nominal)
  📈 Laba Kotor        → omzet - pengeluaran (warna: hijau/merah)
  👥 Leads Baru        → count(leads) periode ini

Setiap kartu:
- Nominal besar
- Perbandingan vs periode sebelumnya: "▲ 12% vs bulan lalu"
  (hijau jika naik untuk omzet/laba/leads, merah jika omzet turun)
- Ikon + warna aksen per kartu

GRAFIK 1 — Tren Omzet vs Pengeluaran (Chart.js)
- Line chart dual axis
- Sumbu X: tanggal/bulan sesuai periode
- Line 1: Omzet (biru)
- Line 2: Pengeluaran (merah)
- Tooltip: tampilkan kedua nilai + selisih (laba)

GRAFIK 2 — Omzet per Kategori Produk (Chart.js)
- Doughnut chart
- Legend: label + % + nominal
- Klik slice → filter tabel penjualan

TABEL TRANSAKSI TERBARU
- 10 transaksi penjualan terakhir
- Kolom: Tanggal | Produk | Qty | Harga | Total | Sumber
- Link "Lihat Semua" → pindah ke halaman Penjualan

═══════════════════════════════════════
PAGE 2 — PENJUALAN
═══════════════════════════════════════
KPI ROW (3 kartu):
- Total Omzet periode
- Total Transaksi (count)
- Rata-rata per Transaksi

GRAFIK — Bar chart omzet per hari/minggu (sesuai periode)

FILTER: search produk + filter kategori + filter sumber

TABEL LENGKAP:
- Semua kolom sheet Penjualan
- Sortable per kolom (klik header)
- Pagination 15 baris per halaman
- Baris total di footer tabel

EXPORT: tombol "Export CSV" → download data terfilter

═══════════════════════════════════════
PAGE 3 — PENGELUARAN
═══════════════════════════════════════
KPI ROW (3 kartu):
- Total Pengeluaran periode
- Pengeluaran Terbesar (1 item)
- Jumlah Transaksi

GRAFIK 1 — Doughnut per kategori pengeluaran
GRAFIK 2 — Bar chart pengeluaran per hari

FILTER: search keterangan + filter kategori + filter metode bayar

TABEL LENGKAP:
- Semua kolom sheet Pengeluaran
- Sortable, pagination 15 baris
- Baris total di footer

EXPORT CSV

═══════════════════════════════════════
PAGE 4 — STOK
═══════════════════════════════════════
KPI ROW (4 kartu):
- Total SKU (jumlah produk unik)
- Stok Kritis (stok_akhir ≤ minimum_stok) → warna merah
- Total Nilai Stok (stok_akhir × harga — jika ada kolom harga)
- Produk Habis (stok_akhir = 0) → warna merah

ALERT BANNER (jika ada stok kritis):
"⚠️ X produk mendekati stok minimum. Segera lakukan reorder."
→ list nama produk kritis

TABEL STOK:
- Semua kolom sheet Stok
- Baris highlight merah jika stok_akhir ≤ minimum_stok
- Baris highlight kuning jika stok_akhir ≤ minimum_stok × 2
- Badge status: [Normal] [Kritis] [Habis]
- Sortable + search by nama/kode produk
- Pagination 15 baris

GRAFIK — Horizontal bar chart top 10 produk by stok_akhir

═══════════════════════════════════════
PAGE 5 — LEADS
═══════════════════════════════════════
KPI ROW (4 kartu):
- Total Leads periode
- Leads Closing (status = "Closing")
- Conversion Rate (closing / total × 100%)
- Nilai Potensi Total (sum nilai_potensi)

GRAFIK 1 — Funnel / Bar chart per status
  Baru → Follow-up → Closing (Batal terpisah)

GRAFIK 2 — Leads per sumber (doughnut)

FILTER: search nama + filter status + filter sumber

TABEL LENGKAP:
- Semua kolom sheet Leads
- Badge berwarna per status:
  Baru      → biru
  Follow-up → kuning
  Closing   → hijau
  Batal     → merah
- Sortable + pagination 15 baris

═══════════════════════════════════════
PAGE 6 — TARGET vs REALISASI
═══════════════════════════════════════
SELECTOR BULAN — pill button per bulan tahun ini

PER BULAN YANG DIPILIH:

Progress Cards (2 kartu):
- Target Omzet vs Realisasi Omzet
  → progress bar + persentase pencapaian
  → status: [Tercapai ✅ | Dalam Jalur 🟡 | Di Bawah Target 🔴]
- Target Leads vs Realisasi Leads
  → same format

GRAFIK — Grouped bar chart semua bulan:
  Bar 1: Target Omzet (outline/transparan)
  Bar 2: Realisasi Omzet (solid)
  Tooltip: target, realisasi, gap, persentase

TABEL RINGKASAN TAHUNAN:
Kolom: Bulan | Target Omzet | Realisasi | Gap | % Pencapaian | Status
- Baris highlight hijau jika tercapai
- Baris highlight merah jika < 80%
- Footer: total target vs total realisasi tahunan

═══════════════════════════════════════
SETUP GUIDE (tampil jika SHEET_ID = placeholder)
═══════════════════════════════════════
Tampilkan modal/overlay panduan langkah:

Step 1: Buat Google Sheet baru
Step 2: Buat 5 tab: Penjualan, Pengeluaran, Stok, Leads, Target
Step 3: Isi header sesuai struktur di atas
Step 4: Klik Share → Anyone with the link → Viewer
Step 5: Copy Sheet ID dari URL:
        docs.google.com/spreadsheets/d/[INI SHEET ID KAMU]/edit
Step 6: Ganti nilai SHEET_ID di baris CONFIG dalam file HTML ini
Step 7: Simpan & buka ulang

Sertakan tombol "Tes Koneksi" → fetch sheet pertama → 
tampilkan ✅ Berhasil atau ❌ Gagal + pesan error spesifik

═══════════════════════════════════════
FITUR TAMBAHAN
═══════════════════════════════════════
AUTO REFRESH:
- setInterval fetch ulang semua data tiap CONFIG.REFRESH_INTERVAL
- Tampilkan animasi spin ikon refresh saat fetching
- Update timestamp "Terakhir diperbarui"
- Jangan reset filter/halaman aktif saat refresh

SKELETON LOADER:
- Saat fetch, tampilkan skeleton (abu animasi pulse) 
  di posisi kartu dan grafik
- Setelah data masuk → replace dengan konten asli

ERROR HANDLING:
- Fetch gagal → banner merah "Gagal memuat data. Periksa koneksi 
  atau pastikan Sheet sudah dipublikasikan."
- Tombol retry manual
- Data terakhir tetap tampil (cache di memori) dengan badge 
  "Data mungkin tidak terkini"

DARK MODE:
- Toggle di sidebar bawah
- Simpan preferensi ke localStorage
- Chart.js warna menyesuaikan dark mode

═══════════════════════════════════════
STYLE GUIDE
═══════════════════════════════════════
--color-primary:    #6366F1   /* indigo */
--color-success:    #10B981   /* hijau */
--color-warning:    #F59E0B   /* kuning */
--color-danger:     #EF4444   /* merah */
--color-info:       #3B82F6   /* biru */
--color-bg:         #F1F5F9
--color-sidebar:    #1E293B
--color-card:       #FFFFFF
--color-text:       #0F172A
--color-muted:      #64748B
--color-border:     #E2E8F0

DARK MODE:
--color-bg:         #0F172A
--color-sidebar:    #020617
--color-card:       #1E293B
--color-text:       #F1F5F9
--color-border:     #334155

--radius-card: 12px
--shadow-card: 0 1px 3px rgba(0,0,0,0.08), 0 4px 16px rgba(0,0,0,0.04)

--font: 'Plus Jakarta Sans', sans-serif (Google Fonts)
Weights: 400 / 500 / 600 / 700

Breakpoints:
- Mobile:  < 768px  → sidebar drawer
- Tablet:  768–1024px → sidebar collapsed (icon only)
- Desktop: > 1024px → sidebar full

═══════════════════════════════════════
ACCEPTANCE CRITERIA
═══════════════════════════════════════
[ ] Jika SHEET_ID placeholder → tampilkan setup guide, bukan error
[ ] Fetch semua 5 sheet paralel saat load
[ ] Skeleton loader tampil saat fetching
[ ] Filter periode (Hari Ini/Minggu/Bulan/Tahun/Custom) 
    mempengaruhi SEMUA angka dan grafik di halaman aktif
[ ] Auto-refresh tiap 60 detik tanpa reset state
[ ] Stok kritis (≤ minimum) highlight merah + alert banner
[ ] Target vs Realisasi menghitung dari data sheet aktual
[ ] Export CSV berfungsi di setiap halaman
[ ] Dark mode toggle + persist localStorage
[ ] Responsive: sidebar drawer di mobile, icon-only di tablet
[ ] Tombol "Tes Koneksi" di setup guide berfungsi
[ ] Error fetch → tampilkan pesan + data cache tetap terbaca
