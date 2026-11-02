# Customer Credit Risk Prediction Menggunakan Machine Learning

## Gambaran Umum Proyek

Proyek ini bertujuan untuk membangun model *machine learning* yang dapat memprediksi risiko gagal bayar (*loan default*) berdasarkan informasi finansial dan karakteristik pinjaman calon peminjam.

Tujuan utama proyek ini adalah mengidentifikasi calon peminjam yang berpotensi mengalami gagal bayar serta mengeksplorasi bagaimana penerapan *machine learning* dapat membantu proses penilaian risiko kredit dan mendukung pengambilan keputusan bisnis berbasis data.

Dalam proyek ini, dilakukan pembangunan dan perbandingan tiga algoritma *machine learning*, yaitu Logistic Regression, Decision Tree, dan Random Forest.

## Tujuan Proyek

- Menganalisis karakteristik peminjam dan informasi terkait pinjaman.
- Melakukan pembersihan data (*data cleaning*) dan analisis eksploratif (*Exploratory Data Analysis*).
- Membangun model *machine learning* untuk memprediksi risiko gagal bayar.
- Membandingkan performa model menggunakan berbagai metrik evaluasi klasifikasi.
- Mengidentifikasi fitur yang paling berpengaruh terhadap hasil prediksi gagal bayar.
- Menghasilkan *business insight* dan rekomendasi berdasarkan hasil analisis.

## Dataset

Dataset yang digunakan dalam proyek ini adalah **Credit Risk Dataset** yang diperoleh dari Kaggle.

