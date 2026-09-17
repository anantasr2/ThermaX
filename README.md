# 🔥 ThermaX — Zn-MOF Thermal Stability Predictor

> **Integrasi Ensemble Stacking dalam Machine Learning untuk Prediksi Stabilitas Termal Metal-Organic Frameworks (MOF)**

Aplikasi web berbasis **QSPR (Quantitative Structure–Property Relationship)** yang memanfaatkan model machine learning untuk memprediksi kestabilan termal Zn-based Metal-Organic Frameworks (Zn-MOF), sekaligus menghasilkan kombinasi parameter struktural optimal secara *inverse*.

**🔗 Live App:** [thermaxmof.vercel.app](https://thermaxmof.vercel.app)
**📦 Source Code:** [github.com/Tilljana/Thermax](https://github.com/Tilljana/Thermax)

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-Web%20Framework-000000?logo=flask&logoColor=white)
![Scikit--learn](https://img.shields.io/badge/scikit--learn-ML%20Model-F7931E?logo=scikitlearn&logoColor=white)
![Deployed](https://img.shields.io/badge/deployed-Vercel-black?logo=vercel)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📑 Daftar Isi

- [Latar Belakang](#-latar-belakang)
- [Fitur Utama](#-fitur-utama)
- [Deskriptor Struktural](#-deskriptor-struktural)
- [Arsitektur & Alur Sistem](#-arsitektur--alur-sistem)
- [Tech Stack](#-tech-stack)
- [Struktur Repository](#-struktur-repository)
- [Instalasi & Menjalankan Lokal](#-instalasi--menjalankan-lokal)
- [Deployment](#-deployment)
- [Roadmap](#-roadmap)
- [Lisensi](#-lisensi)

---

## 🧪 Latar Belakang

Metal-Organic Frameworks (MOF) adalah material berpori kristalin dengan luas permukaan sangat tinggi (1.000–10.000 m²/g) yang banyak dimanfaatkan dalam penyimpanan gas, separasi molekul, katalisis, dan sensor. Salah satu tantangan utama dalam pengembangan MOF — khususnya **Zn-MOF** — adalah memprediksi **stabilitas termalnya** tanpa harus melalui eksperimen laboratorium yang mahal dan memakan waktu (TGA, DSC, PXRD).

**ThermaX** hadir sebagai solusi *data-driven*: sebuah sistem prediksi berbasis **pendekatan QSPR** yang mengombinasikan beberapa model machine learning (*stacking ensemble*) untuk mempelajari hubungan antara deskriptor struktural Zn-MOF dan stabilitas termalnya, sehingga proses eksplorasi material baru dapat dipercepat secara signifikan.

---

## ✨ Fitur Utama

| Fitur | Deskripsi |
|---|---|
| 🔮 **Prediksi Stabilitas Termal** | Input 4 deskriptor struktural → output prediksi *thermal stability* (Log TS) |
| 🔁 **Inverse Prediction** | Tentukan target stabilitas termal → sistem menghasilkan kombinasi parameter struktural optimal |
| 📊 **Feature Contribution Analysis** | Visualisasi kontribusi tiap deskriptor terhadap hasil prediksi |
| 📚 **Knowledge Base** | Modul edukasi tentang MOF, Zn-MOF, stabilitas termal, dan aplikasi industrinya |
| ❓ **FAQ Interaktif** | Penjelasan ringkas metodologi QSPR & cara kerja model untuk pengguna non-teknis |

---

## 🧬 Deskriptor Struktural

Model ThermaX dibangun di atas empat deskriptor struktural utama sebagai *input features*:

| Deskriptor | Keterangan |
|---|---|
| **nZn** | Jumlah atom seng (Zn) dalam kerangka Zn-MOF — memengaruhi densitas koordinasi & kestabilan |
| **nN** | Jumlah atom nitrogen yang berperan dalam ikatan koordinasi struktur MOF |
| **Lig** | Fragmen ligan sebagai penghubung molekuler yang memengaruhi fleksibilitas & kekuatan ikatan |
| **Het** | Kontribusi interaksi atom hetero pada ligan dengan pusat logam terhadap kestabilan termal |

---

## 🏗️ Arsitektur & Alur Sistem

```
┌─────────────────┐      ┌───────────────────┐      ┌────────────────────┐
│   Input User     │ ---> │   Flask Backend     │ ---> │  Stacking Ensemble  │
│ (nZn, nN, Lig,   │      │   (app.py)          │      │  Model (.pkl)       │
│      Het)        │      │                     │      │                     │
└─────────────────┘      └───────────────────┘      └────────────────────┘
                                                              │
                                                              ▼
                                                  ┌────────────────────────┐
                                                  │ Prediksi Log(TS) +      │
                                                  │ Feature Contribution    │
                                                  └────────────────────────┘
```

Model yang telah dilatih (`trained_logreg_model.pkl`) dan scaler (`scaler.pkl`) dimuat oleh backend Flask untuk melakukan inferensi *real-time* setiap kali pengguna mengirimkan parameter melalui antarmuka web.

---

## 🛠️ Tech Stack

| Layer | Teknologi |
|---|---|
| **Backend** | Python 3.x, Flask |
| **Machine Learning** | Scikit-learn, NumPy |
| **Frontend** | HTML Templates (Jinja2), CSS |
| **Model Artifact** | `.pkl` (trained model + scaler) |
| **Deployment** | Vercel (Serverless), Procfile-based process config |

---

## 📂 Struktur Repository

```
Thermax/
├── model/
│   ├── trained_logreg_model.pkl   # Model ML terlatih
│   └── scaler.pkl                 # Scaler untuk normalisasi input
├── templates/
│   └── index.html                 # Antarmuka utama aplikasi
├── app.py                         # Entry point aplikasi Flask
├── requirements.txt                # Dependency Python
├── vercel.json                     # Konfigurasi deployment Vercel
├── Procfile                         # Konfigurasi proses server
├── .gitignore
└── .vercelignore
```

---

## 🚀 Instalasi & Menjalankan Lokal

### Prasyarat
- Python 3.8+
- pip

### Langkah-langkah

```bash
# 1. Clone repository
git clone https://github.com/Tilljana/Thermax.git
cd Thermax

# 2. (Opsional) Buat virtual environment
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Jalankan aplikasi
python app.py
```

Aplikasi akan berjalan secara default di `http://localhost:5000`.

---

## ☁️ Deployment

Project ini dikonfigurasi untuk deploy langsung ke **Vercel** sebagai aplikasi Python serverless, menggunakan `vercel.json` sebagai konfigurasi build/routing dan `Procfile` untuk mendefinisikan proses server.

```bash
npm i -g vercel
vercel
```

**Live:** [https://thermaxmof.vercel.app](https://thermaxmof.vercel.app)

---

## 🗺️ Roadmap

- [ ] Tambah validasi input & penanganan error yang lebih informatif di sisi UI
- [ ] Ekspor riwayat prediksi ke CSV/PDF
- [ ] Perluasan dataset pelatihan untuk jenis MOF selain berbasis Zn
- [ ] Dokumentasi metodologi & referensi dataset secara publik
- [ ] Unit test untuk pipeline preprocessing & inferensi model

---


## 📄 Lisensi

Didistribusikan dengan lisensi **MIT**. Lihat file `LICENSE` untuk detail lebih lanjut.

---

## 👩‍🔬 Peneliti / Pengembang

**Ananta Surya Pratama** 
Riset & pengembangan sistem prediksi berbasis QSPR dan machine learning untuk material Zn-MOF.


> 💡 *Untuk pertanyaan akademik, kolaborasi riset, atau laporan bug, silakan buka issue di repository atau hubungi melalui email di atas.*

---

<p align="center">© 2026 ThermaX — Zn-MOF Predictor | QSPR & Thermal Stability Research</p>