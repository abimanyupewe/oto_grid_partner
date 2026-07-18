# **Software Requirements Specification (SRS) \- OtoGrid Partner App**

**Project Name:** OtoGrid Partner (Aplikasi Mekanik/Mitra)  
**Platform:** Mobile (Android & iOS)  
**Framework:** Flutter (Dart)  
**Paradigma Arsitektur:** Clean Architecture & Feature-First Design

## **1\. DESKRIPSI PRODUK**

OtoGrid Partner adalah alat kerja harian bagi mekanik independen dan bengkel UMKM. Aplikasi ini menuntut keandalan tingkat tinggi dalam hal layanan latar belakang (*background services*) untuk mengirim koordinat secara persisten, serta sistem notifikasi yang agresif agar mekanik tidak melewatkan pesanan masuk meskipun ponsel berada di dalam saku saat mereka bekerja.

## **2\. STANDAR ARSITEKTUR (CLEAN ARCHITECTURE)**

Berbagi fondasi struktur yang sama dengan aplikasi pelanggan (Domain, Data, Presentation) menggunakan flutter\_riverpod dan fpdart. Namun, *Data Layer* pada aplikasi mitra memiliki kompleksitas tambahan berupa *Background Isolate* atau *Service* untuk menangani transmisi lokasi terus-menerus.

## **3\. SPESIFIKASI FITUR APLIKASI (MODULES)**

### **3.1. Modul Ketersediaan (Online/Offline Toggle)**

* **Tombol Status:** Sakelar utama di beranda. Saat diaktifkan, aplikasi melakukan panggilan REST API ke backend Django untuk mengubah status is\_online \= True pada profil mekanik.  
* **Pemeliharaan Sesi:** Saat status aktif, aplikasi wajib mempertahankan koneksi jaringan agar siap menerima *broadcast* WebSocket kapan saja.

### **3.2. Modul Penerimaan Pesanan (Order Broadcasting)**

* **Alert System:** Saat ada pesanan dalam radius (ditentukan oleh PostGIS di backend), aplikasi menerima sinyal WebSocket.  
* **UI Notifikasi:** Muncul *modal bottom sheet* atau dialog layar penuh secara instan dengan nada dering kustom bervolume tinggi.  
* **AI Summary Panel:** Menampilkan hasil diagnosis AI (misal: "Bawa Busi dan Kunci 10"). Teks harus berukuran ekstra besar agar mudah dibaca sekilas.  
* **Sistem Balasan Cepat:** Tombol "Terima" atau "Abaikan" dengan respons sistem di bawah 1 detik untuk menghindari pesanan diambil mekanik lain (First-Come-First-Serve).

### **3.3. Modul Persistent Location Streamer (Telemetri)**

* **Fase Menuju Lokasi:** Saat status pesanan adalah ON\_THE\_WAY, aplikasi wajib mengambil koordinat GPS perangkat mekanik dan mengirimkannya ke endpoint WebSocket Django Channels setiap 5 detik.  
* **Resiliensi Latar Belakang:** Pengiriman koordinat tidak boleh terhenti meskipun layar diredupkan atau aplikasi diminimalkan (memerlukan konfigurasi *foreground service* di Android).

### **3.4. Modul Manajemen Pekerjaan & Navigasi**

* **Integrasi Peta Pihak Ketiga:** Menyediakan tombol "Buka Navigasi" yang memicu URL Launcher untuk membuka Google Maps atau Waze secara eksternal dengan meneruskan titik koordinat pelanggan.  
* **Status Pekerjaan:** Tombol transisi status: "Saya Telah Tiba", "Mulai Pekerjaan", "Selesai & Tagih Pembayaran".

## **4\. PERIZINAN KHUSUS & KEAMANAN**

* **Lokasi (Latar Belakang):** Wajib meminta perizinan tingkat lanjut: Allow all the time (Izinkan sepanjang waktu) di Android, agar koordinat tetap terkirim saat layar mati.  
* **Notifikasi & Alarm:** Memerlukan izin Draw over other apps (Tampil di atas aplikasi lain) dan mengabaikan optimasi baterai (*Battery Optimization Ignore*) agar notifikasi darurat selalu masuk seketika.

## **5\. DEPENDENSI PAKET (PUBSPEC.YAML)**

* **Dependensi Inti:** Sama dengan aplikasi pelanggan (riverpod, dio, fpdart, web\_socket\_channel).  
* **Dependensi Tambahan Esensial:**  
  * flutter\_background\_service (Untuk menjaga pengiriman titik GPS tetap berjalan di latar belakang).  
  * url\_launcher (Untuk mengarahkan mekanik ke Google Maps).  
  * audioplayers (Untuk memutar nada dering darurat khusus).