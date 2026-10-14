# Prediksi Arah Harian IHSG — Portofolio Ilmuwan Data

**M. Syamsuddin Wisnubroto** · Institut Teknologi Sumatera (ITERA)
Sertifikasi BNSP · LSP Digital Kreatif Solusi · Skema DSS.01.00.23 Ilmuwan Data · SKKNI No. 299 Tahun 2020

## Ringkasan

**Pertanyaan:** dengan data pasar yang sudah tersedia pagi hari, bisakah kita menebak apakah IHSG akan ditutup naik hari itu?

BEI tutup pukul 16.00 WIB, sedangkan bursa Amerika buka malam harinya. Jadi setiap pagi kita sudah tahu apa yang terjadi
di pasar global semalam.

- **Data:** data nyata harian 1 Jan 2010 – 30 Sep 2026 untuk 5 variabel: IHSG, S&P 500, VIX, minyak, dan emas.
  Sumber: Yahoo Finance (kode ^JKSE, ^GSPC, ^VIX, CL=F, GC=F), harga penutupan harian.
- **Fitur:** perubahan harian (%) dari 5 variabel tersebut.
- **Target:** 1 jika IHSG pada hari bursa berikutnya naik, 0 jika tidak.
- **Model:** Logistic Regression, Decision Tree, Random Forest, dibandingkan dengan 2 tebakan sederhana (baseline).

## Hasil (data uji 28 Apr 2023 – 29 Sep 2026, 812 hari bursa)

| Model | Accuracy | F1-macro | ROC-AUC |
|---|---|---|---|
| **Logistic Regression** | **0,558** | **0,554** | **0,583** |
| Baseline: ikuti arah S&P 500 | 0,546 | 0,543 | 0,575 |
| Baseline: selalu menebak "naik" | 0,522 | 0,343 | 0,500 |

Keempat target Unit 2 tercapai (accuracy ≥ 0,55; F1 ≥ 0,55; ROC-AUC ≥ 0,58; lebih baik dari "selalu naik"), tetapi
selisihnya tipis. Faktor paling berpengaruh adalah **perubahan S&P 500 semalam**, disusul VIX. Periode uji mencakup
gejolak besar: IHSG turun 41,5% dari puncak 9.134,7 (20 Jan 2026) ke 5.342,1 (8 Jun 2026).

Ini hasil **iterasi kedua**. Iterasi pertama memakai satu variabel tambahan dan hanya mencapai 1 dari 4 target;
variabel itu dikeluarkan karena pengaruhnya hampir nol. Karena data uji yang sama dipakai dua kali, hasil ini perlu
dikonfirmasi dengan data baru setelah September 2026 (rincian di Unit 11).

## Temuan masalah data (diperbaiki di Unit 6)

| Masalah | Jumlah | Tindakan |
|---|---|---|
| Baris kosong (1 Jan 2010) | 1 | Dihapus |
| Harga minyak negatif (20 Apr 2020) | 1 | Diganti nilai hari sebelumnya |
| Hari libur BEI (IHSG disalin) | 304 | Dihapus |

## 11 unit kompetensi

| No | Kode | Unit kompetensi | Notebook |
|---|---|---|---|
| 1 | J.62DMI00.001.1 | Menentukan Objektif Bisnis | [01_objektif_bisnis](notebooks/01_objektif_bisnis.ipynb) |
| 2 | J.62DMI00.002.1 | Menentukan Tujuan Teknis Data Science | [02_tujuan_teknis](notebooks/02_tujuan_teknis.ipynb) |
| 3 | J.62DMI00.005.1 | Menelaah Data | [03_menelaah_data](notebooks/03_menelaah_data.ipynb) |
| 4 | J.62DMI00.006.1 | Memvalidasi Data | [04_memvalidasi_data](notebooks/04_memvalidasi_data.ipynb) |
| 5 | J.62DMI00.007.1 | Menentukan Objek Data | [05_objek_data](notebooks/05_objek_data.ipynb) |
| 6 | J.62DMI00.008.1 | Membersihkan Data | [06_membersihkan_data](notebooks/06_membersihkan_data.ipynb) |
| 7 | J.62DMI00.009.1 | Mengkonstruksi Data | [07_mengkonstruksi_data](notebooks/07_mengkonstruksi_data.ipynb) |
| 8 | J.62DMI00.012.1 | Membangun Skenario Model | [08_skenario_model](notebooks/08_skenario_model.ipynb) |
| 9 | J.62DMI00.013.1 | Membangun Model | [09_membangun_model](notebooks/09_membangun_model.ipynb) |
| 10 | J.62DMI00.014.1 | Mengevaluasi Hasil Pemodelan | [10_evaluasi_model](notebooks/10_evaluasi_model.ipynb) |
| 11 | J.62DMI00.015.1 | Melakukan Proses Review Pemodelan | [11_review_model](notebooks/11_review_model.ipynb) |

Versi HTML (dengan semua hasil dan grafik) ada di folder [`html_output/`](html_output/).

## Struktur folder

```
data/raw/market_data.csv    data mentah
data/processed/             data bersih, data latih & uji (dibuat oleh notebook)
notebooks/                  11 notebook, satu per unit kompetensi
html_output/                versi HTML notebook
figures/                    grafik
models/                     model terbaik & hasil evaluasi
presentation/               slide presentasi
```

## Cara menjalankan

```bash
pip install -r requirements.txt
```

Buka folder `notebooks/` di Jupyter, lalu jalankan notebook **berurutan dari 01 sampai 11**.

*Proyek ini adalah portofolio kompetensi, bukan rekomendasi investasi.*
