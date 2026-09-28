# InnovAI 2026 — Demo: Microsoft Copilot Studio

Progetto **Microsoft Copilot Studio** presentato alla sessione **InnovAI 2026**.

Contiene la definizione dell'agente conversazionale che guida il cittadino nella creazione di una segnalazione, recupera ticket simili dal CRM tramite un'HTTP Action e genera una risposta personalizzata via Azure OpenAI.

Il backend .NET è nel repo companion: [InnovAI2026-Demo](https://github.com/pythonyan/InnovAI2026-Demo)

---

## Come funziona

```
Cittadino → Copilot Studio (topic: NuovaSegnalazione)
                ↓
        HTTP Action → POST /api/similarity
        (custom connector con API Key)
                ↓
        Backend .NET (AI Agent + Azure OpenAI)
                ↓
        Risposta con ticket simili + invio email automatico
```

---

## Struttura del repository

```
InnovAi Demo/
├── agent.mcs.yml              Definizione e istruzioni dell'agente
├── actions/                   HTTP Action verso /api/similarity
├── connectors/                Custom connector (OpenAPI + parametri API Key)
├── topics/                    Flussi conversazionali (NuovaSegnalazione, Greeting, ...)
├── translations/              Traduzioni it-IT dei topic
├── variables/                 Variabili globali (TestoSegnalazione, CategoriaSegnalazione, Top3Tickets)
├── knowledge/                 File di conoscenza caricati nell'agente
├── settings.mcs.yml           Impostazioni agente
└── connectionreferences.mcs.yml
NuovaSegnalazione.yaml         Definizione topic principale (export)
swagger.json                   OpenAPI spec del backend
frasi.txt                      Frasi di esempio per il testing
index.html                     UI demo (client statico)
```

---

## Prerequisiti

- Accesso a **Microsoft Copilot Studio** (licenza Power Platform)
- Estensione **Copilot Studio** per VS Code
- Backend [InnovAI2026-Demo](https://github.com/pythonyan/InnovAI2026-Demo) in esecuzione e raggiungibile pubblicamente (ngrok o Dev Tunnels)

---

## Come aprire il progetto

1. Clona il repo
2. Apri la cartella `InnovAi Demo/` con l'estensione **Copilot Studio** di VS Code
3. Connettiti al tuo environment Power Platform
4. Aggiorna l'URL del custom connector con il tuo endpoint ngrok/Dev Tunnels
5. Pubblica l'agente

---

## Configurazione HTTP Action

Il connettore custom usa **API Key** per autenticarsi. Prima di pubblicare:

| Parametro | Dove configurare |
|---|---|
| URL base del connector | `connectors/.../openapidefinition.json` → `servers[0].url` |
| API Key | Impostata alla creazione della connessione in Copilot Studio |

L'API Key deve corrispondere al valore `Demo:ApiKey` configurato nel backend.

---

## Licenza

MIT — Copyright 2026 Tony Pierascenzi
