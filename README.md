# Prediksi Gagal Bayar Kartu Kredit Menggunakan Ensemble Learning

Project ini merupakan tugas besar Machine Learning dengan topik **Ensemble Learning**. Studi kasus yang digunakan adalah prediksi gagal bayar kartu kredit berdasarkan data nasabah, riwayat pembayaran, jumlah tagihan, dan jumlah pembayaran sebelumnya.

Dataset yang digunakan adalah **Default of Credit Card Clients Dataset** dari UCI Machine Learning Repository.

## Tujuan Project

Tujuan utama project ini adalah membangun dan membandingkan beberapa model klasifikasi untuk memprediksi apakah seorang nasabah akan mengalami gagal bayar pada bulan berikutnya.

Target prediksi:

* `0` = Tidak gagal bayar
* `1` = Gagal bayar

Project ini membandingkan beberapa pendekatan model:

1. Baseline Model
2. Bagging
3. Boosting
4. Stacking
5. Eksperimen penanganan data imbalance menggunakan SMOTE

## Isi Folder

```text
Credit-Card-Default-Ensemble-Learning/
├── README.md
├── REFERENSI_REVISI.md
├── .gitignore
├── data/
│   └── UCI_Credit_Card.csv
├── notebooks/
│   └── Tubes_Ensemble_Credit_Card_Default_V3_RevisiResponsi.ipynb
└── outputs/
    ├── hasil_perbandingan_model_v3.csv
    ├── best_by_category_v3.csv
    ├── ranking_model_v3.csv
    └── hasil_prediksi_model_terbaik_v3.csv
```

Keterangan file:

| File                                                         | Keterangan                                                                          |
| ------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| `Tubes_Ensemble_Credit_Card_Default_V3_RevisiResponsi.ipynb` | Notebook utama project end-to-end                                                   |
| `UCI_Credit_Card.csv`                                        | Dataset utama                                                                       |
| `hasil_perbandingan_model_v3.csv`                            | Hasil evaluasi seluruh model                                                        |
| `best_by_category_v3.csv`                                    | Model terbaik dari setiap kategori                                                  |
| `ranking_model_v3.csv`                                       | Ranking model berdasarkan beberapa metrik                                           |
| `hasil_prediksi_model_terbaik_v3.csv`                        | Hasil prediksi dari model terbaik                                                   |
| `REFERENSI_REVISI.md`                                        | Referensi jurnal terkait imbalance, SMOTE, Random Forest, Extra Trees, dan Stacking |

## Metode yang Digunakan

### 1. Baseline Model

Baseline model digunakan sebagai pembanding awal sebelum menggunakan metode Ensemble Learning.

Model yang digunakan:

* Logistic Regression
* Decision Tree

### 2. Bagging

Bagging digunakan untuk meningkatkan stabilitas prediksi dengan menggabungkan banyak model decision tree.

Model yang digunakan:

* Random Forest
* Extra Trees

### 3. Boosting

Boosting digunakan untuk membangun model secara bertahap, dengan model berikutnya memperbaiki kesalahan model sebelumnya.

Model yang digunakan:

* AdaBoost
* HistGradientBoosting
* XGBoost
* LightGBM

### 4. Stacking

Stacking digunakan untuk menggabungkan beberapa model ensemble agar prediksi akhir menjadi lebih kuat.

Model dasar yang digunakan dalam Stacking:

* Random Forest
* Extra Trees
* HistGradientBoosting

Model ini dipilih karena menggabungkan tiga karakter berbeda:

* Random Forest memberikan stabilitas melalui teknik bagging.
* Extra Trees memberikan variasi lebih besar melalui randomisasi split.
* HistGradientBoosting membantu memperbaiki kesalahan secara bertahap melalui boosting.

Dengan kombinasi tersebut, Stacking tidak hanya dipilih karena nilai evaluasinya tinggi, tetapi juga karena secara algoritmik mampu menggabungkan stabilitas, diversity, dan error correction dari beberapa model dasar.

## Penanganan Data Imbalance

Pada project ini, kelas gagal bayar merupakan kelas yang lebih sedikit dibanding kelas tidak gagal bayar. Oleh karena itu, evaluasi model tidak hanya menggunakan accuracy, tetapi juga menggunakan:

* Precision
* Recall
* F1-score
* ROC-AUC
* PR-AUC
* Confusion Matrix

Selain itu, dilakukan juga eksperimen penanganan imbalance menggunakan:

* Class weight
* Threshold tuning
* SMOTE sebagai pembanding

SMOTE tidak langsung digunakan sebagai metode final. SMOTE diuji sebagai eksperimen tambahan berdasarkan referensi imbalance learning. Hasil akhirnya tetap ditentukan berdasarkan evaluasi model secara menyeluruh.

## Hasil Utama

Berdasarkan hasil eksperimen, model terbaik secara keseluruhan adalah:

**Stacking (Random Forest + Extra Trees + HistGradientBoosting)**

Model ini memberikan performa yang seimbang pada beberapa metrik evaluasi, terutama F1-score, ROC-AUC, dan PR-AUC.

Hasil eksperimen juga menunjukkan bahwa SMOTE sudah diuji sebagai metode pembanding, tetapi tidak dipilih sebagai model final karena tidak meningkatkan performa secara konsisten dibanding model utama.

## Alasan Pemilihan Stacking

Stacking dipilih karena memiliki performa yang baik dan secara metodologis sesuai untuk menggabungkan beberapa model dengan karakter berbeda.

Random Forest berperan sebagai model bagging yang stabil. Extra Trees memberikan variasi prediksi melalui randomisasi yang lebih besar. HistGradientBoosting berperan sebagai model boosting yang memperbaiki kesalahan secara bertahap. Output dari ketiga model tersebut kemudian digabungkan oleh meta learner untuk menghasilkan prediksi akhir.

Dengan demikian, pemilihan Stacking tidak hanya didasarkan pada nilai accuracy atau F1-score tertinggi, tetapi juga pada alasan algoritmik bahwa model ini menggabungkan kekuatan beberapa pendekatan ensemble.

## Cara Menjalankan Notebook

1. Buka folder project di VS Code atau Jupyter Notebook.
2. Pastikan file `UCI_Credit_Card.csv` berada dalam folder yang sama dengan notebook.
3. Install library yang dibutuhkan jika belum tersedia:

```python
%pip install -q xgboost lightgbm imbalanced-learn
```

4. Restart kernel.
5. Jalankan notebook dari awal sampai akhir menggunakan **Run All**.

## Output Project

Notebook akan menghasilkan beberapa output:

* Tabel evaluasi seluruh model
* Grafik perbandingan Accuracy, Precision, Recall, F1-score, ROC-AUC, dan PR-AUC
* Confusion matrix setiap model
* ROC curve dan precision-recall curve
* Ranking model
* Model terbaik per kategori
* Feature importance
* Hasil prediksi model terbaik

## Catatan

Project ini tidak mengklaim bahwa model dapat memprediksi gagal bayar secara sempurna. Prediksi gagal bayar merupakan masalah yang kompleks karena dipengaruhi oleh banyak faktor yang tidak seluruhnya tersedia dalam dataset, seperti pendapatan, pekerjaan, aset, pinjaman lain, dan kondisi ekonomi nasabah.

Oleh karena itu, model lebih tepat digunakan sebagai alat bantu risk scoring, bukan sebagai keputusan akhir mutlak dalam penentuan kelayakan kredit.

## Referensi

Referensi lengkap terkait penanganan data imbalance, SMOTE, Random Forest, Extra Trees, dan Stacking dapat dilihat pada file:

```text
REFERENSI_REVISI.md
```
