# Architettura della CPU (monoprocessore)

## 📚 Architettura Monoprocessore

### 1. Componenti principali

* **CPU (Central Processing Unit)**

  * Contiene **ALU (Arithmetic Logic Unit)** → esegue operazioni aritmetiche e logiche.
  * Contiene **CU (Control Unit)** → controlla e coordina il funzionamento del processore.
  * Contiene i **registri** → memoria interna, velocissima.

* **Memoria principale (RAM)**

  * Contiene dati e istruzioni del programma in esecuzione.
  * È volatile → si cancella allo spegnimento.

* **Dispositivi di I/O (Input/Output)**

  * Permettono comunicazione con l’esterno (tastiera, disco, rete, stampante, …).

* **Bus di sistema**

  * **Bus dati** → trasporta i dati.
  * **Bus indirizzi** → trasporta gli indirizzi di memoria/periferiche.
  * **Bus di controllo** → trasporta segnali di sincronizzazione e comando.

---

## 📌 CPU e Registri

### 1. Registri visibili all’utente

* Accessibili dal programmatore (assembler).
* Tipologie:

  * **Registri dati** → contengono valori da elaborare.
  * **Registri indirizzi** → contengono indirizzi di memoria.

    * **Puntatori diretti** → memorizzano un indirizzo assoluto.
    * **Registri indice** → usati per calcolare indirizzi di array/vettori (`base + indice`).
    * **Puntatori a segmento** → definiscono un segmento di memoria (es. `cs`, `ds`, `ss` nei processori x86).
    * **Stack Pointer (SP)** → punta al top dello stack.

---

### 2. Registri di controllo e stato

* **PC (Program Counter)** → indirizzo della prossima istruzione.
* **IR (Instruction Register)** → istruzione attualmente in esecuzione.
* **PSW (Program Status Word)** → insieme di bit di stato:

  * **Z (zero flag)** → risultato = 0.
  * **N (negative flag)** → risultato negativo.
  * **C (carry flag)** → riporto/borrow nelle operazioni aritmetiche.
  * **V (overflow flag)** → overflow aritmetico.
  * Modalità utente/supervisore.
  * Abilitazione/disabilitazione interrupt.

---

### 3. Registri interni (non visibili all’utente)

* Usati dalla CPU per comunicare con memoria e I/O.
* **MAR (Memory Address Register)** → indirizzo di memoria da leggere/scrivere.
* **MBR (Memory Buffer Register)** → contiene il dato letto o da scrivere in memoria.
* **I/O AR (I/O Address Register)** → contiene l’indirizzo della periferica di I/O.
* **I/O BR (I/O Buffer Register)** → contiene il dato da/per la periferica.

---

## 🔄 Ciclo Fetch/Execute

### Fase FETCH

1. Il **PC** indica l’indirizzo della prossima istruzione.
2. L’indirizzo viene copiato nel **MAR**.
3. La CPU invia la richiesta di lettura memoria tramite il **bus**.
4. L’istruzione viene letta dalla memoria e caricata nel **MBR**.
5. L’istruzione passa nel **IR**.
6. Il **PC** viene aggiornato (incremento sequenziale o salto).

### Fase EXECUTE

* Dipende dall’istruzione:

  * **Operazioni aritmetiche/logiche** → elaborate dalla ALU.
  * **Accesso a memoria** → si usano ancora MAR e MBR.
  * **Accesso a I/O** → si usano registri di I/O.
  * **Istruzioni di controllo** → modificano PC, PSW, modalità di esecuzione.

👉 Dopo EXECUTE si torna a FETCH → ciclo infinito finché non finisce il programma.

---

## ⚙️ Categorie di istruzioni

1. **Scambio dati tra CPU ↔ Memoria**

   * `LOAD` (carica da memoria a registro).
   * `STORE` (salva da registro a memoria).

2. **Scambio dati tra CPU ↔ I/O**

   * `IN` (lettura da periferica a registro).
   * `OUT` (scrittura da registro a periferica).

3. **Manipolazione dati**

   * Aritmetiche → `ADD`, `SUB`, `MUL`, `DIV`.
   * Logiche → `AND`, `OR`, `NOT`, `XOR`.
   * Shift/rotazioni → `SHL`, `SHR`, `ROL`, `ROR`.

4. **Controllo del flusso**

   * Salti condizionati → `BEQ`, `BNE`, `BGT`, `BLT`.
   * Salti incondizionati → `JMP`.
   * Chiamate a procedura → `CALL`, `RET`.

5. **Istruzioni riservate/sistema**

   * Abilitazione/disabilitazione interrupt.
   * Operazioni privilegiate (gestione cache, memoria virtuale, modalità kernel).

---

## 🗺️ Mappa CPU + Registri (testuale dettagliata)

```text
                             +-----------------------------------+
                             |               CPU                 |
                             |-----------------------------------|
                             |   ALU         |   Control Unit    |
                             |-----------------------------------|
                             |   Registri Utente (visibili)      |
                             |   - Registri dati                 |
                             |   - Registri indirizzi            |
                             |       * diretti                   |
                             |       * indice                    |
                             |       * segmento                  |
                             |       * stack pointer (SP)        |
                             |-----------------------------------|
                             |   Registri di Controllo e Stato   |
                             |   - Program Counter (PC)          |
                             |   - Instruction Register (IR)     |
                             |   - PSW (flag, modalità, stato)   |
                             |-----------------------------------|
                             |   Registri Interni (non visibili) |
                             |   - MAR, MBR                      |
                             |   - I/O AR, I/O BR                |
                             +-----------------------------------+
                                        | Bus di Sistema
                 -----------------------------------------------------------
                 |                          |                             |
          +---------------+         +---------------+              +---------------+
          |    MEMORIA    |         |  DISPOSITIVI  |              |   (ALTRI)     |
          | (RAM, Cache)  |         |     I/O       |              | eventuali bus |
          +---------------+         +---------------+              +---------------+
```
