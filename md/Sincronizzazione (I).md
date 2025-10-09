# Sincronizzazione (I)

---

## 🔹 Introduzione

In un sistema multiprogrammato o multithread, più processi o thread possono essere **attivi contemporaneamente** e condividere **risorse comuni**, come variabili, file o dispositivi.
Quando due o più attività tentano di accedere contemporaneamente a una risorsa condivisa, possono verificarsi **condizioni di competizione (race conditions)**, che portano a risultati **imprevedibili e non deterministici**.

Per evitare questi problemi, il sistema operativo (e il programmatore) devono garantire una **sincronizzazione corretta** tra i processi concorrenti, assicurando che **le operazioni critiche siano eseguite in modo mutualmente esclusivo**.

---

## 🔹 1. Sezione critica

La **sezione critica** è la parte di codice di un processo che **accede a risorse condivise** (variabili, buffer, dispositivi).
Durante l’esecuzione della sezione critica, **nessun altro processo** deve poter accedere alle stesse risorse.

### Struttura generale di un processo

```plaintext
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

## 🔹 2. Condizioni di competizione (Race Conditions)

Una **race condition** si verifica quando l’esito finale di un programma **dipende dall’ordine di esecuzione** dei processi concorrenti.
Questo accade perché più processi **leggono e scrivono simultaneamente** su una risorsa condivisa senza sincronizzazione.

### Esempio classico

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

## 🔹 3. Soluzioni software alla mutua esclusione

Prima dell’introduzione di meccanismi hardware e primitivi del kernel, sono state sviluppate **soluzioni puramente software** per garantire l’accesso esclusivo alla sezione critica.
Queste soluzioni operano tramite variabili condivise e cicli di controllo (busy waiting).

### a) Disabilitazione degli interrupt (solo kernel)

Nel kernel, la CPU può **disabilitare gli interrupt** durante l’esecuzione di codice critico:

```c
disable_interrupts();
critical_section();
enable_interrupts();
```

→ impedisce che venga eseguito un context switch.

**Vantaggi:**

* Soluzione semplice ed efficace per il codice del kernel.

**Svantaggi:**

* Non applicabile ai processi utente.
* Rende il sistema meno reattivo (gli interrupt vengono ritardati).
* Pericolosa su architetture multicore (non blocca gli altri core).

---

### b) Soluzione di Peterson

La **soluzione di Peterson** è un algoritmo software classico per due processi, basato su due variabili condivise:

* `flag[i]`: indica se il processo *i* vuole entrare nella sezione critica.
* `turn`: indica a chi tocca entrare.

```c
flag[i] = true;
turn = j;
while (flag[j] && turn == j);
critical_section();
flag[i] = false;
```

**Funzionamento:**

* Ogni processo segnala la propria intenzione (`flag[i] = true`) e cede momentaneamente la priorità all’altro (`turn = j`).
* Solo quando l’altro non è interessato o non ha il turno, può entrare nella sezione critica.

**Proprietà:**
✔ Mutua esclusione
✔ Progresso
✔ Attesa limitata

**Limiti:** valida solo per due processi; inefficiente su sistemi multiprocessore.

---

### c) Algoritmo del panettiere (Bakery Algorithm)

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

**Proprietà:**

* Garantisce mutua esclusione e ordine FIFO.
* Completamente software.

**Svantaggi:**

* Elevato overhead per confronti multipli.
* Poco pratico nei sistemi reali.

---

## 🔹 4. Soluzioni hardware

Per migliorare l’efficienza, i moderni processori offrono **istruzioni atomiche** che garantiscono mutua esclusione senza busy waiting esplicito.

### a) Test-and-Set

Istruzione atomica che **legge e modifica** contemporaneamente una variabile di lock.

```c
boolean TestAndSet(boolean *target) {
    boolean old = *target;
    *target = true;
    return old;
}
```

**Esempio d’uso:**

```c
while (TestAndSet(&lock)); // attende finché lock non è false
critical_section();
lock = false;
```

→ nessuna interruzione può interferire durante l’istruzione atomica.

**Problema:**
causa *busy waiting* (la CPU consuma cicli in attesa).

---

### b) Swap (Exchange)

Scambia in modo atomico il contenuto di due variabili:

```c
Swap(a, b):
    temp = a;
    a = b;
    b = temp;
```

Può essere usato per implementare meccanismi simili a Test-and-Set.

---

### c) Compare-and-Swap (CAS)

Istruzione più evoluta: confronta il valore di una variabile e, se corrisponde a quello atteso, lo sostituisce con un nuovo valore.
È la base dei **lock-free algorithms** nei sistemi multiprocessore.

```c
boolean CAS(int *ptr, int expected, int new) {
    if (*ptr == expected) {
        *ptr = new;
        return true;
    } else return false;
}
```

---

## 🔹 5. Semafori

Proposti da Dijkstra, i **semafori** rappresentano una **soluzione generale e astratta** per gestire la sincronizzazione tra processi, evitando l’uso diretto di busy waiting.

Un semaforo è una **variabile intera S** che può assumere valori ≥ 0, e viene manipolata tramite due operazioni atomiche:

```plaintext
wait(S):   // P (proberen, "provare")
    while (S <= 0)
        ; // attende
    S = S - 1

signal(S): // V (verhogen, "incrementare")
    S = S + 1
```

### Tipologie di semafori

* **Semaforo binario (mutex):** può valere solo 0 o 1 → usato per mutua esclusione.
* **Semaforo contatore:** rappresenta un numero di risorse disponibili (es. posti in un buffer).

### Vantaggi

* Semplice da implementare a livello di kernel.
* Evita race conditions e garantisce mutua esclusione.

### Svantaggi

* Se implementato con busy waiting → spreco CPU.
  (In sistemi reali, il processo viene messo in coda e sospeso.)

---

## 🔹 6. Problema Produttore–Consumatore

Il **problema del produttore–consumatore** (o **bounded buffer problem**) è un classico esempio di uso dei semafori.

### Descrizione

* Un **produttore** genera dati e li inserisce in un buffer.
* Un **consumatore** preleva dati dallo stesso buffer.
* Il buffer ha **capacità limitata** → serve sincronizzazione per evitare:

  * produzione oltre la capacità (overflow),
  * consumo di buffer vuoto (underflow).

### Soluzione con semafori

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

## 🧠 Mappa concettuale di sintesi

```plaintext
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
