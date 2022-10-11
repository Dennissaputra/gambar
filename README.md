# **Laporan Proyek Machine Learning - A. Gilang Aleyusta Savada**
---

## **Domain Proyek**
---
Domain : Pendidikan
Judul : Content & Collaborative Filtered Book Recommendation

[![93536-OJW9WN-85-01-1024x1024](https://i.im.ge/2022/09/13/1TubfF.93536-OJW9WN-85-01-1024x1024.jpg)](https://im.ge/i/1TubfF)

Ditengah bonus demografi yang dihadapi, faktanya Indonesia memiliki tingkat literasi yang sangat rendah. Menurut data UNESCO, minat baca masyarakat Indonesia sangat memprihatinkan, hanya 0,001%, yang artinya dari 1.000 orang Indonesia, hanya 1 orang yang rajin membaca[[1]](https://www.kominfo.go.id/content/detail/10862/teknologi-masyarakat-indonesia-malas-baca-tapi-cerewet-di-medsos/0/sorotan_media). Data tersebut diperkuat dengan riset yang dilakukan oleh Central Connecticut State Univesity berjudul “World’s Most Literate Nations Ranked” pada maret 2016, Indonesia dinyatakan menempati peringkat ke-60 dari 61 negara soal minat membaca, persis berada di bawah Thailand (59) dan di atas Bostwana (61)[[2]](http://www.gurusiana.id/read/fatchurrohman/article/membaca-belum-menjadi-habituasi-masyarakat-indonesia-523187#!).

Literasi harus mandarah daging pada bangsa yang merindukan kejayaan, tidak terkecuali Indonesia di era bonus demografi dewasa ini. Memanfaatkan teknologi bisa menjadi salah satu jalan terbaik untuk mengedukasi bangsa tentang pentingnya literasi demi kehidupan yang lebih baik. Tidak hanya itu instansi pendidikan harus menjadikan membaca serta menulis sebagai sebuah kebutuhan wajib bagi para peserta didik di sekolah. Kebiasaan literasi akan muncul ketika kita mengetahui manfaat besar literasi. Nenek moyang manusia telah memulai kebiasaan menulis dan membaca semenjak 3600 tahun sebelum masehi, sudah banyak buku yang telah berhasil dibuat. Tugas kita sebagai individu bagian dari bangsa ini adalah menumbuhkan minat literasi pribadi “temukan buku yang ada suka, baca, dan anda akan jatuh cinta pada membaca”.

Melihat pentingnya dampak literasi bagi kehidupan kita serta data yang telah diberikan seblumnya. Penulis memberikan gagasan mengenai sistem rekomendasi buku pilihan dengan algoritam Machine Learning untuk mencari buku sesuai ketertarikan sebagai langkah yang dapat ditempuh untuk meningkatkan literasi di tengah masyarakat. Pada kesempatan ini, akan digunakan dua metode, yaitu content dan collaborative based filter.

* Pada Content Based Flter, kita akan menggunakan penulis buku menjadi pusat sebagai pusat dari sistem rekomendasi
* Pada Collaborative Based Flter, kita akan menggunakan penilaian dari berbagai pengguna sebagai pusat dari sistem rekomendasi


## **Business Understanding**
---
### **Problem Statements**
Adapun pokok permasalahan yang dapat diselesaikan pada proyek ini:
* Bagaimana cara membuat sistem yang dapat merekomendasikan buku dari buku yang pernah dibaca sebelumnya?
* Bagaimana cara mendapatkan rekomendasi buku yang dari penulis buku yang sama?
### **Goals**
Adapun tujuan dari proyek ini adalah:
* Mengetahui cara membuat sistem yang dapat merekomendasikan buku - buku dari buku - buku yang pernah kita baca sebelumnya.
* Mengetahui cara mendapatkan buku - buku yang ditulis oleh penulis yang sama dengan buku - buku yang pernah kita baca sebelumnya.
### **Solution statements**
Adapun beberapa model yang berbeda untuk dibandingkan dan dapat menjadi solusi pada proyek ini, diantaranya adalah menggunakan:
* **Content Based Recommendation** memanfaatkan profil dan perilaku dari pengguna yang kemudian direkomendasikan kepada pengguna sebagai referensi yang terkait dengan informasi yang digunakan sebelumnya. Tujuan dari content based recommendation agar dapat memprediksi persamaan dari sejumlah informasi yang didapat dari pengguna.
* **Collaborative Filtering** memanfaatkan mengeksplorasi item atau konten di luar preferensi pengguna berdasarkan perilaku / kebiasaan si pengguna. Tujuannya agar pengguna yang sama dan item yang serupa dapat disukai oleh pengguna sebagai rekomendasi pilihan. Pada Collaborative Based Filtering, akan menggunakan penilaian dari pengguna lain untuk mendapatkan rekomendasi buku.[[3]](https://medium.com/data-folks-indonesia/recommendation-system-dengan-python-definisi-part-1-71154dc3f700)


## **Data Understanding**
---

**Sumber Data (Kaggle)** : [Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset)
Pada dataset ini akan menggunakan 2 buah dataframe saja, yaitu Book.csv dan Ratings.csv. Adapun fitur-fitur yang terdapat pada dataset Book.csv adalah sebagai berikut:
1. ISBN(String): Merupakan ISBN (International Standard Book Number) untuk buku yang terdaftar
2. Book-Title(String): Merupakan judul dari buku yang terdaftar
3. Book-Author(String): Merupakan penulis dari yang terdaftar
4. Year-of-Publication(String): Merupakan tahun terbitnya buku yang terdaftar
5. Publisher(String): Merupakan penerbit buku yang tedaftar
6. Image-URL-S(String): Merupakan tautan untuk gambar sampul berukuran kecil
7. Image-URL-M(String): Merupakan tautan untuk gambar sampul berukuran sedang
8. Image-ULR-L(String): Merupakan tautan untuk gambar sampul berukuran besar

Sedangkan fitur-fitur yang terdapat pada dataset Ratings.csv adalah sebagai berikut:
1. User-ID(String): Merupakan ID dari para pengguna
2. ISBN(String): Merupakan ISBN (International Standard Book Number) untuk buku yang terdaftar
3. Book-Rating(int): Merupakan penilaian dari pengguna terhadap suatu buku


## **Data Preparation**
---
Beberapa teknik yang diterapkan dalam penyiapan data (Data Preparation), yaitu:
* Dropna 
Dropna perlu digunakan dalam proses data preparation untuk membuang seluruh row yang memiliki NaN values. Sebuah model tidak dapat melakukan training apabila terdapat nilai NaN pada data latih.
* Drop Duplicates 
Drop dulicates digunakan dalam proses data preparation untuk membuang data - data yang terduplikasi. Adanya data yang terduplikasi membuat model berlatih menggunakan data yang berulang.

**Content Based Filtering** 
Pada Content Based Filtering preparation yang diperlukan ada 2, yaitu:
* Dataframe dari buku menjadi sebuah list Perubahan dari dataseries menjadi list dipenuhi dengan menggunakan .tolist() method. Proses ini diperlukan karena list ini akan digunakan pada tahap selanjutnya menjadi dictionary baru yg akan menjadi landasan pada sistem rekomendasi
* Memasukkan List ke Dictionary Setelah kita membuat list, kita perlu membuat dictionary yang digunakan untuk memnentukan pasangan key-value pada book_ISBN, book_title, book_author, dan book_year_of_publication.

**Collaborative Based Filtering** 
* Data preparation yang diperlukan pada sistem collaborative based filtering dimulai dengan menyandikan user_id pada rating_dataset dan ISBN pada book_dataset menjadi integer. Setelah disandikan, jumlah dari user_id dan ISBN tersebut akan disimpan pada num_users dan num_book.

Adapun pembagian Data Train dan Data Valid Setelah semua data sudah terkumpul, perlu membagi data tersebut menjadi data latih dan data validasi. Tetapi sebelum itu perlu untuk menarik sample dari dataset yang sudah ada.


## **Modeling**
---
**Content Based Filtering** 
Pada content Based Filtering, kita akan menggunakan TF-IDF Vectorizer untuk membangun sistem rekomendasi berdasarkan penulis buku. TF-IDF atau Term Frequency-Inverse Document Frequency memiliki fungsi untuk mengukur seberapa pentingnya suatu kata terhadap kata lain dalam dokumen. Pada umumnya menghitung skor untuk setiap kata agar menentukan pentingnya dalam sebuah dokumen dan corpus. Pada source code didefinisikan tf = TfidfVectorizer() selanjutnya mendapatkan kata penting dalam kolom book_author yang berasal dari attribut .get_feature_names() dari tf. Kemudian dari string yang didapat akan dimasukkan ke dalam matrik, dalam hal ini menggunakan tfidf_matrix sebagai matriks.

Dalam sistem rekomendasi ini dibutuhkan derajat kesamaan pada item, melalui buku dengan derajat kesamaan antar buku menggunakan cosine similarity. proses dilakukan agar item yang direkomendasikan tidak terlalu jauh dari data pusat. Selanjutnya terdapat fungsi author_recommendation dengan atribut argpartition berguna untuk mengambil sejumlah nilai k, dalam fungsi ini 5 tertinggi dari tingkat kesamaan yang berasal dari dataframe cosine_sim_df. Jumlah rekomendasi yang akan diberikan nantinya akan ditentukan oleh nilai k pada fungsi author_recommendation. Untuk mencari buku yang memiliki kemiripan dengan buku yang sudah dibaca. Setelah menjalankan kode di atas, akan mendapatkan 5 buku rekomendasi yang berasal dari penulis yang sama. Berikut adalah hasil rekomendasi untuk buku "The Diaries of Adam and Eve":

[![image](https://i.im.ge/2022/09/13/1TQ92p.image.png)](https://im.ge/i/1TQ92p)

Terlihat dari buku yang direkomendasikan berasal dari penulis buku yang sama. Buku yang memiliki penulis yang sama memiliki kesamaan konten, gaya penulisan, dan bahasa membuat pembaca nyaman dan tidak perlu beradaptasi dengan perubahan gaya penulisan dan bahasa yang ada.

**Collaborative Based Filtering** 
Model yang akan dipakai dalam Collaborative Based Filtering adalah RecommenderNet. Selanjutnya akan dilakukan proses compile pada model dengan binary crossentropy sebagai loss function, adam sebagai optimizer, dan RMSE sebagai metrik dari model. Setelah proses compile sudah selesai, akan dilatih model dengan batch_size 5 dan 50 epochs. Dalam mendapatkan rekomendasi, perlu untuk menambahkan beberapa kode tambahan, dimulai dengan mengambil user_id secara acak dari rating_dataset. Dari user_id ini dapat diketahui buku-buku yang pernah dibaca dan yang belum pernah dibaca, sehingga hanya dapat merekomendasikan buku yang belum dibaca. Setelah itu kita akan mendapatkan rekomendasi sesuai dengan user_id yang didapatkan. Contoh hasilnya adalah seperti berikut.

| No | Top 10 Book Recommendation for user: 853 |
| ------ | ------ |
| 01 | The Book of Lost Tales 1 (The History of Middle-Earth - Volume 1) : J. R. R. Tolkien
| 02 | Waking Up Screaming: Haunting Tales of Terror : H. P. Lovecraft
| 03 | Dharma Bums : Jack Kerouac
| 04 | Just Here Trying to Save a Few Lives : Tales of Life and Death from the ER : Pamela Grim
| 05 | 2061: Odyssey Three : Arthur C. Clarke
| 06 | The Book of Lost Tales 1 (The History of Middle-Earth - Volume 1) : J. R. R. Tolkien
| 07 | Waking Up Screaming: Haunting Tales of Terror : H. P. Lovecraft
| 08 | Dharma Bums : Jack Kerouac
| 09 | Just Here Trying to Save a Few Lives : Tales of Life and Death from the ER : Pamela Grim
| 10 | 2061: Odyssey Three : Arthur C. Clarke

## **Evaluasi**
---
**Content Based Filtering** 
Pada Content Based Filtering menggunakan akurasi sebagai metrik evaluasi. Akurasi pada Content Based Filtering adalah: Jumlah buku Berdasarkan Penulis Buku / Jumlah Buku yang Direkomendasikan. Dalam proses implementasi metrik akurasi pada projek adalah dengan membuat variabel **books_that_have_been_read_row** yang akan mengambil satu row dari buku yang pernah dibaca sebelumnya serta membuat juga variabel **books_that_have_been_read_author** sebagai penulis buku dari buku yang pernah dibaca sebelumnya.

Pada projek ini terdapat variabel **book_recommendation_authors** yang merupakan sebuah list yang terdiri dari penulis dari buku yang direkomendasikan oleh sistem. Kemudian terdapat looping yang merupakan proses manual di dalamnya setiap penulis dari buku yang direkomendasikan akan dipastikan, apabila sama maka variabel real_author akan bertambah 1.

Kemudian di bawah ini adalah hasil dari akurasi dari model sistem rekomendasi, di mana jumlah buku yang direkomendasikan sesuai dengan penulis buku (Variabel real_author) / Jumlah buku yang direkomendasikan (5).

[![image](https://i.im.ge/2022/09/13/1TTF5f.image.png)](https://im.ge/i/1TTF5f)

Kelebihan pada evaluasi metrik akurasi terletak pada kesederhanaannya untuk dipahami, karena metrik akurasi hanyalah jumlah yang benar dibandingkan dengan keseluruhan jawaban. Sedangkan kekurangan pada evaluasi metrik adalah terletak pada kesederhanannya pula, karena metrik akurasi hanya menghitung jumlah yang benar dibandingkan dengan keseluruhan jawaban dan tidak memperhitungkan aspek lainnya.

**Collaborative Based Filtering** 
Pada Collaborative Based Filtering menggunakan evaluasi metrik RMSE atau root-mean-square error.RMSE adalah ukuran yang sering digunakan untuk perbedaan antara nilai (nilai sampel atau populasi) yang diprediksi oleh model atau penduga dan nilai yang diamati. Berikut adalah rumus RMSE: 
[![image](https://i.im.ge/2022/09/13/1TTNk9.image.png)](https://im.ge/i/1TTNk9)
At = Nilai data Aktual 
Ft = Nilai hasil peramalan 
N= banyaknya data
∑ = Summation (Jumlahkan keseluruhan nilai)

 RMSE terlebih dahulu kita definisikan pada bagian metrik dalam model, kemudian kita visualisasikan lewat grafik. Adapun hasilnya seperti berikut.
 
[![image](https://i.im.ge/2022/09/13/1TTLux.image.png)](https://im.ge/i/1TTLux)

Dapat dilihat dari visualisasi di atas bahwa nilai dari RMSE pada data train terus menurun dari awal epoch (0) sampai epoch terakhir (50) mengalami penurunan dari yang awalnya mendekati nilai RMSE 0.10 menjadi nilai kurang dari RMSE 0.05 pada akhir epoch. Sedangkan untuk data test hampir sama dengan data train mengalami penurunan, perbedaanya dari data train terletak pada kisaran nilainya saja, yaitu RMSE 0,25. Dari data tersebut didapat kesimpulan model yang digunakan adalah baik karena  Root Mean Square Error (RMSE) merupakan besarnya tingkat kesalahan hasil prediksi, dimana semakin kecil (mendekati 0) nilai RMSE maka hasil prediksi akan semakin akurat. 

RMSE memiliki nilai yang lebih kecil daripada MSE, dengan adanya nilai kecil ini dapat menjadi kelebihan dan kekurangan tersendiri. Kelebihan dari nilai kecil adalah kita tidak perlu takut karena nilai error nya kecil dan kita dapat langsung masuk ke tahap selanjutnya, namun dengan nilai error yang kecil, kita dapat menjadi terlalu percaya diri dengan modelnya tanpa melihat posibilitas overfitting atau undefitting.


## **Daftar Pustaka**
---
[[1]](https://www.kominfo.go.id/content/detail/10862/teknologi-masyarakat-indonesia-malas-baca-tapi-cerewet-di-medsos/0/sorotan_media) E. Devega, "TEKNOLOGI Masyarakat Indonesia: Malas Baca Tapi Cerewet di Medsos," www.kominfo.go.id, 2017.
[[2]](http://www.gurusiana.id/read/fatchurrohman/article/membaca-belum-menjadi-habituasi-masyarakat-indonesia-523187#!) F. Rohman, "MEMBACA BELUM MENJADI HABITUASI MASYARAKAT INDONESIA," http://www.gurusiana.id/.
[[3]](https://medium.com/data-folks-indonesia/recommendation-system-dengan-python-definisi-part-1-71154dc3f700) N. Prasetio, "Recommendation System Dengan Python : Definisi (Part 1)," Medium, 2019.
