Clustering Wilayah Prioritas Stunting di DKI Jakarta
 Project ini mengelompokkan wilayah di DKI Jakarta berdasarkan tingkat risiko stunting memakai K-Means (k=3). Datanya tahun 2024 dan dianalisis di tiga level: kelurahan, kecamatan, dan kota administras

Data

Ada lima file CSV di folder data/:

Kelurahan.csv: jumlah balita pendek per kelurahan (267 baris)
Kecamatan.csv: jumlah balita pendek per kecamatan (44 baris)
sanitasi.csv: persentase rumah tangga dengan akses sanitasi layak per kota
Jumlah_dan_Persentase_Penduduk_Miskin_.csv: data kemiskinan per kota
Sangat_Pendek_pada_Balita.csv: capaian balita sangat pendek tingkat provinsi 2022-2024 (tidak dipakai di notebook)

Variabel yang dipakai untuk clustering ada tiga: jumlah balita pendek, persentase sanitasi layak, dan persentase penduduk miskin (periode Maret). Data sanitasi dan kemiskinan cuma ada per kota, jadi nilainya disamakan untuk semua kelurahan dan kecamatan di kota yang sama.

Cara kerja
Load data dan samakan nama kota di semua file
Filter tahun 2024, lalu gabungkan semua variabel jadi satu dataframe per level
EDA: histogram, korelasi, dan total stunting per kota
Tentukan jumlah cluster pakai elbow method dan silhouette score, dipilih k=3
Jalankan K-Means setelah data distandarisasi (StandardScaler)
Cluster diurutkan dari rata-rata stunting tertinggi: Cluster 1 risiko tinggi, 2 sedang, 3 rendah
Visualisasi (scatter, radar, PCA) dan evaluasi model
Simpan hasil ke CSV dan gambar
Hasil

Jumlah wilayah per cluster:

Level	Tinggi	Sedang	Rendah
Kelurahan	1	187	79
Kecamatan	1	28	15

Hasil level kota (6 wilayah) ada di hasil_clustering_kota.csv.

Evaluasi:

Level	Silhouette	Davies-Bouldin	Calinski-Harabasz
Kelurahan	0.5112	0.6132	193.40
Kecamatan	0.4503	0.6651	38.17
Kota	0.4732	0.3675	11.00
Catatan dan keterbatasan
Cluster risiko tinggi isinya cuma satu wilayah di level kelurahan dan kecamatan. Dari datanya, ini kemungkinan besar Pulau Kelapa (811 balita pendek) dan Kepulauan Seribu Utara (862). Angka stunting dan kemiskinan Kepulauan Seribu (13,03%) memang jauh di atas wilayah lain, jadi dia kepisah sendiri sebagai pencilan.
Karena sanitasi dan kemiskinan nilainya sama dalam satu kota, hasil cluster banyak dipengaruhi asal kotanya.
Yang dipakai adalah jumlah balita pendek, bukan persentase, jadi wilayah dengan penduduk banyak cenderung angkanya lebih besar.
Data kemiskinan yang dipakai hanya periode Maret karena kolom September di file sumber kosong.
Clustering cuma mengelompokkan wilayah yang mirip, tidak membuktikan sanitasi atau kemiskinan penyebab stunting.
Cara menjalankan

Notebook dibuat untuk Google Colab dan membaca data dari Google Drive.

Buat folder stunting jakarta di Google Drive, lalu upload semua file CSV ke sana
Buka Clustering_Stunting_Jakarta_FINAL.ipynb di Colab
Cek bagian path file, pastikan DRIVE_FOLDER dan nama filenya sama persis dengan yang ada di Drive
Run all

Kalau mau jalan di lokal, hapus bagian drive.mount, ganti path ke folder data, lalu install:

pip install pandas numpy scikit-learn matplotlib seaborn openpyxl jupyter

Hasilnya tersimpan di folder output/: empat file CSV (hasil_clustering_kelurahan, hasil_clustering_kecamatan, hasil_clustering_kota, tabel_gabungan_3level) dan gambar visualisasi.

Library

Python, pandas, numpy, scikit-learn, matplotlib, seaborn