- **Sumber:** [Kaggle – Credit Risk Dataset](https://www.kaggle.com/datasets/laotse/credit-risk-dataset)
- **Pembuat Dataset:** Lao Tse
- **Jumlah Data Awal:** 32.581 baris
- **Jumlah Data Setelah Cleaning:** 32.411 baris
- **Variabel Target:** `loan_status`

Interpretasi variabel target:

| Nilai | Keterangan |
|---|---|
| 0 | Tidak mengalami gagal bayar (Non-Default) |
| 1 | Mengalami gagal bayar (Default) |

Dataset diunduh secara otomatis menggunakan KaggleHub.

## Tools dan Teknologi

Tools dan library yang digunakan dalam proyek ini:

- **Python:** Bahasa pemrograman utama.
- **Pandas dan NumPy:** Pengolahan dan manipulasi data.
- **Matplotlib dan Seaborn:** Visualisasi data.
- **Scikit-learn:** Preprocessing, pembangunan model, dan evaluasi machine learning.
- **Jupyter Notebook:** Lingkungan untuk analisis dan eksperimen.
- **KaggleHub:** Mengunduh dataset dari Kaggle.

## Tahapan Pengerjaan Proyek

1. **Data Acquisition:** Mengunduh dataset Credit Risk dari Kaggle menggunakan KaggleHub.
2. **Data Cleaning:** Menghapus data duplikat, menangani nilai usia yang tidak wajar, dan mengubah nilai masa kerja yang tidak valid menjadi missing value.
3. **Exploratory Data Analysis (EDA):** Menganalisis distribusi data, tingkat gagal bayar, hubungan antarfitur, serta pola korelasi.
4. **Feature Selection:** Memilih fitur yang relevan dan mengecualikan `loan_grade` serta `loan_int_rate` untuk mengurangi potensi kebocoran target (*target leakage*).
5. **Data Preprocessing:** Melakukan imputasi median dan standard scaling pada fitur numerik, serta imputasi modus dan one-hot encoding pada fitur kategorikal.
6. **Train-Test Split:** Membagi data menjadi 80% data training dan 20% data testing menggunakan stratified sampling.
7. **Model Training:** Membangun tiga model klasifikasi menggunakan algoritma Logistic Regression, Decision Tree, dan Random Forest.
8. **Model Evaluation:** Membandingkan performa ketiga model menggunakan berbagai metrik evaluasi.
9. **Feature Importance:** Mengidentifikasi fitur yang paling berpengaruh menggunakan model Random Forest.
10. **Cross-Validation:** Melakukan evaluasi tambahan terhadap Random Forest menggunakan metode 5-Fold Stratified Cross-Validation.

## Model Machine Learning

Tiga algoritma klasifikasi yang digunakan dalam proyek ini adalah:

- Logistic Regression
- Decision Tree Classifier
- Random Forest Classifier

## Perbandingan Performa Model

Evaluasi dilakukan menggunakan data testing yang sama untuk memastikan perbandingan performa ketiga model dapat dilakukan secara adil.

| Metrik Evaluasi | Logistic Regression | Decision Tree | Random Forest |
|---|---:|---:|---:|
| Accuracy | 73,99% | 86,35% | 84,13% |
| Precision | 44,09% | 73,82% | 62,72% |
| Recall | 70,45% | 58,25% | 67,63% |
| F1-Score | 54,23% | 65,12% | 65,08% |
| ROC-AUC | 80,17% | 84,25% | 86,62% |
| PR-AUC | 61,39% | 72,19% | 77,26% |

### Model Terbaik: Random Forest

Berdasarkan hasil evaluasi, Random Forest menunjukkan performa terbaik secara keseluruhan dalam membedakan peminjam yang berpotensi mengalami gagal bayar dan tidak mengalami gagal bayar.

Model ini memperoleh nilai ROC-AUC tertinggi sebesar **86,62%** dan PR-AUC sebesar **77,26%** dibandingkan kedua model lainnya.

Hasil evaluasi tambahan menggunakan 5-Fold Cross-Validation menunjukkan rata-rata performa sebagai berikut:

| Metrik | Rata-rata |
|---|---:|
| Accuracy | 84,70% |
| Precision | 64,45% |
| Recall | 67,22% |
| F1-Score | 65,78% |
| ROC-AUC | 86,82% |

Hasil tersebut menunjukkan bahwa performa Random Forest relatif konsisten pada beberapa pembagian data validasi.

## Feature Importance

Berdasarkan analisis Feature Importance pada model Random Forest, diperoleh lima fitur teratas yang paling berpengaruh terhadap prediksi risiko gagal bayar:

| Fitur | Importance |
|---|---:|
| loan_percent_income | 31,7% |
| person_income | 21,4% |
| home_ownership_RENT | 8,2% |
| loan_amnt | 7,7% |
| default_on_file_Y | 5,2% |

Dua fitur teratas, yaitu `loan_percent_income` dan `person_income`, memiliki kontribusi importance gabungan sekitar 53%.

Temuan ini menunjukkan bahwa proporsi jumlah pinjaman terhadap pendapatan tahunan serta besarnya pendapatan peminjam merupakan fitur yang penting dalam proses prediksi risiko gagal bayar pada model ini.

## Business Insight & Recommendation

Berdasarkan hasil Exploratory Data Analysis (EDA) dan Feature Importance Random Forest, terdapat beberapa rekomendasi bisnis yang dapat dipertimbangkan oleh perusahaan pembiayaan:

1. **Evaluasi Rasio Pinjaman terhadap Pendapatan**

   Perusahaan disarankan mempertimbangkan rasio jumlah pinjaman terhadap pendapatan tahunan sebagai salah satu indikator utama dalam menilai kemampuan pembayaran calon peminjam. Rasio yang lebih tinggi dapat menjadi pertimbangan untuk melakukan evaluasi tambahan atau penyesuaian batas pinjaman.

2. **Mempertimbangkan Kondisi Pendapatan Peminjam**

   Informasi pendapatan sebaiknya dianalisis bersama dengan jumlah pinjaman yang diajukan. Dengan demikian, perusahaan dapat memperoleh gambaran yang lebih baik mengenai kemampuan calon peminjam dalam memenuhi kewajiban pembayaran.

3. **Menerapkan Pemeriksaan Risiko Tambahan**

   Informasi kepemilikan rumah dan tujuan pinjaman dapat digunakan sebagai indikator pendukung dalam penilaian risiko. Calon peminjam dengan karakteristik yang memiliki tingkat gagal bayar historis lebih tinggi dapat menjalani proses verifikasi tambahan sebelum keputusan kredit ditetapkan.

## Kesimpulan

Proyek ini menunjukkan penerapan *machine learning* dalam proses analisis dan prediksi risiko gagal bayar pinjaman.

Dari ketiga algoritma yang diuji, Random Forest menjadi model dengan performa diskriminasi terbaik berdasarkan nilai ROC-AUC dan PR-AUC. Hasil analisis juga menunjukkan bahwa rasio pinjaman terhadap pendapatan dan pendapatan peminjam merupakan dua fitur yang paling berpengaruh dalam prediksi model.

Secara keseluruhan, proyek ini memberikan pengalaman dalam menerapkan tahapan analisis data dan *machine learning*, mulai dari data cleaning, Exploratory Data Analysis, preprocessing, pembangunan model, evaluasi, hingga penerjemahan hasil analisis menjadi rekomendasi bisnis.

**Catatan:** Proyek ini merupakan eksperimen machine learning independen menggunakan dataset dari Kaggle. Model yang dibangun merupakan prototipe pendukung analisis risiko kredit dan tidak ditujukan sebagai satu-satunya dasar pengambilan keputusan persetujuan atau penolakan pinjaman.
