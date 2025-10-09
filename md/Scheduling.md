# Scheduling

## 🔹 Introduzione generale

In un sistema operativo multiprogrammato, **più processi o thread competono per l’uso della CPU**.
Poiché in genere il numero dei processi attivi è superiore al numero dei processori disponibili, è necessario stabilire un criterio che decida **chi debba essere eseguito in un dato momento**.
Questo insieme di criteri e politiche prende il nome di **scheduling** (o **pianificazione della CPU**).

Il componente del sistema operativo che si occupa di queste decisioni è detto **scheduler**, mentre l’azione di scegliere quale processo assegnare alla CPU si chiama **dispatching**.
Ogni decisione di scheduling implica un **context switch**, cioè il salvataggio dello stato del processo in esecuzione e il caricamento di quello del processo successivo.

L’obiettivo fondamentale dello scheduling è massimizzare **l’utilizzo della CPU** mantenendo **reattività e giustizia (fairness)** tra i processi.

---

## 🔹 Obiettivi dello scheduling

Gli obiettivi variano a seconda del tipo di sistema operativo (batch, interattivo, real-time), ma si possono distinguere due macro-categorie di priorità.

### 1. Obiettivi nei sistemi batch

Nei sistemi batch, dove i processi vengono eseguiti in blocco senza interazione con l’utente, lo scheduling è orientato all’**efficienza globale** del sistema:

* **Massimizzare il throughput** → aumentare il numero di processi completati per unità di tempo.
* **Minimizzare il tempo di turnaround** → ridurre l’intervallo tra la sottomissione e la conclusione di un processo.
* **Ridurre l’overhead di CPU** → minimizzare il tempo speso in cambio di contesto e gestione.

### 2. Obiettivi nei sistemi interattivi

Nei sistemi interattivi, in cui l’utente si aspetta risposte rapide, l’attenzione si sposta sulla **reattività**:

* **Minimizzare il tempo di risposta** → ridurre il ritardo tra l’input dell’utente e la risposta del sistema.
* **Garantire la fairness** → evitare che processi a bassa priorità restino indefinitamente in attesa.
* **Gestire la priorità** → consentire che processi critici (es. di sistema) vengano eseguiti prima.

### 3. Compromessi

Lo scheduling cerca un equilibrio tra:

* **efficienza** (alto throughput)
* **reattività** (risposta veloce)
* **giustizia** (tutti i processi ricevono attenzione)
* **predicibilità** (tempi di risposta costanti)

---

## 🔹 Tipi di scheduling

Il sistema operativo può applicare politiche di scheduling su **diversi livelli** del ciclo di vita dei processi.

### 1. Long-Term Scheduling (a lungo termine)

È responsabile della **selezione dei processi da ammettere in memoria** per l’esecuzione.
Agisce nel momento in cui un nuovo job entra nel sistema.
Il suo compito è regolare il **grado di multiprogrammazione**, ovvero quante attività possono trovarsi contemporaneamente in memoria.

* Se il grado di multiprogrammazione è troppo alto → rischio di **thrashing** (eccessivo swapping e rallentamento generale).
* Se è troppo basso → CPU sotto-utilizzata.

Nei sistemi moderni (es. Linux desktop), questo tipo di scheduling è spesso implicito o automatico, ma resta fondamentale nei sistemi batch e real-time.

### 2. Medium-Term Scheduling (a medio termine)

Gestisce la **sospensione e riattivazione** dei processi.
Il suo obiettivo è migliorare l’utilizzo della memoria principale, eseguendo operazioni di:

* **swap out** → rimuovere temporaneamente un processo dalla memoria.
* **swap in** → ricaricarlo quando ci sono risorse disponibili.

È un meccanismo utile nei sistemi con memoria limitata o con processi di lunga durata, e contribuisce al controllo del carico di sistema.

### 3. Short-Term Scheduling (a breve termine)

È lo **scheduling vero e proprio della CPU**.
Il suo compito è selezionare, tra i processi pronti (stato *ready*), quello che dovrà essere eseguito immediatamente.
Opera con frequenza molto elevata (millisecondi o microsecondi), poiché ogni volta che:

* un processo termina il proprio quanto di tempo,
* entra un nuovo processo ready,
* o un processo viene risvegliato da uno stato di blocco,
  il CPU scheduler deve decidere chi eseguire.

Questo tipo di scheduling è quello che ha **l’impatto diretto sulla reattività percepita dall’utente**.

### 4. I/O Scheduling

Gestisce l’ordine di esecuzione delle richieste ai dispositivi di I/O.
Poiché le operazioni di I/O sono molto più lente di quelle di CPU, l’obiettivo è **ridurre i tempi di attesa** e **ottimizzare il throughput del disco o della periferica**.
Viene approfondito in seguito, ma qui basta sapere che rappresenta una forma specializzata di scheduling, spesso gestita a livello di driver.

---

## 🔹 Tipologie di scheduling: preemptive vs non-preemptive

Uno dei parametri più importanti per classificare gli algoritmi di scheduling è la possibilità o meno di **interrompere un processo in esecuzione**.

* **Non-preemptive** → il processo mantiene la CPU fino a quando termina o entra in stato di attesa.
  È più semplice, ma meno reattivo.
  Esempi: FCFS, SPN, HRRN.

* **Preemptive** → il sistema può forzare la sospensione del processo per assegnare la CPU a un altro (ad esempio, più prioritario o appena arrivato).
  È più complesso ma migliora l’interattività.
  Esempi: RR, SRT.

---

## 🔹 Algoritmi di scheduling della CPU

Il cuore dello scheduling a breve termine è costituito dagli **algoritmi di selezione del processo**.
Ogni algoritmo stabilisce un criterio di scelta e una politica di sostituzione tra processi nella ready queue.

### FCFS – *First Come, First Served*

* È il più semplice algoritmo non-preemptive.
* I processi vengono eseguiti nell’ordine di arrivo nella coda ready (FIFO).
* Una volta ottenuta la CPU, il processo la mantiene fino al termine.

**Vantaggi:**

* Implementazione semplice.
* Nessun overhead di cambio di contesto.

**Svantaggi:**

* Può causare il **convoy effect**: un processo lungo trattiene la CPU e costringe i successivi ad attendere.
* Tempi di risposta elevati per processi brevi.

È adatto per sistemi batch, ma inefficiente in ambienti interattivi.

---

### RR – *Round Robin*

* È una variante preemptive del FCFS.
* Ogni processo riceve un **quanto di tempo (time quantum)** fisso.
* Quando il quanto scade, il processo viene sospeso e rimesso in coda, mentre la CPU passa al successivo.

**Vantaggi:**

* Garantisce **equità** (tutti i processi ottengono la CPU in modo ciclico).
* Migliora la **reattività** nei sistemi interattivi.
* Semplice da implementare.

**Svantaggi:**

* Se il quanto è troppo grande → degrada a FCFS.
* Se è troppo piccolo → aumenta il numero di context switch, riducendo l’efficienza.

La scelta ottimale del **time quantum** è quindi un compromesso tra reattività e overhead.

---

### SPN – *Shortest Process Next* (o SJF – Shortest Job First)

* Politica **non-preemptive** che seleziona il processo con il **burst time più breve**.
* Si basa sull’ipotesi che il tempo di esecuzione di ciascun processo sia stimabile.

**Vantaggi:**

* Minimizza il tempo medio di attesa e di turnaround.
* Teoricamente, è l’algoritmo più efficiente in termini di tempo medio.

**Svantaggi:**

* Difficile stimare con precisione il burst time.
* Possibile **starvation** per processi lunghi che vengono continuamente rimandati.

---

### SRT – *Shortest Remaining Time*

* È la versione **preemptive** di SPN.
* Ogni volta che arriva un nuovo processo, viene confrontato il suo burst con quello rimanente del processo in esecuzione.
* Se il nuovo processo ha un burst più breve, preempie l’attuale.

