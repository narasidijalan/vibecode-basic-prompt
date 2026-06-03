STACK: HTML + CSS + Vanilla JS. Single file. No framework. No CDN kecuali Chart.js.

TASK: Kalkulator Angsuran Kendaraan

INPUTS:
- harga_otр: number (Rp)
- dp: number + toggle [Rp|%], sinkron dua arah realtime
- tenor: select [12,24,36,48,60] bulan
- bunga_pa: number (% per tahun)
- metode: radio [Flat | Anuitas/Efektif]

OUTPUTS (update onInput, tanpa tombol hitung):
- pokok_pinjaman = harga - dp_nominal
- cicilan_bulanan → tampil besar, font 2rem, bold
- total_bunga, total_bayar
- tabel_amortisasi: toggle show/hide, kolom: No | Sisa Pokok | Bunga | Cicilan

FORMULA:
- Flat: cicilan = (pokok/tenor) + (pokok × bunga_pa/12)
- Anuitas: cicilan = PMT = P × [i(1+i)^n] / [(1+i)^n - 1]
  dimana i = bunga_pa/12, n = tenor

VALIDASI:
- Semua field required, tidak boleh ≤ 0
- DP tidak boleh ≥ harga kendaraan
- Tampilkan inline error jika invalid

ACCEPTANCE CRITERIA:
- Hasil cicilan identik dengan fungsi PMT() di Excel/Google Sheets
- Baris terakhir tabel amortisasi: sisa pokok = 0 (±Rp1 toleransi pembulatan)
- Tombol Reset mengosongkan semua field dan output

STYLE: Minimal, bersih. Warna aksen: #10b981 (emerald). Mobile responsive.
