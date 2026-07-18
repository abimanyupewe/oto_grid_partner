# **Style Requirements Specification (SRS) \- Visual & Design System**

**Project Name:** OtoGrid  
**Design Philosophy:** Modern Functional Minimalism, Trust-Centric Design.

## **1\. DESIGN PHILOSOPHY**

Aplikasi OtoGrid dirancang untuk digunakan dalam situasi darurat dan stres tinggi. Fokus utama adalah pada kejernihan, kecepatan akses, dan pengurang beban kognitif pengguna.

* **Minimalism:** Ruang kosong (whitespace) yang luas dioptimalkan untuk memusatkan perhatian pengguna pada aksi yang paling relevan.  
* **Trust & Calm:** Antarmuka harus memberikan kesan stabilitas dan profesionalisme, meredakan kecemasan pengguna melalui palet warna yang tenang dan layout yang konsisten.  
* **Accessibility:** Kontras tinggi dan ukuran elemen interaktif yang ergonomis memastikan kemudahan penggunaan di bawah berbagai kondisi cahaya dan situasi fisik pengguna.

## **2\. COLOR PALETTE**

Sistem warna dipilih untuk melambangkan keamanan dan tindakan cepat tanpa menciptakan alarm visual yang agresif.

* **Primary (Action):** \#2A9D8F (Persian Green). Melambangkan keamanan, ketenangan, dan solusi. Digunakan untuk tombol utama seperti "Pesan Bantuan" atau "Konfirmasi".  
* **Secondary (Alert):** \#E76F51 (Burnt Orange). Digunakan untuk peringatan atau status darurat. Memberikan rasa urgensi tanpa efek kecemasan berlebih yang sering muncul dari warna merah murni.  
* **Neutral (Background):** \#FFFFFF (Pure White) & \#F8F9FA (Soft Gray). Warna dasar untuk kartu konten dan latar belakang layar guna menjaga kebersihan visual.  
* **Text (Typography):** \#264653 (Charcoal). Warna teks utama yang memberikan kontras optimal dengan latar belakang, mengurangi kelelahan mata dibandingkan dengan hitam murni (\#000000).

## **3\. TYPOGRAPHY**

Menggunakan tipografi yang modern, bersih, dan sangat mudah dibaca pada berbagai ukuran layar.

* **Font Family:** Inter (Sans-serif modern).  
* **Hierarchy:**  
  * **Headline:** 24sp, Semi-bold. Digunakan untuk judul layar utama.  
  * **Sub-headline:** 18sp, Medium. Digunakan untuk detail informasi.  
  * **Body Text:** 14sp, Regular. Digunakan untuk deskripsi teks panjang.  
  * **Buttons:** 16sp, Bold. Fokus pada keterbacaan instruksi aksi.

## **4\. UI COMPONENTS SPECIFICATION**

* **Corner Radius (Soft Rounded Corners):** Gunakan 8dp untuk semua kartu (cards) dan tombol (buttons). Sudut yang halus memberikan kesan profesional, stabil, dan tidak kekanak-kanakan.  
* **Elevation (Shadows):** Gunakan soft shadow untuk kartu konten guna memberikan efek kedalaman (depth) yang elegan.  
  * Parameter: x: 0, y: 4, blur: 20, color: \#0000001A.  
* **Button Sizing:** Tinggi tombol utama minimal 56dp. Ini adalah standar untuk kemudahan interaksi satu tangan dalam situasi darurat.

## **5\. UI/UX GUIDELINES FOR HYPERLOCAL MAP**

Peta adalah elemen visual terpenting dalam OtoGrid.

* **Map Style:** Gunakan style peta "Light/Minimal". Sembunyikan semua Point of Interest (POI) yang tidak relevan (seperti detail nama toko kecil atau gedung yang tidak berelasi dengan jalan). Fokus hanya pada jalan dan rute.  
* **Marker Consistency:**  
  * **Ikon Mekanik:** Gunakan aset vektor yang skalabel (SVG). Gunakan warna Primary (\#2A9D8F) agar ikon menonjol di atas peta.  
  * **Ikon Pengguna:** Gunakan pin berwarna biru (\#457B9D) untuk identitas posisi pengguna yang jelas.

## **6\. CONSISTENCY RULE**

* **Visual Hierarchy:** Tidak boleh ada lebih dari tiga warna utama dalam satu layar.  
* **Iconography:** Gunakan set ikon dari pustaka yang konsisten (seperti Lucide atau Heroicons) dengan bobot garis yang tipis dan bersih untuk mendukung filosofi minimalis.  
* **Negative Space:** Setiap elemen UI harus memiliki padding yang cukup (minimal 16dp pada setiap sisi) agar antarmuka tidak terasa sesak.