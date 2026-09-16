# Componenti hardware

Tra i compiti del sistemista c'è l'installazione, la configurare ed il mantenimento dell'hardware dei vari sistemi di cui è responsabile. Risulta quindi fondamentale una buona conoscenza delle tipologia di hardware e della loro gestione.

## Componenti interni

### Case

Il **case** è l'involucro che contiene i componenti interni di un calcolatore. Il case server a
- *proteggere i componenti* da agenti esterni: polvere, urti, ...
- *isolare elettricamente* la parte di interna che contiene circuiti di rame esposti
- *favorire la dissipazione* del calore generato dai componenti esterni.

Sono disponibili case di diverse forme e dimensione, diciamo che sono disponibili diversi **fattori di forma**.

:::{attention} Attenzione
Il fattore di forma del case è collegato al fattore di forma dei componenti che esso deve contenere. Questo vale sempre per alimentatore e scheda madre che non possono essere montati se non hanno fattori di forma compatibili con il case.
:::

Parte del case è anche il **sistema di raffreddamento** composto di ventole che permetto la circolazione *forzata* di area all'interno del case in modo che il calore generato dai componenti venga *dissipato* verso l'esterno del case stesso.

### Alimentatore
L'**alimentatore** (**Power Supply Unit - PSU**) trasferisce e trasforma la corrente e la tensione di rete in corrente e tensione adatta ai componenti interni. Inoltre, l'alimentatore isola tali componenti da sbalzi di tensione e corrente che potrebbero danneggiarli.

Come per il case, anche per l'alimentatore è fondamentale scegliere il corretto **fattore di forma** (in funzione del case sul quale dovrà essere montato).

Altro parametro fondamentale dell'alimentatore è la **potenza massima erogabile** che indica quanta potenza elettrica in Watt l'alimentatore e in grado di trasferire dalla rete elettrica.

Infine anche la quantità e la tipologia di **connettori** forniti da un alimentatore è un importante parametro da prendere in considerazione.

### Scheda madre

La **scheda madre** (**motherboard**) è il componente che connette e fa comunicare tutti gli altri componenti del sistema. È un componente fondamentale e le sue prestazioni determinano le prestazione dell'intera macchina.

La scheda madre viene fissata mediante viti al case ed ovviamente il fatto di forma di scheda a madre e di case devono coincidere (altrimenti il fissaggio non sarà possibile).

Oltre agli slot per connettere i vari componenti ed ai canali di comunicazione, la scheda madre contiene due importanti componenti:
- il **BIOS** tipicamente composto da un chip che contiene tutte le istruzioni necessarie ad avviare il sistema;
- il **chipset** che regola il flusso di informazione tra i vari componenti. Il chipset è solitamente suddiviso in due chip distinti detti *north bridge* e *south bridge*, il primo si occupa della comunicazione con CPU, memoria e PCI Express (dispositivi “veloci”), il secondo dei rimanenti componenti (dispositivi “lenti”).

### Processore (CPU)
La **CPU (Central Processing Unit)** è il componente che *esegue* il programma istruzione dopo istruzione. La CPU è un *chip* di silicio che contiene miliardi di transistor nonostante la dimensione ridotta (pochi centimetri quadrati).

La CPU si inserisce fisicamente in un apposito **socket** (*alloggiamento*) presente nella scheda madre. Nell'installare la CPU sulla scheda madre, bisogna tenere in considerazione che un solo verso è quello corretto, tipicamente identificato da una *tacca* su un angolo del chip.

Esistono due tipologia di *piedinatura* delle CPU
- **PGA (Pin Grid Array)** dalla parte inferiore della CPU sporgono decine di *piedini* (*pin*) che vanno correttamente e delicatamente inseriti nel socket.
- **LGA (Land Grid Array)** dal socket fuoriescono decine di *piedini* su cui si appoggia la CPU che presenta, per ciascun piedino, un contatto metallico nella parte inferiore. LGA è lo standard adottato nelle CPU “moderne”.

:::{attention} Attenzione
Ogni tipologia di CPU deve essere installata in una scheda madre appositamente progettate. Ad esempio, CPU Intel a AMD necessitano di schede madri diverse e *chipset* appositi, tipicamente non compatibili tra loro.
:::

