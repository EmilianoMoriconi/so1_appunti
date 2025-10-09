# Gestione della memoria (II)

## 🔹 Introduzione

Le tecniche di **partizionamento fisso o variabile** viste in precedenza rappresentano i primi metodi di gestione della memoria multiprogrammata, ma hanno un limite evidente:
non permettono di eseguire programmi più grandi della memoria fisica disponibile.

Per superare questa restrizione nasce il concetto di **memoria virtuale**, una tecnica che consente di **astrarre la memoria logica da quella fisica**, permettendo ai processi di “vedere” uno spazio di indirizzi molto più ampio di quello realmente presente nella RAM.

---

## 🔹 1. Memoria virtuale

La **memoria virtuale** è un meccanismo che consente l’esecuzione di processi anche se **solo una parte del loro codice o dei loro dati è effettivamente in memoria**.
Le porzioni non necessarie vengono mantenute su disco (spazio di swap) e caricate solo quando richieste.

### Obiettivi principali

* **Aumentare l’utilizzo della CPU:** i processi non restano in attesa di caricamento completo.
* **Permettere programmi più grandi della RAM fisica.**
* **Isolare gli spazi di memoria dei processi:** ogni processo ha una vista logica indipendente.
* **Gestire automaticamente il caricamento e lo scaricamento delle pagine.**

---

## 🔹 2. Paging

Il **paging** è la tecnica più diffusa per implementare la memoria virtuale.
Consiste nel suddividere la memoria (sia logica che fisica) in **blocchi di dimensione fissa**.

### Concetti fondamentali

* **Pagina (Page):** unità logica di memoria (spazio del processo).
* **Frame:** blocco fisico di memoria (spazio RAM).
* Le dimensioni di pagina e frame sono identiche (tipicamente 4 KB, 8 KB, 16 KB).

Il sistema operativo mantiene una **mappa di corrispondenza** tra pagine logiche e frame fisici, contenuta nella **Page Table** (tabella delle pagine).

### Funzionamento

1. Ogni indirizzo logico è composto da due parti:

   ```plaintext
   [numero di pagina | offset]
   ```

   * Il numero di pagina identifica quale pagina logica viene utilizzata.
   * L’offset indica la posizione all’interno della pagina.

2. L’MMU, tramite la **Page Table**, traduce il numero di pagina nel **numero di frame** corrispondente:

   ```plaintext
   indirizzo fisico = base frame + offset
   ```

3. Se la pagina non si trova in memoria (page fault), viene caricata dal disco nello spazio libero.

### Vantaggi del paging

* Evita la **frammentazione esterna**, poiché i frame sono di dimensione fissa.
* Consente la **rilocazione dinamica** e la **protezione per pagina**.
* Permette **memoria virtuale più ampia** della fisica.

### Svantaggi

* **Frammentazione interna:** l’ultima pagina di un processo potrebbe non essere completamente utilizzata.
* **Overhead di traduzione:** ogni accesso richiede consultare la tabella delle pagine.

---

## 🔹 3. Page Table (Tabella delle pagine)

La **Page Table** è una struttura dati fondamentale che associa ogni pagina logica a un frame fisico.
Ogni processo ha la propria tabella delle pagine.

### Contenuto di ogni voce (entry)

| Campo                  | Descrizione                                                |
| ---------------------- | ---------------------------------------------------------- |
| **Frame number**       | Numero del frame fisico associato alla pagina              |
| **Present bit**        | Indica se la pagina è attualmente in memoria               |
| **Modified/Dirty bit** | Indica se la pagina è stata modificata (serve per lo swap) |
| **Access bit**         | Usato per implementare politiche di rimpiazzo              |
| **Protection bits**    | Specificano i permessi (lettura, scrittura, esecuzione)    |

---

### Accesso alla Page Table

L’accesso alla Page Table introduce un **problema di prestazioni**, perché per ogni operazione di lettura/scrittura su memoria si dovrebbero fare **due accessi**:

1. Uno alla Page Table per ottenere l’indirizzo fisico.
2. Uno alla memoria effettiva per leggere/scrivere i dati.

Per ridurre questo overhead, si introduce una cache hardware dedicata: la **TLB**.

---

## 🔹 4. Translation Lookaside Buffer (TLB)

La **TLB (Translation Lookaside Buffer)** è una **cache interna alla MMU** che memorizza le traduzioni recenti tra pagine logiche e frame fisici.
Il suo scopo è **velocizzare la traduzione degli indirizzi**.

### Funzionamento

1. Quando un processo genera un indirizzo logico, l’MMU controlla prima nella TLB:

   * Se la traduzione è presente (**TLB hit**) → l’indirizzo fisico è immediatamente disponibile.
   * Se non è presente (**TLB miss**) → viene consultata la Page Table, e la traduzione viene poi memorizzata nella TLB.

