# Delivery Performance Analysis and Delivery Time Prediction Based on Olist Dataset.

## Latar Belakang:
- Studi McKinsey mendefinisikan e-commerce sebagai **proses jual beli barang fisik secara online** yang dibagi kembali menjadi dua kategori, yaitu:
    - E-tailing, yaitu jual beli formal melalui platform online yang **didesain untuk memfasilitasi transaksi** seperti Bukalapak dan Tokopedia.
    - Social commerce, yaitu **pemasaran barang melalui media sosial** seperti Facebook atau Instagram dengan pembayaran dan pengiriman dilaksanakan melalui platform lain.
- E-commerce juga merupakan industri yang terbukti tahan dalam situasi pandemi belakangan ini.
- Salah satu faktor utama pendukung keberhasilan bisnis e-commerce adalah performa pengiriman barang (Delivery Performance).
- Delivery Performance dapat dimaknai dengan:
    - Ketepatan pengiriman terhadap estimasi waktu  yang diberikan oleh perusahaan e-commerce.
    - Seberapa cepat waktu pengiriman terhadap jarak yang di tempuh antara penjual dan pembeli.
- Berdasarkan data diatas maka penulis ingin melakukan penelitian mengenai **“Delivery Performance Analysis and Delivery Time Prediction Based on Olist Dataset”**.

## Bisnis Problem.
- Berdasarkan Latar Belakang sebelumnya, penulis memiliki beberapa bisnis problem mengenai **Delivery Performance**, yaitu:
    - Bagaimana hubungan faktor yang ada di dataset dengan waktu pengiriman?
    - Bagaimana hubungan faktor yang ada di dataset kecepatan pengiriman?
    - Seberapa tepat delivery performance dari Olist terhadap waktu estimasi pengiriman?
    - Adakah hubungan antara delivery performance terhadap kepuasan pelanggan?
    - Seberapa tepat ML yang dapat dibuat untuk menentukan waktu pengiriman (Delivery Time)?
    
## Dataset
- Dataset yang digunakan merupakan public dataset yang dikeluarkan oleh Olist dari tahun 2016 – 2018.
- Olist merupakan perusahaan asal Brazil yang bergerak di bidang e-commerce melalui marketplace.
- Olist memiliki 9000 lebih tenant dan lebih dari 2 juta pelanggan di seluruh Brazil.
- Sumber dataset yang di gunakan dari Kaggle dengan link: https://www.kaggle.com/olistbr/brazilian-ecommerce
- Dari dataset tersebut memiliki 9 dataset dalam bentuk csv, yang akan digabungkan ke dalam satu dataset dan akan di seleksi fitur apa saja yang dibutuhkan untuk pengerjaan **Delivery Performance Analysis and Delivery Time Prediction Based on Olist Dataset**, dengan penjelasan singkat tiap dataset sebagai berikut:
    - olist_customers_dataset: Dataset ini memberi informasi mengenai *customer* dan lokasinya.
    - olist_geolocation_dataset: Dataset ini memberi informasi mengenai kode pos di negara Brazil, kordinat long/lat, yang dapat digunakan untuk menghitung jarak antara penjual dan *customer*.
    - olist_order_items_dataset: Dataset ini berisi data tentang item yang dibeli masing-masing order.
    - olist_order_payments: Dataset ini berisi data tentang pilihan metode pembayaran.
    - olist_order_reviews_dataset: Dataset ini berisi tentang *review* yang dibuat oleh *customer*.
    - olist_orders_dataset: Dataset ini merupakan dataset utama yang berisi tentangberbagai informasi mengenai *order* (tanggal pembelian, tanggal pengirimnan barang, estimasi sampai barang, tanggal barang sampai di *customer*)
    - olist_products_dataset: Dataset ini berisi data mengenai product yang dijual oleh *Olist*.
    - olist_sellers_dataset: Dataset ini berisi data tentang penjual yang memenuhi pemesanan yang dibuat di *Olist*.
    - product_category_name_traslation: Dataset ini berisi informasi *Product Category Name* dalam bahasa Inggris.
