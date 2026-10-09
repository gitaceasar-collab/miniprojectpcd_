# miniprojectpcd_

# miniproject-ocr-ijazah

## Mini Project: OCR Nomor Ijazah dan Deteksi Indikasi Tanda Tangan

### 1. Deskripsi Proyek
Mini project ini dibuat untuk menerapkan pengolahan citra digital dalam membaca nomor ijazah menggunakan Optical Character Recognition (OCR) serta mendeteksi indikasi tinta pada area tanda tangan kepala sekolah.

Proyek ini menggunakan Python dan beberapa library pengolahan citra untuk meningkatkan kualitas gambar sebelum dilakukan proses OCR. Pengujian dilakukan pada sembilan gambar dengan kondisi kualitas yang berbeda, seperti gambar buram, kontras rendah, noise tinggi, resolusi rendah, dan kompresi JPEG.

---

### 2. Metode yang Digunakan
Metode yang digunakan dalam proyek ini meliputi:

1. **Grayscale**: Mengubah gambar berwarna menjadi gambar abu-abu untuk menyederhanakan proses pengolahan citra.
2. **Denoising**: Mengurangi noise atau bintik-bintik pada gambar sehingga karakter lebih mudah dikenali oleh sistem OCR.
3. **CLAHE (Contrast Limited Adaptive Histogram Equalization)**: Meningkatkan kontras lokal gambar agar karakter nomor ijazah lebih mudah terlihat, terutama pada gambar dengan kontras rendah.
4. **Adaptive Thresholding (Otsu Binarization)**: Mengubah gambar menjadi hitam-putih berdasarkan kondisi pencahayaan lokal untuk membantu memisahkan karakter dari latar belakang.
5. **Region of Interest (ROI)**: Memotong bagian gambar yang berisi nomor ijazah dan area tanda tangan agar pemrosesan lebih terfokus.
6. **Morphological Operations**: Penggunaan operasi *closing* pada area tanda tangan untuk menyambungkan stroke atau garis tinta yang terputus.
7. **Optical Character Recognition (OCR)**: Menggunakan Tesseract OCR untuk membaca dan mengekstrak angka dari area nomor ijazah.
8. **Character Error Rate (CER)**: Digunakan untuk mengukur tingkat kesalahan hasil OCR dengan membandingkan teks hasil pengenalan terhadap nomor ijazah acuan (*ground truth*). Semakin rendah nilai CER, semakin akurat hasil pengenalan karakter.
9. **Deteksi Indikasi Tinta Tanda Tangan**: Dilakukan dengan menghitung rasio piksel gelap pada area tanda tangan. Hasilnya digunakan sebagai indikator sederhana adanya tinta, bukan untuk membuktikan keaslian tanda tangan.

---

### 3. Hasil dan Analisis Enhancement Berdasarkan CER
Evaluasi dilakukan menggunakan Character Error Rate (CER) untuk mengetahui seberapa akurat hasil OCR dalam membaca nomor ijazah setelah proses preprocessing.

Nilai CER dihitung dengan membandingkan hasil OCR dengan nomor ijazah acuan yang telah ditentukan. Metode enhancement dengan nilai CER rata-rata paling rendah dianggap paling efektif untuk dataset yang diuji karena menghasilkan kesalahan pengenalan karakter yang lebih sedikit.

#### Hasil eksperimen:
- **Metode enhancement paling efektif**: CLAHE + Otsu Binarization
- **Nilai rata-rata CER**: 2.21% (CER Terendah: 1.00%, CER Tertinggi: 11.85%)

Berdasarkan hasil evaluasi, metode **CLAHE + Otsu Binarization** memperoleh nilai CER paling rendah dibandingkan metode lainnya. Hal ini menunjukkan bahwa metode tersebut memberikan hasil pengenalan nomor ijazah yang paling akurat pada dataset pengujian.

Hasil ini terbatas pada gambar dan pengaturan eksperimen yang digunakan. Metode dengan CER terendah belum tentu memberikan hasil terbaik pada semua jenis dokumen atau kondisi gambar.

---

### 4. Dataset
Dataset terdiri dari sembilan gambar dengan variasi kualitas, yaitu:
- Gambar berkualitas tinggi (`01_HighQuality_Enhanced.jpg`)
- Gambar dengan kontras rendah (`02_LowContrast.jpg`)
- Gambar buram (`03_Blurred.jpg`)
- Gambar dengan noise tinggi (`04_HighNoise.jpg`)
- Gambar beresolusi rendah (`05_LowResolution_Upsampled.jpg`)
- Gambar dengan pencahayaan rendah (`06_Faded_Underexposed.jpg`)
- Gambar dengan perubahan warna (`07_ColorShift_WarmTint.jpg`)
- Gambar dengan artefak kompresi JPEG (`08_JPEGCompression_Artifacts.jpg`)
- Gambar dengan gabungan beberapa gangguan kualitas (`09_CombinedDegradation.jpg`)

Dataset digunakan untuk menguji kemampuan preprocessing dan OCR dalam menghadapi variasi kualitas citra.

---

### 5. Teknologi dan Library
Proyek ini menggunakan:
- **Python**
- **Google Colab**
- **OpenCV**
- **Tesseract OCR**
- **Pytesseract**
- **NumPy**
- **Pandas**
- **Matplotlib**
- **Jiwer**

---

### 6. Output Program
Output dari program ini meliputi:
- Hasil preprocessing gambar (Grayscale, CLAHE, Thresholding, Morphology).
- Hasil ekstraksi nomor ijazah menggunakan OCR.
- Indikasi tinta pada area tanda tangan (`PRESENT` / `ABSENT`).
- Nilai CER untuk mengevaluasi akurasi OCR.
- Tabel ringkasan hasil eksperimen.
- File CSV hasil evaluasi (`hasil_evaluasi_9_gambar.csv`, `ringkasan_eksperimen.csv`).

---

### 7. Cara Menjalankan Program (How to Run)
Program dijalankan menggunakan Google Colab. Berikut langkah-langkahnya:

1. Buka [https://colab.research.google.com/](https://colab.research.google.com/).
2. Unggah atau buka file notebook proyek dengan format `.ipynb` (`Tugas7_PCD.ipynb`).
3. Jalankan sel instalasi library dan impor seluruh library yang dibutuhkan:
   ```bash
   !apt-get update -y
   !apt-get install -y tesseract-ocr tesseract-ocr-ind
   !pip install pytesseract opencv-python matplotlib numpy jiwer pandas

### 8. Kesimpulan
Proyek ini menunjukkan penerapan pengolahan citra digital dan OCR untuk membantu membaca nomor ijazah pada gambar dengan kondisi kualitas yang berbeda. Metode preprocessing digunakan untuk meningkatkan keterbacaan karakter sebelum proses OCR dilakukan.

Efektivitas metode enhancement dievaluasi menggunakan CER. Metode dengan nilai CER rata-rata paling rendah dipilih sebagai metode paling efektif berdasarkan hasil eksperimen. Evaluasi ini membantu mengetahui pengaruh preprocessing terhadap akurasi pengenalan karakter.

Deteksi tinta tanda tangan hanya digunakan sebagai indikasi sederhana berdasarkan piksel gelap, sehingga tidak dapat digunakan untuk memastikan keaslian tanda tangan.
