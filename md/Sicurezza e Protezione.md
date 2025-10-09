# Sicurezza e Protezione

---

## 🔹 Introduzione

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

## 🔹 1. Obiettivi della protezione

Il sistema operativo deve garantire:

1. **Integrità:** le risorse possono essere modificate solo da soggetti autorizzati.
2. **Riservatezza:** le informazioni sono accessibili solo a chi ne ha diritto.
3. **Disponibilità:** le risorse devono rimanere accessibili agli utenti legittimi.

Per ottenere questi obiettivi, il sistema definisce un **modello di accesso controllato** tra *soggetti* (processi, utenti) e *oggetti* (file, dispositivi, aree di memoria).

---

## 🔹 2. Domini di protezione

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

### Implementazione pratica

* In UNIX/Linux ogni processo ha **UID (User ID)** e **GID (Group ID)**.
* Il kernel verifica i permessi ogni volta che viene effettuata un’operazione su un file o una risorsa.

---

## 🔹 3. Matrice di accesso

Il modello generale di protezione può essere rappresentato da una **matrice di accesso**, dove:

* **righe** = soggetti (utenti, processi);
* **colonne** = oggetti (file, dispositivi, memoria);
* **celle** = diritti di accesso concessi (read, write, execute).

### Esempio

|             | file1   | file2 | stampante |
| ----------- | ------- | ----- | --------- |
| **utente1** | r, w    | r     | w         |
| **utente2** | r       | –     | –         |
| **root**    | r, w, x | r, w  | w         |

### Rappresentazioni compatte

Poiché la matrice completa è molto grande e sparsa (molti campi vuoti), nella pratica si usano due approcci:

#### a) Liste di controllo d’accesso (ACL – Access Control List)

Per ogni **oggetto** si mantiene l’elenco dei soggetti che possono accedervi e con quali permessi.

Esempio:

```text
file1 → [(utente1, rw), (utente2, r), (root, rwx)]
```

→ tipico modello UNIX (`rwxr-xr--`).

#### b) Capability List

Per ogni **soggetto** si mantiene l’elenco degli oggetti a cui può accedere e con quali diritti.

Esempio:

```text
utente1 → [(file1, rw), (stampante, w)]
```

→ tipico dei sistemi distribuiti o microkernel (es. Mach, seL4).

---

## 🔹 4. Meccanismi di controllo accessi

### a) File system e permessi UNIX

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

### b) Bit speciali

* **setuid (s):** esegue il programma con i permessi del proprietario, non dell’utente corrente (es. `passwd`).
* **setgid (s):** eredita il gruppo del file.
* **sticky bit (t):** nei file condivisi (es. `/tmp`) impedisce la cancellazione da parte di utenti non proprietari.

---

## 🔹 5. Autenticazione e autorizzazione

### Autenticazione

È il processo di **verifica dell’identità** dell’utente.

Metodi principali:

1. **Password (tradizionale):** confrontata con hash sicuro nel file `/etc/shadow`.
2. **Autenticazione a più fattori:** combinazione di elementi (password + token + biometria).
3. **Kerberos:** protocollo basato su ticket temporanei e cifrati (usato in ambienti enterprise).
4. **PAM (Pluggable Authentication Modules):** in Linux, sistema modulare per definire politiche di autenticazione (password, smartcard, LDAP, ecc.).

### Autorizzazione

Avviene dopo l’autenticazione: il sistema verifica **quali risorse e azioni** sono consentite all’utente, consultando ACL, capability o policy del sistema.

---

## 🔹 6. Protezione in modalità kernel e utente

Le CPU moderne operano in **due modalità di esecuzione**:

* **User mode:** accesso limitato, usata dai processi utente.
* **Kernel mode:** privilegi totali, usata dal sistema operativo.

Ogni **system call** implica un passaggio temporaneo in modalità kernel, seguito da un ritorno alla modalità utente.
Questo meccanismo serve a:

* proteggere la memoria del kernel e le tabelle del sistema;
* evitare che processi utente accedano direttamente all’hardware.

---

## 🔹 7. Sicurezza dei dati e cifratura

Per garantire la riservatezza delle informazioni anche in caso di furto fisico o attacco esterno, vengono adottate **tecniche di cifratura** (encryption).

### a) Cifratura simmetrica

Stesso segreto (chiave) per cifrare e decifrare.

* Esempi: AES, DES, ChaCha20.
* Veloce, ma richiede un canale sicuro per scambiare la chiave.

### b) Cifratura asimmetrica

Usa una coppia di chiavi:
**pubblica** per cifrare, **privata** per decifrare.

* Esempi: RSA, ECC.
* Fondamentale per autenticazione, firme digitali, SSH.

### c) Hash e integrità

Funzioni unidirezionali che producono una *firma digitale* dei dati:

* SHA-256, SHA-3, BLAKE2.
* Usate per verificare che i file non siano stati alterati.

### d) Cifratura del file system

* **LUKS (Linux Unified Key Setup)** o **BitLocker (Windows)**:
  cifrano intere partizioni o dischi con chiave derivata dalla password utente.

---

## 🔹 8. Audit e logging

Ogni sistema operativo mantiene **registri di log** che tracciano eventi, accessi e modifiche critiche.
Servono per:

* **analisi forense** in caso di violazioni;
* **monitoraggio di sicurezza**;
* **rilevamento di intrusioni** (IDS, SIEM).

In Linux:

* `/var/log/auth.log` → accessi e login;
* `/var/log/syslog` → eventi di sistema;
* `auditd` → log dettagliato delle system call.

---

## 🔹 9. Backup e ripristino

Nessun sistema è completamente sicuro senza **strategie di backup**.
Il backup garantisce la **disponibilità** dei dati anche dopo guasti o compromissioni.

### Tipi principali

* **Full backup:** copia completa di tutti i file.
* **Incremental:** salva solo i file modificati dall’ultimo backup.
* **Differential:** salva tutti i file modificati dal backup completo più recente.

### Buone pratiche

* Backup periodici automatizzati (cron).
* Copie su supporti esterni o cloud cifrati.
* Test regolari dei ripristini.

---

## 🧠 Mappa concettuale di sintesi

```plaintext
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
