# Gestione della memoria (I)

---

## 🔹 Introduzione

La **memoria centrale (RAM)** è una delle risorse più importanti e delicate di un sistema operativo, poiché costituisce il **luogo fisico dove vengono caricati i programmi** durante la loro esecuzione.
Il compito del sistema operativo è quello di **gestirla in modo efficiente, sicuro e flessibile**, consentendo la convivenza di più processi contemporaneamente senza che interferiscano tra loro.

La gestione della memoria deve garantire tre obiettivi fondamentali:

1. **Rilocazione** → permettere a un processo di essere spostato in memoria senza modificarne il codice.
2. **Protezione** → evitare che un processo acceda a zone di memoria appartenenti ad altri.
3. **Condivisione e uso efficiente** → sfruttare al massimo lo spazio disponibile minimizzando la frammentazione.

Inoltre, è necessario prevedere un meccanismo di **traduzione degli indirizzi logici in indirizzi fisici**, poiché ogni processo “vede” la memoria come se fosse un suo spazio indipendente, ma in realtà deve essere collocato da qualche parte nella RAM fisica.

---

## 🔹 1. Rilocazione

Ogni programma, quando viene compilato, genera **indirizzi logici** (o virtuali), che partono generalmente da 0.
Tuttavia, quando il programma viene caricato in memoria per l’esecuzione, **potrebbe non essere sempre possibile collocarlo nella stessa posizione fisica**.

### Concetto

La **rilocazione** è il meccanismo che permette di **trasformare gli indirizzi logici** generati dal programma negli **indirizzi fisici effettivi** utilizzati in memoria.
Questa traduzione può avvenire in diversi momenti:

#### 1. Rilocazione statica

Avviene **al momento del caricamento** del programma.
Il compilatore o il loader calcolano gli indirizzi fisici prima dell’esecuzione.
→ Il programma non può essere spostato durante l’esecuzione.

#### 2. Rilocazione dinamica

Avviene **durante l’esecuzione** del programma.
Gli indirizzi logici vengono tradotti in indirizzi fisici **a runtime** tramite hardware dedicato (es. MMU – *Memory Management Unit*).
→ Il processo può essere spostato in memoria senza doverlo ricompilare.

### Implementazione hardware

L’MMU gestisce due registri principali:

* **Registro base (Base Register)** → contiene l’indirizzo fisico iniziale dello spazio di memoria del processo.
* **Registro limite (Limit Register)** → indica la dimensione massima dello spazio del processo.

Ogni indirizzo logico generato dal programma viene tradotto come:

[
\text{Indirizzo fisico} = \text{Base} + \text{Indirizzo logico}
]

E viene controllato che non superi il valore di `Base + Limit`.

---

## 🔹 2. Protezione

La **protezione della memoria** serve a impedire che un processo possa **leggere o scrivere in aree non autorizzate**, preservando così l’integrità del sistema operativo e degli altri processi.

### Meccanismi di protezione

1. **Controllo hardware con registri base/limite:**
   Ogni accesso a memoria è verificato dalla MMU: se l’indirizzo logico esce dal range consentito, viene generata un’**eccezione (trap)** e il processo viene bloccato.

2. **Bit di protezione:**
   In sistemi più evoluti, ogni blocco o pagina di memoria può avere **bit che definiscono i permessi** (lettura, scrittura, esecuzione).
   → Utilizzato nei sistemi a memoria virtuale (es. `rwx` in Linux).

3. **Modalità utente e kernel:**
   La CPU lavora in due modalità operative:

   * **User mode:** accesso limitato solo alla memoria utente.
   * **Kernel mode:** accesso completo a tutte le aree di memoria.

   Il cambio di modalità avviene solo tramite **system call o interrupt**.

---

## 🔹 3. Partizionamento della memoria

Il partizionamento rappresenta uno dei primi approcci alla gestione della memoria multiprogrammata.
Consiste nel **suddividere la RAM in più blocchi (partizioni)** nei quali possono essere caricati diversi processi contemporaneamente.

### Tipi principali

#### 1. Partizionamento fisso (Fixed Partitioning)

