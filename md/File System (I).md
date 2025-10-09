# File System (I)

## 🔹 Introduzione generale

Il **file system** è la componente del sistema operativo che gestisce la **memorizzazione permanente dei dati**.
A differenza della memoria principale (RAM), la memoria di massa è **non volatile**, quindi mantiene i dati anche dopo lo spegnimento del sistema.

Il file system si occupa di:

* **organizzare i dati** in strutture logiche (file, directory);
* **gestire lo spazio su disco**;
* **fornire accesso controllato e sicuro** ai dati;
* **astrarre i dispositivi fisici**, offrendo un’interfaccia uniforme ai programmi.

Dal punto di vista dell’utente e dei processi, il file system fornisce un modello **astratto** del disco:
ogni dispositivo di memoria è visto come un insieme di **file e cartelle**, indipendentemente dal tipo di hardware sottostante.

---

## 🔹 1. Concetto di file

Un **file** è un insieme di informazioni memorizzate su un supporto di memoria secondaria, gestite come un’unica unità logica.
Il sistema operativo fornisce una **struttura uniforme** per tutti i file, indipendentemente dal loro contenuto.

### Tipi di file

* **File di testo:** sequenze di caratteri leggibili (es. `.txt`, `.c`, `.md`).
* **File binari:** contengono dati non interpretati direttamente come caratteri (es. eseguibili, immagini, database).
* **File di sistema:** file speciali gestiti dal kernel (es. `/proc` in Linux, device file in `/dev`).

### Attributi di un file

Ogni file possiede una serie di **metadati**, che ne descrivono le proprietà.
Queste informazioni vengono mantenute nella **directory** o in strutture specifiche come gli **inode** (nei sistemi UNIX).

| Attributo             | Descrizione                                 |
| --------------------- | ------------------------------------------- |
| Nome                  | Identificatore del file nel file system     |
| Tipo                  | Binario, testo, eseguibile, directory, ecc. |
| Dimensione            | Numero di byte occupati                     |
| Permessi              | Lettura, scrittura, esecuzione              |
| Proprietario e gruppo | Utente/i che possono accedere               |
| Data e ora            | Creazione, ultima modifica, ultimo accesso  |
| Puntatori ai blocchi  | Indirizzi fisici dei dati sul disco         |

---

## 🔹 2. Operazioni sui file

Il sistema operativo fornisce una serie di **primitive** o **chiamate di sistema (system call)** per la gestione dei file.
Le principali operazioni sono:

| Operazione | Descrizione                                           |
| ---------- | ----------------------------------------------------- |
| **Create** | Crea un nuovo file nel file system                    |
| **Open**   | Apre un file esistente per la lettura o scrittura     |
| **Read**   | Legge dati dal file nella memoria                     |
| **Write**  | Scrive dati dalla memoria nel file                    |
| **Seek**   | Sposta il puntatore interno a una posizione specifica |
| **Close**  | Chiude un file aperto                                 |
| **Delete** | Elimina un file dal file system                       |

Ogni file aperto è associato a un **file descriptor**, un identificatore univoco che il kernel usa per tenere traccia dei file aperti da ciascun processo.

---

## 🔹 3. Struttura logica del file system

Il file system non si limita a gestire file individuali, ma organizza l’intera memoria di massa in **livelli logici**.
Questa stratificazione permette di separare le funzioni astratte (viste dall’utente) dai dettagli fisici del disco.

### Livelli principali

1. **File system utente (User view):**
   L’utente interagisce con i file tramite percorsi e directory (`/home/emiliano/documenti/`).
   → Livello logico e simbolico.

2. **File system logico (Logical):**
   Il sistema operativo gestisce metadati, strutture, permessi e indirizzamenti logici.
   → Qui operano le funzioni di allocazione e protezione.

3. **File system fisico (Physical):**
   Interfaccia diretta con il **device driver del disco**, che gestisce i blocchi fisici e la cache.

Questa stratificazione consente di cambiare il tipo di disco o supporto (SSD, HDD, chiavetta) **senza modificare i programmi utente**, poiché il file system fornisce un livello di astrazione hardware-indipendente.

---

## 🔹 4. Struttura delle directory

Le **directory** (o cartelle) sono file speciali che contengono **elenco e metadati** dei file presenti in una determinata area del file system.
Servono a organizzare e raggruppare logicamente i dati.

### Tipi di struttura delle directory

#### a) Struttura a livello singolo

Tutti i file si trovano in un’unica directory.
→ Molto semplice ma **non scalabile**: i nomi devono essere univoci e l’organizzazione diventa caotica.

#### b) Struttura a due livelli

Ogni utente ha la propria directory separata (es. `/home/utente1/`, `/home/utente2/`).
→ Migliora l’organizzazione, ma non consente gerarchie più profonde.

#### c) Struttura gerarchica (ad albero)

È la struttura più comune (usata in UNIX, Linux, Windows).
Ogni directory può contenere file e altre directory.
→ Permette un’organizzazione logica e modulare.

**Esempio:**

```text
/
├── bin/
├── home/
│   ├── emiliano/
│   │   ├── documenti/
│   │   └── immagini/
└── etc/
```

