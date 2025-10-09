# Storia dei Sistemi Operativi

---

## 🔹 Introduzione

I sistemi operativi non sono nati con i computer moderni: si sono **evoluti gradualmente** insieme all’hardware e alle esigenze dell’utenza.
Ogni nuova generazione di computer ha richiesto **soluzioni più efficienti per gestire il tempo di calcolo, la memoria e le periferiche**, portando alla nascita di modelli sempre più complessi di gestione dei processi.

Comprendere questa evoluzione permette di capire **perché oggi i sistemi operativi funzionano come li conosciamo** (multitasking, time-sharing, multiprocessore, ecc.), e su quali principi si basano i meccanismi che studiamo a livello tecnico.

---

## 🔹 1. Prima generazione: calcolo manuale e programmazione diretta (anni ’40 – primi ’50)

I primi calcolatori elettronici, come **ENIAC (1946)**, **EDSAC (1949)** e **UNIVAC (1951)**, non avevano un sistema operativo.
Ogni programma veniva **caricato manualmente** in memoria tramite **schede perforate, interruttori o nastri magnetici**, e controllato direttamente dall’operatore.

Caratteristiche principali:

* Nessuna multiprogrammazione: un solo programma alla volta.
* Input/Output gestiti manualmente.
* Il tempo della CPU spesso sprecato durante le operazioni I/O.

💡 **Obiettivo tecnico:** automatizzare il caricamento e l’esecuzione dei programmi per ridurre i tempi morti.

---

## 🔹 2. Seconda generazione: sistemi batch (anni ’50 – metà ’60)

Con l’introduzione dei **mainframe IBM 700 e 1400**, nacquero i **sistemi batch**.
I programmi non venivano più caricati manualmente, ma **raggruppati in lotti (batch)** e **gestiti automaticamente** dal sistema operativo.

### Funzionamento del sistema batch

1. L’operatore prepara un **nastro batch** contenente una sequenza di job.
2. Il **monitor residente** (precursore del kernel) carica ed esegue ogni job in sequenza.
3. Al termine, il controllo torna al monitor per passare al successivo.

### Caratteristiche

* **Esecuzione sequenziale non interattiva.**
* Il sistema si occupa di **caricare, eseguire e scaricare** i programmi automaticamente.
* La CPU resta attiva per la maggior parte del tempo → aumento dell’efficienza.

### Limiti

* Nessuna interazione utente.
* Se un job falliva, l’intera sequenza veniva interrotta.
* Impossibilità di correggere o osservare il comportamento del programma in tempo reale.

Esempio: **IBM 7094** con sistema **FMS (Fortran Monitor System)**, poi **IBSYS**.

---

## 🔹 3. Terza generazione: multiprogrammazione e time-sharing (anni ’60 – ’70)

Con l’introduzione dei **transistor** e dei primi **sistemi multiutente**, i computer divennero più potenti e si iniziò a pensare al calcolo **condiviso**.

### Multiprogrammazione

La CPU può **tenere più processi in memoria contemporaneamente**, alternandone l’esecuzione quando uno si blocca (es. per I/O).
→ Migliore utilizzo della CPU, riduzione dei tempi morti.

Il **sistema operativo gestisce il carico**, mantenendo una **ready queue** e passando da un processo all’altro tramite **scheduling e context switch**.

### Time-sharing

Evoluzione naturale della multiprogrammazione:
il tempo della CPU viene **suddiviso in quanti (time slice)** assegnati ciclicamente ai vari utenti o processi.

* Ogni utente percepisce di avere un computer dedicato.
* Nascono i **terminali interattivi**, con input da tastiera e output video.
* Compare la **preemption**, cioè la possibilità di interrompere un processo per assegnare la CPU a un altro.

### Sistemi rappresentativi

* **CTSS (Compatible Time Sharing System)** del MIT (1961).
* **MULTICS (Multiplexed Information and Computing Service)** (1965):
  → introduce concetti moderni come file system gerarchico, protezione, memoria virtuale.
  → da MULTICS nascerà **UNIX** (1970).

💡 Da qui derivano molti concetti base di tutti i sistemi moderni: processi, shell, file system, permessi e scheduling.

---

## 🔹 4. Quarta generazione: sistemi multiprocessore e distribuiti (anni ’80 – ’90)

