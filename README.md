## QRIS Statis ke QRIS Dinamis (JavaScript)

Aplikasi untuk mengubah QRIS statis menjadi QRIS dinamis langsung di browser (tanpa backend). Unggah gambar QRIS, aplikasi akan decode isi QR, menambahkan nominal (tag 54), menghitung ulang CRC (tag 63), lalu menampilkan string dan QR code baru.

Preview Cek: https://qris.kayyzy.my.id/

### Fitur
- Upload gambar QRIS dan decode di browser (jsQR)
- Parsing EMV; injeksi/replace tag 54 (Amount)
- Hitung ulang CRC-16/CCITT (tag 63)
- Tampilkan string QRIS dinamis, tombol salin, dan preview QR

### Cara Menjalankan
1. Buka `index.html` di browser modern (Chrome/Edge/Firefox).
2. Upload gambar QRIS statis (PNG/JPG).
3. Masukkan nominal (contoh: 1000) → klik "Buat QRIS Dinamis".
4. Salin string hasil atau scan QR yang ditampilkan.

Tidak perlu server atau PHP; semua proses di sisi klien.

### Struktur Singkat
- `index.html` — Halaman utama HTML + JavaScript (klien)
- `style.css` — Gaya opsional untuk UI
- `vendor/` — Sisa dependensi PHP lama (tidak dipakai untuk versi JS)

### Catatan Teknis
- Decoder: jsQR via CDN
- CRC: CRC-16/CCITT-FALSE (poly 0x1021, init 0xFFFF)
- EMV: Susun ulang field mempertahankan urutan asli, lewati tag `63` lama, sisip/replace `54`, lalu hitung `63` baru sebagai `6304` + CRC 4-hex uppercase.
- Amount: ditulis dengan dua desimal, misal `1000.00`.

### Troubleshooting
- "Kode tidak valid": pastikan QR merupakan QRIS/EMV yang valid dan gambar jelas.
- Gagal decode: gunakan gambar `png/jpg` resolusi cukup; coba ulang/scan ulang.
- Masalah lain: kirim contoh string QRIS untuk verifikasi tag/CRC.

### Keamanan
Semua proses terjadi di browser. Preview QR memakai `api.qrserver.com`. Ganti dengan generator lokal jika ingin 100% offline.

### Lisensi
MIT

