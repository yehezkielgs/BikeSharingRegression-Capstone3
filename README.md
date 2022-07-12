# Bike Sharing Regression Machine Learning (Capstone Module 3)

Capstone Project merupakan salah satu project yang diberikan sebagai penilaian terhadap pemahaman siswa Purwadhika terhadap modul yang telah dipelajari. Pada Capstone project ini, saya ditugaskan untuk membangun sebuah model machine learning regresi dengan menggunakan data Bike Sharing, yaitu data jasa penyewaan sepeda.

Dataset source: https://drive.google.com/drive/folders/1Qk9VJXpVlYnZofzRmH5z15Kpi-5M8KOv

# Contents
1. Business Problem Understanding
2. Data Understanding
3. Data Preprocessing
4. Modeling
5. Conclusion
6. Recommendation

# Business Problem Understanding

Sistem Bike-sharing merupakan generasi baru dari rental sepeda dimana seluruh proses dari keanggotaan, penyewaan, dan pengembalian telah dilakukan secara otomatis. Melalui sistem ini, pengguna dapat dengan mudah menyewa sepeda dari tempat tertentu dan mengembalikannya di tempat lain.

Sebuah perusahaan penyedia bike-sharing sedang mengembangkan bisnisnya dan berusaha untuk meningkatkan pendapatan yang dimiliki. Oleh karena itu, perusahaan memutuskan untuk menyiapkan sebuah strategi bisnis yang tepat untuk meningkatkan pendapatannya. Dalam menyiapkan hal tersebut, perusahaan ingin memahami mengenai permintaan masyarakat terhadap rental sepeda. Dengan memahami hal tersebut, perusahaan berencana untuk mempersiapkan diri untuk memenuhi kebutuhan masyarakat.

Perusahaan melakukan kontrak dengan perusahaan konsultan pada bidang data untuk mengetahui faktor-faktor yang mempengaruhi permintaan terhadap rental sepeda, secara khusus di Amerika. Perusahaan ingin mengetahui variabel yang signifikan dalam memprediksi permintaan rental sepeda dan seberapa baik variabel tersebut menjelaskan permintaan terhadap rental sepeda. Perusahaan juga ingin mengetahui jumlah sepeda yang harus disiapkan dengan tepat sesuai dengan kebutuhan masyarakat pada berbagai kondisi cuaca.

# Data Understanding
*   Dataset merupakan data jumlah penyewaan sepeda pada tahun 2011-2012 di Amerika
*   Setiap baris data merepresentasikan informasi terkait penyewaan sepeda per hari

**Attributes Information**

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| dteday | Datetime | date |
| hum | Float | Normalized humidity. The values are divided to 100 (max) |
| weathersit | Integer |  weather  <br>1 =  Clear, Few clouds, Partly cloudy, Partly cloudy<br>2 = Mist + Cloudy, Mist + Broken clouds, Mist + Few clouds, Mist<br>3 = Light Snow, Light Rain + Thunderstorm + Scattered clouds, Light Rain +   Scattered clouds<br>4 = Heavy Rain + Ice Pallets + Thunderstorm + Mist, Snow + Fog|
| holiday | Integer | holiday or not |
| season | Integer | season <br>1: winter<br>2: spring<br>3: summer<br>4: fall |
| atemp | Float | Normalized feeling temperature in Celsius. The values are derived via (t-tmin)/(tmax-tmin), tmin=-16, t_max=+50 (only in hourly scale) |
| temp | Float | Normalized temperature in Celsius. The values are derived via (t-tmin)/(tmax-tmin), tmin=-8, t_max=+39 (only in hourly scale) |
| hr | Integer | hour (0 to 23) |
| casual | Integer | count of casual users |
| registered | Integer | count of registered users |
| cnt | Integer | count of total rental bikes including both casual and registered |

# Data Preprocessing
* Penambahan fitur month, year, weekday yang diambil dari dteday
* Merubah tipe data weekday, weathersit, dan season menjadi category
* Menghapus feature atemp, dteday, casual, dan registered
* Menghapus nilai-nilai dari fitur yang bersifat tidak wajar
* Menghapus data-data outlier
* Melakukan encoding pada feature weathersit, season, dan weekday

# Modeling

**Crossvalidation Benchmark model:**
| Model                  | Mean_RMSE   | Std_RMSE | Mean_MAE   | Std_MAE  | Mean_MAPE | Std_MAPE | 
|------------------------|-------------|----------|------------|----------|-----------|----------| 
| Linear Regression      | -144.595706 | 5.330292 | -98.243649 | 3.776170 | -1.381328 | 0.066783 | 
| KNN Regressor          | -106.786115 | 5.938299 | -68.723053 | 3.020746 | -1.173354 | 0.107881 | 
| DecisionTree Regressor | -66.614069  | 3.828002 | -39.279856 | 2.016847 | -0.419450 | 0.020103 | 
| RandomForest Regressor | -49.064595  | 3.641531 | -29.632434 | 1.924376 | -0.304830 | 0.013771 | 
| XGBoost Regressor      | -43.589906  | 2.925081 | -26.596861 | 1.486055 | -0.266885 | 0.014754 | 

**Predict to Test Set:**
| Model        | RMSE      | MAE       | MAPE     | 
|--------------|-----------|-----------|----------| 
| RandomForest | 43.667138 | 26.880957 | 0.297829 | 
| XGB Before Tuning          | 39.528571 | 24.836749 | 0.255728 |		
| XGB AFter Tuning          | 42.987601 | 27.080498 | 0.390707 |

# Conclusion

*   Berdasarkan pemodelan yang telah dilakukan, jam merupakan fitur yang paling berpengaruh terhadap jumlah rental sepeda, dilanjutkan dengan tahun dan hari.
*   Metrik evaluasi yang digunakan pada model adalah nilai RMSE, MAE & MAPE. Jika ditinjau dari nilai RMSE yang dihasilkan oleh model, yaitu sebesar 42.9, kita dapat menyimpulkan bahwa bila nanti model yang kita buat ini digunakan untuk memperkirakan jumlah rental sepeda baru pada rentang nilai seperti yang dilatih terhadap model (maksimal jumlah rental sepeda 645), maka perkiraan jumlah rental sepedanya rata-rata akan meleset kurang lebih sebesar 42.9 dari jumlah rental sepeda yang mungkin seharusnya. Tetapi, tidak menutup kemungkinan juga prediksinya meleset lebih jauh karena bias yang dihasilkan model masih cukup tinggi bila dilihat dari visualisasi antara jumlah rental sepeda aktual dan prediksi.

# Recommendation

Hal-hal yang dapat dilakukan untuk mengembangkan model agar lebih baik lagi, seperti:

1. Melakukan pengelompokan terhadap prediksi yang nilai error yang tinggi baik yang bersifat overestimation dan underestimation. Selanjutnya, kita dapat mmemeriksa hubungan antara error tersebut dengan tiap variabel independen. Hal tersebut dilakukan untuk mengetahui variabel mana saja dan aspek apa yang menyebabkan model menghasilkan error yang tinggi.
<br><br>   
1. Model memerlukan penambahan fitur yang lebih korelatif dengan jumlah rental sepeda, terkait karakteristik perilaku pengguna, lokasi, dan biaya rental sepeda. Selain itu, penambahan data terkini terkait rental sepeda juga dapat meningkatkan kualitas model.
<br><br>   

