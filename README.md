# OtoGrid Partner App

Aplikasi seluler pendamping untuk mekanik independen dan bengkel UMKM dalam ekosistem **OtoGrid** (SaaS Hiperlokal On-Demand Mechanic). Aplikasi ini dirancang untuk menerima pesanan darurat dari pengendara dengan waktu respons seketika menggunakan sistem Geo-Matching berbasis lokasi.

## Fitur Utama
- **AI-Powered Triage Dashboard:** Menerima ringkasan diagnosis teknis yang dihasilkan oleh AI dari keluhan awam pelanggan, lengkap dengan rekomendasi suku cadang dan perkakas (misal: "Bawa Busi Cadangan, Kunci Pas 10").
- **Persistent Location Streamer:** Melacak dan menyiarkan koordinat mekanik secara *real-time* ke server setiap 5 detik menggunakan WebSocket, berjalan secara persisten di *background* meskipun layar redup atau aplikasi diminimalkan.
- **Aggressive Order Broadcasting:** Sistem notifikasi darurat (*First-Come-First-Serve*) yang menggunakan alarm bervolume maksimum dan *full-screen dialog* agar pesanan tidak terlewatkan saat mekanik sedang bekerja.
- **Integrated Navigation:** Akses instan untuk membuka rute ke lokasi pelanggan menggunakan Google Maps/Waze.
- **Order State Machine:** Manajemen siklus transaksi yang ketat (`SEARCHING` ➔ `ACCEPTED` ➔ `ON_THE_WAY` ➔ `ARRIVED` ➔ `WORKING` ➔ `COMPLETED`/`CANCELED`).

## Arsitektur & Teknologi
Aplikasi ini dibangun menggunakan **Flutter** dan mematuhi prinsip **Clean Architecture** (*Domain, Data, Presentation*) serta pendekatan *Feature-First Design*.

- **State Management:** Riverpod (`flutter_riverpod`)
- **Functional Programming:** `fpdart`
- **Jaringan & WebSocket:** `dio`, `web_socket_channel`
- **Background Service & Telemetri:** `flutter_background_service`
- **Audio & Notifikasi Darurat:** `audioplayers`
- **Akses Eksternal:** `url_launcher`

## Visual & UI/UX (Desain Sistem)
Mengadopsi filosofi **Modern Functional Minimalism** dengan fokus pada lingkungan kerja mekanik (kondisi stres tinggi, visibilitas di luar ruangan, tangan kotor).

- **Warna Utama:** `#2A9D8F` (*Persian Green* - Aksi Utama/Aman) & `#E76F51` (*Burnt Orange* - Peringatan/Darurat)
- **Tipografi:** *Inter* (*Sans-serif*) untuk keterbacaan tingkat tinggi dengan kontras tajam.
- **Peta (Map):** Tampilan *Light/Minimal* dengan menyembunyikan POI yang tidak relevan agar navigasi tidak penuh sesak.
- **Komponen:** *Soft rounded corners* (8dp) dengan penggunaan *negative space* yang lega dan teks ekstra besar untuk informasi kritis.

## Perizinan Khusus (Mandatory Permissions)
Karena arsitektur aplikasi yang mengandalkan fungsionalitas latar belakang, aplikasi ini membutuhkan izin lanjutan:
1. **Location (Allow all the time):** Wajib agar sistem *Geo-Matching* dan radar ETA tetap berjalan saat layar mati.
2. **Draw over other apps:** Wajib untuk menimpa layar dengan peringatan darurat pesanan baru.
3. **Ignore Battery Optimization:** Wajib agar OS Android tidak membunuh *background service* yang menangani koneksi WebSocket.

## Instalasi & Pengembangan

1. Pastikan Anda memiliki Flutter SDK terinstal di lingkungan pengembangan Anda.
2. Kloning repositori ini.
3. Unduh semua dependensi paket:
   ```bash
   flutter pub get
   ```
4. Mengingat aplikasi ini sangat bergantung pada izin khusus dan *background service*, **sangat disarankan untuk menjalankan aplikasi pada perangkat fisik (bukan emulator)**:
   ```bash
   flutter run
   ```

---
*Dokumen ini disusun berdasarkan spesifikasi Produk (PRD) dan Sistem (SRS) dari proyek OtoGrid.*
