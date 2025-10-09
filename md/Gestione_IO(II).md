# Gestione I/O (II)

## 🔹 Introduzione

La seconda parte della gestione dell’I/O approfondisce **le strategie di ottimizzazione e di affidabilità** nella gestione dei dispositivi di massa, in particolare i **dischi** (magnetici e SSD).
Qui il sistema operativo non si limita più a coordinare le operazioni di lettura e scrittura, ma deve anche:

* **ordinare e schedulare le richieste di I/O** per ridurre i tempi di accesso al disco;
* **distribuire e replicare i dati** per aumentare l’affidabilità (RAID);
* **adattarsi alla diversa natura fisica** dei dispositivi (HDD vs SSD);
* **gestire i dispositivi in ambiente Linux**, attraverso il sottosistema dei **block device**.

---

## 🔹 1. Struttura fisica e tempi di accesso al disco

Un **disco magnetico (HDD)** è composto da piatti rotanti rivestiti di materiale magnetico, divisi in **tracce** e **settori**.
Il **braccio di lettura/scrittura** si sposta tra le tracce, e i dati vengono letti quando il settore desiderato passa sotto la testina.

### Tempi di accesso

Il tempo totale per soddisfare una richiesta di lettura/scrittura si compone di tre elementi:

1. **Seek time (T_seek):** tempo necessario per spostare la testina sulla traccia corretta.
   → di solito tra 3 e 10 ms.

2. **Rotational latency (T_rot):** tempo di attesa finché il settore desiderato passa sotto la testina.
   → dipende dalla velocità di rotazione del disco (es. 7200 rpm ≈ 4,2 ms in media).

3. **Transfer time (T_trans):** tempo necessario per leggere o scrivere i dati del settore.
   → molto più breve (pochi μs).

[
T_{accesso} = T_{seek} + T_{rot} + T_{trans}
]

Poiché i primi due contributi sono dominanti, **minimizzare gli spostamenti della testina** è l’obiettivo principale degli algoritmi di **disk scheduling**.

---

## 🔹 2. Scheduling dei dischi

Il **disk scheduler** ordina le richieste di I/O pendenti in modo da ridurre i movimenti della testina e migliorare il throughput.
Ogni algoritmo adotta un criterio diverso per decidere **quale richiesta servire per prima**.

### a) FCFS – *First Come, First Served*

Le richieste vengono servite nell’ordine di arrivo.
→ Semplice ma inefficiente: la testina può muoversi continuamente avanti e indietro.

**Vantaggio:** equità.
**Svantaggio:** tempi medi di accesso elevati.

---

### b) SSTF – *Shortest Seek Time First*

Viene servita la richiesta **più vicina alla posizione corrente** della testina.
→ Riduce i tempi medi di spostamento.

**Problema:** può causare **starvation** per richieste lontane se continuano ad arrivare richieste vicine.

---

### c) SCAN (Elevator Algorithm)

La testina si muove in una direzione servendo tutte le richieste fino al bordo del disco, poi inverte la direzione e serve le richieste nell’altro senso.

**Analogia:** come un ascensore che sale e scende servendo i piani nell’ordine.

**Vantaggi:**

* Tempi medi più stabili.
* Nessuna starvation sistematica.

**Svantaggi:**

* Le richieste alle estremità del disco attendono più a lungo.

---

### d) C-SCAN – *Circular SCAN*

Variante di SCAN: la testina serve solo in una direzione (es. da inizio a fine disco) e poi **torna rapidamente all’inizio senza servire richieste nel ritorno**.
→ Garantisce tempi di attesa più uniformi.

---

### e) LOOK e C-LOOK

Sono varianti ottimizzate di SCAN e C-SCAN:

* La testina **non si spinge fino ai bordi del disco**, ma si ferma all’ultima richiesta nella direzione corrente.
* Riduce ulteriormente i movimenti inutili.

---

### f) Confronto generale

| Algoritmo         | Tipo            | Vantaggi                  | Svantaggi                     |
| ----------------- | --------------- | ------------------------- | ----------------------------- |
| **FCFS**          | Non ottimizzato | Semplice, equo            | Movimenti elevati             |
| **SSTF**          | Ottimizzato     | Buon compromesso          | Possibile starvation          |
| **SCAN**          | Bidirezionale   | Buon throughput           | Latenza ai bordi              |
| **C-SCAN**        | Circolare       | Tempi uniformi            | Ritorno a vuoto               |
| **LOOK / C-LOOK** | Ottimizzati     | Evitano movimenti inutili | Più complessi da implementare |

Nei sistemi moderni, vengono spesso utilizzati **scheduler ibridi**, che combinano logiche simili a SSTF e C-LOOK con priorità dinamiche e bilanciamento della latenza.

---

## 🔹 3. RAID – Redundant Array of Independent Disks

Il **RAID** è una tecnica che combina più dischi fisici in un unico insieme logico, con l’obiettivo di migliorare **prestazioni**, **affidabilità** o **entrambe**.

### Motivazioni

