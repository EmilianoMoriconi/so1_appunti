# Processi

---

## 🔹 Introduzione

Uno dei compiti fondamentali di un sistema operativo è la **gestione dei processi**, cioè l’insieme delle attività in esecuzione nel sistema.
Un processo rappresenta l’**unità fondamentale di esecuzione**: è un programma “vivo”, in corso di esecuzione, con un proprio stato, risorse assegnate e contesto operativo.

Il SO deve poter:

* **creare**, **schedulare** e **terminare** i processi;
* **tenere traccia** del loro stato e delle risorse utilizzate;
* **garantire isolamento e sincronizzazione** quando più processi condividono la CPU o la memoria.

Il concetto di processo è quindi alla base di tutto il funzionamento dinamico del sistema operativo.

---

## 🔹 1. Processo vs programma

Un **programma** è un insieme statico di istruzioni memorizzate su disco.
Un **processo**, invece, è la **manifestazione dinamica del programma** in esecuzione: include contesto, risorse, variabili, stack e stato di avanzamento.

| Aspetto   | Programma                         | Processo                         |
| --------- | --------------------------------- | -------------------------------- |
| Natura    | Statico                           | Dinamico                         |
| Posizione | Disco                             | Memoria                          |
| Contenuto | Codice                            | Codice + dati + stato            |
| Scopo     | Rappresenta un compito potenziale | Esegue effettivamente un compito |

Esempio:

> Aprire due finestre di “Calcolatrice” esegue **lo stesso programma** due volte, ma genera **due processi distinti**, ognuno con le proprie variabili e stato interno.

---

## 🔹 2. Componenti di un processo

Un processo in esecuzione è composto da diverse **sezioni di memoria** e **strutture di gestione**.

### a) Spazio di indirizzamento (address space)

Il sistema operativo assegna a ciascun processo un proprio **spazio logico di memoria** suddiviso in sezioni:

| Sezione           | Contenuto                                   |
| ----------------- | ------------------------------------------- |
| **Text (o code)** | Istruzioni eseguibili del programma         |
| **Data**          | Variabili globali e statiche                |
| **Heap**          | Allocazioni dinamiche (es. `malloc`, `new`) |
| **Stack**         | Chiamate di funzione e variabili locali     |

Ogni processo crede di avere un proprio spazio di memoria indipendente, ma in realtà il SO lo mappa sulla memoria fisica in modo controllato.

### b) Stato e contesto

Il **contesto** di un processo rappresenta il suo “punto di vita” nel sistema:

* Valore dei registri CPU (PC, SP, ecc.)
* Stato del processo (ready, running, waiting…)
* Informazioni su memoria, file aperti, priorità, ecc.

Questo contesto è ciò che il SO salva e ripristina durante i **context switch**.

---

## 🔹 3. Stati del processo

Durante il suo ciclo di vita, un processo attraversa diversi **stati logici**, ciascuno gestito dal SO.

### a) Modello a 2 stati

* **Running:** il processo è in esecuzione sulla CPU.
* **Not running:** il processo è pronto o in attesa.

Semplice ma limitato: non distingue tra “pronto” e “bloccato”.

### b) Modello a 5 stati

È il modello più comune nei sistemi moderni.

| Stato                 | Descrizione                                       |
| --------------------- | ------------------------------------------------- |
| **New**               | Il processo è stato creato ma non ancora avviato. |
| **Ready**             | In memoria, attende la CPU.                       |
| **Running**           | Sta eseguendo istruzioni.                         |
| **Blocked (Waiting)** | Attende un evento (es. I/O, segnale).             |
| **Terminated**        | Ha terminato l’esecuzione o è stato ucciso.       |

### c) Stati sospesi

Oltre ai 5 classici, molti SO aggiungono:

* **Ready suspended**: pronto ma spostato su disco per mancanza di memoria.
* **Blocked suspended**: bloccato e non residente in memoria.

Questi stati consentono al SO di gestire la **memoria virtuale** e lo **swap**.

---

## 🔹 4. Transizioni di stato

Le transizioni rappresentano i **passaggi logici** tra gli stati durante la vita del processo.

Esempio di ciclo tipico:

```text
NEW → READY → RUNNING → WAITING → READY → TERMINATED
```

### Casi principali

* **Creazione:** `new → ready` (ammissione in memoria).
* **Scheduling:** `ready → running` (assegnazione CPU).
* **Preemption:** `running → ready` (fine quanto).
* **I/O request:** `running → waiting`.
* **I/O completion:** `waiting → ready`.
* **Exit:** `running → terminated`.

