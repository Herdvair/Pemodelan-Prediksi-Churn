 # Pemodelan Prediksi Churn

 # 💡 Latar Belakang Proyek

Proyek ini bertujuan untuk memprediksi potensi pelanggan yang akan churn menggunakan berbagai algoritma machine learning. Proyek ini mengevaluasi performa beberapa model, yaitu: 

- Logistik Regression
- Decision Tree
- Random Forest
- XG-Boost
- LightGBM
- K-Nearest Neighboes (KNN)

 Hasil ini diharapkan dapat membantu perusahaan dalam mengidentifikasi pelanggan yang beresiko churn dan menyusun strategi retensi yang lebih efektif.

 # 🛠️ Tahapan Proyek
1. Data Cleaning
   
- Pengecekan Duplikat : Tidak Ada
- Pengecekan Missing Value : Tidak Ada
- Pengecekan Outlier : Distribusi data masih wajar

2. EDA (Exploratory Data Analysis)

- **Distribusi Churn**
  
    Berdasarkan visualisasi distribusi churn dan hasil perhitungan proporsi, terlihat bahwa mayoritas nasabah berada pada kategori tidak churn dengan jumlah sekitar 7.963 nasabah atau 79,6% dari total populasi. Sementara itu, nasabah yang masuk kategori churn berjumlah 2.037 atau sekitar 20,37%. Hasil identifikasi ini menunjukkan bahwa jumlah nasabah yang bertahan jauh lebih besar dibandingkan dengan mereka yang keluar.
  
- **Distribusi variabel kategori berdasarkan churn**
  
    - Berdasarkan visualisasi churn berdasarkan gender, terlihat bahwa nasabah perempuan memiliki proporsi churn lebih tinggi dibandingkan nasabah laki-laki, sedangkan laki-laki cenderung lebih banyak bertahan. Hasil identifikasi ini memberikan referensi terhadap strategi marketing dalam pencegahan churn itu sebaiknya lebih fokus ke segmen perempuan, misalnya melalui program loyalitas secara personal, penawaran eksklusif yang sesuai dengan preferensi mereka, komunikasi yang lebih proaktif melalui platform digital atau layanan pelanggan.Untuk nasabah laki-laki, perusahaan dapat mengupayakan retensi dengan skala yang lebih efisien karena segmen ini lebih stabil dalam mempertahankan layanan.
    - Berdasarkan visualisasi churn berdasarkan negara, terdapat pola perilaku nasabah di tiap negara. Nasabah di Germany menunjukkan tingkat churn lebih tinggi dibandingkan dengan negara France dan Spain, sehingga strategi pencegahan churn perlu difokuskan pada segmen Germany melalui pendekatan retensi yang lebih agresif, seperti program loyalitas premium, personalisasi penawaran, atau peningkatan kualitas layanan yang relevan dengan kebutuhan lokal. Sementara itu di France, walau churn tetap ada namun proporsi pelanggan bertahan (Tidak churn) cenderung lebih banyak, sehingga strategi retensi dapat difokuskan dalam menjaga kepuasan nasabah yang sudah loyal. Disisi lain yaitu Spain,, churn lebih rendah dibandingkan Germany namun tetap perlu dipantau agar tidak meningkat, misal kampanye retensi ringan seperti komunikasi proaktif, edukasi produk atau layanan dan program insentif sederhana.
 
- **Distribusi variabel numerik berdasarkan churn**

  Berdasarkan visualisasi boxplot dari berbagai variabel numerik terhadap churn, dapat diketahui bahwa beberapa faktor berpotensi berhubungan dengan perilaku nasabah yang churn. Nasabah dengan usia yang lebih tua (sekitaran 40-an keatas) cenderung memiliki proporsi churn yang lebih tinggi dibandingan yang lebih muda, sehingga program retensi bisa difokuskan pada segmen usia senior dengan menawarkan layanan finansial yang lebih stabil, seperti produk tabungan pensiun, produk jaminan hari tua. Selain itu, nasabah dengan saldo (balance) yang lebih tinggi juga lebih rentan terhadap churn sehingga perusahaan dapat memberikan program loyalitas berbasis saldo atau imbalan eksklusif agar nasabah bernilai tinggi ini tetap bertahan. Sementara variabel lain seperti tenure, product number, credit card, status active member, maupun estimated salary juga terlihat rentan terhadap churn. Dengan demikian, strategi marketing yang tepat adalah melakukan segmentasi pelanggan dan memberikan penawaran retensi yang lebih personal


