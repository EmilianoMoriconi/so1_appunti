# 📖 Interrupt + I/O

## 🔹 Tipi di interrupt

Gli **interrupt** sono segnali hardware o software che interrompono il normale flusso sequenziale della CPU per segnalare un evento da gestire.

### 1. **Asincroni**

* Non dipendono direttamente dall’istruzione corrente.
* Possono arrivare in qualunque momento.
* **Classi principali**:

  * **Da I/O**: generati da dispositivi (es. disco, tastiera) quando completano un’operazione → segnalano successo o errore.
  * **Da fallimento hardware**: guasto improvviso, power failure, errori di memoria (bit di parità).
  * **Da comunicazione tra CPU**: in sistemi multiprocessore.
  * **Da timer**: il clock interno del processore genera interrupt periodici per garantire il time-sharing e la pianificazione dei processi.

➡️ Nei processori Intel, gli interrupt asincroni coincidono con queste categorie.

### 2. **Sincroni (eccezioni)**

* Conseguenza immediata di un’istruzione.
* Non si verificano "a caso", ma perché una certa istruzione incontra una condizione speciale.
* **Esempi**:

  * divisione per zero,
  * overflow aritmetico,
  * istruzione illegale (opcode non valido),
  * accesso a indirizzo non valido,
  * page fault (memoria virtuale),
  * breakpoint / debug,
  * **system call** (chiamata volontaria al SO).

➡️ Nei processori Intel queste sono dette **exceptions**.

---

## 🔹 Interrupt handler

L’**interrupt handler** è la routine del Sistema Operativo che gestisce l’interruzione.

### Funzionamento

1. La CPU sospende il programma corrente.
2. Salva il contesto (registri, PC, PSW).
3. Legge dal **vettore di interrupt** l’indirizzo della routine corrispondente.
4. Esegue la routine di gestione (handler).
5. Ripristina il contesto.
6. Riprende il programma sospeso (o un altro, se c’è stato process switch).

### Modalità di gestione

* **Sequenziale**:

  * Un handler deve terminare prima che un altro possa iniziare.
  * Semplice da implementare, ma meno reattivo se arrivano molte interruzioni.
* **Annidata**:

  * Durante l’esecuzione di un handler, un’interruzione più urgente può interrompere quella in corso.
  * Richiede priorità e una gestione complessa del salvataggio del contesto.
  * Usata nei sistemi moderni per garantire alta reattività.

---

## 🔹 Tecniche di I/O

Il colloquio tra CPU e dispositivi può avvenire in tre modi principali:

### 1. **I/O Programmato (polling)**

* La CPU invia un comando al dispositivo e **controlla ciclicamente** lo stato (busy waiting).
* Vantaggi:

  * Semplice da implementare.
* Svantaggi:

  * CPU sprecata in attesa, inefficiente.
* Usato solo nei sistemi molto semplici o nei primissimi computer.

---

### 2. **I/O Interrupt-Driven**

* La CPU invia il comando al dispositivo e continua altre operazioni.
* Quando il dispositivo è pronto, **genera un interrupt**.
* Passaggi:

  1. CPU manda comando al modulo I/O.
  2. CPU prosegue altre istruzioni.
  3. Dispositivo genera interrupt quando pronto.
  4. Handler salva contesto, trasferisce dati, poi ritorna.
* Vantaggi:

  * Evita attesa attiva → CPU libera nel frattempo.
* Svantaggi:

  * Overhead: ogni singolo dato trasferito causa un interrupt.
  * Inefficiente per grandi quantità di dati.

---

### 3. **DMA (Direct Memory Access)**

* Introduce un **controller DMA** che gestisce i trasferimenti.
* CPU inizializza l’operazione (indirizzo, numero di byte, direzione trasferimento).
* DMA gestisce il flusso tra memoria e dispositivo, senza passare per la CPU.
* Al termine → invia un interrupt di completamento.
* Vantaggi:

  * Massima efficienza, ideale per grandi blocchi di dati.
  * CPU quasi totalmente libera.
* Svantaggi:

  * Richiede hardware dedicato (controller DMA).
  * Contende il bus con la CPU (cycle stealing).

---

## 🔹 Tabella interrupt (vettore di interrupt)

* Struttura dati che contiene, per ogni tipo di interrupt, l’indirizzo della relativa routine di gestione.
* Tipicamente in memoria a indirizzi riservati.
* La CPU la consulta automaticamente al verificarsi di un’interruzione.
* Garantisce che ogni evento sia gestito dalla routine giusta senza dover fare controlli complicati a runtime.

---

## 🔹 Schema comparativo delle tecniche di I/O

| **Tecnica**          | **Coinvolgimento CPU**                     | **Efficienza** | **Quando usarla**                                     |
| -------------------- | ------------------------------------------ | -------------- | ----------------------------------------------------- |
| **Programmato**      | Totale (busy wait)                         | ❌ Molto bassa  | Sistemi semplici o dispositivi veloci                 |
| **Interrupt-Driven** | Medio (ogni trasferimento causa interrupt) | ⚠️ Media       | Per periferiche lente (tastiera, mouse)               |
| **DMA**              | Minimo (solo all’inizio/fine)              | ✅ Alta         | Per trasferimenti massivi (dischi, rete, audio/video) |

Schema a blocchi (testuale):

```text
[CPU] --- polling ---> [Dispositivo]          (I/O programmato)
[CPU] --cmd--> [I/O] --INT--> [CPU handler]   (I/O interrupt-driven)
[CPU] --inizializza--> [DMA] <--> [Memoria]   (DMA)
                           |
                     [Dispositivo]
```
