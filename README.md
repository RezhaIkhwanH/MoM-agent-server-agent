# Agent Notetaker MOM 📝

Agent Notetaker MOM adalah sebuah aplikasi berbasis AI yang dirancang untuk secara otomatis mengubah transkrip atau catatan rapat mentah menjadi dokumen Notulen Rapat (Minutes of Meeting - MOM) yang terstruktur dan profesional dalam bahasa Indonesia.

Proyek ini dibangun menggunakan **FastAPI**, **Langchain**, **Langserve**, dan menggunakan model dari **Groq** untuk menghasilkan ringkasan dan poin-poin rapat dengan cepat dan akurat. Proyek ini juga terintegrasi dengan **MLflow** untuk pelacakan eksperimen (experiment tracking).

## Fitur Utama ✨
- **Otomatisasi MOM**: Mengonversi transkrip mentah menjadi format MOM standar (Detail Rapat, Poin Diskusi, Keputusan, Action Items, dan Langkah Selanjutnya).
- **Bahasa Indonesia**: Dikonfigurasi secara khusus (melalui *system prompt*) untuk menghasilkan notulensi dalam bahasa Indonesia yang formal.
- **REST API**: Menyediakan endpoint API yang mudah diakses menggunakan FastAPI dan Langserve.
- **Experiment Tracking**: Terintegrasi dengan MLflow untuk melacak setiap pemanggilan (run) dan melihat hasilnya secara rapi.
- **Fast Inference**: Menggunakan Groq API (ChatGroq) untuk inferensi LLM yang sangat cepat.

## Prasyarat 🛠️
Sebelum menjalankan proyek ini, pastikan Anda telah menginstal beberapa alat berikut:
- Python 3.9+
- MLflow (berjalan di background)
- Akun dan API Key dari Groq

## Instalasi 💻

1. **Clone repositori ini:**
   `ash
   git clone https://github.com/username-anda/agent-notetaker-mom.git
   cd agent-notetaker-mom
   `

2. **Buat Virtual Environment (opsional namun disarankan):**
   `ash
   python -m venv venv
   # Untuk Windows:
   venv\Scripts\activate
   # Untuk Linux/Mac:
   source venv/bin/activate
   `

3. **Instal dependensi:**
   Pastikan Anda memiliki file equirements.txt (atau instal library secara manual):
   `ash
   pip install fastapi uvicorn langchain langchain-groq langserve pydantic python-dotenv mlflow
   `

4. **Konfigurasi Environment Variables:**
   Buat file .env di direktori utama (root) proyek Anda dan tambahkan Groq API Key Anda:
   `nv
   GROQ_API_KEY=your_groq_api_key_here
   `

## Cara Penggunaan 🚀

### 1. Menjalankan Server MLflow (Untuk Tracking)
Proyek ini mengarah ke MLflow di http://localhost:5000. Buka terminal baru dan jalankan:
`ash
mlflow server --host 127.0.0.1 --port 5000
`

### 2. Menjalankan Agent Secara Lokal (Testing Script)
Jika Anda hanya ingin mencoba agent menggunakan file teks (mom_test.txt), Anda bisa langsung menjalankan file gent.py:
`ash
python agent.py
`
*Pastikan Anda telah membuat file mom_test.txt berisi transkrip rapat di folder yang sama. Hasilnya akan disimpan di folder esult/MOM_result.txt.*

### 3. Menjalankan REST API Server
Untuk menjalankan API server FastAPI dengan Langserve, gunakan Uvicorn:
`ash
uvicorn main:app --reload
`
API akan berjalan di: http://localhost:8000

Anda bisa mengakses:
- **Health Check**: http://localhost:8000/health
- **Langserve API Endpoint**: http://localhost:8000/agent_MOM
- **Playground (UI bawaan Langserve)**: http://localhost:8000/agent_MOM/playground
- **Dokumentasi API Swagger**: http://localhost:8000/docs

## Struktur Proyek 📂

`	ext
.
├── main.py          # Entry point aplikasi FastAPI dan setup Langserve
├── agent.py         # Logika utama Langchain agent, prompt, dan integrasi Groq/MLflow
├── testClient.py    # (Opsional) Script untuk melakukan testing pemanggilan API
├── mom_test.txt     # (Opsional) File teks mentah berisi contoh transkrip rapat
├── .env             # File environment (tidak masuk ke version control)
└── README.md        # Dokumentasi ini
`

## Teknologi yang Digunakan 🔧
- [FastAPI](https://fastapi.tiangolo.com/)
- [LangChain](https://www.langchain.com/)
- [LangServe](https://python.langchain.com/docs/langserve)
- [Groq](https://groq.com/) (LLM Provider)
- [MLflow](https://mlflow.org/) (Experiment Tracking)
