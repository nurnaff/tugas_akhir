# tugas_akhir
# Laporan Proyek Machine Learning - Nur Nafiiyah 
## Domain Proyek
Pertumbuhan teknologi yag pesat menyebabkan peningkatan data dari web, misal e-commerce, film, musik, dan permainan. Masalah utama dalam sistem rekomendasi adalah memberikan informasi yang tepat dari kumpulan data atau informasi. Sistem rekomendasi memberikan informasi dari perilaku histori konsumen/pengguna. Berbagai teknik rekomendasi telah diteliti dengan melihat konten dan berdasarkan kolaboratif, pengetahuan, dan demografi drai pengguna.
Dalam dataset movie terdapat informasi terkait rating dari movie yang dilihat pengguna lain. Dari nilai rating yang diberikan pengguna, maka dapat digunakan sebagai salah satu cara memberikan rekomendasi ke pengguna lain berdasarkan item dan rating movie. Sistem rekomendasi memberikan saran berdasarkan aktivitas (history) sejumlah pengguna. Penelitian yang digunakan acuan adalah [ini link](https://www.sciencedirect.com/science/article/pii/S2666285X22000176)

## Business Understanding
Proyek ini menangani data dalam jumlah besar dan menyaring informasi yang berguna, merekomendasikan film serupa berdasarkan pilihan pengguna dan melakukan analisis pada ulasan film yang dipilih. Popularitas sebuah film didasarkan pada jenis ulasan yang didapatnya dari penonton. Ulasan-ulasan ini dapat mempengaruhi pilihan pengguna lain. Pengguna lebih cenderung memilih film yang direkomendasikan oleh kebanyakan orang. 
### Problem statements
Berdasarkan uraian di atas, maka proyek ini membuat: bagaimana membuat sistem rekomendasi dengan teknik content-based filtering dan collaborative filtering?
### Goals
Untuk menjawab pertanyaan di problem statements, maka yang dilakukan adalah membuat model atau sistem rekomendasi dengan content-based filtering dan collaborative filtering.
### Solution statements
Untuk memberikan rekomendasi berdasarkan data movie yang ditonton pengguna dan rating.

## Data Understanding
Dataset ini diambil dari [kaggle](https://www.kaggle.com/datasets/parasharmanas/movie-recommendation-system). Dalam dataset terdapat dua tabel, yaitu movies.csv, dan ratings.csv

Tabel ``` movies.csv ```, terdapat 62423 baris, dan 3 kolom. Terdiri dari:

``` movieId ``` sebagai kolom Id movie.

``` title ``` sebagai kolom judul movie.

``` genres ``` sebagai kolom jenis genre movie.

Fungsi untuk melihat informasi tabel ``` movies.csv ``` adalah

``` dt.info() ```

Hasilnya:

![movie1](https://github.com/user-attachments/assets/f73cf29a-f883-4cbd-8487-6f2346b9dd10)

Tabel ``` ratings.csv ```, terdapat 25000095 baris, dan 3 kolom. Terdiri dari:

``` userId ``` sebagai kolom Id user.

``` movieId ``` sebagai kolom Id movie.

``` rating ``` sebagai kolom penilaian movie.

``` timestamp ``` sebagai kolom waktu mengisi penilaian movie.

Fungsi untuk melihat informasi dari tabel ``` ratings.csv ``` adalah 

``` rt.info() ```

Hasilnya:

![rati1](https://github.com/user-attachments/assets/daefebd8-513f-4447-9c7c-fdb68322525d)

Mengecek data yang kosong adalah ``` isnull().sum() ```, dan data pada tabel ``` movies.csv ``` dan ``` ratings.csv ``` tidak ada yang kosong, ini hasilnya

![movie2](https://github.com/user-attachments/assets/111a56d6-6d01-43c1-bf65-9820a3d2d68a)

![rati2](https://github.com/user-attachments/assets/669fc21c-92f8-4b78-857e-c79a12749595)

Mengecek data yang duplikat adalah ``` duplicated().sum() ```, dan hasilnya di tabel ``` movies.csv ``` kolom judul ``` title ``` movie terdapat yang duplikat, sehingga dilakukan pengecekan dengan perintah dan hasil:

![Screenshot 2024-10-24 140857](https://github.com/user-attachments/assets/952779cb-2979-4264-a948-b777deaa406f)

Kolom genres mempunyai isi yang bervariasi dengan satu judul ``` title ``` movie terdapat banyak genres yang dihubungkan dengan tanda baca ``` | ```, seperti berikut:

![Screenshot 2024-10-24 141238](https://github.com/user-attachments/assets/aaf06c4b-dc9e-46b3-aeed-66f9e800d431)

Dan hasil fungsi ``` duplicated().sum() ``` pada tabel ``` ratings.csv ```, ``` 0 ```.

Mengecek data yang unik adalah ``` nunique() ```, dan hasilnya pada tabel ``` movies.csv ``` 

![movie3](https://github.com/user-attachments/assets/2357ae47-81b2-45c6-a1ea-7b392bad0f13)

Dan hasilnya fungsi ``` nunique() ``` pada tabel ``` ratings.csv ```

![rati3](https://github.com/user-attachments/assets/719ef532-20e1-42da-96c1-73febbf60892)

Mengecek nilai statistik dari tabel ``` movies.csv ``` dan ``` ratings.csv ``` dengan fungsi: ``` describe() ```.

``` count ``` menampilkan jumlah data/baris tabel.

``` mean ``` menampilkan nilai rata-rata dari setiap kolom angka.

``` std ``` menampilkan nilai standar deviasi dari setiap kolom angka.

``` min ``` menampilkan nilai minimum dari setiap kolom angka.

``` 25%, 50% 75% ``` menampilkan nilai kuartil 1 dan 3, serta median dari setiap kolom angka.

``` max ``` menampilkan nilai maksimum dari setiap kolom angka.

Hasil dari fungsi ``` describe() ``` adalah:

![WhatsApp Image 2024-10-24 at 14 01 13](https://github.com/user-attachments/assets/93b78f5f-db10-4d78-9da6-4cfed36d0129)

![WhatsApp Image 2024-10-24 at 14 01 28](https://github.com/user-attachments/assets/f5799875-f097-41da-b9c1-a14274556efd)

Mengecek bentuk baris dan kolom dari tabel ``` movies.csv ```, fungsinya: ``` shape ```. Hasil dari tabel ```movies.csv```

``` (62423,3) ```

Hasil dari tabel ``` ratings.csv ```

![rati4](https://github.com/user-attachments/assets/79a94001-9a0d-4d8f-a184-ea448d9c3c23)

## Data Preparation
Proses menghapus data yang duplikat dengan fungsi dan hasil sebagai berikut: (jumlah baris berubah)

![Screenshot 2024-10-24 141015](https://github.com/user-attachments/assets/81088c6c-2e47-43b1-858a-cd8ac65416b3)

Menghasilkan: kolom ``` genres ``` pada tabel ``` movies.csv ``` terdapat lebih dari 1 jenis/kategori dengan dihubungkan tanda ``` | ```. Sehingga dilakukan proses satu judul movie hanya ada satu jenis genres dengan fungsi.

``` dt_br['genres']=dt_br['genres'].str.split('|').str[0] ```. Hasilnya

![Screenshot 2024-10-24 141301](https://github.com/user-attachments/assets/4c04fcdd-e83f-4ee9-918b-9e904b436a0d)

Karena data pada genres terdapat isi 'no genres listed' sehingga dilakukan penghapusan, dengan fungsi:

``` dt_br.drop(dt_br[dt_br['genres']=='(no genres listed)'].index,inplace=True) ```. Hasilnya

![Screenshot 2024-10-24 141446](https://github.com/user-attachments/assets/f94f417f-2b66-42b6-b5be-47be8e3f547e)

Menghilangkan tanda baca ``` - ``` pada kolom genres ``` Sci-Fi ``` dan ``` Film-Noir ``` menggunakan fungsi:

``` dt_br['genres']=dt_br['genres'].replace({'Sci-Fi':'SciFi','Film-Noir':'FilmNoir'}) ```. Hasilnya

![Screenshot 2024-10-24 141503](https://github.com/user-attachments/assets/8386f2e6-1ebd-4d48-ae59-3a619eb95313)

Menampilkan grafik jumlah dari setiap jenis ``` genres ```. Fungsinya: ``` dt_br['genres'].value_counts().plot(kind='bar') ```. Hasilnya:

![Screenshot 2024-10-24 143327](https://github.com/user-attachments/assets/75d77736-d19a-45ef-a6ce-b3c4af72f441)

Mengecek kolom yang isi barisnya kurang dari 2000. Karena jenis ``` genres ``` sangat bervariasi dengan jumlah data yang puluhan ribu, sehingga proyek ini hanya menggunakan data dengan ``` genres ``` yang lebih dari 1 dan kurang dari 2000.

![Screenshot 2024-10-24 143409](https://github.com/user-attachments/assets/e6278bb5-d880-4d9f-8eb5-41e405532e6a)

Menghapus baris yang jumlah 1 dan lebih dari 2000 adalah ```imax``` dengan jumlah hanya 1, dengan fungsi 

```dt_br=dt_br[~dt_br['genres'].str.contains('IMAX')]```

```dt_br=dt_br[~dt_br['genres'].str.contains('Adventure')]```

```dt_br=dt_br[~dt_br['genres'].str.contains('Comedy')]```

```dt_br=dt_br[~dt_br['genres'].str.contains('Action')]```

```dt_br=dt_br[~dt_br['genres'].str.contains('Drama')]```

```dt_br=dt_br[~dt_br['genres'].str.contains('Crime')]```

```dt_br=dt_br[~dt_br['genres'].str.contains('Documentary')]```

```dt_br=dt_br[~dt_br['genres'].str.contains('Animation')]```

```dt_br=dt_br[~dt_br['genres'].str.contains('Horror')]```

![Screenshot 2024-10-24 143558](https://github.com/user-attachments/assets/930d5e0c-1aa1-4aa1-9830-03b36d9ffeed)

Melakukan konversi data series menjadi list, dengan menggunakan fungsi ``` tolist() ```.

![Screenshot 2024-10-24 143613](https://github.com/user-attachments/assets/18d210cd-03a0-4391-91fa-a0836caab87d)

Tahap selanjutnya menjadikan data ke bentuk dictionary. 

![movie10](https://github.com/user-attachments/assets/3129b6ec-43a2-4aee-a7cb-9bde34403b81)

Bentuk dari data setelah di dictionary adalah:

``` (4736,3) ```

Fungsi TF-IDF Vectorizer digunakan pada sistem rekomendasi untuk menemukan representasi fitur penting dari setiap genres movie. Tahap ```tfidfvectorizer()```, menghasilkan:

![movie12](https://github.com/user-attachments/assets/39d85478-aa1c-4e73-9ccb-73121600f244)

Kemudian hasil dari fungsi ```tfidfvectorizer()``` dibentuk ke matriks, perintanya:

``` tfidf_matrix=tf.fit_transform(movie_data['jenis']) ```

``` tfidf_matrix.shape ```, bentuknya menjadi ``` (4736,10) ```.

Matriks yang didapatkan berukuran ```(4736,10)```. 4736 merupakan jumlah baris, dan 10 merupakan genres movie. Selanjutnya cara menghasilkan vektor tf-idf dalam bentuk matriks menggunakan fungsi ```todense()```, hasilnya:

![movie14](https://github.com/user-attachments/assets/9dc384db-022a-4286-b2e2-c4c7e0275ead)

Hasil dari matriks ```todense()``` dijadikan dalam bentuk DataFrame, seperti ini:

![movie15](https://github.com/user-attachments/assets/be1f6230-8727-4743-ae1f-15366f4a1535)

Matrik DataFrame di atas ditampilkan sebanyak 10 movie dan 10 jenis genres (nilai korelasi antara movie dengan jenis genres). Selanjutnya melakukan perhitungan derajat kesamaan antar movie dengan fungsi cosine similarity dari library sklearn, dengan perintah dan hasil berikut:

![Screenshot 2024-10-24 162444](https://github.com/user-attachments/assets/a147cdf6-25b5-4ad3-a89f-1f9fe124980e)

Cosine similarity menghasilkan matriks kesamaan antar movie dalam bentuk array. Kemudian menampilkan nilai cosine similarity dari data movie (jumlah data berukuran 4736,4736), seperti berikut:

![Screenshot 2024-10-24 162958](https://github.com/user-attachments/assets/c25a1586-7d6e-4551-b723-37533668f274)

## Membuat Model
Model yang dibangun adalah sistem rekomendasi dengan pendekatan content based filtering. Model yang dibagun adalah sistem rekomendasi movie berdasarkan jenis genres yang ada dalam tabel ``` movies.csv ```. Selanjutnya dari data array cosine similarity di atas dapat digunakan sebagai proses rekomendasi movie yang mempunyai kesamaan. Proses rekomendasi berdasarkan movie yang pernah ditonton pengguna yang mempunyai kesamaan menggunakan ``` def movie_recommendations() ```. Proses rekomendasi berdasarkan parameter judul movie (title), nilai kesamaan (cosine similarity), items (fitur judul movie yang mempunyai kesamaan), dan k (banyaknya movie yang direkomendasikan). Perintah mencari rekomendasi movie yang mirip dengan 'Shark Lake (2015)' dan hasilnya seperti berikut:

![Screenshot 2024-10-24 163712](https://github.com/user-attachments/assets/b9c66733-0893-4961-8a15-c234a66653ef)

![Screenshot 2024-10-24 163824](https://github.com/user-attachments/assets/59046d6d-b4bd-45b8-8d91-12d40ac9d8fa)

Berdasarkan hasil rekomendasi di atas, proyek ini akan menampilkan movie yang mempunyai genres yang mirip dengan movie yang dicari ``` 'Shark Lake (2015)' ```.

## Data Preparation
Model ini memberikan rekomendasi berdasarkan nilai rating yang dimasukan pengguna. Berdasarkan nilai rating tersebut akan diolah untuk digunakan rekomendasi movie yang mirip serta belum pernah ditonton.
- Tahap pertama: melakukan encode userId dan movieId ke bentuk angka (integer).
  
  ![Screenshot 2024-10-24 170309](https://github.com/user-attachments/assets/9c5322ad-24b6-479a-9ea0-7dd5ed269730)

- Tahap kedua: hasil encode data userId dan movieId (berupa angka) dimasukkan ke dalam DataFrame.

  ![Screenshot 2024-10-24 170325](https://github.com/user-attachments/assets/7753cfde-e664-4576-b3ff-14a6986f6656)

- Tahap ketiga: menghitung jumlah user, movie, dan mengubah nilai rating dari String ke float

  ![Screenshot 2024-10-24 170532](https://github.com/user-attachments/assets/64b62959-3faa-4154-825c-d6221a4dcd24)

Hasil dari tahapan di atas kemudian digunakan sebagai data training dan testing, dengan pembagian data training 80% dari total data dan testing 20% dari seluruh data. Variabel input ``` (x) ``` adalah ``` user, movie ```, dan output atau target ``` (y) ``` adalah ``` rating ```.

![Screenshot 2024-10-24 170905](https://github.com/user-attachments/assets/ea62e0e6-a0b4-408f-9933-2da092ed62d1)

## Model Collaborative Filtering
Proses training menggunakan ``` class RecommenderNet(Model) ```, dengan library ``` import tensorflow ``` dan ``` from tensorflow import keras ```. Model ini akan melakukan teknik embeding dengan menghitung nilai kecocokan antara user dan movie.

![Screenshot 2024-10-24 171241](https://github.com/user-attachments/assets/dae7e626-e2a7-4830-a062-9e7bded0b92d)

Parameter ``` compile ``` menggunakan ``` loss function ``` adalah ``` keras.losses.BinaryCrossentropy() ```, ``` optimizer ``` adalah ``` keras.optimizers.Adam(learning_rate=0.001) ```, dan matrics evaluasi adalah ``` keras.metrics.RootMeanSquaredError() ```.

![Screenshot 2024-10-24 171536](https://github.com/user-attachments/assets/4e4db1fb-01f7-4877-a4f8-05403ec855bf)

Tahap training membaca data sebanyak ``` batch_size=512 ``` dan melakukan perulangan epoch 10 kali.

![Screenshot 2024-10-24 171702](https://github.com/user-attachments/assets/d1a7a991-8235-4715-af2b-81e5c70f4a28)

## Evaluasi
Proses training dilakukan sekalian dengan evaluasi testing, dengan diagram evaluasi nilai ``` roor_mean_squared_error ``` sebagai berikut

![Screenshot 2024-10-24 171831](https://github.com/user-attachments/assets/1591ceeb-fbcc-42e3-81da-4cbf9730e7ce)

Diagram loss dari proses training dan evaluasi adalah:

![Screenshot 2024-10-24 172245](https://github.com/user-attachments/assets/747a61df-4638-41c9-aadb-35265c8af403)

Bahwa dari diagram di atas, bahwa nilai ``` RMSE ``` saat training ataupun testing tidak mengalami perubahan yang signifikan (nilai diantara 0,44 sampai 0,45), sedangkan nilai ``` loss ``` saat training dan testing mengalami perubahan naik dari 2,778 sampai 6,659.

Cara merekomendasikan movie berdasarkan rating dan yang belum pernah ditonton, dengan operator ``` bitwise (~) ```.

![Screenshot 2024-10-24 173110](https://github.com/user-attachments/assets/d149771d-20c9-438d-a37a-513ef2852b37)

Proses memberikan rekomendasi movie dengan fungsi ``` model.predict() ``` berdasarkan data user, movie dalam bentuk array.

![Screenshot 2024-10-24 174335](https://github.com/user-attachments/assets/566e83c5-0d2a-4b02-922e-31facbeb6ea4)

Hasil 10 movie hasil rekomendasi:

![image](https://github.com/user-attachments/assets/637456e0-346f-4155-a61d-847ffaced0b9)
