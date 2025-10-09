# Memorie + Sistema Operativo

---

## 🔹 Introduzione generale

Ogni sistema di elaborazione si fonda su un principio fondamentale: **la CPU elabora i dati molto più rapidamente di quanto la memoria o i dispositivi esterni possano fornirli**.
Per garantire efficienza e continuità nell’esecuzione dei programmi, è necessario organizzare la memoria in **più livelli** con caratteristiche diverse di **velocità, costo e capacità**.

Parallelamente, il **Sistema Operativo (SO)** si occupa di **gestire e coordinare** l’uso di queste memorie, garantendo che i processi:

* abbiano accesso sicuro e controllato ai dati;
* possano convivere in memoria senza conflitti;
* ottimizzino l’uso delle risorse fisiche disponibili.

Comprendere la **gerarchia delle memorie** e il **ruolo del SO** nella loro gestione è la base per capire la logica di tutto il sistema informatico.

---

## 🔹 1. Gerarchia delle memorie

Il concetto di **gerarchia di memoria** nasce per conciliare tre fattori in conflitto:

1. **Velocità** (quanto rapidamente si accede ai dati),
2. **Costo per bit** (quanto costa realizzarla),
3. **Capacità** (quanti dati può contenere).

La regola generale è:

> più la memoria è vicina alla CPU → più è veloce → più è costosa → meno è capiente.

### Struttura a livelli

| Livello                | Tipo di memoria    | Tempo di accesso | Capacità   | Gestione               |
| ---------------------- | ------------------ | ---------------- | ---------- | ---------------------- |
| **L1 / L2 / L3**       | Cache              | nanosecondi      | KB–MB      | Hardware (trasparente) |
| **RAM**                | Memoria principale | decine di ns     | GB         | Sistema operativo      |
| **Memoria secondaria** | SSD / HDD          | millisecondi     | TB         | Sistema operativo      |
| **Memoria terziaria**  | Nastri, cloud      | secondi          | molto alta | Manuale / batch        |

---

## 🔹 2. Tipologie di memoria

### a) Memoria primaria

Include **cache e RAM**.
È **volatile**: il contenuto si perde allo spegnimento.
Contiene:

* i programmi in esecuzione,
* i dati attivi,
* le strutture di controllo del sistema operativo.

### b) Memoria secondaria

Comprende **dischi magnetici** e **unità a stato solido (SSD)**.
Non è volatile e serve per **conservare permanentemente** programmi e dati.

### c) Memoria terziaria e virtuale

Usata per backup o archiviazione (nastri, cloud, optical storage).
La **memoria virtuale** è una tecnica logica del SO che permette di **estendere la memoria principale** utilizzando parte del disco (swap area).

---

## 🔹 3. Memoria cache

La **cache** è una memoria ad altissima velocità che funge da **ponte tra CPU e RAM**, riducendo il tempo medio di accesso ai dati.

### Principio di località

La cache sfrutta due proprietà fondamentali dei programmi:

* **Località temporale:** se un dato è stato usato di recente, probabilmente sarà usato di nuovo.
* **Località spaziale:** se è stato usato un dato in memoria, probabilmente saranno usati anche quelli vicini.

### Organizzazione

I dati vengono trasferiti in blocchi chiamati **linee di cache**.
Ogni linea contiene una copia di una parte di memoria principale.
Quando la CPU richiede un indirizzo:

1. Se il dato è già in cache → **cache hit** (accesso veloce).
2. Se non è presente → **cache miss** (dato recuperato dalla RAM).

### Politiche di scrittura

* **Write-through:** ogni modifica in cache viene immediatamente scritta in RAM.
  → più sicura ma lenta.
* **Write-back:** la scrittura in RAM avviene solo quando il blocco viene rimpiazzato.
  → più veloce, ma richiede coerenza.

---

## 🔹 4. Mappatura e sostituzione in cache

### Tipi di mappatura

| Tipo                                       | Descrizione                                             | Caratteristica                     |
| ------------------------------------------ | ------------------------------------------------------- | ---------------------------------- |
| **Diretta**                                | Ogni blocco di memoria mappa in una sola linea di cache | semplice ma può generare conflitti |
| **Associativa**                            | Un blocco può occupare qualsiasi linea                  | flessibile ma costosa              |
| **Associativa a gruppi (set-associative)** | Compromesso: la cache è divisa in gruppi di linee       | bilanciamento prestazioni/costo    |

