# 📘 Memorie + Sistema Operativo

---

## 🔹 1. Gerarchia delle memorie

La gerarchia delle memorie è organizzata in più livelli, ciascuno con caratteristiche diverse in termini di **velocità, capacità e costo**.
L’idea alla base è quella di avvicinare alla CPU memorie sempre più veloci e piccole, mentre quelle grandi e lente vengono lasciate nei livelli più bassi. In questo modo il sistema ottiene un compromesso: la CPU lavora con dati veloci nei registri e nella cache, mentre RAM e memoria di massa garantiscono la capacità necessaria a contenere programmi e archivi.

1. **Registri CPU**: memoria interna al processore, dimensioni ridottissime (pochi byte), ma accesso immediato (un ciclo di clock). Sono indispensabili per tutte le operazioni aritmetico-logiche e per la gestione degli indirizzi.
2. **Cache (L1, L2, L3)**: memorie intermedie ad alta velocità che riducono il tempo di accesso alla RAM. Basano il loro funzionamento sul principio di località (temporale e spaziale). Utilizzano tecniche di mappatura, algoritmi di rimpiazzamento (es. LRU) e politiche di scrittura (write-through, write-back).
3. **RAM**: memoria principale, volatile, con capacità dell’ordine dei GB. Ospita i programmi in esecuzione e i dati necessari. È più lenta della cache, ma molto più veloce della memoria di massa.
4. **Memoria secondaria (HDD/SSD)**: non volatile, capacità molto elevata (centinaia di GB o TB). SSD molto più rapidi degli HDD. Qui sono salvati file e programmi in maniera persistente.
5. **Archiviazione offline**: supporti rimovibili come CD/DVD, Blu-ray, nastri magnetici. Non adatti all’uso operativo quotidiano, ma utili per backup e archiviazione a lungo termine.

---

## 🔹 2. Sistema Operativo: definizione

Il Sistema Operativo (SO) è un **insieme di programmi di controllo** che funge da intermediario tra l’hardware e l’utente. La sua funzione principale è la **gestione efficiente e sicura delle risorse del sistema**, offrendo un insieme di servizi standardizzati sia agli utenti finali che ai programmatori.

### Funzioni principali

* **Gestione processi**: creazione, schedulazione, sospensione e terminazione dei processi. Garantisce la concorrenza e l’uso ottimale della CPU.
* **Gestione memoria**: allocazione e deallocazione della RAM, protezione tra processi, uso della memoria virtuale.
* **Gestione I/O**: interfacciamento con periferiche tramite driver, gestione del buffering e della sincronizzazione.
* **Gestione file system**: organizzazione dei dati in file e directory, gestione dei permessi e protezione.
* **Sicurezza**: meccanismi di autenticazione, autorizzazione e protezione delle risorse.
* **Interfaccia utente**: ambienti CLI e GUI che permettono l’interazione con il sistema.

---

## 🔹 3. Kernel vs Microkernel

### Kernel

Il **kernel** è la parte centrale e permanente del SO, sempre residente in RAM. È responsabile delle operazioni più critiche: gestione della CPU, dei processi, della memoria e delle interruzioni.

### Kernel monolitico

* Tutte le funzioni del SO sono contenute in un unico blocco.
* **Pro**: massima efficienza, velocità.
* **Contro**: scarsa modularità, un singolo errore può compromettere l’intero sistema.

### Microkernel

* Mantiene solo le funzioni essenziali in memoria (scheduler, IPC, memoria di base).
* Tutti gli altri servizi (file system, driver, protocolli) sono implementati come moduli esterni.
* **Pro**: maggiore modularità, sicurezza, portabilità.
* **Contro**: overhead maggiore dovuto alla comunicazione tra moduli.

---

## 🔹 4. Struttura a 13 livelli del SO

Il SO può essere visto come una pila stratificata. Ogni livello si appoggia a quello sottostante e fornisce servizi a quello superiore.

1. Circuiti elettrici → registri, celle di memoria, porte logiche.
2. Istruzioni macchina → operazioni elementari (add, sub, load, store).
3. Procedure → sottoprogrammi riutilizzabili con chiamata e ritorno.
4. Gestione interruzioni → gestione eventi sincroni e asincroni.
5. Processi → astrazione del programma in esecuzione con stati definiti.
6. Memoria secondaria → trasferimento dati tra RAM e disco.
7. Indirizzamento logico → creazione di spazi virtuali per ogni processo.
8. Comunicazioni tra processi (IPC) → pipe, segnali, memoria condivisa.
9. File system → gestione dei file e nomi simbolici.
10. Accesso dispositivi esterni → driver e API per periferiche.
11. Associazione identificatori → collegamento nomi logici ↔ oggetti fisici.
12. Supporto di alto livello → librerie e astrazioni per sviluppatori.
13. Interfaccia utente → shell, CLI, GUI.

---

## 🔹 5. Mappe da costruire

1. **Gerarchia memorie**: piramide dall’alto (registri) al basso (memoria offline), con indicazioni di capacità e velocità.
2. **Struttura a 13 livelli**: pila di blocchi con nome e funzione di ciascun livello.

---

Vuoi che questa versione te la preparo anche in **stile appunti schematici** (tipo elenco con bullet point e sottopunti, molto fitto di dettagli ma rapido da leggere)?
