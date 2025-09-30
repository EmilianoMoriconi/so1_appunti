# 📘 Processi

## 🔹 1. Definizione di processo e PCB

Quando parliamo di **processo**, non dobbiamo confonderlo con il semplice concetto di programma.
Un **programma** è un’entità statica: un file contenente istruzioni, salvato su disco, che da solo non fa nulla finché non viene eseguito.
Un **processo**, invece, è qualcosa di dinamico: è un **programma in esecuzione**, cioè l’istanza attiva di quel programma che vive nella memoria principale, usa la CPU, accede a dispositivi e mantiene uno stato proprio.

Un processo, quindi, non è formato solo dal codice che deve eseguire, ma anche da:

* un insieme di **dati** (variabili globali, strutture, heap, ecc.);
* lo **stack delle chiamate** (che tiene traccia delle funzioni chiamate e delle variabili locali);
* lo **stato di esecuzione**, cioè informazioni sul punto preciso a cui si trova nel programma e su quali risorse sta utilizzando;
* una serie di **attributi** che lo distinguono da tutti gli altri processi.

Tra questi attributi c’è un identificativo univoco, il **PID (Process Identifier)**, che è una sorta di “carta d’identità” del processo, indispensabile al sistema operativo per poterlo distinguere da tutti gli altri.

Perché il sistema operativo riesca a gestire correttamente decine o centinaia di processi contemporaneamente, serve una struttura dati molto importante: il **Process Control Block (PCB)**.
Il PCB è una vera e propria “scheda anagrafica” del processo, gestita dal sistema operativo e mantenuta costantemente aggiornata.

Dentro un PCB troviamo diverse categorie di informazioni:

* **Identificazione**: PID, identificativo del processo padre (PPID), utente proprietario (UID), ecc.
* **Stato del processo**: se è in esecuzione, pronto, in attesa, sospeso, terminato.
* **Stato del processore**: contiene i valori dei registri della CPU quando il processo viene interrotto, incluso il Program Counter (che indica l’indirizzo della prossima istruzione da eseguire) e il Program Status Word (che riassume le condizioni della CPU).
* **Gestione della memoria**: puntatori alle strutture che descrivono lo spazio di memoria del processo (es. tabella delle pagine, segmenti di codice e dati).
* **Gestione I/O**: informazioni sui file aperti, dispositivi in uso, eventuali operazioni di input/output in corso.
* **Scheduling**: dati utilizzati dallo scheduler, come la priorità, il tempo CPU accumulato e la posizione del processo nelle varie code (ready, blocked, ecc.).
* **Collegamenti**: riferimenti a processi padre e figli, o ad altri processi con cui è in relazione.

In sostanza, il PCB permette al sistema operativo di “congelare” un processo (salvando il suo contesto) e poi riprenderlo in seguito esattamente dal punto in cui era stato interrotto.

---

## 🔹 2. Stati del processo

Un processo non rimane sempre nello stesso stato: durante la sua vita attraversa diverse fasi. Per descriverle in modo chiaro, la teoria dei sistemi operativi utilizza **modelli a stati**.

### 🔸 Modello a 2 stati

Il modello più semplice distingue soltanto tra:

* **Running**: il processo è in esecuzione, cioè occupa la CPU.
* **Not Running**: il processo esiste, ma non sta usando la CPU (potrebbe essere pronto o in attesa).

Questo modello, pur essendo intuitivo, è troppo riduttivo, perché non distingue le diverse situazioni in cui un processo può trovarsi quando non è in esecuzione.

---

### 🔸 Modello a 5 stati

È il modello standard, molto più usato perché descrive con precisione la realtà. I cinque stati principali sono:

