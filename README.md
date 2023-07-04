# Project_Uas
import cv2
import numpy as np
from matplotlib import pyplot as plt

cv2 adalah modul OpenCV (Open Source Computer Vision) yang digunakan untuk berbagai operasi pemrosesan citra, seperti konversi warna, deteksi objek, segmentasi, dan lainnya.
numpy (diimpor sebagai np) adalah modul yang menyediakan dukungan untuk array dan operasi matematika dalam Python. Ini sering digunakan dalam pemrosesan citra untuk manipulasi data piksel.
matplotlib.pyplot (diimpor sebagai plt) adalah modul yang digunakan untuk visualisasi data, termasuk grafik, plot, dan tampilan citra.


img = cv2.imread('Image/buah.jpg')

Kode img = cv2.imread('Image/buah.jpg') digunakan untuk membaca citra dengan nama file 'buah.jpg'. Fungsi cv2.imread() adalah fungsi dari modul OpenCV yang digunakan untuk membaca citra dari file.


hsv_image = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

Kode hsv_image = cv2.cvtColor(img, cv2.COLOR_BGR2HSV) digunakan untuk mengubah citra dalam format BGR (Blue-Green-Red) ke format HSV (Hue-Saturation-Value).


kelengkeng_lower = np.array([10, 100, 100], np.uint8)
kelengkeng_upper = np.array([15, 200, 255], np.uint8)
pir_lower = np.array([26, 50, 70], np.uint8)
pir_upper = np.array([100, 255, 255], np.uint8)
salak_lower = np.array([0, 34, 5], np.uint8)
salak_upper = np.array([3, 200, 100], np.uint8)

Dalam kode terdapat nilai "lower" dan "upper" untuk deteksi buah kelengkeng, pir, dan salak dalam ruang warna HSV. Berikut adalah penjelasan dari pembagian program

Untuk deteksi buah kelengkeng:
kelengkeng_lower = np.array([10, 100, 100], np.uint8) menentukan nilai "lower" untuk komponen Hue (H) sebesar 10, Saturation (S) sebesar 100, dan Value (V) sebesar 100.
kelengkeng_upper = np.array([15, 200, 255], np.uint8) menentukan nilai "upper" untuk komponen Hue (H) sebesar 15, Saturation (S) sebesar 200, dan Value (V) sebesar 255.

Untuk deteksi buah pir:
pir_lower = np.array([26, 50, 70], np.uint8) menentukan nilai "lower" untuk komponen Hue (H) sebesar 26, Saturation (S) sebesar 50, dan Value (V) sebesar 70.
pir_upper = np.array([100, 255, 255], np.uint8) menentukan nilai "upper" untuk komponen Hue (H) sebesar 100, Saturation (S) sebesar 255, dan Value (V) sebesar 255.

Untuk deteksi buah salak:
salak_lower = np.array([0, 34, 5], np.uint8) menentukan nilai "lower" untuk komponen Hue (H) sebesar 0, Saturation (S) sebesar 34, dan Value (V) sebesar 5.
salak_upper = np.array([3, 200, 100], np.uint8) menentukan nilai "upper" untuk komponen Hue (H) sebesar 3, Saturation (S) sebesar 200, dan Value (V) sebesar 100.


kernel = np.ones((20,10), np.uint8)
dilated_kelengkeng_mask = cv2.dilate(kelengkeng_mask, kernel, iterations=1)
kernel = np.ones((20,10), np.uint8)
dilated_pir_mask = cv2.dilate(pir_mask, kernel, iterations=1)
kernel = np.ones((20,10), np.uint8)
dilated_salak_mask = cv2.dilate(salak_mask, kernel, iterations=1)


