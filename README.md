# Analisis Sistem Antrean SPBU Menggunakan Model M/M/1
**Studi Kasus: Jalur Pertalite Mobil Bertangki Kiri – SPBU Sekitar ITERA**

Repositori ini berisi analisis terkait perhitungan metrik antrian menggunakan data waktu layanan dari tiga hari observasi. Pendekatan yang digunakan adalah model antrian M/M/1 untuk melihat performa operasional berdasarkan data waktu kedatangan, waktu mulai dilayani, dan waktu selesai dilayani.

## Struktur Berkas

- **data.xlsx**  
  File data utama yang berisi tiga sheet: *day_1*, *day_2*, dan *day_3*.  
  Setiap sheet memuat kolom:
  - `No`
  - `Antrian` (waktu datang)
  - `Dilayani` (waktu mulai diproses)
  - `Selesai` (waktu layanan selesai)

- **Kode_Stokastik_08_RC.ipynb**  
  Dokumen analisis dalam bentuk R. Berisi:
  - Pembersihan dan transformasi data
  - Konversi timestamp berdasarkan tanggal observasi
  - Perhitungan metrik antrian (λ, μ, ρ, Lq, Ls, Ws, Wq)
  - Interpretasi hasil setiap hari
  - Visualisasi pendukung bila diperlukan

## Latar Belakang Singkat
Peningkatan mobilitas masyarakat di sekitar ITERA menyebabkan bertambahnya jumlah kendaraan yang mengisi bahan bakar di SPBU. Pada jalur Pertalite mobil bertangki kiri, antrean sering kali mengular terutama pada jam-jam tertentu. Analisis antrean diperlukan untuk memahami apakah kapasitas pelayanan saat ini sudah memadai atau perlu ditingkatkan. Model **M/M/1** digunakan karena sesuai dengan kondisi lapangan: *satu jalur antrean dan satu nozzle aktif*.

## Metodologi

1. **Normalisasi Waktu**

   Data waktu pada setiap sheet tidak memuat tanggal sehingga diberikan asumsi tanggal sebagai berikut:
   - *day_1*: 11 November 2025  
   - *day_2*: 12 November 2025  
   - *day_3*: 13 November 2025  

2. **Asumsi utama**
   - Kedatangan ~ Poisson
   - Pelayanan ~ Eksponensial
   - Server = 1
   - Disiplin antrean = FCFS
   - Kapasitas sistem = tak terbatas

3. **Parameter dan Ukuran kinerja Sistem Antrian**
   
   Menggunakan formula model **M/M/1** untuk menghitung:
   - Laju kedatangan pelanggan (λ)
   - Laju pelayanan (μ)
   - Utilisasi server (ρ)
   - Jumlah rata-rata pelanggan menunggu (Lq)
   - Waktu tunggu rata-rata di antrian (Wq)
   - Jumlah rata-rata pelanggan dalam sistem (Ls)
   - Waktu total dalam sistem (Ws)

4. **Model Alternatif M/M/s**
   
   Digunakan saat sistem *overload* (ρ > 1), khususnya periode siang.

5. **Interpretasi Hasil**
   
   Setiap parameter dianalisis untuk melihat beban sistem harian, efisiensi layanan, serta potensi bottleneck.

## Diagram Alir Penelitian (Flowchart)

Flowchart berikut menggambarkan tahapan analisis dari observasi hingga evaluasi hasil:

