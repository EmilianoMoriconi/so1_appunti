# Sincronizzazione (II)

---

## 🔹 Introduzione

La sincronizzazione non si limita a garantire la mutua esclusione: in molti casi, più processi devono **cooperare e coordinare le proprie azioni** in modo ordinato.
Inoltre, l’uso scorretto dei meccanismi di sincronizzazione può portare a **situazioni di blocco permanente (deadlock)**, in cui un gruppo di processi resta sospeso in attesa reciproca di risorse.

Questa lezione approfondisce:

* i **monitor** come astrazione ad alto livello per la sincronizzazione strutturata;
* la **natura del deadlock**;
* i **metodi per prevenirlo, evitarlo o rilevarlo**;
* e infine l’**algoritmo del banchiere** di Dijkstra, che ne rappresenta un modello di evitamento dinamico.

---

## 🔹 1. Monitor

Un **monitor** è un **costrutto di sincronizzazione ad alto livello**, introdotto da Hoare e Brinch Hansen, che incapsula:

* le **variabili condivise**,
* le **procedure che operano su di esse**, e
* i **meccanismi di sincronizzazione** (implicitamente gestiti dal linguaggio o dal sistema).

### Concetto

Solo **un processo alla volta** può trovarsi all’interno del monitor → garantisce **mutua esclusione automatica**.

