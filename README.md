# capstone-3
# Prediksi Harga Rumah di California

![Python](https://img.shields.io/badge/Python-3.8%2B-blue) ![Lisensi](https://img.shields.io/badge/Lisensi-MIT-green) ![Status](https://img.shields.io/badge/Status-Selesai-success)

## Ikhtisar

Proyek ini bertujuan untuk memprediksi harga rumah di California menggunakan **Dataset Perumahan California** dari Sensus California 1990. Tujuannya adalah mengembangkan model machine learning yang lebih akurat dibandingkan pendekatan berbasis aturan sederhana, sehingga memberikan prediksi harga rumah yang tepat dan konsisten bagi pemangku kepentingan seperti pembeli, penjual, agen properti, dan investor.

Dataset ini mencakup fitur seperti koordinat geografis (`longitude`, `latitude`), karakteristik rumah (`housing_median_age`, `total_rooms`), informasi demografis (`population`, `households`, `median_income`), dan variabel target (`median_house_value`). Proyek ini mengatasi tantangan memprediksi harga rumah di pasar California yang dinamis dan kompetitif, di mana harga bervariasi signifikan berdasarkan lokasi dan faktor lainnya.

## Daftar Isi
- [Dataset](#dataset)
- [Pernyataan Masalah](#pernyataan-masalah)
- [Metodologi](#metodologi)
- [Hasil](#hasil)
- [Instalasi](#instalasi)
- [Penggunaan](#penggunaan)
- [Kesimpulan](#kesimpulan)
- [Rekomendasi](#rekomendasi)
- [Lisensi](#lisensi)
- [Ucapan Terima Kasih](#ucapan-terima-kasih)

## Dataset

Dataset yang digunakan adalah **Dataset Perumahan California**, yang berisi 14.448 catatan dengan fitur berikut:

| Fitur                | Deskripsi                                                                 |
|----------------------|---------------------------------------------------------------------------|
| **longitude**        | Garis bujur lokasi rumah (ukuran ke arah barat).                          |
| **latitude**         | Garis lintang lokasi rumah (ukuran ke arah utara).                        |
| **housing_median_age** | Usia rata-rata rumah dalam satu blok (angka kecil menunjukkan bangunan baru). |
| **total_rooms**      | Jumlah total kamar dalam satu blok.                                       |
| **total_bedrooms**   | Jumlah total kamar tidur dalam satu blok.                                 |
| **population**       | Jumlah total penduduk dalam satu blok.                                    |
| **households**       | Jumlah total rumah tangga dalam satu blok.                                |
| **median_income**    | Pendapatan rata-rata rumah tangga dalam satu blok (dalam puluhan ribu USD). |
| **ocean_proximity**  | Kedekatan dengan laut (kategori: ISLAND, <1H OCEAN, NEAR OCEAN, NEAR BAY, INLAND). |
| **median_house_value** | Nilai rata-rata rumah dalam satu blok (dalam USD, variabel target).      |

Dataset tersedia di repositori sebagai `data_california_house.csv`.

## Pernyataan Masalah

Memprediksi harga rumah secara akurat di pasar properti California yang beragam dan kompetitif adalah tantangan besar karena dipengaruhi oleh berbagai faktor seperti lokasi, kondisi properti, dan demografi. Tanpa alat prediksi yang andal, penjual berisiko menetapkan harga terlalu tinggi atau rendah, sementara pembeli kesulitan menilai nilai pasar yang wajar. Proyek ini bertujuan membangun model machine learning yang andal untuk memprediksi `median_house_value` berdasarkan fitur yang tersedia, dengan performa lebih baik dibandingkan pendekatan berbasis aturan.

## Metodologi

1. **Persiapan Data**:
   - Memuat dataset dan melakukan analisis data eksploratif.
   - Menangani nilai yang hilang dan outlier menggunakan teknik seperti `SimpleImputer` dan `IsolationForest`.
   - Membuat fitur baru seperti `income_per_person` dan `population_per_household` untuk menangkap pola tambahan.
   - Mengkodekan variabel kategorikal (`ocean_proximity`) menggunakan `OneHotEncoder`.

2. **Pemodelan**:
   - Menguji beberapa model regresi, termasuk:
     - Linear Regression, Lasso, Ridge, ElasticNet
     - DecisionTreeRegressor, RandomForestRegressor, GradientBoostingRegressor
     - KNeighborsRegressor, SVR, MLPRegressor
     - XGBoost, LightGBM
   - Mengoptimalkan hiperparameter menggunakan `RandomizedSearchCV` dengan validasi silang.
   - Mengevaluasi model menggunakan **Mean Absolute Error (MAE)**, **Root Mean Squared Error (RMSE)**, dan **R² Score**.

3. **Perbandingan Baseline**:
   - Mengembangkan model prediksi berbasis aturan sebagai baseline.
   - Membandingkan model machine learning dengan pendekatan berbasis aturan untuk menilai peningkatan performa.

4. **Alat dan Pustaka**:
   - Pustaka Python: `pandas`, `numpy`, `scikit-learn`, `xgboost`, `lightgbm`, `matplotlib`, `seaborn`, `folium`, `imblearn`, `category_encoders`, `jcopml`.
   - Lingkungan: Jupyter Notebook (Google Colab).

## Hasil

Model **LightGBM** mencapai performa terbaik dengan metrik validasi silang berikut:
- **CV MAE**: $29,706.59
- **CV RMSE**: $46,062.48
- **CV R²**: 0.8428

Dibandingkan dengan baseline berbasis aturan, yang memiliki:
- **MAE**: $62,858.59
- **RMSE**: $84,103.33
- **R²**: 0.4689

Model LightGBM jauh lebih unggul, menjelaskan 84,28% variansi harga rumah dan mengurangi kesalahan prediksi.

**Metrik Uji Akhir**:
- **MAE**: $29,911.72
- **RMSE**: $45,912.14
- **R²**: 0.8305

Hasil ini menunjukkan bahwa model cukup akurat, tetapi masih ada ruang untuk perbaikan, terutama untuk properti dengan harga rendah di mana kesalahan mewakili persentase lebih besar dari nilai rumah (misalnya, ~30,6% untuk rumah seharga $150,000).

## Instalasi

Untuk menjalankan proyek ini secara lokal, ikuti langkah-langkah berikut:

1. Kloning repositori:
   ```bash
   git clone https://github.com/nama-pengguna-anda/prediksi-harga-rumah-california.git
   cd prediksi-harga-rumah-california
pip install -r requirements.txt

Kesimpulan
Model LightGBM memberikan solusi yang andal untuk memprediksi harga rumah, jauh lebih baik dibandingkan baseline berbasis aturan.
Model menjelaskan 83,05% variansi harga rumah, tetapi kesalahan lebih berdampak pada properti dengan harga rendah.
Rekayasa fitur dan optimasi hiperparameter sangat penting untuk mencapai performa tinggi.
Rekomendasi
Rekomendasi Teknis
Meningkatkan Kualitas Data:
Tambah data terbaru dari platform real estate seperti Redfin atau Realtor.com.
Terapkan deteksi outlier tambahan menggunakan metode IQR atau Z-score.
Pemodelan Lanjutan:
Eksperimen dengan teknik ensemble seperti stacking atau voting regressor.
Gabungkan LightGBM dengan XGBoost atau CatBoost untuk prediksi yang lebih baik.
Rekayasa Fitur:
Buat fitur interaksi (misalnya, median_income * population_per_household).
Gunakan pengelompokan geografis untuk mengkategorikan lokasi ke dalam kelompok urban, suburban, atau rural.
Optimasi Model:
Terapkan early stopping pada LightGBM untuk mencegah overfitting.
Gunakan pelatihan terdistribusi dengan Dask atau Ray untuk mempercepat penyesuaian hiperparameter.
Rekomendasi Bisnis
Menargetkan Pengguna Beragam:
Bermitra dengan pemerintah daerah untuk analisis perencanaan kota.
Tawarkan model sebagai API untuk startup proptech dengan model berlangganan.
Edukasi Pasar:
Selenggarakan webinar atau workshop tentang prediksi harga rumah berbasis AI untuk agen dan investor.
Publikasikan whitepaper tentang keunggulan model, terutama untuk properti harga rendah.
Fitur Premium:
Kembangkan alat analisis sensitivitas untuk investor (misalnya, dampak perubahan suku bunga).
Buat dashboard interaktif berbasis web untuk prediksi harga secara real-time.
Pasar Niche:
Fokus pada properti liburan di wilayah pesisir California, dengan mempertimbangkan tren musiman.
Kembangkan solusi untuk perumahan hijau, dengan menekankan fitur efisiensi energi dan iklim.
Lisensi
Proyek ini dilisensikan di bawah Lisensi MIT. Lihat file  untuk detailnya.

Ucapan Terima Kasih
Dataset Perumahan California bersumber dari Sensus California 1990.
Terima kasih kepada komunitas open-source untuk pustaka seperti scikit-learn, xgboost, dan lightgbm.
Proyek ini dikembangkan sebagai bagian dari proyek capstone oleh Frans Julian Bryan Sagala.
