# Architettura monoprocessore

---

## 🔹 Introduzione

Un sistema di elaborazione monoprocessore è un sistema dotato di **una sola unità di controllo (CPU)**, responsabile dell’esecuzione sequenziale delle istruzioni di tutti i processi presenti nel sistema.
Tutti i meccanismi di esecuzione, gestione della memoria, I/O e scheduling ruotano attorno alla CPU, che costituisce il **cuore logico del computer**.

Il sistema operativo deve garantire che la CPU sia utilizzata in modo **efficiente** e **ordinato**, coordinando l’accesso alle sue risorse da parte dei processi.
Per comprendere il funzionamento di un sistema operativo, è quindi fondamentale capire **come è organizzata la CPU** e **come essa esegue un programma**.

---

## 🔹 1. Struttura generale della CPU

La **CPU (Central Processing Unit)** è composta da una serie di unità funzionali che cooperano per eseguire le istruzioni dei programmi.
Le tre macro-componenti principali sono:

1. **ALU (Arithmetic Logic Unit)**
   L’unità aritmetico-logica, che esegue le operazioni matematiche (addizione, sottrazione, moltiplicazione, divisione) e logiche (AND, OR, NOT, XOR).

2. **CU (Control Unit)**
   L’unità di controllo, che coordina le varie parti della CPU, interpreta le istruzioni e regola il flusso delle operazioni.
   È responsabile della **sequenza di esecuzione**: preleva le istruzioni dalla memoria, le decodifica e comanda l’ALU o altre unità.

3. **Registri interni**
   Piccole aree di memoria ad altissima velocità utilizzate per memorizzare temporaneamente dati, indirizzi o informazioni di controllo durante l’esecuzione.

---

## 🔹 2. Tipologie di registri

I registri rappresentano il livello più veloce e vicino alla CPU.
Ogni registro ha una funzione specifica e insieme formano la base della **microarchitettura del processore**.

### a) Registri utente

Sono utilizzati direttamente dai programmi per memorizzare dati intermedi o indirizzi.
Esempi tipici:

* **AX, BX, CX, DX** nei processori x86;
* **R0–R31** nei processori RISC (ARM, MIPS, ecc.).

Possono contenere:

* Operandi per le istruzioni aritmetiche.
* Risultati temporanei.
* Indirizzi di memoria (es. puntatori o indici di array).

### b) Registri di controllo e di stato

Non sono direttamente accessibili ai programmi utente: servono al **sistema operativo** e all’hardware per gestire l’esecuzione.

I principali sono:

* **Program Counter (PC)** → contiene l’indirizzo della prossima istruzione da eseguire.
* **Instruction Register (IR)** → mantiene l’istruzione attualmente in esecuzione.
* **Stack Pointer (SP)** → punta alla cima dello stack del processo.
* **Status Register / Flag Register** → contiene i flag (zero, carry, overflow, interrupt enable, ecc.) che indicano lo stato del processore.

### c) Registri interni (buffer)

Usati per collegare la CPU con la memoria e i dispositivi I/O:

* **MAR (Memory Address Register):** contiene l’indirizzo della cella di memoria da leggere o scrivere.
* **MBR (Memory Buffer Register):** contiene i dati letti o da scrivere in memoria.

---

## 🔹 3. Ciclo di esecuzione: Fetch–Decode–Execute

Ogni programma è composto da una sequenza di **istruzioni macchina** che la CPU deve eseguire.
Il processo con cui la CPU legge ed elabora le istruzioni è chiamato **ciclo di fetch–decode–execute**.

### a) Fase di Fetch (prelievo)

* Il **Program Counter (PC)** indica l’indirizzo della prossima istruzione in memoria.
* L’indirizzo viene copiato nel **MAR** e la CPU richiede la lettura alla memoria principale.
* L’istruzione viene caricata nel **Instruction Register (IR)**.
* Il PC viene incrementato (salvo istruzioni di salto).

### b) Fase di Decode (decodifica)

* L’unità di controllo interpreta il contenuto dell’IR e determina quale operazione deve essere eseguita.
* Vengono identificati gli operandi e le modalità di indirizzamento (diretto, indiretto, immediato, indicizzato...).

### c) Fase di Execute (esecuzione)

* L’ALU esegue l’operazione richiesta (aritmetica o logica).
* Se necessario, i risultati vengono scritti nei registri o in memoria.
* Viene aggiornato lo **Status Register** in base al risultato (es. flag di overflow o zero).

Questo ciclo si ripete continuamente, miliardi di volte al secondo, scandito dal **clock** del processore.

---

