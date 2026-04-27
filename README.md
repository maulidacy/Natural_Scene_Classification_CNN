# Proyek Klasifikasi Gambar Natural Scene Menggunakan CNN

## Deskripsi Project

Project ini bertujuan untuk membangun model klasifikasi gambar menggunakan Convolutional Neural Network (CNN). Model dikembangkan untuk mengenali enam kategori gambar natural scene, yaitu:

- buildings
- forest
- glacier
- mountain
- sea
- street

Dataset yang digunakan adalah **Intel Image Classification**. Dataset ini dipilih karena memiliki jumlah gambar lebih dari 1.000, memiliki lebih dari 3 kelas, dan tidak termasuk dataset yang dilarang seperti Rock Paper Scissors atau X-Ray.

## Dataset

Dataset terdiri dari **17.034 gambar** dengan pembagian sebagai berikut:

| Jenis Data | Jumlah Gambar |
|---|---:|
| Training | 14.034 |
| Testing | 3.000 |
| Total | 17.034 |

Jumlah kelas pada dataset adalah **6 kelas**, yaitu:

1. buildings
2. forest
3. glacier
4. mountain
5. sea
6. street

Data training dibagi kembali menjadi training set dan validation set menggunakan `validation_split`.

## Preprocessing dan Data Augmentation

Tahapan preprocessing yang dilakukan:

- Resize gambar ke ukuran `150x150` piksel
- Normalisasi nilai piksel ke rentang `0-1`
- Pembagian data training dan validation
- Data augmentation pada training set

Teknik augmentation yang digunakan:

- Rotation
- Zoom
- Width shift
- Height shift
- Shear
- Horizontal flip

Data augmentation hanya diterapkan pada data training untuk meningkatkan variasi data dan mengurangi risiko overfitting.

## Arsitektur Model

Model yang digunakan adalah CNN berbasis Sequential dengan beberapa layer utama:

- Conv2D
- MaxPooling2D
- BatchNormalization
- GlobalAveragePooling2D
- Dense
- Dropout
- Softmax output layer

Model CNN dipilih karena sesuai dengan karakteristik data gambar dan memenuhi kriteria utama submission, yaitu menggunakan model Sequential, Conv2D, dan Pooling Layer.

## Evaluasi Model

Model dievaluasi menggunakan test set yang tidak digunakan pada proses training.

Hasil evaluasi model:

| Metrik | Nilai |
|---|---:|
| Test Accuracy | 88.33% |

Selain accuracy, evaluasi juga dilakukan menggunakan:

- Classification report
- Confusion matrix
- Plot training dan validation accuracy
- Plot training dan validation loss
- Inference pada beberapa gambar test

Hasil evaluasi menunjukkan bahwa model telah memenuhi kriteria minimum akurasi testing di atas 85%.

## Next Steps & Industry Insight

Berdasarkan hasil evaluasi, model sudah mampu melakukan klasifikasi gambar natural scene dengan cukup baik. Namun, beberapa kelas masih memiliki performa yang sedikit lebih rendah dibanding kelas lainnya, terutama kelas `mountain` dan `glacier`.

Hal ini wajar karena kedua kelas tersebut memiliki karakteristik visual yang mirip. Gambar glacier dan mountain sering sama-sama memiliki dominasi warna putih, abu-abu, tekstur kasar, serta pola visual yang saling tumpang tindih.

Untuk pengembangan selanjutnya, performa model dapat ditingkatkan dengan beberapa pendekatan berikut:

1. **Transfer Learning**  
   Menggunakan model pretrained seperti EfficientNet, ResNet, MobileNetV2, atau InceptionV3 dapat membantu meningkatkan performa model.

2. **Fine-Tuning**  
   Beberapa layer akhir dari model pretrained dapat dilatih ulang agar fitur visual lebih sesuai dengan dataset natural scene.

3. **Peningkatan Resolusi Input**  
   Ukuran input seperti `224x224` piksel dapat membantu model menangkap detail visual yang lebih jelas.

4. **Analisis Error Lanjutan**  
   Analisis gambar yang salah diklasifikasikan dapat membantu memahami pola kesalahan model, misalnya pada gambar dengan salju, kabut, pencahayaan rendah, atau latar belakang yang mirip.

## Format Model

Model final disimpan ke dalam tiga format:

1. SavedModel
2. TensorFlow Lite
3. TensorFlow.js

Struktur output model:

```text
saved_model/
├── saved_model.pb
└── variables/

tflite/
├── model.tflite
└── label.txt

tfjs_model/
├── model.json
└── group1-shard1of1.bin