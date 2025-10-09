# File System (II)

## 🔹 Introduzione

Dopo aver analizzato la struttura logica dei file system e i meccanismi di allocazione dei file, in questa lezione approfondiamo **la gestione dello spazio libero**, **le strutture dati interne (FAT e inode)**, e i meccanismi che garantiscono **l’integrità e la coerenza dei dati**, come **il journaling e la cache del disco**.

L’obiettivo del file system è non solo memorizzare i dati, ma **preservarli in modo sicuro e coerente** anche in caso di crash o spegnimenti improvvisi, mantenendo buone prestazioni di accesso.

---

## 🔹 1. Gestione dello spazio libero

Ogni file system deve gestire **l’insieme dei blocchi liberi** del disco, in modo da poterli assegnare ai file che crescono o ai nuovi file creati.
La scelta della tecnica influenza fortemente la **velocità di allocazione**, l’**uso efficiente dello spazio** e la **facilità di recupero** in caso di errore.

### Tecniche principali

#### a) Bitmap (mappa dei bit)

Il disco è rappresentato da una sequenza di **bit**, uno per ogni blocco:

* `1` → blocco occupato
* `0` → blocco libero

**Vantaggi:**

* Ricerca rapida di blocchi liberi (si possono usare istruzioni bitwise).
* Struttura compatta (es. 1 bit per 4 KB → 128 KB di bitmap per 1 TB di disco).
* Facile salvataggio e aggiornamento.

**Svantaggi:**

* Serve scansionare la bitmap per trovare gruppi contigui di blocchi (per file grandi).
* Se frammentata, le prestazioni di lettura peggiorano.

---

#### b) Lista concatenata di blocchi liberi (Linked free list)

Tutti i blocchi liberi sono collegati tra loro tramite puntatori: ogni blocco libero contiene l’indirizzo del successivo.

**Vantaggi:**

* Implementazione semplice.
* Non serve una tabella separata in memoria.

**Svantaggi:**

* Accesso lento (deve attraversare l’intera lista).
* Se un blocco della lista si danneggia → perdita di collegamento a tutti i blocchi successivi.

---

#### c) Gruppi di blocchi liberi (Grouping)

Usata in alcuni file system UNIX:
ogni blocco libero contiene **indirizzi di più blocchi liberi** (un piccolo array di puntatori), e l’ultimo puntatore rimanda al gruppo successivo.

→ Compromesso tra lista concatenata e bitmap: riduce il numero di accessi per individuare nuovi blocchi.

---

#### d) Contatori (Counting)

Usata quando più blocchi liberi sono consecutivi:
invece di elencarli tutti, si memorizza una coppia `(indirizzo iniziale, quantità)`.

**Esempio:**
(200, 5) → blocchi liberi 200–204.

**Vantaggi:**

* Ideale per file system che liberano interi segmenti di blocchi insieme.
* Molto compatta.

---

## 🔹 2. Strutture dati interne: FAT e inode

### a) FAT – *File Allocation Table*

Usata nei file system della famiglia **MS-DOS, FAT16, FAT32**.

La FAT è una **grande tabella** in cui ogni voce corrisponde a un blocco del disco e contiene:

* `0` → blocco libero
* `EOF` → ultimo blocco del file
* valore `x` → blocco successivo nella catena del file

Il sistema tiene una sola copia (o due per sicurezza) della tabella FAT all’inizio del disco.

**Esempio:**

```
Blocco 5 → 9
Blocco 9 → 13
Blocco 13 → EOF
```

Significa che il file occupa i blocchi 5 → 9 → 13.

**Vantaggi:**

* Implementazione semplice.
* Facile navigazione sequenziale dei file.
* Indipendente dal tipo di dispositivo.

**Svantaggi:**

* Tutta la tabella deve risiedere in memoria → poco scalabile per dischi grandi.
* Accesso casuale costoso (bisogna attraversare la catena).
* Facilmente danneggiabile (la corruzione della FAT può compromettere tutto il file system).

---

### b) inode (UNIX / Linux)

Ogni file è descritto da un **inode**, che contiene tutte le informazioni di gestione e i puntatori ai blocchi di dati.

Come visto, l’inode mantiene:

* **Puntatori diretti** → fino a 12 blocchi dati immediati
* **Puntatori indiretti singoli, doppi, tripli** → strutture ricorsive che permettono di raggiungere file molto grandi

**Esempio tipico (ext4):**

| Tipo di puntatore   | Descrizione                                       | Copertura approssimata |
| ------------------- | ------------------------------------------------- | ---------------------- |
| 12 diretti          | Puntano direttamente ai blocchi dati              | File piccoli (~48 KB)  |
| 1 indiretto singolo | Puntatore a blocco contenente altri indirizzi     | ~4 MB                  |
| 1 indiretto doppio  | Puntatore a blocchi di indirizzi di altri blocchi | ~4 GB                  |
| 1 indiretto triplo  | Puntatore a blocchi di indirizzi di indirizzi     | ~4 TB                  |

Questo approccio rende gli inode **flessibili e scalabili**, ma introduce un **overhead maggiore** per i file di grandi dimensioni (più accessi a livelli intermedi).

---

