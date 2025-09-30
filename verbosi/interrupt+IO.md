
# 📖 Interrupt + I/O

---

## 1. Tipi di Interrupt

Gli **interrupt** sono segnali hardware o software che interrompono il normale flusso di esecuzione del processore per gestire eventi che richiedono attenzione immediata.
Si distinguono in **asincroni** e **sincroni**:

* **Interrupt asincroni**
  Gli interrupt asincroni non sono direttamente collegati all’istruzione che la CPU sta eseguendo in quel momento. Si verificano in maniera indipendente dal codice in corso e possono avvenire in qualsiasi istante.
  Alcuni esempi principali sono:

  * **Interrupt da I/O**: generati dal controllore di un dispositivo (ad esempio disco, tastiera, rete) per segnalare la fine o l’errore di un’operazione.
  * **Interrupt da fallimento hardware**: derivano da eventi imprevisti come la perdita di alimentazione o errori di memoria (ad esempio errori di parità).
  * **Interrupt da comunicazione tra CPU**: nei sistemi multiprocessore una CPU può segnalare un evento ad un’altra.
  * **Interrupt da timer**: generati da un clock interno che invia interruzioni periodiche, utilizzate dal sistema operativo per lo scheduling dei processi e per garantire il time-sharing.

* **Interrupt sincroni (o eccezioni)**
  Gli interrupt sincroni sono una conseguenza diretta dell’esecuzione di una specifica istruzione. Per questo motivo vengono anche detti **eccezioni**.
  Alcuni esempi tipici sono:

  * **overflow aritmetico**,
  * **divisione per zero**,
  * **istruzione illegale o opcode non valido**,
  * **accesso a un indirizzo non valido** o a memoria non disponibile,
  * **page fault**, quando una pagina di memoria virtuale non è presente in RAM,
  * **system call**, che sono eccezioni volontarie generate da un processo per richiedere un servizio al sistema operativo.

---

## 2. Interrupt Handler e Gestione delle Interruzioni

Quando si verifica un interrupt, la CPU sospende temporaneamente l’esecuzione del programma corrente e invoca l’**interrupt handler**, ossia una routine del sistema operativo che gestisce l’evento.

Il funzionamento di base prevede i seguenti passaggi:

1. La CPU salva lo stato corrente (registri, program counter, PSW).
2. Consulta il **vettore di interrupt**, una tabella che associa ciascun tipo di interrupt all’indirizzo della routine corrispondente.
3. Esegue l’handler per gestire l’interruzione.
4. Al termine, ripristina lo stato salvato e riprende l’esecuzione del programma sospeso, oppure passa ad un altro processo se è avvenuto uno scheduling.

### Modalità di gestione degli interrupt multipli

* **Gestione sequenziale**: quando si verifica un interrupt, esso viene gestito interamente prima di passare ad altri. Gli interrupt successivi rimangono in attesa. Questo approccio è semplice da implementare ma riduce la reattività del sistema in caso di più eventi ravvicinati.
* **Gestione annidata**: permette che un interrupt in corso venga interrotto a sua volta da un altro di priorità più alta. In questo modo gli eventi più urgenti vengono gestiti subito, ma richiede un meccanismo più complesso per salvare e ripristinare correttamente i contesti.

---

## 3. Tecniche di I/O

Le operazioni di input/output (I/O) possono essere realizzate con tre tecniche principali, che si differenziano per il grado di coinvolgimento della CPU.

### 3.1 I/O Programmato (Polling)

L’I/O programmato, chiamato anche polling, è la tecnica più semplice e storicamente la prima ad essere utilizzata. In questo approccio la CPU invia un comando al dispositivo di I/O e poi rimane costantemente in attesa, verificando ciclicamente lo stato del dispositivo attraverso la lettura di registri appositi. Il processore controlla di continuo se il dispositivo ha terminato l’operazione, mantenendo quindi un comportamento di attesa attiva (busy waiting). Questo metodo ha il vantaggio della semplicità, ma risulta estremamente inefficiente, perché la CPU non svolge nessun’altra attività durante l’attesa e spreca risorse preziose. Per questo motivo l’I/O programmato è rimasto confinato ai primi calcolatori o a sistemi molto semplici in cui le periferiche sono poche e le esigenze di efficienza sono ridotte.

**In sintesi:**

* È il metodo più semplice e più antico.
* La CPU invia un comando al dispositivo e rimane in attesa controllando continuamente (tramite un ciclo di polling) il registro di stato del dispositivo per sapere quando l’operazione è terminata.
* **Svantaggio principale**: la CPU è totalmente occupata in attesa, senza svolgere altre operazioni (busy waiting).
* Utilizzato solo nei primi computer o in sistemi molto semplici.

### 3.2 I/O Guidato da Interrupt (Interrupt-Driven I/O)

