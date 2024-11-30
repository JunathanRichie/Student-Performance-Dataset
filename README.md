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
- StudentID : merupakan penanda unik dari setiap siswa dalam rentang 1001 - 3392
- Age : merupakan umur dari setiap siswa dalam rentang 15 - 18 tahun
- Ethnicity: merupakan kelompok etnis dari siswa yang dikodekan sebagai berikut: 
0: Caucasian
1: African American
2: Asian
3: Other
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data atau exploratory data analysis.

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