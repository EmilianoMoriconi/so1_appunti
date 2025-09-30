# 📘 Storia dei Sistemi Operativi

## 🔹 1. Sistemi Batch

* **Definizione**:
  I sistemi batch sono stati i primi veri sistemi operativi multiutente.
  L’utente non interagiva direttamente con il computer durante l’esecuzione. I programmi venivano **inseriti in gruppi (batch)**, raccolti su schede perforate o nastri, e processati uno dopo l’altro senza interruzione.

* **Caratteristiche principali**:

  * **Esecuzione sequenziale**: ogni job viene eseguito **tutto in una volta**, senza preemption.
  * **Job Control Language (JCL)**: linguaggio usato per dire al SO quali programmi eseguire e con quali file/dispositivi.
  * **Obiettivo**: massimizzare l’uso del processore (alta **utilizzazione CPU**).
  * **Interazione utente**: nulla → l’utente sottomette il job e attende il risultato dopo molto tempo (stampato o salvato).
  * **Limite**: tempi di attesa molto lunghi, nessuna flessibilità, non adatto ad applicazioni interattive.

* **Schema logico**:
  Job → JCL → inserimento nel batch → esecuzione sequenziale completa → output finale.

---

## 🔹 2. Time Sharing

* **Definizione**:
  Evoluzione dei batch, introdotto dagli anni ’60.
  Sistema multiutente che consente a più utenti di usare il computer **contemporaneamente**, con la CPU che “condivide il tempo” fra vari processi.

* **Caratteristiche principali**:

  * **Esecuzione parziale temporizzata**: la CPU viene suddivisa in **slice di tempo** assegnati ai vari processi.
  * **Multiprogrammazione**: i job non vengono eseguiti tutti interi, ma a turni → concorrenza simulata.
  * **Input da terminale**: comandi inseriti direttamente dall’utente, con interazione immediata.
  * **Obiettivo**: minimizzare il **tempo di risposta** percepito dall’utente.
  * **Limiti**: overhead di gestione più alto, richiede meccanismi hardware/software complessi.

* **Esempi di applicazione**: calcolatori universitari, sistemi multiutente in rete (antesignani dei moderni sistemi interattivi).

---

## 🔹 3. Risultati Hardware / OS

Per rendere possibili i sistemi multiprogrammati e il time sharing, sono stati introdotti **meccanismi hardware fondamentali**:

* **Protezione della memoria**:

  * Impedisce a un job di accedere o modificare aree del sistema operativo o di altri processi.
  * Nascono le basi della **memoria virtuale**.

* **Timer**:

  * Previene che un processo monopolizzi la CPU.
  * Ogni processo riceve un **quantum**; allo scadere, viene interrotto.

* **Istruzioni privilegiate**:

  * Alcune istruzioni possono essere eseguite solo dal sistema operativo (in modalità **kernel mode**).
  * Esempi: gestione interruzioni, I/O diretto, gestione memoria.
  * Distinzione tra **user mode** (programma utente, sicuro) e **kernel mode** (OS, privilegiato).

* **Interrupt**:

  * Non presenti nei primi sistemi.
  * Introdotti per rispondere a eventi esterni (I/O, errori, eccezioni).

---

## 🔹 4. Timeline (semplificata)

* **Anni ’40**: calcolatori primitivi, senza SO.
* **Anni ’50**: sistemi **batch** (schede perforate, job sequenziali).
* **Anni ’60**: nascita del **time sharing** → interattività, multiprogrammazione.
* **Anni ’70**: concetto di **processo** (batch + interattivi + real-time).
* **Anni ’80-’90**: diffusione di sistemi multiutente complessi, reti, UNIX.
* **Oggi**: sistemi multitasking, distribuiti, real-time, cloud.

---

## 🔹 5. Tabella di confronto Batch vs Time Sharing

| **Caratteristica**   | **Batch**                                              | **Time Sharing**                                                |
| -------------------- | ------------------------------------------------------ | --------------------------------------------------------------- |
| **Scopo principale** | Massimizzare l’uso della CPU                           | Minimizzare il tempo di risposta                                |
| **Input**            | Job Control Language, inviato con il job stesso        | Comandi da terminale, interazione diretta                       |
| **Esecuzione**       | Job eseguito interamente, sequenziale                  | Job eseguito parzialmente, a turni (quantum di tempo)           |
| **Utenti**           | Multiutente, ma senza interazione                      | Multiutente con interazione simultanea                          |
| **Output**           | Stampato o salvato, dopo attese lunghe                 | Fornito quasi subito, in modalità interattiva                   |
| **Vantaggi**         | Massima efficienza della CPU, semplice da implementare | Maggiore flessibilità, interazione rapida, utilizzo condiviso   |
| **Svantaggi**        | Nessuna interattività, lunghi tempi di attesa          | Maggior complessità di gestione, overhead del sistema operativo |