L’I/O guidato da interrupt rappresenta un’evoluzione significativa. In questo caso la CPU, dopo aver inviato un comando al dispositivo, non rimane più ferma in attesa, ma prosegue nell’esecuzione di altre istruzioni. Sarà il dispositivo stesso, quando avrà completato l’operazione, a inviare un interrupt al processore. Al ricevimento dell’interruzione, la CPU sospende temporaneamente l’attività che stava svolgendo, salva lo stato del programma in esecuzione ed esegue la routine di gestione predisposta dal sistema operativo per il trasferimento dei dati. Questo approccio elimina la necessità del busy waiting e rende molto più efficiente l’utilizzo del processore, che può impiegare il tempo in attività utili. Tuttavia, l’I/O guidato da interrupt presenta un limite importante: ogni singolo dato trasferito comporta la generazione di un’interruzione. Nei casi in cui i dati siano numerosi, la frequenza degli interrupt può generare un overhead consistente, rallentando le prestazioni complessive del sistema.

**In sintesi:**

* La CPU invia il comando al dispositivo e continua con altre istruzioni.
* Quando il dispositivo è pronto, invia un interrupt: la CPU sospende il programma in corso, salva il contesto ed esegue l’handler per gestire il trasferimento dei dati.
* **Vantaggi**: elimina l’attesa attiva, la CPU può lavorare su altro mentre il dispositivo elabora.
* **Svantaggi**: ogni singolo trasferimento di dati richiede un interrupt, causando un overhead significativo, specialmente se i dati sono molti.

### 3.3 DMA (Direct Memory Access)

Il passo successivo è stato l’introduzione del DMA (Direct Memory Access). Questa tecnica sfrutta un’unità hardware dedicata, il controller DMA, che ha il compito di gestire direttamente i trasferimenti di dati tra i dispositivi di I/O e la memoria principale. La CPU interviene solo nella fase iniziale, quando prepara l’operazione indicando al controller l’indirizzo di memoria coinvolto, la quantità di dati da trasferire e la direzione del trasferimento (da memoria a dispositivo o viceversa). Una volta avviata l’operazione, il controller DMA prende il controllo e gestisce autonomamente il flusso dei dati, senza bisogno dell’intervento costante del processore. Al termine del trasferimento, il controller genera un unico interrupt per notificare alla CPU che l’operazione è stata completata. Questa modalità riduce drasticamente il carico sul processore, che resta libero di svolgere altre operazioni durante l’I/O. L’uso del DMA risulta particolarmente efficiente nei casi di trasferimento di grandi blocchi di dati, come quelli che avvengono con i dischi, le schede di rete o i dispositivi multimediali. L’unico aspetto critico è legato alla necessità di avere hardware dedicato e alla possibile contesa del bus di sistema: il controller DMA, per poter trasferire i dati, deve infatti utilizzare lo stesso bus della CPU, e questo fenomeno, noto come cycle stealing, può ridurre temporaneamente la disponibilità di risorse per il processore.

**In sintesi:**

* Prevede un **controller DMA** dedicato.
* La CPU inizializza l’operazione indicando indirizzo di memoria, numero di dati e direzione di trasferimento.
* Il DMA gestisce autonomamente il trasferimento dei dati tra dispositivo e memoria principale, senza coinvolgere la CPU.
* Alla fine dell’operazione viene generato un interrupt per notificare il completamento.
* **Vantaggi**: altissima efficienza, CPU quasi completamente libera. Perfetto per trasferimenti di grandi blocchi (es. dischi, schede di rete, audio/video).
* **Svantaggi**: richiede hardware dedicato e introduce la contesa del bus (il DMA “ruba cicli” alla CPU, fenomeno detto cycle stealing).

---

## 4. Tabella degli Interrupt (Vettore di Interrupt)

La **tabella degli interrupt**, o vettore di interrupt, è una struttura dati che associa a ciascun tipo di interrupt l’indirizzo della relativa routine di gestione.
Questa tabella è solitamente posizionata in un’area riservata della memoria e viene consultata automaticamente dal processore quando riceve un segnale di interruzione.
In questo modo, il processore non deve cercare manualmente il codice da eseguire, ma accede subito al gestore appropriato.

---

## 5. Confronto delle Tecniche di I/O

Per chiarire meglio le differenze:

| **Tecnica**     | **Coinvolgimento della CPU**               | **Efficienza** | **Quando usarla**                                      |
| --------------- | ------------------------------------------ | -------------- | ------------------------------------------------------ |
| I/O Programmato | Massimo (busy waiting)                     | Molto bassa ❌  | Sistemi semplici o periferiche veloci                  |
| I/O a Interrupt | Medio (ogni trasferimento causa interrupt) | Discreta ⚠️    | Per dispositivi relativamente lenti (tastiera, mouse)  |
| DMA             | Minimo (CPU solo all’inizio/fine)          | Molto alta ✅   | Per trasferimenti massivi (dischi, rete, multimediale) |

Schema a blocchi (semplificato):

```text
I/O Programmato     → CPU attende continuamente dal dispositivo
I/O a Interruzioni  → CPU lavora, poi viene interrotta a dati pronti
DMA                 → Controller gestisce il trasferimento, CPU libera
```
