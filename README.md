````markdown
# COMPUTER_REASONING_CBR

Proyek ini adalah implementasi sistem **Case-Based Reasoning (CBR)** untuk menganalisis dan memprediksi putusan perkara kepailitan berdasarkan dokumen hukum dari situs Mahkamah Agung Indonesia. Sistem ini mencakup *pipeline* lengkap mulai dari pengambilan data (*scraping*), ekstraksi metadata, representasi data, *retrieval*, prediksi, hingga evaluasi performa model.

---

## Deskripsi

Proyek ini terdiri dari lima *notebook* utama:
1.  **01_scraper.ipynb**: Mengambil dokumen PDF putusan kepailitan dari situs Mahkamah Agung dan mengonversinya ke *file* teks.
2.  **02_representation.ipynb**: Mengekstrak metadata dari *file* teks dan menyimpannya dalam format CSV.
3.  **03_retrieval.ipynb**: Melakukan *retrieval* dokumen menggunakan model IndoBERT dan Logistic Regression.
4.  **04_predict.ipynb**: Memprediksi solusi putusan berdasarkan model Logistic Regression, SVM, dan IndoBERT.
5.  **05_evaluation.ipynb**: Mengevaluasi performa model *retrieval* dan prediksi, termasuk analisis kesalahan menggunakan LIME.

---

## Prasyarat

Untuk menjalankan proyek ini, pastikan Anda memiliki:
-   **Python 3.11**
-   **Jupyter Notebook** atau lingkungan pengembangan seperti VSCode
-   **Koneksi internet** untuk mengambil data dari situs Mahkamah Agung
-   **Dependensi** yang tercantum dalam `requirements.txt`

---

## Instalasi

1.  **Clone Repositori**
    ```bash
    git clone [https://github.com/muhhanif27/COMPUTER_REASONING_CBR.git](https://github.com/muhhanif27/COMPUTER_REASONING_CBR.git)
    cd COMPUTER_REASONING_CBR
    cd CBR
    ```

2.  **Buat Virtual Environment (Opsional tetapi Direkomendasikan)**
    ```bash
    python -m venv venv
    source venv/bin/activate  # Linux/Mac
    venv\Scripts\activate     # Windows
    ```

3.  **Instal Dependensi**
    Pastikan Anda berada di direktori `CBR`, lalu jalankan:
    ```bash
    pip install -r requirements.txt
    ```

    Jika *file* `requirements.txt` belum ada, Anda dapat membuatnya dengan daftar dependensi berikut:
    ```plaintext
    pdfminer.six==20250506
    requests==2.32.3
    beautifulsoup4==4.13.4
    lxml==5.4.0
    pandas==2.2.2
    numpy==2.1.3
    sentence-transformers==3.2.1
    torch==2.4.1
    tqdm==4.66.5
    scikit-learn==1.5.2
    matplotlib==3.9.2
    seaborn==0.13.2
    lime==0.2.0.1
    ```

4.  **Unduh NLTK Data**
    Jalankan Python dan unduh data NLTK yang diperlukan:
    ```python
    import nltk
    nltk.download('punkt')
    ```

---

## Struktur Direktori

```plaintext
COMPUTER_REASONING_CBR/
├── CBR/
│   ├── data/
│   │   ├── eval/
│   │   ├── processed/
│   │   ├── raw/
│   │   ├── results/
│   ├── logs/
│   ├── PDF/
│   │   ├── Kepailitan/
│   ├── 01_scraper.ipynb
│   ├── 02_representation.ipynb
│   ├── 03_retrieval.ipynb
│   ├── 04_predict.ipynb
│   ├── 05_evaluation.ipynb
│   ├── requirements.txt
````

-----

## Cara Menjalankan Pipeline End-to-End

*Pipeline* ini mencakup langkah-langkah berikut:

1.  **Scraping Data**: Mengambil dokumen PDF dan mengonversinya ke teks.
2.  **Ekstraksi Metadata**: Memproses teks untuk mengekstrak metadata seperti nomor perkara, tanggal putusan, dll.
3.  **Retrieval dan Prediksi**: Menggunakan model untuk mencari dokumen relevan dan memprediksi solusi putusan.
4.  **Evaluasi**: Menghitung metrik performa dan menganalisis kesalahan.

### Langkah-langkah Eksekusi

1.  **Jalankan 01\_scraper.ipynb**

      - Buka *notebook* di Jupyter:
        ```bash
        jupyter notebook 01_scraper.ipynb
        ```
      - Jalankan semua *cell* untuk mengunduh hingga 60 dokumen PDF kepailitan dari situs Mahkamah Agung dan menyimpan teksnya di *folder* `data/raw/`.
      - URL *default*: `https://putusan3.mahkamahagung.go.id/search.html?q=&jenis_doc=putusan&cat=35ba6ef3a483c9085cd94932ea0ada61&jd=&court=8bb6198cd9528aaac4199a1d5627bbb9&t_put=&t_reg=&t_upl=&t_pr=`
      - **Catatan**: Pastikan koneksi internet stabil. *Log* disimpan di `logs/cleaning.log`.

2.  **Jalankan 02\_representation.ipynb**

      - Eksekusi *notebook* untuk mengekstrak metadata dari *file* teks di `data/raw/` dan menyimpan hasilnya ke `data/processed/cases.csv`.
      - *Log* disimpan di `logs/metadata_extraction.log`.

