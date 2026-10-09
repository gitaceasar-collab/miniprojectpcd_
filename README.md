# miniprojectpcd_

Mini Project: OCR Nomor Ijazah dan Deteksi Indikasi Tanda Tangan

Grayscale Conversion

Metode: Mengubah citra RGB (3 channel) menjadi citra keabu-abuan (1 channel).

Fungsi: Mempermudah pemrosesan citra, mempercepat komputasi, dan mengabaikan distorsi warna latar belakang.

Global Image Enhancement (Denoising)

Metode: Fast Non-Local Means Denoising (cv2.fastNlMeansDenoising).

Fungsi: Menghilangkan noise atau bintik-bintik pada hasil scan/foto ijazah tanpa mengaburkan tepi teks dan garis tanda tangan.

Segmentation / Region of Interest (ROI)

Area Nomor: Pemotongan (cropping) fokus pada area koordinat lokasi nomor ijazah.

Area Tanda Tangan: Pemotongan (cropping) fokus pada area lokasi tanda tangan pejabat berwenang.

Enhancement & Thresholding Area Nomor

Metode: CLAHE (Contrast Limited Adaptive Histogram Equalization) dipadukan dengan Otsu Binarization.

Fungsi: CLAHE meratakan kontras secara lokal pada area nomor ijazah (mengatasi bayangan/watermark latar belakang), lalu Otsu Binarization mengubahnya menjadi citra biner hitam-putih yang sangat tajam untuk dibaca OCR.

Thresholding & Morphology Area Tanda Tangan

Thresholding: Otsu Inverted Thresholding (cv2.THRESH_BINARY_INV + cv2.THRESH_OTSU) untuk memisahkan garis tinta dari background.

Morphology: Operasi Morphological Closing (cv2.MORPH_CLOSE) menggunakan kernel persegi untuk menghubungkan coretan atau garis pen yang terputus-putus.

Signature Detection: Menghitung pixel density ratio (rasio piksel tinta terhadap luas ROI). Jika densitas piksel melebihi nilai ambang batas (threshold), maka tanda tangan dikategorikan sebagai PRESENT, jika tidak maka ABSENT.

OCR (Optical Character Recognition)

Metode: Tesseract OCR Engine (pytesseract) dengan konfigurasi --psm 6.

Fungsi: Mengonversi citra biner nomor ijazah menjadi karakter teks/string.