#### Raffreddamento della CPU
Nonostante le sue ridotte dimensioni, la CPU è uno dei componenti che consuma la maggiore quantità di energia. La massima potenza richiesta da una CPU può variare da qualche decina di Watt a oltre 100 Watt per i processori più performanti. Questa energia viene trasformata in *energia termica* che scalda il silicio. La superficie di un chip può raggiungere temperature elevate (anche oltre i 100°C) al punto da fondere il cristallo e rovinare irreparabilmente il chip.

Per evitare tale surriscaldamento è necessario **dissipare** (spostare) il calore prodotto dalla CPU. Per un adeguato risultato si usano quattro livelli di dissipazione.
1. **Pasta termica** applicata sulla parte superiore della CPU permette al calore di distribuirsi uniformemente sull'intera superficie del chip senza creare punti molto caldi e punti meno caldi.
2. **Dissipatore passivo lamellare** composto da una griglia di sottili *lamelle* metalliche sporgenti pochi centimetri perpendicolarmente alla CPU permette di allontanare il calore dalla superficie della CPU.
3. **Ventola di raffreddamento della CPU** che sposta l'aria calda dal dissipatore lamellare all'interno del case.
4. **Ventola di raffreddamento del case** che sposta l'aria calda dall'interno all'esterno del case.

:::{note} Raffreddamento a liquido
Sistemi di calcolo che generano grosse quantità di calore (ad esempio cluster multi-CPU e multi-GPU) non possono essere raffreddati con le tecniche descritte sopra che risultano insufficienti. In questi casi si usa un sistema di *raffreddamento ad acqua* in cui la spostamento di calore all'interno del case avviene mediante tubi di liquido refrigerante anziché mediante ventole. Il principio di funzionamento è lo stesso delle auto a combustione che raffreddano il motore utilizzando un liquido refrigerante ed un *radiatore* che sposta il caldo all'esterno.
:::

:::{danger} Overclock e Dissipazione
Il sistema di dissipazione viene dimensionato in base al **Thermal Design Power (TDP)** il quale indica la quantità di calore da dissipare durante la normale operatività della CPU. In caso di *overclock* la CPU consuma maggiore energia operando in un regime non considerato dal TDP. Se la dissipazione non è adeguata all'overclock, questo può determinare il blocco del sistema per surriscaldamento (se il sistema di non si bloccasse, finirebbe con il surriscaldarsi e danneggiarsi).
:::

### Memoria Centrale (RAM)
Oltre che la CPU, la scheda madre possiede degli slot dedicati alla **memoria centrale**, più comunemente chiamata **memoria RAM (Random Access Machine)**. Si tratta di una memoria *volatile* (il contenuto viene perso se la memoria non è alimentata) che i programmi da eseguire e i dati che i programmi devono elaborare.

Negli anni, la tecnologia di costruzione della RAM si è evoluta.
- Static RAM (SRAM) è una tipologia di memoria usata nei primissimi (anni '60 del '900) calcolatori elettronici che utilizza porte logiche (esempio Flip-Flop) per memorizzare un bit. Oggi è utilizzata in memorie veloci come cache e registri della CPU, ma non per RAM.
- Dynamic RAM (DRAM) è una tipologia di memoria che utilizza piccole *celle di memoria* per memorizzare un bit. Ad esempio, la presenza o assenza di carica in un condensatore (fatto di silicio) rappresenta il valore 1 o 0 di un bit. Rispetto alle porte logiche usate nelle SRAM, le celle delle DRAM sono estremamente più compatte (meno silicio) ed è possibile creare memorie più ”dense” (maggior numero di bit per superficie di silicio).
- Synchronous Dynamic RAM (SDRAM)
- Double Data Rate RAM (DDR) la più recente tecnologia di sviluppo di memorie RAM, oggi giunta alla versione DDR5. Si tratta di una tecnologia di tipo SDRAM in grado di trasferire dati al doppio della velocità (*double data rate*).[^1]
- Graphics DDR (GDDR) tipologia di RAM DDR appositamente progettata per essere utilizzata nelle GPU (Graphic Processing Unit).