* **Prestazioni:** letture/scritture parallele su più dischi.
* **Affidabilità:** ridondanza dei dati → tolleranza ai guasti.
* **Capacità logica:** unione di più dischi in un volume unico.

---

### Livelli principali

| Livello           | Descrizione                                                    | Vantaggi                                 | Svantaggi                          |
| ----------------- | -------------------------------------------------------------- | ---------------------------------------- | ---------------------------------- |
| **RAID 0**        | *Striping* → suddivide i dati tra i dischi senza ridondanza    | Massime prestazioni                      | Nessuna tolleranza ai guasti       |
| **RAID 1**        | *Mirroring* → copia identica su due dischi                     | Alta affidabilità                        | Capacità dimezzata                 |
| **RAID 5**        | *Striping con parità distribuita* → parità su dischi alternati | Buon equilibrio prestazioni/affidabilità | Penalità in scrittura              |
| **RAID 6**        | Come RAID 5 ma con doppia parità                               | Resiste a 2 guasti simultanei            | Maggiore overhead                  |
| **RAID 10 (1+0)** | Mirroring + striping                                           | Ottimo bilanciamento                     | Costo elevato (richiede ≥4 dischi) |

### Considerazioni

* RAID 0 → performance pura (es. cache temporanee).
* RAID 1 → sistemi critici (database, server).
* RAID 5/6 → file server e NAS.
* RAID 10 → ambienti enterprise ad alte prestazioni.

---

## 🔹 4. HDD vs SSD

Negli ultimi anni, gli **SSD (Solid State Drive)** hanno sostituito in gran parte i dischi magnetici tradizionali, ma la loro gestione a livello di sistema operativo differisce notevolmente.

### HDD (Hard Disk Drive)

* Accesso meccanico (testina + piatti).
* Tempi dominati da seek e rotazione.
* Prestazioni influenzate dalla posizione fisica dei dati.
* Usura trascurabile ma sensibile agli urti.

### SSD (Solid State Drive)

* Nessuna parte meccanica → accesso **completamente elettronico**.
* Tempi di accesso costanti (nessun seek time).
* Prestazioni molto superiori in lettura casuale.
* Numero limitato di cicli di scrittura (usura celle).

### Implicazioni per il sistema operativo

* Gli algoritmi di **disk scheduling** diventano meno rilevanti (nessun movimento testina).
* I driver devono gestire **wear leveling**, **garbage collection** e **comandi TRIM** per mantenere prestazioni costanti.
* Le operazioni di I/O vengono spesso accodate in modo asincrono per massimizzare la concorrenza.

---

## 🔹 5. Gestione I/O in Linux

Linux gestisce l’I/O attraverso una struttura modulare basata su **device file** e **driver a due categorie principali**:

| Tipo                  | Descrizione                                   | Esempi                   |
| --------------------- | --------------------------------------------- | ------------------------ |
| **Character devices** | Scambio dati byte per byte, flusso continuo   | Terminali, porte seriali |
| **Block devices**     | Accesso a blocchi di dati di dimensione fissa | Dischi, SSD, memorie USB |

Ogni dispositivo è rappresentato da un **file speciale** in `/dev`, identificato da due numeri:

* **Major number:** identifica il driver associato.
* **Minor number:** identifica l’istanza specifica del dispositivo.

### Sottosistema del block I/O

Ogni richiesta di I/O passa attraverso:

1. **Page cache / buffer cache**
2. **Elevator scheduler (CFQ, deadline, noop, bfq)**
3. **Driver del dispositivo**
4. **Controller hardware**

Linux offre più **scheduler I/O** selezionabili (es. con `cat /sys/block/sda/queue/scheduler`):

* `noop` → semplice FIFO (ottimo per SSD)
* `deadline` → priorità temporali per evitare starvation
* `cfq` → fairness tra processi (per HDD tradizionali)
* `bfq` → bilanciamento ottimizzato per carichi misti

---

## 🧠 Mappa concettuale di sintesi

```plaintext
GESTIONE I/O (II)
│
├── Struttura disco
│   ├─ Tracce e settori
│   └─ T_accesso = T_seek + T_rot + T_trans
│
├── Scheduling dischi
│   ├─ FCFS → ordine di arrivo
│   ├─ SSTF → minimo spostamento
│   ├─ SCAN / C-SCAN → movimento “ascensore”
│   └─ LOOK / C-LOOK → ottimizzati
│
├── RAID
│   ├─ RAID 0 → striping, veloce
│   ├─ RAID 1 → mirroring, sicuro
│   ├─ RAID 5 → parità distribuita
│   ├─ RAID 6 → doppia parità
│   └─ RAID 10 → mirroring + striping
│
├── HDD vs SSD
│   ├─ HDD → meccanico, lento, seek time
│   ├─ SSD → elettronico, rapido, usura celle
│   └─ TRIM e wear leveling
│
└── I/O in Linux
    ├─ Character / Block device
    ├─ Major e minor number
    ├─ Scheduler: noop, deadline, cfq, bfq
    └─ Stack I/O → cache → scheduler → driver → controller
```
