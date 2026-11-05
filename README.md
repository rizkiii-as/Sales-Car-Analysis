# 🚗 Sales Car Analysis

Analisis data penjualan mobil dari jaringan showroom di 10 kota di Indonesia sepanjang tahun 2025, menggunakan Python (Pandas, Matplotlib, dan Seaborn) di Jupyter Notebook.

Proyek ini mencakup seluruh alur analisis data: **import data → data cleansing → data transformation → sorting/filtering/grouping → exploratory data analysis (EDA) → visualisasi**.

---

## 📌 Daftar Isi

- [Tujuan Proyek](#-tujuan-proyek)
- [Dataset](#-dataset)
- [Tahapan Analisis](#-tahapan-analisis)
- [Hasil Analisis](#-hasil-analisis)
- [Teknologi yang Digunakan](#-teknologi-yang-digunakan)
- [Struktur Repositori](#-struktur-repositori)
- [Cara Menjalankan](#-cara-menjalankan)

---

## 🎯 Tujuan Proyek

Proyek ini menjawab 10 pertanyaan bisnis berikut:

1. Cabang mana yang penjualannya (pendapatan) paling tinggi?
2. Kategori mobil apa yang paling laku (berdasarkan jumlah unit terjual)?
3. Berapa persen transaksi yang berhasil (*completed*) vs *cancelled* vs *refund*?
4. Metode pembayaran apa yang paling sering dipakai?
5. Bagaimana tren jumlah transaksi per bulan?
6. Lima mobil dengan harga tertinggi, beserta cabang dan kategorinya.
7. Berapa rata-rata diskon per cabang?
8. Bagaimana perbandingan harga rata-rata per kategori mobil (dalam bentuk grafik)?
9. Cabang dan kategori mobil apa yang menghasilkan pendapatan terbesar?
10. Berapa rata-rata harga per unit (`price`) untuk masing-masing kombinasi cabang dan kategori?

---

## 📊 Dataset

**File:** `showroom_mobil.csv`
**Jumlah data:** 10.000 transaksi × 16 kolom
**Periode:** 1 Januari 2025 – 31 Desember 2025

| Kolom | Deskripsi |
|---|---|
| `sales_date` | Tanggal transaksi |
| `order_id` | ID transaksi unik (`TRX00001`, dst.) |
| `customer_name` | Nama/ID pelanggan |
| `branch` | Cabang showroom (10 cabang) |
| `product_name` | Nama dan varian mobil (20 produk) |
| `category` | Kategori mobil: SUV, MPV, Hatchback, Pickup, City Car (EV) |
| `color` | Warna mobil |
| `price` | Harga per unit (Rupiah) |
| `quantity` | Jumlah unit dalam transaksi (1–3) |
| `payment_type` | Metode pembayaran: Cash, Cash + Trade In, Kredit, Kredit + Trade In |
| `trade_in` | Nilai tukar tambah (Rupiah) |
| `discount` | Diskon (Rupiah) |
| `total` | Total harga sebelum trade-in dan diskon (`price × quantity`) |
| `total_sales` | Nilai penjualan akhir (`total − trade_in − discount`) |
| `status` | Status transaksi: `completed`, `cancelled`, `refund` |
| `branch_address` | Alamat cabang |

**Cabang:** Bandung, Batam, Jakarta, Karawang, Kendari, Malang, Padang, Palembang, Pontianak, Semarang.

---

## 🔧 Tahapan Analisis

### 1. Import & Inspeksi Data
Memuat data dengan Pandas, lalu memeriksa struktur data menggunakan `head()`, `tail()`, `shape`, `info()`, `describe()`, `columns`, dan `dtypes`.

### 2. Data Cleansing
- Mengecek *missing values* → **tidak ditemukan data kosong**.
- Mengecek duplikasi data (termasuk berdasarkan `order_id`) → **tidak ada data duplikat**.
- Mengubah tipe data `sales_date` menjadi `datetime`.
- Mengecek nilai unik pada kolom `branch` dan `payment_type`.
- Standardisasi teks: menghapus spasi berlebih dan menyeragamkan huruf pada kolom `branch` (*title case*) dan `category` (*uppercase*).

### 3. Data Transformation
- Memecah `sales_date` menjadi kolom `sales_month`, `sales_year`, dan `sales_month_name`.
- Mengganti nama kolom `total` menjadi `total_sales_before_trade_in`.
- *Binning* harga menjadi kolom `segmen_harga`:
  - **Murah**: harga < Rp250 juta
  - **Menengah**: Rp250 juta – Rp400 juta
  - **Mahal**: harga > Rp400 juta

### 4. Sorting, Filtering, dan Grouping
- Filter transaksi berstatus `completed`.
- Filter transaksi cabang Jakarta kategori SUV.
- Filter transaksi `completed` kategori SUV.
- Sorting `total_sales` dari yang terbesar.
- Grouping total dan rata-rata `total_sales` per cabang, serta rata-rata harga per kategori.

### 5. Exploratory Data Analysis & Visualisasi
Menjawab 10 pertanyaan bisnis di atas, disertai grafik (bar chart, pie chart, line chart, dan horizontal bar chart).

---

## 💡 Hasil Analisis

> Perhitungan pendapatan dan unit terjual hanya memakai transaksi berstatus `completed`.

### 1. Cabang dengan pendapatan tertinggi

| Peringkat | Cabang | Total Pendapatan |
|:-:|---|--:|
| 1 | **Malang** | Rp291,6 miliar |
| 2 | Padang | Rp285,9 miliar |
| 3 | Jakarta | Rp283,7 miliar |
| 4 | Bandung | Rp278,6 miliar |
| 5 | Batam | Rp278,1 miliar |

Selisih antarcabang relatif tipis (cabang terendah, Karawang, mencatat Rp264,3 miliar).

### 2. Kategori mobil terlaris (unit terjual)

| Kategori | Unit Terjual |
|---|--:|
| **SUV** | 4.273 |
| MPV | 3.658 |
| Hatchback | 489 |
| Pickup | 466 |
| City Car (EV) | 456 |

SUV dan MPV mendominasi penjualan dengan total lebih dari 85% unit terjual.

### 3. Distribusi status transaksi

| Status | Persentase |
|---|--:|
| Completed | 89,7% |
| Cancelled | 5,4% |
| Refund | 4,9% |

### 4. Metode pembayaran

| Metode | Jumlah Transaksi |
|---|--:|
| **Kredit** | 4.253 |
| Cash | 2.224 |
| Kredit + Trade In | 1.999 |
| Cash + Trade In | 1.524 |

### 5. Tren transaksi bulanan
Jumlah transaksi relatif stabil sepanjang tahun, berkisar antara 767 hingga 877 transaksi per bulan. Puncak tertinggi terjadi pada **Agustus (877)** dan **Juli (875)**, sedangkan yang terendah pada **Februari dan Juni (masing-masing 767)**.

### 6. Lima mobil dengan harga tertinggi
Mobil termahal adalah **Honda CR-V 1.5 Turbo RS** (kategori SUV) dengan harga **Rp650 juta**. Karena harga produk sama di semua cabang, mobil ini muncul di banyak cabang (misalnya Jakarta, Bandung, Batam, Palembang, dan Semarang).

### 7. Rata-rata diskon per cabang

| Cabang | Rata-rata Diskon |
|---|--:|
| Malang | Rp38.314 |
| Semarang | Rp35.160 |
| Palembang | Rp34.659 |
| ... | ... |
| Bandung | Rp27.300 |
| Karawang | Rp24.666 |

Diskon pada data hanya bernilai Rp0 atau Rp1.000.000, dan hanya sekitar 3% transaksi yang mendapat diskon, sehingga rata-ratanya terlihat kecil.

### 8. Rata-rata harga per kategori

| Kategori | Rata-rata Harga |
|---|--:|
| Pickup | Rp520 juta |
| SUV | Rp408,6 juta |
| MPV | Rp298 juta |
| City Car (EV) | Rp250 juta |
| Hatchback | Rp190 juta |

### 9. Kombinasi cabang & kategori dengan pendapatan terbesar

| Peringkat | Cabang – Kategori | Total Pendapatan |
|:-:|---|--:|
| 1 | **Palembang – SUV** | Rp157,6 miliar |
| 2 | Jakarta – SUV | Rp155,7 miliar |
| 3 | Malang – SUV | Rp154,9 miliar |
| 4 | Batam – SUV | Rp152,0 miliar |
| 5 | Karawang – SUV | Rp150,5 miliar |

Seluruh lima besar didominasi kategori **SUV**.

### 10. Rata-rata harga per unit untuk kombinasi cabang & kategori teratas

| Cabang – Kategori | Rata-rata Harga |
|---|--:|
| Batam – SUV | Rp414,0 juta |
| Malang – SUV | Rp413,97 juta |
| Palembang – SUV | Rp412,96 juta |
| Jakarta – SUV | Rp407,8 juta |
| Karawang – SUV | Rp398,3 juta |

### 🔎 Kesimpulan Singkat
- Penjualan **merata** antarcabang; Malang unggul tipis sebagai cabang dengan pendapatan tertinggi.
- **SUV** adalah kategori dengan unit terjual dan pendapatan terbesar.
- Mayoritas konsumen memilih pembayaran **kredit**.
- Sekitar **10% transaksi** berakhir *cancelled* atau *refund*, sehingga berpotensi ditelusuri lebih lanjut penyebabnya.

---

## 🛠 Teknologi yang Digunakan

- **Python 3**
- **Pandas** – manipulasi dan analisis data
- **NumPy** – komputasi numerik
- **Matplotlib** – visualisasi data
- **Seaborn** – visualisasi data
- **Jupyter Notebook** – lingkungan analisis

---

## 📁 Struktur Repositori

```
.
├── sales_car_analysis.ipynb   # Notebook analisis utama
├── showroom_mobil.csv         # Dataset penjualan showroom mobil
└── README.md                  # Dokumentasi proyek
```

---

## ▶️ Cara Menjalankan

1. **Clone repositori**
   ```bash
   git clone https://github.com/<username>/<nama-repositori>.git
   cd <nama-repositori>
   ```

2. **Instal dependensi**
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```

3. **Jalankan Jupyter Notebook**
   ```bash
   jupyter notebook sales_car_analysis.ipynb
   ```

4. Pastikan file `showroom_mobil.csv` berada di folder yang sama dengan notebook, lalu jalankan seluruh sel (*Run All*).

---

## 👤 Penulis

Dibuat oleh **<Nama Anda>**
GitHub: [@<username>](https://github.com/<username>)

---

⭐ Jika proyek ini bermanfaat, jangan lupa beri bintang pada repositori ini!
