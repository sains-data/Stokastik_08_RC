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

### **Normalisasi Waktu**
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

## Ringkasan Hasil Utama



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