1. **New** (nuovo): il processo è appena stato creato dal sistema operativo. In questa fase, il SO alloca le strutture necessarie, inizializza il PCB e prepara la memoria.
2. **Ready** (pronto): il processo è in memoria e ha tutto ciò che serve per essere eseguito, ma non può ancora partire perché la CPU è occupata da altri processi. È in attesa che lo scheduler gli assegni la CPU.
3. **Running** (in esecuzione): il processo sta effettivamente utilizzando la CPU e le sue istruzioni vengono eseguite.
4. **Blocked / Waiting** (bloccato / in attesa): il processo non può continuare perché aspetta il verificarsi di un evento esterno, ad esempio la conclusione di un’operazione di I/O. In questo stato non è pronto a usare la CPU.
5. **Exit / Terminated** (terminato): il processo ha completato la sua esecuzione o è stato terminato forzatamente.

È importante notare che un processo può passare a **Exit** non solo da *Running*, ma anche da *Ready* o *Blocked*, ad esempio se un altro processo lo “uccide” o se si verifica un errore irreversibile.

---

### 🔸 Stati sospesi

Nei sistemi operativi più evoluti esistono anche stati aggiuntivi legati al concetto di **sospensione**.
Quando la memoria principale è troppo piena o ci sono altre necessità, il SO può decidere di “parcheggiare” un processo sulla memoria secondaria (es. su disco), liberando spazio in RAM.

In questo caso abbiamo due sottostati:

* **Ready/Suspend**: processo pronto ma spostato su memoria secondaria.
* **Blocked/Suspend**: processo in attesa di un evento, ma anch’esso spostato fuori dalla RAM.

La sospensione è gestita dal **medium-term scheduler**, che decide quali processi togliere temporaneamente dalla memoria per ottimizzare le risorse.

---

## 🔹 3. Mappa PCB + Diagramma stati

### 📍 La mappa del PCB

Il PCB può essere visto come una tabella o una struttura a blocchi, in cui ogni sezione conserva una diversa tipologia di informazioni. Possiamo immaginarlo organizzato così:

* **Sezione di identificazione**: PID, PPID, UID, TID.
* **Sezione di stato**: stato del processo (ready, running, blocked, suspended, exit).
* **Sezione del processore**: registri, Program Counter, PSW, stack pointer.
* **Sezione di memoria**: puntatori alle tabelle di pagine o segmenti, aree di memoria allocate.
* **Sezione I/O**: dispositivi in uso, file aperti, buffer.
* **Sezione scheduling**: priorità, tempo CPU accumulato, posizione nelle code.
* **Sezione collegamenti**: riferimenti al processo padre, ai figli, o al gruppo di thread a cui appartiene.

---

### 📍 Il diagramma degli stati

Possiamo rappresentare graficamente gli stati del processo con un diagramma:

```text
   ┌─────────────┐
   │    NEW      │
   └──────┬──────┘
          │ Admit
          ▼
   ┌─────────────┐
   │   READY     │◄─────────────┐
   └───┬────▲────┘              │
       │    │                   │
 Dispatch  Event Occurs         │
       ▼    │                   │
   ┌─────────────┐   Timeout    │
   │  RUNNING    │──────────────┘
   └───┬────▲────┘
       │    │
   Event Wait │
       ▼    │ Release
   ┌─────────────┐
   │  BLOCKED    │
   └──────┬──────┘
          │
          ▼
   ┌─────────────┐
   │   EXIT      │
   └─────────────┘
```

* Le **transizioni** indicano come un processo si sposta da uno stato all’altro:

  * *Admit*: il SO accetta un nuovo processo e lo mette nello stato READY.
  * *Dispatch*: lo scheduler sceglie un processo READY e lo manda in RUNNING.
  * *Timeout*: se scade il quanto di tempo assegnato, il processo torna in READY.
  * *Event Wait*: se il processo richiede un evento (es. I/O), passa a BLOCKED.
  * *Event Occurs*: quando l’evento atteso si verifica, torna in READY.
  * *Release*: quando il processo termina, passa a EXIT.

Se aggiungiamo i **sospesi**, i nodi READY e BLOCKED si sdoppiano nelle versioni *Ready/Suspend* e *Blocked/Suspend*, collegate da transizioni che spostano i processi dalla memoria principale a quella secondaria e viceversa.
