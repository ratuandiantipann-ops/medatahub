# MeDataHub – Deteksi Duplikat Data Pasien

Website untuk mendeteksi data pasien yang terduplikasi atau tercatat tidak konsisten, menggunakan kombinasi **Levenshtein Distance** dan **Jaro-Winkler Similarity**. Semua proses berjalan langsung di browser (client-side), sehingga **tidak ada data yang dikirim ke server**.

🔗 **Coba website:** https://ratuandiantipann-ops.github.io/medatahub/

> Final Project Manajemen Data – Kelompok 9

## Latar Belakang
Duplikasi data pasien sering terjadi akibat ketidakkonsistenan identitas dan kesalahan input. Hal ini berdampak pada pelayanan kesehatan, keselamatan pasien, dan proses klaim BPJS. MeDataHub membantu petugas rekam medis menemukan record yang diduga duplikat secara otomatis sebelum data disimpan permanen di Rekam Medis Elektronik (RME).

## Fitur
- Upload file CSV data pasien dengan validasi kolom wajib
- Normalisasi data (nama, alamat, format tanggal lahir)
- Perhitungan skor kemiripan berbobot antar-record
- Threshold yang dapat diatur
- Tabel hasil dugaan duplikat dengan penanda tingkat kemiripan
- Export laporan duplikat ke CSV
- Generator data pasien sintetis untuk uji coba

## Cara Menggunakan
1. Buka website melalui link di atas.
2. Upload file CSV data pasien, atau klik **"Buat Data Contoh"** untuk mencoba dengan data sintetis.
3. Atur threshold skor duplikat sesuai kebutuhan (default 70).
4. Periksa tabel **Hasil Deteksi Duplikat**.
5. Klik **"Download Laporan Duplikat (CSV)"** untuk menyimpan hasilnya.

## Format CSV
File CSV harus memiliki kolom berikut (baris pertama sebagai header):

| Kolom | Keterangan | Contoh |
|---|---|---|
| `id_record` | ID unik record | 101 |
| `nama` | Nama lengkap pasien | Siti Rahimah |
| `tgl_lahir` | Tanggal lahir (YYYY-MM-DD atau DD/MM/YYYY) | 1985-07-14 |
| `nik` | Nomor Induk Kependudukan | 3578xxxxxxxxxxxx |
| `alamat` | Alamat pasien | Jl. Mawar No. 12, Surabaya |

## Cara Kerja Skor
| Atribut | Metode | Bobot |
|---|---|---|
| Nama | Levenshtein similarity | 40% |
| NIK | Exact match | 30% |
| Tanggal lahir | Exact match | 20% |
| Alamat | Jaro-Winkler similarity | 10% |

Skor akhir (0–100) dibandingkan dengan threshold. Skor ≥ 90 ditandai sebagai **duplikat kuat**, di bawahnya **perlu verifikasi manual**. Untuk efisiensi, perbandingan hanya dilakukan antar-record dengan huruf awal nama yang sama (*blocking*).

## Teknologi
- HTML, CSS, JavaScript
- [PapaParse](https://www.papaparse.com/) untuk parsing CSV

## Privasi Data
Seluruh pemrosesan dilakukan di browser pengguna. Data yang diunggah tidak disimpan maupun dikirim ke server. Dataset di repository ini adalah **data sintetis** dan bukan data pasien asli.

## Lisensi
Dirilis di bawah [MIT License](LICENSE).# medatahub
Website deteksi duplikat data pasien (Levenshtein &amp; Jaro-Winkler)
