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

- Berdasarkan data tersebut, kolom StudentID dapat didrop karena tidak memiliki keterkaitan dengan tujuan. Selain itu, kolom GradeClass juga dapat didrop karena menunjukkan hal yang sama dengan GPA tetapi hanya berbeda format. 
  ```py
  # Drop StudentID Column karena tidak memiliki keterkaitan dengan tujuan
  df=df.drop(labels="StudentID", axis=1)
  # Drop GradeClass Column karena menunjukkan hal yang sama dengan academic performance
  df=df.drop(labels="GradeClass", axis=1)
  ```
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
  ![image](https://github.com/user-attachments/assets/40f422f9-90e0-4908-9a6a-c43481bd026b)

- Ethnicity <br>
  ![image](https://github.com/user-attachments/assets/47b5b236-f875-4298-848a-0bfbf1327c34)

- ParentalEducation <br>
  ![image](https://github.com/user-attachments/assets/6a18af14-6c24-4a66-b117-0e64fa978302)

- Tutoring <br>
  ![image](https://github.com/user-attachments/assets/749277c4-17c4-471e-b7e9-3ad6ab81937e)

- ParentalSupport <br>
  ![image](https://github.com/user-attachments/assets/e4f82c08-2d36-44d8-b077-c7994ec57d19)

- Extracurricular <br>
  ![image](https://github.com/user-attachments/assets/2b334673-8be2-407a-9ebf-2b98b028dc80)

- Sports <br>
  ![image](https://github.com/user-attachments/assets/9ba29c8f-cd03-43d4-a14f-ea24e6b92a73)

- Music <br>
  ![image](https://github.com/user-attachments/assets/908ccdbe-f0f1-49b7-81b3-3a581baf2614)
- Volunteering <br>
  ![image](https://github.com/user-attachments/assets/c7850a39-5175-477a-b243-ab048d71850f)
- Data numerik <br>
  ![image](https://github.com/user-attachments/assets/12a383eb-3419-4931-bc94-4f527f1e2991)

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


## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
- Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. **Jelaskan proses improvement yang dilakukan**.
- Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. **Jelaskan mengapa memilih model tersebut sebagai model terbaik**.

## Evaluation
Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.

Sebagai contoh, Anda memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Penjelasan mengenai metrik yang digunakan
- Menjelaskan hasil proyek berdasarkan metrik evaluasi

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

## Referensi
[Educational Data Mining: A Review and Analysis of Student’s Academic Performance](https://www.researchgate.net/publication/341259033_Educational_Data_Mining_A_Review_and_Analysis_of_Student's_Academic_Performance)
