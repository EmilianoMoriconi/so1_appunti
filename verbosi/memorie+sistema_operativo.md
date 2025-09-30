# 📘 Memorie + Sistema Operativo (versione ultra-verbosa)

---

## 🔹 1. Gerarchia delle memorie

Quando pensiamo alla memoria di un computer dobbiamo immaginarla come una **piramide gerarchica**, dove in cima ci sono poche celle rapidissime e costosissime, e alla base ci sono immense quantità di memoria lente ma economiche.
Il progetto di un sistema di memorie nasce da un compromesso: **non possiamo avere tutto insieme (velocità + capacità + basso costo)**, quindi i computer combinano diversi tipi di memoria per sfruttarne i punti di forza.

### 📍 Registri della CPU

* Sono i contenitori **più vicini alla logica di calcolo**, integrati direttamente nei circuiti della CPU.
* Sono pochi (decine), piccolissimi (alcuni byte) ma **ultraveloce**: una lettura o scrittura richiede lo stesso tempo di una singola operazione logica.
* Servono per:

  * conservare **operandi immediati** (es. numeri da sommare);
  * contenere **indirizzi** da cui leggere/scrivere dati;
  * gestire il **flusso di esecuzione** (program counter, registri di stato, stack pointer).
* 📌 **Analogia quotidiana**: i registri sono come il taccuino che tieni in mano mentre fai un calcolo. È piccolissimo ma a portata di mano e immediato da consultare.

---

### 📍 Cache (L1, L2, L3)

* È un livello intermedio che “ammortizza” la differenza enorme di velocità tra CPU e RAM.
* Funziona grazie al **principio di località**:

  * **temporale**: se hai usato un dato poco fa, è probabile che ti serva di nuovo;
  * **spaziale**: se hai preso un dato, probabilmente userai anche i dati vicini.
* La cache è divisa in livelli:

  * **L1** → piccolissima ma integrata direttamente nella CPU, velocità massima;
  * **L2** → più grande ma leggermente più lenta;
  * **L3** → condivisa tra più core, grande ma la meno rapida delle cache.
* Meccanismi chiave:

  * **mappatura**: decide dove inserire i blocchi (direct mapped, associativa, set-associativa);
  * **rimpiazzamento**: sceglie quale blocco eliminare quando la cache è piena (tipico LRU);
  * **politiche di scrittura**:

    * write-through (subito anche in RAM);
    * write-back (solo al bisogno).
* 📌 **Analogia**: la cache è come una scrivania: ci tieni a portata di mano i fogli più usati, senza dover correre ogni volta in archivio (RAM).

---

### 📍 RAM (memoria principale)

* È la **base operativa** del sistema: qui vengono caricati i programmi in esecuzione e i loro dati.
* Capacità grande (GB), volatilità totale (si svuota allo spegnimento).
* Ogni operazione in CPU parte da qui: senza RAM non potresti eseguire neanche il sistema operativo.
* 📌 **Analogia**: è come la tua scrivania grande. Ci appoggi tutto quello che ti serve nel corso della giornata di lavoro, ma alla sera quando vai via (spegnimento) tutto sparisce.

---

### 📍 Memoria secondaria (HDD e SSD)

* È lo **spazio di archiviazione persistente**.
* Capacità enorme (centinaia di GB o TB).
* HDD: dischi magnetici con testine meccaniche → lenti (millisecondi).
* SSD: chip elettronici senza parti mobili → molto più veloci (microsecondi).
* 📌 **Analogia**: è come un grande archivio di faldoni. I documenti stanno lì anche di notte, ma recuperarli è molto più lento rispetto a sfogliare i fogli sulla scrivania (RAM).

---

### 📍 Archiviazione offline

* Supporti rimovibili: CD, DVD, Blu-ray, nastri magnetici.
* Usati non per il lavoro quotidiano, ma per **backup** e **archiviazione storica**.
* 📌 **Analogia**: è come una cassaforte o una biblioteca remota: ottima per conservare dati, pessima per l’accesso rapido.

---

📌 **Schema piramidale riassuntivo**

```text
Registri → velocità altissima, capacità minima
Cache    → velocità molto alta, capacità KB–MB
RAM      → velocità media, capacità GB
SSD/HDD  → velocità bassa, capacità TB
Offline  → velocità molto bassa, capacità enorme
```