Pertama, membuat sebuah kernel dengan ukuran (20,10) menggunakan np.ones((20,10), np.uint8). Kernel ini berfungsi sebagai elemen struktur yang akan digunakan dalam operasi dilasi.
Selanjutnya, melakukan operasi dilasi pada mask buah kelengkeng menggunakan cv2.dilate(kelengkeng_mask, kernel, iterations=1). kelengkeng_mask adalah mask atau citra biner yang diperoleh dari deteksi buah kelengkeng sebelumnya. Operasi dilasi dilakukan dengan menggunakan kernel yang telah dibuat sebelumnya dan dilakukan satu iterasi.
Anda juga melakukan operasi dilasi pada mask buah pir dan salak menggunakan langkah yang sama. pir_mask dan salak_mask adalah mask atau citra biner yang diperoleh dari deteksi buah pir dan salak.


kelengkeng = cv2.bitwise_and(img, img, mask=dilated_kelengkeng_mask)
pir = cv2.bitwise_and(img, img, mask=dilated_pir_mask)
salak = cv2.bitwise_and(img, img, mask=dilated_salak_mask)

kelengkeng = cv2.bitwise_and(img, img, mask=dilated_kelengkeng_mask): Kode ini melakukan operasi bitwise AND antara citra asli (img) dan mask buah kelengkeng yang telah melalui proses dilasi (dilated_kelengkeng_mask). Operasi ini menghasilkan citra baru (kelengkeng) di mana piksel yang ada di dalam area buah kelengkeng pada mask akan diambil dari citra asli, sedangkan piksel di luar area tersebut akan dijadikan hitam (0).
pir = cv2.bitwise_and(img, img, mask=dilated_pir_mask): Kode ini melakukan operasi bitwise AND antara citra asli (img) dan mask buah pir yang telah melalui proses dilasi (dilated_pir_mask). Operasi ini menghasilkan citra baru (pir) di mana piksel yang ada di dalam area buah pir pada mask akan diambil dari citra asli, sedangkan piksel di luar area tersebut akan dijadikan hitam (0).
salak = cv2.bitwise_and(img, img, mask=dilated_salak_mask): Kode ini melakukan operasi bitwise AND antara citra asli (img) dan mask buah salak yang telah melalui proses dilasi (dilated_salak_mask). Operasi ini menghasilkan citra baru (salak) di mana piksel yang ada di dalam area buah salak pada mask akan diambil dari citra asli, sedangkan piksel di luar area tersebut akan dijadikan hitam (0).


fig, axs = plt.subplots(1,4,figsize=(8,5))

axs[0].imshow(img)
axs[0].set_title("gambar asli")
axs[1].imshow(kelengkeng)
axs[1].set_title("kelengkeng")
axs[2].imshow(pir)
axs[2].set_title("pir")
axs[3].imshow(salak)
axs[3].set_title("salak")
plt.show()

fig, axs = plt.subplots(1,4,figsize=(8,5)): Kode ini membuat plot dengan satu baris dan empat kolom, sehingga menghasilkan empat subplot secara horizontal. Ukuran figur ditentukan sebagai (8, 5), yang mengatur lebar dan tinggi dari plot keseluruhan.
axs[0].imshow(img): Kode ini menampilkan citra asli (img) pada subplot pertama (axs[0]) menggunakan fungsi imshow() dari modul matplotlib. imshow() digunakan untuk menampilkan citra dalam plot.
axs[0].set_title("gambar asli"): Kode ini mengatur judul subplot pertama menjadi "gambar asli" menggunakan set_title(). Judul ini akan ditampilkan di atas subplot.
axs[1].imshow(kelengkeng): Kode ini menampilkan citra buah kelengkeng (kelengkeng) pada subplot kedua (axs[1]).
axs[1].set_title("kelengkeng"): Kode ini mengatur judul subplot kedua menjadi "kelengkeng".
axs[2].imshow(pir): Kode ini menampilkan citra buah pir (pir) pada subplot ketiga (axs[2]).
axs[2].set_title("pir"): Kode ini mengatur judul subplot ketiga menjadi "pir".
axs[3].imshow(salak): Kode ini menampilkan citra buah salak (salak) pada subplot keempat (axs[3]).
axs[3].set_title("salak"): Kode ini mengatur judul subplot keempat menjadi "salak".
plt.show(): Kode ini digunakan untuk menampilkan plot secara keseluruhan.
