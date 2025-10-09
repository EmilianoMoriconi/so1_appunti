# 📘 Thread

## 🔹 Introduzione generale

Il concetto di **thread** nasce dall’esigenza di aumentare il grado di concorrenza all’interno dei sistemi operativi moderni.
Un **thread** può essere definito come un **flusso indipendente di controllo** che si muove all’interno di un processo. In altre parole, è l’unità più piccola di esecuzione che il sistema operativo può pianificare sulla CPU.

Un processo può contenere **uno o più thread**. Quando esiste un solo thread, si parla di processo *monothreaded*; quando invece il processo contiene più thread, si parla di *multithreaded*.
In un processo multithread, tutti i thread condividono le **stesse risorse** del processo (come spazio di indirizzamento, file aperti, variabili globali, heap), ma mantengono **stack separati** per poter gestire le proprie chiamate di funzione e variabili locali in modo indipendente.

Questo permette ai thread di operare contemporaneamente su diverse porzioni del programma, riducendo drasticamente il costo in termini di risorse rispetto alla creazione di nuovi processi.
Infatti, la **creazione di un processo** richiede di duplicare lo spazio di memoria, le strutture del kernel e l’ambiente di esecuzione; invece, creare un thread richiede solo la creazione di uno stack e di poche informazioni di contesto.

---

## 🔹 Vantaggi dell’approccio multithread

L’utilizzo dei thread consente di ottenere **parallelismo logico** anche su sistemi single-core, perché l’OS alterna rapidamente i thread in esecuzione, dando l’impressione di simultaneità.
Nei sistemi multi-core, invece, i thread possono essere effettivamente eseguiti in **parallelo reale**, su core diversi.

I principali vantaggi dell’uso dei thread sono:

1. **Maggiore efficienza**: la creazione, la terminazione e lo switch tra thread richiedono meno risorse e tempo rispetto ai processi.
2. **Migliore utilizzo della CPU**: se un thread è bloccato in attesa di I/O, un altro dello stesso processo può continuare ad eseguire.
3. **Comunicazione più semplice**: i thread possono condividere direttamente le variabili e i dati nello stesso spazio di memoria, evitando il bisogno di meccanismi complessi come pipe o socket.
4. **Migliore strutturazione del programma**: un programma complesso può essere suddiviso in flussi logici separati (ad esempio: thread per l’interfaccia grafica, thread per la logica applicativa, thread per I/O o rete).

---

## 🔹 Thread a livello utente (ULT) e a livello kernel (KLT)

Il modo in cui i thread vengono implementati può variare.
Esistono due approcci principali: i **thread a livello utente (ULT)** e i **thread a livello kernel (KLT)**.
La differenza sta in chi gestisce la loro esecuzione e schedulazione.

### ▫️ Thread a livello utente (ULT)

I thread a livello utente vengono gestiti da una **libreria nello user space**.
Il sistema operativo non è consapevole della loro esistenza: per il kernel, l’intero processo appare come un’unica entità schedulabile.

Quando si fa uno *switch* tra thread nello stesso processo, l’operazione è gestita interamente dalla libreria di thread e non richiede alcuna chiamata di sistema.
Questo comporta tempi di esecuzione estremamente ridotti, poiché si evita il passaggio da **user mode a kernel mode**, che rappresenta un’operazione costosa.

Tuttavia, l’assenza di intervento del kernel introduce alcuni problemi:

* se un thread effettua una chiamata bloccante (ad esempio una `read()` su un file o su un socket), **tutto il processo rimane bloccato**, perché il kernel non è in grado di distinguere i singoli thread;
* in presenza di più CPU o core, non è possibile sfruttare il parallelismo hardware, poiché per il kernel c’è sempre un solo processo attivo.

In sintesi, gli ULT sono veloci e leggeri, ma non adatti a sistemi multiprocessore e a programmi che fanno uso intensivo di operazioni bloccanti.

---

### ▫️ Thread a livello kernel (KLT)

I thread a livello kernel vengono invece **gestiti direttamente dal sistema operativo**.
Ogni thread è riconosciuto come entità indipendente e schedulabile.

Questo significa che il kernel può eseguire un thread su un core e un altro thread dello stesso processo su un core diverso, ottenendo **vero parallelismo**.
Inoltre, se un thread si blocca, gli altri thread del processo possono continuare la loro esecuzione.

Il rovescio della medaglia è che la gestione da parte del kernel introduce un **maggiore overhead**:

