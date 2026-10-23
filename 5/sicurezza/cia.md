# Framework CIA

Oggi l'accesso alla rete Internet, usata da miliardi di persone, avviene principalmente utilizzando connessioni *wireless* le quali, utilizzando un *mezzo condiviso*, rendono potenzialmente visibili i dati scambiati. Un software di *sniffing* della rete, quale Wireshark (vedi figura sotto), è sufficiente per osservare tutto il *traffico di rete*, rendendo le comunicazioni visibili *in chiaro*, a meno di non *offuscare* i dati scambiati. L'intercettazione delle conversazioni, non è l'unico problema legato alla sicurezza delle reti, un amministratore ed un progettista di rete devono garantire che la rete risponda ai dei *requisiti di sicurezza* che andiamo ad analizzare in questa sezione.

```{figure} /5/img/wireshark-screenshot.png
:width: 80%

Il programma Wireshark per lo *sniffing* del trafficodi rete.
```

(triade-CIA)=
## La triade CIA

Possiamo schematizzare il problema della sicurezza nei sistemi di gestione delle informazione (ad esempio, nelle reti) con l'acronimo CIA che identifica tre *requisiti* di sicurezza.[^1]

Confidentiality (*confidenzialità* o *riservatezza*)

:   richiede che i dati scambiati
    rimangano confidenziali, cioè conosciuti solo a mittente e
    ricevente. La confidenzialità coinvolge anche la *privacy*, dati che
    non si vogliono rendere noti devono rimanere nascosti
    (confindenziali).

Integrity (*integrità*)

:   richiede che i dati che arrivano al ricevente siano
    gli stessi spediti dal mittente. Sotto questo requisito si trovano
    anche aspetti legati all'integrità del sistema (ad esempio *router*
    e *switch*).

Availability (*disponibilità*)

:   richiede che i dati e i servizi siano sempre
    disponibili a chi ha i *privilegi* di accesso. Disponibilità è
    intesa in senso ampio, se un server non è disponibile, nemmeno i
    dati che vi sono memorizzati sono disponibili.

```{figure} /5/img/alice-bob-mallory.svg
Scambio di messaggi tra Alice e Bob con Mallory che vuole sabotare la conversazione.
```

Per analizzare le problematiche che si presentano durante uno scambio di informazioni in rete, consideriamo la situazione raffigurata nella figura sopra in cui Alice e Bob vogliono scambiarsi informazioni, mentre Mallory vuole sabotare e/o origliare la conversazione Vediamo quindi quali sono i problemi e le possibili violazioni dei requisiti CIA elencati sopra.

### Violazione della confidenzialità: *eavesdropping*

```{figure} /5/img/alice-bob-eavesdropping.svg
Mallory può origliare (*eavesdrop*) la conversazione tra Alice e Bob e può anche salvare copie dei messaggi scambiati.
```

