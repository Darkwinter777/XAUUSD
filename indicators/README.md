# XAUUSD Quant Signal (TradingView)

Indikator Pine Script yang menerapkan aturan di `CLAUDE.md`. Semua aturan ada dalam satu indikator, jadi cukup untuk akun TradingView gratis yang membatasi jumlah indikator per chart.

## Yang dikerjakan indikator
- **Tren:** EMA 200. Sinyal counter-trend hanya muncul saat EMA datar (sideways) dan harga menyentuh BB atas/bawah. Sinyal seperti ini ditandai `CT`.
- **Entry:** harga harus sudah koreksi ke BB tengah atau lebih jauh, lalu dikonfirmasi oleh divergence RSI(14) atau rejection candle.
- **Tidak mengejar harga:** tidak ada Sell kalau harga sudah di BB bawah, dan tidak ada Buy kalau harga sudah di BB atas.
- **DXY:** wajib berlawanan arah dengan trade (Sell emas = DXY naik). Filter US10Y bisa dinyalakan di Settings.
- **Risk:**
  - SL = 2 × ATR(14), TP1 = 0.5R, TP2 = 1R, TP3 = 2R.
  - Lot diatur supaya rugi di SL tidak lebih dari $20.
  - Kalau lot 0.01 pun masih membuat rugi lebih dari $20, SL dipersempit menjadi 20 poin, asalkan masih ≥ 1 × ATR. Kalau 20 poin lebih kecil dari 1 × ATR, hasilnya No Trade.
- **Tampilan:** label `SELL` / `BUY` / `No Trade` beserta alasannya, garis Entry/TP/SL untuk sinyal terakhir, dan panel kartu sinyal di kanan atas.

## Cara pasang
1. Buka TradingView, lalu buka chart emas (misalnya `OANDA:XAUUSD`). Harga bisa berbeda sedikit dari XTB.
2. Buka **Pine Editor** di bagian bawah layar.
3. Hapus isi editor, lalu salin-tempel seluruh isi `xauusd_quant_signal.pine`.
4. Klik **Save**, lalu **Add to chart**.
5. Atur input lewat ikon ⚙️ di indikator. Contohnya rugi maksimal (default $20) atau mematikan rejection candle.

## Alert ke HP
1. Klik **Alert** (ikon jam) dan pilih kondisi **XAUUSD Quant Signal**.
2. Pilih **Any alert() function call** supaya pesan alert berisi kartu sinyal lengkap.
3. Centang notifikasi aplikasi TradingView di HP.

Akun gratis membatasi jumlah alert aktif.

## Batasan
- **Tidak repaint, tapi ada delay.** Sinyal hanya dihitung saat candle close. Sinyal divergence muncul 3 candle setelah puncak atau lembah RSI (input "Pivot RSI kanan"), karena pivot baru pasti setelah candle-candle itu close.
- **Cara arah DXY/US10Y ditentukan.** Arahnya dilihat dari posisi close terhadap EMA 20 di timeframe yang sama. Di luar jam pasar DXY, nilai terakhirnya yang dipakai.
- **Bukan jaminan profit.** Uji dulu dengan **Bar Replay** dan akun demo sebelum dipakai dengan uang sungguhan.
