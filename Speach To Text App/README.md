# Speech to Minutes App 🎤

Un'applicazione Streamlit per convertire file audio in minute di meeting professionali utilizzando Hugging Face Whisper per la trascrizione e DeepSeek R1 per la generazione intelligente delle minute.

## 🏗️ Architettura

- **📁 Input**: File audio da cartella locale o upload
- **🎵 Speech-to-Text**: OpenAI Whisper per trascrizione accurata
- **🤖 AI Processing**: DeepSeek R1 per generazione minute strutturate
- **🌐 Interface**: Streamlit per interfaccia utente intuitiva

## 🚀 Setup Ambiente

### 1. Prerequisiti

- Python 3.8 o superiore
- Git (per clonare il repository)
- Account DeepSeek con API key

### 2. Clona il Repository

```bash
git clone https://github.com/alessandro9110/Databricks-Experiments.git
cd "Databricks-Experiments/Speach To Text App"
```

### 3. Crea Ambiente Virtuale

#### Su Windows (PowerShell)

```powershell
# Crea ambiente virtuale
python -m venv venv

# Attiva ambiente virtuale
.\venv\Scripts\Activate.ps1

# Verifica attivazione
python --version
pip --version
```

#### Su macOS/Linux

```bash
# Crea ambiente virtuale
python3 -m venv venv

# Attiva ambiente virtuale
source venv/bin/activate

# Verifica attivazione
python --version
pip --version
```

### 4. Installa Dipendenze

```bash
# Aggiorna pip
pip install --upgrade pip

# Installa dipendenze base (compatibili con Python 3.14)
pip install streamlit requests python-dotenv pandas matplotlib plotly

# Installa Whisper separatamente
pip install openai-whisper

# Se ottieni errori con Python 3.14, installa solo le dipendenze base
# e usa Whisper tramite CLI (installazione separata)
```

**Nota**: Python 3.14 è molto recente e alcune dipendenze potrebbero non essere compatibili. L'app è stata ottimizzata per funzionare con le dipendenze base disponibili.

### 5. Configurazione API

1. Copia il file `.env` di esempio:
```bash
cp .env .env.local
```

2. Modifica `.env.local` con le tue credenziali:
```env
# DeepSeek API Configuration
DEEPSEEK_API_KEY=your_actual_deepseek_api_key_here
DEEPSEEK_BASE_URL=https://api.deepseek.com

# Audio Processing Configuration
MAX_AUDIO_FILE_SIZE_MB=100
SUPPORTED_AUDIO_FORMATS=mp3,wav,m4a,flac,ogg

# Whisper Model Configuration  
WHISPER_MODEL=medium
WHISPER_DEVICE=cpu

# Output Configuration
OUTPUT_FORMAT=markdown
INCLUDE_TIMESTAMPS=true
```

## 🎵 Preparazione File Audio

1. Crea la cartella audio se non esiste:
```bash
mkdir audio
```

2. Aggiungi i tuoi file audio nella cartella `audio/`:
   - **Formati supportati**: MP3, WAV, M4A, FLAC, OGG
   - **Dimensione massima**: 100MB per file
   - **Qualità consigliata**: 16kHz, mono o stereo

## 🖥️ Utilizzo

### Opzione 1: Jupyter Notebook (Tutorial)

1. Apri il notebook `speech_to_minutes_app.ipynb`
2. Esegui tutte le celle in sequenza
3. Utilizza l'interfaccia Streamlit integrata

### Opzione 2: Streamlit Standalone

1. Avvia l'applicazione Streamlit:
```bash
streamlit run streamlit_app.py
```

2. Apri il browser su `http://localhost:8501`

3. Segui i passaggi nell'interfaccia:
   - Configura le impostazioni nella sidebar
   - Seleziona o carica un file audio
   - Clicca "Avvia Elaborazione"
   - Attendi i risultati
   - Scarica le minute generate

## 📋 Funzionalità

### 🎤 Trascrizione Audio
- **Modelli Whisper**: tiny, base, small, medium, large
- **Lingue supportate**: Italiano, Inglese, Francese, Spagnolo, Tedesco
- **Output**: Trascrizione con timestamp opzionali

### 📝 Generazione Minute
- **Sommario Esecutivo**: Riassunto conciso del meeting
- **Punti Discussi**: Argomenti trattati in dettaglio
- **Azioni Definite**: Task assegnati con responsabili
- **Decisioni Prese**: Risoluzioni formali
- **Punti Aperti**: Questioni da risolvere
- **Prossimi Passi**: Follow-up necessari

### 📊 Analisi e Statistiche
- Tempo di elaborazione
- Conteggio parole
- Rapporto di compressione
- Metriche di performance

## 🔧 Troubleshooting

### Errori Comuni

**1. Errore modulo non trovato**
```bash
# Verifica che l'ambiente virtuale sia attivo
# Reinstalla le dipendenze
pip install -r requirements.txt
```

**2. Errore API DeepSeek**
```bash
# Verifica che l'API key sia corretta nel file .env
# Controlla la connessione internet
# Verifica i limiti del tuo account DeepSeek
```

**3. Errore caricamento modello Whisper**
```bash
# Prova con un modello più piccolo (tiny/base)
# Verifica lo spazio disco disponibile
# Su macOS con Apple Silicon, assicurati che PyTorch sia installato correttamente
```

**4. File audio non supportato**
```bash
# Converti il file in formato supportato usando tools come FFmpeg:
ffmpeg -i input.mp4 -vn -acodec pcm_s16le -ar 16000 output.wav
```

### Performance

**Per migliorare le prestazioni:**

1. **GPU Support** (opzionale):
```bash
# Per NVIDIA GPU
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

2. **Modelli Whisper**:
   - `tiny`: Veloce ma meno accurato
   - `base`: Buon compromesso
   - `medium`: Raccomandato per qualità
   - `large`: Massima qualità, più lento

## 📁 Struttura Progetto

```
Speach To Text App/
├── 📄 README.md
├── 📓 speech_to_minutes_app.ipynb
├── 🐍 streamlit_app.py
├── 📋 requirements.txt
├── ⚙️ .env
├── 📁 audio/               # File audio di input
├── 📁 output/              # Risultati generati
├── 📁 venv/                # Ambiente virtuale
└── 📁 temp_uploads/        # File caricati temporaneamente
```

## 🤝 Contributi

1. Fork del repository
2. Crea un branch per la tua feature (`git checkout -b feature/AmazingFeature`)
3. Commit delle modifiche (`git commit -m 'Add some AmazingFeature'`)
4. Push del branch (`git push origin feature/AmazingFeature`)
5. Apri una Pull Request

## 📄 Licenza

Questo progetto è sotto licenza MIT. Vedi `LICENSE` per maggiori dettagli.

## 🆘 Supporto

Per supporto e domande:
- Apri un Issue su GitHub
- Controlla la sezione Troubleshooting
- Verifica la documentazione API di DeepSeek

## 🔗 Link Utili

- [Hugging Face Transformers](https://huggingface.co/docs/transformers/)
- [DeepSeek API Documentation](https://api.deepseek.com/)
- [Streamlit Documentation](https://docs.streamlit.io/)

---

**Sviluppato con ❤️ per semplificare la creazione di minute di meeting**