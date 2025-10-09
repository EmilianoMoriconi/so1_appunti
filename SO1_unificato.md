
# SISTEMI OPERATIVI- MODULO 1

- [SISTEMI OPERATIVI- MODULO 1](#sistemi-operativi--modulo-1)
  - [Storia dei Sistemi Operativi](#storia-dei-sistemi-operativi)
    - [🔹 Introduzione](#-introduzione)
    - [🔹 1. Prima generazione: calcolo manuale e programmazione diretta (anni ’40 – primi ’50)](#-1-prima-generazione-calcolo-manuale-e-programmazione-diretta-anni-40--primi-50)
    - [🔹 2. Seconda generazione: sistemi batch (anni ’50 – metà ’60)](#-2-seconda-generazione-sistemi-batch-anni-50--metà-60)
      - [Funzionamento del sistema batch](#funzionamento-del-sistema-batch)
      - [Caratteristiche](#caratteristiche)
      - [Limiti](#limiti)
    - [🔹 3. Terza generazione: multiprogrammazione e time-sharing (anni ’60 – ’70)](#-3-terza-generazione-multiprogrammazione-e-time-sharing-anni-60--70)
      - [Multiprogrammazione](#multiprogrammazione)
      - [Time-sharing](#time-sharing)
      - [Sistemi rappresentativi](#sistemi-rappresentativi)
    - [🔹 4. Quarta generazione: sistemi multiprocessore e distribuiti (anni ’80 – ’90)](#-4-quarta-generazione-sistemi-multiprocessore-e-distribuiti-anni-80--90)
      - [Caratteristiche principali](#caratteristiche-principali)
      - [Sistemi notevoli](#sistemi-notevoli)
    - [🔹 5. Quinta generazione: sistemi moderni e virtualizzazione (2000 – oggi)](#-5-quinta-generazione-sistemi-moderni-e-virtualizzazione-2000--oggi)
      - [Tendenze moderne](#tendenze-moderne)
    - [🔹 6. Evoluzione dell’hardware e impatto sul SO](#-6-evoluzione-dellhardware-e-impatto-sul-so)
    - [🔹 7. Timeline sintetica](#-7-timeline-sintetica)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi)
  - [Architettura monoprocessore](#architettura-monoprocessore)
    - [🔹 Introduzione](#-introduzione-1)
    - [🔹 1. Struttura generale della CPU](#-1-struttura-generale-della-cpu)
    - [🔹 2. Tipologie di registri](#-2-tipologie-di-registri)
      - [a) Registri utente](#a-registri-utente)
      - [b) Registri di controllo e di stato](#b-registri-di-controllo-e-di-stato)
      - [c) Registri interni (buffer)](#c-registri-interni-buffer)
    - [🔹 3. Ciclo di esecuzione: Fetch–Decode–Execute](#-3-ciclo-di-esecuzione-fetchdecodeexecute)
      - [a) Fase di Fetch (prelievo)](#a-fase-di-fetch-prelievo)
      - [b) Fase di Decode (decodifica)](#b-fase-di-decode-decodifica)
      - [c) Fase di Execute (esecuzione)](#c-fase-di-execute-esecuzione)
    - [🔹 4. Modalità di indirizzamento](#-4-modalità-di-indirizzamento)
    - [🔹 5. Ciclo di istruzione e ruolo del sistema operativo](#-5-ciclo-di-istruzione-e-ruolo-del-sistema-operativo)
    - [🔹 6. Categorie di istruzioni macchina](#-6-categorie-di-istruzioni-macchina)
    - [🔹 7. Interazione CPU – Memoria – I/O](#-7-interazione-cpu--memoria--io)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-1)
  - [Memorie + Sistema Operativo](#memorie--sistema-operativo)
    - [🔹 Introduzione generale](#-introduzione-generale)
    - [🔹 1. Gerarchia delle memorie](#-1-gerarchia-delle-memorie)
      - [Struttura a livelli](#struttura-a-livelli)
    - [🔹 2. Tipologie di memoria](#-2-tipologie-di-memoria)
      - [a) Memoria primaria](#a-memoria-primaria)
      - [b) Memoria secondaria](#b-memoria-secondaria)
      - [c) Memoria terziaria e virtuale](#c-memoria-terziaria-e-virtuale)
    - [🔹 3. Memoria cache](#-3-memoria-cache)
      - [Principio di località](#principio-di-località)
      - [Organizzazione](#organizzazione)
      - [Politiche di scrittura](#politiche-di-scrittura)
    - [🔹 4. Mappatura e sostituzione in cache](#-4-mappatura-e-sostituzione-in-cache)
      - [Tipi di mappatura](#tipi-di-mappatura)
      - [Politiche di rimpiazzo](#politiche-di-rimpiazzo)
    - [🔹 5. Ruolo del Sistema Operativo nella memoria](#-5-ruolo-del-sistema-operativo-nella-memoria)
      - [Meccanismi principali](#meccanismi-principali)
    - [🔹 6. Struttura logica del Sistema Operativo](#-6-struttura-logica-del-sistema-operativo)
      - [a) Kernel](#a-kernel)
      - [b) Shell e interfaccia utente](#b-shell-e-interfaccia-utente)
      - [c) Livelli di astrazione del SO](#c-livelli-di-astrazione-del-so)
    - [🔹 7. Kernel vs Microkernel](#-7-kernel-vs-microkernel)
      - [Kernel monolitico](#kernel-monolitico)
      - [Microkernel](#microkernel)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-2)
  - [Interrupt e I/O](#interrupt-e-io)
    - [🔹 Introduzione](#-introduzione-2)
    - [🔹 1. Concetto di interrupt](#-1-concetto-di-interrupt)
    - [🔹 2. Tipologie di interrupt](#-2-tipologie-di-interrupt)
      - [a) Interrupt hardware](#a-interrupt-hardware)
      - [b) Interrupt software](#b-interrupt-software)
      - [c) Classificazione funzionale](#c-classificazione-funzionale)
    - [🔹 3. Meccanismo di gestione di un interrupt](#-3-meccanismo-di-gestione-di-un-interrupt)
      - [Fasi principali](#fasi-principali)
    - [🔹 4. Vettore degli interrupt](#-4-vettore-degli-interrupt)
    - [🔹 5. Gestione sequenziale e annidata degli interrupt](#-5-gestione-sequenziale-e-annidata-degli-interrupt)
      - [a) Gestione sequenziale](#a-gestione-sequenziale)
      - [b) Gestione annidata](#b-gestione-annidata)
    - [🔹 6. Context switch e interrupt](#-6-context-switch-e-interrupt)
    - [🔹 7. Tecniche di I/O](#-7-tecniche-di-io)
      - [a) I/O programmato](#a-io-programmato)
      - [b) I/O con interrupt](#b-io-con-interrupt)
      - [c) I/O con DMA (Direct Memory Access)](#c-io-con-dma-direct-memory-access)
    - [🔹 8. Ruolo del sistema operativo negli interrupt e nell’I/O](#-8-ruolo-del-sistema-operativo-negli-interrupt-e-nellio)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-3)
  - [Gestione I/O (I)](#gestione-io-i)
    - [🔹 Introduzione](#-introduzione-3)
    - [🔹 1. Architettura del sottosistema I/O](#-1-architettura-del-sottosistema-io)
      - [Livelli principali](#livelli-principali)
      - [Flusso generale](#flusso-generale)
    - [🔹 2. Componenti dell’I/O](#-2-componenti-dellio)
      - [a) Device Controller](#a-device-controller)
      - [b) Device Driver](#b-device-driver)
    - [🔹 3. Tecniche di comunicazione CPU–Dispositivo](#-3-tecniche-di-comunicazione-cpudispositivo)
      - [a) I/O programmato (Polling)](#a-io-programmato-polling)
      - [b) I/O con interrupt](#b-io-con-interrupt-1)
      - [c) I/O con DMA (Direct Memory Access)](#c-io-con-dma-direct-memory-access-1)
    - [🔹 4. Bufferizzazione](#-4-bufferizzazione)
      - [Tipi di buffer](#tipi-di-buffer)
        - [a) Single Buffer](#a-single-buffer)
        - [b) Double Buffer](#b-double-buffer)
        - [c) Circular Buffer](#c-circular-buffer)
      - [Vantaggi](#vantaggi)
      - [Svantaggi](#svantaggi)
    - [🔹 5. Spooling](#-5-spooling)
      - [Funzionamento](#funzionamento)
      - [Vantaggi](#vantaggi-1)
    - [🔹 6. Struttura software del sistema I/O](#-6-struttura-software-del-sistema-io)
      - [Livelli tipici](#livelli-tipici)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-4)
  - [Gestione I/O (II)](#gestione-io-ii)
    - [🔹 Introduzione](#-introduzione-4)
    - [🔹 1. Struttura fisica e tempi di accesso al disco](#-1-struttura-fisica-e-tempi-di-accesso-al-disco)
      - [Tempi di accesso](#tempi-di-accesso)
    - [🔹 2. Scheduling dei dischi](#-2-scheduling-dei-dischi)
      - [a) FCFS – *First Come, First Served*](#a-fcfs--first-come-first-served)
      - [b) SSTF – *Shortest Seek Time First*](#b-sstf--shortest-seek-time-first)
      - [c) SCAN (Elevator Algorithm)](#c-scan-elevator-algorithm)
      - [d) C-SCAN – *Circular SCAN*](#d-c-scan--circular-scan)
      - [e) LOOK e C-LOOK](#e-look-e-c-look)
      - [f) Confronto generale](#f-confronto-generale)
    - [🔹 3. RAID – Redundant Array of Independent Disks](#-3-raid--redundant-array-of-independent-disks)
      - [Motivazioni](#motivazioni)
      - [Livelli principali](#livelli-principali-1)
      - [Considerazioni](#considerazioni)
    - [🔹 4. HDD vs SSD](#-4-hdd-vs-ssd)
      - [HDD (Hard Disk Drive)](#hdd-hard-disk-drive)
      - [SSD (Solid State Drive)](#ssd-solid-state-drive)
      - [Implicazioni per il sistema operativo](#implicazioni-per-il-sistema-operativo)
    - [🔹 5. Gestione I/O in Linux](#-5-gestione-io-in-linux)
      - [Sottosistema del block I/O](#sottosistema-del-block-io)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-5)
  - [Processi](#processi)
    - [🔹 Introduzione](#-introduzione-5)
    - [🔹 1. Processo vs programma](#-1-processo-vs-programma)
    - [🔹 2. Componenti di un processo](#-2-componenti-di-un-processo)
      - [a) Spazio di indirizzamento (address space)](#a-spazio-di-indirizzamento-address-space)
      - [b) Stato e contesto](#b-stato-e-contesto)
    - [🔹 3. Stati del processo](#-3-stati-del-processo)
      - [a) Modello a 2 stati](#a-modello-a-2-stati)
      - [b) Modello a 5 stati](#b-modello-a-5-stati)
      - [c) Stati sospesi](#c-stati-sospesi)
    - [🔹 4. Transizioni di stato](#-4-transizioni-di-stato)
      - [Casi principali](#casi-principali)
    - [🔹 5. PCB – Process Control Block](#-5-pcb--process-control-block)
      - [Struttura tipica del PCB](#struttura-tipica-del-pcb)
    - [🔹 6. Code di processi](#-6-code-di-processi)
    - [🔹 7. Operazioni sui processi](#-7-operazioni-sui-processi)
      - [a) Creazione](#a-creazione)
      - [b) Terminazione](#b-terminazione)
      - [c) Blocco e sblocco](#c-blocco-e-sblocco)
    - [🔹 8. Processi e gerarchie](#-8-processi-e-gerarchie)
    - [🔹 9. Relazione con i thread](#-9-relazione-con-i-thread)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-6)
  - [📘 Thread](#-thread)
    - [🔹 Introduzione generale](#-introduzione-generale-1)
    - [🔹 Vantaggi dell’approccio multithread](#-vantaggi-dellapproccio-multithread)
    - [🔹 Thread a livello utente (ULT) e a livello kernel (KLT)](#-thread-a-livello-utente-ult-e-a-livello-kernel-klt)
      - [▫️ Thread a livello utente (ULT)](#️-thread-a-livello-utente-ult)
      - [▫️ Thread a livello kernel (KLT)](#️-thread-a-livello-kernel-klt)
      - [▫️ Riepilogo comparativo ULT vs KLT](#️-riepilogo-comparativo-ult-vs-klt)
    - [🔹 Operazioni fondamentali sui thread](#-operazioni-fondamentali-sui-thread)
    - [🔹 Thread in Linux: LWP e PCB](#-thread-in-linux-lwp-e-pcb)
      - [Stati principali in Linux](#stati-principali-in-linux)
    - [🔹 Sintesi finale](#-sintesi-finale)
    - [🔹 Sincronizzazione tra Thread](#-sincronizzazione-tra-thread)
      - [▫️ Problema di concorrenza e sezione critica](#️-problema-di-concorrenza-e-sezione-critica)
    - [🔹 Strumenti di sincronizzazione](#-strumenti-di-sincronizzazione)
      - [1. **Mutex (Mutual Exclusion Lock)**](#1-mutex-mutual-exclusion-lock)
      - [2. **Semafori**](#2-semafori)
      - [3. **Condition Variable**](#3-condition-variable)
      - [4. **Join e sincronizzazione del flusso**](#4-join-e-sincronizzazione-del-flusso)
      - [5. **Barrier**](#5-barrier)
    - [🔹 Problemi tipici della sincronizzazione](#-problemi-tipici-della-sincronizzazione)
      - [▫️ Deadlock](#️-deadlock)
      - [▫️ Starvation](#️-starvation)
      - [▫️ Busy waiting e spinlock](#️-busy-waiting-e-spinlock)
    - [🔹 Sincronizzazione in Linux](#-sincronizzazione-in-linux)
    - [🔹 Sintesi generale](#-sintesi-generale)
  - [Scheduling](#scheduling)
    - [🔹 Introduzione generale](#-introduzione-generale-2)
    - [🔹 Obiettivi dello scheduling](#-obiettivi-dello-scheduling)
      - [1. Obiettivi nei sistemi batch](#1-obiettivi-nei-sistemi-batch)
      - [2. Obiettivi nei sistemi interattivi](#2-obiettivi-nei-sistemi-interattivi)
      - [3. Compromessi](#3-compromessi)
    - [🔹 Tipi di scheduling](#-tipi-di-scheduling)
      - [1. Long-Term Scheduling (a lungo termine)](#1-long-term-scheduling-a-lungo-termine)
      - [2. Medium-Term Scheduling (a medio termine)](#2-medium-term-scheduling-a-medio-termine)
      - [3. Short-Term Scheduling (a breve termine)](#3-short-term-scheduling-a-breve-termine)
      - [4. I/O Scheduling](#4-io-scheduling)
    - [🔹 Tipologie di scheduling: preemptive vs non-preemptive](#-tipologie-di-scheduling-preemptive-vs-non-preemptive)
    - [🔹 Algoritmi di scheduling della CPU](#-algoritmi-di-scheduling-della-cpu)
      - [FCFS – *First Come, First Served*](#fcfs--first-come-first-served)
      - [RR – *Round Robin*](#rr--round-robin)
      - [SPN – *Shortest Process Next* (o SJF – Shortest Job First)](#spn--shortest-process-next-o-sjf--shortest-job-first)
      - [SRT – *Shortest Remaining Time*](#srt--shortest-remaining-time)
      - [HRRN – *Highest Response Ratio Next*](#hrrn--highest-response-ratio-next)
      - [Tabella comparativa algoritmi](#tabella-comparativa-algoritmi)
    - [🔹 Scheduling multiprocessore e Scheduling UNIX/Linux](#-scheduling-multiprocessore-e-scheduling-unixlinux)
    - [🔹 1. Introduzione](#-1-introduzione)
    - [🔹 2. Tipologie di scheduling multiprocessore](#-2-tipologie-di-scheduling-multiprocessore)
      - [a) Asymmetric Multiprocessing (AMP)](#a-asymmetric-multiprocessing-amp)
      - [b) Symmetric Multiprocessing (SMP)](#b-symmetric-multiprocessing-smp)
    - [🔹 3. CPU Affinity](#-3-cpu-affinity)
      - [Tipi di affinità](#tipi-di-affinità)
        - [1. Soft affinity](#1-soft-affinity)
        - [2. Hard affinity](#2-hard-affinity)
    - [🔹 4. Load Balancing](#-4-load-balancing)
      - [Strategie principali](#strategie-principali)
        - [Push migration](#push-migration)
        - [Pull migration](#pull-migration)
    - [🔹 5. Scheduling in UNIX / Linux](#-5-scheduling-in-unix--linux)
    - [🔹 6. Scheduler O(1)](#-6-scheduler-o1)
      - [Struttura](#struttura)
      - [Caratteristiche principali](#caratteristiche-principali-1)
    - [🔹 7. Completely Fair Scheduler (CFS)](#-7-completely-fair-scheduler-cfs)
      - [Principio di funzionamento](#principio-di-funzionamento)
      - [Vantaggi del CFS](#vantaggi-del-cfs)
      - [Intervallo temporale](#intervallo-temporale)
    - [🔹 8. Politiche di scheduling in Linux](#-8-politiche-di-scheduling-in-linux)
    - [🔹 9. Struttura del PCB in Linux per lo scheduling](#-9-struttura-del-pcb-in-linux-per-lo-scheduling)
    - [🔹 10. Sintesi concettuale per mappa](#-10-sintesi-concettuale-per-mappa)
  - [Sincronizzazione (I)](#sincronizzazione-i)
    - [🔹 Introduzione](#-introduzione-6)
    - [🔹 1. Sezione critica](#-1-sezione-critica)
      - [Struttura generale di un processo](#struttura-generale-di-un-processo)
    - [🔹 2. Condizioni di competizione (Race Conditions)](#-2-condizioni-di-competizione-race-conditions)
      - [Esempio classico](#esempio-classico)
    - [🔹 3. Soluzioni software alla mutua esclusione](#-3-soluzioni-software-alla-mutua-esclusione)
      - [a) Disabilitazione degli interrupt (solo kernel)](#a-disabilitazione-degli-interrupt-solo-kernel)
      - [b) Soluzione di Peterson](#b-soluzione-di-peterson)
      - [c) Algoritmo del panettiere (Bakery Algorithm)](#c-algoritmo-del-panettiere-bakery-algorithm)
    - [🔹 4. Soluzioni hardware](#-4-soluzioni-hardware)
      - [a) Test-and-Set](#a-test-and-set)
      - [b) Swap (Exchange)](#b-swap-exchange)
      - [c) Compare-and-Swap (CAS)](#c-compare-and-swap-cas)
    - [🔹 5. Semafori](#-5-semafori)
      - [Tipologie di semafori](#tipologie-di-semafori)
      - [Vantaggi](#vantaggi-2)
      - [Svantaggi](#svantaggi-1)
    - [🔹 6. Problema Produttore–Consumatore](#-6-problema-produttoreconsumatore)
      - [Descrizione](#descrizione)
      - [Soluzione con semafori](#soluzione-con-semafori)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-7)
  - [Sincronizzazione (II)](#sincronizzazione-ii)
    - [🔹 Introduzione](#-introduzione-7)
    - [🔹 1. Monitor](#-1-monitor)
      - [Concetto](#concetto)
      - [Variabili di condizione](#variabili-di-condizione)
      - [Vantaggi](#vantaggi-3)
      - [Svantaggi](#svantaggi-2)
    - [🔹 2. Deadlock](#-2-deadlock)
      - [Esempio classico](#esempio-classico-1)
    - [🔹 3. Condizioni necessarie per il deadlock](#-3-condizioni-necessarie-per-il-deadlock)
    - [🔹 4. Rappresentazione con il grafo delle risorse](#-4-rappresentazione-con-il-grafo-delle-risorse)
      - [Esempio](#esempio)
    - [🔹 5. Strategie per la gestione del deadlock](#-5-strategie-per-la-gestione-del-deadlock)
      - [a) Prevenzione](#a-prevenzione)
      - [b) Evitamento (Dynamic avoidance)](#b-evitamento-dynamic-avoidance)
      - [c) Rilevazione e recupero](#c-rilevazione-e-recupero)
    - [🔹 6. Algoritmo del Banchiere (Banker’s Algorithm)](#-6-algoritmo-del-banchiere-bankers-algorithm)
      - [Concetto](#concetto-1)
      - [Parametri principali](#parametri-principali)
      - [Procedura](#procedura)
      - [Esempio (semplificato)](#esempio-semplificato)
      - [Limiti](#limiti-1)
    - [🔹 7. Riepilogo comparativo](#-7-riepilogo-comparativo)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-8)
  - [Gestione della memoria (I)](#gestione-della-memoria-i)
    - [🔹 Introduzione](#-introduzione-8)
    - [🔹 1. Rilocazione](#-1-rilocazione)
      - [Concetto](#concetto-2)
        - [1. Rilocazione statica](#1-rilocazione-statica)
        - [2. Rilocazione dinamica](#2-rilocazione-dinamica)
      - [Implementazione hardware](#implementazione-hardware)
    - [🔹 2. Protezione](#-2-protezione)
      - [Meccanismi di protezione](#meccanismi-di-protezione)
    - [🔹 3. Partizionamento della memoria](#-3-partizionamento-della-memoria)
      - [Tipi principali](#tipi-principali)
        - [1. Partizionamento fisso (Fixed Partitioning)](#1-partizionamento-fisso-fixed-partitioning)
        - [2. Partizionamento variabile (Dynamic Partitioning)](#2-partizionamento-variabile-dynamic-partitioning)
    - [🔹 4. Buddy System](#-4-buddy-system)
      - [Funzionamento](#funzionamento-1)
        - [Allocazione](#allocazione)
        - [Deallocazione](#deallocazione)
      - [Vantaggi](#vantaggi-4)
      - [Svantaggi](#svantaggi-3)
    - [🔹 5. Considerazioni generali](#-5-considerazioni-generali)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-9)
  - [Gestione della memoria (II)](#gestione-della-memoria-ii)
    - [🔹 Introduzione](#-introduzione-9)
    - [🔹 1. Memoria virtuale](#-1-memoria-virtuale)
      - [Obiettivi principali](#obiettivi-principali)
    - [🔹 2. Paging](#-2-paging)
      - [Concetti fondamentali](#concetti-fondamentali)
      - [Funzionamento](#funzionamento-2)
      - [Vantaggi del paging](#vantaggi-del-paging)
      - [Svantaggi](#svantaggi-4)
    - [🔹 3. Page Table (Tabella delle pagine)](#-3-page-table-tabella-delle-pagine)
      - [Contenuto di ogni voce (entry)](#contenuto-di-ogni-voce-entry)
      - [Accesso alla Page Table](#accesso-alla-page-table)
    - [🔹 4. Translation Lookaside Buffer (TLB)](#-4-translation-lookaside-buffer-tlb)
      - [Funzionamento](#funzionamento-3)
      - [Vantaggi](#vantaggi-5)
      - [Svantaggi](#svantaggi-5)
    - [🔹 5. Paging multilivello](#-5-paging-multilivello)
      - [Funzionamento](#funzionamento-4)
      - [Vantaggi](#vantaggi-6)
      - [Svantaggi](#svantaggi-6)
    - [🔹 6. Segmentazione](#-6-segmentazione)
      - [Concetto](#concetto-3)
      - [Struttura hardware](#struttura-hardware)
      - [Vantaggi](#vantaggi-7)
      - [Svantaggi](#svantaggi-7)
    - [🔹 7. Segmentazione con Paging (ibrido)](#-7-segmentazione-con-paging-ibrido)
      - [Funzionamento](#funzionamento-5)
      - [Vantaggi](#vantaggi-8)
      - [Svantaggi](#svantaggi-8)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-10)
  - [Gestione della memoria (III)](#gestione-della-memoria-iii)
    - [🔹 Introduzione](#-introduzione-10)
    - [🔹 1. Page Fault e Swapping](#-1-page-fault-e-swapping)
    - [🔹 2. Algoritmi di rimpiazzo delle pagine](#-2-algoritmi-di-rimpiazzo-delle-pagine)
      - [FIFO – *First In, First Out*](#fifo--first-in-first-out)
      - [OPT – *Optimal Replacement* (teorico)](#opt--optimal-replacement-teorico)
      - [LRU – *Least Recently Used*](#lru--least-recently-used)
      - [Second-Chance (Clock Algorithm)](#second-chance-clock-algorithm)
      - [NRU – *Not Recently Used*](#nru--not-recently-used)
      - [LFU – *Least Frequently Used*](#lfu--least-frequently-used)
    - [🔹 3. Algoritmi di allocazione dei frame](#-3-algoritmi-di-allocazione-dei-frame)
      - [Allocazione fissa vs dinamica](#allocazione-fissa-vs-dinamica)
      - [Allocazione proporzionale](#allocazione-proporzionale)
      - [Allocazione con priorità](#allocazione-con-priorità)
    - [🔹 4. Thrashing](#-4-thrashing)
      - [Cause principali](#cause-principali)
      - [Effetti](#effetti)
    - [🔹 5. Modelli di controllo del thrashing](#-5-modelli-di-controllo-del-thrashing)
      - [a) Working Set Model](#a-working-set-model)
      - [b) Page Fault Frequency (PFF)](#b-page-fault-frequency-pff)
    - [🔹 6. Prestazioni e compromessi](#-6-prestazioni-e-compromessi)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-11)
  - [File System (I)](#file-system-i)
    - [🔹 Introduzione generale](#-introduzione-generale-3)
    - [🔹 1. Concetto di file](#-1-concetto-di-file)
      - [Tipi di file](#tipi-di-file)
      - [Attributi di un file](#attributi-di-un-file)
    - [🔹 2. Operazioni sui file](#-2-operazioni-sui-file)
    - [🔹 3. Struttura logica del file system](#-3-struttura-logica-del-file-system)
      - [Livelli principali](#livelli-principali-2)
    - [🔹 4. Struttura delle directory](#-4-struttura-delle-directory)
      - [Tipi di struttura delle directory](#tipi-di-struttura-delle-directory)
        - [a) Struttura a livello singolo](#a-struttura-a-livello-singolo)
        - [b) Struttura a due livelli](#b-struttura-a-due-livelli)
        - [c) Struttura gerarchica (ad albero)](#c-struttura-gerarchica-ad-albero)
        - [d) Strutture con link](#d-strutture-con-link)
    - [🔹 5. Gestione dello spazio su disco](#-5-gestione-dello-spazio-su-disco)
      - [Metodi di allocazione](#metodi-di-allocazione)
        - [a) Allocazione contigua](#a-allocazione-contigua)
        - [b) Allocazione concatenata (Linked allocation)](#b-allocazione-concatenata-linked-allocation)
        - [c) Allocazione indicizzata](#c-allocazione-indicizzata)
    - [🔹 6. Gestione dei metadati: inode](#-6-gestione-dei-metadati-inode)
      - [Contenuto di un inode](#contenuto-di-un-inode)
    - [🔹 7. Montaggio del file system](#-7-montaggio-del-file-system)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-12)
  - [File System (II)](#file-system-ii)
    - [🔹 Introduzione](#-introduzione-11)
    - [🔹 1. Gestione dello spazio libero](#-1-gestione-dello-spazio-libero)
      - [Tecniche principali](#tecniche-principali)
        - [a) Bitmap (mappa dei bit)](#a-bitmap-mappa-dei-bit)
        - [b) Lista concatenata di blocchi liberi (Linked free list)](#b-lista-concatenata-di-blocchi-liberi-linked-free-list)
        - [c) Gruppi di blocchi liberi (Grouping)](#c-gruppi-di-blocchi-liberi-grouping)
        - [d) Contatori (Counting)](#d-contatori-counting)
    - [🔹 2. Strutture dati interne: FAT e inode](#-2-strutture-dati-interne-fat-e-inode)
      - [a) FAT – *File Allocation Table*](#a-fat--file-allocation-table)
      - [b) inode (UNIX / Linux)](#b-inode-unix--linux)
    - [🔹 3. Gestione dello spazio libero e allocazione combinata](#-3-gestione-dello-spazio-libero-e-allocazione-combinata)
      - [Extent](#extent)
    - [🔹 4. Journaling e coerenza del file system](#-4-journaling-e-coerenza-del-file-system)
      - [Funzionamento](#funzionamento-6)
      - [Tipi di journaling](#tipi-di-journaling)
      - [Vantaggi](#vantaggi-9)
      - [Svantaggi](#svantaggi-9)
    - [🔹 5. Cache del disco e buffering](#-5-cache-del-disco-e-buffering)
      - [Tipologie di cache](#tipologie-di-cache)
      - [Vantaggi](#vantaggi-10)
      - [Svantaggi](#svantaggi-10)
    - [🔹 6. Verifica e recupero della consistenza](#-6-verifica-e-recupero-della-consistenza)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-13)
  - [Sicurezza e Protezione](#sicurezza-e-protezione)
    - [🔹 Introduzione](#-introduzione-12)
    - [🔹 1. Obiettivi della protezione](#-1-obiettivi-della-protezione)
    - [🔹 2. Domini di protezione](#-2-domini-di-protezione)
      - [Implementazione pratica](#implementazione-pratica)
    - [🔹 3. Matrice di accesso](#-3-matrice-di-accesso)
      - [Esempio](#esempio-1)
      - [Rappresentazioni compatte](#rappresentazioni-compatte)
        - [a) Liste di controllo d’accesso (ACL – Access Control List)](#a-liste-di-controllo-daccesso-acl--access-control-list)
        - [b) Capability List](#b-capability-list)
    - [🔹 4. Meccanismi di controllo accessi](#-4-meccanismi-di-controllo-accessi)
      - [a) File system e permessi UNIX](#a-file-system-e-permessi-unix)
      - [b) Bit speciali](#b-bit-speciali)
    - [🔹 5. Autenticazione e autorizzazione](#-5-autenticazione-e-autorizzazione)
      - [Autenticazione](#autenticazione)
      - [Autorizzazione](#autorizzazione)
    - [🔹 6. Protezione in modalità kernel e utente](#-6-protezione-in-modalità-kernel-e-utente)
    - [🔹 7. Sicurezza dei dati e cifratura](#-7-sicurezza-dei-dati-e-cifratura)
      - [a) Cifratura simmetrica](#a-cifratura-simmetrica)
      - [b) Cifratura asimmetrica](#b-cifratura-asimmetrica)
      - [c) Hash e integrità](#c-hash-e-integrità)
      - [d) Cifratura del file system](#d-cifratura-del-file-system)
    - [🔹 8. Audit e logging](#-8-audit-e-logging)
    - [🔹 9. Backup e ripristino](#-9-backup-e-ripristino)
      - [Tipi principali](#tipi-principali-1)
      - [Buone pratiche](#buone-pratiche)
    - [🧠 Mappa concettuale di sintesi](#-mappa-concettuale-di-sintesi-14)

## Storia dei Sistemi Operativi

---

### 🔹 Introduzione

I sistemi operativi non sono nati con i computer moderni: si sono **evoluti gradualmente** insieme all’hardware e alle esigenze dell’utenza.
Ogni nuova generazione di computer ha richiesto **soluzioni più efficienti per gestire il tempo di calcolo, la memoria e le periferiche**, portando alla nascita di modelli sempre più complessi di gestione dei processi.

Comprendere questa evoluzione permette di capire **perché oggi i sistemi operativi funzionano come li conosciamo** (multitasking, time-sharing, multiprocessore, ecc.), e su quali principi si basano i meccanismi che studiamo a livello tecnico.

---

### 🔹 1. Prima generazione: calcolo manuale e programmazione diretta (anni ’40 – primi ’50)

I primi calcolatori elettronici, come **ENIAC (1946)**, **EDSAC (1949)** e **UNIVAC (1951)**, non avevano un sistema operativo.
Ogni programma veniva **caricato manualmente** in memoria tramite **schede perforate, interruttori o nastri magnetici**, e controllato direttamente dall’operatore.

Caratteristiche principali:

    - Nessuna multiprogrammazione: un solo programma alla volta.
    - Input/Output gestiti manualmente.
    - Il tempo della CPU spesso sprecato durante le operazioni I/O.

💡 **Obiettivo tecnico:** automatizzare il caricamento e l’esecuzione dei programmi per ridurre i tempi morti.

---

### 🔹 2. Seconda generazione: sistemi batch (anni ’50 – metà ’60)

Con l’introduzione dei **mainframe IBM 700 e 1400**, nacquero i **sistemi batch**.
I programmi non venivano più caricati manualmente, ma **raggruppati in lotti (batch)** e **gestiti automaticamente** dal sistema operativo.

#### Funzionamento del sistema batch

1. L’operatore prepara un **nastro batch** contenente una sequenza di job.
2. Il **monitor residente** (precursore del kernel) carica ed esegue ogni job in sequenza.
3. Al termine, il controllo torna al monitor per passare al successivo.

#### Caratteristiche

- **Esecuzione sequenziale non interattiva.**
- Il sistema si occupa di **caricare, eseguire e scaricare** i programmi automaticamente.
- La CPU resta attiva per la maggior parte del tempo → aumento dell’efficienza.

#### Limiti

- Nessuna interazione utente.
- Se un job falliva, l’intera sequenza veniva interrotta.
- Impossibilità di correggere o osservare il comportamento del programma in tempo reale.

Esempio: **IBM 7094** con sistema **FMS (Fortran Monitor System)**, poi **IBSYS**.

---

### 🔹 3. Terza generazione: multiprogrammazione e time-sharing (anni ’60 – ’70)

Con l’introduzione dei **transistor** e dei primi **sistemi multiutente**, i computer divennero più potenti e si iniziò a pensare al calcolo **condiviso**.

#### Multiprogrammazione

La CPU può **tenere più processi in memoria contemporaneamente**, alternandone l’esecuzione quando uno si blocca (es. per I/O).
→ Migliore utilizzo della CPU, riduzione dei tempi morti.

Il **sistema operativo gestisce il carico**, mantenendo una **ready queue** e passando da un processo all’altro tramite **scheduling e context switch**.

#### Time-sharing

Evoluzione naturale della multiprogrammazione:
il tempo della CPU viene **suddiviso in quanti (time slice)** assegnati ciclicamente ai vari utenti o processi.

- Ogni utente percepisce di avere un computer dedicato.
- Nascono i **terminali interattivi**, con input da tastiera e output video.
- Compare la **preemption**, cioè la possibilità di interrompere un processo per assegnare la CPU a un altro.

#### Sistemi rappresentativi

- **CTSS (Compatible Time Sharing System)** del MIT (1961).
- **MULTICS (Multiplexed Information and Computing Service)** (1965):
  → introduce concetti moderni come file system gerarchico, protezione, memoria virtuale.
  → da MULTICS nascerà **UNIX** (1970).

💡 Da qui derivano molti concetti base di tutti i sistemi moderni: processi, shell, file system, permessi e scheduling.

---

### 🔹 4. Quarta generazione: sistemi multiprocessore e distribuiti (anni ’80 – ’90)

L’aumento della potenza e la miniaturizzazione portarono alla diffusione dei **microprocessori** e dei **personal computer**.
Si cominciò a parlare di:

- **sistemi multiprocessore**, con più CPU che cooperano sullo stesso bus o su più core;
- **sistemi distribuiti**, con più macchine interconnesse in rete che condividono risorse.

#### Caratteristiche principali

- Esecuzione parallela di processi su più CPU.
- Introduzione della **cache multipla** e della **coerenza della memoria**.
- Comunicazione tramite **reti locali (LAN)** e **protocolli TCP/IP**.
- Concetti di **trasparenza di rete** e **file system distribuito**.

#### Sistemi notevoli

- UNIX (Berkeley BSD, System V).
- VAX/VMS, OS/2, Windows NT.
- Prime versioni di **Linux** (1991) come evoluzione open source del paradigma UNIX.

---

### 🔹 5. Quinta generazione: sistemi moderni e virtualizzazione (2000 – oggi)

Oggi i sistemi operativi gestiscono ambienti **ibridi, multipiattaforma e virtualizzati**, con risorse distribuite tra più macchine fisiche o virtuali.

#### Tendenze moderne

- **Multicore e hyperthreading:** schedulazione su core logici paralleli.
- **Virtualizzazione:** esecuzione di più sistemi operativi su una singola macchina (VMware, KVM, Hyper-V).
- **Containerizzazione:** isolamento dei processi in ambienti leggeri (Docker, LXC).
- **Cloud computing:** risorse distribuite e scalabili su cluster remoti.
- **Sicurezza avanzata:** sandboxing, SELinux, controllo degli accessi, cifratura integrata.
- **Gestione energetica:** scheduling adattivo e gestione dei consumi per dispositivi mobili.

💡 Il principio fondante resta invariato: il SO deve **astrarre e gestire l’hardware**, fornendo un ambiente sicuro, efficiente e trasparente agli utenti e alle applicazioni.

---

### 🔹 6. Evoluzione dell’hardware e impatto sul SO

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

### 🔹 7. Timeline sintetica

| Periodo       | Caratteristiche                    | Esempi di sistemi       |
| ------------- | ---------------------------------- | ----------------------- |
| **1940–50**   | Nessun OS, programmazione manuale  | ENIAC, UNIVAC           |
| **1950–60**   | Sistemi batch                      | IBM 709, FMS            |
| **1960–70**   | Multiprogrammazione, time-sharing  | CTSS, MULTICS           |
| **1970–90**   | UNIX, multiprocessori, distribuiti | BSD, VAX/VMS            |
| **2000–oggi** | Virtualizzazione, cloud, mobile    | Linux, Windows, Android |

---

### 🧠 Mappa concettuale di sintesi

      ```text
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

## Architettura monoprocessore

---

### 🔹 Introduzione

Un sistema di elaborazione monoprocessore è un sistema dotato di **una sola unità di controllo (CPU)**, responsabile dell’esecuzione sequenziale delle istruzioni di tutti i processi presenti nel sistema.
Tutti i meccanismi di esecuzione, gestione della memoria, I/O e scheduling ruotano attorno alla CPU, che costituisce il **cuore logico del computer**.

Il sistema operativo deve garantire che la CPU sia utilizzata in modo **efficiente** e **ordinato**, coordinando l’accesso alle sue risorse da parte dei processi.
Per comprendere il funzionamento di un sistema operativo, è quindi fondamentale capire **come è organizzata la CPU** e **come essa esegue un programma**.

---

### 🔹 1. Struttura generale della CPU

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

### 🔹 2. Tipologie di registri

I registri rappresentano il livello più veloce e vicino alla CPU.
Ogni registro ha una funzione specifica e insieme formano la base della **microarchitettura del processore**.

#### a) Registri utente

Sono utilizzati direttamente dai programmi per memorizzare dati intermedi o indirizzi.
Esempi tipici:

- **AX, BX, CX, DX** nei processori x86;
- **R0–R31** nei processori RISC (ARM, MIPS, ecc.).

Possono contenere:

- Operandi per le istruzioni aritmetiche.
- Risultati temporanei.
- Indirizzi di memoria (es. puntatori o indici di array).

#### b) Registri di controllo e di stato

Non sono direttamente accessibili ai programmi utente: servono al **sistema operativo** e all’hardware per gestire l’esecuzione.

I principali sono:

- **Program Counter (PC)** → contiene l’indirizzo della prossima istruzione da eseguire.
- **Instruction Register (IR)** → mantiene l’istruzione attualmente in esecuzione.
- **Stack Pointer (SP)** → punta alla cima dello stack del processo.
- **Status Register / Flag Register** → contiene i flag (zero, carry, overflow, interrupt enable, ecc.) che indicano lo stato del processore.

#### c) Registri interni (buffer)

Usati per collegare la CPU con la memoria e i dispositivi I/O:

- **MAR (Memory Address Register):** contiene l’indirizzo della cella di memoria da leggere o scrivere.
- **MBR (Memory Buffer Register):** contiene i dati letti o da scrivere in memoria.

---

### 🔹 3. Ciclo di esecuzione: Fetch–Decode–Execute

Ogni programma è composto da una sequenza di **istruzioni macchina** che la CPU deve eseguire.
Il processo con cui la CPU legge ed elabora le istruzioni è chiamato **ciclo di fetch–decode–execute**.

#### a) Fase di Fetch (prelievo)

- Il **Program Counter (PC)** indica l’indirizzo della prossima istruzione in memoria.
- L’indirizzo viene copiato nel **MAR** e la CPU richiede la lettura alla memoria principale.
- L’istruzione viene caricata nel **Instruction Register (IR)**.
- Il PC viene incrementato (salvo istruzioni di salto).

#### b) Fase di Decode (decodifica)

- L’unità di controllo interpreta il contenuto dell’IR e determina quale operazione deve essere eseguita.
- Vengono identificati gli operandi e le modalità di indirizzamento (diretto, indiretto, immediato, indicizzato...).

#### c) Fase di Execute (esecuzione)

- L’ALU esegue l’operazione richiesta (aritmetica o logica).
- Se necessario, i risultati vengono scritti nei registri o in memoria.
- Viene aggiornato lo **Status Register** in base al risultato (es. flag di overflow o zero).

Questo ciclo si ripete continuamente, miliardi di volte al secondo, scandito dal **clock** del processore.

---

### 🔹 4. Modalità di indirizzamento

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

### 🔹 5. Ciclo di istruzione e ruolo del sistema operativo

Durante il ciclo di esecuzione, la CPU può essere **interrotta** da eventi esterni o interni (interrupt, eccezioni, trap).
Quando ciò accade:

1. La CPU sospende il ciclo in corso.
2. Salva lo stato corrente del processo (registri, PC, flag) nel PCB.
3. Passa al **kernel mode** e invoca il gestore dell’interrupt.
4. Dopo la gestione, ripristina il contesto e riprende l’esecuzione.

Questo meccanismo consente al sistema operativo di **coordinare processi multipli** anche su una singola CPU, simulando il parallelismo attraverso la **commutazione rapida del contesto (context switch)**.

---

### 🔹 6. Categorie di istruzioni macchina

Le istruzioni che una CPU può eseguire appartengono a diverse categorie, ognuna con scopi diversi:

| Categoria               | Esempio                   | Funzione                                       |
| ----------------------- | ------------------------- | ---------------------------------------------- |
| **Dati**                | `LOAD`, `STORE`, `MOV`    | Trasferimento dati tra memoria e registri      |
| **Aritmetiche/logiche** | `ADD`, `SUB`, `AND`, `OR` | Calcoli e operazioni bitwise                   |
| **Controllo di flusso** | `JMP`, `CALL`, `RET`      | Salti, chiamate a funzioni, ritorni            |
| **Gestione I/O**        | `IN`, `OUT`               | Comunicazione con dispositivi                  |
| **Sistema**             | `INT`, `HLT`              | Trap, interruzioni, arresti, cambi di modalità |

---

### 🔹 7. Interazione CPU – Memoria – I/O

La CPU non lavora isolata: per funzionare deve comunicare costantemente con:

- **la memoria principale (RAM)** per caricare istruzioni e dati;
- **i dispositivi di I/O** per leggere e scrivere dati.

Questa comunicazione avviene tramite **bus**:

1. **Bus dati** → trasporta i valori binari.
2. **Bus indirizzi** → indica dove leggere/scrivere.
3. **Bus di controllo** → gestisce segnali di sincronizzazione (read/write, interrupt, clock).

Il sistema operativo regola questo flusso e **decide quale processo può usare la CPU**, realizzando così il principio di **multiprogrammazione**.

---

### 🧠 Mappa concettuale di sintesi

      ```text
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

## Memorie + Sistema Operativo

---

### 🔹 Introduzione generale

Ogni sistema di elaborazione si fonda su un principio fondamentale: **la CPU elabora i dati molto più rapidamente di quanto la memoria o i dispositivi esterni possano fornirli**.
Per garantire efficienza e continuità nell’esecuzione dei programmi, è necessario organizzare la memoria in **più livelli** con caratteristiche diverse di **velocità, costo e capacità**.

Parallelamente, il **Sistema Operativo (SO)** si occupa di **gestire e coordinare** l’uso di queste memorie, garantendo che i processi:

- abbiano accesso sicuro e controllato ai dati;
- possano convivere in memoria senza conflitti;
- ottimizzino l’uso delle risorse fisiche disponibili.

Comprendere la **gerarchia delle memorie** e il **ruolo del SO** nella loro gestione è la base per capire la logica di tutto il sistema informatico.

---

### 🔹 1. Gerarchia delle memorie

Il concetto di **gerarchia di memoria** nasce per conciliare tre fattori in conflitto:

1. **Velocità** (quanto rapidamente si accede ai dati),
2. **Costo per bit** (quanto costa realizzarla),
3. **Capacità** (quanti dati può contenere).

La regola generale è:

> più la memoria è vicina alla CPU → più è veloce → più è costosa → meno è capiente.

#### Struttura a livelli

| Livello                | Tipo di memoria    | Tempo di accesso | Capacità   | Gestione               |
| ---------------------- | ------------------ | ---------------- | ---------- | ---------------------- |
| **L1 / L2 / L3**       | Cache              | nanosecondi      | KB–MB      | Hardware (trasparente) |
| **RAM**                | Memoria principale | decine di ns     | GB         | Sistema operativo      |
| **Memoria secondaria** | SSD / HDD          | millisecondi     | TB         | Sistema operativo      |
| **Memoria terziaria**  | Nastri, cloud      | secondi          | molto alta | Manuale / batch        |

---

### 🔹 2. Tipologie di memoria

#### a) Memoria primaria

Include **cache e RAM**.
È **volatile**: il contenuto si perde allo spegnimento.
Contiene:

- i programmi in esecuzione,
- i dati attivi,
- le strutture di controllo del sistema operativo.

#### b) Memoria secondaria

Comprende **dischi magnetici** e **unità a stato solido (SSD)**.
Non è volatile e serve per **conservare permanentemente** programmi e dati.

#### c) Memoria terziaria e virtuale

Usata per backup o archiviazione (nastri, cloud, optical storage).
La **memoria virtuale** è una tecnica logica del SO che permette di **estendere la memoria principale** utilizzando parte del disco (swap area).

---

### 🔹 3. Memoria cache

La **cache** è una memoria ad altissima velocità che funge da **ponte tra CPU e RAM**, riducendo il tempo medio di accesso ai dati.

#### Principio di località

La cache sfrutta due proprietà fondamentali dei programmi:

- **Località temporale:** se un dato è stato usato di recente, probabilmente sarà usato di nuovo.
- **Località spaziale:** se è stato usato un dato in memoria, probabilmente saranno usati anche quelli vicini.

#### Organizzazione

I dati vengono trasferiti in blocchi chiamati **linee di cache**.
Ogni linea contiene una copia di una parte di memoria principale.
Quando la CPU richiede un indirizzo:

1. Se il dato è già in cache → **cache hit** (accesso veloce).
2. Se non è presente → **cache miss** (dato recuperato dalla RAM).

#### Politiche di scrittura

- **Write-through:** ogni modifica in cache viene immediatamente scritta in RAM.
  → più sicura ma lenta.
- **Write-back:** la scrittura in RAM avviene solo quando il blocco viene rimpiazzato.
  → più veloce, ma richiede coerenza.

---

### 🔹 4. Mappatura e sostituzione in cache

#### Tipi di mappatura

| Tipo                                       | Descrizione                                             | Caratteristica                     |
| ------------------------------------------ | ------------------------------------------------------- | ---------------------------------- |
| **Diretta**                                | Ogni blocco di memoria mappa in una sola linea di cache | semplice ma può generare conflitti |
| **Associativa**                            | Un blocco può occupare qualsiasi linea                  | flessibile ma costosa              |
| **Associativa a gruppi (set-associative)** | Compromesso: la cache è divisa in gruppi di linee       | bilanciamento prestazioni/costo    |

#### Politiche di rimpiazzo

Quando la cache è piena e serve spazio:

- **LRU (Least Recently Used):** elimina il blocco usato meno di recente.
- **FIFO (First In First Out):** elimina il blocco più vecchio.
- **Random:** scelta casuale, semplice ma non ottimale.

---

### 🔹 5. Ruolo del Sistema Operativo nella memoria

Il SO **non gestisce direttamente la cache** (controllata dall’hardware), ma ha il pieno controllo su:

- **Memoria principale (RAM)**
  → allocazione e rilascio per i processi.
- **Memoria secondaria (swap)**
  → gestione della memoria virtuale.
- **Protezione**
  → impedisce che un processo acceda alla memoria di un altro.

#### Meccanismi principali

1. **Rilocazione dinamica:** traduzione indirizzi logici → fisici.
2. **Protezione:** verifica degli indirizzi validi per ogni processo.
3. **Condivisione:** possibilità di usare la stessa area di memoria (es. librerie condivise).
4. **Organizzazione logica:** gestione dello spazio degli indirizzi dei processi.
5. **Organizzazione fisica:** mappatura su memoria e swap.

---

### 🔹 6. Struttura logica del Sistema Operativo

Il sistema operativo può essere visto come un insieme di **moduli cooperanti**, organizzati a livelli di astrazione.

#### a) Kernel

È il **cuore del sistema operativo**, sempre residente in memoria.
Si occupa di:

- Gestione dei processi e scheduling.
- Gestione della memoria principale e virtuale.
- Gestione del file system.
- Gestione delle interruzioni e dei dispositivi.

#### b) Shell e interfaccia utente

Fornisce i mezzi per interagire con il sistema operativo (prompt, GUI, comandi).
È un **programma utente privilegiato**, ma non parte del kernel.

#### c) Livelli di astrazione del SO

| Livello                      | Funzione principale                |
| ---------------------------- | ---------------------------------- |
| **1 – Hardware**             | CPU, memoria, dispositivi fisici   |
| **2 – Microkernel / Kernel** | Gestione risorse di base           |
| **3 – Servizi di sistema**   | File system, I/O, processi         |
| **4 – Librerie e API**       | Interfaccia per i programmi utente |
| **5 – Utente / Shell**       | Interazione e comandi              |

In sistemi didattici o teorici, la stratificazione può arrivare fino a 13 livelli (da hardware fino all’utente finale), dove ogni livello offre servizi a quello superiore e si appoggia su quello inferiore.

---

### 🔹 7. Kernel vs Microkernel

#### Kernel monolitico

Tutte le funzioni (file system, driver, memoria, I/O, ecc.) sono integrate in un unico grande blocco eseguibile in modalità kernel.

- **Pro:** alte prestazioni, accesso diretto alle risorse.
- **Contro:** scarsa modularità, manutenzione difficile, vulnerabile a crash globali.

#### Microkernel

Contiene solo le funzioni essenziali (gestione processi, memoria, comunicazione).
Tutto il resto (driver, file system, GUI) gira in **user mode** come processi separati.

- **Pro:** alta affidabilità e isolamento dei moduli.
- **Contro:** comunicazioni più lente (messaggi inter-processo).

Esempi:

- Kernel monolitici → Linux, BSD.
- Microkernel → MINIX, Mach (base di macOS).

---

### 🧠 Mappa concettuale di sintesi

      ```text
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

## Interrupt e I/O

---

### 🔹 Introduzione

Un sistema operativo deve essere in grado di **gestire eventi asincroni** provenienti sia dall’hardware sia dal software, garantendo che la CPU non rimanga inattiva e che il flusso di esecuzione dei programmi proceda in modo corretto.
Questo comportamento è reso possibile grazie agli **interrupt**, meccanismi che permettono al processore di **interrompere temporaneamente l’esecuzione di un programma** per gestire un evento più urgente.

Gli interrupt sono quindi il **mezzo fondamentale di comunicazione tra CPU, sistema operativo e periferiche di I/O**.
Capire come funzionano significa comprendere il cuore del meccanismo reattivo del sistema operativo.

---

### 🔹 1. Concetto di interrupt

Un **interrupt** è un segnale che richiede al processore di sospendere l’attività corrente e di passare temporaneamente all’esecuzione di una **routine di servizio** (Interrupt Handler o Interrupt Service Routine, ISR).
Dopo aver gestito l’evento, il processore **riprende esattamente dal punto in cui era stato interrotto**.

Questo meccanismo permette al sistema di:

- reagire rapidamente a eventi esterni (es. arrivo dati da tastiera o rete);
- gestire errori o eccezioni interne;
- evitare che la CPU sprechi tempo in attesa di dispositivi lenti.

---

### 🔹 2. Tipologie di interrupt

Gli interrupt si classificano in base all’origine e alla modalità di generazione.

#### a) Interrupt hardware

Generati dai dispositivi esterni per segnalare eventi come:

- completamento di un’operazione di I/O;
- errori hardware;
- richieste da timer o dispositivi di rete.

Esempio:
una stampante invia un segnale di interrupt per indicare che ha terminato la stampa.

#### b) Interrupt software

Generati da istruzioni specifiche del programma (es. `INT n` su x86) o da **eccezioni** come divisione per zero o accesso a memoria non valida.
Sono utilizzati dal sistema operativo per gestire le **system call** e i **trap**.

#### c) Classificazione funzionale

| Tipo          | Origine                               | Esempi                 | Descrizione                           |
| ------------- | ------------------------------------- | ---------------------- | ------------------------------------- |
| **Sincroni**  | Durante l’esecuzione di un’istruzione | Trap, eccezioni, fault | Dipendono dal programma in corso      |
| **Asincroni** | Da eventi esterni alla CPU            | Timer, I/O completato  | Indipendenti dal flusso di istruzioni |

---

### 🔹 3. Meccanismo di gestione di un interrupt

Quando si verifica un interrupt, la CPU esegue una sequenza precisa di operazioni per garantire che l’intervento sia gestito in modo sicuro e coerente.

#### Fasi principali

1. **Rilevamento dell’interrupt**
   Il processore verifica a ogni ciclo di clock se è presente un segnale di interrupt attivo.

2. **Salvataggio del contesto**
   La CPU salva in modo automatico le informazioni necessarie per riprendere il processo interrotto:

   - Program Counter (PC)
   - Registri di stato
   - Altri registri generali (salvati dal kernel o dall’handler)

3. **Cambio di modalità**
   La CPU passa da **user mode** a **kernel mode** per poter eseguire istruzioni privilegiate.

4. **Identificazione della causa**
   Tramite la **tabella vettore degli interrupt**, la CPU individua quale evento ha generato l’interrupt e salta alla **Interrupt Service Routine** corrispondente.

5. **Esecuzione dell’handler**
   L’ISR gestisce l’evento (es. legge un dato dal dispositivo, aggiorna un buffer, segnala la fine dell’I/O).

6. **Ripristino del contesto**
   Dopo la gestione, il sistema ripristina lo stato precedente del processo e ritorna al punto esatto in cui era stato interrotto.

---

### 🔹 4. Vettore degli interrupt

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

### 🔹 5. Gestione sequenziale e annidata degli interrupt

#### a) Gestione sequenziale

In modalità **sequenziale**, la CPU accetta un nuovo interrupt solo quando ha terminato di gestire quello corrente.
→ soluzione semplice, ma poco efficiente per sistemi con eventi frequenti.

#### b) Gestione annidata

In modalità **annidata**, un interrupt può essere interrotto da un altro di **priorità superiore**.
Serve una **priorità gerarchica** per evitare conflitti e perdita di eventi.

Esempio:

- Un interrupt della tastiera può interrompere un processo in esecuzione.
- Ma un interrupt del timer (più urgente) può a sua volta interrompere l’handler della tastiera.

Il kernel gestisce una **maschera di priorità** per abilitare o disabilitare certi interrupt in momenti specifici.

---

### 🔹 6. Context switch e interrupt

Ogni interrupt implica un **context switch** temporaneo:
la CPU deve salvare lo stato del processo corrente per poterlo ripristinare successivamente.

Questo meccanismo è analogo a quello utilizzato dallo **scheduler** per passare da un processo all’altro, ma:

- nel caso dello scheduler → il cambio è pianificato (es. time quantum scaduto);
- nel caso dell’interrupt → è **improvviso e asincrono**.

Un interrupt quindi **non solo segnala un evento**, ma è anche **il meccanismo tecnico con cui il kernel ottiene il controllo della CPU**.

---

### 🔹 7. Tecniche di I/O

Le operazioni di I/O (Input/Output) rappresentano la comunicazione tra CPU e dispositivi periferici.
Poiché i dispositivi sono molto più lenti della CPU, il sistema deve adottare tecniche che massimizzino l’efficienza.

#### a) I/O programmato

La CPU interroga continuamente il dispositivo (polling) fino a che non è pronto.
→ semplice ma inefficiente: la CPU resta bloccata in attesa.

#### b) I/O con interrupt

Il dispositivo genera un interrupt quando è pronto o ha completato un’operazione.
→ la CPU nel frattempo può eseguire altri processi.
→ metodo standard nei sistemi moderni.

#### c) I/O con DMA (Direct Memory Access)

Un **DMA controller** trasferisce i dati direttamente tra memoria e dispositivo, senza intervento della CPU per ogni byte.
→ riduce drasticamente l’overhead della CPU.
→ usato per dischi, schede di rete e audio.

---

### 🔹 8. Ruolo del sistema operativo negli interrupt e nell’I/O

Il sistema operativo gestisce gli interrupt come **porte di ingresso verso il kernel**:

- Decide **quali interrupt abilitare** (priorità, maschere).
- Fornisce le **routine ISR** appropriate.
- Coordina i **driver dei dispositivi** che interagiscono con l’hardware.
- Gestisce **code di I/O** e **sincronizzazione** dei processi in attesa.

L’insieme di queste funzioni costituisce il **sottosistema di I/O del kernel**, base della comunicazione CPU–dispositivi.

---

### 🧠 Mappa concettuale di sintesi

      ```text
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

## Gestione I/O (I)

### 🔹 Introduzione

L’**Input/Output (I/O)** rappresenta la parte del sistema operativo che gestisce la **comunicazione tra la CPU e i dispositivi periferici** (dischi, tastiere, stampanti, reti, ecc.).
Questa componente è essenziale, poiché consente al sistema di **interagire con il mondo esterno**, trasferendo dati tra memoria e dispositivi.

L’I/O è intrinsecamente **più lento** rispetto alla CPU e alla memoria: per questo motivo, uno dei compiti fondamentali del sistema operativo è **ottimizzare il tempo di attesa** e massimizzare la **concorrenza tra calcolo e trasferimento dati**.

In generale, il sottosistema I/O si occupa di:

- nascondere le differenze tra i vari dispositivi;
- gestire errori e stati;
- ottimizzare l’uso delle risorse hardware;
- fornire un’interfaccia uniforme ai processi utente.

---

### 🔹 1. Architettura del sottosistema I/O

Il sistema operativo organizza la gestione dell’I/O secondo una **struttura multilivello**, che va dal software applicativo fino al dispositivo fisico.

#### Livelli principali

1. **Livello utente (User Level):**

   - L’applicazione interagisce con il sistema tramite **chiamate di sistema (system call)** come `read()`, `write()`, `open()`, `close()`.
   - Il programmatore non si occupa dei dettagli hardware: la gestione è delegata al kernel.

2. **Livello kernel (Kernel Level):**

   - Include il **file system**, i **device driver**, la **gestione buffer**, e il **scheduling dell’I/O**.
   - Si occupa di tradurre le richieste utente in operazioni fisiche sul dispositivo.

3. **Livello hardware:**

   - Composto dai **controller dei dispositivi**, che comunicano direttamente con la CPU e la memoria.
   - Ogni controller gestisce uno o più dispositivi fisici.

#### Flusso generale

      ```text

      Programma utente
         ↓
      System call (es. read/write)
         ↓
      Driver dispositivo
         ↓
      Controller hardware
         ↓
      Dispositivo fisico (disk, printer, etc.)

      ```

Il sistema operativo fa da **intermediario e coordinatore**, fornendo un livello di astrazione che rende uniforme l’accesso a dispositivi anche molto diversi tra loro.

---

### 🔹 2. Componenti dell’I/O

#### a) Device Controller

È un’unità hardware che funge da **interfaccia tra la CPU e il dispositivo fisico**.
Ogni controller gestisce uno o più dispositivi dello stesso tipo (es. un controller SATA per i dischi, un controller USB per le periferiche esterne).

- *Funzioni principali:**

- interpretare i comandi provenienti dal driver;
- gestire i registri di stato, controllo e dati;
- segnalare alla CPU il completamento di un’operazione (tramite interrupt).

#### b) Device Driver

È un modulo software (parte del kernel) che **traduce le richieste generiche del sistema operativo in comandi specifici per il controller**.
Ogni tipo di dispositivo ha il proprio driver.

- *Responsabilità principali:**

- inviare comandi al controller;
- gestire gli interrupt di completamento o errore;
- fornire un’interfaccia standard al kernel (es. funzioni `read()`, `write()`).

Il driver rappresenta il punto di contatto diretto tra **software e hardware**, e deve rispettare precise specifiche per interagire con il kernel.

---

### 🔹 3. Tecniche di comunicazione CPU–Dispositivo

Le operazioni di I/O possono essere realizzate con diverse modalità, che variano per **grado di coinvolgimento della CPU**.

#### a) I/O programmato (Polling)

- La CPU controlla periodicamente lo stato del dispositivo leggendo un **registro di stato**.
- Quando il dispositivo è pronto, la CPU trasferisce manualmente i dati.

- *Vantaggi:**

- Implementazione semplice.

- *Svantaggi:**

- La CPU resta impegnata in attesa del dispositivo → **spreco di tempo di calcolo**.
- Poco efficiente per dispositivi lenti.

#### b) I/O con interrupt

- Il dispositivo genera un **interrupt** quando termina un’operazione o è pronto per trasferire dati.
- La CPU può dedicarsi ad altro nel frattempo.

- *Funzionamento:**

1. Il processo richiede un’operazione I/O.
2. Il driver configura il controller e mette il processo in attesa (stato *blocked*).
3. Il dispositivo esegue l’operazione autonomamente.
4. Al completamento, il controller genera un interrupt → il kernel risveglia il processo.

- *Vantaggi:**

- La CPU non resta inattiva.
- Maggiore efficienza e reattività.

- *Svantaggi:**

- Overhead dovuto alla gestione dell’interrupt (context switch).
- Maggiore complessità del kernel.

#### c) I/O con DMA (Direct Memory Access)

Il **DMA** è un meccanismo hardware che permette al controller del dispositivo di **accedere direttamente alla memoria**, senza passare dalla CPU per ogni byte trasferito.

- *Funzionamento:**

1. La CPU prepara la richiesta I/O (indirizzo sorgente, destinazione, quantità).
2. Il **DMA controller** gestisce il trasferimento autonomamente.
3. Al termine, genera un **interrupt** per segnalare il completamento.

- *Vantaggi:**

- Drastica riduzione del carico sulla CPU.
- Prestazioni elevate per trasferimenti di grandi dimensioni (es. disco → RAM).

- *Svantaggi:**

- Hardware più complesso.
- Richiede sincronizzazione tra CPU e DMA per evitare conflitti sulla memoria.

---

### 🔹 4. Bufferizzazione

La **bufferizzazione (buffering)** serve a **compensare le differenze di velocità** tra CPU, memoria e dispositivi di I/O.
Un **buffer** è una zona di memoria temporanea usata per accumulare dati in transito.

#### Tipi di buffer

##### a) Single Buffer

Un solo buffer tra dispositivo e processo.
→ Quando il buffer è pieno, il processo viene sospeso finché non viene svuotato.

##### b) Double Buffer

Due buffer usati in alternanza:

- mentre uno viene riempito, l’altro viene svuotato.
  → Migliora la sovrapposizione tra calcolo e I/O.

##### c) Circular Buffer

Più buffer in sequenza collegati circolarmente (FIFO).
→ Usato in sistemi ad alto throughput (streaming, rete).

#### Vantaggi

- Aumenta il parallelismo tra CPU e I/O.
- Riduce i tempi morti del dispositivo.

#### Svantaggi

- Maggiore uso di memoria.
- Necessità di gestione sincronizzata (accesso concorrente).

---

### 🔹 5. Spooling

Il termine **spooling** (Simultaneous Peripheral Operation On-Line) indica una **tecnica di gestione concorrente** di dispositivi di I/O condivisi, come stampanti o unità disco.

#### Funzionamento

- Le richieste I/O non vengono servite immediatamente ma **accodate in un’area di memoria o su disco (spool area)**.
- Un **demone (spooler)** legge periodicamente la coda e le esegue in ordine.

- *Esempio classico:**
Più utenti inviano stampe → i file vengono messi in coda → lo spooler li stampa in sequenza.

#### Vantaggi

- Permette l’uso **condiviso** di dispositivi non rientranti (non multitasking).
- Evita blocchi del sistema in attesa del completamento di un I/O.
- Migliora la **concorrenza e il throughput complessivo**.

---

### 🔹 6. Struttura software del sistema I/O

Il sottosistema I/O è organizzato su più livelli, dal più astratto (software utente) al più vicino all’hardware.

#### Livelli tipici

| Livello                 | Funzione principale                              |
| ----------------------- | ------------------------------------------------ |
| **Software utente**     | Chiamate di sistema (`read`, `write`)            |
| **Software di sistema** | File system e librerie I/O                       |
| **Device driver**       | Traduzione comandi generici in comandi specifici |
| **Interrupt handler**   | Gestione segnali di completamento o errore       |
| **Controller**          | Comunicazione diretta con il dispositivo fisico  |

Ogni livello comunica con il successivo tramite **interfacce standard**, rendendo il sistema modulare e facilmente estendibile.

---

### 🧠 Mappa concettuale di sintesi

      ```text

      GESTIONE I/O (I)
      │
      ├── Architettura
      │   ├─ Livello utente → system call (read/write)
      │   ├─ Livello kernel → driver, buffer, scheduler
      │   └─ Livello hardware → controller, device
      │
      ├── Componenti
      │   ├─ Device controller → gestisce registri e interrupt
      │   └─ Driver → traduce richieste OS → hardware
      │
      ├── Tecniche I/O
      │   ├─ Programmato → polling, CPU attiva
      │   ├─ Interrupt-driven → CPU notificata
      │   └─ DMA → accesso diretto memoria
      │
      ├── Buffering
      │   ├─ Single → uno solo
      │   ├─ Double → due alternati
      │   └─ Circular → multipli (FIFO)
      │
      ├── Spooling
      │   ├─ Accodamento richieste I/O
      │   ├─ Gestito da spooler
      │   └─ Esempio → stampa multipla
      │
      └── Struttura software
         ├─ Utente → system call
         ├─ Kernel → driver e interrupt handler
         └─ Hardware → controller dispositivo

      ```

## Gestione I/O (II)

### 🔹 Introduzione

La seconda parte della gestione dell’I/O approfondisce **le strategie di ottimizzazione e di affidabilità** nella gestione dei dispositivi di massa, in particolare i **dischi** (magnetici e SSD).
Qui il sistema operativo non si limita più a coordinare le operazioni di lettura e scrittura, ma deve anche:

- **ordinare e schedulare le richieste di I/O** per ridurre i tempi di accesso al disco;
- **distribuire e replicare i dati** per aumentare l’affidabilità (RAID);
- **adattarsi alla diversa natura fisica** dei dispositivi (HDD vs SSD);
- **gestire i dispositivi in ambiente Linux**, attraverso il sottosistema dei **block device**.

---

### 🔹 1. Struttura fisica e tempi di accesso al disco

Un **disco magnetico (HDD)** è composto da piatti rotanti rivestiti di materiale magnetico, divisi in **tracce** e **settori**.
Il **braccio di lettura/scrittura** si sposta tra le tracce, e i dati vengono letti quando il settore desiderato passa sotto la testina.

#### Tempi di accesso

Il tempo totale per soddisfare una richiesta di lettura/scrittura si compone di tre elementi:

1. **Seek time (T_seek):** tempo necessario per spostare la testina sulla traccia corretta.
   → di solito tra 3 e 10 ms.

2. **Rotational latency (T_rot):** tempo di attesa finché il settore desiderato passa sotto la testina.
   → dipende dalla velocità di rotazione del disco (es. 7200 rpm ≈ 4,2 ms in media).

3. **Transfer time (T_trans):** tempo necessario per leggere o scrivere i dati del settore.
   → molto più breve (pochi μs).

[
T_{accesso} = T_{seek} + T_{rot} + T_{trans}
]

Poiché i primi due contributi sono dominanti, **minimizzare gli spostamenti della testina** è l’obiettivo principale degli algoritmi di **disk scheduling**.

---

### 🔹 2. Scheduling dei dischi

Il **disk scheduler** ordina le richieste di I/O pendenti in modo da ridurre i movimenti della testina e migliorare il throughput.
Ogni algoritmo adotta un criterio diverso per decidere **quale richiesta servire per prima**.

#### a) FCFS – *First Come, First Served*

Le richieste vengono servite nell’ordine di arrivo.
→ Semplice ma inefficiente: la testina può muoversi continuamente avanti e indietro.

- *Vantaggio:** equità.
- *Svantaggio:** tempi medi di accesso elevati.

---

#### b) SSTF – *Shortest Seek Time First*

Viene servita la richiesta **più vicina alla posizione corrente** della testina.
→ Riduce i tempi medi di spostamento.

- *Problema:** può causare **starvation** per richieste lontane se continuano ad arrivare richieste vicine.

---

#### c) SCAN (Elevator Algorithm)

La testina si muove in una direzione servendo tutte le richieste fino al bordo del disco, poi inverte la direzione e serve le richieste nell’altro senso.

- *Analogia:** come un ascensore che sale e scende servendo i piani nell’ordine.

- *Vantaggi:**

- Tempi medi più stabili.
- Nessuna starvation sistematica.

- *Svantaggi:**

- Le richieste alle estremità del disco attendono più a lungo.

---

#### d) C-SCAN – *Circular SCAN*

Variante di SCAN: la testina serve solo in una direzione (es. da inizio a fine disco) e poi **torna rapidamente all’inizio senza servire richieste nel ritorno**.
→ Garantisce tempi di attesa più uniformi.

---

#### e) LOOK e C-LOOK

Sono varianti ottimizzate di SCAN e C-SCAN:

- La testina **non si spinge fino ai bordi del disco**, ma si ferma all’ultima richiesta nella direzione corrente.
- Riduce ulteriormente i movimenti inutili.

---

#### f) Confronto generale

| Algoritmo         | Tipo            | Vantaggi                  | Svantaggi                     |
| ----------------- | --------------- | ------------------------- | ----------------------------- |
| **FCFS**          | Non ottimizzato | Semplice, equo            | Movimenti elevati             |
| **SSTF**          | Ottimizzato     | Buon compromesso          | Possibile starvation          |
| **SCAN**          | Bidirezionale   | Buon throughput           | Latenza ai bordi              |
| **C-SCAN**        | Circolare       | Tempi uniformi            | Ritorno a vuoto               |
| **LOOK / C-LOOK** | Ottimizzati     | Evitano movimenti inutili | Più complessi da implementare |

Nei sistemi moderni, vengono spesso utilizzati **scheduler ibridi**, che combinano logiche simili a SSTF e C-LOOK con priorità dinamiche e bilanciamento della latenza.

---

### 🔹 3. RAID – Redundant Array of Independent Disks

Il **RAID** è una tecnica che combina più dischi fisici in un unico insieme logico, con l’obiettivo di migliorare **prestazioni**, **affidabilità** o **entrambe**.

#### Motivazioni

- **Prestazioni:** letture/scritture parallele su più dischi.
- **Affidabilità:** ridondanza dei dati → tolleranza ai guasti.
- **Capacità logica:** unione di più dischi in un volume unico.

---

#### Livelli principali

| Livello           | Descrizione                                                    | Vantaggi                                 | Svantaggi                          |
| ----------------- | -------------------------------------------------------------- | ---------------------------------------- | ---------------------------------- |
| **RAID 0**        | *Striping* → suddivide i dati tra i dischi senza ridondanza    | Massime prestazioni                      | Nessuna tolleranza ai guasti       |
| **RAID 1**        | *Mirroring* → copia identica su due dischi                     | Alta affidabilità                        | Capacità dimezzata                 |
| **RAID 5**        | *Striping con parità distribuita* → parità su dischi alternati | Buon equilibrio prestazioni/affidabilità | Penalità in scrittura              |
| **RAID 6**        | Come RAID 5 ma con doppia parità                               | Resiste a 2 guasti simultanei            | Maggiore overhead                  |
| **RAID 10 (1+0)** | Mirroring + striping                                           | Ottimo bilanciamento                     | Costo elevato (richiede ≥4 dischi) |

#### Considerazioni

- RAID 0 → performance pura (es. cache temporanee).
- RAID 1 → sistemi critici (database, server).
- RAID 5/6 → file server e NAS.
- RAID 10 → ambienti enterprise ad alte prestazioni.

---

### 🔹 4. HDD vs SSD

Negli ultimi anni, gli **SSD (Solid State Drive)** hanno sostituito in gran parte i dischi magnetici tradizionali, ma la loro gestione a livello di sistema operativo differisce notevolmente.

#### HDD (Hard Disk Drive)

- Accesso meccanico (testina + piatti).
- Tempi dominati da seek e rotazione.
- Prestazioni influenzate dalla posizione fisica dei dati.
- Usura trascurabile ma sensibile agli urti.

#### SSD (Solid State Drive)

- Nessuna parte meccanica → accesso **completamente elettronico**.
- Tempi di accesso costanti (nessun seek time).
- Prestazioni molto superiori in lettura casuale.
- Numero limitato di cicli di scrittura (usura celle).

#### Implicazioni per il sistema operativo

- Gli algoritmi di **disk scheduling** diventano meno rilevanti (nessun movimento testina).
- I driver devono gestire **wear leveling**, **garbage collection** e **comandi TRIM** per mantenere prestazioni costanti.
- Le operazioni di I/O vengono spesso accodate in modo asincrono per massimizzare la concorrenza.

---

### 🔹 5. Gestione I/O in Linux

Linux gestisce l’I/O attraverso una struttura modulare basata su **device file** e **driver a due categorie principali**:

| Tipo                  | Descrizione                                   | Esempi                   |
| --------------------- | --------------------------------------------- | ------------------------ |
| **Character devices** | Scambio dati byte per byte, flusso continuo   | Terminali, porte seriali |
| **Block devices**     | Accesso a blocchi di dati di dimensione fissa | Dischi, SSD, memorie USB |

Ogni dispositivo è rappresentato da un **file speciale** in `/dev`, identificato da due numeri:

- **Major number:** identifica il driver associato.
- **Minor number:** identifica l’istanza specifica del dispositivo.

#### Sottosistema del block I/O

Ogni richiesta di I/O passa attraverso:

1. **Page cache / buffer cache**
2. **Elevator scheduler (CFQ, deadline, noop, bfq)**
3. **Driver del dispositivo**
4. **Controller hardware**

Linux offre più **scheduler I/O** selezionabili (es. con `cat /sys/block/sda/queue/scheduler`):

- `noop` → semplice FIFO (ottimo per SSD)
- `deadline` → priorità temporali per evitare starvation
- `cfq` → fairness tra processi (per HDD tradizionali)
- `bfq` → bilanciamento ottimizzato per carichi misti

---

### 🧠 Mappa concettuale di sintesi

      ```text
      GESTIONE I/O (II)
      │
      ├── Struttura disco
      │   ├─ Tracce e settori
      │   └─ T_accesso = T_seek + T_rot + T_trans
      │
      ├── Scheduling dischi
      │   ├─ FCFS → ordine di arrivo
      │   ├─ SSTF → minimo spostamento
      │   ├─ SCAN / C-SCAN → movimento “ascensore”
      │   └─ LOOK / C-LOOK → ottimizzati
      │
      ├── RAID
      │   ├─ RAID 0 → striping, veloce
      │   ├─ RAID 1 → mirroring, sicuro
      │   ├─ RAID 5 → parità distribuita
      │   ├─ RAID 6 → doppia parità
      │   └─ RAID 10 → mirroring + striping
      │
      ├── HDD vs SSD
      │   ├─ HDD → meccanico, lento, seek time
      │   ├─ SSD → elettronico, rapido, usura celle
      │   └─ TRIM e wear leveling
      │
      └── I/O in Linux
         ├─ Character / Block device
         ├─ Major e minor number
         ├─ Scheduler: noop, deadline, cfq, bfq
         └─ Stack I/O → cache → scheduler → driver → controller

      ```

## Processi

---

### 🔹 Introduzione

Uno dei compiti fondamentali di un sistema operativo è la **gestione dei processi**, cioè l’insieme delle attività in esecuzione nel sistema.
Un processo rappresenta l’**unità fondamentale di esecuzione**: è un programma “vivo”, in corso di esecuzione, con un proprio stato, risorse assegnate e contesto operativo.

Il SO deve poter:

- **creare**, **schedulare** e **terminare** i processi;
- **tenere traccia** del loro stato e delle risorse utilizzate;
- **garantire isolamento e sincronizzazione** quando più processi condividono la CPU o la memoria.

Il concetto di processo è quindi alla base di tutto il funzionamento dinamico del sistema operativo.

---

### 🔹 1. Processo vs programma

Un **programma** è un insieme statico di istruzioni memorizzate su disco.
Un **processo**, invece, è la **manifestazione dinamica del programma** in esecuzione: include contesto, risorse, variabili, stack e stato di avanzamento.

| Aspetto   | Programma                         | Processo                         |
| --------- | --------------------------------- | -------------------------------- |
| Natura    | Statico                           | Dinamico                         |
| Posizione | Disco                             | Memoria                          |
| Contenuto | Codice                            | Codice + dati + stato            |
| Scopo     | Rappresenta un compito potenziale | Esegue effettivamente un compito |

Esempio:

> Aprire due finestre di “Calcolatrice” esegue **lo stesso programma** due volte, ma genera **due processi distinti**, ognuno con le proprie variabili e stato interno.

---

### 🔹 2. Componenti di un processo

Un processo in esecuzione è composto da diverse **sezioni di memoria** e **strutture di gestione**.

#### a) Spazio di indirizzamento (address space)

Il sistema operativo assegna a ciascun processo un proprio **spazio logico di memoria** suddiviso in sezioni:

| Sezione           | Contenuto                                   |
| ----------------- | ------------------------------------------- |
| **Text (o code)** | Istruzioni eseguibili del programma         |
| **Data**          | Variabili globali e statiche                |
| **Heap**          | Allocazioni dinamiche (es. `malloc`, `new`) |
| **Stack**         | Chiamate di funzione e variabili locali     |

Ogni processo crede di avere un proprio spazio di memoria indipendente, ma in realtà il SO lo mappa sulla memoria fisica in modo controllato.

#### b) Stato e contesto

Il **contesto** di un processo rappresenta il suo “punto di vita” nel sistema:

- Valore dei registri CPU (PC, SP, ecc.)
- Stato del processo (ready, running, waiting…)
- Informazioni su memoria, file aperti, priorità, ecc.

Questo contesto è ciò che il SO salva e ripristina durante i **context switch**.

---

### 🔹 3. Stati del processo

Durante il suo ciclo di vita, un processo attraversa diversi **stati logici**, ciascuno gestito dal SO.

#### a) Modello a 2 stati

- **Running:** il processo è in esecuzione sulla CPU.
- **Not running:** il processo è pronto o in attesa.

Semplice ma limitato: non distingue tra “pronto” e “bloccato”.

#### b) Modello a 5 stati

È il modello più comune nei sistemi moderni.

| Stato                 | Descrizione                                       |
| --------------------- | ------------------------------------------------- |
| **New**               | Il processo è stato creato ma non ancora avviato. |
| **Ready**             | In memoria, attende la CPU.                       |
| **Running**           | Sta eseguendo istruzioni.                         |
| **Blocked (Waiting)** | Attende un evento (es. I/O, segnale).             |
| **Terminated**        | Ha terminato l’esecuzione o è stato ucciso.       |

#### c) Stati sospesi

Oltre ai 5 classici, molti SO aggiungono:

- **Ready suspended**: pronto ma spostato su disco per mancanza di memoria.
- **Blocked suspended**: bloccato e non residente in memoria.

Questi stati consentono al SO di gestire la **memoria virtuale** e lo **swap**.

---

### 🔹 4. Transizioni di stato

Le transizioni rappresentano i **passaggi logici** tra gli stati durante la vita del processo.

Esempio di ciclo tipico:

      ```text
      NEW → READY → RUNNING → WAITING → READY → TERMINATED

      ```

#### Casi principali

- **Creazione:** `new → ready` (ammissione in memoria).
- **Scheduling:** `ready → running` (assegnazione CPU).
- **Preemption:** `running → ready` (fine quanto).
- **I/O request:** `running → waiting`.
- **I/O completion:** `waiting → ready`.
- **Exit:** `running → terminated`.

Il **dispatcher** del SO gestisce queste transizioni tramite **context switch**.

---

### 🔹 5. PCB – Process Control Block

Per ogni processo, il sistema operativo mantiene una struttura dati chiamata **PCB (Process Control Block)**, che contiene tutte le informazioni necessarie per la sua gestione.

#### Struttura tipica del PCB

| Categoria               | Contenuto                                   |
| ----------------------- | ------------------------------------------- |
| **Identificazione**     | PID (Process ID), PPID (Parent ID), utente  |
| **Stato di esecuzione** | Stato (ready, running…), contesto CPU       |
| **Scheduling**          | Priorità, tempo CPU usato, puntatore a code |
| **Memoria**             | Puntatori a tabelle delle pagine o segmenti |
| **File e I/O**          | File aperti, dispositivi assegnati          |
| **Sicurezza**           | UID, permessi di accesso                    |

Durante un **context switch**, il kernel salva il PCB del processo uscente e carica quello del processo entrante.
È attraverso questa struttura che il SO “ricorda” esattamente dove ogni processo si era fermato.

---

### 🔹 6. Code di processi

Per gestire i diversi stati, il SO organizza i processi in **code**.

| Coda                | Descrizione                                |
| ------------------- | ------------------------------------------ |
| **Ready queue**     | Processi pronti in attesa di CPU           |
| **Device queues**   | Processi in attesa di completamento I/O    |
| **Job queue**       | Tutti i processi presenti nel sistema      |
| **Suspended queue** | Processi temporaneamente rimossi dalla RAM |

Ogni scheduler opera su una coda diversa (long, short, medium-term scheduler).

---

### 🔹 7. Operazioni sui processi

#### a) Creazione

Un processo può generare nuovi processi figli tramite una **system call** (es. `fork()` in UNIX).
Il processo figlio eredita parte dello stato del padre (file aperti, variabili, ambiente).

#### b) Terminazione

Un processo può terminare:

- **Volontariamente** (`exit()`)
- **Forzatamente** (`kill()`, errore, segnale del SO)

Quando un processo termina, il suo PCB viene rimosso e le risorse liberate.

#### c) Blocco e sblocco

Durante l’esecuzione, un processo può:

- essere **bloccato** (es. in attesa di I/O);
- essere **risvegliato** quando l’evento atteso si verifica.

---

### 🔹 8. Processi e gerarchie

Nei sistemi moderni i processi formano **alberi di esecuzione**:

- Ogni processo padre può generare più processi figli.
- I figli possono a loro volta creare altri processi.

Esempio in UNIX:

      ```text
      init (PID 1)
      ├─ systemd
      │   ├─ login
      │   ├─ sshd
      │   └─ bash
      │       └─ python

      ```

Il kernel mantiene relazioni **PPID (Parent Process ID)** per tracciare queste gerarchie.
Quando un padre termina, i figli diventano **orfani** e vengono “adottati” da `init`.

---

### 🔹 9. Relazione con i thread

Un processo può contenere **uno o più thread**, ovvero **flussi di esecuzione paralleli** che condividono la stessa memoria e risorse del processo.
Il processo fornisce l’**ambiente di esecuzione**, mentre i thread sono le **unità effettive di esecuzione**.
Questo concetto verrà approfondito nella lezione successiva.

---

### 🧠 Mappa concettuale di sintesi

      ```text
      PROCESSI
      │
      ├── Definizione
      │   ├─ Unità di esecuzione gestita dal SO
      │   └─ Programma + stato + risorse
      │
      ├── Componenti
      │   ├─ Spazio memoria → code, data, heap, stack
      │   ├─ Contesto CPU → registri, PC, flag
      │   └─ PCB → dati di controllo
      │
      ├── Stati
      │   ├─ New, Ready, Running, Waiting, Terminated
      │   └─ Sospesi (Ready/Blocked suspended)
      │
      ├── Transizioni
      │   ├─ new→ready →running →waiting →ready→terminated
      │   └─ Gestite da scheduler + dispatcher
      │
      ├── Code di sistema
      │   ├─ Ready queue
      │   ├─ Device queues
      │   └─ Suspended queue
      │
      ├── Operazioni
      │   ├─ Creazione (fork)
      │   ├─ Terminazione (exit / kill)
      │   └─ Blocco / sblocco
      │
      ├── Gerarchie
      │   └─ Processi padre/figlio, PID e PPID
      │
      └── Relazione con i thread
         └─ Processo = contenitore, thread = unità esecutiva

      ```

## 📘 Thread

### 🔹 Introduzione generale

Il concetto di **thread** nasce dall’esigenza di aumentare il grado di concorrenza all’interno dei sistemi operativi moderni.
Un **thread** può essere definito come un **flusso indipendente di controllo** che si muove all’interno di un processo. In altre parole, è l’unità più piccola di esecuzione che il sistema operativo può pianificare sulla CPU.

Un processo può contenere **uno o più thread**. Quando esiste un solo thread, si parla di processo *monothreaded*; quando invece il processo contiene più thread, si parla di *multithreaded*.
In un processo multithread, tutti i thread condividono le **stesse risorse** del processo (come spazio di indirizzamento, file aperti, variabili globali, heap), ma mantengono **stack separati** per poter gestire le proprie chiamate di funzione e variabili locali in modo indipendente.

Questo permette ai thread di operare contemporaneamente su diverse porzioni del programma, riducendo drasticamente il costo in termini di risorse rispetto alla creazione di nuovi processi.
Infatti, la **creazione di un processo** richiede di duplicare lo spazio di memoria, le strutture del kernel e l’ambiente di esecuzione; invece, creare un thread richiede solo la creazione di uno stack e di poche informazioni di contesto.

---

### 🔹 Vantaggi dell’approccio multithread

L’utilizzo dei thread consente di ottenere **parallelismo logico** anche su sistemi single-core, perché l’OS alterna rapidamente i thread in esecuzione, dando l’impressione di simultaneità.
Nei sistemi multi-core, invece, i thread possono essere effettivamente eseguiti in **parallelo reale**, su core diversi.

I principali vantaggi dell’uso dei thread sono:

1. **Maggiore efficienza**: la creazione, la terminazione e lo switch tra thread richiedono meno risorse e tempo rispetto ai processi.
2. **Migliore utilizzo della CPU**: se un thread è bloccato in attesa di I/O, un altro dello stesso processo può continuare ad eseguire.
3. **Comunicazione più semplice**: i thread possono condividere direttamente le variabili e i dati nello stesso spazio di memoria, evitando il bisogno di meccanismi complessi come pipe o socket.
4. **Migliore strutturazione del programma**: un programma complesso può essere suddiviso in flussi logici separati (ad esempio: thread per l’interfaccia grafica, thread per la logica applicativa, thread per I/O o rete).

---

### 🔹 Thread a livello utente (ULT) e a livello kernel (KLT)

Il modo in cui i thread vengono implementati può variare.
Esistono due approcci principali: i **thread a livello utente (ULT)** e i **thread a livello kernel (KLT)**.
La differenza sta in chi gestisce la loro esecuzione e schedulazione.

#### ▫️ Thread a livello utente (ULT)

I thread a livello utente vengono gestiti da una **libreria nello user space**.
Il sistema operativo non è consapevole della loro esistenza: per il kernel, l’intero processo appare come un’unica entità schedulabile.

Quando si fa uno *switch* tra thread nello stesso processo, l’operazione è gestita interamente dalla libreria di thread e non richiede alcuna chiamata di sistema.
Questo comporta tempi di esecuzione estremamente ridotti, poiché si evita il passaggio da **user mode a kernel mode**, che rappresenta un’operazione costosa.

Tuttavia, l’assenza di intervento del kernel introduce alcuni problemi:

- se un thread effettua una chiamata bloccante (ad esempio una `read()` su un file o su un socket), **tutto il processo rimane bloccato**, perché il kernel non è in grado di distinguere i singoli thread;
- in presenza di più CPU o core, non è possibile sfruttare il parallelismo hardware, poiché per il kernel c’è sempre un solo processo attivo.

In sintesi, gli ULT sono veloci e leggeri, ma non adatti a sistemi multiprocessore e a programmi che fanno uso intensivo di operazioni bloccanti.

---

#### ▫️ Thread a livello kernel (KLT)

I thread a livello kernel vengono invece **gestiti direttamente dal sistema operativo**.
Ogni thread è riconosciuto come entità indipendente e schedulabile.

Questo significa che il kernel può eseguire un thread su un core e un altro thread dello stesso processo su un core diverso, ottenendo **vero parallelismo**.
Inoltre, se un thread si blocca, gli altri thread del processo possono continuare la loro esecuzione.

Il rovescio della medaglia è che la gestione da parte del kernel introduce un **maggiore overhead**:

- ogni creazione o terminazione di thread richiede una chiamata di sistema;
- ogni cambio di contesto (context switch) implica il salvataggio dello stato nel PCB del thread e il passaggio in kernel mode.

Lo scheduling è centralizzato e non può essere personalizzato dall’applicazione, ma garantisce pieno supporto al multiprocessore e una gestione robusta delle risorse.

---

#### ▫️ Riepilogo comparativo ULT vs KLT

| Aspetto                  | ULT (User Level Thread)   | KLT (Kernel Level Thread) |
| ------------------------ | ------------------------- | ------------------------- |
| Gestione                 | Libreria in user space    | Kernel                    |
| Visibilità OS            | Processo unico            | Ogni thread schedulabile  |
| Creazione / terminazione | Molto veloce              | Più costosa               |
| Context switch           | Solo user mode            | Richiede mode switch      |
| Blocco thread            | Blocca tutto il processo  | Blocca solo il thread     |
| Supporto multicore       | No                        | Sì, pieno                 |
| Scheduling               | Personalizzabile dall’app | Gestito dal kernel        |

---

### 🔹 Operazioni fondamentali sui thread

I thread, indipendentemente dal tipo di implementazione, possono trovarsi in stati diversi e compiere alcune operazioni tipiche:

- **Spawn**: creazione di un nuovo thread, che eredita il contesto del processo padre e viene aggiunto alla ready queue.
- **Block**: sospensione volontaria o forzata di un thread, ad esempio in attesa di un evento o di una risorsa condivisa.
- **Unblock**: riattivazione di un thread precedentemente sospeso, quando la condizione di attesa è soddisfatta.
- **Finish**: terminazione del thread, che libera lo stack e le strutture di gestione associate.

Ogni thread mantiene il proprio **contesto di esecuzione**, costituito da:

- il valore dei registri del processore (incluso il program counter),
- lo stato (running, ready, waiting, ecc.),
- lo stack per le variabili locali,
- un puntatore alla memoria condivisa del processo.

Il **context switch** tra thread consiste nel salvare il contesto del thread uscente e nel caricare quello del thread entrante.
Nei sistemi ULT questo avviene in user mode (molto rapido), mentre nei KLT comporta il coinvolgimento del kernel (più lento ma più sicuro).

---

### 🔹 Thread in Linux: LWP e PCB

Nel sistema operativo Linux, l’implementazione dei thread si basa su un concetto intermedio chiamato **Lightweight Process (LWP)**.
Un LWP è una struttura schedulabile che rappresenta un thread, ma possiede molte caratteristiche di un processo classico.

In Linux, non esiste una distinzione netta tra processi e thread: entrambi sono entità gestite tramite la stessa struttura dati, chiamata **task_struct**, che funge da **Process Control Block (PCB)**.
Ogni LWP ha quindi un proprio PCB, ma più LWP possono condividere le stesse risorse, come lo spazio di indirizzamento, i file aperti e le aree di memoria.

I campi principali del PCB di Linux sono:

- **stato** del thread (TASK_RUNNING, TASK_INTERRUPTIBLE, ecc.);
- **registri salvati** e **puntatori allo stack del kernel**;
- **relazioni di parentela** (padre, figli, gruppo di thread);
- **informazioni di scheduling** (priorità, CPU assegnata, contatori di tempo);
- **segnali e gestori di segnali**;
- **puntatori alle risorse condivise** (file, memoria, namespace, ecc.).

#### Stati principali in Linux

Linux utilizza un modello di stati più articolato rispetto a quello classico dei processi:

- **TASK_RUNNING** → thread in esecuzione o pronto per l’esecuzione;
- **TASK_INTERRUPTIBLE** → thread bloccato ma risvegliabile da un segnale;
- **TASK_UNINTERRUPTIBLE** → bloccato, non risvegliabile finché la risorsa non è disponibile;
- **TASK_STOPPED / TASK_TRACED** → thread fermato o sotto debug;
- **EXIT_ZOMBIE / EXIT_DEAD** → thread terminato, ma non ancora completamente rimosso dalle strutture del kernel.

Ogni thread in Linux ha un **TID (Thread ID)** univoco e appartiene a un gruppo di thread identificato da un **TGID (Thread Group ID)**.
Il TGID corrisponde al PID del thread principale del gruppo, cioè quello che rappresenta il processo “padre” visto dall’esterno.

---

### 🔹 Sintesi finale

In Linux, i thread non sono entità separate dai processi ma ne rappresentano delle “versioni leggere”.
Tutti i thread che appartengono allo stesso processo condividono:

- il codice eseguibile,
- lo spazio di memoria virtuale,
- le risorse di I/O,
- i segnali e il gruppo di credenziali.

Ogni thread mantiene però il proprio **stack, registri e stato indipendente**, permettendo al kernel di schedularli singolarmente.

Questa architettura ibrida unisce la flessibilità dei KLT con la leggerezza degli ULT, rendendo il modello di Linux uno dei più efficienti per i sistemi multiprocessore.

### 🔹 Sincronizzazione tra Thread

Quando più thread condividono risorse comuni — ad esempio variabili globali, strutture dati in memoria, file o buffer di I/O — è necessario **coordinare il loro accesso** per evitare conflitti e risultati incoerenti.
Questo problema prende il nome di **sincronizzazione**.

#### ▫️ Problema di concorrenza e sezione critica

Il caso più tipico è quello della **sezione critica**, ovvero una porzione di codice che accede a risorse condivise e che non deve essere eseguita da più thread contemporaneamente.

Senza un’adeguata sincronizzazione, possono verificarsi condizioni di **race condition** (condizioni di competizione): due o più thread tentano di leggere o modificare la stessa variabile contemporaneamente, e il risultato finale dipende dall’ordine di esecuzione, che è imprevedibile.

Per garantire l’integrità dei dati, il sistema operativo (o la libreria dei thread) deve assicurare che la sezione critica soddisfi tre condizioni fondamentali:

1. **Mutua esclusione:** solo un thread per volta può trovarsi nella sezione critica.
2. **Progresso:** se nessun thread è nella sezione critica, deve essere consentito l’ingresso a uno di quelli in attesa.
3. **Attesa limitata:** nessun thread deve essere escluso indefinitamente.

---

### 🔹 Strumenti di sincronizzazione

La sincronizzazione può essere implementata in vari modi, a seconda del livello di astrazione (software, libreria o kernel).
I principali strumenti sono:

#### 1. **Mutex (Mutual Exclusion Lock)**

Il mutex è il meccanismo più elementare per implementare la **mutua esclusione**.
Si tratta di una variabile binaria che può trovarsi in due stati: *libero* (unlocked) o *occupato* (locked).

- Quando un thread entra nella sezione critica, deve **acquisire (lock)** il mutex.
  Se il mutex è libero, il thread entra; se invece è già occupato, il thread viene sospeso finché non diventa disponibile.
- Quando il thread termina la sezione critica, **rilascia (unlock)** il mutex, permettendo ad altri di entrare.

L’uso corretto dei mutex garantisce che solo un thread per volta acceda alla risorsa condivisa.
Tuttavia, un uso scorretto può generare **deadlock**, ovvero situazioni in cui due o più thread rimangono bloccati perché ognuno attende un mutex posseduto da un altro.

- *Esempio logico:**

- Thread A blocca `mutex1` e poi tenta di bloccare `mutex2`.
- Thread B ha già bloccato `mutex2` e tenta di bloccare `mutex1`.
  Nessuno dei due potrà proseguire → deadlock.

---

#### 2. **Semafori**

I **semafori** sono una generalizzazione del mutex introdotta da Dijkstra.
Un semaforo è una variabile intera non negativa che rappresenta il **numero di risorse disponibili**.

Si gestisce tramite due operazioni atomiche:

- `wait()` (o `P`): decrementa il semaforo. Se il valore diventa negativo, il thread si blocca.
- `signal()` (o `V`): incrementa il semaforo. Se ci sono thread bloccati, ne risveglia uno.

Esistono due tipi principali di semafori:

1. **Semaforo binario:** può assumere solo i valori 0 o 1 (equivalente a un mutex).
2. **Semaforo contatore:** può assumere valori maggiori di 1, utile per controllare un numero finito di risorse identiche (es. connessioni di rete, buffer).

I semafori sono potenti ma più difficili da gestire correttamente, poiché non garantiscono automaticamente l’esclusività d’accesso e possono facilmente portare a situazioni di **starvation** (alcuni thread attendono indefinitamente).

---

#### 3. **Condition Variable**

Le **condition variable** permettono a un thread di sospendersi in attesa di una certa condizione logica e di essere risvegliato quando quella condizione diventa vera.
Sono sempre usate insieme a un mutex.

Il meccanismo è il seguente:

- Il thread acquisisce un mutex ed entra in una sezione monitorata.
- Se la condizione non è ancora soddisfatta, chiama `wait()` sulla condition variable: questo rilascia temporaneamente il mutex e sospende il thread.
- Quando un altro thread modifica la condizione, chiama `signal()` o `broadcast()` sulla condition variable, risvegliando uno o più thread sospesi.
- I thread risvegliati riacquisiscono il mutex e ricontrollano la condizione.

Questo modello è usato nei **monitor**, ovvero strutture di sincronizzazione di alto livello che incapsulano variabili condivise e le operazioni di accesso in modo sicuro.

---

#### 4. **Join e sincronizzazione del flusso**

Oltre alle sezioni critiche, è necessario sincronizzare il **flusso di esecuzione** dei thread, ovvero controllare *quando* un thread deve attendere il completamento di un altro.
Il metodo più comune è la **join operation**.

Quando un thread principale (ad esempio il thread "padre") crea altri thread figli, può eseguire su ciascuno di essi l’operazione:

      ```c
      pthread_join(thread_id, NULL);

      ```

In questo modo, il thread padre si sospende fino a quando il thread figlio identificato da `thread_id` termina.
Questa operazione assicura che tutte le elaborazioni parallele si completino prima di proseguire.

---

#### 5. **Barrier**

Una **barriera** è un meccanismo che consente a un gruppo di thread di sincronizzarsi a un punto preciso del programma.
Ogni thread, al raggiungimento della barriera, si blocca finché anche tutti gli altri non la raggiungono.
Solo quando tutti i thread sono arrivati, la barriera si apre e tutti possono proseguire.
È molto utilizzata nei programmi scientifici o nei calcoli distribuiti, dove diverse parti di un algoritmo devono sincronizzarsi periodicamente.

---

### 🔹 Problemi tipici della sincronizzazione

#### ▫️ Deadlock

Un **deadlock** si verifica quando due o più thread si bloccano reciprocamente, ognuno in attesa di una risorsa posseduta dall’altro.
Le quattro condizioni necessarie per il verificarsi di un deadlock (secondo Coffman) sono:

1. **Mutua esclusione** – le risorse non possono essere condivise.
2. **Hold and wait** – un thread trattiene una risorsa e ne richiede altre.
3. **No preemption** – le risorse non possono essere sottratte forzatamente.
4. **Attesa circolare** – esiste una catena di thread in cui ciascuno attende una risorsa posseduta dal successivo.

Prevenire o evitare i deadlock richiede strategie come:

- imporre un **ordine globale di acquisizione delle risorse**,
- introdurre **timeout**,
- o applicare algoritmi di rilevamento e recupero (ad esempio rilasciando e ripetendo l’operazione).

---

#### ▫️ Starvation

La **starvation** si verifica quando uno o più thread non riescono mai ad accedere a una risorsa, a causa della presenza costante di altri thread con priorità più alta.
Può accadere, ad esempio, in algoritmi non equi di scheduling o in uso scorretto dei semafori.

#### ▫️ Busy waiting e spinlock

Un’altra problematica è il **busy waiting**, che si verifica quando un thread, invece di sospendersi, continua a controllare in un ciclo se una risorsa è libera (tipico degli spinlock).
Questo può sprecare tempo di CPU, ma su sistemi multiprocessore è utile per sezioni critiche molto brevi, in quanto evita il costo del cambio di contesto.

---

### 🔹 Sincronizzazione in Linux

In ambiente Linux (e in generale nei sistemi POSIX), la sincronizzazione tra thread è gestita tramite la **pthread library** (`<pthread.h>`).
Essa fornisce meccanismi standardizzati per:

- **Mutex** (`pthread_mutex_t`),
- **Condition variables** (`pthread_cond_t`),
- **Semafori** (`sem_t`),
- **Barrier** (`pthread_barrier_t`).

Il kernel Linux, inoltre, offre meccanismi di sincronizzazione interni (come *spinlock*, *seqlock*, *rwlock* e *RCU – Read-Copy-Update*) utilizzati per proteggere strutture dati interne del kernel stesso, dove la rapidità è più importante della sospensione dei thread.

---

### 🔹 Sintesi generale

In un sistema multithread, la sincronizzazione è l’elemento che garantisce la **correttezza logica** del programma e la **coerenza dei dati**.
Senza di essa, l’esecuzione concorrente porterebbe a comportamenti imprevedibili e errori difficili da individuare.

L’obiettivo è sempre trovare il **compromesso tra sicurezza e efficienza**:

- troppa sincronizzazione riduce il parallelismo;
- troppo poca genera condizioni di gara o inconsistenza.

Un buon sistema operativo (e un buon programmatore) deve quindi progettare sezioni critiche piccole, atomiche e protette da meccanismi adeguati, scegliendo il tipo di sincronizzazione più adatto alla situazione.

## Scheduling

### 🔹 Introduzione generale

In un sistema operativo multiprogrammato, **più processi o thread competono per l’uso della CPU**.
Poiché in genere il numero dei processi attivi è superiore al numero dei processori disponibili, è necessario stabilire un criterio che decida **chi debba essere eseguito in un dato momento**.
Questo insieme di criteri e politiche prende il nome di **scheduling** (o **pianificazione della CPU**).

Il componente del sistema operativo che si occupa di queste decisioni è detto **scheduler**, mentre l’azione di scegliere quale processo assegnare alla CPU si chiama **dispatching**.
Ogni decisione di scheduling implica un **context switch**, cioè il salvataggio dello stato del processo in esecuzione e il caricamento di quello del processo successivo.

L’obiettivo fondamentale dello scheduling è massimizzare **l’utilizzo della CPU** mantenendo **reattività e giustizia (fairness)** tra i processi.

---

### 🔹 Obiettivi dello scheduling

Gli obiettivi variano a seconda del tipo di sistema operativo (batch, interattivo, real-time), ma si possono distinguere due macro-categorie di priorità.

#### 1. Obiettivi nei sistemi batch

Nei sistemi batch, dove i processi vengono eseguiti in blocco senza interazione con l’utente, lo scheduling è orientato all’**efficienza globale** del sistema:

- **Massimizzare il throughput** → aumentare il numero di processi completati per unità di tempo.
- **Minimizzare il tempo di turnaround** → ridurre l’intervallo tra la sottomissione e la conclusione di un processo.
- **Ridurre l’overhead di CPU** → minimizzare il tempo speso in cambio di contesto e gestione.

#### 2. Obiettivi nei sistemi interattivi

Nei sistemi interattivi, in cui l’utente si aspetta risposte rapide, l’attenzione si sposta sulla **reattività**:

- **Minimizzare il tempo di risposta** → ridurre il ritardo tra l’input dell’utente e la risposta del sistema.
- **Garantire la fairness** → evitare che processi a bassa priorità restino indefinitamente in attesa.
- **Gestire la priorità** → consentire che processi critici (es. di sistema) vengano eseguiti prima.

#### 3. Compromessi

Lo scheduling cerca un equilibrio tra:

- **efficienza** (alto throughput)
- **reattività** (risposta veloce)
- **giustizia** (tutti i processi ricevono attenzione)
- **predicibilità** (tempi di risposta costanti)

---

### 🔹 Tipi di scheduling

Il sistema operativo può applicare politiche di scheduling su **diversi livelli** del ciclo di vita dei processi.

#### 1. Long-Term Scheduling (a lungo termine)

È responsabile della **selezione dei processi da ammettere in memoria** per l’esecuzione.
Agisce nel momento in cui un nuovo job entra nel sistema.
Il suo compito è regolare il **grado di multiprogrammazione**, ovvero quante attività possono trovarsi contemporaneamente in memoria.

- Se il grado di multiprogrammazione è troppo alto → rischio di **thrashing** (eccessivo swapping e rallentamento generale).
- Se è troppo basso → CPU sotto-utilizzata.

Nei sistemi moderni (es. Linux desktop), questo tipo di scheduling è spesso implicito o automatico, ma resta fondamentale nei sistemi batch e real-time.

#### 2. Medium-Term Scheduling (a medio termine)

Gestisce la **sospensione e riattivazione** dei processi.
Il suo obiettivo è migliorare l’utilizzo della memoria principale, eseguendo operazioni di:

- **swap out** → rimuovere temporaneamente un processo dalla memoria.
- **swap in** → ricaricarlo quando ci sono risorse disponibili.

È un meccanismo utile nei sistemi con memoria limitata o con processi di lunga durata, e contribuisce al controllo del carico di sistema.

#### 3. Short-Term Scheduling (a breve termine)

È lo **scheduling vero e proprio della CPU**.
Il suo compito è selezionare, tra i processi pronti (stato *ready*), quello che dovrà essere eseguito immediatamente.
Opera con frequenza molto elevata (millisecondi o microsecondi), poiché ogni volta che:

- un processo termina il proprio quanto di tempo,
- entra un nuovo processo ready,
- o un processo viene risvegliato da uno stato di blocco,
  il CPU scheduler deve decidere chi eseguire.

Questo tipo di scheduling è quello che ha **l’impatto diretto sulla reattività percepita dall’utente**.

#### 4. I/O Scheduling

Gestisce l’ordine di esecuzione delle richieste ai dispositivi di I/O.
Poiché le operazioni di I/O sono molto più lente di quelle di CPU, l’obiettivo è **ridurre i tempi di attesa** e **ottimizzare il throughput del disco o della periferica**.
Viene approfondito in seguito, ma qui basta sapere che rappresenta una forma specializzata di scheduling, spesso gestita a livello di driver.

---

### 🔹 Tipologie di scheduling: preemptive vs non-preemptive

Uno dei parametri più importanti per classificare gli algoritmi di scheduling è la possibilità o meno di **interrompere un processo in esecuzione**.

- **Non-preemptive** → il processo mantiene la CPU fino a quando termina o entra in stato di attesa.
  È più semplice, ma meno reattivo.
  Esempi: FCFS, SPN, HRRN.

- **Preemptive** → il sistema può forzare la sospensione del processo per assegnare la CPU a un altro (ad esempio, più prioritario o appena arrivato).
  È più complesso ma migliora l’interattività.
  Esempi: RR, SRT.

---

### 🔹 Algoritmi di scheduling della CPU

Il cuore dello scheduling a breve termine è costituito dagli **algoritmi di selezione del processo**.
Ogni algoritmo stabilisce un criterio di scelta e una politica di sostituzione tra processi nella ready queue.

#### FCFS – *First Come, First Served*

- È il più semplice algoritmo non-preemptive.
- I processi vengono eseguiti nell’ordine di arrivo nella coda ready (FIFO).
- Una volta ottenuta la CPU, il processo la mantiene fino al termine.

- *Vantaggi:**

- Implementazione semplice.
- Nessun overhead di cambio di contesto.

- *Svantaggi:**

- Può causare il **convoy effect**: un processo lungo trattiene la CPU e costringe i successivi ad attendere.
- Tempi di risposta elevati per processi brevi.

È adatto per sistemi batch, ma inefficiente in ambienti interattivi.

---

#### RR – *Round Robin*

- È una variante preemptive del FCFS.
- Ogni processo riceve un **quanto di tempo (time quantum)** fisso.
- Quando il quanto scade, il processo viene sospeso e rimesso in coda, mentre la CPU passa al successivo.

- *Vantaggi:**

- Garantisce **equità** (tutti i processi ottengono la CPU in modo ciclico).
- Migliora la **reattività** nei sistemi interattivi.
- Semplice da implementare.

- *Svantaggi:**

- Se il quanto è troppo grande → degrada a FCFS.
- Se è troppo piccolo → aumenta il numero di context switch, riducendo l’efficienza.

La scelta ottimale del **time quantum** è quindi un compromesso tra reattività e overhead.

---

#### SPN – *Shortest Process Next* (o SJF – Shortest Job First)

- Politica **non-preemptive** che seleziona il processo con il **burst time più breve**.
- Si basa sull’ipotesi che il tempo di esecuzione di ciascun processo sia stimabile.

- *Vantaggi:**

- Minimizza il tempo medio di attesa e di turnaround.
- Teoricamente, è l’algoritmo più efficiente in termini di tempo medio.

- *Svantaggi:**

- Difficile stimare con precisione il burst time.
- Possibile **starvation** per processi lunghi che vengono continuamente rimandati.

---

#### SRT – *Shortest Remaining Time*

- È la versione **preemptive** di SPN.
- Ogni volta che arriva un nuovo processo, viene confrontato il suo burst con quello rimanente del processo in esecuzione.
- Se il nuovo processo ha un burst più breve, preempie l’attuale.

- *Vantaggi:**

- Migliora il tempo medio di attesa rispetto a SPN.
- Ottimale nei sistemi con processi brevi e frequenti.

- *Svantaggi:**

- Elevato overhead dovuto ai continui preemption.
- Ancora più esposto al rischio di starvation per processi lunghi.

---

#### HRRN – *Highest Response Ratio Next*

- Politica **non-preemptive** che migliora SPN introducendo un criterio di priorità dinamica:
  [
  R = \frac{W + S}{S}
  ]
  dove:
  ( W ) = tempo di attesa,
  ( S ) = tempo di servizio stimato.

- *Funzionamento:**

- I processi che attendono da molto tempo aumentano progressivamente la propria priorità.
- In questo modo, un processo lungo ma in attesa da tempo ottiene la CPU prima o poi.

- *Vantaggi:**

- Evita starvation.
- Buon compromesso tra tempo medio di attesa e fairness.

- *Svantaggi:**

- Non preemptive → non adatto a sistemi interattivi.
- Richiede calcolo periodico del rapporto ( R ).

---

#### Tabella comparativa algoritmi

| Algoritmo     | Preemptive | Vantaggi principali                | Svantaggi principali                 |
| ------------- | ---------- | ---------------------------------- | ------------------------------------ |
| **FCFS**      | No         | Semplice, poco overhead            | Convoy effect, scarsa reattività     |
| **RR**        | Sì         | Equità, buoni tempi di risposta    | Dipende dal quanto, overhead elevato |
| **SPN (SJF)** | No         | Ottimo tempo medio di attesa       | Starvation, stima burst difficile    |
| **SRT**       | Sì         | Migliora SPN, ottimizza tempi medi | Starvation, overhead alto            |
| **HRRN**      | No         | Evita starvation, bilanciato       | Non preemptive, calcolo frequente    |

---

### 🔹 Scheduling multiprocessore e Scheduling UNIX/Linux

---

### 🔹 1. Introduzione

Nei sistemi moderni, la presenza di **più CPU o core** rende necessario un tipo di scheduling più complesso, capace di distribuire in modo equilibrato il carico di lavoro tra i processori.
In questo contesto, il compito dello scheduler non è più solo decidere *quale processo eseguire*, ma anche *su quale processore eseguirlo*.
Il problema viene quindi esteso da una dimensione temporale (“quando”) a una dimensione spaziale (“dove”).

Il principale obiettivo dello **scheduling multiprocessore** è quello di garantire:

- un **uso bilanciato** delle CPU (nessun core sovraccarico o inattivo);
- un **throughput elevato** complessivo;
- la **minimizzazione del tempo di attesa e di risposta**;
- la **coerenza della cache**, cioè evitare spostamenti inutili di thread tra core.

---

### 🔹 2. Tipologie di scheduling multiprocessore

Esistono diversi modelli e strategie per gestire la pianificazione su più CPU, che si differenziano per il grado di **cooperazione e indipendenza** tra i processori.

#### a) Asymmetric Multiprocessing (AMP)

Nel modello **asimmetrico**, solo un processore (detto *master*) è responsabile dello scheduling e della gestione dei processi di sistema.
Gli altri processori (*slave*) si limitano a eseguire i processi assegnati.

- *Caratteristiche:**

- Il processore master gestisce la ready queue globale e distribuisce il lavoro.
- I processori slave non prendono decisioni di scheduling.
- È un modello semplice, ma con **collo di bottiglia**: il master può diventare un punto di congestione.
- Utilizzato nei primi sistemi multiprocessore o embedded.

---

#### b) Symmetric Multiprocessing (SMP)

Il modello **simmetrico** è quello adottato dai sistemi moderni (inclusi Linux, Windows, macOS).
Tutti i processori sono equivalenti e ciascuno possiede **il proprio scheduler locale**.

- *Caratteristiche principali:**

- Tutte le CPU possono accedere alle stesse code dei processi (ready queue).
- Ogni CPU può schedulare processi in modo indipendente.
- I processi possono essere spostati da una CPU all’altra (migrazione).

- *Problema principale:** la **migrazione dei processi** tra CPU comporta perdita di efficienza della cache (cache miss), poiché i dati del processo devono essere caricati nella cache del nuovo processore.
Per questo motivo, i moderni scheduler SMP cercano di mantenere, se possibile, la **CPU affinity**.

---

### 🔹 3. CPU Affinity

La **CPU affinity** (o *process affinity*) rappresenta la tendenza di un processo o thread a essere eseguito sempre sulla stessa CPU.
Questo migliora le prestazioni grazie al **riuso della cache**, riducendo il numero di cache miss e migliorando la località dei dati.

#### Tipi di affinità

##### 1. Soft affinity

- Il sistema tenta di mantenere il processo sulla stessa CPU, ma non lo garantisce.
- È una preferenza, non un vincolo.
- Usata nei sistemi generici per flessibilità.

##### 2. Hard affinity

- L’associazione tra processo e CPU è obbligatoria.
- Può essere impostata manualmente dall’utente o dal sistema operativo (`taskset` in Linux).
- Riduce il bilanciamento dinamico ma aumenta la coerenza della cache.

---

### 🔹 4. Load Balancing

In un sistema multiprocessore, può accadere che alcune CPU siano sovraccariche e altre inattive.
Il **load balancing** serve a distribuire equamente il carico di lavoro tra le CPU.

#### Strategie principali

##### Push migration

Lo scheduler controlla periodicamente le code di tutte le CPU e sposta attivamente processi da quelle sovraccariche a quelle libere.

##### Pull migration

Una CPU inattiva “pesca” un processo da una coda di un’altra CPU.

Il bilanciamento può essere:

- **globale:** tutte le CPU condividono una coda comune di processi (ready queue globale).
  → Più equo ma meno scalabile.
- **locale:** ogni CPU ha la propria coda, con meccanismi di bilanciamento periodici.
  → Più efficiente ma più complesso da mantenere coerente.

---

### 🔹 5. Scheduling in UNIX / Linux

Linux utilizza un modello di scheduling **SMP completamente simmetrico**, con un approccio **multilivello** e **basato su priorità dinamiche**.
Nel corso delle versioni, sono stati sviluppati diversi scheduler; i più importanti sono:

- **O(1) Scheduler** (fino a Linux 2.6)
- **CFS – Completely Fair Scheduler** (dal kernel 2.6.23 in poi, tutt’ora in uso)

Oltre a questi, Linux supporta anche politiche real-time conformi allo standard **POSIX**.

---

### 🔹 6. Scheduler O(1)

L’**O(1) scheduler** è stato introdotto per ottenere una decisione di scheduling in tempo costante (complessità O(1)), indipendentemente dal numero di processi nel sistema.

#### Struttura

- Ogni CPU possiede due code:

  - **Active queue:** contiene i processi pronti all’esecuzione.
  - **Expired queue:** contiene i processi che hanno esaurito il proprio quanto.
    Quando la coda attiva si svuota, le due code vengono scambiate.

#### Caratteristiche principali

- Ogni processo ha una **priorità dinamica**, che aumenta o diminuisce in base al comportamento (CPU-bound o I/O-bound).
- Gli I/O-bound vengono favoriti per ridurre i tempi di risposta.
- I processi di tipo batch vengono penalizzati progressivamente per evitare starvation.

Questo scheduler è molto efficiente e scalabile, ma tende a favorire eccessivamente i processi interattivi.

---

### 🔹 7. Completely Fair Scheduler (CFS)

Il **CFS (Completely Fair Scheduler)**, introdotto nelle versioni moderne di Linux, si basa sul principio di **equa condivisione della CPU** tra i processi, senza utilizzare code statiche né quanti di tempo fissi.

L’idea di fondo è che **ogni processo deve ottenere una frazione di CPU proporzionale alla sua priorità**, in modo “completamente equo”.

#### Principio di funzionamento

- Ogni processo ha un valore chiamato **vruntime (virtual runtime)**, che misura il tempo di CPU effettivamente ottenuto.
- Lo scheduler mantiene un **albero bilanciato (red-black tree)** ordinato per `vruntime`.
- Il processo con il minor `vruntime` (cioè quello che ha ricevuto meno CPU) viene selezionato per l’esecuzione.
- Quando un processo esegue, il suo `vruntime` aumenta; così, nel tempo, tutti ricevono un trattamento proporzionale.

#### Vantaggi del CFS

- Non richiede code distinte o scambi periodici.
- Bilancia automaticamente CPU-bound e I/O-bound.
- Supporta facilmente il bilanciamento tra CPU diverse.
- È deterministico e scalabile.

#### Intervallo temporale

Il CFS non definisce un quanto fisso; calcola dinamicamente un **target latency**, cioè il tempo in cui tutti i processi attivi dovrebbero ottenere la CPU almeno una volta.
Se ci sono pochi processi, ciascuno ottiene una fetta più grande; se i processi aumentano, la fetta diventa più piccola.

---

### 🔹 8. Politiche di scheduling in Linux

Linux supporta tre **classi di scheduling principali**, ciascuna con logica e priorità distinte:

| Classe             | Descrizione                        | Politica                                | Note                                            |
| ------------------ | ---------------------------------- | --------------------------------------- | ----------------------------------------------- |
| **SCHED_OTHER**    | Default (CFS) per processi normali | Time-sharing                            | Priorità dinamiche, fairness                    |
| **SCHED_FIFO**     | Real-time, priorità assoluta       | Non-preemptive FIFO                     | Usata per processi critici, esempio audio/video |
| **SCHED_RR**       | Real-time, round-robin             | Preemptive                              | Simile a FIFO ma con quanto di tempo fisso      |
| **SCHED_DEADLINE** | Real-time soft                     | Basato su EDF (Earliest Deadline First) | Introdotto per sistemi deterministici           |

Le politiche real-time (`SCHED_FIFO`, `SCHED_RR`, `SCHED_DEADLINE`) hanno **priorità superiori** rispetto ai processi CFS.
In caso di conflitto, i thread real-time hanno sempre la precedenza.

---

### 🔹 9. Struttura del PCB in Linux per lo scheduling

Il **PCB** (`task_struct`) contiene campi specifici per la gestione dello scheduling:

- **policy** → indica la classe (OTHER, FIFO, RR, DEADLINE)
- **prio** e **static_prio** → priorità statica e dinamica
- **vruntime** → tempo di CPU virtuale
- **se.run_list** → puntatore nell’albero red-black del CFS
- **cpus_allowed** → maschera di affinità CPU
- **se.load.weight** → peso proporzionale alla priorità

Ogni CPU ha inoltre una propria **runqueue** locale (`rq`), che mantiene i processi ready e coordina il bilanciamento.

---

### 🔹 10. Sintesi concettuale per mappa

      ```text
      SCHEDULING (II)
      │
      ├── Scheduling multiprocessore
      │   ├─ AMP → master/slave, semplice ma collo di bottiglia
      │   └─ SMP → CPU simmetriche, schedulazione locale
      │
      ├── CPU Affinity
      │   ├─ Soft affinity → preferenza
      │   └─ Hard affinity → vincolo fisso
      │
      ├── Load balancing
      │   ├─ Push migration → spinta dai core attivi
      │   └─ Pull migration → prelievo da core inattivi
      │
      ├── Linux Scheduler
      │   ├─ O(1) → due code (active/expired), priorità dinamiche
      │   ├─ CFS → fairness tramite vruntime e red-black tree
      │   └─ Target latency → fetta CPU proporzionale
      │
      ├── Politiche Linux
      │   ├─ SCHED_OTHER → CFS (normale)
      │   ├─ SCHED_FIFO → real-time FIFO
      │   ├─ SCHED_RR → real-time Round Robin
      │   └─ SCHED_DEADLINE → EDF (Earliest Deadline First)
      │
      └── PCB Linux
         ├─ policy, prio, vruntime
         ├─ se.load.weight
         └─ cpus_allowed (affinità)

      ```

## Sincronizzazione (I)

---

### 🔹 Introduzione

In un sistema multiprogrammato o multithread, più processi o thread possono essere **attivi contemporaneamente** e condividere **risorse comuni**, come variabili, file o dispositivi.
Quando due o più attività tentano di accedere contemporaneamente a una risorsa condivisa, possono verificarsi **condizioni di competizione (race conditions)**, che portano a risultati **imprevedibili e non deterministici**.

Per evitare questi problemi, il sistema operativo (e il programmatore) devono garantire una **sincronizzazione corretta** tra i processi concorrenti, assicurando che **le operazioni critiche siano eseguite in modo mutualmente esclusivo**.

---

### 🔹 1. Sezione critica

La **sezione critica** è la parte di codice di un processo che **accede a risorse condivise** (variabili, buffer, dispositivi).
Durante l’esecuzione della sezione critica, **nessun altro processo** deve poter accedere alle stesse risorse.

#### Struttura generale di un processo

      ```text
      while (true) {
         Entry Section    → Richiede accesso alla sezione critica
         Critical Section → Accesso alla risorsa condivisa
         Exit Section     → Rilascia la risorsa
         Remainder Section → Codice non critico
      }

      ```

L’obiettivo è progettare **protocolli di sincronizzazione** che garantiscano tre proprietà fondamentali:

1. **Mutua esclusione:**
   solo un processo alla volta può essere nella sezione critica.

2. **Progresso:**
   se nessun processo è nella sezione critica, solo i processi che desiderano entrarvi possono decidere chi entra, evitando attese inutili.

3. **Attesa limitata (bounded waiting):**
   nessun processo deve restare in attesa indefinitamente (assenza di starvation).

---

### 🔹 2. Condizioni di competizione (Race Conditions)

Una **race condition** si verifica quando l’esito finale di un programma **dipende dall’ordine di esecuzione** dei processi concorrenti.
Questo accade perché più processi **leggono e scrivono simultaneamente** su una risorsa condivisa senza sincronizzazione.

#### Esempio classico

Supponiamo due processi P1 e P2 che incrementano una variabile condivisa `x`:

      ```text
      P1: x = x + 1
      P2: x = x + 1

      ```

In assenza di sincronizzazione, la sequenza di esecuzione potrebbe essere:

      ```text
      P1 legge x = 5
      P2 legge x = 5
      P1 scrive x = 6
      P2 scrive x = 6

      ```

→ risultato finale: `x = 6` invece di `7`.

Questo problema nasce perché le operazioni non sono atomiche (lettura + modifica + scrittura) e si sovrappongono.

---

### 🔹 3. Soluzioni software alla mutua esclusione

Prima dell’introduzione di meccanismi hardware e primitivi del kernel, sono state sviluppate **soluzioni puramente software** per garantire l’accesso esclusivo alla sezione critica.
Queste soluzioni operano tramite variabili condivise e cicli di controllo (busy waiting).

#### a) Disabilitazione degli interrupt (solo kernel)

Nel kernel, la CPU può **disabilitare gli interrupt** durante l’esecuzione di codice critico:

      ```c

      disable_interrupts();
      critical_section();
      enable_interrupts();

      ```

→ impedisce che venga eseguito un context switch.

- *Vantaggi:**

- Soluzione semplice ed efficace per il codice del kernel.

- *Svantaggi:**

- Non applicabile ai processi utente.
- Rende il sistema meno reattivo (gli interrupt vengono ritardati).
- Pericolosa su architetture multicore (non blocca gli altri core).

---

#### b) Soluzione di Peterson

La **soluzione di Peterson** è un algoritmo software classico per due processi, basato su due variabili condivise:

- `flag[i]`: indica se il processo *i* vuole entrare nella sezione critica.
- `turn`: indica a chi tocca entrare.

      ```c

      flag[i] = true;
      turn = j;
      while (flag[j] && turn == j);
      critical_section();
      flag[i] = false;

      ```

- *Funzionamento:**

- Ogni processo segnala la propria intenzione (`flag[i] = true`) e cede momentaneamente la priorità all’altro (`turn = j`).
- Solo quando l’altro non è interessato o non ha il turno, può entrare nella sezione critica.

- *Proprietà:**
✔ Mutua esclusione
✔ Progresso
✔ Attesa limitata

- *Limiti:** valida solo per due processi; inefficiente su sistemi multiprocessore.

---

#### c) Algoritmo del panettiere (Bakery Algorithm)

Proposto da Lamport, estende la soluzione di Peterson a **più processi**.

Ogni processo prende un “numero” come in una panetteria:
quello con il numero più basso entra per primo nella sezione critica.

      ```c
      choosing[i] = true;
      number[i] = 1 + max(number[0..n-1]);
      choosing[i] = false;
      while (∃ j: (choosing[j] || (number[j] != 0 &&
         (number[j], j) < (number[i], i))));
      critical_section();
      number[i] = 0;

      ```

- *Proprietà:**

- Garantisce mutua esclusione e ordine FIFO.
- Completamente software.

- *Svantaggi:**

- Elevato overhead per confronti multipli.
- Poco pratico nei sistemi reali.

---

### 🔹 4. Soluzioni hardware

Per migliorare l’efficienza, i moderni processori offrono **istruzioni atomiche** che garantiscono mutua esclusione senza busy waiting esplicito.

#### a) Test-and-Set

Istruzione atomica che **legge e modifica** contemporaneamente una variabile di lock.

      ```c
      boolean TestAndSet(boolean *target) {
         boolean old = *target;
         - target = true;
         return old;
      }

      ```

- *Esempio d’uso:**

      ```c
      while (TestAndSet(&lock)); // attende finché lock non è false
      critical_section();
      lock = false;

      ```

→ nessuna interruzione può interferire durante l’istruzione atomica.

- *Problema:**
causa *busy waiting* (la CPU consuma cicli in attesa).

---

#### b) Swap (Exchange)

Scambia in modo atomico il contenuto di due variabili:

      ```c
      Swap(a, b):
         temp = a;
         a = b;
         b = temp;

      ```

Può essere usato per implementare meccanismi simili a Test-and-Set.

---

#### c) Compare-and-Swap (CAS)

Istruzione più evoluta: confronta il valore di una variabile e, se corrisponde a quello atteso, lo sostituisce con un nuovo valore.
È la base dei **lock-free algorithms** nei sistemi multiprocessore.

      ```c
      boolean CAS(int *ptr, int expected, int new) {
         if (*ptr == expected) {
            - ptr = new;
            return true;
         } else return false;
      }

      ```

---

### 🔹 5. Semafori

Proposti da Dijkstra, i **semafori** rappresentano una **soluzione generale e astratta** per gestire la sincronizzazione tra processi, evitando l’uso diretto di busy waiting.

Un semaforo è una **variabile intera S** che può assumere valori ≥ 0, e viene manipolata tramite due operazioni atomiche:

      ```text
      wait(S):   // P (proberen, "provare")
         while (S <= 0)
            ; // attende
         S = S - 1

      signal(S): // V (verhogen, "incrementare")
         S = S + 1

      ```

#### Tipologie di semafori

- **Semaforo binario (mutex):** può valere solo 0 o 1 → usato per mutua esclusione.
- **Semaforo contatore:** rappresenta un numero di risorse disponibili (es. posti in un buffer).

#### Vantaggi

- Semplice da implementare a livello di kernel.
- Evita race conditions e garantisce mutua esclusione.

#### Svantaggi

- Se implementato con busy waiting → spreco CPU.
  (In sistemi reali, il processo viene messo in coda e sospeso.)

---

### 🔹 6. Problema Produttore–Consumatore

Il **problema del produttore–consumatore** (o **bounded buffer problem**) è un classico esempio di uso dei semafori.

#### Descrizione

- Un **produttore** genera dati e li inserisce in un buffer.
- Un **consumatore** preleva dati dallo stesso buffer.
- Il buffer ha **capacità limitata** → serve sincronizzazione per evitare:

  - produzione oltre la capacità (overflow),
  - consumo di buffer vuoto (underflow).

#### Soluzione con semafori

      ```c
      semaphore mutex = 1;   // accesso esclusivo al buffer
      semaphore full = 0;    // numero di elementi pieni
      semaphore empty = N;   // numero di spazi liberi

      Producer:
      while (true) {
         produce_item();
         wait(empty);
         wait(mutex);
         insert_item();
         signal(mutex);
         signal(full);
      }

      Consumer:
      while (true) {
         wait(full);
         wait(mutex);
         remove_item();
         signal(mutex);
         signal(empty);
         consume_item();
      }

      ```

✔ Evita overflow e underflow
✔ Garantisce mutua esclusione
✔ Sincronizza correttamente produttore e consumatore

---

### 🧠 Mappa concettuale di sintesi

      ```text
      SINCRONIZZAZIONE (I)
      │
      ├── Sezione critica
      │   ├─ Accesso a risorse condivise
      │   ├─ Proprietà: mutua esclusione, progresso, attesa limitata
      │
      ├── Race condition
      │   └─ Esito dipende dall’ordine di esecuzione
      │
      ├── Soluzioni software
      │   ├─ Disabilitazione interrupt (solo kernel)
      │   ├─ Peterson → 2 processi
      │   └─ Bakery → n processi, numerazione
      │
      ├── Soluzioni hardware
      │   ├─ Test-and-Set
      │   ├─ Swap
      │   └─ Compare-and-Swap (CAS)
      │
      ├── Semafori
      │   ├─ Operazioni P (wait) / V (signal)
      │   ├─ Binario e contatore
      │   └─ Gestiti dal kernel (no busy waiting)
      │
      └── Problema Produttore–Consumatore
         ├─ Buffer limitato
         ├─ Semafori: mutex, full, empty
         └─ Evita overflow/underflow

      ```

## Sincronizzazione (II)

---

### 🔹 Introduzione

La sincronizzazione non si limita a garantire la mutua esclusione: in molti casi, più processi devono **cooperare e coordinare le proprie azioni** in modo ordinato.
Inoltre, l’uso scorretto dei meccanismi di sincronizzazione può portare a **situazioni di blocco permanente (deadlock)**, in cui un gruppo di processi resta sospeso in attesa reciproca di risorse.

Questa lezione approfondisce:

- i **monitor** come astrazione ad alto livello per la sincronizzazione strutturata;
- la **natura del deadlock**;
- i **metodi per prevenirlo, evitarlo o rilevarlo**;
- e infine l’**algoritmo del banchiere** di Dijkstra, che ne rappresenta un modello di evitamento dinamico.

---

### 🔹 1. Monitor

Un **monitor** è un **costrutto di sincronizzazione ad alto livello**, introdotto da Hoare e Brinch Hansen, che incapsula:

- le **variabili condivise**,
- le **procedure che operano su di esse**, e
- i **meccanismi di sincronizzazione** (implicitamente gestiti dal linguaggio o dal sistema).

#### Concetto

Solo **un processo alla volta** può trovarsi all’interno del monitor → garantisce **mutua esclusione automatica**.

      ```text
      monitor Buffer {
         item buffer[N];
         int count = 0;
         condition full, empty;

         procedure insert(item x) {
            if (count == N) wait(full);
            buffer[count++] = x;
            signal(empty);
         }

         procedure remove(item x) {
            if (count == 0) wait(empty);
            x = buffer[--count];
            signal(full);
         }
      }

      ```

#### Variabili di condizione

Le **variabili di condizione** permettono di sospendere e risvegliare i processi all’interno del monitor:

- `wait(c)`: sospende il processo su `c` finché un altro non lo risveglia.
- `signal(c)`: risveglia un processo sospeso su `c` (se presente).

#### Vantaggi

- Sintassi chiara e strutturata: facile da integrare nei linguaggi ad alto livello (es. Java, C#, Ada).
- Elimina l’uso esplicito dei semafori.
- Evita errori di sincronizzazione dovuti a dimenticanze o inversioni di ordine (`wait`/`signal`).

#### Svantaggi

- Minor controllo sul comportamento fine del sistema.
- La semantica di `signal` varia:

  - **Hoare semantics:** il processo risvegliato entra subito nel monitor.
  - **Mesa semantics (usata in Java):** il processo risvegliato è solo pronto, ma non entra subito (può esserci starvation).

---

### 🔹 2. Deadlock

Un **deadlock** si verifica quando un insieme di processi si trova in uno stato in cui **ognuno attende una risorsa posseduta da un altro processo del gruppo**, e **nessuno può progredire**.

#### Esempio classico

Due processi P1 e P2, due risorse R1 e R2:

      ```text
      P1: lock(R1); lock(R2);
      P2: lock(R2); lock(R1);

      ```

→ Possibile situazione:

- P1 ottiene R1 e attende R2.
- P2 ottiene R2 e attende R1.
  → Nessuno può procedere ⇒ **deadlock**.

---

### 🔹 3. Condizioni necessarie per il deadlock

Perché si verifichi un deadlock, devono sussistere **tutte e quattro** le seguenti condizioni (Coffman, 1971):

1. **Mutua esclusione:**
   almeno una risorsa non può essere condivisa (es. stampante, mutex).

2. **Hold and wait:**
   un processo trattiene una risorsa e ne richiede altre.

3. **Nessuna prelazione (No preemption):**
   le risorse non possono essere forzatamente sottratte a un processo.

4. **Attesa circolare (Circular wait):**
   esiste una catena di processi in cui ciascuno attende una risorsa detenuta dal successivo.

[
P_1 → R_1 → P_2 → R_2 → … → P_n → R_n → P_1
]

Se anche una sola di queste condizioni viene impedita, il deadlock **non può verificarsi**.

---

### 🔹 4. Rappresentazione con il grafo delle risorse

Un **Resource Allocation Graph (RAG)** rappresenta graficamente le relazioni tra processi e risorse:

- **Nodo processo** → ( P_i )
- **Nodo risorsa** → ( R_j )
- **Arco di richiesta:** ( P_i → R_j )
- **Arco di assegnazione:** ( R_j → P_i )

#### Esempio

      ```text
      R1 → P1 → R2 → P2 → R1

      ```

→ ciclo → **deadlock potenziale**

- *Osservazioni:**

- Se non ci sono cicli → nessun deadlock.
- Se c’è un ciclo → possibile deadlock (certo, se ogni risorsa ha un solo istanza).

---

### 🔹 5. Strategie per la gestione del deadlock

#### a) Prevenzione

Evita a priori che si verifichi un deadlock, **impedendo una o più delle quattro condizioni**.

| Condizione       | Metodo di prevenzione                            |
| ---------------- | ------------------------------------------------ |
| Mutua esclusione | Usare risorse condivisibili dove possibile       |
| Hold and wait    | Richiedere tutte le risorse all’inizio           |
| No preemption    | Rimuovere risorse a processi bloccati            |
| Circular wait    | Imporre un ordine totale di acquisizione risorse |

- *Esempio:**
numerare tutte le risorse e richiederle sempre in ordine crescente.

- *Svantaggi:**

- Poca flessibilità.
- Spreco di risorse (processi che richiedono più del necessario).

---

#### b) Evitamento (Dynamic avoidance)

L’allocazione viene concessa solo se **mantiene il sistema in uno stato sicuro**.

Uno **stato sicuro** è tale che esiste un ordine di esecuzione dei processi che consente a ciascuno di terminare senza deadlock.

→ L’algoritmo principale di questa categoria è **l’Algoritmo del Banchiere**.

---

#### c) Rilevazione e recupero

Si **permette che il deadlock avvenga**, ma il sistema:

1. lo **rileva** (analizzando periodicamente il grafo delle risorse);
2. esegue un’azione di **recupero** (termina o sospende alcuni processi).

- *Metodi di recupero:**

- **Prelazione risorse:** forzare il rilascio da parte di un processo.
- **Rollback:** riportare un processo a uno stato precedente.
- **Terminazione selettiva:** uccidere uno o più processi coinvolti nel ciclo.

---

### 🔹 6. Algoritmo del Banchiere (Banker’s Algorithm)

Proposto da Dijkstra, l’**algoritmo del banchiere** è un metodo di **evitamento del deadlock** in cui il sistema decide se concedere una richiesta di risorsa **in base alla sicurezza dello stato risultante**.

#### Concetto

Un “banchiere” (il sistema) concede un prestito (una risorsa) solo se, anche dopo la concessione, **può garantire che tutti i clienti (processi)** saranno in grado di completare le loro operazioni in qualche ordine.

#### Parametri principali

| Simbolo                            | Significato                              |
| ---------------------------------- | ---------------------------------------- |
| `Available`                        | Risorse attualmente libere               |
| `Max[i]`                           | Risorse massime richieste dal processo i |
| `Allocation[i]`                    | Risorse già assegnate al processo i      |
| `Need[i] = Max[i] - Allocation[i]` | Risorse ancora necessarie                |

#### Procedura

1. Quando un processo `P_i` richiede una risorsa, il sistema controlla se:

         ```text
            Request[i] <= Need[i]
            Request[i] <= Available
         ```

   Se sì, si **simula l’assegnazione**.

2. Si verifica se il nuovo stato è **sicuro**:

   - esiste un ordine in cui tutti i processi possono completare.

3. Se lo stato è sicuro → la risorsa viene concessa;
   altrimenti → il processo viene sospeso.

#### Esempio (semplificato)

      ```text
      Available = [3, 3, 2]
      P1 Need = [7, 4, 3]
      P2 Need = [1, 2, 2]
      P3 Need = [6, 0, 0]

      ```

→ Il sistema valuta se concedere una richiesta senza uscire dallo stato sicuro.
Se la concessione rompe la condizione, la richiesta viene **posticipata**.

#### Limiti

- Richiede conoscenza preventiva di `Max[i]`.
- Costoso per grandi sistemi.
- Efficace solo per risorse riutilizzabili (CPU, I/O, memoria).

---

### 🔹 7. Riepilogo comparativo

| Strategia                | Quando agisce | Meccanismo               | Vantaggi              | Svantaggi                |
| ------------------------ | ------------- | ------------------------ | --------------------- | ------------------------ |
| **Prevenzione**          | Prima         | Evita condizioni di base | Semplice, sicura      | Inefficiente             |
| **Evitamento (Banker)**  | Durante       | Stato sicuro             | Flessibile            | Costoso, richiede Max[i] |
| **Rilevazione/Recupero** | Dopo          | Analisi grafi            | Adatto a batch system | Possibile perdita dati   |

---

### 🧠 Mappa concettuale di sintesi

      ```text
      SINCRONIZZAZIONE (II)
      │
      ├── Monitor
      │   ├─ Struttura: variabili, procedure, condizione
      │   ├─ wait / signal
      │   └─ Mutua esclusione automatica
      │
      ├── Deadlock
      │   ├─ Attesa reciproca tra processi
      │   ├─ Condizioni (Coffman):
      │   │   ├─ Mutua esclusione
      │   │   ├─ Hold and wait
      │   │   ├─ No preemption
      │   │   └─ Attesa circolare
      │   └─ RAG → rilevazione cicli
      │
      ├── Gestione deadlock
      │   ├─ Prevenzione → elimina condizioni
      │   ├─ Evitamento → stato sicuro (Banker)
      │   └─ Rilevazione e recupero → kill / rollback
      │
      └── Algoritmo del banchiere
         ├─ Available, Max, Allocation, Need
         ├─ Concede risorsa se stato resta sicuro
         └─ Evita il deadlock dinamicamente

      ```

## Gestione della memoria (I)

---

### 🔹 Introduzione

La **memoria centrale (RAM)** è una delle risorse più importanti e delicate di un sistema operativo, poiché costituisce il **luogo fisico dove vengono caricati i programmi** durante la loro esecuzione.
Il compito del sistema operativo è quello di **gestirla in modo efficiente, sicuro e flessibile**, consentendo la convivenza di più processi contemporaneamente senza che interferiscano tra loro.

La gestione della memoria deve garantire tre obiettivi fondamentali:

1. **Rilocazione** → permettere a un processo di essere spostato in memoria senza modificarne il codice.
2. **Protezione** → evitare che un processo acceda a zone di memoria appartenenti ad altri.
3. **Condivisione e uso efficiente** → sfruttare al massimo lo spazio disponibile minimizzando la frammentazione.

Inoltre, è necessario prevedere un meccanismo di **traduzione degli indirizzi logici in indirizzi fisici**, poiché ogni processo “vede” la memoria come se fosse un suo spazio indipendente, ma in realtà deve essere collocato da qualche parte nella RAM fisica.

---

### 🔹 1. Rilocazione

Ogni programma, quando viene compilato, genera **indirizzi logici** (o virtuali), che partono generalmente da 0.
Tuttavia, quando il programma viene caricato in memoria per l’esecuzione, **potrebbe non essere sempre possibile collocarlo nella stessa posizione fisica**.

#### Concetto

La **rilocazione** è il meccanismo che permette di **trasformare gli indirizzi logici** generati dal programma negli **indirizzi fisici effettivi** utilizzati in memoria.
Questa traduzione può avvenire in diversi momenti:

##### 1. Rilocazione statica

Avviene **al momento del caricamento** del programma.
Il compilatore o il loader calcolano gli indirizzi fisici prima dell’esecuzione.
→ Il programma non può essere spostato durante l’esecuzione.

##### 2. Rilocazione dinamica

Avviene **durante l’esecuzione** del programma.
Gli indirizzi logici vengono tradotti in indirizzi fisici **a runtime** tramite hardware dedicato (es. MMU – *Memory Management Unit*).
→ Il processo può essere spostato in memoria senza doverlo ricompilare.

#### Implementazione hardware

L’MMU gestisce due registri principali:

- **Registro base (Base Register)** → contiene l’indirizzo fisico iniziale dello spazio di memoria del processo.
- **Registro limite (Limit Register)** → indica la dimensione massima dello spazio del processo.

Ogni indirizzo logico generato dal programma viene tradotto come:

[
\text{Indirizzo fisico} = \text{Base} + \text{Indirizzo logico}
]

E viene controllato che non superi il valore di `Base + Limit`.

---

### 🔹 2. Protezione

La **protezione della memoria** serve a impedire che un processo possa **leggere o scrivere in aree non autorizzate**, preservando così l’integrità del sistema operativo e degli altri processi.

#### Meccanismi di protezione

1. **Controllo hardware con registri base/limite:**
   Ogni accesso a memoria è verificato dalla MMU: se l’indirizzo logico esce dal range consentito, viene generata un’**eccezione (trap)** e il processo viene bloccato.

2. **Bit di protezione:**
   In sistemi più evoluti, ogni blocco o pagina di memoria può avere **bit che definiscono i permessi** (lettura, scrittura, esecuzione).
   → Utilizzato nei sistemi a memoria virtuale (es. `rwx` in Linux).

3. **Modalità utente e kernel:**
   La CPU lavora in due modalità operative:

   - **User mode:** accesso limitato solo alla memoria utente.
   - **Kernel mode:** accesso completo a tutte le aree di memoria.

   Il cambio di modalità avviene solo tramite **system call o interrupt**.

---

### 🔹 3. Partizionamento della memoria

Il partizionamento rappresenta uno dei primi approcci alla gestione della memoria multiprogrammata.
Consiste nel **suddividere la RAM in più blocchi (partizioni)** nei quali possono essere caricati diversi processi contemporaneamente.

#### Tipi principali

##### 1. Partizionamento fisso (Fixed Partitioning)

La memoria viene divisa in **partizioni di dimensione predefinita** (uguale o diversa).
Ogni processo viene caricato in una partizione libera sufficientemente grande.

- *Vantaggi:**

- Implementazione semplice.
- Buona protezione (ogni processo resta nella propria partizione).

- *Svantaggi:**

- **Frammentazione interna:** se un processo non riempie la sua partizione, parte della memoria resta inutilizzata.
- Numero di processi limitato al numero di partizioni.
- Difficile adattarsi a programmi di dimensioni variabili.

---

##### 2. Partizionamento variabile (Dynamic Partitioning)

In questo approccio non ci sono partizioni fisse: la memoria viene **assegnata dinamicamente** in base alla dimensione del processo.

Quando un processo termina, la sua area viene liberata, ma ciò può generare **frammentazione esterna**, cioè spazi liberi non contigui e inutilizzabili singolarmente.

- *Soluzioni possibili:**

- **Compattazione:** spostare i processi in modo da riunire le aree libere in un unico blocco (operazione costosa).
- **Allocazione con strategie specifiche:**

  - **First Fit:** assegna la prima area libera sufficientemente grande.
  - **Best Fit:** assegna l’area più piccola possibile che soddisfi la richiesta.
  - **Worst Fit:** assegna l’area più grande disponibile (per ridurre la frammentazione residua).

---

### 🔹 4. Buddy System

Il **Buddy System** è un metodo di allocazione della memoria che combina l’efficienza del partizionamento variabile con la semplicità del fisso.
È largamente usato nei sistemi moderni (incluso Linux) per gestire la memoria fisica.

#### Funzionamento

L’idea è di dividere la memoria in blocchi di dimensione pari a potenze di 2.
Quando un processo richiede `n` byte, il sistema cerca il blocco più piccolo di potenza di 2 che possa contenerlo.

##### Allocazione

1. Se il blocco disponibile è troppo grande, viene **diviso in due metà (buddies)** di uguale dimensione.
2. Il processo viene collocato in uno dei due.
3. Le suddivisioni continuano finché non si trova un blocco sufficientemente piccolo.

##### Deallocazione

Quando il processo termina, il blocco viene liberato e, se il suo “buddy” adiacente è anch’esso libero, i due vengono **riuniti** (merge).
In questo modo il sistema riduce la frammentazione e riutilizza in modo efficiente la memoria.

#### Vantaggi

- Riduce la **frammentazione esterna**.
- Supporta facilmente la **compattazione dinamica**.
- Implementazione semplice con operazioni binarie.

#### Svantaggi

- Possibile **frammentazione interna** (se la richiesta non è esattamente una potenza di 2).
- Gli split e merge frequenti possono introdurre **overhead di gestione**.

---

### 🔹 5. Considerazioni generali

Ogni tecnica di gestione della memoria rappresenta un compromesso tra **flessibilità**, **efficienza** e **overhead di gestione**.
Sistemi moderni utilizzano combinazioni di più tecniche (es. buddy system per la memoria fisica + paging per quella virtuale).

---

### 🧠 Mappa concettuale di sintesi

      ```text
      GESTIONE DELLA MEMORIA (I)
      │
      ├── Obiettivi
      │   ├─ Rilocazione → indirizzi logici → fisici
      │   ├─ Protezione → accessi controllati
      │   └─ Uso efficiente → frammentazione minima
      │
      ├── Rilocazione
      │   ├─ Statica → traduzione al caricamento
      │   ├─ Dinamica → traduzione runtime (MMU)
      │   └─ Base + Limit Register
      │
      ├── Protezione
      │   ├─ Registri base/limite
      │   ├─ Bit di protezione (rwx)
      │   └─ Modalità user/kernel
      │
      ├── Partizionamento
      │   ├─ Fisso → frammentazione interna
      │   ├─ Variabile → frammentazione esterna
      │   │   └─ Strategie: First Fit, Best Fit, Worst Fit
      │
      └── Buddy System
         ├─ Blocchi in potenze di 2
         ├─ Split / Merge dinamico
         ├─ Vantaggi → meno frammentazione
         └─ Svantaggi → overhead e sprechi

      ```

## Gestione della memoria (II)

### 🔹 Introduzione

Le tecniche di **partizionamento fisso o variabile** viste in precedenza rappresentano i primi metodi di gestione della memoria multiprogrammata, ma hanno un limite evidente:
non permettono di eseguire programmi più grandi della memoria fisica disponibile.

Per superare questa restrizione nasce il concetto di **memoria virtuale**, una tecnica che consente di **astrarre la memoria logica da quella fisica**, permettendo ai processi di “vedere” uno spazio di indirizzi molto più ampio di quello realmente presente nella RAM.

---

### 🔹 1. Memoria virtuale

La **memoria virtuale** è un meccanismo che consente l’esecuzione di processi anche se **solo una parte del loro codice o dei loro dati è effettivamente in memoria**.
Le porzioni non necessarie vengono mantenute su disco (spazio di swap) e caricate solo quando richieste.

#### Obiettivi principali

- **Aumentare l’utilizzo della CPU:** i processi non restano in attesa di caricamento completo.
- **Permettere programmi più grandi della RAM fisica.**
- **Isolare gli spazi di memoria dei processi:** ogni processo ha una vista logica indipendente.
- **Gestire automaticamente il caricamento e lo scaricamento delle pagine.**

---

### 🔹 2. Paging

Il **paging** è la tecnica più diffusa per implementare la memoria virtuale.
Consiste nel suddividere la memoria (sia logica che fisica) in **blocchi di dimensione fissa**.

#### Concetti fondamentali

- **Pagina (Page):** unità logica di memoria (spazio del processo).
- **Frame:** blocco fisico di memoria (spazio RAM).
- Le dimensioni di pagina e frame sono identiche (tipicamente 4 KB, 8 KB, 16 KB).

Il sistema operativo mantiene una **mappa di corrispondenza** tra pagine logiche e frame fisici, contenuta nella **Page Table** (tabella delle pagine).

#### Funzionamento

1. Ogni indirizzo logico è composto da due parti:

         ```text

            [numero di pagina | offset]
         ```

   - Il numero di pagina identifica quale pagina logica viene utilizzata.
   - L’offset indica la posizione all’interno della pagina.

2. L’MMU, tramite la **Page Table**, traduce il numero di pagina nel **numero di frame** corrispondente:

         ```text
            indirizzo fisico = base frame + offset
         ```

3. Se la pagina non si trova in memoria (page fault), viene caricata dal disco nello spazio libero.

#### Vantaggi del paging

- Evita la **frammentazione esterna**, poiché i frame sono di dimensione fissa.
- Consente la **rilocazione dinamica** e la **protezione per pagina**.
- Permette **memoria virtuale più ampia** della fisica.

#### Svantaggi

- **Frammentazione interna:** l’ultima pagina di un processo potrebbe non essere completamente utilizzata.
- **Overhead di traduzione:** ogni accesso richiede consultare la tabella delle pagine.

---

### 🔹 3. Page Table (Tabella delle pagine)

La **Page Table** è una struttura dati fondamentale che associa ogni pagina logica a un frame fisico.
Ogni processo ha la propria tabella delle pagine.

#### Contenuto di ogni voce (entry)

| Campo                  | Descrizione                                                |
| ---------------------- | ---------------------------------------------------------- |
| **Frame number**       | Numero del frame fisico associato alla pagina              |
| **Present bit**        | Indica se la pagina è attualmente in memoria               |
| **Modified/Dirty bit** | Indica se la pagina è stata modificata (serve per lo swap) |
| **Access bit**         | Usato per implementare politiche di rimpiazzo              |
| **Protection bits**    | Specificano i permessi (lettura, scrittura, esecuzione)    |

---

#### Accesso alla Page Table

L’accesso alla Page Table introduce un **problema di prestazioni**, perché per ogni operazione di lettura/scrittura su memoria si dovrebbero fare **due accessi**:

1. Uno alla Page Table per ottenere l’indirizzo fisico.
2. Uno alla memoria effettiva per leggere/scrivere i dati.

Per ridurre questo overhead, si introduce una cache hardware dedicata: la **TLB**.

---

### 🔹 4. Translation Lookaside Buffer (TLB)

La **TLB (Translation Lookaside Buffer)** è una **cache interna alla MMU** che memorizza le traduzioni recenti tra pagine logiche e frame fisici.
Il suo scopo è **velocizzare la traduzione degli indirizzi**.

#### Funzionamento

1. Quando un processo genera un indirizzo logico, l’MMU controlla prima nella TLB:

   - Se la traduzione è presente (**TLB hit**) → l’indirizzo fisico è immediatamente disponibile.
   - Se non è presente (**TLB miss**) → viene consultata la Page Table, e la traduzione viene poi memorizzata nella TLB.

2. La TLB ha dimensioni ridotte (tipicamente da 16 a 512 voci) e viene gestita con politiche di rimpiazzo simili a quelle della cache (LRU, FIFO).

#### Vantaggi

- Riduce drasticamente il tempo medio di accesso alla memoria.
- Migliora le prestazioni della memoria virtuale senza modificare la logica di paging.

#### Svantaggi

- Costo hardware elevato.
- Necessità di aggiornamento in caso di cambio di contesto (ogni processo ha la propria Page Table → invalidazione TLB).

---

### 🔹 5. Paging multilivello

Per processi molto grandi, la Page Table può diventare **enorme**.
Esempio: uno spazio di indirizzamento logico di 32 bit con pagine da 4 KB → 2²⁰ voci per tabella (oltre 4 MB per processo).

Per ridurre l’uso di memoria, si utilizza la **Page Table multilivello**, che suddivide la tabella in più parti.

#### Funzionamento

1. L’indirizzo logico è diviso in più campi:

         ```text
            [indice livello 1 | indice livello 2 | offset]
         ```

2. Solo i livelli necessari vengono mantenuti in memoria (gli altri possono restare su disco).
3. In sistemi a 64 bit, si usano fino a **4 o 5 livelli** di tabelle (es. x86-64 con PML4, PDPT, PD, PT).

#### Vantaggi

- Riduce l’uso di memoria per le tabelle.
- Supporta grandi spazi di indirizzamento (64 bit).
- Pagina le Page Table stesse (memoria virtuale ricorsiva).

#### Svantaggi

- Aumenta la complessità hardware e i tempi di traduzione (più accessi successivi).
- Compensato dalla presenza della TLB.

---

### 🔹 6. Segmentazione

Il **paging** divide la memoria in blocchi di dimensione fissa, ma alcuni programmi sono più naturalmente suddivisi in **unità logiche di dimensione variabile** (funzioni, stack, heap, moduli).
Per questo nasce la **segmentazione**.

#### Concetto

La segmentazione suddivide la memoria logica in **segmenti** distinti, ciascuno con **un significato logico** (es. codice, dati, stack).

Ogni indirizzo logico è composto da:

[
\text{<numero segmento, offset>}
]

#### Struttura hardware

Il sistema mantiene una **Segment Table**, in cui ogni voce contiene:

| Campo          | Descrizione                             |
| -------------- | --------------------------------------- |
| **Base**       | Indirizzo fisico di inizio del segmento |
| **Limit**      | Dimensione del segmento                 |
| **Protezione** | Permessi di accesso                     |

#### Vantaggi

- Maggiore **modularità e sicurezza** (ogni segmento può essere protetto).
- Più adatta ai linguaggi ad alto livello (mappa direttamente funzioni e strutture dati).
- Facile condivisione di segmenti comuni (es. librerie condivise).

#### Svantaggi

- **Frammentazione esterna** (i segmenti sono di dimensione variabile).
- Complessità di gestione rispetto al paging puro.

---

### 🔹 7. Segmentazione con Paging (ibrido)

I sistemi moderni (es. **x86**) combinano **segmentazione** e **paging**, sfruttando i vantaggi di entrambi.

#### Funzionamento

1. Ogni segmento ha la propria tabella delle pagine.
2. L’indirizzo logico diventa:

         ```text
            [segmento | pagina | offset]
         ```

3. Il segmento fornisce la base logica, mentre il paging gestisce la mappatura fisica.

#### Vantaggi

- Flessibilità e modularità della segmentazione.
- Efficienza e assenza di frammentazione esterna del paging.

#### Svantaggi

- Aumento dell’overhead di traduzione (più livelli da risolvere).
- Implementazione hardware più complessa.

---

### 🧠 Mappa concettuale di sintesi

      ```text
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

## Gestione della memoria (III)

---

### 🔹 Introduzione

Dopo aver introdotto la memoria virtuale e i meccanismi di paging, resta da affrontare uno degli aspetti più complessi della gestione della memoria: **la scelta delle pagine da mantenere in RAM e quelle da rimpiazzare** quando la memoria fisica è piena.

Ogni volta che un processo accede a una pagina non presente in memoria, si verifica un **page fault**, che richiede di caricare la pagina dal disco.
Questo evento è molto costoso (migliaia di cicli di CPU) e influisce direttamente sulle prestazioni del sistema.

Per questo motivo, è fondamentale adottare **algoritmi di rimpiazzo** efficienti e strategie di controllo che limitino il numero di page fault e prevengano fenomeni di **thrashing**.

---

### 🔹 1. Page Fault e Swapping

Un **page fault** si verifica quando un processo accede a una pagina che **non è attualmente in memoria fisica**.
Il sistema operativo interviene con una serie di operazioni:

1. **Interruzione** → la CPU rileva il page fault e passa il controllo al sistema operativo.
2. **Verifica** → si controlla se l’indirizzo richiesto è valido e la pagina appartiene effettivamente al processo.
3. **Scelta del frame da liberare** → se la memoria è piena, occorre liberare un frame usando un **algoritmo di rimpiazzo**.
4. **Scrittura su disco** → se la pagina nel frame scelto è “dirty”, viene salvata (scritta su disco).
5. **Caricamento della nuova pagina** → la pagina mancante viene caricata dallo spazio di swap nel frame libero.
6. **Aggiornamento delle tabelle** (Page Table e TLB).
7. **Ripresa dell’esecuzione** dal punto in cui il processo era stato interrotto.

Il **tempo medio di accesso effettivo alla memoria (EAT)** dipende dalla frequenza di page fault e dal tempo necessario per gestirli:

[
EAT = (1 - p) \times t_m + p \times t_{pf}
]

dove:

- ( t_m ) = tempo di accesso alla memoria,
- ( p ) = probabilità di page fault,
- ( t_{pf} ) = tempo di servizio del page fault (molto elevato).

Anche una piccola percentuale di page fault (es. 0,01%) può aumentare drasticamente il tempo medio di accesso.

---

### 🔹 2. Algoritmi di rimpiazzo delle pagine

Quando non ci sono frame liberi, il sistema operativo deve scegliere **quale pagina rimuovere dalla memoria** per fare spazio a quella nuova.
Questa decisione è critica: una scelta sbagliata può aumentare il numero di page fault.

Di seguito i principali algoritmi, dal più semplice al più sofisticato.

---

#### FIFO – *First In, First Out*

- Le pagine vengono gestite in una coda circolare: la più vecchia viene rimpiazzata per prima.
- Implementazione semplice, ma **non tiene conto dell’utilizzo effettivo**.

- *Problemi:**

- Possibile **anomalìa di Belady** → aumentando il numero di frame, i page fault possono aumentare invece di diminuire.
- Scarsa efficienza per programmi che riutilizzano frequentemente le stesse pagine.

---

#### OPT – *Optimal Replacement* (teorico)

- Rimpiazza la pagina che **non sarà più utilizzata per il periodo di tempo più lungo**.
- È l’algoritmo ideale in termini di prestazioni minime di page fault.

- *Limite:**
Non può essere implementato realmente, perché richiede la conoscenza futura della sequenza di accessi.
→ Viene usato come **riferimento teorico** per confrontare le prestazioni degli altri algoritmi.

---

#### LRU – *Least Recently Used*

- Rimpiazza la pagina **non utilizzata da più tempo**.
- Si basa sul principio di **località temporale**: le pagine usate di recente tenderanno a essere usate ancora a breve.

- *Implementazioni possibili:**

1. **Contatori temporali:** ogni pagina ha un timestamp aggiornato a ogni accesso.
   → quando serve rimpiazzare, si sceglie quella con il timestamp più vecchio.
   (Preciso ma costoso da aggiornare a ogni accesso).

2. **Stack (lista ordinata):** le pagine sono mantenute in una lista, e ogni accesso sposta la pagina in testa.
   → buona accuratezza ma overhead alto.

- *Vantaggi:**

- Prestazioni vicine all’ottimo.

- *Svantaggi:**

- Costi hardware e software elevati per mantenere lo storico.

---

#### Second-Chance (Clock Algorithm)

È una **versione approssimata di LRU**, molto usata nei sistemi reali.
Le pagine sono disposte in un **buffer circolare** (come FIFO), ma ogni pagina ha un **bit di riferimento (R)**.

- *Funzionamento:**

1. Quando si deve rimpiazzare una pagina, si controlla il bit R della pagina “più vecchia”:

   - Se R = 0 → viene rimpiazzata.
   - Se R = 1 → il bit viene azzerato e la pagina riceve una “seconda possibilità”.
2. L’indicatore (clock hand) avanza fino a trovare una pagina con R = 0.

- *Vantaggi:**

- Prestazioni simili a LRU, ma con overhead ridotto.
- Implementazione efficiente a livello hardware.

---

#### NRU – *Not Recently Used*

Classifica le pagine in quattro categorie, combinando due bit:

| Bit R | Bit M | Categoria                        | Priorità di rimpiazzo |
| ----- | ----- | -------------------------------- | --------------------- |
| 0     | 0     | Non usata né modificata          | Alta                  |
| 0     | 1     | Non usata, modificata            | Media                 |
| 1     | 0     | Usata di recente, non modificata | Bassa                 |
| 1     | 1     | Usata e modificata               | Molto bassa           |

L’algoritmo sceglie una pagina casuale dalla **classe con priorità più alta** disponibile.
Semplice ma meno preciso rispetto a LRU.

---

#### LFU – *Least Frequently Used*

Rimuove la pagina **meno utilizzata nel tempo** (in base a un contatore di accessi).
Buono per carichi stabili, ma può reagire male a variazioni improvvise di comportamento (pagine vecchie ma “popolari” restano troppo a lungo).

---

### 🔹 3. Algoritmi di allocazione dei frame

Ogni processo deve avere assegnato un certo numero di **frame** in memoria fisica.
Il sistema operativo deve stabilire **quanti frame concedere** e come gestirli nel tempo.

#### Allocazione fissa vs dinamica

- **Allocazione fissa:**
  ogni processo riceve un numero costante di frame per tutta la durata.
  → semplice ma inefficiente se i processi cambiano comportamento.

- **Allocazione dinamica:**
  i frame vengono assegnati e revocati dinamicamente in base al carico o al numero di page fault.

#### Allocazione proporzionale

I frame vengono assegnati in proporzione alla dimensione del processo:
[
\text{frame_i} = \frac{\text{dimensione_i}}{\text{totale_memoria}} \times \text{frame_totali}
]

#### Allocazione con priorità

I processi con priorità più alta ricevono più frame (o frame riservati) per ridurre il rischio di page fault critici.

---

### 🔹 4. Thrashing

Il **thrashing** è un fenomeno che si verifica quando un processo spende più tempo a eseguire operazioni di **paging (swap in/out)** che ad eseguire istruzioni utili.
In pratica, la memoria è troppo piccola per mantenere il **working set** del processo, causando continui page fault.

#### Cause principali

- Numero di processi troppo alto rispetto alla RAM disponibile.
- Allocazione inadeguata dei frame.
- Algoritmi di rimpiazzo non ottimali.

#### Effetti

- Crollo del throughput.
- CPU fortemente sotto-utilizzata (la maggior parte del tempo attende I/O).
- Drastico rallentamento del sistema.

---

### 🔹 5. Modelli di controllo del thrashing

#### a) Working Set Model

Il **working set** di un processo è l’insieme delle pagine che **sono state utilizzate recentemente** in una finestra temporale ∆ (numero di riferimenti).

L’idea è che un processo ha bisogno di mantenere in RAM il proprio working set per funzionare in modo efficiente.

- *Strategia:**

- Si monitora il working set di ciascun processo.
- Se la somma dei working set di tutti i processi supera la memoria fisica, il sistema sospende o swap-out alcuni processi.
  → Evita il thrashing globale.

#### b) Page Fault Frequency (PFF)

Si basa sulla **frequenza di page fault** del processo:

- Se la frequenza di page fault è **troppo alta**, vengono assegnati più frame.
- Se è **troppo bassa**, alcuni frame vengono tolti (per essere assegnati ad altri processi).

Questo metodo consente un adattamento dinamico in base al comportamento effettivo.

---

### 🔹 6. Prestazioni e compromessi

Il controllo della memoria virtuale si basa su un equilibrio tra:

- **Numero di frame assegnati** ↔ **page fault rate**
- **Politiche di rimpiazzo** ↔ **overhead di gestione**
- **Multiprogrammazione** ↔ **thrashing**

Un sistema operativo efficiente deve saper **adattare dinamicamente le politiche di allocazione e sostituzione** in funzione del carico.

---

### 🧠 Mappa concettuale di sintesi

      ```text

      GESTIONE DELLA MEMORIA (III)
      │
      ├── Page Fault
      │   ├─ Rilevamento e gestione
      │   ├─ Swapping su disco
      │   └─ Tempo medio EAT = (1-p)*tm + p*tpf
      │
      ├── Algoritmi di rimpiazzo
      │   ├─ FIFO → semplice, ma Belady
      │   ├─ OPT → ideale, teorico
      │   ├─ LRU → località temporale
      │   ├─ Second-Chance → approssimazione LRU
      │   ├─ NRU → classi R/M
      │   └─ LFU → frequenza accessi
      │
      ├── Allocazione frame
      │   ├─ Fissa vs dinamica
      │   ├─ Proporzionale → dimensione processo
      │   └─ Per priorità
      │
      ├── Thrashing
      │   ├─ Cause → troppe page fault
      │   ├─ Effetti → CPU inattiva, swap continuo
      │   └─ Soluzioni → Working Set, PFF
      │
      └── Controllo dinamico
         ├─ Working Set → memoria minima necessaria
         └─ PFF → adattamento automatico

      ```

---

Vuoi che per **Martedì 14/10 – File System (I)** passiamo alla parte su **organizzazione, strutture, e gestione dei file (directory, metadati, allocazione)** con lo stesso stile e profondità?

## File System (I)

### 🔹 Introduzione generale

Il **file system** è la componente del sistema operativo che gestisce la **memorizzazione permanente dei dati**.
A differenza della memoria principale (RAM), la memoria di massa è **non volatile**, quindi mantiene i dati anche dopo lo spegnimento del sistema.

Il file system si occupa di:

- **organizzare i dati** in strutture logiche (file, directory);
- **gestire lo spazio su disco**;
- **fornire accesso controllato e sicuro** ai dati;
- **astrarre i dispositivi fisici**, offrendo un’interfaccia uniforme ai programmi.

Dal punto di vista dell’utente e dei processi, il file system fornisce un modello **astratto** del disco:
ogni dispositivo di memoria è visto come un insieme di **file e cartelle**, indipendentemente dal tipo di hardware sottostante.

---

### 🔹 1. Concetto di file

Un **file** è un insieme di informazioni memorizzate su un supporto di memoria secondaria, gestite come un’unica unità logica.
Il sistema operativo fornisce una **struttura uniforme** per tutti i file, indipendentemente dal loro contenuto.

#### Tipi di file

- **File di testo:** sequenze di caratteri leggibili (es. `.txt`, `.c`, `.md`).
- **File binari:** contengono dati non interpretati direttamente come caratteri (es. eseguibili, immagini, database).
- **File di sistema:** file speciali gestiti dal kernel (es. `/proc` in Linux, device file in `/dev`).

#### Attributi di un file

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

### 🔹 2. Operazioni sui file

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

### 🔹 3. Struttura logica del file system

Il file system non si limita a gestire file individuali, ma organizza l’intera memoria di massa in **livelli logici**.
Questa stratificazione permette di separare le funzioni astratte (viste dall’utente) dai dettagli fisici del disco.

#### Livelli principali

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

### 🔹 4. Struttura delle directory

Le **directory** (o cartelle) sono file speciali che contengono **elenco e metadati** dei file presenti in una determinata area del file system.
Servono a organizzare e raggruppare logicamente i dati.

#### Tipi di struttura delle directory

##### a) Struttura a livello singolo

Tutti i file si trovano in un’unica directory.
→ Molto semplice ma **non scalabile**: i nomi devono essere univoci e l’organizzazione diventa caotica.

##### b) Struttura a due livelli

Ogni utente ha la propria directory separata (es. `/home/utente1/`, `/home/utente2/`).
→ Migliora l’organizzazione, ma non consente gerarchie più profonde.

##### c) Struttura gerarchica (ad albero)

È la struttura più comune (usata in UNIX, Linux, Windows).
Ogni directory può contenere file e altre directory.
→ Permette un’organizzazione logica e modulare.

- *Esempio:**

      ```text
      /
      ├── bin/
      ├── home/
      │   ├── emiliano/
      │   │   ├── documenti/
      │   │   └── immagini/
      └── etc/

      ```

##### d) Strutture con link

Alcuni file system supportano **collegamenti (link)** che puntano a file o directory esistenti:

- **Hard link:** riferimento diretto allo stesso inode (identico file).
- **Symbolic link (soft link):** file separato che contiene il percorso del file originale.

---

### 🔹 5. Gestione dello spazio su disco

Il disco è suddiviso in **blocchi fisici** (tipicamente da 512 byte a 4 KB).
Il file system deve assegnare questi blocchi ai file in modo efficiente, tenendo conto di prestazioni e frammentazione.

#### Metodi di allocazione

##### a) Allocazione contigua

I blocchi di un file sono memorizzati in **posizioni consecutive** sul disco.

- *Vantaggi:**

- Accesso sequenziale molto veloce (i dati sono adiacenti).
- Facile calcolo dell’indirizzo fisico.

- *Svantaggi:**

- Necessario conoscere la dimensione del file in anticipo.
- **Frammentazione esterna**: difficile trovare blocchi contigui liberi.

---

##### b) Allocazione concatenata (Linked allocation)

Ogni file è una **catena di blocchi** collegati da puntatori.
Il primo blocco contiene un riferimento al successivo, e così via.

- *Vantaggi:**

- Nessuna frammentazione esterna.
- Facile estendere i file.

- *Svantaggi:**

- Accesso casuale lento (necessario attraversare la catena).
- Overhead di spazio per i puntatori.
- Rischio di perdita di dati se un blocco della catena si danneggia.

---

##### c) Allocazione indicizzata

Ogni file ha una **tabella di indice** (index block) che elenca tutti i blocchi che compongono il file.
Simile alla Page Table nella memoria virtuale.

- *Vantaggi:**

- Accesso diretto e casuale efficiente.
- Nessuna frammentazione esterna.
- Facile estensione del file.

- *Svantaggi:**

- Overhead di spazio per mantenere gli indici.
- L’indice stesso deve essere memorizzato e gestito come file.

- *Esempio (in UNIX):**
Il sistema usa strutture **inode**, dove ogni inode contiene:

- indirizzi diretti (blocchi immediati),
- indiretti singoli, doppi e tripli (puntatori a tabelle di indirizzi).

---

### 🔹 6. Gestione dei metadati: inode

Nei sistemi UNIX/Linux, ogni file è rappresentato da un **inode** (index node), una struttura che memorizza **tutte le informazioni sul file tranne il nome**.

#### Contenuto di un inode

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

### 🔹 7. Montaggio del file system

I moderni sistemi supportano **più file system contemporaneamente** (es. ext4, FAT32, NTFS, ecc.), montati in una **gerarchia unica**.

L’operazione di **mount** associa un file system fisico (es. una partizione o chiavetta) a una directory esistente nel file system principale.

- *Esempio:**

      ```bash
      mount /dev/sdb1 /mnt/usb
      ```

      → La partizione `sdb1` sarà accessibile sotto la directory `/mnt/usb`.

      ---

### 🧠 Mappa concettuale di sintesi

      ```text
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

## File System (II)

### 🔹 Introduzione

Dopo aver analizzato la struttura logica dei file system e i meccanismi di allocazione dei file, in questa lezione approfondiamo **la gestione dello spazio libero**, **le strutture dati interne (FAT e inode)**, e i meccanismi che garantiscono **l’integrità e la coerenza dei dati**, come **il journaling e la cache del disco**.

L’obiettivo del file system è non solo memorizzare i dati, ma **preservarli in modo sicuro e coerente** anche in caso di crash o spegnimenti improvvisi, mantenendo buone prestazioni di accesso.

---

### 🔹 1. Gestione dello spazio libero

Ogni file system deve gestire **l’insieme dei blocchi liberi** del disco, in modo da poterli assegnare ai file che crescono o ai nuovi file creati.
La scelta della tecnica influenza fortemente la **velocità di allocazione**, l’**uso efficiente dello spazio** e la **facilità di recupero** in caso di errore.

#### Tecniche principali

##### a) Bitmap (mappa dei bit)

Il disco è rappresentato da una sequenza di **bit**, uno per ogni blocco:

- `1` → blocco occupato
- `0` → blocco libero

- *Vantaggi:**

- Ricerca rapida di blocchi liberi (si possono usare istruzioni bitwise).
- Struttura compatta (es. 1 bit per 4 KB → 128 KB di bitmap per 1 TB di disco).
- Facile salvataggio e aggiornamento.

- *Svantaggi:**

- Serve scansionare la bitmap per trovare gruppi contigui di blocchi (per file grandi).
- Se frammentata, le prestazioni di lettura peggiorano.

---

##### b) Lista concatenata di blocchi liberi (Linked free list)

Tutti i blocchi liberi sono collegati tra loro tramite puntatori: ogni blocco libero contiene l’indirizzo del successivo.

- *Vantaggi:**

- Implementazione semplice.
- Non serve una tabella separata in memoria.

- *Svantaggi:**

- Accesso lento (deve attraversare l’intera lista).
- Se un blocco della lista si danneggia → perdita di collegamento a tutti i blocchi successivi.

---

##### c) Gruppi di blocchi liberi (Grouping)

Usata in alcuni file system UNIX:
ogni blocco libero contiene **indirizzi di più blocchi liberi** (un piccolo array di puntatori), e l’ultimo puntatore rimanda al gruppo successivo.

→ Compromesso tra lista concatenata e bitmap: riduce il numero di accessi per individuare nuovi blocchi.

---

##### d) Contatori (Counting)

Usata quando più blocchi liberi sono consecutivi:
invece di elencarli tutti, si memorizza una coppia `(indirizzo iniziale, quantità)`.

- *Esempio:**
(200, 5) → blocchi liberi 200–204.

- *Vantaggi:**

- Ideale per file system che liberano interi segmenti di blocchi insieme.
- Molto compatta.

---

### 🔹 2. Strutture dati interne: FAT e inode

#### a) FAT – *File Allocation Table*

Usata nei file system della famiglia **MS-DOS, FAT16, FAT32**.

La FAT è una **grande tabella** in cui ogni voce corrisponde a un blocco del disco e contiene:

- `0` → blocco libero
- `EOF` → ultimo blocco del file
- valore `x` → blocco successivo nella catena del file

Il sistema tiene una sola copia (o due per sicurezza) della tabella FAT all’inizio del disco.

- *Esempio:**

      ```text
      Blocco 5 → 9
      Blocco 9 → 13
      Blocco 13 → EOF
      ```

Significa che il file occupa i blocchi 5 → 9 → 13.

- *Vantaggi:**

- Implementazione semplice.
- Facile navigazione sequenziale dei file.
- Indipendente dal tipo di dispositivo.

- *Svantaggi:**

- Tutta la tabella deve risiedere in memoria → poco scalabile per dischi grandi.
- Accesso casuale costoso (bisogna attraversare la catena).
- Facilmente danneggiabile (la corruzione della FAT può compromettere tutto il file system).

---

#### b) inode (UNIX / Linux)

Ogni file è descritto da un **inode**, che contiene tutte le informazioni di gestione e i puntatori ai blocchi di dati.

Come visto, l’inode mantiene:

- **Puntatori diretti** → fino a 12 blocchi dati immediati
- **Puntatori indiretti singoli, doppi, tripli** → strutture ricorsive che permettono di raggiungere file molto grandi

- *Esempio tipico (ext4):**

| Tipo di puntatore   | Descrizione                                       | Copertura approssimata |
| ------------------- | ------------------------------------------------- | ---------------------- |
| 12 diretti          | Puntano direttamente ai blocchi dati              | File piccoli (~48 KB)  |
| 1 indiretto singolo | Puntatore a blocco contenente altri indirizzi     | ~4 MB                  |
| 1 indiretto doppio  | Puntatore a blocchi di indirizzi di altri blocchi | ~4 GB                  |
| 1 indiretto triplo  | Puntatore a blocchi di indirizzi di indirizzi     | ~4 TB                  |

Questo approccio rende gli inode **flessibili e scalabili**, ma introduce un **overhead maggiore** per i file di grandi dimensioni (più accessi a livelli intermedi).

---

### 🔹 3. Gestione dello spazio libero e allocazione combinata

I file system moderni (es. ext4, NTFS, APFS, XFS) combinano più tecniche per **massimizzare efficienza e integrità**:

- **Bitmap per lo spazio libero** → rapida individuazione blocchi.
- **Inode o strutture indicizzate** → gestione efficiente dei file.
- **Allocazione per estensioni (extent)** → blocchi contigui trattati come un’unica unità logica (riduce frammentazione e overhead).

#### Extent

Un **extent** rappresenta una sequenza contigua di blocchi fisici assegnati a un file.
Invece di memorizzare ogni blocco singolo, l’inode memorizza `(blocco_inizio, lunghezza)`.

- *Vantaggi:**

- Migliore località spaziale (file più compatti sul disco).
- Meno frammentazione e minore overhead nella tabella degli indici.

- *Usato in:** ext4, XFS, NTFS, Btrfs.

---

### 🔹 4. Journaling e coerenza del file system

Uno dei problemi principali dei file system tradizionali è la **perdita di coerenza** in caso di crash (es. interruzione di corrente durante la scrittura).
Il **journaling** è un meccanismo che registra **le operazioni imminenti su un’area speciale del disco (journal)** prima di eseguirle realmente.

#### Funzionamento

1. Ogni operazione (creazione, eliminazione, modifica) viene **scritta nel journal** come transazione.
2. Solo dopo la conferma della scrittura nel journal, l’operazione viene **eseguita sui dati reali**.
3. Se il sistema si blocca prima del completamento, al riavvio il file system **legge il journal** e:

   - applica le operazioni non ancora completate, oppure
   - le annulla per mantenere la consistenza.

#### Tipi di journaling

- **Write-ahead logging:** scrive prima nel journal, poi nei blocchi dati (metodo standard).
- **Ordered journaling:** prima i dati, poi i metadati (usato in ext3/ext4).
- **Full data journaling:** registra anche i contenuti dei file (massima sicurezza, ma rallenta).

#### Vantaggi

- Riduce drasticamente i tempi di recupero dopo crash.
- Garantisce la **consistenza dei metadati**.
- Evita la necessità di eseguire lo scan completo del disco (come `fsck`).

#### Svantaggi

- Overhead in scrittura (ogni operazione viene duplicata).
- Journal stesso può frammentarsi nel tempo.

---

### 🔹 5. Cache del disco e buffering

Per migliorare le prestazioni, il sistema operativo utilizza **buffer in memoria** per evitare accessi frequenti e lenti al disco.
Questa tecnica è gestita dal **buffer cache** o **page cache** del kernel.

#### Tipologie di cache

1. **Read cache:**
   Le pagine lette dal disco vengono mantenute in RAM; se lo stesso file viene letto di nuovo, l’accesso è immediato.

2. **Write-back cache:**
   Le scritture non vengono eseguite subito sul disco ma accumulate e scritte periodicamente o al rilascio del file.

3. **Write-through cache:**
   Ogni scrittura aggiorna immediatamente il disco → maggiore sicurezza ma minore velocità.

#### Vantaggi

- Accesso ai file fino a 100× più rapido rispetto all’I/O diretto.
- Riduzione delle scritture ridondanti.
- Maggiore parallelismo tra processi e I/O.

#### Svantaggi

- Perdita di dati in caso di crash prima dello svuotamento del buffer.
- Necessità di sincronizzazione (`sync`, `fsync`) per forzare il flush dei dati sul disco.

---

### 🔹 6. Verifica e recupero della consistenza

Nonostante i meccanismi di journaling, possono verificarsi errori dovuti a:

- danni fisici del disco,
- corruzione del journal,
- errori di sincronizzazione.

I sistemi UNIX/Linux utilizzano comandi di controllo come:

- **`fsck` (file system check):** analizza e corregge le incongruenze (blocchi orfani, inode non referenziati).
- **`e2fsck`:** specifico per file system ext2/3/4.
- **`xfs_repair`:** per XFS.

Durante la verifica, il sistema confronta bitmap, inode e directory per ricostruire la struttura logica corretta.

---

### 🧠 Mappa concettuale di sintesi

      ```text

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

## Sicurezza e Protezione

---

### 🔹 Introduzione

Un sistema operativo non deve solo gestire risorse e processi in modo efficiente: deve anche **proteggerli** da accessi non autorizzati e **preservare la sicurezza dei dati e delle operazioni**.
In altre parole, deve garantire che ogni processo o utente **possa accedere solo alle risorse per le quali è autorizzato**.

La **protezione** riguarda la **correttezza e l’integrità interna del sistema**, mentre la **sicurezza** si estende anche a minacce esterne (es. accessi da rete, utenti malevoli, malware).

Questi due concetti, spesso sovrapposti, si distinguono così:

| Aspetto             | Protezione                             | Sicurezza                           |
| ------------------- | -------------------------------------- | ----------------------------------- |
| Scopo               | Limitare l’uso improprio delle risorse | Impedire violazioni e attacchi      |
| Origine del rischio | Interna (errori, conflitti)            | Esterna (malware, intrusione)       |
| Mezzo               | Meccanismi di controllo accessi        | Cifratura, autenticazione, auditing |

---

### 🔹 1. Obiettivi della protezione

Il sistema operativo deve garantire:

1. **Integrità:** le risorse possono essere modificate solo da soggetti autorizzati.
2. **Riservatezza:** le informazioni sono accessibili solo a chi ne ha diritto.
3. **Disponibilità:** le risorse devono rimanere accessibili agli utenti legittimi.

Per ottenere questi obiettivi, il sistema definisce un **modello di accesso controllato** tra *soggetti* (processi, utenti) e *oggetti* (file, dispositivi, aree di memoria).

---

### 🔹 2. Domini di protezione

Un **dominio di protezione** è un insieme di risorse e permessi associati a un soggetto (es. utente o processo).
Ogni dominio definisce **cosa un soggetto può fare** su un determinato oggetto.

Esempio:

| Oggetto         | Operazioni consentite |
| --------------- | --------------------- |
| File personale  | read, write           |
| File di sistema | read                  |
| Stampante       | write                 |
| Disco di swap   | nessuna               |

Durante l’esecuzione, un processo può **cambiare dominio** (es. quando passa da modalità utente a kernel tramite una *system call*).

#### Implementazione pratica

- In UNIX/Linux ogni processo ha **UID (User ID)** e **GID (Group ID)**.
- Il kernel verifica i permessi ogni volta che viene effettuata un’operazione su un file o una risorsa.

---

### 🔹 3. Matrice di accesso

Il modello generale di protezione può essere rappresentato da una **matrice di accesso**, dove:

- **righe** = soggetti (utenti, processi);
- **colonne** = oggetti (file, dispositivi, memoria);
- **celle** = diritti di accesso concessi (read, write, execute).

#### Esempio

|             | file1   | file2 | stampante |
| ----------- | ------- | ----- | --------- |
| **utente1** | r, w    | r     | w         |
| **utente2** | r       | –     | –         |
| **root**    | r, w, x | r, w  | w         |

#### Rappresentazioni compatte

Poiché la matrice completa è molto grande e sparsa (molti campi vuoti), nella pratica si usano due approcci:

##### a) Liste di controllo d’accesso (ACL – Access Control List)

Per ogni **oggetto** si mantiene l’elenco dei soggetti che possono accedervi e con quali permessi.

Esempio:

      ```text
      file1 → [(utente1, rw), (utente2, r), (root, rwx)]

      ```

→ tipico modello UNIX (`rwxr-xr--`).

##### b) Capability List

Per ogni **soggetto** si mantiene l’elenco degli oggetti a cui può accedere e con quali diritti.

Esempio:

      ```text
      utente1 → [(file1, rw), (stampante, w)]

      ```

→ tipico dei sistemi distribuiti o microkernel (es. Mach, seL4).

---

### 🔹 4. Meccanismi di controllo accessi

#### a) File system e permessi UNIX

Ogni file ha associati tre insiemi di permessi:

| Categoria      | Descrizione                            |
| -------------- | -------------------------------------- |
| **User (u)**   | Proprietario del file                  |
| **Group (g)**  | Utenti appartenenti allo stesso gruppo |
| **Others (o)** | Tutti gli altri utenti                 |

E tre bit di permesso:

| Permesso | Significato |
| -------- | ----------- |
| **r**    | lettura     |
| **w**    | scrittura   |
| **x**    | esecuzione  |

Esempio:

      ```text
      -rwxr-xr--
      ```

= il proprietario può leggere/scrivere/eseguire,
il gruppo può leggere/eseguire,
gli altri possono solo leggere.

#### b) Bit speciali

- **setuid (s):** esegue il programma con i permessi del proprietario, non dell’utente corrente (es. `passwd`).
- **setgid (s):** eredita il gruppo del file.
- **sticky bit (t):** nei file condivisi (es. `/tmp`) impedisce la cancellazione da parte di utenti non proprietari.

---

### 🔹 5. Autenticazione e autorizzazione

#### Autenticazione

È il processo di **verifica dell’identità** dell’utente.

Metodi principali:

1. **Password (tradizionale):** confrontata con hash sicuro nel file `/etc/shadow`.
2. **Autenticazione a più fattori:** combinazione di elementi (password + token + biometria).
3. **Kerberos:** protocollo basato su ticket temporanei e cifrati (usato in ambienti enterprise).
4. **PAM (Pluggable Authentication Modules):** in Linux, sistema modulare per definire politiche di autenticazione (password, smartcard, LDAP, ecc.).

#### Autorizzazione

Avviene dopo l’autenticazione: il sistema verifica **quali risorse e azioni** sono consentite all’utente, consultando ACL, capability o policy del sistema.

---

### 🔹 6. Protezione in modalità kernel e utente

Le CPU moderne operano in **due modalità di esecuzione**:

- **User mode:** accesso limitato, usata dai processi utente.
- **Kernel mode:** privilegi totali, usata dal sistema operativo.

Ogni **system call** implica un passaggio temporaneo in modalità kernel, seguito da un ritorno alla modalità utente.
Questo meccanismo serve a:

- proteggere la memoria del kernel e le tabelle del sistema;
- evitare che processi utente accedano direttamente all’hardware.

---

### 🔹 7. Sicurezza dei dati e cifratura

Per garantire la riservatezza delle informazioni anche in caso di furto fisico o attacco esterno, vengono adottate **tecniche di cifratura** (encryption).

#### a) Cifratura simmetrica

Stesso segreto (chiave) per cifrare e decifrare.

- Esempi: AES, DES, ChaCha20.
- Veloce, ma richiede un canale sicuro per scambiare la chiave.

#### b) Cifratura asimmetrica

Usa una coppia di chiavi:

- *pubblica** per cifrare, **privata** per decifrare.
- Esempi: RSA, ECC.
- Fondamentale per autenticazione, firme digitali, SSH.

#### c) Hash e integrità

Funzioni unidirezionali che producono una *firma digitale* dei dati:

- SHA-256, SHA-3, BLAKE2.
- Usate per verificare che i file non siano stati alterati.

#### d) Cifratura del file system

- **LUKS (Linux Unified Key Setup)** o **BitLocker (Windows)**:
  cifrano intere partizioni o dischi con chiave derivata dalla password utente.

---

### 🔹 8. Audit e logging

Ogni sistema operativo mantiene **registri di log** che tracciano eventi, accessi e modifiche critiche.
Servono per:

- **analisi forense** in caso di violazioni;
- **monitoraggio di sicurezza**;
- **rilevamento di intrusioni** (IDS, SIEM).

In Linux:

- `/var/log/auth.log` → accessi e login;
- `/var/log/syslog` → eventi di sistema;
- `auditd` → log dettagliato delle system call.

---

### 🔹 9. Backup e ripristino

Nessun sistema è completamente sicuro senza **strategie di backup**.
Il backup garantisce la **disponibilità** dei dati anche dopo guasti o compromissioni.

#### Tipi principali

- **Full backup:** copia completa di tutti i file.
- **Incremental:** salva solo i file modificati dall’ultimo backup.
- **Differential:** salva tutti i file modificati dal backup completo più recente.

#### Buone pratiche

- Backup periodici automatizzati (cron).
- Copie su supporti esterni o cloud cifrati.
- Test regolari dei ripristini.

---

### 🧠 Mappa concettuale di sintesi

      ```text

      SICUREZZA E PROTEZIONE
      │
      ├── Obiettivi
      │   ├─ Integrità
      │   ├─ Riservatezza
      │   └─ Disponibilità
      │
      ├── Domini di protezione
      │   ├─ Ogni processo → risorse + permessi
      │   └─ UID / GID in UNIX
      │
      ├── Matrice di accesso
      │   ├─ ACL → per oggetto
      │   └─ Capability → per soggetto
      │
      ├── Meccanismi
      │   ├─ Permessi UNIX (rwx)
      │   ├─ setuid, setgid, sticky bit
      │   └─ Modalità kernel / utente
      │
      ├── Autenticazione e autorizzazione
      │   ├─ Password, Kerberos, PAM
      │   ├─ ACL e policy
      │   └─ Controllo post-login
      │
      ├── Cifratura e sicurezza dati
      │   ├─ Simmetrica → AES
      │   ├─ Asimmetrica → RSA, ECC
      │   ├─ Hash → SHA, BLAKE2
      │   └─ Full disk encryption (LUKS, BitLocker)
      │
      ├── Audit e logging
      │   ├─ /var/log/, auditd
      │   ├─ IDS / SIEM
      │   └─ Analisi forense
      │
      └── Backup e ripristino
         ├─ Full, Incremental, Differential
         └─ Copie sicure e test periodici

      ```