![Flowchart Penelitian](https://github.com/sains-data/Stokastik_08_RC/blob/db651ba820a4d469021c795bbe354aaef22631b7/Flowchart_Stokastik_08_RC.png)

Berikut penjelasan ringkas tahapan dalam diagram alir penelitian:

### **1. Observasi Lapangan**  
Pengamatan langsung dilakukan pada jalur pengisian Pertalite mobil untuk mencatat waktu kedatangan, mulai pelayanan, dan selesai pelayanan.

### **2. Input Data Observasi**  
Data dimasukkan ke format pengolahan seperti Excel atau R.

### **3. Validasi Data**  
Pemeriksaan dilakukan untuk memastikan data tidak mengandung duplikasi atau kesalahan.

### **4. Koreksi Data (Jika Diperlukan)**  
Jika ada ketidaksesuaian, data diperbaiki terlebih dahulu sebelum analisis dilanjutkan.

### **5. Pra-proses Data**  
Meliputi konversi waktu ke detik, perhitungan waktu antar-kedatangan, serta waktu pelayanan.

### **6. Hitung Parameter Sistem Antrean**  
Menghitung parameter dasar seperti laju kedatangan (λ) dan laju pelayanan (μ).

### **7. Uji Stabilitas Sistem (ρ)**  
Menghitung tingkat utilisasi (ρ = λ/μ) untuk menentukan apakah sistem stabil (ρ < 1) atau overload (ρ > 1).

### **8. Hitung Ukuran Kinerja Sistem**  
Jika sistem stabil, ukuran seperti Ls, Lq, Ws, dan Wq dihitung.

### **9. Evaluasi Hasil per Periode Waktu**  
Perbandingan dilakukan antara periode pagi, siang, dan sore untuk mengidentifikasi waktu paling kritis.

### **10. Apakah Diperlukan Simulasi Alternatif?**  
Jika ditemukan kondisi tidak stabil, maka digunakan model alternatif.

### **11. Perbandingan Model M/M/s**  
Evaluasi dampak penambahan server (2, 3, atau 4 server) terhadap antrean.

### **12. Hasil Akhir & Interpretasi**  
Semua temuan dianalisis dan digunakan sebagai dasar rekomendasi operasional SPBU.

### **13. Selesai**  
Proses penelitian berakhir setelah seluruh tahapan tuntas.

---

## Ringkasan Hasil Utama
1. **Periode Siang (11.00–13.00)** — *Tidak Stabil (ρ = 1.14)*
  - λ > μ → sistem overload  dan ρ > 1
  - Parameter Ls, Lq, Ws, Wq tidak valid (negatif)  
  - Antrean panjang tidak terhindarkan

2. **Periode Pagi (07.30–09.30)** — *Stabil (ρ = 0.79)*
  - Antrean terbentuk namun masih manageable
  - Waktu tunggu rata-rata ± 8 menit
  
3. **Periode Sore (16.00–18.00)** — *Sangat Stabil (ρ = 0.28)*
  - Secara teori tidak terjadi antrean
  - Namun antrean fisik tetap terlihat akibat gangguan jalur motor (blockage)
  
4. **Perbandingan Model Multi-Server**
  - **M/M/2**: Waktu tunggu turun drastis  
  - **M/M/3–4**: Peningkatan kecil, tidak sebanding dengan biaya  
  - **Rekomendasi** → Tambahkan *1 server* pada jam puncak siang hari 

## Kesimpulan
  - Model **M/M/1** efektif untuk pagi dan sore, tetapi **gagal di periode siang**.
  - Sistem terbukti **overload** pada jam 11.00–13.00 (ρ > 1).
  - Penambahan **1 server** sudah cukup untuk menstabilkan sistem.
  - Faktor eksternal seperti jalur motor perlu dipertimbangkan karena tidak tercakup dalam model klasik.

## Cara Menjalankan (Google Colab — R)

Notebook: **Kode_Stokastik_08_RC.ipynb**

1. Buka Google Colab
   
   https://colab.research.google.com/
   
2. Upload Notebook

   File → Upload Notebook → Kode_Stokastik_08_RC.ipynb

3. Aktifkan Kernel R

   Jalankan di sel pertama:

```bash
sudo apt-get install -y libssl-dev libcurl4-gnutls-dev libxml2-dev
R -e "install.packages('IRkernel'); IRkernel::installspec(user = TRUE)"

Ubah runtime: Runtime → Change runtime type → R

4. Install Paket yang Dibutuhkan

%%R
install.packages(c("tidyverse", "readxl", "lubridate"))

5. Upload Data Observasi

- Sidebar kiri: Folder → Upload → data.xlsx
- Panggil data: data <- readxl::read_excel("/content/data.xlsx")

6. Jalankan Semua Sel

## Tujuan Proyek

Repositori ini dibuat untuk membantu proses analisis performa antrian berdasarkan data riil, serta memberikan gambaran terkait efisiensi layanan harian dengan pendekatan model antrian klasik.

## 👥 Tim Penyusun

| Nama | NIM |
|------|------|
| Elok Fiola | 122450051 |
| Oktavia Nurwenda Puspita S | 122450041 |
| Feryadi Yulius | 122450087 |
| Nawwaf Abdurrahman | 122450018 |

Program Studi Sains Data — Fakultas Sains  
Institut Teknologi Sumatera (ITERA), 2025

## Lisensi

Proyek ini dirilis menggunakan lisensi bebas sesuai kebutuhan pemilik repositori.

## Kontribusi
Pull request, penambahan fitur, dan diskusi sangat dipersilakan.  
Silakan buat *issue* untuk mengusulkan ide atau perbaikan.
