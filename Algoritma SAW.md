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
    - Kamu menghitung respon sistem terhadap beberapa skenario reduksi gangguan (rep).

Ini setara dengan pendekatan what-if analysis dalam keandalan jaringan.