* ogni creazione o terminazione di thread richiede una chiamata di sistema;
* ogni cambio di contesto (context switch) implica il salvataggio dello stato nel PCB del thread e il passaggio in kernel mode.

Lo scheduling è centralizzato e non può essere personalizzato dall’applicazione, ma garantisce pieno supporto al multiprocessore e una gestione robusta delle risorse.

---

### ▫️ Riepilogo comparativo ULT vs KLT

| Aspetto                  | ULT (User Level Thread)   | KLT (Kernel Level Thread) |
| ------------------------ | ------------------------- | ------------------------- |
| Gestione                 | Libreria in user space    | Kernel                    |
| Visibilità OS            | Processo unico            | Ogni thread schedulabile  |
| Creazione / terminazione | Molto veloce              | Più costosa               |
| Context switch           | Solo user mode            | Richiede mode switch      |
| Blocco thread            | Blocca tutto il processo  | Blocca solo il thread     |
| Supporto multicore       | No                        | Sì, pieno                 |
| Scheduling               | Personalizzabile dall’app | Gestito dal kernel        |

---

## 🔹 Operazioni fondamentali sui thread

I thread, indipendentemente dal tipo di implementazione, possono trovarsi in stati diversi e compiere alcune operazioni tipiche:

* **Spawn**: creazione di un nuovo thread, che eredita il contesto del processo padre e viene aggiunto alla ready queue.
* **Block**: sospensione volontaria o forzata di un thread, ad esempio in attesa di un evento o di una risorsa condivisa.
* **Unblock**: riattivazione di un thread precedentemente sospeso, quando la condizione di attesa è soddisfatta.
* **Finish**: terminazione del thread, che libera lo stack e le strutture di gestione associate.

Ogni thread mantiene il proprio **contesto di esecuzione**, costituito da:

* il valore dei registri del processore (incluso il program counter),
* lo stato (running, ready, waiting, ecc.),
* lo stack per le variabili locali,
* un puntatore alla memoria condivisa del processo.

Il **context switch** tra thread consiste nel salvare il contesto del thread uscente e nel caricare quello del thread entrante.
Nei sistemi ULT questo avviene in user mode (molto rapido), mentre nei KLT comporta il coinvolgimento del kernel (più lento ma più sicuro).

---

## 🔹 Thread in Linux: LWP e PCB

Nel sistema operativo Linux, l’implementazione dei thread si basa su un concetto intermedio chiamato **Lightweight Process (LWP)**.
Un LWP è una struttura schedulabile che rappresenta un thread, ma possiede molte caratteristiche di un processo classico.

In Linux, non esiste una distinzione netta tra processi e thread: entrambi sono entità gestite tramite la stessa struttura dati, chiamata **task_struct**, che funge da **Process Control Block (PCB)**.
Ogni LWP ha quindi un proprio PCB, ma più LWP possono condividere le stesse risorse, come lo spazio di indirizzamento, i file aperti e le aree di memoria.

I campi principali del PCB di Linux sono:

* **stato** del thread (TASK_RUNNING, TASK_INTERRUPTIBLE, ecc.);
* **registri salvati** e **puntatori allo stack del kernel**;
* **relazioni di parentela** (padre, figli, gruppo di thread);
* **informazioni di scheduling** (priorità, CPU assegnata, contatori di tempo);
* **segnali e gestori di segnali**;
* **puntatori alle risorse condivise** (file, memoria, namespace, ecc.).

### Stati principali in Linux

Linux utilizza un modello di stati più articolato rispetto a quello classico dei processi:

* **TASK_RUNNING** → thread in esecuzione o pronto per l’esecuzione;
* **TASK_INTERRUPTIBLE** → thread bloccato ma risvegliabile da un segnale;
* **TASK_UNINTERRUPTIBLE** → bloccato, non risvegliabile finché la risorsa non è disponibile;
* **TASK_STOPPED / TASK_TRACED** → thread fermato o sotto debug;
* **EXIT_ZOMBIE / EXIT_DEAD** → thread terminato, ma non ancora completamente rimosso dalle strutture del kernel.

Ogni thread in Linux ha un **TID (Thread ID)** univoco e appartiene a un gruppo di thread identificato da un **TGID (Thread Group ID)**.
Il TGID corrisponde al PID del thread principale del gruppo, cioè quello che rappresenta il processo “padre” visto dall’esterno.

---

## 🔹 Sintesi finale

In Linux, i thread non sono entità separate dai processi ma ne rappresentano delle “versioni leggere”.
Tutti i thread che appartengono allo stesso processo condividono:

* il codice eseguibile,
* lo spazio di memoria virtuale,
* le risorse di I/O,
* i segnali e il gruppo di credenziali.

Ogni thread mantiene però il proprio **stack, registri e stato indipendente**, permettendo al kernel di schedularli singolarmente.

Questa architettura ibrida unisce la flessibilità dei KLT con la leggerezza degli ULT, rendendo il modello di Linux uno dei più efficienti per i sistemi multiprocessore.

## 🔹 Sincronizzazione tra Thread

Quando più thread condividono risorse comuni — ad esempio variabili globali, strutture dati in memoria, file o buffer di I/O — è necessario **coordinare il loro accesso** per evitare conflitti e risultati incoerenti.
Questo problema prende il nome di **sincronizzazione**.

### ▫️ Problema di concorrenza e sezione critica

Il caso più tipico è quello della **sezione critica**, ovvero una porzione di codice che accede a risorse condivise e che non deve essere eseguita da più thread contemporaneamente.

Senza un’adeguata sincronizzazione, possono verificarsi condizioni di **race condition** (condizioni di competizione): due o più thread tentano di leggere o modificare la stessa variabile contemporaneamente, e il risultato finale dipende dall’ordine di esecuzione, che è imprevedibile.

Per garantire l’integrità dei dati, il sistema operativo (o la libreria dei thread) deve assicurare che la sezione critica soddisfi tre condizioni fondamentali:

1. **Mutua esclusione:** solo un thread per volta può trovarsi nella sezione critica.
2. **Progresso:** se nessun thread è nella sezione critica, deve essere consentito l’ingresso a uno di quelli in attesa.
3. **Attesa limitata:** nessun thread deve essere escluso indefinitamente.

---

## 🔹 Strumenti di sincronizzazione

La sincronizzazione può essere implementata in vari modi, a seconda del livello di astrazione (software, libreria o kernel).
I principali strumenti sono:

### 1. **Mutex (Mutual Exclusion Lock)**

Il mutex è il meccanismo più elementare per implementare la **mutua esclusione**.
Si tratta di una variabile binaria che può trovarsi in due stati: *libero* (unlocked) o *occupato* (locked).

* Quando un thread entra nella sezione critica, deve **acquisire (lock)** il mutex.
  Se il mutex è libero, il thread entra; se invece è già occupato, il thread viene sospeso finché non diventa disponibile.
* Quando il thread termina la sezione critica, **rilascia (unlock)** il mutex, permettendo ad altri di entrare.

L’uso corretto dei mutex garantisce che solo un thread per volta acceda alla risorsa condivisa.
Tuttavia, un uso scorretto può generare **deadlock**, ovvero situazioni in cui due o più thread rimangono bloccati perché ognuno attende un mutex posseduto da un altro.

**Esempio logico:**

* Thread A blocca `mutex1` e poi tenta di bloccare `mutex2`.
* Thread B ha già bloccato `mutex2` e tenta di bloccare `mutex1`.
  Nessuno dei due potrà proseguire → deadlock.

---

### 2. **Semafori**

I **semafori** sono una generalizzazione del mutex introdotta da Dijkstra.
Un semaforo è una variabile intera non negativa che rappresenta il **numero di risorse disponibili**.

Si gestisce tramite due operazioni atomiche:

* `wait()` (o `P`): decrementa il semaforo. Se il valore diventa negativo, il thread si blocca.
* `signal()` (o `V`): incrementa il semaforo. Se ci sono thread bloccati, ne risveglia uno.

Esistono due tipi principali di semafori:

1. **Semaforo binario:** può assumere solo i valori 0 o 1 (equivalente a un mutex).
2. **Semaforo contatore:** può assumere valori maggiori di 1, utile per controllare un numero finito di risorse identiche (es. connessioni di rete, buffer).

I semafori sono potenti ma più difficili da gestire correttamente, poiché non garantiscono automaticamente l’esclusività d’accesso e possono facilmente portare a situazioni di **starvation** (alcuni thread attendono indefinitamente).

---

### 3. **Condition Variable**

Le **condition variable** permettono a un thread di sospendersi in attesa di una certa condizione logica e di essere risvegliato quando quella condizione diventa vera.
Sono sempre usate insieme a un mutex.

Il meccanismo è il seguente:

* Il thread acquisisce un mutex ed entra in una sezione monitorata.
* Se la condizione non è ancora soddisfatta, chiama `wait()` sulla condition variable: questo rilascia temporaneamente il mutex e sospende il thread.
* Quando un altro thread modifica la condizione, chiama `signal()` o `broadcast()` sulla condition variable, risvegliando uno o più thread sospesi.
* I thread risvegliati riacquisiscono il mutex e ricontrollano la condizione.

