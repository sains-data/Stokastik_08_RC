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

- **main.Rmd**  
  Dokumen analisis dalam bentuk R Markdown. Berisi:
  - Pembersihan dan transformasi data
  - Konversi timestamp berdasarkan tanggal observasi
  - Perhitungan metrik antrian (λ, μ, ρ, Lq, Wq, W, L)
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

5. **Model Alternatif M/M/s**
Digunakan saat sistem *overload* (ρ > 1), khususnya periode siang.

6. **Interpretasi Hasil**
   Setiap parameter dianalisis untuk melihat beban sistem harian, efisiensi layanan, serta potensi bottleneck.

## Ringkasan Hasil Utama
1. **Periode Siang (11.00–13.00)** — *Tidak Stabil (ρ = 1.14)*
  - λ > μ → sistem overload  
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

## Cara Menjalankan

1. Pastikan Anda memiliki R dan paket berikut:
   - `tidyverse`
   - `readxl`
   - `lubridate`
   - Paket tambahan lain yang digunakan dalam *main.Rmd* bila ada.

2. Buka file `main.Rmd` menggunakan RStudio.

3. Jalankan seluruh chunk atau lakukan knit ke HTML/PDF untuk mendapatkan laporan lengkap.

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
