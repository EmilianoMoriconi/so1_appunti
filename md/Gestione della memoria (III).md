# Gestione della memoria (III)

---

## 🔹 Introduzione

Dopo aver introdotto la memoria virtuale e i meccanismi di paging, resta da affrontare uno degli aspetti più complessi della gestione della memoria: **la scelta delle pagine da mantenere in RAM e quelle da rimpiazzare** quando la memoria fisica è piena.

Ogni volta che un processo accede a una pagina non presente in memoria, si verifica un **page fault**, che richiede di caricare la pagina dal disco.
Questo evento è molto costoso (migliaia di cicli di CPU) e influisce direttamente sulle prestazioni del sistema.

Per questo motivo, è fondamentale adottare **algoritmi di rimpiazzo** efficienti e strategie di controllo che limitino il numero di page fault e prevengano fenomeni di **thrashing**.

---

## 🔹 1. Page Fault e Swapping

Un **page fault** si verifica quando un processo accede a una pagina che **non è attualmente in memoria fisica**.
Il sistema operativo interviene con una serie di operazioni:

1. **Interruzione** → la CPU rileva il page fault e passa il controllo al sistema operativo.
2. **Verifica** → si controlla se l’indirizzo richiesto è valido e la pagina appartiene effettivamente al processo.
3. **Scelta del frame da liberare** → se la memoria è piena, occorre liberare un frame usando un **algoritmo di rimpiazzo**.
4. **Scrittura su disco** → se la pagina nel frame scelto è “dirty”, viene salvata (scritta su disco).
5. **Caricamento della nuova pagina** → la pagina mancante viene caricata dallo spazio di swap nel frame libero.
6. **Aggiornamento delle tabelle** (Page Table e TLB).
7. **Ripresa dell’esecuzione** dal punto in cui il processo era stato interrotto.

Il **tempo medio di accesso effettivo alla memoria (EAT)** dipende dalla frequenza di page fault e dal tempo necessario per gestirli:

[
EAT = (1 - p) \times t_m + p \times t_{pf}
]

dove:

* ( t_m ) = tempo di accesso alla memoria,
* ( p ) = probabilità di page fault,
* ( t_{pf} ) = tempo di servizio del page fault (molto elevato).

Anche una piccola percentuale di page fault (es. 0,01%) può aumentare drasticamente il tempo medio di accesso.

---

## 🔹 2. Algoritmi di rimpiazzo delle pagine

Quando non ci sono frame liberi, il sistema operativo deve scegliere **quale pagina rimuovere dalla memoria** per fare spazio a quella nuova.
Questa decisione è critica: una scelta sbagliata può aumentare il numero di page fault.

Di seguito i principali algoritmi, dal più semplice al più sofisticato.

---

### FIFO – *First In, First Out*

* Le pagine vengono gestite in una coda circolare: la più vecchia viene rimpiazzata per prima.
* Implementazione semplice, ma **non tiene conto dell’utilizzo effettivo**.

**Problemi:**

* Possibile **anomalìa di Belady** → aumentando il numero di frame, i page fault possono aumentare invece di diminuire.
* Scarsa efficienza per programmi che riutilizzano frequentemente le stesse pagine.

---

### OPT – *Optimal Replacement* (teorico)

* Rimpiazza la pagina che **non sarà più utilizzata per il periodo di tempo più lungo**.
* È l’algoritmo ideale in termini di prestazioni minime di page fault.

**Limite:**
Non può essere implementato realmente, perché richiede la conoscenza futura della sequenza di accessi.
→ Viene usato come **riferimento teorico** per confrontare le prestazioni degli altri algoritmi.

---

### LRU – *Least Recently Used*

* Rimpiazza la pagina **non utilizzata da più tempo**.
* Si basa sul principio di **località temporale**: le pagine usate di recente tenderanno a essere usate ancora a breve.

**Implementazioni possibili:**

1. **Contatori temporali:** ogni pagina ha un timestamp aggiornato a ogni accesso.
   → quando serve rimpiazzare, si sceglie quella con il timestamp più vecchio.
   (Preciso ma costoso da aggiornare a ogni accesso).

2. **Stack (lista ordinata):** le pagine sono mantenute in una lista, e ogni accesso sposta la pagina in testa.
   → buona accuratezza ma overhead alto.

**Vantaggi:**

* Prestazioni vicine all’ottimo.

**Svantaggi:**

* Costi hardware e software elevati per mantenere lo storico.

---

### Second-Chance (Clock Algorithm)

È una **versione approssimata di LRU**, molto usata nei sistemi reali.
Le pagine sono disposte in un **buffer circolare** (come FIFO), ma ogni pagina ha un **bit di riferimento (R)**.

**Funzionamento:**

1. Quando si deve rimpiazzare una pagina, si controlla il bit R della pagina “più vecchia”:

   * Se R = 0 → viene rimpiazzata.
   * Se R = 1 → il bit viene azzerato e la pagina riceve una “seconda possibilità”.
2. L’indicatore (clock hand) avanza fino a trovare una pagina con R = 0.

**Vantaggi:**

* Prestazioni simili a LRU, ma con overhead ridotto.
* Implementazione efficiente a livello hardware.

---

