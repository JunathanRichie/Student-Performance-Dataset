# Laporan Proyek Machine Learning - Junathan Richie

## Domain Proyek

Dengan adanya perkembangan teknologi yang ada, muncul suatu istilah yaitu _Educational Data Mining_ (EDM). EDM adalah bidang yang menggabungkan beberapa disiplin ilmu seperti _data mining_, _machine learning_, _psychometrics_, _data visualization_, dan _learning theory_ untuk mendapatkan informasi di bidang pendidikan [(Sadia et al., 2020)](https://www.researchgate.net/publication/341259033_Educational_Data_Mining_A_Review_and_Analysis_of_Student's_Academic_Performance). EDM menjadi suatu topik riset yang populer karena adanya digitalisasi pada bidang pendidikan membuat tersedianya data di bidang pendidikan. Selain itu, pendidikan juga adalah salah satu faktor terpenting dalam perkembangan sumber daya manusia (SDM) di dunia. 
<br>
Berdasarkan latar belakang di atas, proyek ini akan membahas mengenai _predictive analytics_ di bidang pendidikan. Proses _predictive analytics_ yang dilakukan berupa regresi terhadap GPA (_Grade Point Average_) pada dataset _Student Performance Dataset_. Dataset tersebut menyimpan berbagai informasi seperti demografi, kebiasaan belajar, pengaruh orang tua, kegiatan ekstrakurikuler, dan performa akademik. Proyek ini diharapkan bisa menjadi dasar untuk mengembangkan model-model yang berkaitan dengan prediksi performa siswa atau mahasiswa dalam pendidikan serta dapat berguna untuk mengembangkan bidang pendidikan. 

## Business Understanding

### Problem Statements
Rumusan masalah berdasarkan latar belakang di atas sebagai berikut. 
- Apa faktor yang paling mempengaruhi GPA? 
- Bagaimana model _machine learning_ yang tepat untuk melakukan prediksi GPA?

### Goals
Tujuan dari proyek ini adalah sebagai berikut: 
- dapat menganalisis faktor yang paling mempengaruhi GPA
- mendapatkan model _machine learning_ yang tepat untuk prediksi GPA

### Solution statements
Cara yang dapat dilakukan untuk meraih goals tersebut adalah sebagai berikut:
- melakukan pengolahan data untuk melihat korelasi dari fitur-fitur yang ada
- menggunakan model dengan metode K-Nearest Neighbor (KNN) disertai dengan hyperparameter tuning
- menggunakan model dengan metode RandomForest disertai dengan hyperparameter tuning
- menggunakan model dengan metode GradientBoosting disertai dengan hyperparameter tuning
- menggunakan model dengan metode XGBoost disertai dengan hyperparameter tuning
- menggunakan model dengan metode Support Vector Regression (SVR) dengan hyperparameter tuning
- melakukan perbandingan dari hasil evaluasi berbagai model yang telah dilakukan

## Data Understanding
Dataset yang digunakan adalah dataset _Students Performance Dataset_ yang dibuat oleh Rabie El Kharoua dan dapat diunduh dari [Kaggle](https://www.kaggle.com/datasets/rabieelkharoua/students-performance-dataset/data). Dataset ini terdiri dari 2.392 data dari siswa SMA dengan 14 fitur (kolom). 

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- StudentID : merupakan penanda unik dari setiap siswa
- Age : merupakan umur dari setiap siswa
- Ethnicity: merupakan kelompok etnis dari siswa yang dikodekan sebagai berikut: <br>
0: Caucasian <br>
1: African American <br>
2: Asian <br>
3: Other 
- ParentalEducation: merupakan tingkat pendidikan dari orang tua siswa yang dikodekan sebagai berikut: <br>
0: None <br>
1: High School <br>
2: Some College <br>
3: Bachelor's <br>
4: Higher
- StudyTimeWeekly: merupakan waktu belajar mingguan
- Absences: jumlah absen dalam 1 tahun ajaran
- Tutoring: bernilai 0 ketika siswa tidak mengikuti bimbingan belajar, bernilai 1 ketika siswa mengikuti bimbingan belajar
- ParentalSupport: merupakan tingkatan dari support orang tu yang dikodekan sebagai berikut: <br>
0: None <br>
1: Low <br>
2: Moderate <br>
3: High <br>
4: Very High
- Extracurricular: merupakan partisipasi dalam ekstrakurikuler. Nilai 0 menunjukkan tidak berpartisipasi, sedangkan nilai 1 menunjukkan partisipasi dalam ekstrakurikuler
- Sports: nilai 0 menunjukkan tidak ada partisipasi dalam olahraga, nilai 1 menunjukkan partisipasi dalam olahraga
- Music: nilai 0 menunjukkan tidak berpartisipasi dalam kegiatan musik, sedangkan nilai 1 menunjukkan partisipasi dalam kegiatan musik
- Volunteering: nilai 0 menunjukkan tidak berpartisipasi dalam kegiatan sukarelawan, sedangkan nilai 1 menunjukkan partisipasi dalam kegiatan sukarelawan
- GPA: merupakan _Grade Point Average_ yaitu nilai dari siswa
- GradeClass: merupakan klasifikasi dari GPA, dengan ketentuan sebagai berikut: <br>
0: 'A' (GPA >= 3.5) <br>
1: 'B' (3.0 <= GPA < 3.5) <br>
2: 'C' (2.5 <= GPA < 3.0) <br>
3: 'D' (2.0 <= GPA < 2.5) <br>
4: 'F' (GPA < 2.0)
### Exploratory Data Analysis - Deskripsi Variabel
- Tipe data dari variabel

  | #  | Column               | Non-Null Count | Dtype   |
  |----|----------------------|----------------|---------|
  | 0  | StudentID            | 2392 non-null  | int64   |
  | 1  | Age                  | 2392 non-null  | int64   |
  | 2  | Gender               | 2392 non-null  | int64   |
  | 3  | Ethnicity            | 2392 non-null  | int64   |
  | 4  | ParentalEducation    | 2392 non-null  | int64   |
  | 5  | StudyTimeWeekly      | 2392 non-null  | float64 |
  | 6  | Absences             | 2392 non-null  | int64   |
  | 7  | Tutoring             | 2392 non-null  | int64   |
  | 8  | ParentalSupport      | 2392 non-null  | int64   |
  | 9  | Extracurricular      | 2392 non-null  | int64   |
  | 10 | Sports               | 2392 non-null  | int64   |
  | 11 | Music                | 2392 non-null  | int64   |
  | 12 | Volunteering         | 2392 non-null  | int64   |
  | 13 | GPA                  | 2392 non-null  | float64 |
  | 14 | GradeClass           | 2392 non-null  | float64 |

  Berdasarkan data tersebut terlihat bahwa tipe data dari dataset tersebut hanya terdiri dari int64 dan float64. Hal ini menunjukkan bahwa seluruh data kategorikal seperti Gender, Ethnicity, ParentalEducation, dan lainnya telah diubah dikodekan dengan angka sehingga menjadi int64.
- Deskripsi dari setiap data
  
  | Statistic          | StudentID   | Age         | Gender      | Ethnicity   | ParentalEducation | StudyTimeWeekly | Absences    | Tutoring    | ParentalSupport | Extracurricular | Sports      | Music       | Volunteering | GPA         | GradeClass  |
  |---------------------|-------------|-------------|-------------|-------------|-------------------|-----------------|-------------|-------------|-----------------|-----------------|-------------|-------------|--------------|-------------|-------------|
  | count              | 2392.000000 | 2392.000000 | 2392.000000 | 2392.000000 | 2392.000000       | 2392.000000     | 2392.000000 | 2392.000000 | 2392.000000     | 2392.000000     | 2392.000000 | 2392.000000 | 2392.000000  | 2392.000000 | 2392.000000 |
  | mean               | 2196.500000 | 16.468645   | 0.510870    | 0.877508    | 1.746237          | 9.771992        | 14.541388   | 0.301421    | 2.122074        | 0.383361        | 0.303512    | 0.196906    | 0.157191     | 1.906186    | 2.983696    |
  | std                | 690.655244  | 1.123798    | 0.499986    | 1.028476    | 1.000411          | 5.652774        | 8.467417    | 0.458971    | 1.122813        | 0.486307        | 0.459870    | 0.397744    | 0.364057     | 0.915156    | 1.233908    |
  | min                | 1001.000000 | 15.000000   | 0.000000    | 0.000000    | 0.000000          | 0.001057        | 0.000000    | 0.000000    | 0.000000        | 0.000000        | 0.000000    | 0.000000    | 0.000000     | 0.000000    | 0.000000    |
  | 25%                | 1598.750000 | 15.000000   | 0.000000    | 0.000000    | 1.000000          | 5.043079        | 7.000000    | 0.000000    | 1.000000        | 0.000000        | 0.000000    | 0.000000    | 0.000000     | 1.174803    | 2.000000    |
  | 50%                | 2196.500000 | 16.000000   | 1.000000    | 0.000000    | 2.000000          | 9.705363        | 15.000000   | 0.000000    | 2.000000        | 0.000000        | 0.000000    | 0.000000    | 0.000000     | 1.893393    | 4.000000    |
  | 75%                | 2794.250000 | 17.000000   | 1.000000    | 2.000000    | 2.000000          | 14.408410       | 22.000000   | 1.000000    | 3.000000        | 1.000000        | 1.000000    | 0.000000    | 0.000000     | 2.622216    | 4.000000    |
  | max                | 3392.000000 | 18.000000   | 1.000000    | 3.000000    | 4.000000          | 19.978094       | 29.000000   | 1.000000    | 4.000000        | 1.000000        | 1.000000    | 1.000000    | 1.000000     | 4.000000    | 4.000000    |

- Berdasarkan fungsi describe di atas tidak terlihat keanehan pada data. Akan tetapi, kolom StudentID dapat didrop karena tidak memiliki keterkaitan dengan tujuan. Selain itu, kolom GradeClass juga dapat didrop karena menunjukkan hal yang sama dengan GPA tetapi hanya berbeda format. 

### Explaratory Data Analysis - Outliers
Pengecekan outliers pada data numerik
- StudyTimeWeekly <br>
  ![image](https://github.com/user-attachments/assets/82b262e8-bd20-46a8-a92b-cf5ede598240) <br>
  Keterangan: Tidak ada outliers
- Absences <br>
  ![image](https://github.com/user-attachments/assets/23eae511-cb39-470c-833f-db254a3a7aa7) <br>
  Keterangan: Tidak ada outliers

### Explaratory Data Analysis - Univariate Analysis
- Gender <br>
  ![image](https://github.com/user-attachments/assets/40f422f9-90e0-4908-9a6a-c43481bd026b) <br>
  Gender pada data hampir setara dengan female sebanyak 1222 (51,1%) dan male sebanyak 1170 (48,9%). 
- Ethnicity <br>
  ![image](https://github.com/user-attachments/assets/47b5b236-f875-4298-848a-0bfbf1327c34) <br>
  Setengah dari kelompok etnis data terdiri dari Caucasian sebanyak 1207 (50,5%). Data-data lainnya yaitu African American sebanyak 493 (20,6%), Asian sebanyak 470(19,6%), dan Other (lainnya) sebanyak 222 (9,3%).

- ParentalEducation <br>
  ![image](https://github.com/user-attachments/assets/6a18af14-6c24-4a66-b117-0e64fa978302) <br>
  Data dari ParentalEducation terdiri dari Some College sebanyak 934 (39,0%), High School sebanyak 728 (30,4%), Bachelor's sebanyak 367 (15,3%), None sebanyak 243 (10,2%), dan Higher sebanyak 120 (5,0%). Hal ini menunjukkan bahwa sebagian besar orang tua memiliki tingkat pendidikan menengah ke atas.
  Parental
- Tutoring <br>
  ![image](https://github.com/user-attachments/assets/749277c4-17c4-471e-b7e9-3ad6ab81937e) <br>
  Berdasarkan data yang ada, 1671 siswa (69,9%) tidak mengikuti bimbingan belajar dan sisanya 721 (30,1%) mengikuti bimbingan belajar. Hal ini menunjukkan bahwa mayoritas siswa pada data tidak mengikuti bimbingan belajar. 
- ParentalSupport <br>
  ![image](https://github.com/user-attachments/assets/e4f82c08-2d36-44d8-b077-c7994ec57d19) <br>
  Data dari kolom ParentalSupport terdiri dari Moderate sebanyak 740 sampel (30,9%), High sebanyak 697 sampel (29,1%), Low sebanyak 489 sampel (20,4%), Very High sebanyak 254 sampel (10,6%), None sebanyak 212 (8,9%). Hal ini menunjukkan bahwa support dari orang tua cenderung tinggi. 
- Extracurricular <br>
  ![image](https://github.com/user-attachments/assets/2b334673-8be2-407a-9ebf-2b98b028dc80) <br>
  Data dari kolom Extracurricular menunjukkan sebagian besar tidak mengikuti ekstrakurikuler, yaitu sebanyak 1475 (61,7%) dan sisanya yang mengikuti ekstrakurikuler sebanyak 917 (38,3%).
- Sports <br>
  ![image](https://github.com/user-attachments/assets/9ba29c8f-cd03-43d4-a14f-ea24e6b92a73) <br>
  Data dari kolom sports menunjukkan sebagian besar tidak mengikuti kegiatan olahraga, yaitu sebanyak 1666 (69,6%) dan yang mengikuti kegiatan olahraga sebanyak 726 (30,4%).
- Music <br>
  ![image](https://github.com/user-attachments/assets/908ccdbe-f0f1-49b7-81b3-3a581baf2614)<br>
  Persentase siswa yang mengikuti kegiatan musik sebanyak 80,3% (1921 sampel) dan yang tidak mengikuti sebanyak 19,7% (471 sampel). Hal ini menunjukkan bahwa dari data, hanya sedikit siswa yang mengikuti kegiatan musik.
- Volunteering <br>
  ![image](https://github.com/user-attachments/assets/c7850a39-5175-477a-b243-ab048d71850f) <br>
  Persentase siswa yang mengikuti kegiatan volunteering sebanyak 84,3% (2016 sampel) dan yang tidak mengikuti sebanyak 15,7% (376 sampel)
- Data numerik <br>
  ![image](https://github.com/user-attachments/assets/12a383eb-3419-4931-bc94-4f527f1e2991)<br>
  Informasi yang didapat adalah:
  - Penyebaran Age, StudyTimeWeekly, dan Absences terdistribusi secara merata. 
  - Penyebaran GPA berbentuk seperti lonceng (distribusi normal) dengan mayoritas data berada di antara 1,0 hingga 3,0.

### Explaratory Data Analysis - Multivariate Analysis
Rata-rate 'GPA' Relatif terhadap :
- Gender <br>
  ![image](https://github.com/user-attachments/assets/9bf15b0a-5961-4dd0-8631-2bd7ace6e2f5)
- Ethnicity <br>
  ![image](https://github.com/user-attachments/assets/2b1f0243-8e56-4e3e-922b-4d103926e87c)
- ParentalEducation <br>
  ![image](https://github.com/user-attachments/assets/6734912c-dfb5-4533-aea4-1cff013b150e)
- Tutoring <br>
  ![image](https://github.com/user-attachments/assets/dbcc3e58-fd43-4dac-9043-5bae58fcba53)
- ParentalSupport <br>
  ![image](https://github.com/user-attachments/assets/3e302512-008f-48e2-973f-a3d5d654242b)
- Extracurricular <br>
  ![image](https://github.com/user-attachments/assets/871aee5f-e105-464a-974a-8ad709d9b76c)
- Sports <br>
  ![image](https://github.com/user-attachments/assets/341c4257-0c76-4d23-b3d2-378c50399257)
- Music <br>
  ![image](https://github.com/user-attachments/assets/7995c246-21cb-4750-b978-1d29013e8fdc)
- Volunteering <br>
  ![image](https://github.com/user-attachments/assets/6d724fb3-6b2a-422f-a58e-34e28c8103e8)
- Data numerik <br>
  ![image](https://github.com/user-attachments/assets/e932d69e-cc96-4b3d-91cf-558ea04e3cc1)
- Correlation Matrix <br>
  ![image](https://github.com/user-attachments/assets/7c57538f-5c80-4fb4-8fe1-1de2fa14f671)

Kesimpulan: <br>
- Fitur Age, Gender, Ethnicity, dan Volunteering memiliki korelasi sangat kecil terhadap GPA sehingga bisa dihiraukan (drop).
- Fitur Absences menjadi fitur yang paling berpengaruh terhadap GPA dengan 0.92 poin pada bagian Correlation Matrix

## Data Preparation
Data Preparation adalah tahap untuk memproses data sebelum digunakan untuk training model. Data preparation yang dilakukan pada proyek ini adalah:
- drop kolom yang tidak berpengaruh atau tidak relevan
- encoding fitur kategori
- train test split
- standarisasi
### Drop Kolom yang Tidak Berpengaruh atau Tidak Relevan
Kolom yang dapat didrop pada dataset ini adalah: 
- StudentID: StudentID dapat didrop karena tidak berkaitan dengan tujuan untuk prediksi GPA. 
- GradeClass: GradeClass dapat didrop karena memberikan informasi yang sama dengan GPA tetapi hanya dalam format yang berbeda (GradeClass dalam bentuk kategorikal)
- Age: Age dapat didrop karena hasil dari multivariate analysis menunjukkan bahwa Age memiliki korelasi sangat kecil terhadap GPA. 
- Gender: Gender dapat didrop karena gender memiliki korelasi yang sangat kecil terhadap GPA dari hasil multivariate analysis. 
- Ethnicity: Ethnicity dapat didrop karena memiliki korelasi yang sangat kecil terhadap GPA dari hasil multivariate analysis. 
- Volunteering: Volunteering dapat didrop karena hasil multivariate analysis menunjukkan Volunteering memiliki korelasi yang sangat kecil terhadap GPA. 
### Encoding Fitur Kategori
Encoding fitur kategori perlu dilakukan karena sebagian besar model machine learning hanya dapat menerima data dalam bentuk numerik. Oleh karena itu, data dalam bentuk string atau object harus diubah terlebih dahulu menjadi bentuk numerik. Pada proyek ini, sebelumnya data kategorikal sudah berbentuk int64. Akan tetapi, karena sebelumnya diperlukan explaratory data analysis maka data diubah menjadi bentuk object (string). Pengembalian data menjadi data numerik dilakukan dengan mapping dari string ke index dari data awal. 
```py
# Mengembalikan ke index untuk persiapan training
df['ParentalEducation'] = df['ParentalEducation'].map(parental_education_to_index)
df['Tutoring'] = df['Tutoring'].map(bool_to_index_map)
df['ParentalSupport'] = df['ParentalSupport'].map(parental_support_to_index)
df['Extracurricular'] = df['Extracurricular'].map(bool_to_index_map)
df['Sports'] = df['Sports'].map(bool_to_index_map)
df['Music'] = df['Music'].map(bool_to_index_map)
```
### Train Test Split
Sebelum train test split dilakukan, dibuat terlebih dahulu variabel x dan y. Variabel x adalah variabel yang akan menyimpan berbagai fitur untuk melakukan prediksi, sedangkan variabel y digunakan untuk menyimpan label atau target dari hasil prediksi. Pada proyek ini, variabel x akan berisi: 
- ParentalEducation
- StudyTimeWeekly
- Absences
- Tutoring
- ParentalSupport
- Extracurricular
- Sports
- Music <br>

sedangkan variabel y akan berisi GPA yang merupakan target dari prediksi model. 
<br>
Train test split adalah metode untuk membagi data menjadi data train dan data test. Hal ini dilakukan agar model teruji melakukan prediksi pada data yang sebelumnya belum pernah dilihat. Hal ini penting untuk mengetahui kinerja model di dunia nyata terhadap data-data yang baru. Train test split yang dilakukan pada proyek ini adalah dengan perbandingan 70% data training dan 30% data test. Hasil pembagian menunjukkan dari 2392 data awal menjadi 1674 data untuk train dan 718 data untuk test.

### Standarisasi
Standarisasi adalah metode untuk mengubah distribusi data numerik sehingga memiliki rata-rata (mean) sebesar 0 dan standar deviasi sebesar 1. Proses ini dilakukan dengan mengurangi nilai mean dari setiap data dan membaginya dengan standar deviasi. Pada proyek ini, standarisasi dilakukan menggunakan StandardScaler dari sklearn. Standarisasi penting karena membantu model bekerja lebih optimal, terutama untuk algoritma yang sensitif terhadap skala fitur, seperti regresi linier atau SVM. Data yang tidak distandarkan dapat menyebabkan skala antar fitur berbeda, sehingga bobot antar fitur menjadi tidak seimbang. Selain itu, proses training model dapat menjadi lebih lambat atau sulit untuk mencapai konvergensi. Dalam proyek ini, fit_transform diterapkan pada data training untuk menghitung parameter statistik (mean dan standar deviasi) serta mentransformasi data, sedangkan transform diterapkan pada data test menggunakan parameter yang dihitung dari data training untuk menjaga konsistensi.
```py
from sklearn.preprocessing import StandardScaler
numerical_features = ['StudyTimeWeekly', 'Absences']
scaler = StandardScaler()
X_train[numerical_features] = scaler.fit_transform(X_train.loc[:, numerical_features])
X_test[numerical_features] = scaler.transform(X_test.loc[:, numerical_features])
```
## Modeling
### K-Nearest Neighbors Regressor
#### Cara Kerja
KNN bekerja dengan cara menghitung jarak antara data yang sedang diproses dengan semua data training. Model kemudian memilih "k" tetangga terdekat berdasarkan jarak tersebut. Nilai prediksi dihitung berdasarkan nilai target data dari tetangga tersebut. 
#### Tahapan Penerapan Model
1. Import library yang dibutuhkan
    ```py
    from sklearn.neighbors import KNeighborsRegressor
    from sklearn.metrics import mean_squared_error
    from sklearn.model_selection import GridSearchCV
    ```
2. Melakukan hyperparameter tuning dengan menggunakan Grid Search Cross Val<br>
    Grid Search Cross Val adalah metode untuk melakukan hyperparameter tuning dengan mencoba semua kombinasi parameter yang ditentukan dalam sebuah grid dan mengevaluasi performanya menggunakan cross-validation.
    ```py
    # Definisikan rentang nilai untuk n_neighbors
    param_grid = {'n_neighbors': range(1, 30), 'weights': ['uniform','distance']} 
    # Buat objek KNN dan GridSearchCV
    knn = KNeighborsRegressor()
    grid_search = GridSearchCV(knn, param_grid, cv=5, scoring='neg_mean_squared_error')
    ```
    Parameter yang bisa diatur untuk KNN pada proyek ini adalah: 
    - `n_neighbors` : jumlah k (tetangga) yang dipilih untuk membuat prediksi
    - `weights` : menentukan kontribusi setiap tetangga dalam memengaruhi prediksi. Uniform berarti semua tetangga memiliki bobot yang sama, terlepas dari jaraknya. Distance berarti memberikan bobot berdasarkan jarak: tetangga yang lebih dekat memiliki pengaruh lebih besar. Hasil dari Grid Search Cross Val menunjukkan sebagai berikut
    ```
    Best n_neighbors: 16
    Best weights: distance
    Best cross-validated MSE: 0.07808246633956835
    ```
    Hasil hyperparameter tuning akan disimpan dalam variabel `knn_best`
    ```py
    knn_best = grid_search.best_estimator_
    ```
#### Kelebihan
- Sederhana dan mudah dipahami
- Mudah beradaptasi saat sampel training baru ditambahkan karena data pelatihan sudah disimpan
- Memiliki sedikit hyperparameter

#### Kekurangan
- Sensitif terhadap nilai K yang dipilih. Nilai yang kurang tepat dapat menyebabkan overfitting atau underfitting. 
- Biaya komputasi yang besar karena harus menghitung jarak ke semua titik dalam data training
- Tidak cocok untuk data dengan dimensi tinggi (banyak fitur) karena jarak Euclidean menjadi kurang bermakna pada data berdimensi tinggi (_curse of dimensionality_)

### Random Forest Regressor
#### Cara Kerja
Random Forest Regressor bekerja dengan suatu teknik yang disebut bagging. Teknik ini dilakukan dengan menghasilkan banyak decision tree. Setiap tree akan melakukan prediksi secara independen untuk data input. Setelah itu, Random Forest akan menggabungkan prediksi dari setiap tree untuk menghasilkan output.
#### Tahapan Penerapan Model
1. Import library yang dibutuhkan
    ```py
    from sklearn.ensemble import RandomForestRegressor
    ```
2. Melakukan hyperparameter tuning dengan menggunakan Grid Search Cross Val
    ```py
    param_grid_rf = {
    'n_estimators': [100, 200, 300],
    'max_depth': [None, 10, 20, 30],
    'min_samples_split': [2, 5, 10],
    'min_samples_leaf': [1, 2, 4],
    'max_features': ['sqrt', 'log2'] 
    }
    rf = RandomForestRegressor()
    grid_search_rf = GridSearchCV(rf, param_grid_rf, cv=5, scoring='neg_mean_squared_error', verbose=1, n_jobs=-1)
    ```
    Parameter yang diatur dalam RandomForestRegressor pada proyek ini sebagai berikut.
    - `n_estimator`: jumlah Decision Tree yang akan dibuat dalam Random Forest.
    - `max_depth`: batas maksimum kedalaman tiap tree. Mengatur kedalaman dapat mencegah overfitting dengan membatasi kompleksitas tree. Nilai yang terlalu kecil dapat menyebabkan underfitting.
    - `min_samples_split`: jumlah minimum data sample yang diperlukan untuk membagi node internal.
    - `min_samples_leaf`: jumlah minimum data sample yang diperlukan untuk membentuk leaf (node terminal)
    - `max_features`: jumlah maksimum fitur yang dipertimbangkan untuk pembagian di setiap node. Ini membantu memperkenalkan variasi antar tree dalam random forest. 
      - sqrt: akar kuadrat dari total fitur
      - log2: logaritma dasar 2 dari total fitur
    

    Hasil dari hyperparameter tuning ini adalah sebagai berikut.
    ```
    Best RandomForest Parameters: {'max_depth': None, 'max_features': 'log2', 'min_samples_leaf': 1, 'min_samples_split': 2, 'n_estimators': 300}
    Best cross-validated MSE for RandomForest: 0.056103227833959504
    ```
    Hasil hyperparameter tuning ini akan disimpan pada variabel rf_best yang nantinya akan digunakan dalam training
    ```py
    rf_best = grid_search_rf.best_estimator_
    ```
#### Kelebihan
- Mengurangi risiko overfitting karena menggunakan kombinasi dari banyak pohon
- Dapat menangani secara akurat pada data nonlinear
- Feature Importance: dapat memberikan informasi pentingnya setiap fitur dalam membuat prediksi
#### Kekurangan
- Sulit diinterpretasikan karena gabungan dari banyak pohon
- Membutuhkan biaya komputasi yang besar terutama untuk dataset berukuran besar karena perlu membangun banyak decision tree
- Banyak parameter yang perlu dituning

### Gradient Boosting Regressor
#### Cara Kerja
Gradient Boosting Regressor adalah algoritma ensemble yang membangun model prediksi secara bertahap dengan fokus pada pengurangan error dari model sebelumnya. Pada setiap langkah, dibuat decision tree untuk melakukan optimasi terhadap error dari model sebelumnya. Hasil akhir dari model ini adalah kombinasi dari semua pohon bobot yang ditentukan oleh learning rate.
#### Tahapan Penerapan Model
1. Import library yang dibutuhkan
    ```py
    from sklearn.ensemble import GradientBoostingRegressor
    ```
2. Melakukan hyperparameter tuning dengan menggunakan Grid Search Cross Val
    ```py
    param_grid_gb = {
      'n_estimators': [50,100, 200, 300],
      'learning_rate': [1.0, 0.1, 0.01, 0.001],
      'max_depth': [2,3,4]
    }
    gb = GradientBoostingRegressor()
    grid_search_gb = GridSearchCV(gb, param_grid_gb, cv=5, scoring='neg_mean_squared_error', verbose=1, n_jobs=-1)
    ```
    Parameter yang diatur dalam Gradient Boosting Regressor sebagai berikut.
    - `n_estimators`: jumlah Decision Tree yang akan dibuat dalam Gradient Boosting Regressor.
    - `learning_rate`: mengontrol kontribusi setiap tree dalam memperbaiki kesalahan
    - `max_depth`: kedalaman maksimum setiap tree


    Hasil dari hyperparameter tuning sebagai berikut.
    ```
    Best GradientBoosting Parameters:  {'learning_rate': 0.1, 'max_depth': 2, 'n_estimators': 200}
    Best cross-validated MSE for GradientBoosting: 0.04330606590407221
    ```
    Hasil hyperparameter tuning ini akan disimpan dalam variabel gb_best yang akan digunakan untuk training
    ```py
    gb_best = grid_search_gb.best_estimator_
    ```
#### Kelebihan
- Akurasi tinggi karena ditrain berdasarkan error dari hasil sebelumnya.
- Dapat menangkap pattern yang kompleks dari data
- Tahan terhadap outliers 
#### Kekurangan
- Rentan terhadap noise dan dapat terjadi overfitting terhadap noise dalam data
- Sulit diinterpretasikan 
- Biaya komputasi besar terutama jika dataset besar atau tree memiliki kedalaman yang tinggi

### XGB Regressor
#### Cara Kerja
XGB Regressor adalah versi lebih efisien dan ditingkatkan dari Gradient Boosting Regressor. Keduanya menggunakan prinsip yang sama yaitu membangun Decision Tree secara bertahap dan berfokus pada error dari Tree sebelumnya. Akan tetapi, XGBoost memiliki beberapa perbedaan yaitu penggunaan second-order gradients untuk mempercepat pelatihan dan meningkatkan akurasi. XGB menyediakan fitur regularisasi (L1 dan L2) untuk menghindari overfitting yang tidak ada di Gradient Boosting Regressor standar. 

#### Tahapan Penerapan Model
1. Import library yang dibutuhkan
    ```py
    from xgboost import XGBRegressor
    ```
2. Melakukan hyperparameter tuning dengan menggunakan Grid Search Cross Val
    ```py
    param_grid_xgb = {
      'n_estimators': [100, 200, 300],
      'learning_rate': [1.0, 0.1, 0.01, 0.001],
      'max_depth': [3,5,7],
      'subsample': [0.7, 0.8, 0.9],
      'colsample_bytree': [0.7,0.8,0.9]
    }
    grid_search_xgb = GridSearchCV(xgb, param_grid_xgb, scoring='neg_mean_squared_error', cv=5, verbose=1, n_jobs=-1)
    ```
    Parameter yang diatur dalam XGBRegressor pada proyek ini sebagai berikut:
    - `n_estimators`: jumlah tree (decision trees) yang akan dibuat oleh model
    - `learning_rate`: mengontrol kontribusi setiap tree dalam memperbaiki kesalahan
    - `max_depth`: kedalaman maksimum setiap tree
    - `subsample`: proporsi data yang digunakan untuk melatih setiap tree
    - `colsample_bytree`: proporsi fitur yang dipilih secara acak untuk digunakan dalam pembentukan setiap tree
    
    
    Berdasarkan hasil cross val didapatkan hyperparameter tuning sebagai berikut.
    ```
    Best XGBoost Parameters:  {'colsample_bytree': 0.7, 'learning_rate': 0.1, 'max_depth': 3, 'n_estimators': 100, 'subsample': 0.9}
    Best cross-validated MSE for XGBoost: 0.0429376708045406
    ```
    Hyperparameter tuning disimpan dalam variabel xgb_best
    ```py
    xgb_best = grid_search_xgb.best_estimator_
    ```
#### Kelebihan
- Memiliki akurasi tinggi karena bekerja dengan membangun error dari Tree sebelumnya
- Memiliki kecepatan dan efisiensi lebih baik daripada Gradient Boosting Regressor
- Mempunyai regularisasi (L1 dan L2) untuk menghindari overfitting
#### Kekurangan
- Memiliki banyak hyperparameter yang perlu dituning
- Model sulit dipahami dan diinterpretasikan

### Support Vector Regression
#### Cara Kerja
SVR bekerja dengan mencari sebuah fungsi yang memiliki margin kesalahan terkecil. Margin ini didefinisikan sebagai data yang berada di luar batas toleransi (epsilon). SVR berusaha untuk menyesuaikan model agar sebanyak mungkin data tetap berada dalam margin sekaligus menjaga model tetap sesederhana mungkin.
#### Tahapan Penerapan Model
1. Import library yang dibutuhkan
    ```py
    from sklearn.svm import SVR
    ```
2. Melakukan hyperparameter tuning dengan menggunakan Grid Search Cross Val
    ```py
    param_grid_svr = {
        'C': [0.1, 1, 10, 100],           # Range nilai C
        'epsilon': [0.01, 0.1, 0.2, 0.5], # Range nilai epsilon
        'gamma': ['scale', 'auto', 0.1, 1] # Pilihan gamma: scale, auto, atau angka
    }
    grid_search_svr = GridSearchCV(svr, param_grid_svr, scoring='neg_mean_squared_error', cv=5, verbose=1, n_jobs=-1)
    ```
    Parameter yang diatur dalam Support Vector Regression pada proyek ini sebagai berikut:
    - `C`: parameter regularisasi yang mengontrol keseimbangan antara kesalahan di training data dan margin.
    - `epsilon`: zona toleransi (margin) di sekitar prediksi model. Error tidak dihitung selama prediksi berada dalam batas tersebut.
    - `gamma`: parameter kernel yang memengaruhi cakupan pengaruh setiap data point pada model.
    
    Berdasarkan hasil cross val didapatkan hyperparameter tuning sebagai berikut.
    ```
    Best SupportVectorRegression Parameters:  {'C': 1, 'epsilon': 0.1, 'gamma': 0.1}
    Best cross-validated MSE for SupportVectorRegression: 0.04316792974427414
    ```
    Hyperparameter tuning disimpan dalam variabel svr_best
    ```py
    svr_best = grid_search_svr.best_estimator_
    ```
#### Kelebihan
- Bekerja dengan baik pada data multi-dimensional
- Bekerja dengan baik pada dataset kecil
- Fleksibel karena margin toleransi dan kompleksitas model dapat diatur pada parameter C dan epsilon
#### Kekurangan
- Sensitif terhadap parameter C dan epsilon sehingga memerlukan eksperimen dan tuning yang tepat
- Waktu pelatihan lama dan tidak cocok untuk dataset besar 
### Model Terbaik
Model terbaik yang didapatkan adalah GradientBoosting. Hal ini dapat dilihat berdasarkan `test_mse` yang terkecil. 

## Evaluation
Metrik evaluasi yang digunakan dalam proyek ini adalah mean_squared_error (MSE). MSE umum digunakan untuk masalah regresi karena mengukur rata-rata error kuadrat antara nilai prediksi dan nilai aktual dalam regresi. MSE diformulasikan sebagai berikut. <br>
![image](https://github.com/user-attachments/assets/ed3e3edf-008b-4923-862a-1e3022f5126b)

MSE bekerja dengan mengukur besar error dari setiap prediksi lalu menghitungnya berdasarkan formula di atas. MSE secara sederhana berarti besar error rata-rata dari hasil prediksi dengan kenyataan. Nilai MSE yang semakin kecil menunjukkan hasil model yang semakin baik. Hasil MSE dari setiap model dapat dilihat pada tabel berikut. `test_mse` dapat dijadikan acuan karena menunjukkan performa model di dunia nyata berbeda dengan `train_mse`. Hasil `test_mse` menunjukkan kemampuan model dalam menghindari overfitting dan generalization terhadap data-data baru yang belum dilihat oleh model sebelumnya. Hasil seluruh model dirangkum dalam tabel di bawah ini.
|           |       KNN |   RandomForest |   GradientBoosting |   XGBoost |   SupportVectorRegression |
|:----------|----------:|---------------:|-------------------:|----------:|--------------------------:|
| **train_mse** | 0.0      |     0.007507   |       0.055534  | 0.029742 |                 0.035521 |
| **test_mse**  | 0.077413 |     0.055534   |        0.041823 | 0.042595 |                 0.042754 |

Berdasarkan MSE tersebut, didapatkan informasi sebagai berikut:
- hasil model terbaik adalah **XGBoost** dengan test_mse terkecil yaitu 0.041823. Nilai 0.041823 jika digunakan untuk prediksi GPA dalam rentang 0.0 hingga 4.0 menunjukkan hasil yang baik. 
- test_mse yang baik menunjukkan bahwa model memberi performa yang baik dalam situasi di dunia nyata. 
- Hasil KNN dengan train_mse yang kecil tetapi tidak sebanding dengan test_mse menunjukkan bahwa model cenderung overfit. 

## Kesimpulan

Kesimpulan dari proyek ini sebagai berikut.
- Berdasarkan, correlation matrix didapatkan bahwa absences adalah fitur yang paling berpengaruh terhadap GPA.
- Model machine learning yang paling tepat untuk prediksi GPA dari dataset ini adalah XGBoost dengan parameter sebagai berikut.
  ```py
  'colsample_bytree': 0.7, 
  'learning_rate': 0.1, 
  'max_depth': 3, 
  'n_estimators': 100, 
  'subsample': 0.9
  ```
  Hasil dari test_val pada GPA dengan model ini adalah ```0.041583```
## Referensi
[Educational Data Mining: A Review and Analysis of Student’s Academic Performance](https://www.researchgate.net/publication/341259033_Educational_Data_Mining_A_Review_and_Analysis_of_Student's_Academic_Performance)
