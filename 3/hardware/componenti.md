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
La **CPU (Central Processing Unit)** è il componente che *esegue* il programma istruzione dopo istruzione. La CPU è un *chip* di silicio che contiene miliardi di transistor nonostante la dimnesione ridotta (pochi centimetri quadrati).

La CPU si inserisce fisicamente in un apposito **socket** (*alloggiamento*) presente nella scheda madre. Nell'installare la CPU sulla scheda madre, bisogna tenere in considerazione che un solo verso è quello corretto, tipicamente identificato da una *tacca* su un angolo del chip.

Esistono due tipologia di *piedinatura* delle CPU
- **PGA (Pin Grid Array)** dalla parte inferiore della CPU sporgono decine di *pideini* (*pin*) che vanno correttamente e delicatamente inseriti nel socket.
- **LGA (Land Grid Array)** dal socket fuoriscono decine di *piedini* su cui si appoggia la CPU che presenta, per ciascun piedino, un contatto metallico nella parte inferiore. LGA è lo standard adottato nelle CPU “moderne”.

:::{attention} Attenzione
Ogni tipologia di CPU deve essere installata in una scheda madre appositamente progettate. Ad esempio, CPU Intel a AMD necessitano di schede madri diverse e *chipset* appositi, tipicamente non compatibili tra loro.
:::

#### Raffreddamento della CPU
Nonostante le sue ridotte dimensioni, la CPU è uno dei componenti che consuma la maggiore quantità di energia. La massima potenza richiesta da una CPU può variare da qualche decina di Watt a oltre 100 Watt per i processori più performanti. Questa energia viene trasformata in *energia termica* che scalda il silicio. La superficie di un chip può raggiungere temperature elevate (anche oltre i 100°C) al punto da fondere il cristallo e rovinare irreparabilmente il chip.

Per evitare tale surriscaldamento è necessario **dissipare** (spostare) il calore prodotto dalla CPU. Per un adeguato risultato si usano quattro livelli di dissipamento.
1. **Pasta termica** applicata sulla parte superiore della CPU permette al calore di distribuirsi uniformemente sull'intera superficie del chip senza creare punti molto caldi e punti meno caldi.
2. **Dissipatore passivo lamellare** composto da una grigila di sottili *lamelle* metalliche sporgenti pochi centimetri perpendicolarmente alla CPU permette di allontanare il calore dalla superficie della CPU.
3. **Ventola di raffredamento della CPU** che sposta l'aria calda dal dissipatore lamellare all'interno del case.
4. **Ventola di raffredmaneto del case** che sposta l'aria calda dall'interno all'esterno del case.

:::{note} Raffreddamento a liquido
Sistemi di calcolo che generano grosse quantità di calore (ad esempio cluster multiì-CPU e multi-GPU) non possono essere raffredati con le tecniche descritte sopra che risultano insufficienti. In questi casi si usa un sistema di *raffreddamento ad acqua* in cui la spostamento di calore all'interno del case avviene mediante tubi di liquido refrigerante anziché mediante ventole. Il principio di funzionamento è lo stesso delle auto a combustione che raffreddano il motore utilizzando un liquido refrigerante ed un *radiatore* che sposta il caldo all'esterno.
:::

:::{danger} Overclock e Dissipazione
Il sistema di dissipazione viene dimensionato in base al **Thermal Design Power (TDP)** il quale indica la quantità di calore da dissipare durante la normale operatività della CPU. In caso di *overclock* la CPU consuma maggiore energia operando in un regime non considerato dal TDP. Se la dissipazione non è adeguata all'overclock, questo può determinare il blocco del sistema per surriscaldamento (se il sistema di non si bloccasse, finirebbe con il surriscoldarsi e danneggiarsi).
:::

### Memoria Centrale (RAM)

### Unità disco

### Scheda grafica

### Scheda di Rete

## Componenti Esterni

### Tastiera

### Mouse

### Monitor

### Stampante
