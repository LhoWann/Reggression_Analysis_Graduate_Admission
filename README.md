Tentu, berikut adalah draf interpretasi akhir yang dapat Anda gunakan untuk file `README.md` di repositori GitHub Anda.

---

# 📈 Analisis Regresi: Prediksi Penerimaan Pascasarjana

Proyek ini menganalisis dataset "Graduate Admission" untuk memprediksi **Peluang Diterima** (`Chance of Admit`) seorang mahasiswa berdasarkan berbagai faktor akademik dan non-akademik. Model yang digunakan adalah **Regresi Linear Berganda (OLS)**.

**File Notebook:** `regresi_linear_ridwan.ipynb`

## 🎯 1. Ringkasan Proyek

* **Tujuan:** Membangun model regresi linear untuk memahami faktor-faktor apa saja yang secara signifikan memengaruhi peluang penerimaan mahasiswa.
* **Dataset:** `graduate_admission.csv` (1000 baris, 8 kolom).
* **Variabel Dependen (Y):** `Chance of Admit`
* **Variabel Independen (X):**
    * `GRE Score` (x1)
    * `TOEFL Score` (x2)
    * `University Rating` (x3)
    * `SOP` (Statement of Purpose) (x4)
    * `LOR` (Letter of Recommendation) (x5)
    * `GPA` (x6)
    * `Research` (x7)

## 🛠️ 2. Metodologi dan Preprocessing

1.  **Eksplorasi Data (EDA):** Data dipastikan bersih. Tidak ditemukan *missing values* (nilai null) ataupun data duplikat.
2.  **Standard Scaling:** Semua 7 variabel independen (X) distandarisasi menggunakan `StandardScaler`. Langkah ini sangat penting dan berhasil mengatasi masalah **multikolinearitas** yang sebelumnya terdeteksi (Condition Number turun dari >8000 menjadi **1.17**).
3.  **Split Data:** Data dibagi menjadi 70% data latih (700 sampel) dan 30% data tes (300 sampel).
4.  **Pemodelan:** Model OLS (Ordinary Least Squares) dibangun menggunakan `statsmodels` pada data latih.

## 📊 3. Hasil Model (Data Latih - OLS)

Model yang dihasilkan menunjukkan performa yang sangat kuat pada data latih.

* **R-squared:** **0.904**
    * Model ini mampu menjelaskan **90.4%** varians dari `Chance of Admit`. Ini adalah nilai yang sangat tinggi.
* **Prob (F-statistic):** **0.00**
    * Model ini sangat signifikan secara statistik.
* **Signifikansi Fitur (P>|t|):**
    * Semua 7 variabel independen (`x1` s/d `x7`) memiliki P-value **0.000** (< 0.05).
    * **Kesimpulan:** **Semua 7 fitur** adalah prediktor yang signifikan secara statistik.

### 🔍 Interpretasi Koefisien (`coef`)

Karena fitur telah di-scaling, koefisien menunjukkan peningkatan `Chance of Admit` untuk setiap 1 standar deviasi kenaikan pada fitur tersebut.

* **`const` (Konstanta):** 0.7308 (Peluang dasar jika semua fitur berada di nilai rata-rata).
* **`x7` (Research):** 0.0746 (Fitur paling berpengaruh)
* **`x3` (University Rating):** 0.0291
* **`x6` (GPA):** 0.0287
* **`x5` (LOR):** 0.0248
* **`x4` (SOP):** 0.0227
* **`x2` (TOEFL Score):** 0.0105
* **`x1` (GRE Score):** 0.0091

## 🩺 4. Validasi Asumsi Model

Model regresi yang baik harus memenuhi beberapa asumsi klasik:

1.  **Multikolinearitas (Cond. No.): 1.17**
    * Nilai yang sangat rendah (ideal < 30). **Asumsi terpenuhi** (tidak ada multikolinearitas).
2.  **Autokorelasi (Durbin-Watson): 1.946**
    * Nilai sangat dekat dengan 2. **Asumsi terpenuhi** (tidak ada autokorelasi).
3.  **Normalitas Residual (Prob(Jarque-Bera) & Shapiro-Wilk):**
    * Prob(JB) = 0.103 (> 0.05)
    * Shapiro-Wilk p-value = 0.740 (> 0.05)
    * **Asumsi terpenuhi**. Plot distribusi residual juga menunjukkan bentuk lonceng yang normal.
4.  **Homoskedastisitas (Residuals vs. Predicted Plot):**
    * Plot menunjukkan sebaran titik yang acak dan merata di sekitar garis nol.
    * **Asumsi terpenuhi** (tidak ada pola corong/heteroskedastisitas).

## 🚀 5. Evaluasi Model (Data Tes)

Model diuji pada 300 data yang belum pernah dilihat sebelumnya.

* **R-square (Test):** **0.895** (89.5%)
    * Performa model tetap sangat tinggi pada data tes dan nilainya sangat dekat dengan R-square data latih (90.4%). Ini menunjukkan model dapat **digeneralisasi dengan baik** dan **tidak overfitting**.
* **Mean Squared Error (MSE):** **0.00096**
    * Nilai error kuadrat rata-rata sangat kecil, menunjukkan prediksi model sangat akurat.

## ✅ 6. Kesimpulan Akhir

Model Regresi Linear Berganda ini **sangat kuat, akurat, dan valid secara statistik** untuk memprediksi peluang penerimaan pascasarjana. Semua 7 fitur terbukti menjadi prediktor yang signifikan, dengan **Pengalaman Riset** (`Research`) menjadi faktor yang paling berpengaruh.