---

## 🔹 2. Sistema Operativo: definizione

Il **Sistema Operativo (SO)** è il **direttore d’orchestra** del computer.
Senza di lui, hardware e programmi sarebbero come strumenti scollegati: CPU, memoria, dischi, periferiche non saprebbero coordinarsi.

👉 È un **insieme di programmi** che:

1. gestisce le risorse hardware e software;
2. fornisce servizi a utenti e programmatori;
3. rende il computer **usabile, sicuro ed efficiente**.

### 📍 Funzioni principali del SO

1. **Gestione processi**: decide quali programmi possono usare la CPU, li sospende e li riattiva, li termina.
2. **Gestione memoria**: assegna porzioni di RAM, gestisce la memoria virtuale, protegge ogni processo dagli altri.
3. **Gestione I/O**: controlla tastiera, schermo, stampanti, dischi tramite driver.
4. **Gestione file system**: organizza i dati in file e cartelle, con permessi e protezioni.
5. **Sicurezza**: controlla chi accede a cosa, autentica utenti, difende i dati.
6. **Interfaccia utente**: permette interazione (comandi testuali o interfaccia grafica).

📌 **Analogia**: se il computer fosse un’azienda, l’hardware sarebbero i lavoratori e le macchine, i programmi sarebbero i progetti da realizzare, e il SO sarebbe il direttore che assegna compiti, tiene i registri e controlla la sicurezza.

---

## 🔹 3. Kernel vs Microkernel

Il **kernel** è il cuore del SO, sempre caricato in RAM: tutto passa da lui.

### 📍 Kernel monolitico

* Tutte le funzioni del SO (gestione file, driver, memoria) sono integrate in un unico grande blocco.
* ✅ Veloce ed efficiente (tutto è interno).
* ❌ Fragile: un errore in un driver può mandare in crash l’intero sistema.

---

### 📍 Microkernel

* Tiene in memoria solo le **funzioni minime** (scheduler, comunicazioni tra processi).
* Tutto il resto (driver, file system, protocolli) è gestito come **moduli separati** caricati solo quando servono.
* ✅ Più sicuro e modulare.
* ❌ Più lento per via del traffico di messaggi tra moduli.

📌 **Esempio**: Linux usa un kernel monolitico (con moduli caricabili), mentre sistemi come Minix e QNX usano microkernel.

---

## 🔹 4. Struttura a 13 livelli del SO

Immagina il sistema operativo come un **grattacielo di 13 piani**.
Ogni piano è costruito sopra quello inferiore e offre servizi a quello superiore.

1. **Circuiti elettrici**: porte logiche, registri, celle di memoria.
2. **Istruzioni macchina**: le primitive come somma, sottrazione, load/store.
3. **Procedure**: sottoprogrammi riutilizzabili con chiamata e ritorno.
4. **Gestione interruzioni**: meccanismo che interrompe il flusso normale per gestire eventi.
5. **Processi**: astrazione di un programma in esecuzione, con stati (ready, running, blocked).
6. **Memoria secondaria**: trasferimento di blocchi tra RAM e disco.
7. **Indirizzamento logico**: ogni processo ha il suo spazio virtuale di indirizzi.
8. **Comunicazioni tra processi (IPC)**: segnali, pipe, memoria condivisa.
9. **File system**: nomi simbolici, file persistenti.
10. **Accesso dispositivi**: driver e API standardizzate.
11. **Associazione identificatori**: legare nomi logici a risorse fisiche.
12. **Supporto di alto livello**: librerie e astrazioni per i programmatori.
13. **Interfaccia utente**: CLI, GUI, shell.

📌 **Analogia**: come in un’azienda, ogni reparto (livello) fa un lavoro specializzato e si appoggia a quello sotto. L’utente interagisce solo con il livello più alto, senza preoccuparsi dei dettagli.

---

## 🔹 5. Mappe da costruire

1. **Gerarchia delle memorie**

   * Disegna una piramide: in cima i registri (pochi e veloci), in basso le memorie offline (enormi ma lente).

2. **Struttura a 13 livelli del SO**

   * Rappresentala come una pila di blocchi.
     Ogni blocco: nome del livello + funzione chiave.