In questo caso Mallory è in grado di leggere i messaggi che Alice e Bob si scambiano. Questo è possibile se Mallory ha un dispositivo che accede alla stessa rete di Alice o alla rete di Bob o è in grado di intercettare i pacchetti che i due si scambiano (ad esempio Mallory ha installato un *malware* sul dispositivo di Bob o su un'altro dispositivo connesso alla rete da cui Bob comunica). Utilizzando un programma come Wireshark, Mallory può catturare i pacchetti che Alice e Bob si stanno scambiando e, se questi non sono *cifrati* (quindi offuscati), Mallory sarà in grado di leggerne il contenuto, quindi origliando la conversazione tra Alice e Bob.

Va considerato che Mallory può fare una copia dei pacchetti scambiati tra Alice e Bob e tentarne la decifratura *offline*. Questa operazione è utile se le informazioni scambiate hanno valore anche terminata la comunicazione (ad esempio codici e numeri di una carta di credito, documenti riservati, ...). L'utilizzo di tecniche *brut-force* per l'individuazione dei codici (*chiavi*) di cifratura può essere più facilmente ed efficacemente realizzato *offline* su pacchetti precedentemente salvati.

:::{tip} Esercizio
Discutere la *confidenzialità* nello scenario descritto sotto. Si considerino quali sono i dati che si vogliono mantenere riservati e quali sono le possibile *minacce* che possono rendere visibili (non più confidenziali) tali dati.

**Scenario** L'azienda **InCura** di occupa di assicurazioni sanitarie integrative. **InCura** possiede circa 30 dipendenti di cui metà consulenti che si recano presso i clienti o presso potenziali clienti. Ogni consulente è dotato di un dispositivo portatile (tablet o laptop) dal quale ha accesso all'intera anagrafica aziendale compresi dati sensibili su clienti (domicilio, telefono, stato di salute, ...).
:::

### Violazione dell'integrità: *tampering*

```{figure} /5/img/alice-bob-tampering.svg
Mallory può sostituire un messaggio con una versione modificata (*tampering*).

```

In questo caso Mallory è in grado di modificare il contenuto di tutti o di alcuni pacchetti che Alice e Bob si stanno scambiando. Questo è possibile, ad esempio, se Mallory ha modificato il codice di un *router* intermedio tra Alice e Bob ed è quindi in grado di sostituire i pacchetti originali con quelli appositamente creati (*forged*). La cifratura (offuscamento del contenuto) dei pacchetti aiuta, ma può non essere sufficiente. Ad esempio le parti *in chiaro* (non cifrate) come l'indirizzo IP possono essere modificate senza bisogno di decifrare il contenuto del messaggio. Inoltre, Mallory può compromettere l'integrità della comunicazione inserendo messaggi malevoli nella conversazione.


##### Autenticità e *spoofing*

```{figure} /5/img/alice-bob-mitm.svg
Mallory è in grado di frapporsi nella comunicazione tra Alice e Bob (*spoofing* e *man in the
middle*).
```

Come visto, l'integrità di un messaggio riguarda anche l'identità del mittente (ad esempio il suo indirizzo IP). Se Mallory riesce ad impersonificare il ruolo di uno tra Alice e Bob allora si parla di *spoofing* (vedi figura sopra). Il requisito di integrità richiede anche che non si possano verificare situazioni di spoofing.

Infine, l'integrità dei messaggi riguarda anche il *non ripudio* (*non-repudiation*) per cui il mittente non può negare di aver inviato un messaggio. Chiaramente se non è possibile garantire l'integrità del messaggio, il mittente può sempre ripudiare un messaggio sostenendo che è stato modificato.

### Violazione della disponibilità: *Denial of Service (DoS)*

```{figure} /5/img/alice-bob-dos.svg
Mallory è in grado di interrompere la comunicazione tra Alice e Bob.
```

In questo caso Mallory rende impossibile la comunicazione tra Alice e Bob. Questo è possibile, ad esempio, se Mallory può rendere inutilizzabile uno dei canali fisici di comunicazione. Nel caso di una comunicazione via cavo è possibile che Mallory interrompa fisicamente il collegamento, nel caso di connessioni *wireless*, Mallory può generare segnali di disturbo (chiamati *segnali di jamming*) impedendo ad Alice o Bob di utilizzare il mezzo fisico.


Molto più frequenti sono gli attacchi di tipo *Denial of Service* che Mallory può mettere in atto rendendo indisponibili dispositivi o servizi di rete, quali router o server. I dispositivi sotto attacco dispositivi vengono inondati di richieste malevoli al punti da non essere in grado di gestire le richieste legittime. Se Mallory ha la possibilità di utilizzare più dispositivi, chiamate **botnet**, l'attacco DoS combinato risulta ancora più dirompente, si parla in questo caso di *Distributed DoS (DDoS)*. Spesso le *botnet* sono composte di dispositivi infettati con *malware* per la maggior parte del tempo non fanno nulla al punto che i legittimi proprietari non sono al corrente che il proprio dispositivo è parte di una *botnet*.

#### Ransomware

Un altro attacco alla disponibilità, molto efficace e recentemente molto frequente prende il nome di **ransomware**. In questo caso Mallory utilizza tecniche di cifratura per “mettere sotto chiave” i dati utilizzati da Alice e/o da Bob rendendo quindi tali dati *indisponibili*. Successivamente Mallory richiede il pagamento di un riscatto (*ransom*), spesso in moneta non tracciabile tipo *bitcoin* per restituire i dati. 

:::{danger} Importante
Vale la pena ricordare che tale pagamento non garantisce la restituzione dei dati, al contrario, un primo pagamento segnala a Mallory che Alice e/o Bob sono disposti a pagare che potrebbe decidere di chiedere ulteriori pagamenti prima.
:::

## La sigla AAA

Per garantire la massima protezione rispetto agli attacchi descritti nella precedente sezione, è necessario che i sistemi (dispositivi, protocolli, ...) e le persone coinvolte siano gestiti in modo adeguato. Nell'ambito dei sistemi informativi ed anche nell'ambito delle reti, si è sviluppato un *framework*[^2] per le gestione riassunto dalla sigla **AAA: Authentication, Authorization, Accounting**.

### Authentication

Il primo aspetto definito dal framework AAA è l'**autenticazione** (**authentication**) che prevede il controllo di *chi* accede ai dati e o alla rete.

#### Modalità di autenticazione
Vediamo ora alcuni delle più comuni modalità di autenticazione.

Credenziali username e password

:   Ogni *utente* è identificato da un nome, solitamente una stringa;
    inoltre una seconda stringa è utilizzata come “parola d'ordine” (la
    password) che deve essere nota solo all'utente associato al
    nome. La coppia *username* e *password* rappresenta le
    *credenziali* di autenticazione.

