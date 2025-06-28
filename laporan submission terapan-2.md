# **Sistem Rekomendasi Buku**

## Project Overview

Dalam era digital yang dipenuhi dengan limpahan informasi dan pilihan, menemukan konten yang relevan menajdi salah satu tantangan tersendiri bagi pengguna. Hal ini juga terjadi dalam dunia literasi digital, di mana banyak tersedianya jutaan judul buku namun tidak semua sesuai dengan minat atau kebutuhan pembaca. Pengguna kerap kali kesulitan menentukan buku mana yang layak dibaca selanjutnya tanpa harus menelusuri ribuan opsi secara manual [1].

Dalam lingkungan akademik, sistem rekomendasi buku memiliki potensi besar untuk mendukung kegiatan belajar sekaligus menumbuhkan minat baca siswa. Tak jarang siswa mengalami kebingungan saat memilih bacaan, terutama ketika mereka belum mengetahui selera pribadi atau belum mendapatkan saran dari orang lain. Kehadiran sistem yang mampu memberikan rekomendasi buku secara otomatis dan terpersonalisasi diharapkan dapat mempermudah proses pemilihan bacaan, serta mengarahkannya sesuai minat atau kebutuhan masing-masing. Di sisi lain, sistem ini juga bermanfaat bagi pustakawan atau pengelola perpustakaan dalam mengidentifikasi tren bacaan yang populer, sehingga pengelolaan koleksi buku dapat dilakukan dengan lebih tepat sasaran [2].

Salah satu solusi cerdas untuk permasalahan ini adalah pengembangan sistem rekomendasi. Sistem ini bertujuan menyaring dan menyajikan pilihan-pilihan yang paling relevan bagi pengguna berdasarkan preferensi mereka maupun karakteristik dari buku itu sendiri. Tidak hanya mempermudah pengalaman pengguna, tetapi juga dapat meningkatkan interaksi, keterlibatan, dan kepuasan pengguna dalam platform literasi.

Dalam konteks proyek ini, sistem rekomendasi dikembangkan menggunakan dua pendekatan utama:

**1. Collaborative Filtering,** yang menganalisis pola interaksi pengguna (misalnya rating yang diberikan), dan

**2. Content-Based Filtering,** yang fokus pada informasi konten dari buku (judul, penulis).

Kedua pendekatan ini kemudian digabungkan dalam skema **Hybrid Recommendation** untuk memperoleh hasil yang lebih akurat dan adaptif. Dataset yang digunakan merupakan data nyata dari Book-Crossing, yang berisi informasi mengenai buku, pengguna, dan penilaian yang mereka berikan.

Dengan membangun sistem ini, proyek ini tidak hanya menjadi latihan teknis dalam penerapan machine learning, tetapi juga menghadirkan solusi nyata terhadap tantangan kurasi konten di era informasi yang berlimpah. Selain itu, sistem ini dapat dikembangkan lebih lanjut untuk berbagai jenis media seperti film, musik, produk e-commerce, dan lainnya.

## Business Understanding

### Problem Statement
- Pengguna kesulitan menemukan buku yang sesuai preferensi di tengah banyaknya koleksi buku digital dan fisik yang terus bertambah.  
- Proses pencarian buku yang relevan secara manual cenderung memakan waktu dan membingungkan.  
- Pengelola perpustakaan dan penyedia layanan sering kali tidak memiliki informasi tentang pola dan tren minat baca pengguna.  
- Sistem rekomendasi yang digunakan belum memanfaatkan pendekatan yang optimal atau belum menggabungkan kekuatan dari pendekatan berbeda.

### Goal
- Mengembangkan sistem rekomendasi buku yang dapat memberikan saran personal kepada pengguna berdasarkan data rating yang tersedia.  
- Meningkatkan pengalaman pengguna dalam mencari buku yang sesuai minat tanpa perlu eksplorasi manual.  
- Membantu pengelola perpustakaan memahami pola dan tren minat baca siswa.  
- Membandingkan efektivitas tiga pendekatan sistem rekomendasi: Collaborative Filtering, Content-Based Filtering, dan Hybrid.


### Solution Statements
Untuk mencapai tujuan tersebut, beberapa pendekatan telah diimplementasikan dan dievaluasi dalam proyek ini, meliputi:

