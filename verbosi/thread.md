# 📘 Thread

## 🔹 Concetto di Thread

Un thread rappresenta un **flusso di esecuzione** all’interno di un processo.
Ogni processo viene creato con almeno un thread, ma può contenerne più di uno.
La presenza di più thread consente a un singolo processo di svolgere **più compiti in parallelo**, pur continuando a condividere le stesse risorse del processo (memoria, file aperti, dispositivi di I/O).

L’unico elemento che i thread non condividono è lo **stack delle chiamate**, poiché ogni thread deve mantenere in maniera indipendente le variabili locali e il contesto delle funzioni che sta eseguendo.
Tutto il resto, come codice, dati globali, heap e risorse acquisite, rimane invece in comune.

Il vantaggio principale dei thread rispetto ai processi è che risultano **più leggeri**, perché:

* sono più rapidi da creare e da terminare;
* lo switching tra thread richiede meno operazioni rispetto a quello tra processi;
* la comunicazione tra thread è più semplice, in quanto avviene direttamente tramite la memoria condivisa.

Per questo motivo, i thread sono utilizzati quando è necessario implementare forme di **parallelismo** o **concorrenza** senza introdurre il costo elevato della gestione di più processi indipendenti.

---

## 🔹 Implementazioni: ULT e KLT

Esistono due approcci principali per implementare i thread: **ULT (User Level Thread)** e **KLT (Kernel Level Thread)**.

### 1. ULT – User Level Thread

Nei thread a livello utente, la gestione è affidata a una **libreria nello user space**.
Il kernel non è a conoscenza dell’esistenza dei singoli thread, ma vede soltanto il processo.

* **Vantaggi**:

  * Creazione, terminazione e cambio di thread molto veloci, perché non è necessario invocare il kernel.
  * Nessun passaggio da user mode a kernel mode durante lo switching.
  * Ogni applicazione può definire una propria politica di scheduling dei thread, indipendente da quella del sistema operativo.
  * Consentono di utilizzare i thread anche su sistemi operativi che non li supportano nativamente.

* **Svantaggi**:

  * Se un thread si blocca in una chiamata di sistema bloccante (es. I/O), tutto il processo si blocca insieme a lui, inclusi gli altri thread.
  * Non è possibile sfruttare appieno i sistemi multiprocessore o multicore, poiché i thread di un processo rimangono vincolati a un singolo core.
  * Il sistema operativo non può utilizzare i thread per le proprie funzioni di sistema.

---

### 2. KLT – Kernel Level Thread

Nei thread a livello kernel, la gestione è effettuata direttamente dal **sistema operativo**.
Ogni thread è riconosciuto e schedulato come entità indipendente.

* **Vantaggi**:

  * Se un thread si blocca, gli altri thread dello stesso processo possono continuare a eseguire.
  * In presenza di sistemi multiprocessore, più thread dello stesso processo possono essere eseguiti realmente in parallelo su CPU diverse.
  * Consentono al sistema operativo stesso di utilizzare thread interni (kernel threads) per le proprie operazioni, ad esempio per la gestione della memoria o delle operazioni I/O.

* **Svantaggi**:

  * La creazione e la terminazione di thread sono più costose in termini di tempo, perché richiedono l’intervento del kernel.
  * Lo scheduling è deciso unicamente dal kernel, quindi è meno flessibile per le applicazioni.
  * Il context switch è più pesante, perché comporta un passaggio da user mode a kernel mode.

---

📊 **Riepilogo comparativo ULT vs KLT**

| Aspetto                  | ULT (User Level Thread)         | KLT (Kernel Level Thread)  |
| ------------------------ | ------------------------------- | -------------------------- |
| Gestione                 | Libreria user space             | Kernel                     |
| Visibilità al SO         | Il kernel vede un solo processo | Ogni thread è indipendente |
| Creazione e terminazione | Molto rapida                    | Più lenta                  |
| Context switch           | Leggero (solo user space)       | Più pesante (mode switch)  |
| Blocco thread            | Blocca tutto il processo        | Blocca solo il thread      |
| Supporto multicore       | Non utilizzabile                | Pieno supporto             |
| Scheduling               | Personalizzabile dall’app       | Gestito dal kernel         |

---

## 🔹 Operazioni Fondamentali sui Thread

Un thread, una volta creato, può compiere le seguenti operazioni principali:

1. **Spawn**: creazione di un nuovo thread all’interno del processo.
2. **Block**: sospensione esplicita del thread, ad esempio in attesa di un evento o di un altro thread.
3. **Unblock**: riattivazione di un thread che era stato bloccato.
4. **Finish**: terminazione del thread al termine della sua esecuzione.

Queste operazioni consentono di gestire in maniera dinamica i thread e di coordinare le loro esecuzioni.

---

## 🔹 Thread in Linux

In Linux, i thread sono implementati come **Lightweight Process (LWP)**.
Un LWP è l’unità schedulabile di base: quindi, per Linux, non esistono processi “puri”, ma soltanto insiemi di LWP che condividono risorse comuni.

### Identificazione

* **PID**: identificatore di processo, che in realtà coincide con il TGID.
* **TGID** (Thread Group ID): identifica il gruppo di thread che costituisce un processo.
* **TID** (Thread ID): identifica il singolo thread.

Ogni thread è quindi schedulabile come unità indipendente, ma fa parte di un gruppo che viene percepito dall’utente come un processo.

### PCB in Linux

Ogni LWP ha un proprio **Process Control Block (PCB)**, che contiene:

* lo **stack del kernel**, usato nelle chiamate in modalità sistema;
* puntatori agli altri thread del gruppo;
* riferimenti al processo padre e ai processi figli;
* informazioni sullo stato del thread;
* strutture per la gestione dei segnali.

In questo modo il kernel può gestire separatamente i singoli thread, pur mantenendo il legame con il gruppo a cui appartengono.

### Stati dei Thread in Linux

Linux adotta una variante del modello classico a 5 stati, con le seguenti categorie:

* **TASK_RUNNING**: comprende sia *ready* che *running*.
* **TASK_INTERRUPTIBLE / TASK_UNINTERRUPTIBLE**: diverse forme di *blocked*, a seconda che il thread possa o meno essere risvegliato da un segnale.
* **TASK_STOPPED / TASK_TRACED**: thread fermato o sotto debug.
* **EXIT_ZOMBIE / EXIT_DEAD**: thread terminato, ma ancora presente nelle strutture del kernel.

---

📌 In sintesi, i thread in Linux sono trattati come entità autonome schedulabili (LWP), ma organizzati in gruppi che all’utente appaiono come processi.
Questo modello unisce la flessibilità dei KLT, gestiti dal kernel, con la possibilità di implementare librerie ULT che vengono poi mappate in LWP reali.