#### d) Strutture con link

Alcuni file system supportano **collegamenti (link)** che puntano a file o directory esistenti:

* **Hard link:** riferimento diretto allo stesso inode (identico file).
* **Symbolic link (soft link):** file separato che contiene il percorso del file originale.

---

## 🔹 5. Gestione dello spazio su disco

Il disco è suddiviso in **blocchi fisici** (tipicamente da 512 byte a 4 KB).
Il file system deve assegnare questi blocchi ai file in modo efficiente, tenendo conto di prestazioni e frammentazione.

### Metodi di allocazione

#### a) Allocazione contigua

I blocchi di un file sono memorizzati in **posizioni consecutive** sul disco.

**Vantaggi:**

* Accesso sequenziale molto veloce (i dati sono adiacenti).
* Facile calcolo dell’indirizzo fisico.

**Svantaggi:**

* Necessario conoscere la dimensione del file in anticipo.
* **Frammentazione esterna**: difficile trovare blocchi contigui liberi.

---

#### b) Allocazione concatenata (Linked allocation)

Ogni file è una **catena di blocchi** collegati da puntatori.
Il primo blocco contiene un riferimento al successivo, e così via.

**Vantaggi:**

* Nessuna frammentazione esterna.
* Facile estendere i file.

**Svantaggi:**

* Accesso casuale lento (necessario attraversare la catena).
* Overhead di spazio per i puntatori.
* Rischio di perdita di dati se un blocco della catena si danneggia.

---

#### c) Allocazione indicizzata

Ogni file ha una **tabella di indice** (index block) che elenca tutti i blocchi che compongono il file.
Simile alla Page Table nella memoria virtuale.

**Vantaggi:**

* Accesso diretto e casuale efficiente.
* Nessuna frammentazione esterna.
* Facile estensione del file.

**Svantaggi:**

* Overhead di spazio per mantenere gli indici.
* L’indice stesso deve essere memorizzato e gestito come file.

**Esempio (in UNIX):**
Il sistema usa strutture **inode**, dove ogni inode contiene:

* indirizzi diretti (blocchi immediati),
* indiretti singoli, doppi e tripli (puntatori a tabelle di indirizzi).

---

## 🔹 6. Gestione dei metadati: inode

Nei sistemi UNIX/Linux, ogni file è rappresentato da un **inode** (index node), una struttura che memorizza **tutte le informazioni sul file tranne il nome**.

### Contenuto di un inode

| Campo                         | Descrizione                                |
| ----------------------------- | ------------------------------------------ |
| Identificatore (inode number) | Numero univoco del file                    |
| Tipo di file                  | Normale, directory, device, link           |
| Permessi e modalità           | rwx per utente, gruppo e altri             |
| Proprietario / gruppo         | UID e GID                                  |
| Dimensione                    | In byte                                    |
| Timestamp                     | Creazione, modifica, accesso               |
| Puntatori ai blocchi          | Diretti, indiretti singoli, doppi e tripli |

Il nome del file è mantenuto separatamente nella directory, che associa il nome all’inode corrispondente.
Questo meccanismo consente la presenza di più **hard link** per lo stesso file (più nomi che puntano allo stesso inode).

---

## 🔹 7. Montaggio del file system

I moderni sistemi supportano **più file system contemporaneamente** (es. ext4, FAT32, NTFS, ecc.), montati in una **gerarchia unica**.

L’operazione di **mount** associa un file system fisico (es. una partizione o chiavetta) a una directory esistente nel file system principale.

**Esempio:**

``` bash
mount /dev/sdb1 /mnt/usb
```

→ La partizione `sdb1` sarà accessibile sotto la directory `/mnt/usb`.

---

## 🧠 Mappa concettuale di sintesi

```plaintext
FILE SYSTEM (I)
│
├── Definizione
│   ├─ Organizzazione dati su memoria permanente
│   ├─ Interfaccia astratta ai dispositivi
│   └─ Gestione accesso e protezione
│
├── File
│   ├─ Tipi → testo, binario, sistema
│   ├─ Attributi → nome, tipo, permessi, dimensione, date
│   └─ Metadati → gestiti in inode
│
├── Operazioni
│   ├─ Create, Open, Read, Write
│   ├─ Seek, Close, Delete
│   └─ File descriptor
│
├── Struttura logica
│   ├─ Livello utente → percorsi
│   ├─ Livello logico → metadati, allocazione
│   └─ Livello fisico → blocchi e driver
│
├── Directory
│   ├─ Singolo livello
│   ├─ Due livelli
│   ├─ Gerarchico (ad albero)
│   └─ Link simbolici / hard link
│
├── Allocazione spazio
│   ├─ Contigua → veloce, ma frammentata
│   ├─ Concatenata → flessibile, lenta
│   └─ Indicizzata → efficiente, overhead indice
│
├── Inode
│   ├─ Identifica file
│   ├─ Metadati e puntatori
│   └─ Supporta hard link
│
└── Montaggio
    ├─ mount device → directory
    └─ Unione di più FS in una gerarchia
```
