# 📘 Memorie + Sistema Operativo

---

## 🔹 1. Gerarchia delle memorie

La gerarchia delle memorie nasce per conciliare **costo, velocità e capacità**.
La regola di base è:
👉 **più la memoria è vicina alla CPU → più è veloce → ma più è costosa e piccola.**

### 📍 Strati principali

1. **Registri della CPU**

   * Memoria interna al processore.
   * Dimensione: pochi byte (decine o centinaia).
   * Velocità: un accesso = 1 ciclo di clock (nanosecondi).
   * Uso: contengono dati immediati per le operazioni aritmetico-logiche e indirizzi.

2. **Cache (L1, L2, L3)**

   * Memoria ad alta velocità posta tra CPU e RAM.
   * Piccola (da qualche KB a pochi MB).
   * Funziona con il **principio di località**:

     * **Spaziale**: i dati vicini a quello usato probabilmente serviranno.
     * **Temporale**: i dati usati recentemente probabilmente verranno riutilizzati.
   * Meccanismi di gestione:

     * **Mappatura** (direct mapped, associativa, set-associativa).
     * **Rimpiazzamento** (LRU: least recently used).
     * **Politiche di scrittura**:

       * **Write-through** → ogni scrittura in cache aggiorna subito la RAM.
       * **Write-back** → scrittura rinviata, aggiorna la RAM solo quando il blocco viene sostituito.

3. **RAM (memoria principale)**

   * Volatile.
   * Grandezza: GB.
   * Accesso: più lento della cache, ma molto più veloce dei dischi.
   * Funzione: contiene i programmi in esecuzione e i dati su cui lavorano.

4. **Memoria secondaria (HDD, SSD)**

   * Non volatile.
   * Grande capacità (centinaia di GB, TB).
   * Accesso lento (millisecondi HDD, microsecondi SSD).
   * Conserva file, programmi, dati a lungo termine.

5. **Memorie di archiviazione offline**

   * Esempi: CD/DVD, Blu-ray, nastri magnetici.
   * Usate per backup o archiviazione a lungo termine.

📌 **Schema riassuntivo**

```text
Registri CPU   → velocità: altissima, capacità: pochissimi byte
Cache L1/L2/L3→ velocità: molto alta, capacità: KB–MB
RAM            → velocità: medio-alta, capacità: GB
Dischi (SSD/HDD) → velocità: bassa, capacità: TB
Archiviazione offline → velocità: molto bassa, capacità: enorme
```

---

## 🔹 2. Sistema Operativo: definizione

Il **Sistema Operativo (SO)** è un **insieme di programmi** che gestisce le risorse di un calcolatore (CPU, memoria, dispositivi I/O, rete, file system) e fornisce servizi agli utenti e ai programmatori.

### 📍 Funzioni principali

* **Gestione processi**

  * Creazione, esecuzione, sospensione, terminazione.
  * Scheduling e concorrenza.
* **Gestione memoria**

  * Allocazione/deallocazione.
  * Protezione e condivisione.
  * Memoria virtuale.
* **Gestione I/O**

  * Driver per periferiche.
  * Buffering, caching.
* **Gestione file system**

  * Creazione, lettura, scrittura, cancellazione file.
  * Protezione e permessi.
* **Sicurezza e protezione**

  * Controllo accessi, autenticazione, integrità.
* **Interfaccia utente**

  * CLI (Command Line Interface).
  * GUI (Graphical User Interface).

---

## 🔹 3. Kernel vs Microkernel

### 📍 Kernel

* È il **nucleo** del SO: la parte che rimane sempre in RAM.
* Contiene le **funzioni essenziali**:

  * gestione processi, memoria, interrupt, I/O di base.
* È il livello più vicino all’hardware.

### 📍 Kernel monolitico

* Tutte le funzionalità sono caricate in memoria dal boot fino allo spegnimento.
* Pro:

  * Esecuzione veloce.
  * Gestione diretta delle risorse.
* Contro:

  * Poco modulare.
  * Se un driver o modulo ha un bug, può compromettere l’intero sistema.

### 📍 Microkernel

* In memoria restano solo le funzioni essenziali (scheduler, gestione memoria, IPC).
* Tutte le altre funzionalità (file system, driver, protocolli) sono gestite da moduli separati e caricati solo quando servono.
* Pro:

  * Maggiore modularità, sicurezza e portabilità.
* Contro:

  * Maggior numero di comunicazioni tra moduli → overhead → prestazioni inferiori.

---

## 🔹 4. Struttura a 13 livelli del SO

Il SO può essere visto come una pila di **13 livelli**, dal più basso (hardware) al più alto (utente).
Ogni livello **usa i servizi** del livello sottostante e **offre servizi** a quello sopra.

1. **Circuiti elettrici**
   – registri, celle di memoria, porte logiche.
   – Operazioni elementari: azzerare un registro, leggere una cella.

2. **Istruzioni macchina**
   – operazioni di base: somma, sottrazione, load, store.

3. **Procedure (subroutine)**
   – concetto di chiamata e ritorno, codice riutilizzabile.

4. **Gestione interruzioni**
   – gestione di eventi asincroni e sincroni.

5. **Processi**
   – concetto di programma in esecuzione, gestione stato (ready, running, blocked).

6. **Memoria secondaria**
   – trasferimento blocchi dati tra RAM e dischi.

7. **Indirizzamento logico**
   – creazione spazi di indirizzi virtuali indipendenti per ogni processo.

8. **Comunicazioni tra processi (IPC)**
   – pipe, segnali, messaggi, memoria condivisa.

9. **File system**
   – gestione nomi simbolici, memorizzazione persistente dei file.

10. **Accesso dispositivi esterni**
    – standardizzazione dell’uso delle periferiche (API e driver).

11. **Associazione identificatori**
    – collegamento tra nomi logici (es. file.txt) e oggetti fisici (settori disco).

12. **Supporto di alto livello**
    – librerie di sistema, astrazioni per sviluppatori.

13. **Interfaccia utente**
    – CLI, GUI, shell: ambiente in cui l’utente interagisce con il sistema.

📌 Idea chiave:
Ogni livello **nasconde i dettagli** del livello sottostante e offre astrazioni più comode.

---

## 🔹 5. Mappe da costruire

1. **Mappa gerarchia memorie**

   * Piramide verticale:

     * In alto: **registri** (velocissimi, costosi, pochi byte).
     * Poi: **cache** (nanosecondi, MB).
     * Poi: **RAM** (nanosecondi, GB).
     * Poi: **HDD/SSD** (ms/µs, TB).
     * Alla base: **memoria offline** (lentissima, enorme).

2. **Schema livelli SO**

   * Una pila di 13 rettangoli sovrapposti.
   * Ogni livello con nome + breve funzione (es. Livello 9 = file system → gestione file persistenti).