### Politiche di rimpiazzo

Quando la cache è piena e serve spazio:

* **LRU (Least Recently Used):** elimina il blocco usato meno di recente.
* **FIFO (First In First Out):** elimina il blocco più vecchio.
* **Random:** scelta casuale, semplice ma non ottimale.

---

## 🔹 5. Ruolo del Sistema Operativo nella memoria

Il SO **non gestisce direttamente la cache** (controllata dall’hardware), ma ha il pieno controllo su:

* **Memoria principale (RAM)**
  → allocazione e rilascio per i processi.
* **Memoria secondaria (swap)**
  → gestione della memoria virtuale.
* **Protezione**
  → impedisce che un processo acceda alla memoria di un altro.

### Meccanismi principali

1. **Rilocazione dinamica:** traduzione indirizzi logici → fisici.
2. **Protezione:** verifica degli indirizzi validi per ogni processo.
3. **Condivisione:** possibilità di usare la stessa area di memoria (es. librerie condivise).
4. **Organizzazione logica:** gestione dello spazio degli indirizzi dei processi.
5. **Organizzazione fisica:** mappatura su memoria e swap.

---

## 🔹 6. Struttura logica del Sistema Operativo

Il sistema operativo può essere visto come un insieme di **moduli cooperanti**, organizzati a livelli di astrazione.

### a) Kernel

È il **cuore del sistema operativo**, sempre residente in memoria.
Si occupa di:

* Gestione dei processi e scheduling.
* Gestione della memoria principale e virtuale.
* Gestione del file system.
* Gestione delle interruzioni e dei dispositivi.

### b) Shell e interfaccia utente

Fornisce i mezzi per interagire con il sistema operativo (prompt, GUI, comandi).
È un **programma utente privilegiato**, ma non parte del kernel.

### c) Livelli di astrazione del SO

| Livello                      | Funzione principale                |
| ---------------------------- | ---------------------------------- |
| **1 – Hardware**             | CPU, memoria, dispositivi fisici   |
| **2 – Microkernel / Kernel** | Gestione risorse di base           |
| **3 – Servizi di sistema**   | File system, I/O, processi         |
| **4 – Librerie e API**       | Interfaccia per i programmi utente |
| **5 – Utente / Shell**       | Interazione e comandi              |

In sistemi didattici o teorici, la stratificazione può arrivare fino a 13 livelli (da hardware fino all’utente finale), dove ogni livello offre servizi a quello superiore e si appoggia su quello inferiore.

---

## 🔹 7. Kernel vs Microkernel

### Kernel monolitico

Tutte le funzioni (file system, driver, memoria, I/O, ecc.) sono integrate in un unico grande blocco eseguibile in modalità kernel.

* **Pro:** alte prestazioni, accesso diretto alle risorse.
* **Contro:** scarsa modularità, manutenzione difficile, vulnerabile a crash globali.

### Microkernel

Contiene solo le funzioni essenziali (gestione processi, memoria, comunicazione).
Tutto il resto (driver, file system, GUI) gira in **user mode** come processi separati.

* **Pro:** alta affidabilità e isolamento dei moduli.
* **Contro:** comunicazioni più lente (messaggi inter-processo).

Esempi:

* Kernel monolitici → Linux, BSD.
* Microkernel → MINIX, Mach (base di macOS).

---

## 🧠 Mappa concettuale di sintesi

```plaintext
MEMORIE + SISTEMA OPERATIVO
│
├── Gerarchia delle memorie
│   ├─ Cache → veloce, costosa, piccola
│   ├─ RAM → principale, volatile
│   ├─ Disco → secondaria, persistente
│   └─ Terziaria → backup, archiviazione
│
├── Cache
│   ├─ Località temporale e spaziale
│   ├─ Write-through / write-back
│   ├─ Mappatura → diretta, associativa, set-associativa
│   └─ Rimpiazzo → LRU, FIFO, Random
│
├── Ruolo del SO
│   ├─ Gestione RAM e swap
│   ├─ Rilocazione e protezione
│   ├─ Condivisione e organizzazione logica
│   └─ Memoria virtuale
│
├── Struttura del SO
│   ├─ Kernel → gestione risorse
│   ├─ Shell → interfaccia utente
│   └─ Livelli (1–5 o fino a 13)
│
└── Kernel vs Microkernel
    ├─ Monolitico → veloce, poco modulare
    └─ Microkernel → affidabile, più lento
```