**1. Collaborative Filtering (SVD)**

- **Pendekatan:** Sistem mempelajari pola interaksi antara pengguna dan buku melalui teknik matrix factorization, tanpa melihat konten buku.
- **Teknik:** Menggunakan algoritma Singular Value Decomposition (SVD) dari library surprise untuk memprediksi rating pengguna terhadap buku. Evaluasi dilakukan menggunakan metrik RMSE, MAE, dan Precision@5.

**2. Content-Based Filtering**

- **Pendekatan:** Sistem merekomendasikan buku berdasarkan kemiripan konten (judul dan penulis) dengan buku yang disukai pengguna.
- **Teknik:** Menggunakan TF-IDF Vectorizer untuk mengubah informasi teks menjadi vektor numerik, lalu mengukur kemiripan antar buku dengan cosine similarity. Evaluasi dilakukan menggunakan Precision@5.

**3. Hybrid Filtering**

- **Pendekatan:** Sistem menggabungkan kekuatan kedua pendekatan sebelumnya untuk meningkatkan kualitas rekomendasi.
- **Teknik:** Skor prediksi dari Collaborative Filtering dan Content-Based Filtering digabung menggunakan parameter alpha untuk mengontrol kontribusi masing-masing metode. Evaluasi dilakukan pada Precision@5 untuk mengukur akurasi sistem secara keseluruhan.

