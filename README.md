# Klasterisasi Time Series Multivariat 29 Sensor Boiler Batu Bara Menggunakan K-Means Berbasis Non-overlapping Windows

Proyek UTS Data Mining 2026, Program Studi S1 Teknik Informatika.

Klasterisasi kondisi operasi boiler batu bara memakai K-Means berbasis representasi jendela temporal.
Sebanyak 29 sensor proses dipakai sebagai fitur, dan suhu uap keluaran boiler (TE_8332A) dipakai sebagai acuan eksternal.

## Tim

| Nama | NPM | Email |
|------|-----|-------|
| Hamzah Abdillah Gabriela     | 140810240029    | hamzah24001@mail.unpad.ac.id      |
| Muhammad Rizky Khatami     | 140810240073    | muhammad24207@mail.unpad.ac.id      |
| Khalit Putra Afana     | 140810240007    | khalit24001@mail.unpad.ac.id        |
| Muhammad Fathin Raihan     | 140810240026    | muhammad24028@mail.unpad.ac.id      |
| Renadi Wilantara     | 140810240061    | renadi24001@mail.unpad.ac.id      |

## Dataset

*A long-tailed distribution time-series dataset in boiler equipment* (Hu dkk., *Scientific Data*, 2025,
doi: [10.1038/s41597-025-05096-4](https://doi.org/10.1038/s41597-025-05096-4)). Berkas yang dipakai adalah versi mentah
`xinan_uncompleted_data.csv`: 86.400 sampel, interval 5 detik, 30 atribut.

- Kaggle: https://www.kaggle.com/datasets/nikitamanaenkov/time-series-of-industrial-boiler-operations
- figshare: https://figshare.com/articles/dataset/A_long-tailed_distribution_time-series_dataset_in_boiler_equipment/28822793

## Metode

1. EDA: statistik deskriptif, boxplot, korelasi Pearson, dan autokorelasi.
2. Praproses: interpolasi linear berbasis waktu, winsorizing 3×IQR, dan RobustScaler.
3. Representasi temporal: jendela 5 menit tanpa tumpang-tindih berisi mean, std, dan slope tiap sensor (87 fitur).
4. Reduksi dimensi: StandardScaler, lalu PCA dengan kriteria Kaiser.
5. K-Means dengan k = 2–10. Pemilihan k memakai Elbow, Silhouette, dan Davies–Bouldin Index.
6. Pembanding: K-Means titik per titik dan K-Means pada rata-rata jendela, serta uji sensitivitas panjang jendela.

## Hasil utama

| Representasi | k | Silhouette | DBI |
|---|---|---|---|
| A. Titik per titik | 2 | 0,166 | 2,019 |
| B. Rata-rata jendela | 2 | 0,174 | 1,955 |
| C. Usulan (mean, std, slope) | 2 | 0,260 | 2,408 |

Representasi usulan unggul pada Silhouette, tetapi lebih buruk pada DBI.
Klaster 1 mencakup 12,6% waktu dan berisi episode singkat fluktuasi tekanan tungku.
Pada klaster ini, porsi suhu uap di luar rentang normal 530–545 °C adalah 12,28%, sedangkan pada klaster stabil 7,55%.

## Struktur repositori

```
UTS_DataMining_EDA_Klasterisasi.ipynb   notebook EDA dan klasterisasi (sudah berisi output)
xinan_uncompleted_data.csv              dataset mentah
figures/                                gambar hasil notebook dan gambar paper
outputs/                                tabel hasil (CSV)
paper/                                  paper final format IEEE
literatur/                              diagram alir PRISMA dan tabel gap analysis 8 paper rujukan
```

## Running

Lokal: buka notebook dengan Python 3.10 atau lebih baru. Paket yang dibutuhkan adalah pandas, numpy, scikit-learn, dan matplotlib.
Jalankan semua sel; gambar dan tabel akan ditulis ulang ke `figures/` dan `outputs/`.

Google Colab: unggah `xinan_uncompleted_data.csv` ke panel *Files*, lalu pilih *Runtime → Run all*.