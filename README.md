# 📦 Analisis Prioritas Produk BigBasket dengan SQL Magic & Python

> Proyek ini merupakan analisis end-to-end terhadap dataset produk dari BigBasket menggunakan SQL Magic di Jupyter Notebook dan visualisasi Python. Tujuannya adalah membangun **Model Prioritas Produk Multi-Faktor** berbasis `margin` dan `rating` konsumen.

---

## 🛠️ Teknologi yang Digunakan

- 📘 **Jupyter Notebook**
- 🧠 **SQL Magic (`%%sql`)**
- 🗃️ **SQLite (embedded database)**
- 📊 **Pandas, Seaborn, Matplotlib** untuk visualisasi

---

## 📂 Dataset

- **Sumber Dataset:**  
  [BigBasket Entire Product List – Kaggle](https://www.kaggle.com/datasets/surajjha101/bigbasket-entire-product-list-28k-datapoints/data)

- **Nama File:** `BigBasket_Products.csv`
- **Atribut Utama:**  
  `product`, `category`, `brand`, `sale_price`, `market_price`, `rating`, `description`, dll.

---

## 🚀 Alur Analisis

### ✅ Step 1: Setup Lingkungan SQL & Impor Dataset
- Mengaktifkan SQL Magic (`%load_ext sql`)
- Membuat database SQLite (`products.db`)
- Mengimpor file CSV ke dalam tabel `products`

### ✅ Step 2: Exploratory Data Analysis (EDA)
- Menampilkan 5 data teratas
- Menghitung total data, deteksi duplikat berdasarkan `product`
- Menghapus duplikat dan baris dengan data penting kosong
- Menampilkan statistik deskriptif `sale_price`, `market_price`, dan `rating`
- Menyajikan distribusi produk berdasarkan kategori & brand

### ✅ Step 3: Perhitungan Margin & Normalisasi
- Menambahkan kolom `margin = market_price - sale_price`
- Menghitung nilai minimum dan maksimum `margin` dan `rating`
- Membuat **view `normalized_products`** dengan:
  - `norm_margin`: margin yang dinormalisasi ke skala 0–1
  - `norm_rating`: rating yang dinormalisasi ke skala 0–1

### ✅ Step 4: Skor Prioritas Produk
- Menggabungkan `norm_margin` dan `norm_rating` menjadi `priority_score`
  
  ```sql
  priority_score = 0.6 * norm_margin + 0.4 * norm_rating
- Disimpan dalam view scored_products
- Menampilkan produk dengan skor tertinggi

## ✅ Step 5: Analisis Brand, Kategori & Kuadran
- Menghitung rata-rata skor prioritas per kategori dan brand
- Membagi produk menjadi 4 kuadran berdasarkan kombinasi margin dan rating:
| Kuadran | Ciri-ciri                | Strategi                     |
| ------- | ------------------------ | ---------------------------- |
| I       | High Rating, High Margin | Fokus promosi dan distribusi |
| II      | High Rating, Low Margin  | Optimasi harga / bundling    |
| III     | Low Rating, Low Margin   | Pertimbangkan eliminasi      |
| IV      | Low Rating, High Margin  | Evaluasi kualitas produk     |
- Visualisasi scatter plot dengan garis pemisah berdasarkan rata-rata rating & margin

## ✅ Step 6: Visualisasi Lanjutan & Insight
- Bar Chart: Top 10 produk dengan skor tertinggi
- Pie Chart: Distribusi kategori pada Top 20 produk
- Heatmap Korelasi: Hubungan antar variabel numerik
- Insight & Rekomendasi:
  - Produk Kuadran I menjadi prioritas utama
  - Beberapa kategori dominan seperti Beauty & Hygiene mendominasi skor tinggi
  - Produk Kuadran III memiliki risiko bisnis tertinggi

# 📌 Hasil Akhir
Model analisis ini dapat membantu pengambilan keputusan bisnis dalam:
- Strategi promosi produk
- Manajemen stok & suplai berdasarkan profitabilitas
- Identifikasi produk unggulan untuk distribusi massal

# 📝 Catatan Tambahan
Proyek ini dapat dikembangkan lebih lanjut menjadi:
- Dashboard interaktif dengan Streamlit / Dash
- Penambahan data penjualan untuk prediksi permintaan
- Analisis klaster produk

# 👨‍💻 Kontributor
> Danang Hilal Kurniawan
> Data Science Enthusiast | Supply Chain Analytics



