# tugas_akhir
# Laporan Proyek Machine Learning - Nur Nafiiyah 
## Domain Proyek
Pertumbuhan teknologi yag pesat menyebabkan peningkatan data dari web, misal e-commerce, film, musik, dan permainan. Masalah utama dalam sistem rekomendasi adalah memberikan informasi yang tepat dari kumpulan data atau informasi. Sistem rekomendasi memberikan informasi dari perilaku histori konsumen/pengguna. Berbagai teknik rekomendasi telah diteliti dengan melihat konten dan berdasarkan kolaboratif, pengetahuan, dan demografi drai pengguna.
Dalam dataset movie terdapat informasi terkait rating dari movie yang dilihat pengguna lain. Dari nilai rating yang diberikan pengguna, maka dapat digunakan sebagai salah satu cara memberikan rekomendasi ke pengguna lain berdasarkan item dan rating movie. Sistem rekomendasi memberikan saran berdasarkan aktivitas (history) sejumlah pengguna. Penelitian yang digunakan acuan adalah [ini link](https://www.sciencedirect.com/science/article/pii/S2666285X22000176)

## Business Understanding
Proyek ini menangani data dalam jumlah besar dan menyaring informasi yang berguna, merekomendasikan film serupa berdasarkan pilihan pengguna dan melakukan analisis pada ulasan film yang dipilih. Popularitas sebuah film didasarkan pada jenis ulasan yang didapatnya dari penonton. Ulasan-ulasan ini dapat mempengaruhi pilihan pengguna lain. Pengguna lebih cenderung memilih film yang direkomendasikan oleh kebanyakan orang. 
- Problem statements, berdasarkan uraian di atas, maka proyek ini membuat: bagaimana membuat sistem rekomendasi dengan teknik content-based filtering?
- Goals, untuk menjawab pertanyaan di problem statements, maka dilakukan: membuat model atau sistem rekomendasi.
- Solution statements, untuk memberikan rekomendasi berdasarkan data movie yang ditonton pengguna dan rating.

## Data Understanding
Dataset ini diambil dari [kaggle](https://www.kaggle.com/datasets/parasharmanas/movie-recommendation-system).
Dalam dataset terdapat dua tabel, yaitu movies.csv, dan ratings.csv

Tabel ``` movies.csv ```
terdapat 62423 baris, dan 3 kolom. Terdiri dari:

``` movieId ``` sebagai kolom Id movie.

``` title ``` sebagai kolom judul movie.

``` genres ``` sebagai kolom jenis genre movie.

Fungsi untuk melihat informasi tabel ``` movies.csv ``` adalah

``` dt.info() ```

Hasilnya:

![movie1](https://github.com/user-attachments/assets/f73cf29a-f883-4cbd-8487-6f2346b9dd10)

Tabel ``` ratings.csv ```
terdapat 25000095 baris, dan 3 kolom. Terdiri dari:

``` userId ``` sebagai kolom Id user.

``` movieId ``` sebagai kolom Id movie.

``` rating ``` sebagai kolom penilaian movie.

``` timestamp ``` sebagai kolom waktu mengisi penilaian movie.

Fungsi untuk melihat informasi dari tabel ``` ratings.csv ``` adalah 

``` rt.info() ```

Hasilnya:

![rati1](https://github.com/user-attachments/assets/daefebd8-513f-4447-9c7c-fdb68322525d)

Mengecek data yang kosong adalah ``` isnull().sum() ``` 
dan data pada tabel ``` movies.csv ``` tidak ada yang kosong, ini hasilnya

![movie2](https://github.com/user-attachments/assets/111a56d6-6d01-43c1-bf65-9820a3d2d68a)

dan pada tabel ``` ratings.csv ``` tidak ada yang kosong, ini hasilnya

![rati2](https://github.com/user-attachments/assets/669fc21c-92f8-4b78-857e-c79a12749595)

Mengecek data yang duplikat adalah ``` duplicated().sum() ```
dan hasilnya dikedua tabel ``` movies.csv ``` dan ``` ratings.csv ``` nilainya 0, ini hasilnya

``` Data yang duplikat:  0 ```

Mengecek data yang unik adalah ``` nunique() ```

dan hasilnya pada tabel ``` movies.csv ``` 

![movie3](https://github.com/user-attachments/assets/2357ae47-81b2-45c6-a1ea-7b392bad0f13)

dan hasilnya pada tabel ``` ratings.csv ```

![rati3](https://github.com/user-attachments/assets/719ef532-20e1-42da-96c1-73febbf60892)

Mengecek bentuk baris dan kolom dari tabel ``` movies.csv ```, fungsinya: ``` shape ```. Hasil dari tabel ```movies.csv```

![movie8](https://github.com/user-attachments/assets/b45dcf9d-fa98-45de-b41f-229c96fef278)

Hasil dari tabel ``` ratings.csv ```

![rati4](https://github.com/user-attachments/assets/79a94001-9a0d-4d8f-a184-ea448d9c3c23)

## Data Preparation

Kolom genres mempunyai isi yang bervariasi dan double, seperti dalam perintah berikut:

![movie4](https://github.com/user-attachments/assets/efcd679b-19b1-4d78-ae48-27e8bf73c026)

Menghasilkan: kolom ``` genres ``` pada tabel ``` movies.csv ``` terdapat lebih dari 1 jenis/kategori dengan dihubungkan tanda ``` | ```. Sehingga dilakukan proses satu judul movie hanya ada satu jenis genres dengan fungsi.

``` dt['genres']=dt['genres'].str.split('|').str[0] ```. Hasilnya

![movie5](https://github.com/user-attachments/assets/a61634aa-8d98-43e1-a5b8-f25223889af9)

Karena data pada genres terdapat isi 'no genres listed' sehingga dilakukan penghapusan, dengan fungsi:

``` dt.drop(dt[dt['genres']=='(no genres listed)'].index,inplace=True) ```. Hasilnya

![movie6](https://github.com/user-attachments/assets/aa867ffe-6aee-481d-a36f-e4f43425e944)

Menghilangkan tanda baca ``` - ``` pada kolom genres ``` Sci-Fi ``` dan ``` Film-Noir ``` menggunakan fungsi:

``` dt['genres']=dt['genres'].replace({'Sci-Fi':'SciFi','Film-Noir':'FilmNoir'}) ```. Hasilnya

![movie7](https://github.com/user-attachments/assets/fbf74b72-1e80-48e7-adec-8b5288b937f6)

Mengecek kolom yang isi barisnya kurang dari 10.

![movie16](https://github.com/user-attachments/assets/564bbd53-9058-4f88-a06c-25bda19743b1)

Menghapus baris yang jumlah kurang dari 10 adalah ```imax``` dengan jumlah hanya 1, dengan fungsi 
```dt=dt[~dt['genres'].str.contains('IMAX')]``` dan hasil:

![movie17](https://github.com/user-attachments/assets/aceb90b6-e40b-440d-af91-a59f79612663)


Melakukan konversi data series menjadi list, dengan menggunakan fungsi ``` tolist() ```.

![movie9](https://github.com/user-attachments/assets/7fa23196-e5b3-4725-bb54-3292da21b8f0)

Tahap selanjutnya menjadikan data ke bentuk dictionary. 

![movie10](https://github.com/user-attachments/assets/3129b6ec-43a2-4aee-a7cb-9bde34403b81)

Bentuk dari data setelah di dictionary adalah:
![movie11](https://github.com/user-attachments/assets/91002751-b60f-4e36-b36e-f06888ec4aab)

## Membuat Model
Model yang dibangun adalah sistem rekomendasi dengan pendekatan content based filtering. Model yang dibagun adalah sistem rekomendasi movie berdasarkan jenis genres yang ada dalam tabel ``` movies.csv ```. Fungsi TF-IDF Vectorizer digunakan pada sistem rekomendasi untuk menemukan representasi fitur penting dari setiap genres movie. Tahap ```tfidfvectorizer()```, menghasilkan:

![movie12](https://github.com/user-attachments/assets/39d85478-aa1c-4e73-9ccb-73121600f244)

Kemudian hasil dari fungsi ```tfidfvectorizer()``` dibentuk ke matriks, hasilnya:

![movie13](https://github.com/user-attachments/assets/b1f59d10-5763-42f0-a4c0-ab84df2ad29b)

Matriks yang didapatkan berukuran ```(57361,19)```. 57361 merupakan jumlah baris, dan 19 merupakan genres movie. Selanjutnya cara menghasilkan vektor tf-idf dalam bentuk matriks menggunakan fungsi ```todense()```, hasilnya:

![movie14](https://github.com/user-attachments/assets/9dc384db-022a-4286-b2e2-c4c7e0275ead)

Hasil dari matriks ```todense()``` dijadikan dalam bentuk DataFrame, seperti ini:

![movie15](https://github.com/user-attachments/assets/be1f6230-8727-4743-ae1f-15366f4a1535)

