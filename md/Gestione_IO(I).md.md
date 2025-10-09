# Gestione I/O (I)

## 🔹 Introduzione

L’**Input/Output (I/O)** rappresenta la parte del sistema operativo che gestisce la **comunicazione tra la CPU e i dispositivi periferici** (dischi, tastiere, stampanti, reti, ecc.).
Questa componente è essenziale, poiché consente al sistema di **interagire con il mondo esterno**, trasferendo dati tra memoria e dispositivi.

L’I/O è intrinsecamente **più lento** rispetto alla CPU e alla memoria: per questo motivo, uno dei compiti fondamentali del sistema operativo è **ottimizzare il tempo di attesa** e massimizzare la **concorrenza tra calcolo e trasferimento dati**.

In generale, il sottosistema I/O si occupa di:

* nascondere le differenze tra i vari dispositivi;
* gestire errori e stati;
* ottimizzare l’uso delle risorse hardware;
* fornire un’interfaccia uniforme ai processi utente.

---

## 🔹 1. Architettura del sottosistema I/O

Il sistema operativo organizza la gestione dell’I/O secondo una **struttura multilivello**, che va dal software applicativo fino al dispositivo fisico.

### Livelli principali

1. **Livello utente (User Level):**

   * L’applicazione interagisce con il sistema tramite **chiamate di sistema (system call)** come `read()`, `write()`, `open()`, `close()`.
   * Il programmatore non si occupa dei dettagli hardware: la gestione è delegata al kernel.

2. **Livello kernel (Kernel Level):**

   * Include il **file system**, i **device driver**, la **gestione buffer**, e il **scheduling dell’I/O**.
   * Si occupa di tradurre le richieste utente in operazioni fisiche sul dispositivo.

3. **Livello hardware:**

   * Composto dai **controller dei dispositivi**, che comunicano direttamente con la CPU e la memoria.
   * Ogni controller gestisce uno o più dispositivi fisici.

### Flusso generale

```text
Programma utente
   ↓
System call (es. read/write)
   ↓
Driver dispositivo
   ↓
Controller hardware
   ↓
Dispositivo fisico (disk, printer, etc.)
```

Il sistema operativo fa da **intermediario e coordinatore**, fornendo un livello di astrazione che rende uniforme l’accesso a dispositivi anche molto diversi tra loro.

---

## 🔹 2. Componenti dell’I/O

### a) Device Controller

È un’unità hardware che funge da **interfaccia tra la CPU e il dispositivo fisico**.
Ogni controller gestisce uno o più dispositivi dello stesso tipo (es. un controller SATA per i dischi, un controller USB per le periferiche esterne).

**Funzioni principali:**

* interpretare i comandi provenienti dal driver;
* gestire i registri di stato, controllo e dati;
* segnalare alla CPU il completamento di un’operazione (tramite interrupt).

### b) Device Driver

È un modulo software (parte del kernel) che **traduce le richieste generiche del sistema operativo in comandi specifici per il controller**.
Ogni tipo di dispositivo ha il proprio driver.

**Responsabilità principali:**

* inviare comandi al controller;
* gestire gli interrupt di completamento o errore;
* fornire un’interfaccia standard al kernel (es. funzioni `read()`, `write()`).

Il driver rappresenta il punto di contatto diretto tra **software e hardware**, e deve rispettare precise specifiche per interagire con il kernel.

---

## 🔹 3. Tecniche di comunicazione CPU–Dispositivo

Le operazioni di I/O possono essere realizzate con diverse modalità, che variano per **grado di coinvolgimento della CPU**.

### a) I/O programmato (Polling)

* La CPU controlla periodicamente lo stato del dispositivo leggendo un **registro di stato**.
* Quando il dispositivo è pronto, la CPU trasferisce manualmente i dati.

**Vantaggi:**

* Implementazione semplice.

**Svantaggi:**

* La CPU resta impegnata in attesa del dispositivo → **spreco di tempo di calcolo**.
* Poco efficiente per dispositivi lenti.

### b) I/O con interrupt

* Il dispositivo genera un **interrupt** quando termina un’operazione o è pronto per trasferire dati.
* La CPU può dedicarsi ad altro nel frattempo.

**Funzionamento:**

1. Il processo richiede un’operazione I/O.
2. Il driver configura il controller e mette il processo in attesa (stato *blocked*).
3. Il dispositivo esegue l’operazione autonomamente.
4. Al completamento, il controller genera un interrupt → il kernel risveglia il processo.

**Vantaggi:**

* La CPU non resta inattiva.
* Maggiore efficienza e reattività.

