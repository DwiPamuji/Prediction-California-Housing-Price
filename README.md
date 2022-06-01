# California Housing Price
source : [data_california_house.csv](https://drive.google.com/file/d/1NJ7DsgZ3zIdZWTz17RQWgbtDBuk1JVg3/view)

# Content
1. Business Problem Understanding
1. Data Understanding
1. Data Preprocessing
1. Exploration Data Analysis
1. Modeling
1. Hyperparameter Tuning
1. Compare KNN Tuning Predict dengan Actual
1. Kesimpulan
1. Rekomendasi
1. Using Machine Learning
*****

**Context**

Tempat tinggal merupakan kebutuhan pokok setiap manusia. Tetapi tidak semua orang memiliki pengetahuan tentang harga rumah yang sesuai dengan value yang di berikan. Di setiap negara cukup sulit untuk orang awam mengetahui harga rumah yang memiliki harga yang sesuai dengan value yang di berikan rumah atau perumahan tsb. Begitupun di negara california yang memiliki 50 lebih daerah yang tentunya tiap daerah memiliki harga rumah yang berbeda-beda. Fenomena ini menjadi kesempatan dan tantangan tersendiri untuk para developer perumahan untuk dapat membangun perumahan yang memiliki harga yang dapat bersaing di daerah tersebut dan tentunya memiliki value yang sesuai.

**Problem Statement**

Tantangan terbesar untuk para developer perumahan adalah membangun rumah dengan harga dan value rumah yang kompetitif dengan perumahan yang ada di sekitar daerah tersebut. **Sehingga rumah yang di tawarkan atau di bangun oleh developer dapat memberikan keuntungan financial yang maksimal dan rumah yang di bangun juga dapat terjual dengan cepat.**

**Goals**

Developer perumahan perlu memiliki 'tool' yang dapat memprediksi serta membantu mereka untuk dapat **menentukan harga dan value rumah yang akan mereka bangun** adanya perbedaan jumlah kamar, jumlah kamar mandi dan rata" atau median penghasilan masyarakat pada suatu perumahan akan membantu dalam memprediksi harga wajar suatu perumahan di suatu daerah. Yang mana akan mendatangkan profit untuk developer perumahan dan tentunya dengan harga yang kompetitif dan terjangkau orang masyarakat di daerah tersebut.

**Analytic Approach**

Jadi, yang perlu kita lakukan adalah menganalisis data untuk dapat menemukan pola dari fitur - fitur yang ada, yang membedakan satu perumahan dengan perumahan lainnya.

Selanjutnya, kita akan membangun suatu model regresi yang akan membantu Developer Perumahan untuk dapat menyediakan 'tool' prediksi harga rumah yang akan mereka bangun, **yang mana akan berguna untuk developer memperkirakan budget untuk membangun perumahan secara maksimal agar dapat menghasilkan keuntungan finansial yang maksimal dan tentunya dengan value yang dapat bersaing di daerah tersebut.**

**Metric Evaluation**

Evaluasi metrik yang akan digunakan adalah RMSE, MAE, MAPE dan R-Squared, di mana RMSE adalah nilai rataan akar kuadrat dari error, MAE adalah rataan nilai absolut dari error, sedangkan MAPE adalah rataan persentase error yang dihasilkan oleh model regresi. Semakin kecil nilai RMSE, MAE, MAPE yang dihasilkan, berarti model semakin akurat dalam memprediksi harga sewa sesuai dengan limitasi fitur yang digunakan. sedangan R-squared digunakan untuk mengetahui seberapa baik model dapat merepresentasikan varians keseluruhan data. Semakin mendekati 1, maka semakin fit pula modelnya terhadap data observasi. Namun, metrik ini tidak valid untuk model non-linear.

# Data Understanding

> ## Dataset 1 (```data_california_house.csv```)
- dataset merupakan hasil surve sensus perumahan di california pada tahun 1990
- setiap data dalam dataset menginformasikan terkait perumahan dan populasi perumahan

**Attributes Information**

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| longitude | float64 | Koordinat garis bujur |
| latitude | float64 | Koordinat garis lintang |
| housing_median_age | float64 | Median Umur Rumah |
| total_rooms | float64 | Total Ruangan |
| total_bedrooms | float64 | Total Kamar Tidur |
| population | float64 | Populassi Perumahan |
| households | float64 | Total Rumah Tangga |
| median_income | float64 | Median pendapatan dengan satuan sepuluh ribu US Dollar |
| ocean_proximity | object  | Jarak Perumahan dari Laut |
| median_house_value | float64 | Median Harga Rumah dengan satuan US dollar |

longitude	latitude	housing_median_age	total_rooms	total_bedrooms	population	households	median_income	ocean_proximity	median_house_value

> ## Dataset 2 (```Data_JALAN_KOTA_DAERAH.csv```)
- dataset ini merupakan interpretasi lokasi perumahan yang di dapat dari mengolah feature ```Latitude```, ```Longitude``` menggunakan library geopy.geocoders yang menghasilkan feature ```road```,	```county```,	```city```,	dan ```state``` 

**Attributes Information**

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| road | object | Lokasi Jalan Perumahan |
| county | object | Lokasi Daerah Perumahan |
| city | object | Lokasi Kota Perumahan |
| state | object | Negara Perumahan |

# Data Preprocessing

ada 2 data set yang akan di gabung kan yaitu :
1. Dataset ```data_california_house.csv```
2. Dataset ```Data_JALAN_KOTA_DAERAH.csv``` yang berisi feature ```road```, ```county```, ```city```, dan ```state``` yang di olah dari feature ```longtitude``` dan ```latitude``` dari dataset ```data_california_house.csv```. 

Alasan saya membuat feature baru dengan dataset baru karena proses pengolahan convert dari feature ```longtitude``` dan ```latitude``` menjadi feature ```road```, ```county```, ```city```, dan ```state``` memakan waktu yang relatif lama sehingga akan lebih efektif bisa prosesnya saya lakukan di file yang berbeda. file ```ipymb``` juga akan saya lampirkan

> ## Missing Value
beberapa feature yang memiliki missing value dan jumlah missing value sebagai berikut: 
1. total_bedrooms ----- 137
2. road --------------- 732
3. county ------------- 387
4. city --------------- 5858

> ## Handling Missing Value

1. total_bedrooms ----- Di input dengan nilai median pada feature total_bedrooms
2. road --------------- Di drop
3. county ------------- Di input dengan value "San Fransisco County"
4. city --------------- Di drop

# EDA 

![image](https://user-images.githubusercontent.com/7431442/171388711-a5efcd46-9dc5-492f-ba52-5e5263366e52.png)
![image](https://user-images.githubusercontent.com/7431442/171388861-02465b8c-de0f-4a2f-8788-932ed925b173.png)
![image](https://user-images.githubusercontent.com/7431442/171388906-ea4e301f-0f33-4432-93e5-6ddc10a4def8.png)

Dari 3 plot di atas dapat di simpulkan bahwa :
1. Harga rumah sangat terpengaruh oleh lokasi dan kepadatan penduduknya
1. Tidak semua rumah yang berlokasi dekat dengan laut memiliki harga yang tinggi

> ## Data Correlation

![image](https://user-images.githubusercontent.com/7431442/171389318-d4cf527a-e9ab-40fb-815a-75e2ae5ae939.png)
![image](https://user-images.githubusercontent.com/7431442/171389731-314ef260-bafc-4b5c-99dd-949ec6673a25.png)

Dari plot correlation matrix di atas terlihat bahwa hanya feature ```median_income``` saja yang memiliki nilai korelasi yang cukup tinggi terhadap feature ```median_house_value```. dimana korelasinya adalah positif dimana tiap kenaikan ```median_income``` semakin meningkat pula niali ```median_house_value``` atau semakin tinggi pendapatan penduduk akan semakin tinggi harga rumah di daerah tersebut.

> ## Outlier

![image](https://user-images.githubusercontent.com/7431442/171391972-d6cf4b5c-0aaa-4760-ab4a-3155f80409cf.png)

gambar di atas adalah data outlier, data yang akan di hapus adalah data yang melewati garis merah

Distribusi Sebelum outlier di hapus
![image](https://user-images.githubusercontent.com/7431442/171392500-61664547-f161-4ed6-a780-8b32c51f05f9.png)

Distribusi Setelah outlier di hapus
![image](https://user-images.githubusercontent.com/7431442/171392688-7bbd8a93-b5ad-42b8-be6e-df0e159e2ca7.png)

# Modeling
ada 9 model yang di uji. berikut hasil cross validation score dari matric RMSE dan MAE :

![image](https://user-images.githubusercontent.com/7431442/171393123-603a7990-fd7e-4a5c-bffd-70c30b73dd2f.png)

hasil uji dengan data test 2 model yang terbaik yang akan di hyperparam :

![image](https://user-images.githubusercontent.com/7431442/171393401-27469ecc-2b47-4db5-b828-02fbb0fcbbe6.png)

# Compare hasil Tunning KNN dan XGBoost
compare hasil sebelum dan sesudah tunning

![image](https://user-images.githubusercontent.com/7431442/171393613-303ab865-83fb-4dd7-94df-52eb8b9a28c0.png)

scaterplot compare KNN tuning dan XGBoost tuning

![image](https://user-images.githubusercontent.com/7431442/171393882-48df9301-9ccd-440a-b4e7-de4645a913cc.png)

KNN tuning menghsilkan data predict yang lebih baik di banding terlihat pada XGBoost tuning memiliki data predict yang lebih bias

# Compare hasil Predict KNN Tuning dengan data Actual

Berikut grafik perbandingan KNN Predict dengan data Actual

![image](https://user-images.githubusercontent.com/7431442/171394564-a3f64853-25e9-46e5-a003-739f6856cf1c.png)
![image](https://user-images.githubusercontent.com/7431442/171394615-ad4b25b4-0aa8-4346-901b-970b85ec0a30.png)

Untuk mengetahui hasil lebih lanjut akan di jelaskan pada file python di dalam repository.