OAuth (Single Sign On - SSO)

:   Un servizio esterno (tipici esempi sono Google, Facebook, Microsoft,
    ...) a cui si è registrati ed autenticati (ad esempio con username e
    password) si occupa di “testimoniare” l'identità. OAuth è un
    protocollo per gestire questo tipo di autenticazione. Si parla a
    volte di *Single Sign On* perché l'idea è che una volta autenticato
    (*signed on*) su un servizione (es. Google) posso accedere ad altri
    servizi.

Autenticazione Biometrica

:   Un qualche tipo parametro biometrico (impronta digitale, retina,
    voce, ...) viene utilizzato per identificare l'utente che è l'unico
    a possedere quella “lettura” biometrica.

One-Time Password (OTP)

:   Dato un nome utente da autenticare, il sistema genera una password
    temporanea che viene comunicata mediante “canali” alternativi.
    L'utente riceve ed inserisce tale password che non è più valida (si
    può usare una sola volta). Tipici canali per comunicare l'OTP sono:
    email, SMS, notifiche su dispositivi mobile, authenticator app, ...

#### Multi-Factor Authentication (MFA)

Ogni singolo metodo di autenticazione ha qualche *vulnerabilità*. Per aumentare la sicurezza è consigliabile usare più di un metodo di autenticazione, tecnica nota come **Multi-Factor Authentication** (*autenticazione a più fattori*), abbreviato in MFA.

:::{tip} Esempio
È ormai comune accedere a servizi quali posta, banca, social media e molti altri, in cui l'autenticazione mediante nome utente e password non è più sufficiente. Spesso, quindi, vi viene chiesto di “confermare la nostra identità” utilizzando un codice OTP ricevuto via mail, SMS e *notifica push* sullo smartphone. Questo è un classico esempio di autenticazione a più fattori.
:::

### Authorization

Il secondo aspetto è l'**autorizzazione** (**authorization**), che stabilisce *quali* risorse o servizi un soggetto autenticato è autorizzato a utilizzare e con *quali privilegi*. Essa viene applicata solo dopo il completamento positivo del processo di autenticazione e definisce i diritti di accesso secondo politiche di sicurezza predefinite.

### Accounting

L'ultimo aspetto del framework AAA è l'**accounting**, che consiste nella registrazione e nel monitoraggio delle attività svolte dagli utenti sulla rete. Questo meccanismo permette di tracciare l'utilizzo delle risorse, rilevare eventuali abusi e supportare attività di *audit*, fatturazione o analisi di sicurezza.

### Esempio: protocollo RADIUS

Un esempio concreto di applicazione del framework AAA è il protocollo **RADIUS** (**Remote Authentication Dial-In User Service**), un protocollo client-server ampiamente utilizzato per il controllo centralizzato degli accessi alle reti. RADIUS opera tipicamente in scenari di accesso remoto o di rete locale, dove un *Network Access Server* (NAS) delega as un server RADIUS la gestione delle operazioni di sicurezza. In questo contesto, l'**Authentication** viene utilizzata per verificare l'identità dell'utente tramite credenziali come username e password; l'**Authorization** definisce le risorse e i servizi a cui l'utente autenticato può accedere, specificando ad esempio *policy* di accesso o parametri di connessione; infine, l'**Accounting** consente di registrare le attività dell'utente, come la durata della sessione e il volume di traffico generato, supportando funzioni di monitoraggio, auditing e fatturazione.

[^1]: CIA è la sigla più utilizzata, tuttavia essa non tiene conto di
    altri requisiti quali *Authenticity* (autenticità) e
    *accountability*. @SB12

[^2]: In questo caso si tratta di un *framework concettuale* simile al
    framework introdotto con il modello ISO/OSI e differente dai
    *framework di programmazione* (ad esempio Bootstrap o Flutter).