3. Feature Engineering
- Cek Multicollinearity (Only Logistic Regression) : Hasil vif score cenderung merata dan tidak ada vif score yang lebih dari 2, sehingga tidak ada kolom yang harus dihapus.
- Encoding : Melakukan encode pada data kategori di kolom country dan gender.
- Scaling : Dilakukan standarisasi nilai pada kolom credit_score, age, tenure, balance, products_number, estimated_salary karena memiliki range data berbeda-beda di data aslinya.

# 🤖 Pemodelan & Hasil
Pada eksperimen ini dilakukan identifikasi performa model dengan _weight-balanced_  dan model dengan handling imbalanced data menggunakan _SMOTEENN_. Berikut hasilnya:

1. Model dengan _weight-balanced_
   
   | Model | Dataset | True Positive | True Negative | False Positive | False Negative | Accuracy | Precision | Recall | F1-Score |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| **Logistic Regression** | Train | 1134 | 4529 | 1827 | 510 | 0.7079 | 0.3830 | 0.6898 | 0.4925 |
|  | Test | 280 | 1159 | 448 | 113 | 0.7195 | 0.3846 | 0.7125 | 0.4996 |
| **KNN** | Train | 893 | 6136 | 220 | 751 | 0.8786 | 0.8023 | 0.5432 | 0.6478 |
|  | Test | 177 | 1506 | 101 | 216 | 0.8415 | 0.6367 | 0.4504 | 0.5276 |
| **Decision Tree** | Train | 1644 | 6356 | 0 | 0 | 1.0000 | 1.0000 | 1.0000 | 1.0000 |
|  | Test | 191 | 1408 | 199 | 202 | 0.7995 | 0.4897 | 0.4860 | 0.4879 |
| **SVM** | Train | 1315 | 5233 | 1123 | 329 | 0.8185 | 0.5394 | 0.7999 | 0.6443 |
|  | Test | 303 | 1280 | 327 | 90 | 0.7915 | 0.4810 | 0.7710 | 0.5924 |

Kesimpulan :

Diantara model diatas, lebih seimbang adalah SVM. Dapat dilihat dari recall tinggi dan lebih stabil dibandingkan model lain, gap antara train dan test juga beda tipis. Meskipun precision hanya 48%, model ini dapat mengenali nasabah yang benar-benar churn. Cocok untuk strategi deteksi churn lebih luas dengan resiko false positive.

3. Model dengan SMOTEENN


| Model                | Data Type | Accuracy | Precision | Recall | F1-Score |
|----------------------|------------|-----------|------------|---------|-----------|
| **Logistic Regression** | Train | 0.7951 | 0.8115 | 0.8335 | 0.8223 |
|                      | Test  | 0.6645 | 0.3435 | 0.7761 | 0.4762 |
| **KNN**              | Train | 0.9861 | 0.9798 | 0.9960 | 0.9879 |
|                      | Test  | 0.7250 | 0.3990 | 0.7888 | 0.5299 |
| **Decision Tree**    | Train | 1.0000 | 1.0000 | 1.0000 | 1.0000 |
|                      | Test  | 0.7555 | 0.4262 | 0.7048 | 0.5312 |
| **SVM**              | Train | 0.9267 | 0.9349 | 0.9363 | 0.9356 |
|                      | Test  | 0.7455 | 0.4229 | 0.8092 | 0.5555 |

Kesimpulan :

Diantara model diatas, Logistic Regression dengan SMOTEENN lebih baik dalam mengenali churn (recall tinggi), tapi dengan trade off false positive sangat banyak. Sehingga model ini sangat boros pada biaya marketing karena banyak pelanggan loyal salah sasaran. Disamping itu, sebenanrya recall SVM lebih baik daripada logistic namun model SVM terindikasi overfitting karena gap antara train dan test sangat jauh.

# 


