# PA_PC_202231039_IKHWANUL-FATIHA_C_A
## MEMBUAT LIBRARY
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
import skimage
```
*
Menggunakan library cv2 digunakan untuk memproses gambar dan video.
Library matplotlib.pyplot digunakan untuk menampilkan gambar.
Library numpy digunakan untuk melakukan operasi aritmatika.
%matplotlib inline adalah magic command di Jupyter Notebook yang memberitahu notebook untuk menampilkan plot secara langsung di dalam notebook, bukan di jendela terpisah.
skimage atau scikit-image adalah pustaka untuk pemrosesan gambar di Python.
```python
image = cv2.imread('fatih ni.jpg')

cv2.imshow("Fatih", image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
*
image = cv2.imread('fatih ni.jpg')
cv2.imread adalah fungsi dari OpenCV yang digunakan untuk membaca gambar dari file. Fungsi ini mengambil nama file sebagai argumen dan mengembalikan gambar sebagai array numpy.

cv2.imshow("Fatih", image)
cv2.imshow adalah fungsi dari OpenCV yang digunakan untuk menampilkan gambar di jendela. Fungsi ini mengambil dua argumen: nama jendela (dalam hal ini, "Fatih") dan gambar yang akan ditampilkan.

cv2.waitKey(0)
cv2.waitKey adalah fungsi dari OpenCV yang menunggu penekanan tombol. Argumen 0 berarti menunggu tanpa batas waktu hingga tombol ditekan.

cv2.destroyAllWindows()
cv2.destroyAllWindows adalah fungsi dari OpenCV yang digunakan untuk menutup semua jendela yang dibuat oleh cv2.imshow.
```python
color_image = cv2.cvtColor(cv2.imread('fatih ni.jpg'), cv2.COLOR_BGR2RGB)
gray = cv2.cvtColor(color_image, cv2.COLOR_BGR2GRAY)
edges = cv2.Canny(gray, 100, 200)
```
*
color_image = cv2.cvtColor(cv2.imread('fatih ni.jpg'), cv2.COLOR_BGR2RGB)
cv2.imread('fatih ni.jpg'): Membaca gambar dari file dengan nama 'fatih ni.jpg'. Gambar ini dibaca dalam format BGR (Blue, Green, Red) yang merupakan format default di OpenCV.
cv2.cvtColor(..., cv2.COLOR_BGR2RGB): Mengkonversi gambar dari format BGR ke format RGB. Ini dilakukan karena banyak pustaka lain seperti matplotlib menggunakan format RGB.
gray = cv2.cvtColor(color_image, cv2.COLOR_BGR2GRAY)
cv2.cvtColor(..., cv2.COLOR_BGR2GRAY): Mengkonversi gambar RGB menjadi gambar skala abu-abu. Konversi ini dilakukan karena banyak algoritma pemrosesan gambar, termasuk deteksi tepi, bekerja lebih efektif pada gambar skala abu-abu.
edges = cv2.Canny(gray, 100, 200)
cv2.Canny(gray, 100, 200): Menerapkan algoritma deteksi tepi Canny pada gambar skala abu-abu. Algoritma ini mendeteksi tepi pada gambar. Dua parameter terakhir (100 dan 200) adalah nilai ambang batas bawah dan atas untuk deteksi tepi.
```python
cv2.imshow("Foto Fatih", edges)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
*
cv2.imshow("Foto Fatih", edges)
Menampilkan gambar hasil deteksi tepi dengan nama jendela "Foto Fatih".
cv2.waitKey(0)
Menunggu penekanan tombol pada jendela yang terbuka. Argumen 0 berarti menunggu tanpa batas waktu hingga tombol ditekan.
cv2.destroyAllWindows()
Menutup semua jendela yang dibuat oleh OpenCV.
```python
fig, axs = plt.subplots(1, 2, figsize=(10, 10))
ax = axs.ravel()

ax[0].imshow(color_image)
ax[0].set_title("Gambar Asli Berwarna")

ax[1].imshow(edges, cmap="gray")
ax[1].set_title("Gambar Setelah di Olah")
```
*
fig, axs = plt.subplots(1, 2, figsize=(10, 10))
plt.subplots(1, 2, figsize=(10, 10)) membuat satu baris dan dua kolom dari subplot dengan ukuran masing-masing 10x10 inci.
fig adalah figure object yang mengandung semua plot.
axs adalah array dari Axes objects.
ax = axs.ravel()
axs.ravel() meratakan array axs agar lebih mudah diakses dengan indeks.
ax[0].imshow(color_image)
ax[0] merujuk ke subplot pertama.
imshow(color_image) menampilkan gambar berwarna asli pada subplot pertama.
ax[0].set_title("Gambar Asli Berwarna")
set_title("Gambar Asli Berwarna") memberikan judul pada subplot pertama.
ax[1].imshow(edges, cmap="gray")
ax[1] merujuk ke subplot kedua.
imshow(edges, cmap="gray") menampilkan gambar hasil deteksi tepi dalam skala abu-abu pada subplot kedua.
ax[1].set_title("Gambar Setelah di Olah")
set_title("Gambar Setelah di Olah") memberikan judul pada subplot kedua.
```python
lines = cv2.HoughLinesP(edges, 1, np.pi/250, 20, maxLineGap = -50)
image_line = image.copy()
contours, _ = cv2.findContours(edges, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
```
*
lines = cv2.HoughLinesP(edges, 1, np.pi/250, 20, maxLineGap = -50)
cv2.HoughLinesP adalah fungsi dari OpenCV untuk melakukan deteksi garis menggunakan Transformasi Hough Probabilistik.
edges: Gambar hasil deteksi tepi yang dihasilkan oleh cv2.Canny.
1: Resolusi parameter jarak rho dalam piksel.
np.pi/250: Resolusi parameter sudut theta dalam radian.
20: Ambang batas minimum untuk voting, garis dengan jumlah voting di bawah nilai ini akan diabaikan.
maxLineGap = -50: Parameter ini seharusnya positif dan menunjukkan jarak maksimum antara dua segmen garis untuk dianggap sebagai satu garis. Nilai negatif tidak masuk akal untuk parameter ini dan akan menyebabkan kesalahan. Misalnya, gunakan nilai positif seperti 50.
image_line = image.copy()
image.copy(): Membuat salinan dari gambar asli untuk menggambar garis yang terdeteksi.
contours, _ = cv2.findContours(edges, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
cv2.findContours adalah fungsi untuk menemukan kontur pada gambar biner.
edges: Gambar hasil deteksi tepi.
cv2.RETR_TREE: Mode retrieval, yang mengembalikan semua kontur dan merekonstruksi seluruh hierarki kontur.
cv2.CHAIN_APPROX_SIMPLE: Metode approximasi kontur, yang menghapus semua titik redundan dan hanya menyimpan titik penting untuk mendeskripsikan kontur.
```python
image_line = color_image.copy()
cv2.drawContours(image_line, contours, -1, (0, 255, 0), 2)
```
*
color_image adalah gambar berwarna yang telah dibaca dan dikonversi dari format BGR ke RGB menggunakan cv2.cvtColor(image, cv2.COLOR_BGR2RGB). Salinan dari color_image disimpan dalam variabel image_line untuk mempertahankan gambar asli yang tidak berubah saat menggambar kontur.
cv2.drawContours adalah fungsi OpenCV yang digunakan untuk menggambar kontur pada gambar.
image_line: Gambar yang akan diubah dengan menggambar kontur.
contours: Daftar kontur yang akan digambar. Di sini, contours diperoleh dari hasil cv2.findContours.
-1: Indeks kontur yang akan digambar. -1 berarti semua kontur dalam daftar akan digambar.
(0, 255, 0): Warna garis yang akan digunakan untuk menggambar kontur, dalam format BGR. Di sini, (0, 255, 0) mewakili warna hijau.
2: Ketebalan garis kontur dalam piksel.
```python
fig,axs = plt.subplots(1,3,figsize = (10,10))
ax = axs.ravel()

ax[0].imshow(color_image)
ax[0].set_title("Gambar Asli Berwarna")

ax[1].imshow(edges, cmap = "gray")
ax[1].set_title("CANNY EDGE DETECTION")

ax[2].imshow(image_line)
ax[2].set_title("CONTOURS DETECTION")
```
*
Subplot Pertama: Gambar Asli Berwarna

ax[0].imshow(color_image): Menampilkan gambar berwarna asli di subplot pertama.
ax[0].set_title("Gambar Asli Berwarna"): Memberikan judul untuk subplot pertama.
Subplot Kedua: Hasil Deteksi Tepi dengan Canny

ax[1].imshow(edges, cmap='gray'): Menampilkan gambar hasil deteksi tepi dengan Canny di subplot kedua.
ax[1].set_title("CANNY EDGE DETECTION"): Memberikan judul untuk subplot kedua.
Subplot Ketiga: Hasil Deteksi Kontur

ax[2].imshow(image_line): Menampilkan gambar hasil deteksi kontur di subplot ketiga.
ax[2].set_title("CONTOURS DETECTION"): Memberikan judul untuk subplot ketiga.
