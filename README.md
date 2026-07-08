# Hierarchical Clustering - Dataset Iris

Proyek tugas Machine Learning yang menerapkan algoritma **Agglomerative Hierarchical Clustering** untuk mengelompokkan data bunga Iris tanpa menggunakan label spesies (unsupervised learning).

**Penyusun:** Muhamad Fikriansyah (NIM 24260028)
**Program Studi:** Teknik Informatika — Universitas Nahdlatul Ulama Indonesia (UNUSIA)

## 📌 Deskripsi

Dataset Iris berisi 150 sampel bunga dengan 4 atribut numerik (panjang & lebar sepal, panjang & lebar petal). Proyek ini menguji apakah struktur alami data — tanpa bantuan label spesies — dapat ditemukan kembali menggunakan hierarchical clustering.

## 🗂️ Isi Repository

| File | Keterangan |
|---|---|
| `hierarchical_clustering_iris.ipynb` | Notebook Python berisi seluruh proses analisis |
| `Hierarchical_Clustering_Presentation.pptx` | Slide presentasi materi & hasil (16 slide) |
| `Tugas_Fikriansyah_MC_Hierarchical_Clustering_Wine_Dataset.docx` | Laporan tugas dalam format Word |

## ⚙️ Alur Kerja

1. Membaca dataset Iris langsung dari UCI Machine Learning Repository
2. Eksplorasi data (info, missing value, statistik deskriptif)
3. Standarisasi fitur menggunakan `StandardScaler`
4. Membangun **dendrogram** dengan metode **Ward linkage**
5. Menentukan jumlah cluster optimal dengan memotong dendrogram → **3 cluster**
6. Menjalankan `AgglomerativeClustering` dan menambahkan label cluster ke data
7. Validasi hasil dengan crosstab terhadap spesies asli
8. Visualisasi scatter plot (Petal Length vs Petal Width) berwarna per cluster

## 📊 Hasil

3 cluster yang terbentuk secara alami sejalan dengan 3 spesies asli Iris (*Iris-setosa*, *Iris-versicolor*, *Iris-virginica*). Fitur *Petal Length* dan *Petal Width* terbukti paling diskriminatif dalam memisahkan spesies.

## 🧠 Kesimpulan

Hierarchical clustering berhasil menangkap struktur alami data Iris tanpa menggunakan label spesies, menjadikannya alat eksploratif yang kuat sebelum masuk ke tahap supervised learning.

## 🛠️ Library yang Digunakan

- `pandas`, `numpy`
- `matplotlib`
- `scipy.cluster.hierarchy` (linkage, dendrogram)
- `sklearn.preprocessing` (StandardScaler)
- `sklearn.cluster` (AgglomerativeClustering)

## 📚 Referensi

- Mukhtar, M., et al. (2024). *Hierarchical Clustering Algorithm-Dendogram Using Euclidean and Manhattan Distance*. Teknika: Jurnal Sains dan Teknologi.
- Alamtaha, Z., Djakaria, I., & Yahya, N. I. (2023). *Implementasi Algoritma Hierarchical Clustering dan Non-Hierarchical Clustering untuk Pengelompokkan Pengguna Media Sosial*. ESTIMASI.
- Wardani, S. D. K., et al. (2023). *Perbandingan Hasil Metode Clustering K-Means, DB Scanner & Hierarchical untuk Analisa Segmentasi Pasar*. JIKO.
- Pedregosa, F., et al. (2011). *Scikit-learn: Machine Learning in Python*. JMLR.
- Scikit-learn Documentation — Hierarchical Clustering.
- SciPy Documentation — Hierarchical Clustering (scipy.cluster.hierarchy).