## 🔹 3. Gestione dello spazio libero e allocazione combinata

I file system moderni (es. ext4, NTFS, APFS, XFS) combinano più tecniche per **massimizzare efficienza e integrità**:

* **Bitmap per lo spazio libero** → rapida individuazione blocchi.
* **Inode o strutture indicizzate** → gestione efficiente dei file.
* **Allocazione per estensioni (extent)** → blocchi contigui trattati come un’unica unità logica (riduce frammentazione e overhead).

### Extent

Un **extent** rappresenta una sequenza contigua di blocchi fisici assegnati a un file.
Invece di memorizzare ogni blocco singolo, l’inode memorizza `(blocco_inizio, lunghezza)`.

**Vantaggi:**

* Migliore località spaziale (file più compatti sul disco).
* Meno frammentazione e minore overhead nella tabella degli indici.

**Usato in:** ext4, XFS, NTFS, Btrfs.

---

## 🔹 4. Journaling e coerenza del file system

Uno dei problemi principali dei file system tradizionali è la **perdita di coerenza** in caso di crash (es. interruzione di corrente durante la scrittura).
Il **journaling** è un meccanismo che registra **le operazioni imminenti su un’area speciale del disco (journal)** prima di eseguirle realmente.

### Funzionamento

1. Ogni operazione (creazione, eliminazione, modifica) viene **scritta nel journal** come transazione.
2. Solo dopo la conferma della scrittura nel journal, l’operazione viene **eseguita sui dati reali**.
3. Se il sistema si blocca prima del completamento, al riavvio il file system **legge il journal** e:

   * applica le operazioni non ancora completate, oppure
   * le annulla per mantenere la consistenza.

### Tipi di journaling

* **Write-ahead logging:** scrive prima nel journal, poi nei blocchi dati (metodo standard).
* **Ordered journaling:** prima i dati, poi i metadati (usato in ext3/ext4).
* **Full data journaling:** registra anche i contenuti dei file (massima sicurezza, ma rallenta).

### Vantaggi

* Riduce drasticamente i tempi di recupero dopo crash.
* Garantisce la **consistenza dei metadati**.
* Evita la necessità di eseguire lo scan completo del disco (come `fsck`).

### Svantaggi

* Overhead in scrittura (ogni operazione viene duplicata).
* Journal stesso può frammentarsi nel tempo.

---

## 🔹 5. Cache del disco e buffering

Per migliorare le prestazioni, il sistema operativo utilizza **buffer in memoria** per evitare accessi frequenti e lenti al disco.
Questa tecnica è gestita dal **buffer cache** o **page cache** del kernel.

### Tipologie di cache

1. **Read cache:**
   Le pagine lette dal disco vengono mantenute in RAM; se lo stesso file viene letto di nuovo, l’accesso è immediato.

2. **Write-back cache:**
   Le scritture non vengono eseguite subito sul disco ma accumulate e scritte periodicamente o al rilascio del file.

3. **Write-through cache:**
   Ogni scrittura aggiorna immediatamente il disco → maggiore sicurezza ma minore velocità.

### Vantaggi

* Accesso ai file fino a 100× più rapido rispetto all’I/O diretto.
* Riduzione delle scritture ridondanti.
* Maggiore parallelismo tra processi e I/O.

### Svantaggi

* Perdita di dati in caso di crash prima dello svuotamento del buffer.
* Necessità di sincronizzazione (`sync`, `fsync`) per forzare il flush dei dati sul disco.

---

## 🔹 6. Verifica e recupero della consistenza

Nonostante i meccanismi di journaling, possono verificarsi errori dovuti a:

* danni fisici del disco,
* corruzione del journal,
* errori di sincronizzazione.

I sistemi UNIX/Linux utilizzano comandi di controllo come:

* **`fsck` (file system check):** analizza e corregge le incongruenze (blocchi orfani, inode non referenziati).
* **`e2fsck`:** specifico per file system ext2/3/4.
* **`xfs_repair`:** per XFS.

Durante la verifica, il sistema confronta bitmap, inode e directory per ricostruire la struttura logica corretta.

---

## 🧠 Mappa concettuale di sintesi

```plaintext
FILE SYSTEM (II)
│
├── Gestione spazio libero
│   ├─ Bitmap → veloce, compatta
│   ├─ Lista concatenata → semplice, lenta
│   ├─ Gruppi di blocchi → ibrido
│   └─ Contatori → blocchi contigui
│
├── Strutture dati
│   ├─ FAT → tabella globale, semplice
│   ├─ inode → puntatori diretti/indiretti
│   └─ Extent → blocchi contigui in gruppo
│
├── Journaling
│   ├─ Journal = log delle operazioni
│   ├─ Recupero dopo crash
│   ├─ Tipi: write-ahead, ordered, full
│   └─ Vantaggi → consistenza, tempi ridotti
│
├── Cache e buffering
│   ├─ Read cache → dati letti
│   ├─ Write-back → scrittura differita
│   ├─ Write-through → scrittura immediata
│   └─ Rischi → perdita dati se crash
│
└── Consistenza e verifica
    ├─ fsck, e2fsck, xfs_repair
    └─ Ricostruzione metadati e directory
```