**Svantaggi:**

* Overhead dovuto alla gestione dell’interrupt (context switch).
* Maggiore complessità del kernel.

### c) I/O con DMA (Direct Memory Access)

Il **DMA** è un meccanismo hardware che permette al controller del dispositivo di **accedere direttamente alla memoria**, senza passare dalla CPU per ogni byte trasferito.

**Funzionamento:**

1. La CPU prepara la richiesta I/O (indirizzo sorgente, destinazione, quantità).
2. Il **DMA controller** gestisce il trasferimento autonomamente.
3. Al termine, genera un **interrupt** per segnalare il completamento.

**Vantaggi:**

* Drastica riduzione del carico sulla CPU.
* Prestazioni elevate per trasferimenti di grandi dimensioni (es. disco → RAM).

**Svantaggi:**

* Hardware più complesso.
* Richiede sincronizzazione tra CPU e DMA per evitare conflitti sulla memoria.

---

## 🔹 4. Bufferizzazione

La **bufferizzazione (buffering)** serve a **compensare le differenze di velocità** tra CPU, memoria e dispositivi di I/O.
Un **buffer** è una zona di memoria temporanea usata per accumulare dati in transito.

### Tipi di buffer

#### a) Single Buffer

Un solo buffer tra dispositivo e processo.
→ Quando il buffer è pieno, il processo viene sospeso finché non viene svuotato.

#### b) Double Buffer

Due buffer usati in alternanza:

* mentre uno viene riempito, l’altro viene svuotato.
  → Migliora la sovrapposizione tra calcolo e I/O.

#### c) Circular Buffer

Più buffer in sequenza collegati circolarmente (FIFO).
→ Usato in sistemi ad alto throughput (streaming, rete).

### Vantaggi

* Aumenta il parallelismo tra CPU e I/O.
* Riduce i tempi morti del dispositivo.

### Svantaggi

* Maggiore uso di memoria.
* Necessità di gestione sincronizzata (accesso concorrente).

---

## 🔹 5. Spooling

Il termine **spooling** (Simultaneous Peripheral Operation On-Line) indica una **tecnica di gestione concorrente** di dispositivi di I/O condivisi, come stampanti o unità disco.

### Funzionamento

* Le richieste I/O non vengono servite immediatamente ma **accodate in un’area di memoria o su disco (spool area)**.
* Un **demone (spooler)** legge periodicamente la coda e le esegue in ordine.

**Esempio classico:**
Più utenti inviano stampe → i file vengono messi in coda → lo spooler li stampa in sequenza.

### Vantaggi

* Permette l’uso **condiviso** di dispositivi non rientranti (non multitasking).
* Evita blocchi del sistema in attesa del completamento di un I/O.
* Migliora la **concorrenza e il throughput complessivo**.

---

## 🔹 6. Struttura software del sistema I/O

Il sottosistema I/O è organizzato su più livelli, dal più astratto (software utente) al più vicino all’hardware.

### Livelli tipici

| Livello                 | Funzione principale                              |
| ----------------------- | ------------------------------------------------ |
| **Software utente**     | Chiamate di sistema (`read`, `write`)            |
| **Software di sistema** | File system e librerie I/O                       |
| **Device driver**       | Traduzione comandi generici in comandi specifici |
| **Interrupt handler**   | Gestione segnali di completamento o errore       |
| **Controller**          | Comunicazione diretta con il dispositivo fisico  |

Ogni livello comunica con il successivo tramite **interfacce standard**, rendendo il sistema modulare e facilmente estendibile.

---

## 🧠 Mappa concettuale di sintesi

```plaintext
GESTIONE I/O (I)
│
├── Architettura
│   ├─ Livello utente → system call (read/write)
│   ├─ Livello kernel → driver, buffer, scheduler
│   └─ Livello hardware → controller, device
│
├── Componenti
│   ├─ Device controller → gestisce registri e interrupt
│   └─ Driver → traduce richieste OS → hardware
│
├── Tecniche I/O
│   ├─ Programmato → polling, CPU attiva
│   ├─ Interrupt-driven → CPU notificata
│   └─ DMA → accesso diretto memoria
│
├── Buffering
│   ├─ Single → uno solo
│   ├─ Double → due alternati
│   └─ Circular → multipli (FIFO)
│
├── Spooling
│   ├─ Accodamento richieste I/O
│   ├─ Gestito da spooler
│   └─ Esempio → stampa multipla
│
└── Struttura software
    ├─ Utente → system call
    ├─ Kernel → driver e interrupt handler
    └─ Hardware → controller dispositivo
```
