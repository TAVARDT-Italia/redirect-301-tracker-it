# Verificatore di Reindirizzamenti HTTP 301 e Catene di Salti

[![Verifica Reindirizzamenti](https://img.shields.io/badge/TAVARDT-Redirect%20301-5b3cf5.svg)](https://tools.tavardt.com/it/verifica-reindirizzamenti-301/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Audit di percorsi di reindirizzamento, rilevamento di loop infiniti, conservazione del PageRank e crawl budget.

Sviluppato e mantenuto dalla divisione di ingegneria di indicizzazione e standard tecnici web di **TAVARDT**.

***

## Vettori di Rischio e Impatto Operativo nei Reindirizzamenti HTTP

Catene prolungate di reindirizzamenti disperdono l autorevolezza di posizionamento, consumano il budget di scansione e rallentano i siti italiani. I percorsi circolari bloccano il browser e spingono i motori di ricerca ad abbandonare la scansione.

Il passaggio intermedio da protocollo sicuro HTTPS a connessione non protetta HTTP mina la sicurezza delle sessioni e allerta i visitatori. L ispezione continua tutela la trasmissione di segnali organici e garantisce una navigazione reattiva.

***

## Funzionalita Centrali di Audit Tecnico

* **Tracciamento Salto per Salto**: Analisi controllata di stati 301, 302, 303, 307 e 308 senza reindirizzamento automatico del client.
* **Rilevamento Tempestivo di Loop Infiniti**: Identificazione di percorsi chiusi tramite elenco delle URL gia visitate, con blocco del test e azzeramento del punteggio.
* **Validazione Stato HTTP Destinazione Finale**: Verifica del codice di risposta finale, con penalizzazione di 60 punti in caso di esito differente da 200 OK.
* **Controllo Lunghezza Catena e Link Equity**: Ritiro di 15 punti per ogni transizione eccedente 3 passaggi al fine di preservare il crawl budget.
* **Rilevamento Degradazione di Protocollo**: Segnalazione di passaggi da HTTPS a HTTP non cifrato con decurtazione di 20 punti.
* **Misurazione Latente Cumulativa**: Calcolo del tempo di risposta per singolo salto e durata globale del transito in millisecondi.
* **Indice di Efficienza del Reindirizzamento**: Punteggio da 0 a 100 che classifica il percorso in OPTIMISED, LONG CHAIN (WARNING) o FAILURE / LOOP (CRITICAL).

***

## Installazione ed Esecuzione

Richiede Python 3.8 o superiore senza dipendenze esterne.

```bash
git clone https://github.com/TAVARDT-Italia/redirect-301-tracker-it.git
cd redirect-301-tracker-it
python redirect_tracker.py https://azienda.it
```

Per produrre l output in formato JSON strutturato in pipeline automatiche:

```bash
python redirect_tracker.py https://azienda.it -j
```

***

## Domande Frequenti (FAQ Tecnico)

### 1. Come incidono le catene di reindirizzamento estese sul passaggio di autorevolezza?
Ogni passaggio intermedio disperde parte dell autorevolezza accumulata e incrementa i tempi di risposta percepiti dagli spider. Se la catena eccede la soglia canonica, i crawler possono interrompere il tracciamento prima di raggiungere il documento finale.

### 2. In che modo il verificatore intercetta i loop circolari senza rimanere bloccato?
Il sistema archivia le URL gia analizzate e ricorre a un handler dedicato che disattiva l avanzamento automatico del client. Nel momento in cui rileva una risorsa gia vista, l audit si interrompe e il punteggio viene azzerato.

### 3. Quali rischi comporta una regressione di sicurezza da HTTPS a HTTP durante la catena?
Il passaggio intermedio su protocollo HTTP disattiva i parametri di cifratura esponendo dati sensibili e cookie a intercettazione. Cio produce una perdita di conformita e genera avvisi di sicurezza nei browser moderni.

### 4. Qual e la differenza tra reindirizzamenti permanenti e temporanei per il SEO?
Le risposte 301 e 308 attestano uno spostamento definitivo convogliando stabilmente lo storico dei link sulla nuova destinazione. Al contrario, i codici 302 e 307 rappresentano stati contingenti che invitano gli indici a mantenere la risorsa originale.

### 5. Per quale ragione e cruciale accertare la risposta HTTP della pagina finale?
Un itinerario che termina con un errore 4xx o 5xx vanifica gli sforzi di migrazione e conduce alla scomparsa della pagina dagli indici. Lo strumento collauda l URL finale per certificare il ritorno positivo dello stato 200 OK.

***

## Consulenza in SEO Tecnico e Migrazione di Portali

Per architetture complesse di migrazione e allineamento agli standard W3C, consultare il team di **TAVARDT**.

***

## Collegamenti Utili

* **Portale Aziendale:** https://ag.tavardt.com/it/
* **Suite di Diagnostica:** https://tools.tavardt.com/it/
* **Contatto Tecnico:** https://ag.tavardt.com/it/contatto/

***

### Licenza
Distribuito con Licenza MIT. Consultare il file LICENSE per i dettagli completi.

***

© 2026 TAVARDT. Tutti i diritti riservati.