## 🔹 4. Modalità di indirizzamento

Le istruzioni macchina devono specificare **come accedere agli operandi** (cioè dove si trovano i dati).
Le modalità di indirizzamento più comuni sono:

| Modalità        | Descrizione                                                                          | Esempio            |
| --------------- | ------------------------------------------------------------------------------------ | ------------------ |
| **Immediato**   | L’operando è contenuto direttamente nell’istruzione                                  | `MOV R1, #5`       |
| **Diretto**     | L’istruzione contiene l’indirizzo effettivo del dato                                 | `MOV R1, (1000)`   |
| **Indiretto**   | L’istruzione contiene un riferimento a un registro che contiene l’indirizzo del dato | `MOV R1, (R2)`     |
| **Indicizzato** | L’indirizzo è ottenuto sommando un valore base e un indice                           | `MOV R1, (R2 + 4)` |

Le modalità di indirizzamento sono fondamentali perché permettono di gestire dati e istruzioni in modo flessibile, senza dover riscrivere codice per ogni indirizzo.

---

## 🔹 5. Ciclo di istruzione e ruolo del sistema operativo

Durante il ciclo di esecuzione, la CPU può essere **interrotta** da eventi esterni o interni (interrupt, eccezioni, trap).
Quando ciò accade:

1. La CPU sospende il ciclo in corso.
2. Salva lo stato corrente del processo (registri, PC, flag) nel PCB.
3. Passa al **kernel mode** e invoca il gestore dell’interrupt.
4. Dopo la gestione, ripristina il contesto e riprende l’esecuzione.

Questo meccanismo consente al sistema operativo di **coordinare processi multipli** anche su una singola CPU, simulando il parallelismo attraverso la **commutazione rapida del contesto (context switch)**.

---

## 🔹 6. Categorie di istruzioni macchina

Le istruzioni che una CPU può eseguire appartengono a diverse categorie, ognuna con scopi diversi:

| Categoria               | Esempio                   | Funzione                                       |
| ----------------------- | ------------------------- | ---------------------------------------------- |
| **Dati**                | `LOAD`, `STORE`, `MOV`    | Trasferimento dati tra memoria e registri      |
| **Aritmetiche/logiche** | `ADD`, `SUB`, `AND`, `OR` | Calcoli e operazioni bitwise                   |
| **Controllo di flusso** | `JMP`, `CALL`, `RET`      | Salti, chiamate a funzioni, ritorni            |
| **Gestione I/O**        | `IN`, `OUT`               | Comunicazione con dispositivi                  |
| **Sistema**             | `INT`, `HLT`              | Trap, interruzioni, arresti, cambi di modalità |

---

## 🔹 7. Interazione CPU – Memoria – I/O

La CPU non lavora isolata: per funzionare deve comunicare costantemente con:

* **la memoria principale (RAM)** per caricare istruzioni e dati;
* **i dispositivi di I/O** per leggere e scrivere dati.

Questa comunicazione avviene tramite **bus**:

1. **Bus dati** → trasporta i valori binari.
2. **Bus indirizzi** → indica dove leggere/scrivere.
3. **Bus di controllo** → gestisce segnali di sincronizzazione (read/write, interrupt, clock).

Il sistema operativo regola questo flusso e **decide quale processo può usare la CPU**, realizzando così il principio di **multiprogrammazione**.

---

## 🧠 Mappa concettuale di sintesi

```plaintext
ARCHITETTURA MONOPROCESSORE
│
├── Struttura CPU
│   ├─ ALU → esegue operazioni logico-aritmetiche
│   ├─ CU → coordina il ciclo istruzioni
│   └─ Registri → memorie veloci interne
│
├── Registri
│   ├─ Utente → dati e indirizzi
│   ├─ Controllo → PC, IR, SP, flag
│   └─ Interni → MAR, MBR per memoria
│
├── Ciclo istruzione
│   ├─ Fetch → prelievo
│   ├─ Decode → decodifica
│   └─ Execute → esecuzione ALU
│
├── Indirizzamento
│   ├─ Immediato, Diretto, Indiretto, Indicizzato
│   └─ Flessibilità e riuso codice
│
├── Interruzioni
│   ├─ Salvataggio contesto
│   ├─ Gestione kernel mode
│   └─ Context switch tra processi
│
├── Categorie istruzioni
│   ├─ Dati, Aritmetiche, Controllo, I/O, Sistema
│   └─ Funzioni operative della CPU
│
└── Comunicazione
    ├─ Bus dati / indirizzi / controllo
    └─ CPU–Memoria–I/O → multiprogrammazione
```
