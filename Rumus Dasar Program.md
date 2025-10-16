# Optimal Recloser at PLN Serpong

Rangkuman Rumus dan Dasar Logika Program Simulasi SAIDI
Program ini adalah model heuristik berbasis kriteria berbobot yang menggabungkan prinsip-prinsip dari Analisis Keputusan Multi-Kriteria (MCDA) dan konsep keandalan sistem.
1. Dasar Rumus: Analisis Keputusan Multi-Kriteria (MCDA)
   - Normalisasi (Min-Max Scaling)
     
     <img width="588" height="98" alt="Screenshot 2025-10-14 102111" src="https://github.com/user-attachments/assets/ee0133b8-7a86-404d-bb5e-5390f64842c6" />

     Menyamakan skala semua kriteria (Pelanggan, Jarak, Daya) ke rentang 0 hingga 1.

   - SAIDI Score Raw (Fungsi Bobot)

     <img width="869" height="75" alt="Screenshot 2025-10-14 101754" src="https://github.com/user-attachments/assets/555c2695-c6e8-4039-9581-111b89164627" />


     Menghitung skor prioritas murni berdasarkan bobot yang ditetapkan (W).

   - SAIDI Score Akhir (SAIDI_SCORE)
  
     <img width="830" height="102" alt="Screenshot 2025-10-14 101858" src="https://github.com/user-attachments/assets/ad04fdea-1279-4005-b673-c38f8536c7c7" />

     Mengaitkan skor prioritas dengan dampak pelanggan absolut.

2. Dasar Rumus: Simulasi Keandalan (SAIDI)
   -  Downtime Awal (Proksi Durasi)
  
      <img width="957" height="65" alt="Screenshot 2025-10-14 102732" src="https://github.com/user-attachments/assets/ca23087d-9639-49ab-beee-6a7d362475d0" />

      Menetapkan durasi padam awal berdasarkan skor prioritas.

   - Simulasi Reduksi Gangguan
  
     <img width="912" height="149" alt="image" src="https://github.com/user-attachments/assets/c73340a2-adb7-44e6-9818-303a62df36d1" />

     Mensimulasikan dampak pemasangan RC pada waktu pemulihan.
     
3. Perhitungan SAIDI Sistem (Output Akhir)
   - Total Customer-Hours

     <img width="762" height="79" alt="Screenshot 2025-10-14 104544" src="https://github.com/user-attachments/assets/3c9e5b27-0d7c-4f1a-b69b-d549ee47143a" />

     Mengukur total jam padam yang dialami oleh semua pelanggan di segmen tersebut.

   - System SAIDI (Sebelum dan Sesudah)
  
     <img width="806" height="106" alt="Screenshot 2025-10-14 104824" src="https://github.com/user-attachments/assets/16b08ff0-223e-4211-bbdc-c983ae0bd93c" />

     Menghitung rata-rata durasi padam per pelanggan di seluruh sistem (metrik keandalan utama).

   - Absolute SAIDI Reduction (Reduksi Total)

     <img width="780" height="62" alt="Screenshot 2025-10-14 105023" src="https://github.com/user-attachments/assets/f23ce476-6c9c-4020-87f4-16ec0c569aec" />

     Menghitung jumlah jam padam yang berhasil dihindari atau dikurangi oleh penempatan RC yang direkomendasikan.

4. Logika Penentuan RC
   - Ambang Batas (Threshold)
  
     <img width="922" height="72" alt="Screenshot 2025-10-14 105306" src="https://github.com/user-attachments/assets/80d58659-b3e0-450b-ad1f-0b7d70cb4fb9" />

     Menetapkan batas bawah, hanya memilih 25% lokasi paling kritis dengan potensi perbaikan tertinggi.

   - Penentuan Awal RC
  
     <img width="990" height="112" alt="Screenshot 2025-10-14 105842" src="https://github.com/user-attachments/assets/6ca34fe6-3d85-4248-a991-1bdca33ba9d1" />
  
     Menyaring Kandidat Berdasarkan Manfaat dan Kelayakan Teknis.

   - Aturan Anti-Berdekatan (Dalam Loop)
  
     <img width="1027" height="212" alt="Screenshot 2025-10-14 110336" src="https://github.com/user-attachments/assets/5ad1c088-c418-4ec4-a0d8-901a61d4d2e9" />

     Memastikan Recloser yang dipasang memiliki jarak yang cukup untuk koordinasi proteksi dan menghindari jarak recloser pada lokasi yang berdekatan.


