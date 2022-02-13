# Laporan Proyek Machine Learning - Haryo Dwi Setyoputro
## Domain Proyek

Proyek Machine Learning ini dibuat untuk memenuhi submission kelas Machine Learning Terapan yang diselenggarakan oleh Dicoding Academy. 

## Business Understanding

Dalam dunia perdagangan saham, tentu harga saham perusahaan yang diperdagangkan di bursa saham mengalami fluktuasi setiap harinya. Kadangkala harganya naik, kadangkala pula harganya mengalami penurunan. Para investor, yaitu orang yang melakukan jual beli saham, sangat berharap bisa mendapatkan keuntungan ketika mereka menjual/membeli saham mereka, dan berharap juga mendapatkan saham yang bagus dengan harga yang murah, sehingga bisa mendatangkan keuntungan yang lebih besar di masa mendatang. 

Seringkali fluktuasi harga saham itu sulit diprediksi secara manual, sehingga menimbulkan kebingungan bagi para pelaku pasar saham mengenai kapankah saat terbaik untuk menjual atau membeli saham tertentu, agar bisa mendatangkan keuntungan yang diharapkan. Di zaman teknologi seperti sekarang ini, untungnya kita punya machine learning. Dengan adanya teknologi machine learning kita dapat membuat model yang dapat memprediksi harga tertinggi dari suatu saham pada esok hari maupun beberapa hari kedepan. Hal itu tentunya akan mempermudah trader maupun investor, apalagi yang masih baru. Metrik yang digunakan untuk mengevaluasi model machine learning ini adalah Root Mean Square Error (RMSE). Root Mean Squared Error (RMSE) merupakan salah satu cara untuk mengevaluasi model regresi linear dengan mengukur tingkat akurasi hasil perkiraan suatu model. RMSE dihitung dengan mengkuadratkan error (prediksi – observasi) dibagi dengan jumlah data (= rata-rata), lalu diakarkan. RMSE tidak memiliki satuan.


### Problem Statements

Ada beberapa permasalahan yang dinyatakan dari proyek ini : 
- Bagaimana cara untuk memprediksi harga saham beberapa hari ke depan dengan akurat?
- Apakah penggunaan model machine learning dapat membantu memecahkan permasalahan tersebut?
- Bagaimana cara membuat model machine learning yang baik tersebut?

### Goals

Dalam proyek ini, akan dicoba untuk menjawab pertanyaan pada problem statements di atas, yaitu : Membuat model machine learning yang mampu memprediksi harga saham di masa depan, untuk kasus ini, dalam skala hari, dengan akurat. 

 
 ### Solution statements

Dalam proyek ini dibangun model machine learning yang menggunakan algoritma Long Short Term Memory Network (LSTM), untuk memprediksi harga tertinggi saham pada hari tertentu. LSTM ini mampu mempelajari data historis, sehingga termasuk kategori time series. LSTM merupakan tipe Recurrent Neural Network, yang sangat cocok menggolongkan, memroses, dan memperkirakan deret waktu dengan durasi yang tidak diketahui. Maka metode ini cocok untuk memprediksi harga tertinggi saham pada beberapa hari berikutnya. Pada akhir proyek akan dibandingkan data hasil prediksi dan data sebenarnya untuk memeriksa keakuratan model.

## Data Understanding

Proyek ini menggunakan dataset saham perusahaan-perusahaan smartphone ternama yang dapat diunduh pada link: https://www.kaggle.com/haryodwi/saham-smartphone
Ini adalah dataset yang menunjukkan fluktuasi harga saham perusahaan smartphone ternama, seperti Samsung, Alcatel, Xiaomi, Apple dan lainnya dalam kurun waktu tahun 2016 hingga 2021. Untuk proyek ini, kita akan mencoba menggunakan dataset harga saham perusahaan Apple. Dataset Apple ini memiliki format .csv dengan 1258 baris dan 7 kolom. Dan setelah diperiksa, tidak ditemukan data null ataupun missing value. 