:::{attention} Attenzione
Le varie tecnologie di RAM richiedono degli slot specifici per ciascuna tecnologia. Anche nei casi in cui due tecnologie (es. DDR4 e DDR5) utilizzino lo stesso connettore, di norma risultano incompatibili.
:::

### Unità disco (memoria di massa)
Dal momento che la memoria centrale è *volatile*, serve una memoria che permetta di mantenere programmi e dati anche quando il sistema non è alimentato. Oggi esistono due tipologie di **memorie di massa**.

- **Disco Rigido Magnetico (HDD - Hard Disk Disk)** che utilizza dei dischi magnetici rotanti per memorizzare bit (polarità magnetica). Si tratta di una tecnologia che permette di mantenere enormi quantità di dati (alcuni TiB per ciascuna unità). Trattandosi di un sistema *meccanico* la velocità di accesso ai dati non è molto elevata (qualche centinaio di MiB al secondo).
- **Unità a Stato Solido (SDD - Solid State Disk)** che utilizza delle memorie elettroniche per memorizzare i bit. Si tratta di una tecnologia più veloce rispetto ai HDD che può raggiungere velocità di trasferimento anche di GiB per secondo.[^2]

- **Unità ottica** permettono la lettura e la scrittura su dischi ottici quali CD, DVD, Blu-ray, ... Questi dispositivi utilizzano un *laser* che rileva le variazioni di una superficie riflettente (il disco). Nei PC moderni non è comune trovare queste unità le cui funzionalità sono state sostituite da memorie esterne removibili (esempio USB Pen Drive o memorie SD).

### Scheda grafica (Graphic Card)
La **scheda grafica** (**graphic card**) rappresenta il componente che interagisce con lo schermo sul quale disegna (*render*) la scena da visualizzare (ad esempio in un gioco o nel browser). La scheda video può essere **integrata** nella scheda madre o può essere **discreta** ed inserita in un apposito slot della scheda madre (slot *PCI Express, PCIe*).

Per interagire con lo schermo, la scheda video è dotata di **porte**. Oggi sono disponibili diversi standard per le porte video.
- High-Definition Multimedia Interface (HDMI)
- DisplayPort
- Thunderbolt 
- DVI (Digital Visual Interface)
- Video Graphics Array (VGA)

#### Graphic Processing Unit (GPU)
Agli inizi degli anni 2000 nVidia (uno dei più importanti produttori di schede grafiche) ha introdotto una nuova tipologia di processori grafici chiamati *General Purpose GPU* ovvero **GPU (Graphic Processing Unit)** per il calcolo generale. Con questa novità, nVidia ha creato dispositivi che non solo permettono di *accelerare* le prestazioni grafiche, ma anche di accelerare il calcolo generico aiutando la CPU nell'esecuzione di alcuni programmi. Per eseguire il calcolo la GPU è dotata di una propria memoria di tipo GDDR (Graphics DDR).

Con l'esplosione dell'AI (*Artificial Intelligence*), le GPU sono risultate le migliori piattaforme hardware sia per il *training* di modelli di AI sia per l'*inferenza*. Oggi, le GPU nVidia rappresentano hardware indispensabile per tutte le applicazioni di intelligenza aritificiale.

:::{note} Non solo nVidia
Il concetto di GPU non oggi un'esclusiva di nVidia. GPU sono presenti integrate negli stessi chip della CPU. Ad esempio, la serie M di Apple (M1, M2, ...) contiene nello stesso chip della CPU (ARM) anche una GPU. In questi sistemi, la stessa memoria RAM utilizza dalla CPU è utilizzata anche dalla GPU, si parla di memoria *condivisa*.
:::

### Scheda di Rete

## Componenti Esterni

### Tastiera

### Mouse

### Monitor

### Stampante

---
[^1]: Il trucco che permette alle DDR di raddoppiare la velocità di trasferimento è utilizzare sia il fronte di salita che quello di discesa del clock.
[^2]: Oggi il problema è rappresentato dal tipo di connessione usata anziché il disco in sé. I dischi più veloci usano la porta PCI Express sono detti dischi NVMe. Più lenti, ma meno costosi, sono gli SSD che utilizzano il protocollo SATA.
