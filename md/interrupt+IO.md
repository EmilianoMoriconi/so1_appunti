# Interrupt e I/O

---

## 🔹 Introduzione

Un sistema operativo deve essere in grado di **gestire eventi asincroni** provenienti sia dall’hardware sia dal software, garantendo che la CPU non rimanga inattiva e che il flusso di esecuzione dei programmi proceda in modo corretto.
Questo comportamento è reso possibile grazie agli **interrupt**, meccanismi che permettono al processore di **interrompere temporaneamente l’esecuzione di un programma** per gestire un evento più urgente.

Gli interrupt sono quindi il **mezzo fondamentale di comunicazione tra CPU, sistema operativo e periferiche di I/O**.
Capire come funzionano significa comprendere il cuore del meccanismo reattivo del sistema operativo.

---

## 🔹 1. Concetto di interrupt

Un **interrupt** è un segnale che richiede al processore di sospendere l’attività corrente e di passare temporaneamente all’esecuzione di una **routine di servizio** (Interrupt Handler o Interrupt Service Routine, ISR).
Dopo aver gestito l’evento, il processore **riprende esattamente dal punto in cui era stato interrotto**.

Questo meccanismo permette al sistema di:

* reagire rapidamente a eventi esterni (es. arrivo dati da tastiera o rete);
* gestire errori o eccezioni interne;
* evitare che la CPU sprechi tempo in attesa di dispositivi lenti.

---

## 🔹 2. Tipologie di interrupt

Gli interrupt si classificano in base all’origine e alla modalità di generazione.

### a) Interrupt hardware

Generati dai dispositivi esterni per segnalare eventi come:

* completamento di un’operazione di I/O;
* errori hardware;
* richieste da timer o dispositivi di rete.

Esempio:
una stampante invia un segnale di interrupt per indicare che ha terminato la stampa.

### b) Interrupt software

Generati da istruzioni specifiche del programma (es. `INT n` su x86) o da **eccezioni** come divisione per zero o accesso a memoria non valida.
Sono utilizzati dal sistema operativo per gestire le **system call** e i **trap**.

### c) Classificazione funzionale

| Tipo          | Origine                               | Esempi                 | Descrizione                           |
| ------------- | ------------------------------------- | ---------------------- | ------------------------------------- |
| **Sincroni**  | Durante l’esecuzione di un’istruzione | Trap, eccezioni, fault | Dipendono dal programma in corso      |
| **Asincroni** | Da eventi esterni alla CPU            | Timer, I/O completato  | Indipendenti dal flusso di istruzioni |

---

## 🔹 3. Meccanismo di gestione di un interrupt

Quando si verifica un interrupt, la CPU esegue una sequenza precisa di operazioni per garantire che l’intervento sia gestito in modo sicuro e coerente.

### Fasi principali

1. **Rilevamento dell’interrupt**
   Il processore verifica a ogni ciclo di clock se è presente un segnale di interrupt attivo.

2. **Salvataggio del contesto**
   La CPU salva in modo automatico le informazioni necessarie per riprendere il processo interrotto:

   * Program Counter (PC)
   * Registri di stato
   * Altri registri generali (salvati dal kernel o dall’handler)

3. **Cambio di modalità**
   La CPU passa da **user mode** a **kernel mode** per poter eseguire istruzioni privilegiate.

4. **Identificazione della causa**
   Tramite la **tabella vettore degli interrupt**, la CPU individua quale evento ha generato l’interrupt e salta alla **Interrupt Service Routine** corrispondente.

5. **Esecuzione dell’handler**
   L’ISR gestisce l’evento (es. legge un dato dal dispositivo, aggiorna un buffer, segnala la fine dell’I/O).

6. **Ripristino del contesto**
   Dopo la gestione, il sistema ripristina lo stato precedente del processo e ritorna al punto esatto in cui era stato interrotto.

---

## 🔹 4. Vettore degli interrupt

Ogni tipo di interrupt è associato a una specifica **voce del vettore degli interrupt**, una tabella contenente gli indirizzi delle routine di servizio.

Esempio (semplificato):

| Codice | Sorgente interrupt       | Routine associata |
| ------ | ------------------------ | ----------------- |
| 0      | Divisione per zero       | `ISR_DIVZERO`     |
| 8      | Timer                    | `ISR_TIMER`       |
| 13     | Violazione di protezione | `ISR_PROTFAULT`   |
| 33     | Tastiera                 | `ISR_KEYBOARD`    |

