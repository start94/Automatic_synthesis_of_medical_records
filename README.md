# 🏥 Automatic_synthesis_of_medical_records



Questo progetto costruisce un sistema **automatico e scalabile** per la **sintesi di cartelle cliniche** ospedaliere, partendo da un file JSON remoto. Utilizza il modello **BART (facebook/bart-large-cnn)** di HuggingFace per generare riassunti NLP leggibili e informativi per ogni paziente.

---

## 🔍 Obiettivo

✅ Leggere cartelle cliniche da un file JSON via URL  
✅ Generare un riassunto automatico per ciascun paziente usando BART  
✅ Salvare i risultati in `clinical_summaries.json`  
✅ Stampare i riassunti e statistiche finali (ricoveri, lunghezze medie, modello, device, ecc.)

---

## 🧠 Tecnologie Utilizzate

| Libreria | Descrizione |
|----------|-------------|
| `transformers` | Caricamento e uso del modello BART |
| `torch` | Gestione device (GPU/CPU) e tensori |
| `datetime` | Timestamp dei riassunti |
| `warnings` | Gestione warning non critici |
| `json` | Parsing dei dati clinici e salvataggio risultati |

---

## ⚙️ Come Funziona

### 1. Caricamento del modello NLP

```python
from transformers import BartTokenizer, BartForConditionalGeneration
tokenizer = BartTokenizer.from_pretrained("facebook/bart-large-cnn")
model = BartForConditionalGeneration.from_pretrained("facebook/bart-large-cnn")
Il modello viene automaticamente caricato su GPU se disponibile (cuda).

2. Caricamento dati clinici

def load_clinical_data(url: str):
    ...
Vengono scaricate cartelle cliniche da un file JSON remoto. In caso di errore, viene mostrato un messaggio e inizializzata una lista vuota.

3. Preparazione testo clinico

def prepare_clinical_text(patient_data):
    ...
Unisce nome, ricoveri, diagnosi, anamnesi, farmaci e prognosi in un testo coerente da fornire al modello.

4. Generazione riassunto

def generate_summary(text, max_length=150, min_length=50):
    ...
Tokenizza il testo, genera il riassunto con beam search (num_beams=4) e lo decodifica in linguaggio naturale.

5. Salvataggio dei risultati

with open('clinical_summaries.json', 'w') as f:
    ...
Il file include:

Data di generazione

Modello usato

Numero pazienti

Riassunti completi

📊 Esempio Output
yaml

Patient 1
 Original text length: 515 characters
 Total hospitalizations: 2
 Summary: Diagnosis: Pneumonia. Medications: Captopril, Prednisone...
Statistiche Finali:
👥 Pazienti processati: 10

🏥 Ricoveri totali: 21

📏 Lunghezza media testo originale: 564 caratteri

🤖 Modello NLP: facebook/bart-large-cnn

💻 Device: GPU (cuda)

🔗 Dati di Input
URL JSON (cartelle cliniche):
hospital_records.json

✅ Caratteristiche del Sistema
Riproducibile: dati esterni via URL

Scalabile: adatto a migliaia di pazienti

Realistico: simula una reale applicazione ospedaliera

Estensibile: facilmente adattabile ad altri modelli o lingue

📌 Esempio di Avvio Rapido
bash

pip install torch transformers
python clinical_summarizer.py
Assicurati di avere Python ≥ 3.7 e una connessione a Internet per scaricare modello e dati.

📄 Licenza
Questo progetto è distribuito con licenza. Libero utilizzo a fini educativi e di ricerca.

✍️ Autore
Raffaele Diomaiuto · AI Developer Junior 
