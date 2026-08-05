```markdown
# 🌫️ Prediksi Kualitas Udara (ISPU) DKI Jakarta Menggunakan Random Forest

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Random_Forest-orange.svg)
![Platform](https://img.shields.io/badge/Platform-Google_Colab-yellow.svg)

## 📖 Deskripsi Project
Project ini bertujuan untuk membangun model *Machine Learning* yang mampu mengklasifikasikan kualitas udara di Jakarta berdasarkan Indeks Standar Pencemaran Udara (ISPU) ke dalam 4 kategori: **BAIK, SEDANG, TIDAK SEHAT,** dan **SANGAT TIDAK SEHAT**. 

Dataset yang digunakan merupakan data pengukuran harian dari 5 stasiun pemantauan SPKU (Stasiun Pemantau Kualitas Udara) di DKI Jakarta yang mencatat konsentrasi parameter polutan utama (PM10, SO2, CO, O3, NO2).

## 🗄️ Dataset
Dataset yang digunakan dalam project ini merupakan data Indeks Standar Pencemaran Udara (ISPU) di DKI Jakarta mulai dari tahun 2010 hingga 2021.
* **Sumber Data:** [Air Quality Index in Jakarta (2010-2021) - Kaggle](https://www.kaggle.com/datasets/senadu34/air-quality-index-in-jakarta-2010-2021)
* **File yang digunakan:** `ispu_dki_all.csv`

## 🎯 Problem Statement & Objective
* **Masalah:** Penentuan kategori ISPU biasanya bergantung pada satu nilai tertinggi (*critical parameter*). Apakah model ML bisa mempelajari pola hubungan antar seluruh gas polutan untuk mengklasifikasikan udara tanpa harus bergantung pada satu nilai akhir?
* **Tujuan:** Membangun model klasifikasi (*Multiclass Classification*) menggunakan **Random Forest** yang tidak hanya akurat, tetapi juga terhindar dari *Data Leakage*, *Overfitting*, serta mampu menangani data yang sangat tidak seimbang (*imbalanced dataset*).

## 🛠️ Alur Kerja (End-to-End Pipeline)
Project ini dibagi ke dalam 4 modul terpisah untuk menjaga integritas dan modularitas kode:

### 1. EDA (Exploratory Data Analysis)
* Analisis distribusi data per stasiun (DKI1 - DKI5).
* Identifikasi anomali polutan (Contoh: Stasiun Jagakarsa memiliki lonjakan nilai O3 yang sangat ekstrem dibanding stasiun lain).
* Analisis korelasi dan penentuan polutan *critical* paling berpengaruh.

### 2. Preprocessing
* **Data Leakage Prevention:** Menghapus kolom `max` dan `critical` dari fitur karena berisi "kunci jawaban" dari target `categori`.
* **Missing Value Handling:** Menghapus kolom `PM2.5` (100% kosong) dan melakukan imputasi median berdasarkan stasiun masing-masing.
* **Outlier Handling:** Menerapkan *IQR Capping* pada nilai O3 yang ekstrem agar model tidak bias.
* **Scaling:** Menggunakan `RobustScaler` karena distribusi data polutan yang tidak normal (*skewed*).
* **Export:** Menyimpan hasil bersih ke format `.pkl`.

### 3. Modeling
* Algoritma: **Random Forest Classifier**.
* Menggunakan parameter `class_weight='balanced'` untuk menangani *imbalanced class*.
* **Smart Splitting Logic:** Menerapkan logika khusus pada `train_test_split` untuk memastikan kelas minoritas (seperti "BERBAHAYA" yang hanya memiliki 1-2 baris data) **wajib masuk ke dalam data uji (Test Set)** agar bisa dievaluasi, bukan terserap seluruhnya di data latih.

### 4. Evaluation
* **Fitting Analysis:** Membandingkan *Train Accuracy* vs *Test Accuracy* untuk membuktikan model tidak mengalami *Overfitting* atau *Underfitting* (Good Fit).
* **Metrik Utama:** Fokus pada **Macro F1-Score** (bukan sekadar Akurasi) karena ketidakseimbangan kelas.
* **ROC AUC Curve:** Menggunakan pendekatan *One-vs-Rest* (OvR) secara manual untuk menangani error ketika salah satu kelas tidak ada di data uji.
* **Feature Importance:** Mengidentifikasi polutan apa yang paling berkontribusi terhadap prediksi model.

## 📁 Struktur Repository
```text
├── data/
│   └── ispu_dki_all.csv          # Dataset mentah (Download dari Kaggle)
├── notebooks/
│   ├── 1_EDA.ipynb               # Analisis eksplorasi
│   ├── 2_Preprocessing.ipynb     # Pembersihan dan ekspor data
│   ├── 3_Modeling.ipynb          # Training model dan simpan .pkl
│   └── 4_Evaluation.ipynb        # Evaluasi (Akurasi, F1, ROC AUC)
├── pkl_files/
│   ├── data_preprocessed.pkl     # Data bersih siap pakai
│   └── model_bundle.pkl          # Model & data test hasil training
├── images/                       # Folder untuk menyimpan gambar grafik
├── README.md
└── requirements.txt
```

## 📊 Hasil Evaluasi
*(Catatan: Sisipkan gambar hasil grafik kamu dari Google Colab ke folder `images/`, lalu tampilkan di sini menggunakan syntax markdown)*

**1. Analisis Fitting Model**
> Menunjukkan selisih (Gap) antara Train dan Test yang sangat kecil, membuktikan model *Good Fit*. 
> 
> *(Sisipkan gambar: Output teks "ANALISIS KESEIMBANGAN MODEL")*

**2. Classification Report**
> Menampilkan Precision, Recall, dan F1-Score per kategori.
> 
> *(Sisipkan gambar: Output teks "LAPORAN KLASIFIKASI DETAIL")*

**3. Confusion Matrix & ROC AUC**
> Visualisasi ketepatan prediksi dan kemampuan model membedakan kelas.
> 
> *(Sisipkan gambar: Grafik Confusion Matrix)*
> 
> *(Sisipkan gambar: Grafik Kurva ROC AUC)*

**4. Feature Importance**
> Polutan apa yang paling menentukan kualitas udara menurut model?
> 
> *(Sisipkan gambar: Grafik Bar Feature Importance)*

## 💡 Key Insights & Takeaways
1. **Sifat Deterministik ISPU:** Model berhasil mendapatkan akurasi tinggi (~99%) karena sifat data ISPU yang mengikuti aturan batas ambang (threshold) yang kaku, bukan data medis yang ambigu.
2. **Dominasi Polutan Tertentu:** *(Tulis temuan kamu di sini, misalnya: "Stasiun Jagakarsa didominasi oleh polutan O3 sebagai penyebab utama ketidaksehatan udara...")*
3. **Keberhasilan Smart Splitting:** Berhasil mendeteksi dan menangani kelas minoritas ekstrem tanpa membuat model error.

## 🚀 Cara Menjalankan Project
1. Download dataset dari Kaggle: [Air Quality Index in Jakarta (2010-2021)](https://www.kaggle.com/datasets/senadu34/air-quality-index-in-jakarta-2010-2021).
2. Pastikan anda memiliki file dengan nama **`ispu_dki_all.csv`**.
3. Clone repository ini:
   ```bash
   git clone https://github.com/username-kamu/ISPU-Jakarta-RandomForest.git
   ```
4. Letakkan file `ispu_dki_all.csv` ke dalam folder `data/`.
5. Buka Google Colab dan upload folder project tersebut, atau jalankan secara lokal dengan menginstall dependencies:
   ```bash
   pip install -r requirements.txt
   jupyter notebook
   ```
6. Jalankan *notebook* secara berurutan: `1_EDA` -> `2_Preprocessing` -> `3_Modeling` -> `4_Evaluation`.

## 👨‍💻 Author
**Dhafa Marcelio**

[![Instagram](https://img.shields.io/badge/Instagram-dapdhapa-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/dapdhapa/?hl=en)
[![Facebook](https://img.shields.io/badge/Facebook-Dhafa_Marcelio-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://www.facebook.com/muhammad.dhafa.3720190)

---
*Dibangun menggunakan Python dan Scikit-Learn dalam rangka eksplorasi Data Mining & Machine Learning.*
```