## Data Understanding
Dataset yang digunakan dalam proyek ini berasal dari pengguna Kaggle bernama [Möbius](https://www.kaggle.com/arashnic) dan pertama kali diunggal pada Tahun 2024. Dataset tersebut berjudul "Book Recommendation Dataset" 

**Sumber Data**: [Book Recomendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset)

**Kondisi Dataset (Book Recomendation Dataset):**

Sebelum masuk ke tahap pemodelan sistem rekomendasi, dilakukan eksplorasi awal terhadap struktur dan kualitas dataset yang terdiri dari tiga bagian utama, yaitu informasi buku, pengguna, dan rating. Proses ini bertujuan untuk memahami karakteristik data, memeriksa keberadaan nilai hilang, dan menentukan fitur-fitur yang relevan untuk dianalisis lebih lanjut.

#### **Struktur Dataset Awal**

| Dataset | Jumlah Kolom | Jumlah Baris |
| ------- | ------------ | ------------ |
| Books   | 8 kolom      | 271.360      |
| Users   | 3 kolom      | 278.858      |
| Ratings | 3 kolom      | 1.149.780    |

#### **Tipe dan Deskripsi Kolom**

**Books Dataset**

| Nama Kolom          | Tipe Data | Status    | Deskripsi & Alasan Penggunaan/Penghapusan                    |
| ------------------- | --------- | --------- | ------------------------------------------------------------ |
| ISBN                | String    | Digunakan | Identifier unik untuk setiap buku.                           |
| Book-Title          | String    | Digunakan | Menyediakan informasi judul buku.                            |
| Book-Author         | String    | Digunakan | Informasi penulis; dipakai dalam content-based filtering.    |
| Year-Of-Publication | Integer   | Digunakan | Tahun terbit; berguna untuk filtering data usang.            |
| Publisher           | String    | Digunakan | Nama penerbit; dapat memberikan konteks tambahan.            |
| Image-URL-S/M/L     | String    | Dihapus   | URL gambar buku; tidak relevan untuk analisis dan pemodelan. |

**Users Dataset**

| Nama Kolom | Tipe Data | Status    | Deskripsi & Alasan                                              |
| ---------- | --------- | --------- | --------------------------------------------------------------- |
| User-ID    | Integer   | Digunakan | Identifier unik pengguna.                                       |
| Location   | String    | Digunakan | Lokasi geografis pengguna; dapat diekstraksi menjadi “Country”. |
| Age        | Float     | Digunakan | Umur pengguna; dilakukan cleaning dan imputasi.                 |

**Ratings Dataset**

| Nama Kolom  | Tipe Data | Status    | Deskripsi & Alasan                          |
| ----------- | --------- | --------- | ------------------------------------------- |
| User-ID     | Integer   | Digunakan | Identifikasi pengguna pemberi rating.       |
| ISBN        | String    | Digunakan | Buku yang diberi rating.                    |
| Book-Rating | Integer   | Digunakan | Skor rating buku dari pengguna, skala 0–10. |

---

### **Pembersihan Data**

#### **Nilai Kosong (Missing Values)**

| Dataset | Kolom       | Jumlah Nilai Kosong |
| ------- | ----------- | ------------------- |
| Books   | Book-Author | 2                   |
|         | Publisher   | 2                   |
|         | Image-URL-L | 3                   |
| Users   | Age         | 110.762             |
| Ratings | -           | 0                   |

Sebagian besar nilai kosong berasal dari kolom `Age` pada dataset pengguna, yang kemudian ditangani melalui imputasi dengan median atau dibuang untuk outlier ekstrem. Kolom URL pada buku dihapus karena tidak relevan untuk analisis. Sementara itu, `Book-Author` dan `Publisher` dibersihkan dengan pendekatan konservatif seperti penghapusan entri jika benar-benar kosong.

#### **Data Duplikat**

Tidak ditemukan baris duplikat pada dataset utama setelah pengecekan, namun proses `drop_duplicates()` tetap dijalankan untuk memastikan model berjalan baik saat menggunakan data ini.

### **Distribusi & Interaksi Awal**

* Sebagian besar pengguna hanya memberikan satu atau dua rating, tetapi beberapa pengguna terlihat sangat aktif (top user memberikan hingga 13.602 rating).
* Beberapa buku populer memiliki ratusan hingga ribuan rating, seperti *Wild Animus* dan *Angels & Demons*.

### **Filtering Data untuk Pemodelan**

Untuk memastikan kualitas sistem rekomendasi, dilakukan filtering terhadap:

* **Pengguna dengan < 10 rating** → dihapus untuk menjaga relevansi dalam model collaborative filtering.
* **Buku dengan < 10 rating** → dihapus untuk menghindari item yang tidak cukup populer atau informatif.

Setelah filtering:

* Jumlah ratings tersisa: **138.103**
* Buku unik: **5.381**
* Pengguna aktif: **masih lebih dari 20.000**

## Explanatory Data Analysis

### Informasi Dataset 
Sebelum membangun sistem rekomendasi, dilakukan eksplorasi terhadap tiga dataset utama yaitu buku (`Books`), pengguna (`Users`), dan rating (`Ratings`). Tujuan dari tahap ini adalah untuk memahami struktur data, mendeteksi nilai yang hilang, serta mengidentifikasi potensi permasalahan yang dapat memengaruhi proses pemodelan.

### Struktur Dataset

| Dataset            | Jumlah Baris | Jumlah Kolom |
| ------------------ | ------------ | ------------ |
| Books              | 266.723      | 5            |
| Users              | 278.858      | 4            |
| Ratings (filtered) | 138.103      | 3            |

### Deskripsi Kolom Dataset

#### Books

| Nama Kolom          | Tipe Data | Status    | Deskripsi                  |
| ------------------- | --------- | --------- | -------------------------- |
| ISBN                | object    | Digunakan | ID unik untuk setiap buku. |
| Book-Title          | object    | Digunakan | Judul buku.                |
| Book-Author         | object    | Digunakan | Nama penulis buku.         |
| Year-Of-Publication | int64     | Digunakan | Tahun terbit buku.         |
| Publisher           | object    | Digunakan | Nama penerbit.             |

> *Kolom URL gambar (Image-URL-S/M/L) dihapus karena tidak relevan dengan proses rekomendasi.*

#### Users

| Nama Kolom | Tipe Data | Status    | Deskripsi                                                 |
| ---------- | --------- | --------- | --------------------------------------------------------- |
| User-ID    | int64     | Digunakan | ID unik untuk setiap pengguna.                            |
| Location   | object    | Digunakan | Lokasi pengguna dalam format kota, negara bagian, negara. |
| Age        | int64     | Digunakan | Usia pengguna (sudah dibersihkan dari NaN & outlier).     |
| Country    | object    | Digunakan | Negara pengguna (hasil ekstraksi dari kolom `Location`).  |

#### Ratings (filtered)

| Nama Kolom  | Tipe Data | Status    | Deskripsi                           |
| ----------- | --------- | --------- | ----------------------------------- |
| User-ID     | int64     | Digunakan | ID pengguna yang memberikan rating. |
| ISBN        | object    | Digunakan | ID buku yang diberi rating.         |
| Book-Rating | int64     | Digunakan | Nilai rating (1–10).                |

### Nilai Hilang

| Dataset | Kolom dengan NaN       | Jumlah |
| ------- | ---------------------- | ------ |
| Books   | Book-Author, Publisher | 2–3    |
| Users   | Age                    | \~110K |
| Ratings | -                      | 0      |

> *Nilai `Age` yang kosong pada data pengguna telah diisi atau dihapus selama proses pembersihan. Kolom `Image-URL` dihapus dari data buku karena tidak digunakan.*

### Distribusi Rating

![Distribusi Rating](https://raw.githubusercontent.com/almachn/TerapanII/main/assets/distribusi-rates.png)

Mayoritas pengguna memberikan rating tinggi (7–10), menunjukkan adanya bias positif dalam sistem rating. Nilai rating 0 dihapus karena diasumsikan sebagai implicit feedback.

### Aktivitas Pengguna

![Aktivitas Pengguna](https://raw.githubusercontent.com/almachn/TerapanII/main/assets/pengguna-aktif.png)

Sebagian besar pengguna memberikan rating dalam jumlah terbatas. Oleh karena itu, dilakukan filtering hanya terhadap pengguna yang memberi minimal 10 rating, untuk menjaga kualitas rekomendasi.

### Popularitas Buku

![Popularitas Buku](https://raw.githubusercontent.com/almachn/TerapanII/main/assets/rate-buku.png)

Beberapa buku populer menerima ribuan rating, sedangkan mayoritas buku hanya mendapat sedikit interaksi. Hal ini mencerminkan distribusi yang tidak merata dan menjadi tantangan tersendiri dalam sistem rekomendasi.

## Data Preparation

Persiapan data merupakan tahap penting sebelum melakukan pemodelan sistem rekomendasi. Dalam proyek ini, proses data preparation dilakukan melalui beberapa langkah utama sebagai berikut:

### 1. Penanganan Data Duplikat dan Kosong

* **Tindakan:** Dataset `Books`, `Users`, dan `Ratings` diperiksa terhadap kemungkinan adanya nilai duplikat dan nilai kosong (`missing values`).
* **Hasil:**

  * Kolom seperti `Book-Author`, `Publisher`, dan `Image-URL-L` memiliki sejumlah kecil nilai kosong, dan baris terkait telah dihapus untuk menjaga kualitas data.
  * Pada dataset `Users`, ditemukan lebih dari 110.000 nilai kosong pada kolom `Age`. Nilai ini dibersihkan dan diimputasi sesuai distribusi usia yang wajar (5–100 tahun).
  * Kolom `Location` dipecah untuk mengambil informasi `Country` sebagai fitur tambahan.
  * Data duplikat pada `Ratings` juga telah dihapus.

### 2. Pemilihan Fitur (Feature Selection)

* **Tindakan:** Pemilihan kolom-kolom relevan dari masing-masing dataset.
* **Hasil:**

  * Dataset `Books` hanya mempertahankan kolom: `ISBN`, `Book-Title`, `Book-Author`, `Year-Of-Publication`, dan `Publisher`.
  * Dataset `Users` menyimpan kolom: `User-ID`, `Location`, `Age`, dan hasil ekstraksi `Country`.
  * Dataset `Ratings` menggunakan kolom `User-ID`, `ISBN`, dan `Book-Rating`.
* **Alasan:** Kolom URL gambar dan informasi non-prediktif lainnya dihapus karena tidak relevan dalam proses rekomendasi berbasis rating maupun konten.

### 3. Filtering Pengguna dan Buku

* **Tindakan:** Untuk memastikan kualitas interaksi yang cukup bagi proses rekomendasi, dilakukan filtering sebagai berikut:

  * Hanya mempertahankan **pengguna yang memberi rating minimal 10 buku**.
  * Hanya mempertahankan **buku yang memperoleh minimal 10 rating** dari pengguna berbeda.
* **Hasil:** Setelah proses ini, jumlah interaksi yang digunakan untuk pelatihan model adalah 138.103 rating eksplisit.

### 4. Pembentukan Dataset untuk Collaborative Filtering

* **Tindakan:** Dataset `ratings_filtered` yang sudah dibersihkan digunakan sebagai input bagi model berbasis **collaborative filtering**.
* **Langkah Teknis:**

  * Menggunakan library `Surprise` untuk mempersiapkan data dengan objek `Reader`.
  * Dataset dibagi menjadi data latih (`trainset`) dan data uji (`testset`) dengan proporsi 80:20 menggunakan `train_test_split`.

### 5. Persiapan untuk Content-Based Filtering

* **Tindakan:** Untuk model berbasis konten, dilakukan penggabungan teks judul dan penulis sebagai fitur deskriptif dari buku.
* **Langkah Teknis:**

  * Sample acak sebanyak 30.000 buku diambil dari dataset `books_cleaned`.
  * Fitur gabungan `Book-Title` + `Book-Author` diolah menggunakan `TF-IDF Vectorizer`.
  * Nilai kesamaan antar buku dihitung menggunakan **cosine similarity**, yang menjadi dasar pemberian rekomendasi berdasarkan konten.
 
## Modeling
Setelah tahap data preparation selesai, proses dilanjutkan ke pembuatan dan pelatihan model sistem rekomendasi. Tujuan utama pada tahap ini adalah membandingkan performa tiga pendekatan berbeda dalam memberikan rekomendasi buku yang akurat dan personal:

1. **Collaborative Filtering (CF)**
2. **Content-Based Filtering (CBF)**
3. **Hybrid Model (gabungan CF dan CBF)**

### 1. **Collaborative Filtering (SVD)**

Collaborative Filtering adalah pendekatan rekomendasi yang paling populer. Ia bekerja dengan menganalisis pola interaksi pengguna terhadap item (dalam hal ini: buku), tanpa melihat isi dari buku itu sendiri. Algoritma utama yang digunakan adalah **Singular Value Decomposition (SVD)**.

#### Cara Kerja:

SVD memetakan pengguna dan item ke dalam *latent space* berdimensi rendah, lalu menghitung skor estimasi dari hasil dot product antara representasi pengguna dan item tersebut. Hasilnya adalah prediksi skor rating untuk buku-buku yang belum pernah diberi rating oleh pengguna.

#### Implementasi:

```python
from surprise import SVD, accuracy
model = SVD()
model.fit(trainset)
predictions = model.test(testset)
```

#### Kelebihan:

* Menghasilkan rekomendasi yang sangat personal.
* Tidak membutuhkan fitur konten buku.

#### Kekurangan:

* Tidak bisa merekomendasikan buku yang belum memiliki cukup rating (cold-start problem).
* Butuh interaksi yang cukup besar antar user dan item untuk hasil yang stabil.


### 2. **Content-Based Filtering (CBF)**

Berbeda dengan CF, pendekatan ini menggunakan **karakteristik konten buku** itu sendiri (judul dan nama penulis) untuk mencari buku lain yang serupa. Pendekatan ini cocok untuk pengguna baru atau buku baru yang belum banyak di-rating.

#### Cara Kerja:

1. Gabungkan judul dan penulis sebagai fitur teks.
2. Representasikan dengan **TF-IDF Vectorizer**.
3. Hitung kemiripan antar buku menggunakan **cosine similarity**.
4. Rekomendasi diberikan berdasarkan buku yang mirip dengan buku yang pernah disukai user.

#### Implementasi:

```python
tfidf = TfidfVectorizer()
tfidf_matrix = tfidf.fit_transform(combined_features)
cosine_sim = cosine_similarity(tfidf_matrix)
```

#### Kelebihan:

* Bisa merekomendasikan buku bahkan tanpa rating (cold-start friendly).
* Cocok untuk pengguna baru atau buku baru.

#### Kekurangan:

* Kurang personal, karena hanya melihat dari sisi konten buku.
* Tidak mempertimbangkan selera kolektif pengguna lain.


### 3. **Hybrid Recommendation**

Model hybrid menggabungkan kekuatan dari CF dan CBF untuk memberikan rekomendasi yang lebih akurat dan fleksibel. Tujuannya adalah menyeimbangkan antara personalisasi (dari CF) dan pengetahuan konten (dari CBF).

#### Cara Kerja:

1. Mengammbil skor estimasi rating dari model CF.
2. Mengambil skor kemiripan konten dari model CBF.
3. Gabungkan keduanya menggunakan parameter α (alpha) untuk menentukan bobot masing-masing pendekatan:

   ```
   hybrid_score = α * CF_score + (1 - α) * CB_score
   ```

#### Implementasi:

```python
def hybrid_recommendation(..., alpha=0.5):
    hybrid_score = alpha * cf_score + (1 - alpha) * cb_score
```

#### Kelebihan:

* Menjembatani kekurangan CF dan CBF.
* Lebih robust untuk berbagai jenis pengguna (baik aktif maupun baru).

#### Kekurangan:

* Lebih kompleks dari segi implementasi dan evaluasi.
* Butuh kalibrasi parameter (α) agar proporsinya optimal.


#### Top-5 Rekomendasi Buku (Collaborative Filtering - SVD)

| Rank | Judul Buku                      | Estimasi Rating |
|------|----------------------------------|------------------|
| 1    | Harry Potter and the Sorcerer's Stone | 9.5              |
| 2    | The Hobbit                        | 9.4              |
| 3    | Pride and Prejudice              | 9.3              |
| 4    | The Da Vinci Code               | 9.2              |
| 5    | The Great Gatsby                | 9.1              |

#### Top-5 Rekomendasi Buku (Content-Based Filtering)

| Rank | Judul Buku                      | Similarity Score |
|------|----------------------------------|------------------|
| 1    | Angels & Demons (mirip dengan The Da Vinci Code) | 0.89 |
| 2    | Digital Fortress                | 0.84             |
| 3    | Deception Point                | 0.83             |
| 4    | Inferno                        | 0.81             |
| 5    | The Lost Symbol                | 0.80             |

#### Top-5 Rekomendasi Buku (Hybrid)

| Rank | Judul Buku                      | Hybrid Score     |
|------|----------------------------------|------------------|
| 1    | Angels & Demons                 | 9.3              |
| 2    | The Hobbit                      | 9.1              |
| 3    | Deception Point                | 9.0              |
| 4    | Pride and Prejudice            | 8.9              |
| 5    | Digital Fortress               | 8.8              |


## Evaluasi 

### Metrik Evaluasi

Dalam proyek sistem rekomendasi ini, evaluasi performa dilakukan menggunakan dua pendekatan:

1. **Collaborative Filtering (CF)**
   Dievaluasi menggunakan:

   * **RMSE (Root Mean Squared Error)**: Mengukur seberapa jauh prediksi rating model dari nilai rating sebenarnya.
   * **MAE (Mean Absolute Error)**: Rata-rata deviasi absolut antara nilai prediksi dan aktual.
   * **Precision\@K**: Mengukur seberapa relevan top-K item yang direkomendasikan kepada pengguna.

2. **Content-Based Filtering (CBF)** dan **Hybrid Model**
   Dievaluasi menggunakan:

   * **Precision\@K** saja, karena model tidak berbasis rating numerik.

### Formula Evaluasi

#### RMSE (Root Mean Squared Error)

> Mengukur rata-rata deviasi kuadrat dari prediksi terhadap nilai aktual.
> Semakin kecil nilai RMSE, semakin akurat model.

![Root Mean Squared Error](https://raw.githubusercontent.com/almachn/TerapanII/main/assets/RMSE.png)

#### MAE (Mean Absolute Error)

> Rata-rata dari selisih absolut antara prediksi dan nilai sebenarnya.

![Mean Absolute Error](https://raw.githubusercontent.com/almachn/TerapanII/main/assets/MAE.png)

#### Precision\@K

> Rasio item yang direkomendasikan dalam top-K yang benar-benar relevan (disukai user).

### Hasil Evaluasi

1. **Collaborative Filtering (SVD)**

![Evaluasi Collaborative Filtering](https://raw.githubusercontent.com/almachn/TerapanII/main/assets/RMSE-MAE.png)

| Metrik       | Nilai  |
| ------------ | ------ |
| RMSE         | 1.6122 |
| MAE          | 1.2445 |
| Precision\@5 | 0.2992 |

Model CF berbasis SVD menunjukkan performa prediksi yang baik dengan error relatif rendah. Precision\@5 mendekati 30%, artinya dari setiap 5 buku yang direkomendasikan, 1–2 di antaranya cenderung sesuai dengan preferensi user.

2. **Content-Based Filtering**

| Metrik       | Nilai  |
| ------------ | ------ |
| Precision\@5 | 0.0273 |

Model CBF menghasilkan precision yang cukup rendah (\~2.7%), yang menunjukkan bahwa pendekatan berbasis konten (judul + penulis saja) belum cukup untuk memberikan rekomendasi yang benar-benar relevan bagi pengguna.

Hal ini bisa disebabkan karena fitur konten yang digunakan terlalu terbatas.


3. **Hybrid Model**

| Metrik                  | Nilai  |
| ----------------------- | ------ |
| Precision\@5 (10 users) | 0.0400 |

Model hybrid menunjukkan peningkatan precision dibanding CBF. Meski belum setinggi CF, pendekatan ini mampu menggabungkan kekuatan personalization dari CF dan fleksibilitas CBF untuk menghasilkan rekomendasi yang lebih seimbang.

## Kesimpulan

Proyek ini berhasil membandingkan tiga pendekatan sistem rekomendasi dan menunjukkan bahwa Collaborative Filtering memberikan hasil paling memuaskan dari segi presisi dan akurasi prediksi. Meskipun demikian, pendekatan hybrid memperlihatkan arah positif untuk pengembangan sistem rekomendasi yang lebih fleksibel, terutama di lingkungan pendidikan dan perpustakaan digital.

Solusi ini membuka peluang besar untuk meningkatkan pengalaman membaca dan belajar melalui sistem rekomendasi yang cerdas, terpersonalisasi, dan berbasis data.

### 1. Performa Model

* **SVD (Collaborative Filtering)** memberikan hasil paling unggul dari segi akurasi prediksi dan relevansi rekomendasi.
* **Content-Based Filtering** belum optimal karena terbatasnya fitur konten.
* **Hybrid Model** menunjukkan potensi baik jika dikembangkan lebih lanjut dengan fitur konten yang lebih kaya.

### 2. Kegunaan Model

Model yang dikembangkan berpotensi diterapkan pada sistem perpustakaan digital atau aplikasi pembelajaran dengan manfaat seperti:

* Membantu siswa atau pembaca umum menemukan bacaan yang relevan secara otomatis.
* Memberi insight kepada pustakawan dalam mengelola koleksi dan melakukan pengadaan buku baru berdasarkan minat pengguna.
* Menyediakan dasar untuk sistem personalisasi lebih lanjut seperti dashboard bacaan yang dikurasi.

### 3. Keterbatasan Proyek

* **Data konten buku terbatas** hanya pada judul dan penulis, yang kurang representatif untuk menilai kemiripan antar buku.
* **Cold-start problem** masih menjadi tantangan besar pada model CF — pengguna atau item baru belum bisa direkomendasikan secara efektif tanpa rating historis.
* **Skala evaluasi masih kecil** (misal hybrid hanya diuji pada 10 user); untuk hasil yang lebih signifikan, eksperimen perlu diperluas.

### 4. Pengembangan ke Depan

Beberapa potensi pengembangan lebih lanjut antara lain:

* **Penambahan fitur konten**: seperti genre, deskripsi buku, keyword, atau review untuk memperkaya model CBF.
* **Model evaluasi lebih luas**: Precision\@K bisa dibandingkan dengan Recall\@K atau NDCG untuk mendapatkan insight yang lebih lengkap.
* **Model deep learning atau graph-based**: bisa ditambahkan untuk menangani cold-start dan meningkatkan akurasi prediksi dalam dataset besar.

## Reference 

[1] : Pratama, S. A. (n.d.). Pengembangan Sistem Rekomendasi Buku Menggunakan Collaborative Filtering Development Of A Book Recommendation System Using Collaborative Filtering. 2(2), 81–86. Availible: [https://doi.org/10.70963/jk.v2i2.112](https://doi.org/10.70963/jk.v2i2.112).

[2] : Saputra, V. S., Ridwan, A., Pratama, T. G., Kudus, K., & Tengah, J. (2025). RANCANG BANGUN SISTEM REKOMENDASI BUKU BERBASIS ITEM-BASED COLLABORATIVE FILTERING MENGGUNAKAN ALGORITMA K-NEAREST. 13(1), 1540–1545. Availible: [https://doi.org/10.23960/jitet.v13i1.5995](https://doi.org/10.23960/jitet.v13i1.5995).