**Vantaggi:**

* Migliora il tempo medio di attesa rispetto a SPN.
* Ottimale nei sistemi con processi brevi e frequenti.

**Svantaggi:**

* Elevato overhead dovuto ai continui preemption.
* Ancora più esposto al rischio di starvation per processi lunghi.

---

### HRRN – *Highest Response Ratio Next*

* Politica **non-preemptive** che migliora SPN introducendo un criterio di priorità dinamica:
  [
  R = \frac{W + S}{S}
  ]
  dove:
  ( W ) = tempo di attesa,
  ( S ) = tempo di servizio stimato.

**Funzionamento:**

* I processi che attendono da molto tempo aumentano progressivamente la propria priorità.
* In questo modo, un processo lungo ma in attesa da tempo ottiene la CPU prima o poi.

**Vantaggi:**

* Evita starvation.
* Buon compromesso tra tempo medio di attesa e fairness.

**Svantaggi:**

* Non preemptive → non adatto a sistemi interattivi.
* Richiede calcolo periodico del rapporto ( R ).

---

### Tabella comparativa algoritmi

| Algoritmo     | Preemptive | Vantaggi principali                | Svantaggi principali                 |
| ------------- | ---------- | ---------------------------------- | ------------------------------------ |
| **FCFS**      | No         | Semplice, poco overhead            | Convoy effect, scarsa reattività     |
| **RR**        | Sì         | Equità, buoni tempi di risposta    | Dipende dal quanto, overhead elevato |
| **SPN (SJF)** | No         | Ottimo tempo medio di attesa       | Starvation, stima burst difficile    |
| **SRT**       | Sì         | Migliora SPN, ottimizza tempi medi | Starvation, overhead alto            |
| **HRRN**      | No         | Evita starvation, bilanciato       | Non preemptive, calcolo frequente    |

---

## 🔹 Scheduling multiprocessore e Scheduling UNIX/Linux

---

## 🔹 1. Introduzione

Nei sistemi moderni, la presenza di **più CPU o core** rende necessario un tipo di scheduling più complesso, capace di distribuire in modo equilibrato il carico di lavoro tra i processori.
In questo contesto, il compito dello scheduler non è più solo decidere *quale processo eseguire*, ma anche *su quale processore eseguirlo*.
Il problema viene quindi esteso da una dimensione temporale (“quando”) a una dimensione spaziale (“dove”).

Il principale obiettivo dello **scheduling multiprocessore** è quello di garantire:

* un **uso bilanciato** delle CPU (nessun core sovraccarico o inattivo);
* un **throughput elevato** complessivo;
* la **minimizzazione del tempo di attesa e di risposta**;
* la **coerenza della cache**, cioè evitare spostamenti inutili di thread tra core.

---

## 🔹 2. Tipologie di scheduling multiprocessore

Esistono diversi modelli e strategie per gestire la pianificazione su più CPU, che si differenziano per il grado di **cooperazione e indipendenza** tra i processori.

### a) Asymmetric Multiprocessing (AMP)

Nel modello **asimmetrico**, solo un processore (detto *master*) è responsabile dello scheduling e della gestione dei processi di sistema.
Gli altri processori (*slave*) si limitano a eseguire i processi assegnati.

**Caratteristiche:**

* Il processore master gestisce la ready queue globale e distribuisce il lavoro.
* I processori slave non prendono decisioni di scheduling.
* È un modello semplice, ma con **collo di bottiglia**: il master può diventare un punto di congestione.
* Utilizzato nei primi sistemi multiprocessore o embedded.

---

### b) Symmetric Multiprocessing (SMP)

Il modello **simmetrico** è quello adottato dai sistemi moderni (inclusi Linux, Windows, macOS).
Tutti i processori sono equivalenti e ciascuno possiede **il proprio scheduler locale**.

**Caratteristiche principali:**

* Tutte le CPU possono accedere alle stesse code dei processi (ready queue).
* Ogni CPU può schedulare processi in modo indipendente.
* I processi possono essere spostati da una CPU all’altra (migrazione).