L’aumento della potenza e la miniaturizzazione portarono alla diffusione dei **microprocessori** e dei **personal computer**.
Si cominciò a parlare di:

* **sistemi multiprocessore**, con più CPU che cooperano sullo stesso bus o su più core;
* **sistemi distribuiti**, con più macchine interconnesse in rete che condividono risorse.

### Caratteristiche principali

* Esecuzione parallela di processi su più CPU.
* Introduzione della **cache multipla** e della **coerenza della memoria**.
* Comunicazione tramite **reti locali (LAN)** e **protocolli TCP/IP**.
* Concetti di **trasparenza di rete** e **file system distribuito**.

### Sistemi notevoli

* UNIX (Berkeley BSD, System V).
* VAX/VMS, OS/2, Windows NT.
* Prime versioni di **Linux** (1991) come evoluzione open source del paradigma UNIX.

---

## 🔹 5. Quinta generazione: sistemi moderni e virtualizzazione (2000 – oggi)

Oggi i sistemi operativi gestiscono ambienti **ibridi, multipiattaforma e virtualizzati**, con risorse distribuite tra più macchine fisiche o virtuali.

### Tendenze moderne

* **Multicore e hyperthreading:** schedulazione su core logici paralleli.
* **Virtualizzazione:** esecuzione di più sistemi operativi su una singola macchina (VMware, KVM, Hyper-V).
* **Containerizzazione:** isolamento dei processi in ambienti leggeri (Docker, LXC).
* **Cloud computing:** risorse distribuite e scalabili su cluster remoti.
* **Sicurezza avanzata:** sandboxing, SELinux, controllo degli accessi, cifratura integrata.
* **Gestione energetica:** scheduling adattivo e gestione dei consumi per dispositivi mobili.

💡 Il principio fondante resta invariato: il SO deve **astrarre e gestire l’hardware**, fornendo un ambiente sicuro, efficiente e trasparente agli utenti e alle applicazioni.

---

## 🔹 6. Evoluzione dell’hardware e impatto sul SO

Ogni innovazione hardware ha determinato un’evoluzione corrispondente nel software di sistema:

| Innovazione hardware | Impatto sul sistema operativo             |
| -------------------- | ----------------------------------------- |
| Timer hardware       | Scheduling preemptive e time-sharing      |
| Interrupt controller | Gestione asincrona di eventi              |
| Memoria virtuale     | Separazione spazi utente e kernel         |
| Dischi e SSD         | File system complessi e caching           |
| Multiprocessori      | Scheduling parallelo, CPU affinity        |
| Virtualizzazione     | Gestione di macchine virtuali e container |

---

## 🔹 7. Timeline sintetica

| Periodo       | Caratteristiche                    | Esempi di sistemi       |
| ------------- | ---------------------------------- | ----------------------- |
| **1940–50**   | Nessun OS, programmazione manuale  | ENIAC, UNIVAC           |
| **1950–60**   | Sistemi batch                      | IBM 709, FMS            |
| **1960–70**   | Multiprogrammazione, time-sharing  | CTSS, MULTICS           |
| **1970–90**   | UNIX, multiprocessori, distribuiti | BSD, VAX/VMS            |
| **2000–oggi** | Virtualizzazione, cloud, mobile    | Linux, Windows, Android |

---

## 🧠 Mappa concettuale di sintesi

```plaintext
STORIA DEI SISTEMI OPERATIVI
│
├── 1ª generazione → nessun OS
│   └─ Programmazione manuale, ENIAC
│
├── 2ª generazione → sistemi batch
│   ├─ Lotti di job automatici
│   └─ Nessuna interazione utente
│
├── 3ª generazione → multiprogrammazione e time-sharing
│   ├─ Processi multipli in memoria
│   ├─ Scheduling, context switch
│   └─ Nascita di MULTICS e UNIX
│
├── 4ª generazione → multiprocessore e distribuiti
│   ├─ CPU multiple, rete, trasparenza
│   └─ UNIX, VMS, Linux
│
├── 5ª generazione → moderni e virtualizzati
│   ├─ Multicore, container, cloud
│   └─ Sicurezza e isolamento
│
└── Hardware ↔ Software
    ├─ Timer → scheduling
    ├─ Memoria virtuale → isolamento
    ├─ Multiprocessori → parallelismo
    └─ Virtualizzazione → risorse dinamiche
```
