# Program Bahasa Python untuk Mendeteksi Marka Jalan
## Praktikum Akhir Pengolahan Citra
#### Mohamad Tanwirul Akbar
#### 202131066 
#### Pengolahan Citra A
Program ini dijalankan untuk mendeteksi warna kuning yang terdapat pada gambar. Dimana program tersebut dijalankan dengan filter garis HoughLinesP.
### Penjelasan Singkat
HoughLinesP adalah sebuah metode yang digunakan dalam pemrosesan citra untuk mendeteksi garis lurus dalam sebuah gambar. Metode ini sering digunakan dalam deteksi marka jalan pada aplikasi Computer Vision dan juga pengolahan citra.
Fungsi HoughLinesP secara khusus mengimplementasikan Transformasi Hough Probabilistik (Probabilistic Hough Transform). Transformasi Hough adalah teknik yang digunakan untuk mendeteksi garis lurus dalam citra dengan mengubahnya ke dalam domain parameter (ruang Hough). Ruang Hough sendiri terdiri dari dua parameter, yaitu sudut (theta "θ") dan jarak (rho "ρ"), yang mempresentasikan garis lurus dalam citra.
Setelah mendapatkan garis-garis yang terdeteksi, Anda dapat menggunakan informasi ini untuk menggambar atau mengambil tindakan lain terkait marka jalan. Misalnya, Anda dapat menggambarkan garis-garis ini kembali ke citra asli, atau menggunakan mereka untuk analisis lanjutan seperti pengenalan bentuk atau penghitungan parameter jalan.
Penting untuk dicatat bahwa HoughLinesP dapat memberikan hasil yang baik dalam kondisi ideal, tetapi dapat sensitif terhadap gangguan dan kekacauan dalam citra. Oleh karena itu, seringkali diperlukan pra-pemrosesan citra, seperti filterisasi atau segmentasi, untuk memperbaiki hasil deteksi garis.

## Langkah - Langkah Pengerjaan
1. Ambil foto sesuai ketentuan pada tugas yang telah ditetapkan
2. Screenshot rincian foto yang akan digunakan sebagai sumber gambar
3. Pindahkan gambar-gambar dalam 1 folder agar mudah dalam penguploadan tugas di repository GitHub
4. Mulailah membuat Pemrograman python dengan Jupyter Notebook
5. Buatlah file .ipynb pada folder yang sama dengan gambar yang ingin dilakukan deteksi
6. Sesuaikan Program dengan source code pada readme.md ini
7. Setelah program berjalan sesuai yang diinginkan, maka mulailah membuat repository baru pada akun GitHub masing-masing
8. Lalu Upload semua Source yang diperlukan untuk membuat Pendeteksi Marka jalan Berikut

Source Code
```bash
import cv2
import numpy as np
import matplotlib.pyplot as plt
import PIL
```
Lakukan Import Library yang akan digunakan untuk menjalankan program
```bash
img = cv2.imread('jalan.jpg')
```
Baca file gambar yang akan ditampilkan
```bash
cv2.imshow('gambar asli', img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
Coba untuk tampilkan gambar, dalam windows. Maka gambar akan ditampilkan dengan ukuran pixel yang besar
```bash
scale_percent = 12
width = int (img.shape[1]*scale_percent/100)
height = int (img.shape[0]*scale_percent/100)
dimen = (width,height)
```
Lakukan resize dengan skala 12% dapat dicoba berulang untuk mendapatkan ukuran pixel yang diinginkan
```bash
resize = cv2.resize(img, dimen, interpolation = cv2.INTER_AREA)
```
lakukan fungsi resize, dimana source gambar akan tersimpan pada variabel baru resize
```bash
image = cv2.cvtColor(resize, cv2.COLOR_BGR2RGB)
plt.imshow(image)
```
Mencoba untuk menampilkan rezise yang disimpan pada variabel image. Dan sebelum menampilkan gambar, lakukan filtering BGR2RGB agar warna gambar sesuai dengan warna asli.
Lalu tampilkan dengan fungsi imshow pada image.

#### Pada bagian selanjutnya terdapat deteksi garis warna kuning pada gambar dengan cara mengganti format warna ke HSV
```bash
hsv = cv2.cvtColor(resize, cv2.COLOR_BGR2HSV)
bawah_kuning = np.array([18, 75, 130])
atas_kuning = np.array([48, 255, 255])
batas = cv2.inRange(hsv, bawah_kuning, atas_kuning)
```
Penggunaan warna HSV mempermudah deteksi garis, lalu tentukan batas bawah dan batas atas warna untuk mendeteksi warna yang akan diberi tanda (mark).
```bash
lines = cv2.HoughLinesP(batas, 1, np.pi/180, 22, maxLineGap=40)
img_line = resize.copy()
for line in lines:
    x1, y1, x2, y2, = line[0]
    cv2.line(img_line, (x1,y1), (x2,y2), (0,0,255),1)
```
Lakukan fungsi HoughLinesP untuk menambahkan garis pada gambar, dan img_line menyimpan gambar asli sehingga gambar asli akan ditumpuk dengan garis deteksi
```bash
img2 = cv2.cvtColor(img_line, cv2.COLOR_BGR2RGB)
fig, axs = plt.subplots(1,2, figsize = (10,10))
ax = axs.ravel()
ax[0].imshow(image)
ax[0].set_title('Gambar asli')
ax[1].imshow(img2)
ax[1].set_title('Pasca Deteksi')
```
Tampilkan gambar asli dan setelah deteksi untuk membandingkan keduanya. maka gambar sudah berhasil dideteksi
## Source Gambar dan Rinciannya

[Gambar](https://github.com/Tanwirul0411/PA-PC_202131066_M.TanwirulAkbar_A/blob/main/Jalan.jpg)

[Bukti Rincian Gambar](https://raw.githubusercontent.com/Tanwirul0411/PA-PC_202131066_M.TanwirulAkbar_A/main/Screenshot_2023-07-04-09-26-57-895_com.miui.gallery.jpg)

#### Hasil Output
![image](https://github.com/Tanwirul0411/PA-PC_202131066_M.TanwirulAkbar_A/assets/125352733/7a396312-f19b-415a-ace8-4c3fa6e43df6)