```plaintext
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

### Variabili di condizione

Le **variabili di condizione** permettono di sospendere e risvegliare i processi all’interno del monitor:

* `wait(c)`: sospende il processo su `c` finché un altro non lo risveglia.
* `signal(c)`: risveglia un processo sospeso su `c` (se presente).

### Vantaggi

* Sintassi chiara e strutturata: facile da integrare nei linguaggi ad alto livello (es. Java, C#, Ada).
* Elimina l’uso esplicito dei semafori.
* Evita errori di sincronizzazione dovuti a dimenticanze o inversioni di ordine (`wait`/`signal`).

### Svantaggi

* Minor controllo sul comportamento fine del sistema.
* La semantica di `signal` varia:

  * **Hoare semantics:** il processo risvegliato entra subito nel monitor.
  * **Mesa semantics (usata in Java):** il processo risvegliato è solo pronto, ma non entra subito (può esserci starvation).

---

## 🔹 2. Deadlock

Un **deadlock** si verifica quando un insieme di processi si trova in uno stato in cui **ognuno attende una risorsa posseduta da un altro processo del gruppo**, e **nessuno può progredire**.

### Esempio classico

Due processi P1 e P2, due risorse R1 e R2:

```text
P1: lock(R1); lock(R2);
P2: lock(R2); lock(R1);
```

→ Possibile situazione:

* P1 ottiene R1 e attende R2.
* P2 ottiene R2 e attende R1.
  → Nessuno può procedere ⇒ **deadlock**.

---

## 🔹 3. Condizioni necessarie per il deadlock

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

## 🔹 4. Rappresentazione con il grafo delle risorse

Un **Resource Allocation Graph (RAG)** rappresenta graficamente le relazioni tra processi e risorse:

* **Nodo processo** → ( P_i )
* **Nodo risorsa** → ( R_j )
* **Arco di richiesta:** ( P_i → R_j )
* **Arco di assegnazione:** ( R_j → P_i )

### Esempio

```text
R1 → P1 → R2 → P2 → R1
```

→ ciclo → **deadlock potenziale**

**Osservazioni:**

* Se non ci sono cicli → nessun deadlock.
* Se c’è un ciclo → possibile deadlock (certo, se ogni risorsa ha un solo istanza).

---

## 🔹 5. Strategie per la gestione del deadlock

### a) Prevenzione

Evita a priori che si verifichi un deadlock, **impedendo una o più delle quattro condizioni**.

| Condizione       | Metodo di prevenzione                            |
| ---------------- | ------------------------------------------------ |
| Mutua esclusione | Usare risorse condivisibili dove possibile       |
| Hold and wait    | Richiedere tutte le risorse all’inizio           |
| No preemption    | Rimuovere risorse a processi bloccati            |
| Circular wait    | Imporre un ordine totale di acquisizione risorse |

**Esempio:**
numerare tutte le risorse e richiederle sempre in ordine crescente.

**Svantaggi:**

* Poca flessibilità.
* Spreco di risorse (processi che richiedono più del necessario).

---

### b) Evitamento (Dynamic avoidance)

L’allocazione viene concessa solo se **mantiene il sistema in uno stato sicuro**.

Uno **stato sicuro** è tale che esiste un ordine di esecuzione dei processi che consente a ciascuno di terminare senza deadlock.

→ L’algoritmo principale di questa categoria è **l’Algoritmo del Banchiere**.

---

### c) Rilevazione e recupero

Si **permette che il deadlock avvenga**, ma il sistema:

1. lo **rileva** (analizzando periodicamente il grafo delle risorse);
2. esegue un’azione di **recupero** (termina o sospende alcuni processi).

**Metodi di recupero:**

* **Prelazione risorse:** forzare il rilascio da parte di un processo.
* **Rollback:** riportare un processo a uno stato precedente.
* **Terminazione selettiva:** uccidere uno o più processi coinvolti nel ciclo.

---

## 🔹 6. Algoritmo del Banchiere (Banker’s Algorithm)

Proposto da Dijkstra, l’**algoritmo del banchiere** è un metodo di **evitamento del deadlock** in cui il sistema decide se concedere una richiesta di risorsa **in base alla sicurezza dello stato risultante**.

### Concetto

Un “banchiere” (il sistema) concede un prestito (una risorsa) solo se, anche dopo la concessione, **può garantire che tutti i clienti (processi)** saranno in grado di completare le loro operazioni in qualche ordine.

### Parametri principali

| Simbolo                            | Significato                              |
| ---------------------------------- | ---------------------------------------- |
| `Available`                        | Risorse attualmente libere               |
| `Max[i]`                           | Risorse massime richieste dal processo i |
| `Allocation[i]`                    | Risorse già assegnate al processo i      |
| `Need[i] = Max[i] - Allocation[i]` | Risorse ancora necessarie                |

### Procedura

1. Quando un processo `P_i` richiede una risorsa, il sistema controlla se:

   ```text
   Request[i] <= Need[i]
   Request[i] <= Available
   ```

   Se sì, si **simula l’assegnazione**.

2. Si verifica se il nuovo stato è **sicuro**:

   * esiste un ordine in cui tutti i processi possono completare.

3. Se lo stato è sicuro → la risorsa viene concessa;
   altrimenti → il processo viene sospeso.

### Esempio (semplificato)

```text
Available = [3, 3, 2]
P1 Need = [7, 4, 3]
P2 Need = [1, 2, 2]
P3 Need = [6, 0, 0]
```

→ Il sistema valuta se concedere una richiesta senza uscire dallo stato sicuro.
Se la concessione rompe la condizione, la richiesta viene **posticipata**.

### Limiti

* Richiede conoscenza preventiva di `Max[i]`.
* Costoso per grandi sistemi.
* Efficace solo per risorse riutilizzabili (CPU, I/O, memoria).

---

## 🔹 7. Riepilogo comparativo

| Strategia                | Quando agisce | Meccanismo               | Vantaggi              | Svantaggi                |
| ------------------------ | ------------- | ------------------------ | --------------------- | ------------------------ |
| **Prevenzione**          | Prima         | Evita condizioni di base | Semplice, sicura      | Inefficiente             |
| **Evitamento (Banker)**  | Durante       | Stato sicuro             | Flessibile            | Costoso, richiede Max[i] |
| **Rilevazione/Recupero** | Dopo          | Analisi grafi            | Adatto a batch system | Possibile perdita dati   |

---

## 🧠 Mappa concettuale di sintesi

```plaintext
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