### Ada 6 parameter yang terdapat pada dataset ini : 
- Date : Menunjukkan waktu dalam satuan hari
- Open : Harga pembukaan/awal saham Apple pada hari tersebut
- High : Harga tertinggi saham Apple dihari tersebut
- Low : Harga terendah saham Apple dihari tersebut
- Close : Harga penutupan/akhir saham Apple dihari tersebut
- Adj Close : Adjusted close adalah harga penutupan setelah penyesuaian untuk semua pembagian dan pembagian dividen yang berlaku.
- Volume : Jumlah sekuritas yang diperdagangkan selama periode waktu tertentu.

 
## Data Preparation
- Pada tahap ini kita memisahkan data dengan menggunakan fungsi filter, karena kita hanya memerlukan data harga High (harga tertinggi) saham Apple setiap harinya, kita bisa masukkan ke dalam dataframe baru, dengan nama variable 'dataDf'. Setelah itu, dicek ulang apakah ada data yang berubah. Data masih masih seperti semula dengan tidak adanya nilai null dan berjumlah 1258 data. Setelah itu rubah data ke array numpy dan kita perlu mendapatkan beberapa baris untuk dilakukannya training.

- Proses selanjutnya adalah membuat training dataset. Pada pembuatan training dataset akan dilakukan proses scaled dan membagi dataset menjadi 2 buah unit train. X dan Y train. Keduanya akan dirubah kedalam numpy array dan akan dilakukan penyesuaian dimensi menggunakan reshape sehingga pemrosesan akan menjadi lebih mudah.

- Setelah data frame terubah menjadi array, kita akan melakukan scalling data/normalisasi data dengan MinMaxScaler. MinMaxScaler akan membuat data berada pada rentang 0-1

 
## Modeling
Pada tahap modeling, machine learning ini menggunakan algoritma Long Short Term Memory Network (LTSM) dalam memprediksi harga tertingginya. LSTM merupakan tipe Recurrent Neural Network yang dapat mempelajari data historis atau time series. Ia merupakan algoritma deep learning yang kompleks dan dapat mempelajari informasi jangka panjang dengan sangat baik. Pada modeling LSTM digunakan 2 layer LSTM dengan tiap layernya menggunakan 128 dan 64 hidden unit. Hyperparameter yang digunakan selanjutnya adalah digunakanya 2 buah dense layer dengan epoch sebesar 25 dan batch_size =1.


## Evaluation
Setelah modeling dan training selesai, yang kita lakukan adalah proses evaluasi : 

- **Membuat testing data dan ubah ke numpy array, kemudian reshape**

Membuat testing data set dengan nilai yang telah discale sebelumnya. Dilanjutkan dengan proses membuat data sets x_test dan y_test,merubahnya ke numpy array dan melakukan reshape.

- **Melakukan prediksi**

Untuk mendapatkan data prediksi kita menggunakan formula 'model.predict(x_test)'. Hasilnya akan bisa digunakan untuk mendapatkan root mean squared error.

- **Mendapatkan root mean squared error (RMSE)**

Pada project machine learning ini menggunakan matriks Root mean squared error (RMSE). RMSE adalah aturan penilaian kuadrat yang juga mengukur besarnya rata-rata kesalahan. Ini adalah akar kuadrat dari rata-rata perbedaan kuadrat antara prediksi dan observasi aktual. Root Mean Squared Error (RMSE) merupakan salah satu cara untuk mengevaluasi model regresi linear dengan mengukur tingkat akurasi hasil perkiraan suatu model. Nilai RMSE rendah menunjukkan bahwa variasi nilai yang dihasilkan oleh suatu model prakiraan mendekati variasi nilai obeservasinya. RMSE menghitung seberapa berbedanya seperangkat nilai. Semakin kecil nilai RMSE, semakin dekat nilai yang diprediksi dan diamati. Model machine learning menggunakan algoritma LSTM ini menghasilkan nilai RMSE sebesar 1.9005831524226937. Hal tersebut menunjukkan bahwa model machine learning ini layak untuk diterapkan.

- **Melakukan plot data**

![download](https://user-images.githubusercontent.com/85089960/153745849-62d5fd7a-2848-42b3-a659-0e4fed4005e4.png)

Kita melakukan visualisasi untuk melihat keakuratan model prediksi dengan membandingkan garis prediksi dengan garis valid. Dari grafik bisa dilihat bahwa pola hasil prediksi cukup mendekati hasil sebenarnya (valid). Selain itu dalam tabel harga juga terlihat bahwa hasil prediksi pada kolom "Predictions" cukup mendekati hasil dari kolom "High". Hal ini menunjukkan bahwa model machine learning ini layak untuk diterapkan untuk memprediksi harga saham Apple.
