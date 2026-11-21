# Sistem Deteksi Penyakit Tanaman Berbasis Citra Daun

 Aplikasi yang membantu petani mengenali penyakit tanaman sejak dini dari foto daun menggunakan *Convolutional Neural Network* (CNN), sehingga penanganan bisa dilakukan sebelum penyakit meluas.

Proyek ini disusun untuk memenuhi tugas mata kuliah **Rekayasa Perangkat Lunak** oleh **Kelompok 7**.

![Status](https://img.shields.io/badge/status-in%20development-yellow)
![Model](https://img.shields.io/badge/model-MobileNetV2-green)


---

## 📖 Daftar Isi

- [Latar Belakang](#-latar-belakang)
- [Fitur Utama](#-fitur-utama)
- [Calon Pengguna](#-calon-pengguna)
- [Arsitektur dan Teknologi](#-arsitektur-dan-teknologi)
- [Dataset](#-dataset)
- [Prioritas Pengembangan](#-prioritas-pengembangan)
- [Struktur Repository](#-struktur-repository)
- [Cara Menjalankan](#-cara-menjalankan)
- [Alur Kerja Tim](#-alur-kerja-tim)
- [Dokumentasi](#-dokumentasi)
- [Anggota Tim](#-anggota-tim)
- [Lisensi](#-lisensi)

---

# Latar Belakang

Penyakit tanaman seperti hawar daun, bercak daun, blas, dan layu bakteri dapat menurunkan hasil panen secara signifikan. Petani umumnya mengenali penyakit hanya dari pengamatan visual, padahal gejala awal sering mirip satu sama lain, atau mirip dengan kekurangan hara dan serangan hama. Penyuluh pertanian jumlahnya terbatas, sehingga penyakit sering terlambat dikenali dan pestisida dipilih berdasarkan perkiraan.

Masalah utama yang diselesaikan:

- Keterlambatan deteksi penyakit
- Kesalahan diagnosis akibat gejala yang mirip
- Akses terbatas ke pakar, terutama di daerah terpencil
- Penggunaan pestisida yang tidak tepat
- Tidak adanya pencatatan kejadian penyakit

Solusi: pengguna cukup memotret daun yang bergejala, lalu sistem mengklasifikasikan penyakitnya dan menampilkan hasil beserta rekomendasi penanganan dalam hitungan detik.

---

## Fitur Utama

- Ambil foto daun atau unggah dari galeri (web / seluler)
- Prediksi penyakit beserta tingkat keyakinan (*confidence score*), menampilkan 3 prediksi teratas
- Rekomendasi penanganan: tindakan budidaya, pengendalian hayati, dan pilihan pestisida
- Riwayat diagnosis per pengguna dan per lahan
- Verifikasi pakar untuk hasil dengan keyakinan rendah
- Dasbor sebaran penyakit untuk penyuluh dan dinas pertanian
- Unduh laporan diagnosis (PDF)

---

## Calon Pengguna

| Aktor | Peran dalam sistem |
| --- | --- |
| Petani / Pengguna umum | Mengunggah foto, melihat diagnosis dan rekomendasi, mengelola riwayat |
| Penyuluh | Seperti petani, ditambah memantau data wilayah binaan dan dasbor sebaran |
| Pakar | Memverifikasi hasil berkeyakinan rendah, memberi label koreksi, mengelola basis pengetahuan penyakit |
| Administrator | Mengelola akun, data master, dataset, dan versi model |

---

## Arsitektur dan Teknologi

**Alur inti sistem:**

```
Foto daun → Validasi foto → Pra-pemrosesan → Model CNN (MobileNetV2) → Prediksi + Rekomendasi → Riwayat
                                                      │
                                         keyakinan < ambang batas (mis. 70%)
                                                      ▼
                                             Antrean verifikasi pakar
```

**Teknologi** *(sesuaikan dengan yang benar-benar dipakai tim)*:

| Komponen | Teknologi |
| --- | --- |
| Model *deep learning* | MobileNetV2 (*transfer learning*) |
| Machine learning | Python, TensorFlow / Keras *(atau PyTorch)* |
| Backend / API | `TODO` (mis. FastAPI / Flask / Laravel) |
| Frontend | `TODO` (mis. React / Flutter / HTML+JS) |
| Database | `TODO` (mis. PostgreSQL / MySQL) |
| Deployment | `TODO` |

---

##  Dataset

belum

---

## Prioritas Pengembangan

Menggunakan metode **MoSCoW**:

| Prioritas | Cakupan |
| --- | --- |
| **Must** | Registrasi/login, ambil & unggah foto, validasi foto, pra-pemrosesan, klasifikasi, tampilan rekomendasi, riwayat diagnosis (FR-01, 03, 04, 05, 06, 07, 10) |
| **Should** | Profil & data lahan, verifikasi pakar, umpan balik, lokasi & waktu diagnosis, manajemen data master dan akun (FR-02, 08, 09, 11, 12, 15, 16) |
| **Could** | Dasbor sebaran, laporan PDF, penambahan dataset & pelatihan ulang, manajemen versi model (FR-13, 14, 17, 18) |

**Target kualitas (kebutuhan nonfungsional utama):**

- *F1-score* makro ≥ 85% pada data uji lapangan
- Waktu dari unggah foto sampai hasil tampil ≤ 5 detik (jaringan 4G)
- Autentikasi, HTTPS, dan kontrol akses berbasis peran
- Antarmuka sederhana berbahasa Indonesia

---

## Struktur Repository

> Sesuaikan dengan struktur folder yang sebenarnya.

```
.
├── docs/            # Dokumen analisis & perancangan (SRS, diagram, dll.)
├── data/            # Dataset (tidak di-commit)
├── ml/              # Notebook, skrip pelatihan, dan evaluasi model
├── backend/         # Kode API / server
├── frontend/        # Kode antarmuka web / seluler
├── .gitignore
└── README.md
```

---

## Cara Menjalankan

> Bagian ini diisi setelah kode tersedia. Contoh kerangka:

```bash
# 1. Clone repository
git clone https://github.com/<username>/<nama-repo>.git
cd <nama-repo>

# 2. Siapkan environment (contoh Python)
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

# 3. Jalankan aplikasi
# TODO: tambahkan perintah menjalankan backend / frontend
```

---

## Alur Kerja Tim

Agar kolaborasi rapi dan minim konflik:

1. Branch `main` hanya berisi kode yang stabil. **Jangan push langsung ke `main`.**
2. Buat branch baru untuk setiap tugas, dengan format `tipe/nama-singkat`
   Contoh: `feature/upload-foto`, `fix/validasi-gambar`, `docs/update-readme`
3. Tulis pesan commit yang jelas, mis. `feat: tambah validasi ukuran foto`
4. Buka **Pull Request** ke `main` dan minta minimal satu anggota lain untuk me-review sebelum *merge*.
5. Gunakan tab **Issues** untuk membagi tugas dan melacak progres (bisa dihubungkan ke kode FR/NFR, mis. "FR-04: Validasi foto").

---

## 📚 Dokumentasi

- [Identifikasi Masalah dan Analisis Kebutuhan Sistem](docs/) *(letakkan file dokumen di folder `docs/` lalu perbarui tautan ini)*

---

## Anggota Tim

**Kelompok 7**: Rekayasa Perangkat Lunak

| Nama | NIM |
| --- | --- |
| Rina Tisna Nurasih | 60124005 |
| Nabila Juannita Enas | 60124006 |
| Zidan Reffa Pratama | 60124026 |
| Yusufi Noviati | 60124046 |

---

## Lisensi

Proyek ini dibuat untuk keperluan akademik. Tentukan lisensi yang sesuai (mis. MIT) bila repository akan dibuka untuk umum.