2. La TLB ha dimensioni ridotte (tipicamente da 16 a 512 voci) e viene gestita con politiche di rimpiazzo simili a quelle della cache (LRU, FIFO).

### Vantaggi

* Riduce drasticamente il tempo medio di accesso alla memoria.
* Migliora le prestazioni della memoria virtuale senza modificare la logica di paging.

### Svantaggi

* Costo hardware elevato.
* Necessità di aggiornamento in caso di cambio di contesto (ogni processo ha la propria Page Table → invalidazione TLB).

---

## 🔹 5. Paging multilivello

Per processi molto grandi, la Page Table può diventare **enorme**.
Esempio: uno spazio di indirizzamento logico di 32 bit con pagine da 4 KB → 2²⁰ voci per tabella (oltre 4 MB per processo).

Per ridurre l’uso di memoria, si utilizza la **Page Table multilivello**, che suddivide la tabella in più parti.

### Funzionamento

1. L’indirizzo logico è diviso in più campi:

   ```plaintext
   [indice livello 1 | indice livello 2 | offset]
   ```
2. Solo i livelli necessari vengono mantenuti in memoria (gli altri possono restare su disco).
3. In sistemi a 64 bit, si usano fino a **4 o 5 livelli** di tabelle (es. x86-64 con PML4, PDPT, PD, PT).

### Vantaggi

* Riduce l’uso di memoria per le tabelle.
* Supporta grandi spazi di indirizzamento (64 bit).
* Pagina le Page Table stesse (memoria virtuale ricorsiva).

### Svantaggi

* Aumenta la complessità hardware e i tempi di traduzione (più accessi successivi).
* Compensato dalla presenza della TLB.

---

## 🔹 6. Segmentazione

Il **paging** divide la memoria in blocchi di dimensione fissa, ma alcuni programmi sono più naturalmente suddivisi in **unità logiche di dimensione variabile** (funzioni, stack, heap, moduli).
Per questo nasce la **segmentazione**.

### Concetto

La segmentazione suddivide la memoria logica in **segmenti** distinti, ciascuno con **un significato logico** (es. codice, dati, stack).

Ogni indirizzo logico è composto da:

[
\text{<numero segmento, offset>}
]

### Struttura hardware

Il sistema mantiene una **Segment Table**, in cui ogni voce contiene:

| Campo          | Descrizione                             |
| -------------- | --------------------------------------- |
| **Base**       | Indirizzo fisico di inizio del segmento |
| **Limit**      | Dimensione del segmento                 |
| **Protezione** | Permessi di accesso                     |

### Vantaggi

* Maggiore **modularità e sicurezza** (ogni segmento può essere protetto).
* Più adatta ai linguaggi ad alto livello (mappa direttamente funzioni e strutture dati).
* Facile condivisione di segmenti comuni (es. librerie condivise).

### Svantaggi

* **Frammentazione esterna** (i segmenti sono di dimensione variabile).
* Complessità di gestione rispetto al paging puro.

---

## 🔹 7. Segmentazione con Paging (ibrido)

I sistemi moderni (es. **x86**) combinano **segmentazione** e **paging**, sfruttando i vantaggi di entrambi.

### Funzionamento

1. Ogni segmento ha la propria tabella delle pagine.
2. L’indirizzo logico diventa:

   ```plaintext
   [segmento | pagina | offset]
   ```

3. Il segmento fornisce la base logica, mentre il paging gestisce la mappatura fisica.

### Vantaggi

* Flessibilità e modularità della segmentazione.
* Efficienza e assenza di frammentazione esterna del paging.

### Svantaggi

* Aumento dell’overhead di traduzione (più livelli da risolvere).
* Implementazione hardware più complessa.

---

## 🧠 Mappa concettuale di sintesi

```plaintext
GESTIONE DELLA MEMORIA (II)
│
├── Memoria virtuale
│   ├─ Spazio logico > spazio fisico
│   ├─ Swap su disco
│   └─ Caricamento su richiesta (page fault)
│
├── Paging
│   ├─ Pagine (logiche) ↔ Frame (fisici)
│   ├─ Page Table → mappa logico/fisico
│   └─ Frammentazione interna
│
├── Page Table
│   ├─ Frame, Present, Dirty, Access, Protection
│   ├─ Overhead di traduzione
│   └─ Soluzione → TLB
│
├── TLB
│   ├─ Cache hardware delle traduzioni
│   ├─ Hit/Miss
│   └─ Politiche di rimpiazzo
│
├── Paging multilivello
│   ├─ Page Table gerarchiche
│   ├─ Riduzione uso memoria
│   └─ Aumento tempi traduzione
│
├── Segmentazione
│   ├─ Unità logiche variabili
│   ├─ Segment Table (Base, Limit)
│   └─ Frammentazione esterna
│
└── Segmentazione + Paging
    ├─ Indirizzo = [segmento | pagina | offset]
    ├─ Flessibilità e protezione
    └─ Maggiore complessità
```