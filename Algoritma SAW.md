# Analisis Singkat Program
1. Input data gardu tiap penyulang dari Excel.
2. Lakukan normalisasi terhadap tiga kriteria utama:
   - Jumlah pelanggan (PELANGGAN)
   - Panjang jaringan (PANJAR)
   - Daya terpasang (DAYA_KVA)
3. Hitung skor total berbobot (kombinasi linear dari ketiganya).
4. Hitung SAIDI, simulasi beberapa kali (Rep0, Rep1, Rep2).
5. Klasifikasikan hasilnya dengan batasan (threshold 75% dan 50%) jadi Yes, Maybe, No.
7. Terapkan aturan “anti-berdempetan” untuk RC berurutan.
8. Hitung system SAIDI before/after.

Jadi secara konsep, program mengambil keputusan berdasarkan multi-kriteria yang ditimbang secara deterministik.

A. Metode yang Secara Langsung Relevan
- Multi-Criteria Decision Making (MCDM)
  Program kamu sudah sepenuhnya MCDM, hanya saja dalam bentuk deterministik berbobot langsung (Simple Additive Weighting / SAW).
  - Nama metode yang relevan: Simple Additive Weighting (SAW)
    - SAW memang menggunakan normalisasi + bobot + penjumlahan tertimbang untuk menghasilkan skor akhir.
    - Tepat seperti potongan program di bagian ini:

      df_feeder['SAIDI_SCORE_RAW'] = (
      WEIGHT_PELANGGAN * norm_p +
      WEIGHT_JARAK * norm_j +
      WEIGHT_DAYA * norm_d
      )
- Reliability Indices Calculation (IEEE 1366-2012 Standard)
  Langkah program menghitung SAIDI, downtime, dan reduksi RC sepenuhnya mengikuti IEEE 1366.
  - Kenapa relevan:
    1. SAIDI (System Average Interruption Duration Index) adalah indeks keandalan utama.
    2. Perhitungan sebelum dan sesudah RC kamu sudah sesuai struktur “interruption hours × customers / total customers”
    3. Program juga melakukan perbandingan before-after yang sejalan dengan metode reliability assessment.
       
- Scenario-based Reliability Simulation
  Bagian Rep0, Rep1, Rep2 dan reduksi RC 25% adalah simulasi skenario keandalan → metode ini sering disebut Scenario-Based Reliability Analysis
  - Relevansi:
    - Program menghitung respon sistem terhadap beberapa skenario reduksi gangguan (rep).
    - Ini setara dengan pendekatan what-if analysis dalam keandalan jaringan.
- Threshold-based Classification Method
  Bagian klasifikasi RC (“Yes”, “Maybe”, “No”) berdasarkan nilai persentil SAIDI_REDUCTION_RC termasuk pendekatan threshold-based decision classification.
  - Relevansi:
    - Pendekatan ini digunakan dalam reliability zoning atau decision ranking.
    - Program menggunakan nilai ambang (percentile 50% dan 75%) yang umum digunakan di analisis berbasis ranking.

# Hubungan Langsung antara Program dan SAW
Di dalam program ada tiga tahapan inti yang identik dengan struktur
SAW

<img width="746" height="225" alt="Screenshot 2025-11-06 121721" src="https://github.com/user-attachments/assets/8c413cb3-42ff-4186-9566-71d4d7d5f36b" />

1. Mengapa SAW Tepat Sebagai Induk Metode
   
   Metode SAW cocok karena:
   - Kriteria program bersifat kuantitatif dan bisa dinormalisasi (jumlah pelanggan, daya, dan panjang jarak).
   - Tujuan program adalah memilih alternatif terbaik (gardu yang layak diberi recloser).
   - Mudah dikombinasikan dengan indeks keandalan seperti SAIDI/SAIFI → ini disebut hybrid reliability–MCDM method di jurnal ketenagalistrikan.

3. Bukti dari Kode Python
   - Contoh potongan ini adalah bentuk matematis klasik dari SAW:
  
     df_feeder['SAIDI_SCORE_RAW'] = (
    WEIGHT_PELANGGAN * norm_p +
    WEIGHT_JARAK * norm_j +
    WEIGHT_DAYA * norm_d
    )
   
   - Persis dengan rumus SAW:
   <img width="460" height="147" alt="Screenshot 2025-11-06 122410" src="https://github.com/user-attachments/assets/dff851e8-c77d-4b0e-9593-91b8302b4b51" />

   dimana:
   - 𝑉𝑖 = nilai total alternatif ke-i
   - wj = bobot kriteria ke-j
   - rij = nilai normalisasi alternatif ke-i terhadap kriteria ke-j