**Problema principale:** la **migrazione dei processi** tra CPU comporta perdita di efficienza della cache (cache miss), poiché i dati del processo devono essere caricati nella cache del nuovo processore.
Per questo motivo, i moderni scheduler SMP cercano di mantenere, se possibile, la **CPU affinity**.

---

## 🔹 3. CPU Affinity

La **CPU affinity** (o *process affinity*) rappresenta la tendenza di un processo o thread a essere eseguito sempre sulla stessa CPU.
Questo migliora le prestazioni grazie al **riuso della cache**, riducendo il numero di cache miss e migliorando la località dei dati.

### Tipi di affinità

#### 1. Soft affinity

* Il sistema tenta di mantenere il processo sulla stessa CPU, ma non lo garantisce.
* È una preferenza, non un vincolo.
* Usata nei sistemi generici per flessibilità.

#### 2. Hard affinity

* L’associazione tra processo e CPU è obbligatoria.
* Può essere impostata manualmente dall’utente o dal sistema operativo (`taskset` in Linux).
* Riduce il bilanciamento dinamico ma aumenta la coerenza della cache.

---

## 🔹 4. Load Balancing

In un sistema multiprocessore, può accadere che alcune CPU siano sovraccariche e altre inattive.
Il **load balancing** serve a distribuire equamente il carico di lavoro tra le CPU.

### Strategie principali

#### Push migration

Lo scheduler controlla periodicamente le code di tutte le CPU e sposta attivamente processi da quelle sovraccariche a quelle libere.

#### Pull migration

Una CPU inattiva “pesca” un processo da una coda di un’altra CPU.

Il bilanciamento può essere:

* **globale:** tutte le CPU condividono una coda comune di processi (ready queue globale).
  → Più equo ma meno scalabile.
* **locale:** ogni CPU ha la propria coda, con meccanismi di bilanciamento periodici.
  → Più efficiente ma più complesso da mantenere coerente.

---

## 🔹 5. Scheduling in UNIX / Linux

Linux utilizza un modello di scheduling **SMP completamente simmetrico**, con un approccio **multilivello** e **basato su priorità dinamiche**.
Nel corso delle versioni, sono stati sviluppati diversi scheduler; i più importanti sono:

* **O(1) Scheduler** (fino a Linux 2.6)
* **CFS – Completely Fair Scheduler** (dal kernel 2.6.23 in poi, tutt’ora in uso)

Oltre a questi, Linux supporta anche politiche real-time conformi allo standard **POSIX**.

---

## 🔹 6. Scheduler O(1)

L’**O(1) scheduler** è stato introdotto per ottenere una decisione di scheduling in tempo costante (complessità O(1)), indipendentemente dal numero di processi nel sistema.

### Struttura

* Ogni CPU possiede due code:

  * **Active queue:** contiene i processi pronti all’esecuzione.
  * **Expired queue:** contiene i processi che hanno esaurito il proprio quanto.
    Quando la coda attiva si svuota, le due code vengono scambiate.

### Caratteristiche principali

* Ogni processo ha una **priorità dinamica**, che aumenta o diminuisce in base al comportamento (CPU-bound o I/O-bound).
* Gli I/O-bound vengono favoriti per ridurre i tempi di risposta.
* I processi di tipo batch vengono penalizzati progressivamente per evitare starvation.

Questo scheduler è molto efficiente e scalabile, ma tende a favorire eccessivamente i processi interattivi.

---

## 🔹 7. Completely Fair Scheduler (CFS)

Il **CFS (Completely Fair Scheduler)**, introdotto nelle versioni moderne di Linux, si basa sul principio di **equa condivisione della CPU** tra i processi, senza utilizzare code statiche né quanti di tempo fissi.

L’idea di fondo è che **ogni processo deve ottenere una frazione di CPU proporzionale alla sua priorità**, in modo “completamente equo”.

### Principio di funzionamento

