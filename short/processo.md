# 📘 Processi

## 🔹 1. Definizione di processo e PCB

* **Processo**:
  Un processo è un **programma in esecuzione**, arricchito di tutte le informazioni necessarie al sistema operativo per gestirlo.
  Non coincide con il solo codice del programma: include anche i **dati**, lo **stack delle chiamate** e lo **stato di esecuzione**.

  * È dinamico: cambia durante la vita (creazione, esecuzione, terminazione).
  * Ha un’identità unica: il **PID (Process Identifier)**, usato dal SO per riferirsi ad esso.

* **PCB (Process Control Block)**:
  È una struttura dati che contiene gli **attributi del processo**.
  Serve al SO per gestire e controllare l’evoluzione del processo.
  Contiene:

  * **Identificazione**: PID, UID (utente proprietario), identificatori dei thread (TID, TGID in Linux).
  * **Stato del processo**: running, ready, blocked, ecc.
  * **Stato del processore**: valori dei registri, Program Counter, PSW (Program Status Word).
  * **Gestione memoria**: puntatori alle tabelle delle pagine, segmenti di codice e dati.
  * **Gestione file e I/O**: puntatori ai file aperti e dispositivi assegnati.
  * **Informazioni di scheduling**: priorità, code di appartenenza, tempi di CPU utilizzati.
  * **Collegamenti**: riferimenti a processi padre/figli e thread del gruppo.

  👉 L’insieme di **programma + dati + stack + PCB** viene chiamato **immagine di processo (process image)**.

---

## 🔹 2. Stati del processo

Il comportamento di un processo viene descritto da **modelli a stati**:

### 🔸 Modello a 2 stati

* **Running** → il processo è in esecuzione sulla CPU.
* **Not Running** → il processo esiste ma non è in esecuzione (potrebbe essere pronto o in attesa).
  👉 È troppo semplice, ma utile come base.

### 🔸 Modello a 5 stati

1. **New** → processo appena creato.
2. **Ready** → in memoria, pronto per essere eseguito ma in attesa della CPU.
3. **Running** → in esecuzione sulla CPU.
4. **Blocked/Waiting** → in attesa di un evento esterno (es. I/O).
5. **Exit/Terminated** → ha terminato la sua esecuzione.

* Possono esserci transizioni dirette da *Ready* o *Blocked* a *Exit* (es. un processo viene “ucciso” da un altro).

### 🔸 Stato sospeso (suspended)

* **Ready/Suspend** → pronto ma “parcheggiato” in memoria secondaria (swap).
* **Blocked/Suspend** → in attesa, ma spostato fuori dalla RAM.
  👉 Usato dal **medium-term scheduler** per liberare memoria.

---

## 🔹 3. Mappa PCB + Diagramma stati

### 📍 Mappa PCB (contenuti principali)

* **Identificativi**: PID, parent PID, UID, TID.
* **Stato**: running, ready, blocked, sospeso, exit.
* **Registri CPU**: PC, registri generali, registri di stato.
* **Memoria**: puntatori a page table, segmenti di codice/dati.
* **I/O**: tabella file, dispositivi assegnati.
* **Scheduling**: priorità, tempo CPU usato, code ready/blocked.
* **Relazioni**: puntatori a processi padre/figli e thread.

### 📍 Diagramma degli stati

```text
   ┌───────────┐
   │   NEW     │
   └─────┬─────┘
         │
         ▼
   ┌───────────┐
   │   READY   │◄────────────┐
   └───┬───▲───┘             │
       │   │                 │
       ▼   │                 │
   ┌───────────┐             │
   │ RUNNING   │             │
   └───┬───▲───┘             │
       │   │                 │
       ▼   │                 │
   ┌───────────┐             │
   │  BLOCKED  │             │
   └─────┬─────┘             │
         │                   │
         ▼                   │
   ┌───────────┐             │
   │  EXIT     │─────────────┘
   └───────────┘
```

🔸 Estensione con **sospesi**: READY/BLOCKED hanno anche le versioni *suspend* (in memoria secondaria).