- Dari proses *data cleaning* dan *data preprocessing* yang di lakukan diatas, maka di buat satu dataset yang akan digunakan untuk melakukan **Delivery Performance Analysis and Delivery Time Prediction Based on Olist Dataset** dengan nama file ``brazilian_ecommerce_after_cleaning.csv``, dan dalam dataset tersebut juga dipilih **feature** yang akan digunakan baik untuk proses **EDA**, maupun **Model Building untuk Machine Learning**, berikut adalah penjelasan singkat mengenai kolom yang akan digunakan:
    - **Data Cleaning yang diambil dari dataset Olist**:
        - customer_id: *unique id* dari tiap *customer*.
        - customer_zip_code: kodepos dari *costumer*.
        - customer_city: kota asal dari *costumer*.
        - customer_state: asal negara bagian dari *costumer*.
        - customer_lat: koordinat latitude dari *costumer*.
        - customer_lng: koordinat longitude dari *costumer*.
        - seller_id: *unique id* dari tiap *seller*.
        - seller_zip_code: kodepos dari *seller*.
        - seller_city: kota asal dari *seller*.
        - seller_state: asal negara bagian dari *seller*.
        - seller_lat: koordinat latitude dari *seller*.
        - seller_lng: koordinat longitude dari *seller*
        - order_id: unique id* dari tiap *order*
        - order_status: status pengiriman.
        - review_score: *review score* yang diberikan *customer* setelah barang sampai.
        - quantity: jumlah barang yang dibeli.
        - order_purchase_timestamp: tanggal pembelian barang.
        - order_approved_at: tanggal order di approve.
        - shipping_limit_date: batas waktu penyerahan barang dari *seller* ke pihak ekspedisi.
        - order_delivered_carrier_date: tanggal *actual* ketika barang diserahkan dari *seller* ke pihak ekspedisi.
        - order_estimated_delivery_date: tanggal estimasi barang sampai ke *customer* yang dikeluarkan oleh pihak Olist.
        - actual_delivered_date: tanggal *actual* barang sampai ke *costumer*.
        - product_id: *unique id* dari tiap *product*.
        - product_category_name_english: nama *product category name* dalam bahasa inggris.
        - price: harga barang per *quantity*.
        - product_weight_g: berat tiap barang dalam gram per *quantity*.
        - product_length_cm: panjang dimensi barang.
        - product_height_cm: tinggi dimensi barang.
        - product_width_cm: lebar dimensi barang.
        - freight_value: harga jasa pengiriman barang per *quantity*.

    - **Feature yang dibuat untuk menunjukan analisa dari hasil Data Preprocessing**:
        - distance (Km): jarak antara *seller* dan *costumer*.
        - total_price: *price* x *quantity*.
        - volume_cm3: *product_length_cm* x *product_height_cm* x *product_width_cm*.
        - total_volume_cm3: *volume_cm3* x *quantity*.
        - total_freight_value: *freight_value* x *quantity*.
        - total_payment: *total_price* + *total_freight_value*.
        - seller_delivery_performance (days):performa *seller* dalam mengirim barang ke pihak ekspedisi, apakah melewati batas yang ditentukan atau tidak (shipping_limit_date - order_delivered_carrier_date).
        - delivery_performance (days) : performa perngiriman dalam mengirim barang hingga sampai ke pihak *customer*, apakah melewati batas yang ditentukan atau tidak (order_estimated_delivery_date - actual_delivered_date).
        - shipping_time_(days): lama waktu yang dibutuhkan oleh pihak ekspedisi untuk mengirim barang hingga sampai ke pihak *customer* (actual_delivered_date - order_delivered_carrier_date).
        - delivery_time (days): lama waktu pengiriman barang dari order tersebut diterima dan di bayar (*approved*). (actual_delivered_date - order_approved_at)
        - delivery_time/distance: kecepatan pengiriman berdasarkan lama waktu pengiriman/jarak antara *seller* dan customer (delivery_time (days)/distance (Km)).
        
**Dalam proyek ini, terdapat 3 tahap yang saya lakukan:**
- *Data Cleaning & Data Preprocessing* (*Handling Missing Value*, menggabungkan dataset, membuat *feature* baru, *handling duplicate value*)
- *Exporatory Data Analysis*
- Membuat model *Machine Learning* untuk membuat prediksi lama pengiriman barang berdasarkan *Feature* yang ada didalam dataset.

## Machine Learning Modeling
Setelah dilakukan tahap *Data Cleaning & Preprocessing* dan tahap *Exploratory Data Analysis*, lalu dipilih *feature* yang akan digunakan dalam model *machine learning* menggunakan metode statistik dengan *Pearson Correlation*.

Berikut ini adalah langkah yang saya lakukan untuk membuat model *Machine Learning* yang digunakan:

1. Handling outlier pada dependant varible
2. Feature selection untuk menentukan independent variable
3. Menentukan model dengan regression model
4. Tuning model
5. Melakukan *Cross Validation* untuk menghindari overfitting model
5. Evaluasi model

Model machine learning yang paling bagus adalah **RandomForestRegressor** dengan nilai

- RMSE Traning = 1.11
- RMSE Test = 2.05
- R2_Score Test = 0.99
- R2_Score Traning = 0.95

## Dashboard
Saya mengguanakan Flask untuk membuat *dashboard*

**Home**
<br>

![Home](https://user-images.githubusercontent.com/65010867/93131433-3d5f4000-f6fe-11ea-97d7-725f3688b01a.png)

<br>

**Dataset**

![Dataset](https://user-images.githubusercontent.com/65010867/93131519-68499400-f6fe-11ea-9d75-5ebdd2a65522.png)

<br>

**Data Visualisation**

![Visualisasi](https://user-images.githubusercontent.com/65010867/93131616-9038f780-f6fe-11ea-9039-86a99b041dea.png)

<br>

**Prediction**

![Predict](https://user-images.githubusercontent.com/65010867/93131669-a47cf480-f6fe-11ea-800c-11d24db5454c.png)

<br>

**Result**

![Result](https://user-images.githubusercontent.com/65010867/93131705-b9598800-f6fe-11ea-9dbf-a4fa589633d5.png)
