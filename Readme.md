# Proyek Klasifikasi Gambar Bunga (Flowers Recognition)

## Informasi Umum
- **Nama Proyek**: Flowers Recognition  
- **Nama Peneliti**: Sion Pardosi  
- **Tanggal**: Mei 2025  

## Deskripsi Proyek
Proyek ini bertujuan membangun sistem otomatis untuk mengenali dan mengklasifikasikan lima jenis bunga—daisy, dandelion, rose, sunflower, dan tulip—menggunakan metode Convolutional Neural Network (CNN) yang dioptimasi melalui transfer learning MobileNetV2. Aplikasi ini bermanfaat untuk mempermudah identifikasi bunga dalam konteks pertanian, hortikultura, dan penelitian botani.

## Dataset
- **Sumber**: Flowers Recognition Dataset (public domain)  
- **Jumlah Gambar**: 4.242 gambar tersebar merata pada lima kelas  
- **Pembagian Dataset**:  
  - Training: 70% (~2.969 gambar)  
  - Validation: 15% (~636 gambar)  
  - Testing: 15% (~637 gambar)  

## Arsitektur Model
Model dikembangkan menggunakan transfer learning dengan MobileNetV2 (pre-trained pada ImageNet) sebagai base model, dilengkapi lapisan berikut:  
1. **Global Average Pooling 2D** untuk mereduksi dimensi fitur  
2. **Dense Layer (512 unit, ReLU)** sebagai penggabung fitur  
3. **Batch Normalization** untuk stabilisasi distribusi aktivasi  
4. **Dropout (0.5)** sebagai regularisasi  
5. **Output Layer (5 unit, Softmax)** untuk klasifikasi multi-kelas  

## Proses Training
- **Optimizer**: Adam (learning rate = 0.001)  
- **Loss Function**: Categorical Crossentropy  
- **Metrik**: Accuracy  
- **Epochs**: 20 (dengan Early Stopping jika validasi stagnan)  
- **Batch Size**: 32  
- **Augmentasi Data**: Rotasi, pergeseran width/height, shear, zoom, flip horizontal  
- **Callbacks**:  
  - ModelCheckpoint (simpan bobot terbaik)  
  - EarlyStopping (monitor validasi loss)  
  - ReduceLROnPlateau (turunkan learning rate bila diperlukan)  
  - TensorBoard (visualisasi training)  

## Hasil dan Evaluasi
- **Akurasi Training**: 96,09%  
- **Akurasi Validation**: 89,35%  
- **Akurasi Testing**: 88,97%  
- **Loss Testing**: 0,3741  

Kurva training menunjukkan konvergensi yang baik tanpa overfitting signifikan. Confusion matrix memperlihatkan kinerja stabil pada semua kelas, dengan kesalahan minor pada kelas warna serupa.

## Inferensi Model
Model disimpan dan diuji dalam tiga format:  
1. **SavedModel** (deployment server)  
2. **TensorFlow Lite** (mobile & embedded)  
3. **TensorFlow.js** (browser & aplikasi JS)  

Pengujian inferensi pada sampel acak dari data test memperlihatkan confidence tinggi pada prediksi yang benar, menegaskan keandalan model.

## Catatan Implementasi
- **Transfer Learning**: Mempercepat pelatihan dan meningkatkan akurasi dengan memanfaatkan bobot pre-trained  
- **Data Augmentation**: Menambah variasi data latih untuk mengurangi overfitting  
- **Regularisasi**: Dropout & Batch Normalization menjaga generalisasi model  
- **Adaptive Learning Rate**: ReduceLROnPlateau mencegah stuck di local minima  

## Cara Menjalankan Proyek
1. Install dependencies:

pip install -r requirements.txt


2. Jalankan notebook `Notebook.ipynb`

3. Untuk mengonversi model ke format TFJS, pastikan telah menginstal TensorFlow.js:

pip install tensorflowjs


## Struktur Direktori

submission/
│
├── saved_model/                      # Model dalam format SavedModel
├── tflite_model/                     # Model dalam format TF-Lite
│── tfjs_model/                       # Model dalam format TFJS
│
├── Notebook.ipynb                    # Proses Klasifikasi Gambar dilakukan
│
├── README.md                         # Dokumentasi proyek
│
└── requirements.txt                  # Daftar library yang dibutuhkan


## Kesimpulan
Model klasifikasi bunga yang dikembangkan menunjukkan hasil yang memuaskan dengan akurasi testing mencapai 88.97%, melebihi batas minimal yang ditentukan yaitu 85%. Penggunaan transfer learning dan teknik augmentasi data terbukti efektif dalam meningkatkan performa model. Model ini dapat digunakan untuk berbagai aplikasi seperti identifikasi bunga pada aplikasi mobile atau web.