* Ogni processo ha un valore chiamato **vruntime (virtual runtime)**, che misura il tempo di CPU effettivamente ottenuto.
* Lo scheduler mantiene un **albero bilanciato (red-black tree)** ordinato per `vruntime`.
* Il processo con il minor `vruntime` (cioè quello che ha ricevuto meno CPU) viene selezionato per l’esecuzione.
* Quando un processo esegue, il suo `vruntime` aumenta; così, nel tempo, tutti ricevono un trattamento proporzionale.

### Vantaggi del CFS

* Non richiede code distinte o scambi periodici.
* Bilancia automaticamente CPU-bound e I/O-bound.
* Supporta facilmente il bilanciamento tra CPU diverse.
* È deterministico e scalabile.

### Intervallo temporale

Il CFS non definisce un quanto fisso; calcola dinamicamente un **target latency**, cioè il tempo in cui tutti i processi attivi dovrebbero ottenere la CPU almeno una volta.
Se ci sono pochi processi, ciascuno ottiene una fetta più grande; se i processi aumentano, la fetta diventa più piccola.

---

## 🔹 8. Politiche di scheduling in Linux

Linux supporta tre **classi di scheduling principali**, ciascuna con logica e priorità distinte:

| Classe             | Descrizione                        | Politica                                | Note                                            |
| ------------------ | ---------------------------------- | --------------------------------------- | ----------------------------------------------- |
| **SCHED_OTHER**    | Default (CFS) per processi normali | Time-sharing                            | Priorità dinamiche, fairness                    |
| **SCHED_FIFO**     | Real-time, priorità assoluta       | Non-preemptive FIFO                     | Usata per processi critici, esempio audio/video |
| **SCHED_RR**       | Real-time, round-robin             | Preemptive                              | Simile a FIFO ma con quanto di tempo fisso      |
| **SCHED_DEADLINE** | Real-time soft                     | Basato su EDF (Earliest Deadline First) | Introdotto per sistemi deterministici           |

Le politiche real-time (`SCHED_FIFO`, `SCHED_RR`, `SCHED_DEADLINE`) hanno **priorità superiori** rispetto ai processi CFS.
In caso di conflitto, i thread real-time hanno sempre la precedenza.

---

## 🔹 9. Struttura del PCB in Linux per lo scheduling

Il **PCB** (`task_struct`) contiene campi specifici per la gestione dello scheduling:

* **policy** → indica la classe (OTHER, FIFO, RR, DEADLINE)
* **prio** e **static_prio** → priorità statica e dinamica
* **vruntime** → tempo di CPU virtuale
* **se.run_list** → puntatore nell’albero red-black del CFS
* **cpus_allowed** → maschera di affinità CPU
* **se.load.weight** → peso proporzionale alla priorità

Ogni CPU ha inoltre una propria **runqueue** locale (`rq`), che mantiene i processi ready e coordina il bilanciamento.

---

## 🔹 10. Sintesi concettuale per mappa

```plaintext
SCHEDULING (II)
│
├── Scheduling multiprocessore
│   ├─ AMP → master/slave, semplice ma collo di bottiglia
│   └─ SMP → CPU simmetriche, schedulazione locale
│
├── CPU Affinity
│   ├─ Soft affinity → preferenza
│   └─ Hard affinity → vincolo fisso
│
├── Load balancing
│   ├─ Push migration → spinta dai core attivi
│   └─ Pull migration → prelievo da core inattivi
│
├── Linux Scheduler
│   ├─ O(1) → due code (active/expired), priorità dinamiche
│   ├─ CFS → fairness tramite vruntime e red-black tree
│   └─ Target latency → fetta CPU proporzionale
│
├── Politiche Linux
│   ├─ SCHED_OTHER → CFS (normale)
│   ├─ SCHED_FIFO → real-time FIFO
│   ├─ SCHED_RR → real-time Round Robin
│   └─ SCHED_DEADLINE → EDF (Earliest Deadline First)
│
└── PCB Linux
    ├─ policy, prio, vruntime
    ├─ se.load.weight
    └─ cpus_allowed (affinità)
```