3.  **Jalankan 03\_retrieval.ipynb**

      - Eksekusi *notebook* untuk melakukan *retrieval* dokumen menggunakan IndoBERT dan Logistic Regression.
      - Hasil evaluasi *retrieval* ditampilkan di *output notebook*, termasuk akurasi dan *recall*.

4.  **Jalankan 04\_predict.ipynb**

      - Eksekusi *notebook* untuk memprediksi solusi putusan menggunakan tiga model: Logistic Regression, SVM, dan IndoBERT.
      - Hasil prediksi disimpan di `data/results/logreg_predictions.csv`, `data/results/svm_predictions.csv`, dan `data/results/indobert_predictions.csv`.

5.  **Jalankan 05\_evaluation.ipynb**

      - Eksekusi *notebook* untuk mengevaluasi performa *retrieval* dan prediksi.
      - Metrik evaluasi disimpan di `data/eval/retrieval_metrics.csv` dan `data/eval/prediction_metrics.csv`.
      - Visualisasi (*confusion matrix* dan *bar chart*) dihasilkan dan disimpan di `data/eval/performance_bar_chart.png`.

### Contoh Perintah

Berikut adalah contoh perintah untuk menjalankan *notebook* secara berurutan di Jupyter Notebook:

```bash
cd COMPUTER_REASONING_CBR
cd CBR
jupyter notebook
```

  - Buka setiap *notebook* (`01_scraper.ipynb`, `02_representation.ipynb`, dll.) melalui antarmuka Jupyter.
  - Klik **Run All Cells** untuk setiap *notebook* atau jalankan *cell* satu per satu untuk memantau proses.

Atau, konversi *notebook* ke *script* Python dan jalankan melalui *terminal*:

```bash
cd COMPUTER_REASONING_CBR
cd CBR
jupyter nbconvert --to script 01_scraper.ipynb
python 01_scraper.py
```

Ulangi langkah ini untuk *notebook* lainnya.

-----

## Catatan Penting

  - **Batasan File**: *Pipeline* ini diatur untuk memproses maksimum 60 *file* PDF/teks untuk menghindari masalah panjang *path* di Windows (maksimum 260 karakter).
  - **Koneksi Internet**: Pastikan koneksi internet stabil saat menjalankan `01_scraper.ipynb`.
  - **Model IndoBERT**: Model `indobenchmark/indobert-base-p1` diunduh secara otomatis saat menjalankan `03_retrieval.ipynb` atau `04_predict.ipynb`. Jika terjadi *error*, pastikan dependensi `sentence-transformers` dan `torch` terinstal dengan benar.
  - **LIME Analysis**: Analisis kesalahan menggunakan LIME pada `05_evaluation.ipynb` mungkin memerlukan waktu lebih lama untuk teks panjang.
  - **Log File**: *Log* aktivitas disimpan di *folder* `logs/` untuk *debugging* dan pelacakan.

-----

## Contoh Output

1.  **Scraper**: *Folder* `PDF/Kepailitan/` akan berisi *file* PDF, dan `data/raw/` akan berisi *file* teks (`case_001.txt`, `case_002.txt`, dll.).
2.  **Metadata**: *File* `data/processed/cases.csv` berisi kolom seperti `case_id`, `nomor_perkara`, `ringkasan_fakta`, dll.
3.  **Retrieval**: *Output notebook* menampilkan akurasi@5 dan *recall*@10 untuk IndoBERT dan Logistic Regression.
4.  **Prediksi**: *File* CSV di `data/results/` berisi prediksi solusi dan *top-5 case ID*.
5.  **Evaluasi**: *File* CSV di `data/eval/` berisi metrik seperti akurasi, presisi, *recall*, dan F1-*score*. Gambar *confusion matrix* disimpan di `data/eval/`.

-----

## Troubleshooting

  - **Error saat scraping**: Periksa koneksi internet atau URL situs Mahkamah Agung. Pastikan situs tidak memblokir permintaan berulang.
  - **Error model IndoBERT**: Pastikan GPU tersedia untuk performa optimal atau instal `torch` versi CPU-only jika tidak ada GPU.
  - **Path too long error**: Kurangi panjang nama *file* atau pindahkan proyek ke direktori dengan *path* lebih pendek (misalnya, `C:\CBR`).
  - **LIME error**: Pastikan `lime` terinstal (`pip install lime`) dan teks *input* tidak kosong.

-----

## Kontribusi

Jika Anda ingin berkontribusi:

1.  Fork repositori ini.
2.  Buat *branch* baru (`git checkout -b feature/nama-fitur`).
3.  *Commit* perubahan (`git commit -am 'Menambahkan fitur X'`).
4.  *Push* ke *branch* (`git push origin feature/nama-fitur`).
5.  Buat Pull Request.

-----

## Lisensi

Proyek ini dilisensikan di bawah [MIT License](https://www.google.com/search?q=LICENSE).

-----

## Kontak

Untuk pertanyaan atau dukungan, hubungi:

  - Email: mhanif0203@gmail.com
  - GitHub Issues: [https://github.com/muhhanif27/COMPUTER\_REASONING\_CBR/issues](https://github.com/muhhanif27/COMPUTER_REASONING_CBR/issues)

<!-- end list -->

```
```
