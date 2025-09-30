# ✅ Checklist Studio Sistemi Operativi 1

(30 settembre → 12 ottobre, domeniche OFF)

## Settimana 1

- [ ] **Mar 30/09** – Architettura monoprocessore  
  - [ ] CPU e registri (utente, controllo, interni)  
  - [ ] Ciclo fetch/execute  
  - [ ] Categorie istruzioni  
  - [ ] Mappa CPU + registri  

- [ ] **Mer 01/10** – Interrupt + I/O  
  - [ ] Tipi di interrupt (sincroni, asincroni)  
  - [ ] Handler, sequenziale vs annidato  
  - [ ] Tecniche I/O: programmato, interrupt-driven, DMA  
  - [ ] Tabella interrupt + schema tecniche I/O  

- [ ] **Gio 02/10** – Memorie + Sistema Operativo  
  - [ ] Gerarchia delle memorie (cache, mapping, replacement, write-back/through)  
  - [ ] Definizione SO, kernel vs microkernel  
  - [ ] Livelli (1–13)  
  - [ ] Mappa gerarchia memorie + schema livelli SO  

- [ ] **Ven 03/10** – Storia dei Sistemi Operativi  
  - [ ] Sistemi batch  
  - [ ] Time sharing  
  - [ ] Risultati hardware/OS (timer, istruzioni privilegiate)  
  - [ ] Timeline + tabella batch vs time sharing  

- [ ] **Sab 04/10** – Processi  
  - [ ] Definizione e PCB  
  - [ ] Stati del processo (2, 5 stati, sospesi)  
  - [ ] Mappa PCB + diagramma stati  

- [ ] **Dom 05/10** – OFF  

---

## Settimana 2

- [ ] **Lun 06/10** – Thread  
  - [ ] ULT vs KLT (vantaggi/svantaggi)  
  - [ ] Operazioni: spawn, block, unblock, finish  
  - [ ] Linux: LWP, PCB, stati  
  - [ ] Tabella ULT vs KLT + schema PCB Linux  

- [ ] **Mar 07/10** – Scheduling (I)  
  - [ ] Obiettivi dello scheduling  
  - [ ] Tipi: long, medium, short, I/O  
  - [ ] Algoritmi: FCFS, RR, SPN, SRT, HRRN  
  - [ ] Mappa scheduling + tabella algoritmi  

- [ ] **Mer 08/10** – Scheduling (II)  
  - [ ] Scheduling multiprocessore  
  - [ ] Scheduling UNIX/Linux (SCHED_FIFO, RR, OTHER)  
  - [ ] Schema scheduling Linux  

- [ ] **Gio 09/10** – Gestione della memoria (I)  
  - [ ] Requisiti: rilocazione, protezione, condivisione, organizzazione logica/fisica  
  - [ ] Partizionamento: statico, dinamico, buddy system  
  - [ ] Schema indirizzi logici/fisici + tabella algoritmi posizionamento  

- [ ] **Ven 10/10** – Gestione della memoria (II)  
  - [ ] Paginazione semplice  
  - [ ] Segmentazione  
  - [ ] Memoria virtuale: TLB, politiche di sostituzione (FIFO, LRU, Ottimo, Clock)  
  - [ ] Schema traduzione indirizzi + tabella replacement  

- [ ] **Sab 11/10** – Memoria avanzata  
  - [ ] Resident set, cleaning policy, load control  
  - [ ] Thrashing e working set  
  - [ ] Gestione memoria in Linux (buddy, slab)  
  - [ ] Mappa riassuntiva memoria virtuale  

- [ ] **Dom 12/10** – I/O e File System  
  - [ ] Dispositivi, driver, buffering, spooling  
  - [ ] Scheduling dischi (FCFS, SSTF, SCAN, C-SCAN, LOOK, C-LOOK)  
  - [ ] RAID: 0, 1, 5, 6 (pro/contro)  
  - [ ] SSD vs HDD  
  - [ ] File system: concetti base, operazioni, attributi  
  - [ ] Organizzazione directory (lista, due livelli, albero, grafo)  
  - [ ] Metodi di allocazione (contigua, concatenata, indicizzata)  
  - [ ] Gestione spazio libero (bitmap, liste)  
  - [ ] Journaling (fisico, logico, COW, log-structured)  
  - [ ] Inode in UNIX/Linux, tipi di file, permessi  
  - [ ] Mappe I/O + FS complete  
