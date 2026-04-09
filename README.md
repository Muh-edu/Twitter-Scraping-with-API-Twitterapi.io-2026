# 🐦 Twitter Advanced Search Scraper

Scraper tweet otomatis menggunakan [TwitterAPI.io](https://twitterapi.io) dengan fitur **auto-resume**, **checkpoint**, dan **backup berkala**. Cocok untuk riset, analisis data, atau pengumpulan dataset tweet dalam skala besar.

---

## ✨ Fitur Utama

| Fitur | Keterangan |
|---|---|
| 🔄 Auto-Resume | Lanjutkan scraping dari titik terakhir jika terhenti |
| 📍 Checkpoint | Progress disimpan setiap periode selesai |
| 💾 Backup Berkala | Auto-download file CSV setiap 10 periode |
| 📅 Batching per Tanggal | Query dipecah per rentang tanggal untuk menghindari limit |
| 🧹 Deduplication | Data duplikat otomatis dihapus berdasarkan tweet ID |
| 📊 Sorted Output | Hasil diurutkan dari tweet terlama ke terbaru |

---

## 📁 Struktur File

```
twitter-scraper/
├── twitter_scraper.ipynb   # Notebook utama (jalankan di Google Colab)
├── README.md               # Dokumentasi ini
├── tweets_lengkap.csv      # Output hasil scraping (dibuat otomatis)
└── checkpoint_progress.txt # File checkpoint (dibuat otomatis)
```

---

## 🚀 Cara Penggunaan

### 1. Buka di Google Colab
Klik tombol berikut atau upload `twitter_scraper.ipynb` ke [colab.research.google.com](https://colab.research.google.com).

### 2. Isi Konfigurasi

Di bagian **Cell 1 – Konfigurasi**, isi variabel berikut:

```python
API_KEY        = "your_api_key_here"   # API Key dari twitterapi.io
START_DATE     = "2024-01-01"          # Tanggal mulai (format YYYY-MM-DD)
END_DATE       = "2024-03-01"          # Tanggal akhir (format YYYY-MM-DD)
DAYS_PER_BATCH = 7                     # Jumlah hari per batch query
LIMIT_PER_PERIOD = 10000               # Batas tweet per periode
BASE_QUERY     = 'kata_kunci lang:id'  # Query pencarian Twitter
```

### 3. Jalankan Semua Cell
Pilih **Runtime → Run all** atau jalankan cell satu per satu dari atas ke bawah.

---

## 🔑 Mendapatkan API Key

1. Daftar di [twitterapi.io](https://twitterapi.io)
2. Masuk ke dashboard → **API Keys**
3. Salin API Key Anda dan tempel di variabel `API_KEY`

---

## 📝 Contoh Query

```python
# Contoh: Mencari tweet tentang produk tertentu dalam Bahasa Indonesia
BASE_QUERY = '("nama produk" OR "review produk" OR #NamaProduk) lang:id'

# Contoh: Mencari tweet dari akun tertentu
BASE_QUERY = 'from:username lang:id'

# Contoh: Mencari tweet dengan hashtag tertentu
BASE_QUERY = '#HashtagKamu lang:id'
```

> 📖 Lihat [dokumentasi query Twitter](https://developer.twitter.com/en/docs/twitter-api/tweets/search/integrate/build-a-query) untuk sintaks lengkap.

---

## 📤 Output

File CSV (`tweets_lengkap.csv`) dipisahkan dengan `;` (semicolon) dan berisi kolom-kolom dari respons API, termasuk:

| Kolom | Keterangan |
|---|---|
| `id` | ID unik tweet |
| `text` | Isi teks tweet |
| `created_at` | Waktu posting tweet |
| `author_id` | ID akun pembuat tweet |
| *(dan kolom lain dari API)* | Tergantung respons API |

---

## ♻️ Resume Scraping yang Terhenti

Jika scraping terhenti (koneksi putus, sesi Colab timeout, dll.):

1. **Pastikan file checkpoint masih ada** di sidebar Colab (`checkpoint_progress.txt`)
2. **Jalankan ulang script** — scraper akan otomatis lanjut dari periode terakhir
3. File CSV lama akan digabungkan dengan data baru, duplikat dihapus otomatis

```
🔄 RESUME dari periode 15
```

---

## ⚠️ Catatan Penting

- Gunakan API Key dengan **bijak** — setiap request mengurangi kuota Anda
- Google Colab **bisa timeout** setelah beberapa jam; gunakan fitur resume untuk melanjutkan
- Jangan simpan API Key langsung di file yang di-push ke GitHub publik
- File CSV bisa diunduh manual dari sidebar Files di Colab kapan saja

---

## 🛠️ Dependensi

Semua library sudah tersedia di Google Colab secara default:

```
requests
pandas
```

---

## 📄 Lisensi

MIT License — bebas digunakan untuk keperluan riset dan non-komersial.

---

> Dibuat untuk kemudahan riset data Twitter/X. Pastikan penggunaan sesuai dengan [Terms of Service Twitter/X](https://twitter.com/en/tos).
