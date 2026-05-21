# 🔬 Lab Report Generator

Generator otomatis **Analisis & Kesimpulan** laporan praktikum berbasis AI.  
Dibangun dengan Streamlit, Google Gemini 1.5 Flash, dan DeepSeek V3.

---

## ✨ Fitur

| Fitur | Keterangan |
|-------|-----------|
| 📊 Analisis & Pembahasan | Min. 1000 kata, paragraf naratif, dengan citasi referensi |
| ✅ Kesimpulan | 3 poin padat berisi sebab-akibat |
| 📋 Langkah Kerja | Generate otomatis dari konteks praktikum |
| ✏️ Sesuaikan Isi | Edit bagian tertentu dengan instruksi natural |
| 🔄 Regenerate | Frasa berbeda tiap generate (variasi otomatis) |
| 📥 Export DOCX | Dokumen Word terformat siap print |
| 🌐 Export HTML | File HTML bergaya laporan akademik |
| 🖼️ Analisis Foto | Baca foto data & percobaan via Gemini |
| 📄 Baca PDF Modul | Ekstrak konteks dari file modul praktikum |

---

## 🏗️ Arsitektur AI

```
Foto percobaan/data  ──►  Google Gemini 1.5 Flash  ──►  deskripsi teks
PDF modul            ──►  pdfplumber                ──►  ringkasan teks
                                                          │
                                                          ▼
                                                   DeepSeek V3
                                                          │
                                         ┌────────────────┼────────────────┐
                                         ▼                ▼                ▼
                               Analisis &         Kesimpulan      Langkah Kerja
                               Pembahasan
```

---

## 🚀 Cara Deploy ke Streamlit Cloud

### 1. Fork / Clone Repo

```bash
git clone https://github.com/username/lab-report-generator.git
cd lab-report-generator
```

### 2. Dapatkan API Keys

**Google Gemini (Gratis):**
1. Buka [aistudio.google.com](https://aistudio.google.com/app/apikey)
2. Klik **Create API key**
3. Copy API key

**DeepSeek:**
1. Daftar di [platform.deepseek.com](https://platform.deepseek.com)
2. Buka **API Keys** → **Create new secret key**
3. Copy API key

### 3. Setup Secrets (Lokal)

Edit file `.streamlit/secrets.toml`:

```toml
GOOGLE_API_KEY = "AIzaSy..."
DEEPSEEK_API_KEY = "sk-..."
```

> ⚠️ **Jangan commit `secrets.toml` ke GitHub!** File `.gitignore` sudah mengecualikannya.

### 4. Test Lokal

```bash
pip install -r requirements.txt
streamlit run app.py
```

### 5. Deploy ke Streamlit Cloud

1. Push ke GitHub:
   ```bash
   git add .
   git commit -m "init: lab report generator"
   git push origin main
   ```

2. Buka [share.streamlit.io](https://share.streamlit.io)
3. Klik **New app** → pilih repo → branch `main` → `app.py`
4. Klik **Advanced settings** → **Secrets** → paste isi `secrets.toml`
5. Klik **Deploy!**

---

## 📁 Struktur Proyek

```
lab-report-generator/
├── app.py                    # Aplikasi utama Streamlit
├── requirements.txt          # Dependensi Python
├── .streamlit/
│   └── secrets.toml          # API keys (jangan di-commit!)
├── utils/
│   ├── __init__.py
│   ├── image_processor.py    # Google Gemini image analysis
│   ├── pdf_processor.py      # PDF text extraction
│   ├── text_generator.py     # DeepSeek V3 text generation
│   └── export_handler.py     # DOCX & HTML export
└── README.md
```

---

## 🔧 Kustomisasi

### Ubah panjang minimum analisis
Di `utils/text_generator.py`, cari `min. 1000 kata` dan ubah nilainya.

### Tambah kata terlarang
Di `utils/text_generator.py`, tambahkan ke list `FORBIDDEN_WORDS` dan update `SYSTEM_PROMPT`.

### Ubah model AI
- Gemini: ganti `"gemini-1.5-flash"` di `image_processor.py` (e.g. `"gemini-2.0-flash"`)
- DeepSeek: model `"deepseek-chat"` adalah alias untuk DeepSeek-V3 terbaru

---

## 📌 Catatan Penggunaan

- **Foto hasil data** yang jelas (tabel terbaca, angka terlihat) sangat meningkatkan kualitas analisis
- **Daftar pustaka** ditulis 1 referensi per baris; citasi `[1]`, `[2]` otomatis ditambahkan ke teks
- Tiap klik **Generate** atau **Regenerate** menghasilkan frasa yang berbeda (seed acak + temperature 1.0)
- **Export DOCX** sudah berformat laporan: margin, font Times New Roman, indentasi paragraf

---

## 📄 Lisensi

MIT License — bebas digunakan dan dimodifikasi untuk keperluan akademik.