# "Optimal placement of switching and protection devices in radial distribution networks to enhance system reliability using the AHP-PSO method"

Tujuan Utama Paper:

Paper ini bertujuan untuk menemukan lokasi yang paling optimal untuk penempatan perangkat proteksi (seperti recloser dan sectionalizer) di jaringan distribusi. Tujuannya adalah untuk meningkatkan keandalan sistem, yang diukur menggunakan indeks seperti SAIDI dan SAIFI.

1. Metode yang Digunakan
Paper ini sangat relevan karena menggunakan dua metode utama yang sangat terkait secara konseptual dengan program:
- AHP (Analytic Hierarchy Process): Ini adalah metode matematis untuk menentukan bobot (prioritas) dari berbagai kriteria. AHP digunakan untuk memutuskan kriteria mana yang paling penting untuk dioptimalkan (misalnya, SAIDI, SAIFI, atau biaya).
  - Keterkaitan dengan Program: Konsep ini sama persis dengan penggunaan bobot (WEIGHT_PELANGGAN, WEIGHT_JARAK, WEIGHT_DAYA) untuk menghasilkan SAIDI_SCORE.

- PSO (Particle Swarm Optimization): Ini adalah algoritma optimasi yang meniru perilaku kawanan burung. PSO digunakan untuk mencari solusi terbaik di antara jutaan kemungkinan lokasi perangkat. Tujuannya adalah untuk menemukan kombinasi lokasi yang menghasilkan nilai SAIDI terendah.
  - Keterkaitan dengan Program: PSO melakukan hal yang sama dengan yang dilakukan program yaitu, mencari lokasi terbaik. dan menggunakan metode heuristik berbasis aturan (persentil, hindari GI/GH, dll.)

2. Rumus dan Keterkaitan
- Paper ini akan memiliki dua jenis rumus utama yang relevan:
  - Rumus Keandalan Standar (SAIDI/SAIFI): Ini adalah rumus dasar yang di kenal, yang akan digunakan sebagai bagian dari fungsi tujuan yang ingin diminimalkan.
  - Fungsi Tujuan Berbobot (Objective Function): Ini adalah rumus yang sangat penting. Paper ini akan meminimalkan kombinasi dari SAIDI, SAIFI, dan biaya investasi.Rumus:

    <img width="833" height="132" alt="Screenshot 2025-10-14 113232" src="https://github.com/user-attachments/assets/259cf211-46e6-4a26-833d-4de10b38f69b" />

Dimana:

<img width="1282" height="81" alt="Screenshot 2025-10-14 113538" src="https://github.com/user-attachments/assets/3c6e9188-a4fc-4ab2-a721-dcb01d00f752" />

Keterkaitan dengan Program: Fungsi ini adalah landasan teoretis untuk SAIDI_SCORE. Program dapat menjelaskan bahwa SAIDI_SCORE dari Program ini adalah representasi sederhana dari fungsi tujuan berbobot ini. Program menggunakan bobot untuk kriteria operasional untuk mencari keandalan setiap recloser.

- Kesimpulan antara kaitan Jurnal dan Program
  
  jurnal "Optimal placement of switching and protection devices in radial distribution networks using the AHP-PSO method" sepenuhnya mendukung validitas program dengan memberikan landasan teoretis yang kuat untuk metodologi Analisis Keputusan Multi-Kriteria (MCDA). jurnal ini menggunakan AHP untuk menentukan bobot yang kemudian digunakan dalam Fungsi Tujuan Berbobot (Min F), sebuah konsep yang secara fundamental sama dengan penggunaan program terhadap koefisien bobot (0.6,0.2,0.2) untuk menghasilkan SAIDI Score sebagai metrik prioritas. Dengan demikian, program dapat diposisikan sebagai solusi heuristik yang disederhanakan dan praktis—yang menggabungkan aturan operasional (misalnya, skip GI/GH) dengan prinsip MCDA yang disahkan paper tersebut—untuk mencapai tujuan yang sama dengan algoritma optimasi PSO, yaitu mengarahkan investasi ke titik paling efisien guna meminimalkan dampak gangguan sistem.
