# 🌤️ Weather Image Classification using CNN

## Deskripsi Proyek
Proyek ini bertujuan untuk melakukan **klasifikasi kondisi cuaca** menggunakan **Convolutional Neural Network (CNN)**.  
Dataset yang digunakan adalah *Weather Image Dataset* dengan kategori cuaca berikut:
- Cloudy
- Foggy
- Lightning
- Rainbow
- Rainy
- Rime
- Sandstorm
- Sunrise

Model CNN dilatih menggunakan *TensorFlow* dan *Keras*, dengan pembagian dataset menjadi *train*, *validation*, dan *test set* untuk memastikan model dapat belajar dan melakukan generalisasi dengan baik.

---

## Struktur Dataset
Dataset berada di folder `WeatherData/` dengan subfolder untuk setiap kelas cuaca.  
Dataset dibagi menggunakan `ImageDataGenerator` sesuai kode:

- **Training Set:** 80% dari total gambar  
- **Validation Set:** 10% dari total gambar  
- **Test Set:** 10% dari total gambar  

Semua gambar diubah ke ukuran *150x150 piksel* sebelum dimasukkan ke dalam model.

## Arsitektur Model CNN
Model dibangun menggunakan *Sequential API* dengan susunan layer sebagai berikut:

1. `Conv2D(32, (3,3), activation='relu')`
2. `MaxPooling2D(2,2)`
3. `Conv2D(64, (3,3), activation='relu')`
4. `MaxPooling2D(2,2)`
5. `Flatten()`
6. `Dense(128, activation='relu')`
7. `Dropout(0.5)`
8. `Dense(num_classes, activation='softmax')`

- **Optimizer:** `Adam`  
- **Loss Function:** `categorical_crossentropy`  
- **Metrics:** `accuracy`

---

## Callback
Model menggunakan callback *EarlyStopping* dengan parameter:
- `monitor='val_loss'`
- `patience=5`
- `restore_best_weights=True`

Callback ini otomatis menghentikan training ketika model tidak lagi mengalami peningkatan performa, untuk mencegah overfitting.

---

## Hasil Pelatihan
Model dilatih selama maksimal 30 epoch dengan EarlyStopping aktif.  
Hasil pelatihan diharapkan menunjukkan:
- **Training Accuracy:** ~95–98%  
- **Validation Accuracy:** ~97–100%  

Visualisasi hasil pelatihan menunjukkan model stabil dan tidak overfitting.

---

## Penyimpanan Model
Model disimpan dalam beberapa format agar bisa digunakan di berbagai platform:

| Format       | File                   | Kegunaan                       |
|--------------|------------------------|--------------------------------|
| SavedModel   | `model_weather_cnn/`   | Untuk server/cloud deployment  |
| TF-Lite      | `model_weather_cnn.tflite` | Untuk aplikasi mobile (Android) |
| TFJS         | `model_tfjs/`          | Untuk aplikasi berbasis web    |
| Best Model   | `best_model.keras`     | Model terbaik untuk prediksi   |

---

## Cara Menjalankan Proyek

### Instalasi Library
Pastikan semua library terinstall:
```bash
pip install -r requirements.txt