# Tugas Kelompok 6 OpenCV

**Mata Kuliah:** Machine Learning & Computer Vision  
**Dosen Pengampu:** Herfandi, Ph.D. — Informatika — Universitas Teknologi Sumbawa (UTS)

---

## Profil Kelompok

| No | Nama | NIM |
|----|------|-----|
| 1 | Sherly Novia Indriani | 231001057 |
| 2 | Dinda Oktavia Pratiwi | 231001026 |
| 3 | Ahsanul Ikram | 231001077 |
| 4 | Wanda Setya Budi | 231001008 |

**Kelas:** Informatika — [C]

---

## Deskripsi Proyek

Repositori ini merupakan dokumentasi teknis hasil praktik kelompok mengenai implementasi **Machine Learning berbasis OpenCV** untuk sistem **Face Recognition**. Praktikum ini memperkenalkan pendekatan klasik yang menggabungkan **Local Binary Pattern Histogram (LBPH)** sebagai metode ekstraksi fitur wajah dengan **Support Vector Machine (SVM)** sebagai classifier, sebagai alternatif yang lebih kuat dibanding pendekatan Nearest Neighbor bawaan OpenCV.

Materi praktik mencakup perbandingan beberapa implementasi secara menyeluruh — mulai dari SVM dasar, LBPH custom, hingga kombinasi keduanya menggunakan dua library berbeda (OpenCV ML dan Scikit-Learn) — dan diakhiri dengan deployment sistem pengenalan wajah secara real-time menggunakan kamera.

---

## Lingkungan Pengembangan (Environment)

Seluruh skrip dalam repositori ini disusun dan diuji menggunakan spesifikasi berikut:

* **Kode Editor:** Jupyter Notebook / Visual Studio Code
* **Interpreter:** Python 3.x
* **Library Utama:** OpenCV (`cv2`), Scikit-Learn, Scikit-Image, NumPy, Matplotlib, Pickle

---

## Cakupan Praktikum

Tahapan implementasi yang dilakukan mencakup:

1. **SVM Dasar dengan OpenCV ML:** Membangun dan melatih model SVM sederhana menggunakan data 2D untuk memahami konsep *hyperplane*, *kernel*, parameter `C` (regularisasi), dan *term criteria* sebelum diterapkan pada data wajah.

2. **Load & Preprocessing Dataset:** Membaca dataset wajah LFW dari struktur folder, mendeteksi dan meng-crop area wajah menggunakan Haar Cascade Classifier, lalu melakukan resize dan konversi ke grayscale agar konsisten sebagai input model.

3. **Label Encoding & Split Dataset:** Mengubah label nama menjadi representasi integer menggunakan `LabelEncoder` dari Scikit-Learn, lalu membagi dataset menjadi *training set* (75%) dan *test set* (25%) menggunakan `train_test_split`.

4. **Implementasi LBPH Manual (Tanpa OpenCV):** Membangun kelas `LBPHFaceRecognizer_custom` dari nol menggunakan Scikit-Image untuk ekstraksi LBP, teknik *sliding window* untuk histogram per blok, dan metrik **Chi-Square distance** dengan Nearest Neighbors sebagai classifier.

5. **Perbandingan dengan LBPH OpenCV:** Menjalankan `cv2.face.LBPHFaceRecognizer_create()` bawaan OpenCV dan membandingkan hasilnya secara kuantitatif dengan implementasi custom.

6. **LBPH + SVM OpenCV (V1):** Mengganti classifier Nearest Neighbor dengan **SVM kernel Chi2 dari OpenCV ML**, menyimpan model ke format `.yml`, dan mengevaluasi peningkatan performa dibanding LBPH + Nearest Neighbor.

7. **LBPH + SVM Scikit-Learn (V2):** Membangun ulang pipeline menggunakan **SVC dari Scikit-Learn dengan precomputed kernel** dan Gram Matrix Chi-Square, menyimpan model dengan **Pickle** (`.pkl`), dan membandingkan hasilnya dengan V1.

8. **Evaluasi Model:** Menganalisis performa setiap pendekatan secara komprehensif menggunakan *Confusion Matrix* dan *Classification Report* (Precision, Recall, F1-Score) per kelas.

9. **Pengumpulan Data Wajah Sendiri:** Menangkap foto wajah anggota kelompok menggunakan kamera laptop, menyimpan ke folder dataset, dan melatih ulang model dengan kelas baru tersebut.

10. **Face Recognition Real-Time (Video Frame):** Mengintegrasikan seluruh pipeline ke dalam sistem inferensi real-time — Haar Cascade untuk deteksi, LBPH untuk ekstraksi fitur, SVM untuk identifikasi — dengan anotasi bounding box dan nama langsung di frame video.

---

## 🔍 Analisis & Kesimpulan Teknis

1. **Chi-Square sebagai Metrik Histogram:** Dibanding Euclidean distance, Chi-Square terbukti lebih tepat untuk membandingkan distribusi histogram karena memperhitungkan proporsi relatif tiap bin, bukan hanya selisih absolutnya. Ini menjadikannya pilihan utama dalam sistem berbasis LBPH.

2. **Keunggulan SVM atas Nearest Neighbor:** LBPH + SVM secara konsisten menghasilkan F1-Score yang lebih tinggi dibanding LBPH + Nearest Neighbor. SVM mencari *optimal hyperplane* yang memaksimalkan margin antar kelas, sehingga lebih tahan terhadap variasi dan noise dalam data wajah.

3. **Precomputed Kernel sebagai Fleksibilitas:** Pendekatan V2 dengan `kernel='precomputed'` pada Scikit-Learn memungkinkan penggunaan fungsi kernel kustom (Chi-Square) yang tidak tersedia secara bawaan. Ini membuka ruang untuk bereksperimen dengan berbagai metrik jarak tanpa bergantung pada implementasi library.

4. **Pentingnya Pickle untuk Model Scikit:** Berbeda dengan OpenCV yang memiliki method `.save()` ke format `.yml`, model Scikit-Learn harus disimpan menggunakan Pickle. Pemahaman ini krusial untuk deployment model di lingkungan produksi.

5. **Kesimpulan:** Kombinasi LBPH (feature extractor) + SVM (classifier) merupakan fondasi yang kuat untuk sistem face recognition klasik. Meski kini telah banyak digantikan oleh deep learning, pemahaman mendalam atas pipeline ini — mulai dari ekstraksi fitur manual hingga pemilihan classifier — tetap menjadi bekal esensial sebelum beralih ke arsitektur CNN dan jaringan yang lebih kompleks.

---

## 📽️ Presentasi Video

Demonstrasi lengkap pipeline, penjelasan kode baris demi baris oleh seluruh anggota kelompok, serta hasil inferensi real-time dapat diakses melalui tautan berikut:

👉 *[https://youtu.be/dHVrrN_YQVc]*

---
