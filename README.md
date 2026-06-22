# Pengembangan Model Machine Learning Berbasis Regresi Untuk Valuasi Harga Hunian di Tangerang Selatan

> Final Project — Study Club Data Science Beginner, KSM Veterantech UPNVJ

---

## Identitas

| | |
|---|---|
| **Nama** | Hasan Shofiyyur Rahman |
| **NIM** | 2410512011 |
| **Study Club** | Data Science Beginner — KSM Veterantech UPNVJ |
| **Dataset** | House Pricing South Tangerang |
| **Algoritma** | Linear Regression & Random Forest Regressor |

---

## Deskripsi Proyek

Harga hunian merupakan salah satu indikator ekonomi yang paling dinamis, dipengaruhi oleh banyak faktor seperti lokasi, luas bangunan, jumlah kamar, dan fasilitas lainnya. Di wilayah **Tangerang Selatan**, pertumbuhan kawasan perumahan yang pesat membuat valuasi harga hunian menjadi kebutuhan penting bagi calon pembeli, penjual, maupun investor.

Proyek ini membangun model **Machine Learning berbasis Regresi** untuk memprediksi harga hunian di Tangerang Selatan berdasarkan fitur-fitur properti yang tersedia. Dua model dibandingkan:
- **Linear Regression** — sebagai baseline model
- **Random Forest Regressor** — sebagai model utama dengan hyperparameter tuning

### Alur ML Workflow

```
1. Data Collecting => 2. EDA => 3. Data Preprocessing => 4. Model Training => 5. Model Evaluation
```

---

## Dataset

| Atribut | Detail |
|---------|--------|
| **Nama** | House Pricing South Tangerang |
| **Jumlah Data Awal** | ~25.316 sampel |
| **Jumlah Data Setelah Cleaning** | ~20.075 sampel |
| **Jumlah Kolom** | 6 kolom (4 fitur + 1 target + 1 lokasi) |
| **Missing Values** | Ada (ditangani pada tahap preprocessing) |

### Deskripsi Fitur

| Fitur | Keterangan |
|---|---|
| `bed` | Jumlah kamar tidur |
| `bath` | Jumlah kamar mandi |
| `floor_area_sqm` | Luas bangunan dalam meter persegi |
| `kecamatan` | Lokasi kecamatan (di-extract dari alamat listing, di-encode menggunakan LabelEncoder) |

### Target Variable

| Variabel | Keterangan |
|---|---|
| `price_cleaned` | Harga hunian (dalam Rupiah) |

---

## Tech Stack

| Library | Kegunaan |
|---------|----------|
| Python 3.x | Bahasa pemrograman utama |
| Pandas | Manipulasi & analisis data |
| NumPy | Komputasi numerik |
| Matplotlib | Visualisasi data |
| Seaborn | Visualisasi statistik |
| Scikit-learn | Modeling, preprocessing, evaluasi |

---

## Struktur Proyek

```
Pengembangan Model ML .../
├── data/
│   └── Dataset_HousePricing_South_Tangerang.csv   # Dataset
├── notebooks/
│   └── prediksi_harga_rumah_tangsel.ipynb          # Notebook utama (EDA + Model)
├── .gitignore                                       # Git ignore file
├── requirements.txt                                 # Dependencies
└── README.md                                        # File ini
```

---

## Cara Menjalankan

### 1. Clone Repository
```bash
git clone <repo-url>
cd Pengembangan-Model-ML-Regresi-Valuasi-Harga-Hunian-Tangerang-Selatan
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Jalankan Notebook
```bash
jupyter notebook notebooks/prediksi_harga_rumah_tangsel.ipynb
```

Atau buka di **Google Colab** dengan mengupload notebook beserta dataset.

---

## Metodologi

### 1. Data Collecting
Dataset berisi data listing hunian di wilayah Tangerang Selatan dengan informasi harga, luas bangunan, jumlah kamar tidur, kamar mandi, dan lokasi.

### 2. Exploratory Data Analysis (EDA)
- Analisis struktur dataset (`.info()`, `.describe()`, `.shape`)
- Pengecekan dan penanganan missing values
- Penghapusan data duplikat (~5.241 baris duplikat dihapus)
- Pembersihan format harga dan luas bangunan dari string ke numerik
- Feature engineering: Extract `kecamatan` dari kolom `listing-location`
- Visualisasi distribusi fitur dan korelasi antar variabel
- Analisis 10 area/kecamatan terbanyak (Bintaro, BSD, Gading Serpong, dll.)

### 3. Data Preprocessing
- **Missing Value Handling:** Menggunakan `SimpleImputer` untuk mengisi nilai kosong
- **Encoding:** Menggunakan `LabelEncoder` untuk mengkonversi fitur kategorik `kecamatan`
- **Feature Scaling:** Menggunakan `StandardScaler` untuk normalisasi fitur numerik
- **Train-Test Split:** 80:20 dengan `random_state=42`
- **Data setelah preprocessing:** 16.060 data latih, 4.015 data uji

### 4. Model Training
Dua model dilatih dan dibandingkan:
- **Linear Regression** — model baseline menggunakan `sklearn.linear_model.LinearRegression`
- **Random Forest Regressor** — model utama menggunakan `sklearn.ensemble.RandomForestRegressor`

### 5. Model Evaluation & Hyperparameter Tuning
- **Hyperparameter Tuning:** Menggunakan `RandomizedSearchCV` pada Random Forest
  - Parameter yang dituning: `n_estimators`, `max_depth`, `min_samples_split`, `min_samples_leaf`
  - Settingan terbaik: `n_estimators=300`, `min_samples_split=5`, `min_samples_leaf=2`, `max_depth=None`
- **Metrik Evaluasi:**

| Metrik | Random Forest (Base) | Random Forest (Tuned) |
|---|---|---|
| **MAE** | Rp 952.685.070 | Rp 954.212.334 |
| **R² Score** | 0.6772 | 0.6972 |

- **Peningkatan akurasi** setelah tuning: **+0.0200 poin R²**
- **Interpretasi:** Faktor yang paling mempengaruhi harga rumah adalah `floor_area_sqm` (luas bangunan), diikuti oleh `bath`, `bed`, dan `kecamatan_encoded`

---

## Hasil & Kesimpulan

- Model **Random Forest Regressor** setelah tuning menghasilkan **R² = 0.6972**, artinya model mampu menjelaskan ~70% variasi harga hunian
- **Luas bangunan** (`floor_area_sqm`) menjadi fitur paling penting dalam menentukan harga
- Terdapat ruang peningkatan model dengan menambahkan fitur tambahan seperti:
  - Tahun pembangunan
  - Jarak ke fasilitas publik (stasiun, mall, sekolah)
  - Status sertifikat tanah (SHM/HGB)

---

## Referensi

- Scikit-learn Documentation: https://scikit-learn.org/stable/
- Scikit-learn Linear Regression: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html
- Scikit-learn Random Forest: https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html
- Scikit-learn RandomizedSearchCV: https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.RandomizedSearchCV.html

---

*Final Project — Study Club Data Science Beginner, KSM Veterantech UPNVJ, 2026*