Questo modello è usato nei **monitor**, ovvero strutture di sincronizzazione di alto livello che incapsulano variabili condivise e le operazioni di accesso in modo sicuro.

---

### 4. **Join e sincronizzazione del flusso**

Oltre alle sezioni critiche, è necessario sincronizzare il **flusso di esecuzione** dei thread, ovvero controllare *quando* un thread deve attendere il completamento di un altro.
Il metodo più comune è la **join operation**.

Quando un thread principale (ad esempio il thread "padre") crea altri thread figli, può eseguire su ciascuno di essi l’operazione:

```c
pthread_join(thread_id, NULL);
```

In questo modo, il thread padre si sospende fino a quando il thread figlio identificato da `thread_id` termina.
Questa operazione assicura che tutte le elaborazioni parallele si completino prima di proseguire.

---

### 5. **Barrier**

Una **barriera** è un meccanismo che consente a un gruppo di thread di sincronizzarsi a un punto preciso del programma.
Ogni thread, al raggiungimento della barriera, si blocca finché anche tutti gli altri non la raggiungono.
Solo quando tutti i thread sono arrivati, la barriera si apre e tutti possono proseguire.
È molto utilizzata nei programmi scientifici o nei calcoli distribuiti, dove diverse parti di un algoritmo devono sincronizzarsi periodicamente.

---

## 🔹 Problemi tipici della sincronizzazione

### ▫️ Deadlock

Un **deadlock** si verifica quando due o più thread si bloccano reciprocamente, ognuno in attesa di una risorsa posseduta dall’altro.
Le quattro condizioni necessarie per il verificarsi di un deadlock (secondo Coffman) sono:

1. **Mutua esclusione** – le risorse non possono essere condivise.
2. **Hold and wait** – un thread trattiene una risorsa e ne richiede altre.
3. **No preemption** – le risorse non possono essere sottratte forzatamente.
4. **Attesa circolare** – esiste una catena di thread in cui ciascuno attende una risorsa posseduta dal successivo.

Prevenire o evitare i deadlock richiede strategie come:

* imporre un **ordine globale di acquisizione delle risorse**,
* introdurre **timeout**,
* o applicare algoritmi di rilevamento e recupero (ad esempio rilasciando e ripetendo l’operazione).

---

### ▫️ Starvation

La **starvation** si verifica quando uno o più thread non riescono mai ad accedere a una risorsa, a causa della presenza costante di altri thread con priorità più alta.
Può accadere, ad esempio, in algoritmi non equi di scheduling o in uso scorretto dei semafori.

### ▫️ Busy waiting e spinlock

Un’altra problematica è il **busy waiting**, che si verifica quando un thread, invece di sospendersi, continua a controllare in un ciclo se una risorsa è libera (tipico degli spinlock).
Questo può sprecare tempo di CPU, ma su sistemi multiprocessore è utile per sezioni critiche molto brevi, in quanto evita il costo del cambio di contesto.

---

## 🔹 Sincronizzazione in Linux

In ambiente Linux (e in generale nei sistemi POSIX), la sincronizzazione tra thread è gestita tramite la **pthread library** (`<pthread.h>`).
Essa fornisce meccanismi standardizzati per:

* **Mutex** (`pthread_mutex_t`),
* **Condition variables** (`pthread_cond_t`),
* **Semafori** (`sem_t`),
* **Barrier** (`pthread_barrier_t`).

Il kernel Linux, inoltre, offre meccanismi di sincronizzazione interni (come *spinlock*, *seqlock*, *rwlock* e *RCU – Read-Copy-Update*) utilizzati per proteggere strutture dati interne del kernel stesso, dove la rapidità è più importante della sospensione dei thread.

---

## 🔹 Sintesi generale

In un sistema multithread, la sincronizzazione è l’elemento che garantisce la **correttezza logica** del programma e la **coerenza dei dati**.
Senza di essa, l’esecuzione concorrente porterebbe a comportamenti imprevedibili e errori difficili da individuare.

L’obiettivo è sempre trovare il **compromesso tra sicurezza e efficienza**:

* troppa sincronizzazione riduce il parallelismo;
* troppo poca genera condizioni di gara o inconsistenza.

Un buon sistema operativo (e un buon programmatore) deve quindi progettare sezioni critiche piccole, atomiche e protette da meccanismi adeguati, scegliendo il tipo di sincronizzazione più adatto alla situazione.