Quando l’interrupt viene rilevato, la CPU accede direttamente alla voce corrispondente del vettore e salta alla funzione associata.

---

## 🔹 5. Gestione sequenziale e annidata degli interrupt

### a) Gestione sequenziale

In modalità **sequenziale**, la CPU accetta un nuovo interrupt solo quando ha terminato di gestire quello corrente.
→ soluzione semplice, ma poco efficiente per sistemi con eventi frequenti.

### b) Gestione annidata

In modalità **annidata**, un interrupt può essere interrotto da un altro di **priorità superiore**.
Serve una **priorità gerarchica** per evitare conflitti e perdita di eventi.

Esempio:

* Un interrupt della tastiera può interrompere un processo in esecuzione.
* Ma un interrupt del timer (più urgente) può a sua volta interrompere l’handler della tastiera.

Il kernel gestisce una **maschera di priorità** per abilitare o disabilitare certi interrupt in momenti specifici.

---

## 🔹 6. Context switch e interrupt

Ogni interrupt implica un **context switch** temporaneo:
la CPU deve salvare lo stato del processo corrente per poterlo ripristinare successivamente.

Questo meccanismo è analogo a quello utilizzato dallo **scheduler** per passare da un processo all’altro, ma:

* nel caso dello scheduler → il cambio è pianificato (es. time quantum scaduto);
* nel caso dell’interrupt → è **improvviso e asincrono**.

Un interrupt quindi **non solo segnala un evento**, ma è anche **il meccanismo tecnico con cui il kernel ottiene il controllo della CPU**.

---

## 🔹 7. Tecniche di I/O

Le operazioni di I/O (Input/Output) rappresentano la comunicazione tra CPU e dispositivi periferici.
Poiché i dispositivi sono molto più lenti della CPU, il sistema deve adottare tecniche che massimizzino l’efficienza.

### a) I/O programmato

La CPU interroga continuamente il dispositivo (polling) fino a che non è pronto.
→ semplice ma inefficiente: la CPU resta bloccata in attesa.

### b) I/O con interrupt

Il dispositivo genera un interrupt quando è pronto o ha completato un’operazione.
→ la CPU nel frattempo può eseguire altri processi.
→ metodo standard nei sistemi moderni.

### c) I/O con DMA (Direct Memory Access)

Un **DMA controller** trasferisce i dati direttamente tra memoria e dispositivo, senza intervento della CPU per ogni byte.
→ riduce drasticamente l’overhead della CPU.
→ usato per dischi, schede di rete e audio.

---

## 🔹 8. Ruolo del sistema operativo negli interrupt e nell’I/O

Il sistema operativo gestisce gli interrupt come **porte di ingresso verso il kernel**:

* Decide **quali interrupt abilitare** (priorità, maschere).
* Fornisce le **routine ISR** appropriate.
* Coordina i **driver dei dispositivi** che interagiscono con l’hardware.
* Gestisce **code di I/O** e **sincronizzazione** dei processi in attesa.

L’insieme di queste funzioni costituisce il **sottosistema di I/O del kernel**, base della comunicazione CPU–dispositivi.

---

## 🧠 Mappa concettuale di sintesi

```plaintext
INTERRUPT E I/O
│
├── Concetto
│   ├─ Interruzione esecuzione CPU
│   ├─ Routine ISR → gestisce evento
│   └─ Ripresa del programma
│
├── Tipi
│   ├─ Hardware → dispositivi, timer
│   ├─ Software → trap, eccezioni
│   └─ Sincroni / Asincroni
│
├── Gestione
│   ├─ Rilevamento → segnale interrupt
│   ├─ Salvataggio contesto
│   ├─ Kernel mode + vettore interrupt
│   └─ Ripristino stato processo
│
├── Priorità
│   ├─ Sequenziale → uno per volta
│   └─ Annidata → priorità gerarchica
│
├── Tecniche I/O
│   ├─ Programmato → polling
│   ├─ Interrupt-driven → CPU libera
│   └─ DMA → accesso diretto a memoria
│
└── Ruolo SO
    ├─ Gestione ISR e driver
    ├─ Scheduling I/O
    └─ Interfaccia CPU–dispositivi
```
