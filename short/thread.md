# 📘 Thread

## 🔹 Concetto di Thread

* Un **thread** è un *flusso di esecuzione* all’interno di un processo.
* Un processo può avere più thread, ognuno con la propria sequenza di istruzioni da eseguire.
* I thread **condividono le risorse del processo** (memoria, file aperti, dispositivi I/O), ma hanno **stack separati** per le variabili locali e i contesti di chiamata.
* Questo permette di ottenere **parallelismo logico**: anche su un processore singolo-core, l’OS alterna i thread così velocemente che sembrano andare in parallelo.
* Vantaggi: minore overhead rispetto ai processi, più facile comunicazione e sincronizzazione, maggiore efficienza.

---

## 🔹 Implementazioni: ULT vs KLT

### 1. **ULT – User Level Thread**

* I thread sono gestiti da **librerie nello user space**, non dal kernel.
* Il sistema operativo non sa nemmeno che esistono: per lui c’è un solo processo.

**Vantaggi**:

* Creazione e terminazione molto veloci (non serve interazione con il kernel).
* Lo switching fra thread è più leggero perché non richiede **mode switch**.
* Ogni applicazione può implementare il proprio algoritmo di scheduling personalizzato.
* Consentono di avere thread anche su sistemi operativi che non li supportano nativamente.

**Svantaggi**:

* Se un thread si blocca (ad esempio su I/O), si blocca tutto il processo con tutti i suoi thread.
* In presenza di più core, tutti i thread di un processo restano comunque vincolati a **un solo core**.
* Il sistema operativo non può gestire direttamente i thread per operazioni di sistema.

---

### 2. **KLT – Kernel Level Thread**

* I thread sono gestiti direttamente dal **kernel**.
* Ogni thread è visto come un’entità schedulabile indipendente.

**Vantaggi**:

* Se un thread si blocca, gli altri thread dello stesso processo possono continuare.
* Supportano il vero parallelismo su architetture multi-core/multi-CPU.
* Consentono al sistema operativo di usare thread interni (kernel threads) per svolgere le proprie operazioni.

**Svantaggi**:

* Creazione, terminazione e context switch sono più costosi, perché serve l’intervento del kernel.
* Lo scheduling è centralizzato e meno flessibile (deciso dal SO, non dall’applicazione).

---

📊 **Tabella Comparativa ULT vs KLT**

| Caratteristica         | ULT (User Level Thread)            | KLT (Kernel Level Thread)         |
| ---------------------- | ---------------------------------- | --------------------------------- |
| Gestione               | Libreria in user space             | Kernel                            |
| Visibilità OS          | Processo unico                     | Ogni thread indipendente          |
| Creazione/terminazione | Molto veloce                       | Più lenta (serve kernel)          |
| Context switch         | Leggero, senza mode switch         | Più pesante, con mode switch      |
| Blocco thread          | Blocca tutti i thread del processo | Blocca solo il thread interessato |
| Multi-core             | Non sfruttato                      | Supporto pieno                    |
| Scheduling             | Personalizzabile dall’app          | Fissato dal kernel                |

---

## 🔹 Operazioni sui Thread

1. **Spawn** → Creazione di un nuovo thread (“germogliare” da un thread esistente).
2. **Block** → Sospensione del thread (non per I/O, ma volontaria, ad esempio in attesa di un altro thread).
3. **Unblock** → Riattivazione del thread sospeso.
4. **Finish** → Terminazione di un thread al termine della sua esecuzione.

---

## 🔹 Thread in Linux

* In Linux, i thread sono implementati come **Lightweight Process (LWP)**.
* Per Linux, *non esistono processi in senso classico*: tutto è un LWP.
* Più LWP che condividono risorse comuni formano quello che all’utente appare come un processo multithread.

### Identificatori

* **PID**: Process Identifier (visibile all’utente, in realtà coincide con il **TGID**).
* **TGID**: Thread Group ID → identificatore del gruppo di thread (il primo thread creato).
* **TID**: Thread Identifier → identifica i singoli thread.

### PCB (Process Control Block) in Linux

* Ogni thread ha un proprio PCB (perché è schedulabile singolarmente).
* Il PCB contiene:

  * Stato del thread.
  * Registri del processore e kernel stack.
  * Puntatori ai thread dello stesso gruppo.
  * Puntatori a padre, figli e fratelli.
  * Informazioni su segnali e interruzioni.

### Stati dei thread in Linux

* **TASK_RUNNING**: include sia *ready* che *running*.
* **TASK_INTERRUPTIBLE / UNINTERRUPTIBLE**: blocked (diverse cause di attesa).
* **TASK_STOPPED / TASK_TRACED**: fermo o in debug.
* **EXIT_ZOMBIE / EXIT_DEAD**: terminato, in attesa di rimozione.

---

📌 **Schema Riassuntivo PCB Linux**

* **Thread info** → contiene kernel stack e puntatori a strutture di sistema.
* **Thread group** → link agli altri thread del processo.
* **Parent/real parent** → processi padre.
* **Signal handlers** → gestori dei segnali.
* **Resources** → file aperti, memoria condivisa, ecc.