La memoria viene divisa in **partizioni di dimensione predefinita** (uguale o diversa).
Ogni processo viene caricato in una partizione libera sufficientemente grande.

**Vantaggi:**

* Implementazione semplice.
* Buona protezione (ogni processo resta nella propria partizione).

**Svantaggi:**

* **Frammentazione interna:** se un processo non riempie la sua partizione, parte della memoria resta inutilizzata.
* Numero di processi limitato al numero di partizioni.
* Difficile adattarsi a programmi di dimensioni variabili.

---

#### 2. Partizionamento variabile (Dynamic Partitioning)

In questo approccio non ci sono partizioni fisse: la memoria viene **assegnata dinamicamente** in base alla dimensione del processo.

Quando un processo termina, la sua area viene liberata, ma ciò può generare **frammentazione esterna**, cioè spazi liberi non contigui e inutilizzabili singolarmente.

**Soluzioni possibili:**

* **Compattazione:** spostare i processi in modo da riunire le aree libere in un unico blocco (operazione costosa).
* **Allocazione con strategie specifiche:**

  * **First Fit:** assegna la prima area libera sufficientemente grande.
  * **Best Fit:** assegna l’area più piccola possibile che soddisfi la richiesta.
  * **Worst Fit:** assegna l’area più grande disponibile (per ridurre la frammentazione residua).

---

## 🔹 4. Buddy System

Il **Buddy System** è un metodo di allocazione della memoria che combina l’efficienza del partizionamento variabile con la semplicità del fisso.
È largamente usato nei sistemi moderni (incluso Linux) per gestire la memoria fisica.

### Funzionamento

L’idea è di dividere la memoria in blocchi di dimensione pari a potenze di 2.
Quando un processo richiede `n` byte, il sistema cerca il blocco più piccolo di potenza di 2 che possa contenerlo.

#### Allocazione

1. Se il blocco disponibile è troppo grande, viene **diviso in due metà (buddies)** di uguale dimensione.
2. Il processo viene collocato in uno dei due.
3. Le suddivisioni continuano finché non si trova un blocco sufficientemente piccolo.

#### Deallocazione

Quando il processo termina, il blocco viene liberato e, se il suo “buddy” adiacente è anch’esso libero, i due vengono **riuniti** (merge).
In questo modo il sistema riduce la frammentazione e riutilizza in modo efficiente la memoria.

### Vantaggi

* Riduce la **frammentazione esterna**.
* Supporta facilmente la **compattazione dinamica**.
* Implementazione semplice con operazioni binarie.

### Svantaggi

* Possibile **frammentazione interna** (se la richiesta non è esattamente una potenza di 2).
* Gli split e merge frequenti possono introdurre **overhead di gestione**.

---

## 🔹 5. Considerazioni generali

Ogni tecnica di gestione della memoria rappresenta un compromesso tra **flessibilità**, **efficienza** e **overhead di gestione**.
Sistemi moderni utilizzano combinazioni di più tecniche (es. buddy system per la memoria fisica + paging per quella virtuale).

---

## 🧠 Mappa concettuale di sintesi

```plaintext
GESTIONE DELLA MEMORIA (I)
│
├── Obiettivi
│   ├─ Rilocazione → indirizzi logici → fisici
│   ├─ Protezione → accessi controllati
│   └─ Uso efficiente → frammentazione minima
│
├── Rilocazione
│   ├─ Statica → traduzione al caricamento
│   ├─ Dinamica → traduzione runtime (MMU)
│   └─ Base + Limit Register
│
├── Protezione
│   ├─ Registri base/limite
│   ├─ Bit di protezione (rwx)
│   └─ Modalità user/kernel
│
├── Partizionamento
│   ├─ Fisso → frammentazione interna
│   ├─ Variabile → frammentazione esterna
│   │   └─ Strategie: First Fit, Best Fit, Worst Fit
│
└── Buddy System
    ├─ Blocchi in potenze di 2
    ├─ Split / Merge dinamico
    ├─ Vantaggi → meno frammentazione
    └─ Svantaggi → overhead e sprechi
```
