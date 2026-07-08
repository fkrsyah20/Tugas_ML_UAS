# Hierarchical Clustering — Wine Dataset

**Muhammad Fikriansyah — NIM 24260028**
Program Studi Teknik Informatika, Universitas Nahdlatul Ulama Indonesia

---

## 1. Tujuan

Mengelompokkan sampel wine ke dalam beberapa kelompok (cluster) berdasarkan kemiripan karakteristik kimianya, menggunakan metode **Hierarchical Clustering (Agglomerative, Ward Linkage)**, tanpa menggunakan label kelas asli (*unsupervised learning*). Project ini juga menguji apakah pola cluster yang terbentuk dari data training dapat diterapkan secara konsisten pada data baru (testing), serta memvisualisasikan hasilnya menggunakan PCA.

---

## 2. Kumpulan Data (Dataset)

**Wine Dataset** — hasil analisis kimia wine dari 3 kultivar anggur berbeda.

| Detail | Keterangan |
|---|---|
| Jumlah sampel | 178 baris |
| Jumlah atribut | 13 fitur numerik |
| Jumlah kelas | 3 (`target`: 0, 1, 2) |
| Tipe data | Numerik kontinu (float) |
| Missing value | Dicek & dibersihkan (`dropna()`) |
| Data duplikat | Dicek & dibersihkan (`drop_duplicates()`) |

**Atribut:** alcohol, malic_acid, ash, alcalinity_of_ash, magnesium, total_phenols, flavanoids, nonflavanoid_phenols, proanthocyanins, color_intensity, hue, od280/od315_of_diluted_wines, proline

---

## 3. Tahapan Algoritma

1. **Load data** — baca `wine_dataset.csv`
2. **Data cleaning** — hapus duplikat & missing value
3. **Pemisahan fitur & target** — `X` (fitur) dan `y` (label, tidak dipakai untuk clustering)
4. **Standarisasi fitur** — `StandardScaler` (mean=0, std=1)
5. **Train-test split** — 80% training, 20% testing
6. **Training model** — `AgglomerativeClustering` pada data training
7. **Hitung centroid** — rata-rata tiap cluster hasil training
8. **Assign cluster data testing** — berdasarkan jarak terdekat ke centroid (nearest-centroid)
9. **Reduksi dimensi (PCA)** — 13 dimensi → 2 dimensi
10. **Visualisasi** — scatter plot cluster training vs testing

---

## 4. Alur Algoritma Hierarchical Clustering (Agglomerative)

```
1. Anggap setiap data sebagai satu cluster tersendiri
2. Hitung jarak antar seluruh pasangan cluster/data
3. Gabungkan dua cluster dengan jarak terdekat
4. Perbarui matriks jarak antar cluster
5. Ulangi langkah 2–4 hingga tersisa jumlah cluster yang diinginkan
6. Bentuk dendrogram dari seluruh proses penggabungan
```

Pendekatan yang digunakan: **Agglomerative (Bottom-Up)** — dimulai dari data individual, digabung bertahap hingga membentuk cluster besar. (Berbeda dengan Divisive/Top-Down yang jarang dipakai karena lebih kompleks.)

---

## 5. Parameter yang Digunakan

| Parameter | Nilai | Keterangan |
|---|---|---|
| `n_clusters` | 3 | Jumlah cluster akhir, disesuaikan dengan jumlah kelas asli |
| `linkage` | ward | Meminimalkan variansi dalam cluster |
| Jarak | Euclidean | Metode pengukuran jarak antar data |
| `test_size` | 0.2 | Proporsi data testing (20%) |
| `random_state` | 42 | Seed acak agar hasil split konsisten |
| `n_components` (PCA) | 2 | Jumlah dimensi hasil reduksi untuk visualisasi |

---

## 6. Rumus yang Digunakan

**Euclidean Distance** (jarak antar titik data, dasar perhitungan jarak & assign cluster):

d(x, y) = √( Σᵢ (xᵢ − yᵢ)² )

**Standarisasi (Z-score)**, digunakan pada `StandardScaler`:

z = (x − μ) / σ

di mana μ = rata-rata fitur, σ = standar deviasi fitur.

**Ward Linkage** — menggabungkan dua cluster yang menghasilkan **kenaikan variansi internal (Sum of Squared Errors) paling kecil** dibanding kombinasi penggabungan lain.

**Centroid (rata-rata cluster)**, dipakai untuk assign data testing:

centroid_k = (1/n) Σ xᵢ , untuk semua xᵢ pada cluster k

---

## 7. Properti Model

| Properti | Nilai |
|---|---|
| Jenis pembelajaran | Unsupervised learning |
| Sifat cluster | Hard clustering (satu data → satu cluster, bukan probabilistik) |
| Struktur hasil | Hierarki bertingkat (dapat direpresentasikan dendrogram) |
| Skalabilitas | Kurang cocok untuk dataset besar (kompleksitas tinggi, umumnya O(n²) atau lebih) |
| Kemampuan prediksi data baru | Tidak native — diakali dengan pendekatan centroid manual |
| Sensitivitas | Sensitif terhadap outlier & skala fitur (karena itu wajib standarisasi) |

---

## 8. Teknologi yang Digunakan

| Teknologi | Fungsi |
|---|---|
| Python | Bahasa pemrograman utama |
| Google Colab | Environment eksekusi & upload dataset |
| pandas | Manipulasi & pembersihan data tabular |
| numpy | Operasi numerik & perhitungan jarak |
| scikit-learn | `StandardScaler`, `train_test_split`, `AgglomerativeClustering`, `PCA` |
| matplotlib | Visualisasi hasil clustering (scatter plot) |

---

## 9. Hasil Project

- Data berhasil dibersihkan (bebas duplikat & missing value) dan distandarisasi sebelum diproses
- Model berhasil membentuk **3 cluster** dari 80% data training, dengan distribusi jumlah anggota tiap cluster yang dapat dilihat melalui `value_counts()`
- Data testing (20%) berhasil diklasifikasikan ke salah satu dari 3 cluster menggunakan pendekatan nearest-centroid
- Visualisasi PCA (2D) menunjukkan sebaran data training (titik bulat) dan testing (tanda X), memperlihatkan seberapa jelas pemisahan antar cluster secara visual

---

## 10. Kesimpulan

Hierarchical Clustering dengan Ward Linkage berhasil mengelompokkan sampel wine ke dalam 3 kelompok berdasarkan kemiripan komposisi kimianya, tanpa memerlukan label kelas sejak awal. Standarisasi fitur terbukti krusial karena skala atribut yang berbeda jauh (misalnya *proline* vs *hue*) dapat mendominasi perhitungan jarak jika tidak disamakan. Meskipun algoritma ini secara default tidak mendukung prediksi terhadap data baru, keterbatasan tersebut dapat diatasi dengan pendekatan centroid manual sehingga model tetap dapat diuji generalisasinya pada data testing. Secara keseluruhan, metode ini terbukti efektif untuk dataset berukuran kecil-menengah seperti Wine Dataset, dan berpotensi diterapkan pada kasus nyata seperti segmentasi produk atau quality control di industri minuman.

---
**Penyusun:** Muhammad Fikriansyah — NIM 24260028 — Teknik Informatika — UNUSIA