### NRU – *Not Recently Used*

Classifica le pagine in quattro categorie, combinando due bit:

| Bit R | Bit M | Categoria                        | Priorità di rimpiazzo |
| ----- | ----- | -------------------------------- | --------------------- |
| 0     | 0     | Non usata né modificata          | Alta                  |
| 0     | 1     | Non usata, modificata            | Media                 |
| 1     | 0     | Usata di recente, non modificata | Bassa                 |
| 1     | 1     | Usata e modificata               | Molto bassa           |

L’algoritmo sceglie una pagina casuale dalla **classe con priorità più alta** disponibile.
Semplice ma meno preciso rispetto a LRU.

---

### LFU – *Least Frequently Used*

Rimuove la pagina **meno utilizzata nel tempo** (in base a un contatore di accessi).
Buono per carichi stabili, ma può reagire male a variazioni improvvise di comportamento (pagine vecchie ma “popolari” restano troppo a lungo).

---

## 🔹 3. Algoritmi di allocazione dei frame

Ogni processo deve avere assegnato un certo numero di **frame** in memoria fisica.
Il sistema operativo deve stabilire **quanti frame concedere** e come gestirli nel tempo.

### Allocazione fissa vs dinamica

* **Allocazione fissa:**
  ogni processo riceve un numero costante di frame per tutta la durata.
  → semplice ma inefficiente se i processi cambiano comportamento.

* **Allocazione dinamica:**
  i frame vengono assegnati e revocati dinamicamente in base al carico o al numero di page fault.

### Allocazione proporzionale

I frame vengono assegnati in proporzione alla dimensione del processo:
[
\text{frame_i} = \frac{\text{dimensione_i}}{\text{totale_memoria}} \times \text{frame_totali}
]

### Allocazione con priorità

I processi con priorità più alta ricevono più frame (o frame riservati) per ridurre il rischio di page fault critici.

---

## 🔹 4. Thrashing

Il **thrashing** è un fenomeno che si verifica quando un processo spende più tempo a eseguire operazioni di **paging (swap in/out)** che ad eseguire istruzioni utili.
In pratica, la memoria è troppo piccola per mantenere il **working set** del processo, causando continui page fault.

### Cause principali

* Numero di processi troppo alto rispetto alla RAM disponibile.
* Allocazione inadeguata dei frame.
* Algoritmi di rimpiazzo non ottimali.

### Effetti

* Crollo del throughput.
* CPU fortemente sotto-utilizzata (la maggior parte del tempo attende I/O).
* Drastico rallentamento del sistema.

---

## 🔹 5. Modelli di controllo del thrashing

### a) Working Set Model

Il **working set** di un processo è l’insieme delle pagine che **sono state utilizzate recentemente** in una finestra temporale ∆ (numero di riferimenti).

L’idea è che un processo ha bisogno di mantenere in RAM il proprio working set per funzionare in modo efficiente.

**Strategia:**

* Si monitora il working set di ciascun processo.
* Se la somma dei working set di tutti i processi supera la memoria fisica, il sistema sospende o swap-out alcuni processi.
  → Evita il thrashing globale.

### b) Page Fault Frequency (PFF)

Si basa sulla **frequenza di page fault** del processo:

* Se la frequenza di page fault è **troppo alta**, vengono assegnati più frame.
* Se è **troppo bassa**, alcuni frame vengono tolti (per essere assegnati ad altri processi).

Questo metodo consente un adattamento dinamico in base al comportamento effettivo.

---

## 🔹 6. Prestazioni e compromessi

Il controllo della memoria virtuale si basa su un equilibrio tra:

* **Numero di frame assegnati** ↔ **page fault rate**
* **Politiche di rimpiazzo** ↔ **overhead di gestione**
* **Multiprogrammazione** ↔ **thrashing**

Un sistema operativo efficiente deve saper **adattare dinamicamente le politiche di allocazione e sostituzione** in funzione del carico.

---

## 🧠 Mappa concettuale di sintesi

```plaintext
GESTIONE DELLA MEMORIA (III)
│
├── Page Fault
│   ├─ Rilevamento e gestione
│   ├─ Swapping su disco
│   └─ Tempo medio EAT = (1-p)*tm + p*tpf
│
├── Algoritmi di rimpiazzo
│   ├─ FIFO → semplice, ma Belady
│   ├─ OPT → ideale, teorico
│   ├─ LRU → località temporale
│   ├─ Second-Chance → approssimazione LRU
│   ├─ NRU → classi R/M
│   └─ LFU → frequenza accessi
│
├── Allocazione frame
│   ├─ Fissa vs dinamica
│   ├─ Proporzionale → dimensione processo
│   └─ Per priorità
│
├── Thrashing
│   ├─ Cause → troppe page fault
│   ├─ Effetti → CPU inattiva, swap continuo
│   └─ Soluzioni → Working Set, PFF
│
└── Controllo dinamico
    ├─ Working Set → memoria minima necessaria
    └─ PFF → adattamento automatico
```

---

Vuoi che per **Martedì 14/10 – File System (I)** passiamo alla parte su **organizzazione, strutture, e gestione dei file (directory, metadati, allocazione)** con lo stesso stile e profondità?
