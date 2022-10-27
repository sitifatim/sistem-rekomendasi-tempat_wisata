# Laporan Proyek Machine Learning - Siti Fatimatuzzahro

## Project Overview
![gambar](https://th.bing.com/th/id/OIP.4x_aEG3I8M8gropN1eV0BwHaC5?pid=ImgDet&rs=1)

Indonesia merupakan negara kepulauan yang memiliki ribuan tempat wisata menawan. Tempat wisata di Indonesia selain terkenal akan keindahannya juga mendatangkan banyak manfaat bagi masyarakat Indonesia. Salah satu manfaat tersebut yaitu memberi pelayanan untuk publik seperti lahan rekreasi, hiburan, dan olahraga santai. Manfaati lain dari tempat wisata adalah membuka peluang lapangan kerja bagi masyarakat di sekitar tempat wisata seperti berdagang, menyediakan angkutan bagi para wisatawan, menyediakan jasa, telekomunikasi dan sebagainya. Manfaat lainyang tak kalah penting dari tempat wisata adalah sebagai tempat pengembangan pendidikan dan pengetahuan atau penelitian serta sebagai usaha menambah aset daerah yang sangat berharga untuk investasi jangka panjang daerah [1]. Jumlah wisatawan tiap tahunnya semakin meningkat dari 2013 sebanyak 8,8 juta orang meningkat hampir dua kali lipat pada 2019 sebanyak 16 juta orang. Dengan minat publik pada tempat wisata yang semakin meningkat, tentunya akan mendatangkan banyak manfaat bagi masyarakat dan negara sehingga tiap tahunnya, selalu ada tempat wisata baru yang muncul [2]. Namun demikian, meskipun bertambahnya tempat wisata mendatangkan kebaikan bagi masyarakat sekitar, akan tetapi tidak semua tempat wisata terekspos pada publik meskipun memiliki penilain yang baik dari para wisatawan yang telah berkunjung. Hal ini terjadi oleh beberapa kemungkinan salah satunya ialah kurang tereksposnya tempat wisata pada publi. Oleh karena itu, diperlukannya suatu sistem rekomendasi untuk memudahkan publik mendapatkan rekomendasi tempat wisata baru yang tentunya memiliki penilaian baik sehingga perjalanan wisata tidak akan mengecewakan. 

## **Business Understanding**
### Problem Statements
* Bagaimana cara membuat sistem rekomendasi untuk dapat merekomendasikan tempat wisata berdasarkan penilaian?
* Metode apa yang akan digunakan untuk pembuatan sistem rekomendasi tersebut?

### Goals
* Pembuatan sistem rekomendasi dapat dilakukan dengan kecerdasan buatan yaitu membuat sistem rekomendasi berbasis machine learning
* Metode sistem rekomendasi yang akan dibuat ialah menggunakan Collaborative Filtering dimana mengandalkan model-based untuk merekomendasikan hal baru pada pengguna

## **Data Understanding**
Dataset yang digunakan merupakan dataset yang berasal dari Kaggle dengan judul "Indonesia Tourism Destination" yang dapat diakses pada [link](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination?select=tourism_with_id.csv) ini. Dataset ini mengumpulkan destinasi-destinasi wisata yang dikumpulkan dari lima kota besar di Indonesia diantaranya adalah Jakarta, Semarang, Bandung, Yogyakarta, dan Surabaya. Data-data tersebut dikumpulkan oleh Tim GetLoc untuk keperluan Capstone Bangkit Academy 2021. Adapun jumlah total dari dataset ialah sebanyak 10.000 data berisikan variabel-variable yaitu dummy Id pengunjung (User_Id), Id tempat wisata (Place_Id), dan rating tempat wisata (Place_Ratings). Deskripsi tentang variabel-variabel tersebut ialah sebagai berikut:
* User_Id : berisikan sekumpulan data unik dari user atau dalam kasus dataset ini, merupakan para wisatawan
* Place_Id : berisikan kode unik yang mempresentasikan tempat wisata di Indonesia
* Place_Ratings : berisikan rating atau penilaian yang diberikan oleh user (wisatawan) terhadap tempat wisata yang telah dikunjungi

## **Data Preparation**
Ada beberapa tahap pada tahapan data preparation yaitu sebagai berikut:
* Encoding fitur User_Id dan Place_Id ke bentuk integer. Hal ini dilakukan agar data dapat ditraining model.
* Mapping User_Id dan Place_Id ke dataframe bertujuan untuk memetakan dua fitur tersebut ke dataframe.
* Pengecekan beberapa item seperti jumlah user, jumlah tempat, dan mengubah nilai rating menjadi float. Dari pengecekan item yang telah dilakukan, didapatkan hasil jumlah user sebanyak 300 user, jumlah tempat sebanyak 437 tempat, minimum rating yang diberikan adalah 1, dan maksimum rating yang diberikan adalah 5.
* Pembagian dataset ke data training dan data validation. Data training akan dijadikan data untuk saat training model berlangsung sedangkan data validasi adalah untuk memvalidasi model yang sudah terbentuk (testing). Sebelum dilakukan pembagian, dataset terlebih dahulu diacak terlebih dahulu agar model lebih terbiasa dengan data acak atau tidak berurutan. Selanjutnya dataset akan dibagi dengan rasio 80:20. 

## **Modeling**

Pada tahap ini, model menghitung skor kecocokan antara user dan tempat dengan teknik embedding. Pertama, melakukan proses embedding terhadap data user dan tempat. Selanjutnya, lakukan operasi perkalian dot product antara embedding user dan tempat. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi sigmoid. Selanjutnya, melakukan compile dengan model yang sudah dibuat dan kemudian melakukan proses training. Sebelum dilakukan proses training, ada beberapa parameter model yang ditambahkan dan yaitu sebagai berikut:

Tabel 1. Parameter Model

| Parameter   |Cara Kerja|
|:------------|:------------------|
|recommendernet|bekerja membangun sebuah grup layer menjadi objek dengan inferensi fitur-fitur seperti input yang digunakan, layer yang digunakan, hingga fungsi aktivasi yang digunakan. Pada model ini menggunakan input num_place dan num_resto. Layer yang digunakan sebanyak 4 layer embedding. Aktivasi yang digunakan adalah aktivasi sigmoid karena output yang diinginkan adalah bukan multiclass|
|loss         |loss digunakan untuk mengetahui seberapa dekat model dapat memprediksi hal baru. Loss yang digunakan pada model ini adalah Binary Crossentropy karena output model adalah binary class|
|optimizer    |berfungsi untuk mengoptimalkan prediksi model. Optimizer yang digunakan ialah Adam karena merupakan optimizer ter-update dibandingkan RMSprop dan SGD|
|metric evaluation| berfungsi untuk menampilkan error dari prediksi model dan aktual value. Metric evaluation yang digunakan adalah RMS karena mudah digunakan dan cukup sensitif perubahannya|
## **Evaluation**

Evaluasi sistem rekomendasi mencakup dua hal yaitu evaluasi model dengan visualisasi hasil training model dan percobaan sistem rekomendasi untuk rekomendasi tempat baru. Berikut merupakan tahapan evaluasi:

### Visualisasi Model 

![ScreenShot Tool -20221027003745](https://user-images.githubusercontent.com/99231159/198099128-e31885f7-8ac7-43d1-bd64-71a6fd4199d4.png)

Gambar 4. Visualisasi Hasil Training

Berdasarkan visualisasi diatas, dapat dilihat bahwa proses training mengalami naik turun yang cukup berubah-ubah atau tidak konstan dibandingan proses testing. Akan tetapi, meskipun demikian, dapat dilihat pula bahwa meskipun pada proses trainingnya tidak cukup halus, hasil akhir dari training memiliki nilai error dibawah 0,34 dan pada validasi sebesar 0,36 yang mana tidak terlalu buruk untuk sistem rekomendasi. 

### Percobaan Rekomendasi Tempat Baru
Langkah ini dilakukan untuk melihat performa model apakah dapat merekomendasikan tempat baru atau tidak. Mengingat yang akan direkomendasikan merupakan rekomendasi tempat, maka akan dibuat variabel baru yaitu place_have_not_visit yang berisikan daftar tempat yang belum pernah dikunjungi user. Hasil dari tahap ini dapat dilihat pada gambar 5.

![ScreenShot Tool -20221027004747](https://user-images.githubusercontent.com/99231159/198099300-74357a38-8dcf-461c-9454-ca79ae18b13c.png)

Gambar 5. Rekomendasi Tempat Wisata Baru

Berdasarkan gambar 5, dapat dilihat bahwa model berhasil merekomendasikan tempat baru. Collaborative Filtering cukup mudah digunakan dan cepat dalam pemrosesannya akan tetapi mungkin terbatas pada filtering beberapa variabel saja. Untuk filtering dengan lebih banyak variabel, disarankan untuk dapat mecoba metode lain selain Collaborative Filtering.

## **References**
[1] Iwan Setiawan, "POTENSI DESTINASI WISATA DI INDONESIA MENUJU KEMANDIRIAN
EKONOMI", PROSIDING SEMINAR NASIONAL MULTI DISIPLIN ILMU & CALL FOR PAPERS UNISBANK (SENDI_U)

[2] Adenisa Aulia Rahma, "Potensi Sumber Daya Alam dalam Mengembangkan Sektor Pariwisata di Indonesia", Jurnal Nasional Pariwisata, 2020.
