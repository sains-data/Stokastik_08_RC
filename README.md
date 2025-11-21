# Analisis Waktu Antrian dengan R (M/M/1 Queueing Model)

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

## Metodologi

1. **Normalisasi Waktu**
   Data waktu pada setiap sheet tidak memuat tanggal sehingga diberikan asumsi tanggal sebagai berikut:
   - *day_1*: 11 November 2025  
   - *day_2*: 12 November 2025  
   - *day_3*: 13 November 2025  

2. **Perhitungan Metrik Antrian**
   Menggunakan formula model **M/M/1** untuk menghitung:
   - Tingkat kedatangan pelanggan (λ)
   - Tingkat pelayanan (μ)
   - Utilisasi server (ρ)
   - Jumlah rata-rata pelanggan menunggu (Lq)
   - Waktu tunggu rata-rata di antrian (Wq)
   - Waktu total dalam sistem (W)
   - Jumlah rata-rata pelanggan dalam sistem (L)

3. **Interpretasi Hasil**
   Setiap parameter dianalisis untuk melihat beban sistem harian, efisiensi layanan, serta potensi bottleneck.

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

## Lisensi

Proyek ini dirilis menggunakan lisensi bebas sesuai kebutuhan pemilik repositori.