Il **dispatcher** del SO gestisce queste transizioni tramite **context switch**.

---

## 🔹 5. PCB – Process Control Block

Per ogni processo, il sistema operativo mantiene una struttura dati chiamata **PCB (Process Control Block)**, che contiene tutte le informazioni necessarie per la sua gestione.

### Struttura tipica del PCB

| Categoria               | Contenuto                                   |
| ----------------------- | ------------------------------------------- |
| **Identificazione**     | PID (Process ID), PPID (Parent ID), utente  |
| **Stato di esecuzione** | Stato (ready, running…), contesto CPU       |
| **Scheduling**          | Priorità, tempo CPU usato, puntatore a code |
| **Memoria**             | Puntatori a tabelle delle pagine o segmenti |
| **File e I/O**          | File aperti, dispositivi assegnati          |
| **Sicurezza**           | UID, permessi di accesso                    |

Durante un **context switch**, il kernel salva il PCB del processo uscente e carica quello del processo entrante.
È attraverso questa struttura che il SO “ricorda” esattamente dove ogni processo si era fermato.

---

## 🔹 6. Code di processi

Per gestire i diversi stati, il SO organizza i processi in **code**.

| Coda                | Descrizione                                |
| ------------------- | ------------------------------------------ |
| **Ready queue**     | Processi pronti in attesa di CPU           |
| **Device queues**   | Processi in attesa di completamento I/O    |
| **Job queue**       | Tutti i processi presenti nel sistema      |
| **Suspended queue** | Processi temporaneamente rimossi dalla RAM |

Ogni scheduler opera su una coda diversa (long, short, medium-term scheduler).

---

## 🔹 7. Operazioni sui processi

### a) Creazione

Un processo può generare nuovi processi figli tramite una **system call** (es. `fork()` in UNIX).
Il processo figlio eredita parte dello stato del padre (file aperti, variabili, ambiente).

### b) Terminazione

Un processo può terminare:

* **Volontariamente** (`exit()`)
* **Forzatamente** (`kill()`, errore, segnale del SO)

Quando un processo termina, il suo PCB viene rimosso e le risorse liberate.

### c) Blocco e sblocco

Durante l’esecuzione, un processo può:

* essere **bloccato** (es. in attesa di I/O);
* essere **risvegliato** quando l’evento atteso si verifica.

---

## 🔹 8. Processi e gerarchie

Nei sistemi moderni i processi formano **alberi di esecuzione**:

* Ogni processo padre può generare più processi figli.
* I figli possono a loro volta creare altri processi.

Esempio in UNIX:

```text
init (PID 1)
 ├─ systemd
 │   ├─ login
 │   ├─ sshd
 │   └─ bash
 │       └─ python
```

Il kernel mantiene relazioni **PPID (Parent Process ID)** per tracciare queste gerarchie.
Quando un padre termina, i figli diventano **orfani** e vengono “adottati” da `init`.

---

## 🔹 9. Relazione con i thread

Un processo può contenere **uno o più thread**, ovvero **flussi di esecuzione paralleli** che condividono la stessa memoria e risorse del processo.
Il processo fornisce l’**ambiente di esecuzione**, mentre i thread sono le **unità effettive di esecuzione**.
Questo concetto verrà approfondito nella lezione successiva.

---

## 🧠 Mappa concettuale di sintesi

```plaintext
PROCESSI
│
├── Definizione
│   ├─ Unità di esecuzione gestita dal SO
│   └─ Programma + stato + risorse
│
├── Componenti
│   ├─ Spazio memoria → code, data, heap, stack
│   ├─ Contesto CPU → registri, PC, flag
│   └─ PCB → dati di controllo
│
├── Stati
│   ├─ New, Ready, Running, Waiting, Terminated
│   └─ Sospesi (Ready/Blocked suspended)
│
├── Transizioni
│   ├─ new→ready →running →waiting →ready→terminated
│   └─ Gestite da scheduler + dispatcher
│
├── Code di sistema
│   ├─ Ready queue
│   ├─ Device queues
│   └─ Suspended queue
│
├── Operazioni
│   ├─ Creazione (fork)
│   ├─ Terminazione (exit / kill)
│   └─ Blocco / sblocco
│
├── Gerarchie
│   └─ Processi padre/figlio, PID e PPID
│
└── Relazione con i thread
    └─ Processo = contenitore, thread = unità esecutiva
```
